

#  Explicación de `pipe()` en C
`pipe()` crea un **canal de comunicación** entre **dos procesos**.  
- **Un proceso escribe datos en un extremo del pipe**.  
- **Otro proceso lee esos datos desde el otro extremo**.  
- **Es unidireccional**, es decir, los datos solo fluyen en una dirección.  

**Diagrama conceptual del `pipe()`**  
```
Proceso Padre                   Proceso Hijo
-------------                   ------------
  Escribe en pipe → (fds[1]) ───► (fds[0]) → Lee del pipe
```
- `fds[1]` → Extremo de **escritura**.  
- `fds[0]` → Extremo de **lectura**.  

---

##  Código con `pipe()`
```c
#include <stdio.h>
#include <unistd.h>

int main() {
    int fds[2];  // fds[0] será para lectura, fds[1] para escritura
    pipe(fds);   // Creamos el pipe

    int pid = fork();  // Creamos un proceso hijo

    if (pid == 0) {  // Código del proceso hijo
        close(fds[0]);  // Cerramos el extremo de lectura en el hijo (no lo usamos)
        char mensaje[] = "Hola desde el hijo";
        write(fds[1], mensaje, sizeof(mensaje));  // Escribimos en el pipe
        close(fds[1]);  // Cerramos el extremo de escritura
    } else {  // Código del proceso padre
        close(fds[1]);  // Cerramos el extremo de escritura en el padre
        char buffer[100];
        read(fds[0], buffer, sizeof(buffer));  // Leemos del pipe
        printf("Padre recibió: %s\n", buffer);  // Mostramos el mensaje recibido
        close(fds[0]);  // Cerramos el extremo de lectura
    }

    return 0;
}
```


#  Explicación paso a paso

**1. Se crea un pipe**
 `pipe(fds);`  
- `fds[0]` → Se usa para **leer** datos.  
- `fds[1]` → Se usa para **escribir** datos.  
- El kernel se encarga de almacenar los datos en una **cola interna** hasta que el proceso de lectura los consuma.  


**2. Se crea un proceso hijo con `fork()`**
 `int pid = fork();`  
- Ahora hay **dos procesos separados**:  
  - **El proceso padre.**  
  - **El proceso hijo (que es una copia del padre).**  
- **Ambos procesos heredan el pipe (`fds`)**, lo que significa que pueden compartir datos.  

 **Estado después de `fork()`**  
```
Padre (PID 1001)                  Hijo (PID 1002)
-------------                     -------------
  fds[0] (lectura)                 fds[0] (lectura)
  fds[1] (escritura)               fds[1] (escritura)
```

---

**3. Cierre de extremos innecesarios**
Cada proceso **cierra el extremo del pipe que no usa**:  
- **En el hijo:**  
```c
close(fds[0]);  // No va a leer, así que cierra el extremo de lectura
```
- **En el padre:**  
```c
close(fds[1]);  // No va a escribir, así que cierra el extremo de escritura
```
Esto **evita problemas** y libera recursos del sistema.  

 **Estado después de cerrar extremos innecesarios:**  
```
Padre (PID 1001)                  Hijo (PID 1002)
-------------                     -------------
  fds[0] (lectura)   <--- Pipe ---  fds[1] (escritura)
```
- **Ahora solo hay comunicación en una dirección:**  
    - **El hijo escribe en `fds[1]`**.  
    - **El padre lee desde `fds[0]`**.  

---

 **4. El proceso hijo escribe en el pipe**
 **En el proceso hijo:**  
```c
char mensaje[] = "Hola desde el hijo";
write(fds[1], mensaje, sizeof(mensaje));
close(fds[1]);  // Cerramos el extremo de escritura después de escribir
```
- **El mensaje "Hola desde el hijo" se almacena en el pipe** (buffer interno del SO).  
- **Luego, el hijo cierra `fds[1]` porque ya no necesita escribir más.**  

---

**5. El proceso padre lee del pipe**
 **En el proceso padre:**  
```c
char buffer[100];
read(fds[0], buffer, sizeof(buffer));
printf("Padre recibió: %s\n", buffer);
close(fds[0]);  // Cerramos el extremo de lectura
```
- **El padre lee los datos que el hijo escribió en el pipe.**  
- **Muestra el mensaje recibido en la pantalla.**  

 **Salida esperada en la terminal:**  
```
Padre recibió: Hola desde el hijo
```
La comunicación se completó exitosamente.  

---

**Resumen gráfico del flujo**
1. **El padre crea un pipe.**  
2. **Se ejecuta `fork()`, creando un proceso hijo.**  
3. **El hijo cierra el extremo de lectura y escribe un mensaje en `fds[1]`.**  
4. **El padre cierra el extremo de escritura y lee el mensaje desde `fds[0]`.**  
5. **El padre imprime el mensaje en pantalla.**  

 **Diagrama del flujo de comunicación:**  
```
Proceso Hijo                            Proceso Padre
------------                            ------------
  close(fds[0]);   // No necesita leer   close(fds[1]);   // No necesita escribir
  write(fds[1], "Hola");                read(fds[0], buffer);
  close(fds[1]);   // Ya terminó         close(fds[0]);   // Ya terminó
```
Se logra la comunicación entre procesos usando `pipe()`. 

---

**¿Qué pasa si el orden de `read()` y `write()` cambia?**  
- **Si el padre intenta leer antes de que el hijo escriba**, el proceso padre se **queda esperando** (`bloqueado`) hasta que el hijo escriba.  
- **Si el hijo intenta escribir y nadie lee**, se llenará el buffer del pipe y el hijo también se **quedará esperando** (`bloqueado`).  

Por eso, siempre es importante **asegurar el orden correcto** en los procesos.  

---

**Variación: Comunicación bidireccional con dos pipes**
Si queremos que **el hijo y el padre se envíen datos entre sí**, necesitamos **dos pipes**.  

 **Diagrama de pipes bidireccional:**  
```
Pipe 1 (padre → hijo)
fds1[1] → escribe (padre)
fds1[0] → lee (hijo)

Pipe 2 (hijo → padre)
fds2[1] → escribe (hijo)
fds2[0] → lee (padre)
```
**Código simplificado:**  
```c
int fds1[2], fds2[2];
pipe(fds1);  // Pipe 1: Padre → Hijo
pipe(fds2);  // Pipe 2: Hijo → Padre

int pid = fork();

if (pid == 0) {  // Proceso hijo
    close(fds1[1]); close(fds2[0]);
    char buffer[100];
    read(fds1[0], buffer, sizeof(buffer));  
    printf("Hijo recibió: %s\n", buffer);
    write(fds2[1], "Mensaje del hijo", 16);
} else {  // Proceso padre
    close(fds1[0]); close(fds2[1]);
    write(fds1[1], "Mensaje del padre", 17);
    char buffer[100];
    read(fds2[0], buffer, sizeof(buffer));
    printf("Padre recibió: %s\n", buffer);
}
```
**Salida esperada:**  
```
Hijo recibió: Mensaje del padre
Padre recibió: Mensaje del hijo
```
Se logra comunicación en ambas direcciones.  

---
