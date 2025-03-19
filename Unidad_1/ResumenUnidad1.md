# **Cómo entenderlo fácilmente al Sistema Operativo**  
Imagina que tu computadora es un teatro:  
- **El sistema operativo** es el director de escena. Se encarga de coordinar todo lo que sucede: luces, sonido, actores y efectos especiales.  
- **El hardware** (procesador, memoria, disco, etc.) es el escenario, donde ocurre la acción.  
- **Las aplicaciones** (navegador, juegos, editores de texto) son los actores que siguen las instrucciones del director.  

El sistema operativo:  
- **Asigna recursos** (quién usa el procesador, cuánta memoria se le da a cada programa).  
- **Facilita la comunicación** entre los programas (por ejemplo, copiando y pegando entre aplicaciones).  
- **Abstrae el hardware**, es decir, hace que no te importe si usas un disco SSD o HDD, un mouse USB o Bluetooth, porque el sistema operativo lo maneja todo por vos.  

### **Un ejemplo práctico**  
Cuando abrís un navegador para ver un video, el SO se encarga de:  
 * Permitir que el navegador acceda a Internet.  
 * Administrar la memoria y el procesador para que el video se reproduzca sin cortes.  
 * Coordinar el sonido con los parlantes.  

Así, sin que lo notes, el sistema operativo está funcionando en segundo plano para que todo marche bien. 

Entonces de forma correctamente definida se entiende que
un **sistema operativo (SO)** es el software que controla y administra el hardware de una computadora, permitiendo que los programas se ejecuten sin que tengan que preocuparse por los detalles técnicos del hardware



### **Requisitos clave de un Sistema Operativo**  
Un sistema operativo debe cumplir con tres requisitos fundamentales para que los programas funcionen bien y no interfieran entre sí:  

## 1) Multiplexación (Compartir recursos)

 **¿Qué significa?**  
Multiplexación significa que el sistema operativo **distribuye los recursos** (procesador, memoria, disco, etc.) entre varios programas al mismo tiempo.  
 
Imaginá que el procesador es un **chef en una cocina** y los programas son diferentes **platos que hay que preparar**.  
- El chef no puede cocinar todo a la vez, así que alterna entre las tareas (corta verduras, fríe, hierve agua) y **parece que está haciendo todo al mismo tiempo**.  
- Así funciona el procesador: el SO hace que los programas usen la CPU por turnos tan rápidos que parece que todo se ejecuta simultáneamente.  

**Ejemplo técnico (CPU y Memoria)**  
- El SO asigna **tiempo de CPU** a cada proceso, haciendo que se ejecuten por turnos en milisegundos (esto se llama **planificación de procesos**).  
- También divide la memoria RAM para que cada programa tenga su propio espacio y no interfiera con otros.  

**Sin multiplexación:** Un solo programa podría usar todo el sistema, dejando a los demás sin recursos.  
**Con multiplexación:** Todos los programas reciben una parte justa de los recursos y pueden ejecutarse sin problemas.  



## 2) Aislamiento (Protección entre programas)  
 **¿Qué significa?**  
El SO **evita que un programa interfiera con otro** o con el sistema. Esto previene que errores o virus dañen toda la computadora.  

Imagina que en un **examen**, cada estudiante tiene su propio banco y espacio.  
- Si alguien intenta espiar o copiar, el profesor lo impide.  
- Así funciona el SO: cada programa tiene su propia área protegida y no puede acceder a la memoria de otro.  

**Ejemplo técnico**  
- Cada programa tiene su propio **espacio de memoria virtual**, lo que significa que no puede leer o escribir en la memoria de otro programa.  
- Si un programa falla, el SO lo **cierra sin afectar a los demás**.  
- Los sistemas operativos modernos usan **permisos y privilegios** para evitar que los programas accedan a archivos o partes del sistema sin autorización.  

**Sin aislamiento:** Un programa con errores podría borrar datos de otros programas o incluso del sistema.  
**Con aislamiento:** Los programas funcionan de manera independiente y segura.  


## 3) Interacción (Comunicación entre procesos)
**¿Qué significa?**  
El SO permite que los programas **se comuniquen entre sí** de manera controlada para compartir información o coordinar tareas.  
  
Pensá en dos personas que trabajan juntas en una empresa y necesitan pasarse información.  
- Si se comunican bien (por email o chat), pueden trabajar juntas sin problemas.  
- Si no tienen una forma de comunicarse, cada una haría su parte sin coordinación y sería un caos.  

 **Ejemplo técnico**  
- El SO ofrece mecanismos como **pipes, sockets y memoria compartida** para que los procesos puedan enviarse datos.  
- Ejemplo clásico:  
  - **Un programa descarga un archivo** y otro programa lo **lee y lo abre** automáticamente.  
  - Esto es posible porque el SO permite que se pasen información.  

**Sin interacción:** Los programas trabajarían de manera aislada, sin poder compartir datos.  
**Con interacción:** Se pueden integrar y coordinar mejor.  

---

### Recordá siempre:  
- **Multiplexación:** El SO **comparte los recursos** entre programas sin que uno bloquee a los demás.  
- **Aislamiento:** Cada programa tiene su propio espacio protegido **para evitar que interfieran entre sí**.  
- **Interacción:** Permite que los programas **se comuniquen de forma segura** para trabajar en conjunto.  

---

### ¿Qué es un proceso?
Un **proceso** es un **programa en ejecución**. Es decir, cuando abrís una aplicación (como un navegador o un editor de texto), el sistema operativo **crea un proceso** para ese programa.  

**Ejemplo:**  
- Un archivo de Word guardado en tu disco no es un proceso, es solo un archivo.  
- Cuando lo abrís, el SO **crea un proceso** para ejecutarlo en la memoria.  

**Diferencia entre Programa y Proceso:**  
- **Programa** → Código en un archivo (estático, no está en ejecución).  
- **Proceso** → El programa cuando se está ejecutando (dinámico, usa CPU y memoria).  

### ¿Dónde se ejecutan los procesos?
Los procesos se ejecutan en **User-Land**, pero piden ayuda al **Kernel-Land** *[ver resumen unidad 2]*  para hacer operaciones avanzadas como leer archivos, conectarse a Internet, etc.  

**Ejemplo:**  
- Un navegador necesita cargar una página. Como no puede acceder directamente a la red, le pide al kernel que lo haga por él.  
- Para eso usa **llamadas al sistema** (**syscalls**), como `open()`, `read()`, `write()`.  



### Características de un proceso 
- **Tiene su propia memoria** (espacio de direcciones).  
- **Se ejecuta de forma independiente**, pero puede comunicarse con otros procesos.  
- **Cada proceso tiene un identificador único** llamado **PID** (**Process ID**).  
- **Puede crear procesos hijos** usando `fork()`.  
- **Puede terminar su ejecución voluntaria o involuntariamente** (error, cierre forzado, etc.).  



### ¿Cómo funciona un proceso? (Ciclo de vida)
Un proceso pasa por **varios estados** durante su vida:  

1. **Nuevo (New)** → El proceso está siendo creado.  
2. **Listo (Ready)** → Está esperando su turno para usar la CPU.  
3. **Ejecutando (Running)** → La CPU está ejecutando sus instrucciones.  
4. **Esperando (Waiting)** → Se pausa porque espera un recurso (como leer un archivo).  
5. **Terminado (Terminated)** → Finaliza su ejecución y libera recursos.  

**Ejemplo:**  
- Abrís un navegador (**Nuevo → Listo**).  
- Cuando la CPU lo ejecuta (**Running**), ves la ventana en pantalla.  
- Si está cargando una página, queda en **Waiting** mientras recibe los datos de Internet.  
- Cuando cerrás el navegador, pasa a **Terminated** y libera la memoria.  

 **Diagrama de estados de un proceso:**  
```
   [Nuevo] ---> [Listo] ---> [Ejecutando] ---> [Terminado]
                      \----> [Esperando] -----/
```  



### Componentes de un proceso  
Un proceso tiene varias partes:  

-  **Código (Text Segment)** → Contiene el programa en sí.  
-  **Datos (Data Segment)** → Variables globales y datos inicializados.  
-  **Heap** → Espacio de memoria dinámico para variables que se crean en tiempo de ejecución (`malloc()`).  
-  **Stack** → Almacena variables locales y llamadas a funciones.  
-  **Registros de CPU** → Contienen datos temporales y el contador de instrucciones (PC, que dice qué línea de código se ejecuta).  
- **File Descriptors** → Referencias a archivos abiertos por el proceso.  

 **Diagrama de memoria de un proceso:**  
```
 +-------------------+
 | Código           |  ← Código del programa
 +-------------------+
 | Datos            |  ← Variables globales
 +-------------------+
 | Heap             |  ← Crece hacia abajo (memoria dinámica)
 +-------------------+
 | Stack            |  ← Crece hacia arriba (memoria de funciones y variables locales)
 +-------------------+
```


### Comportamiento de un proceso 

- **Creación de un proceso:**  
  - Se usa la syscall `fork()` para crear un **proceso hijo**.  
  - Ambos procesos (padre e hijo) ejecutan el mismo código, pero tienen PIDs diferentes.  

- **Ejecución:**  
  - El SO decide **cuándo y cuánto tiempo** ejecuta cada proceso.  
  - Si hay muchos procesos, usa un **planificador** para distribuir el tiempo de CPU.  

- **Comunicación entre procesos:**  
  - Los procesos pueden **compartir información** usando **pipes, memoria compartida o señales**.  

- **Terminación:**  
  - Un proceso puede **terminar voluntariamente** (`exit()`) o ser **terminado por otro proceso** (`kill(pid)`).  
  - Cuando un proceso termina, su entrada en la **Process Table** se libera.  


### Ejemplo práctico en C 
```c
#include <stdio.h>
#include <stdlib.h>
#include <unistd.h>

int main() {
    printf("Soy un proceso con PID: %d\n", getpid());
    
    int pid = fork(); // Creamos un proceso hijo
    
    if (pid == 0) {  
        printf("Soy el proceso hijo con PID: %d\n", getpid());
    } else {  
        printf("Soy el proceso padre con PID: %d y mi hijo es: %d\n", getpid(), pid);
    }

    return 0;
}
```
 **En la Salida:**  
```
Soy un proceso con PID: 12345  
Soy el proceso padre con PID: 12345 y mi hijo es: 12346  
Soy el proceso hijo con PID: 12346  
```
Aquí se ve cómo el proceso padre crea un **proceso hijo**, y ambos imprimen su propio PID.  



### Entonces queda claro que:  
- **Un proceso es un programa en ejecución.**  
- **Tiene su propia memoria y recursos (PID, memoria, archivos abiertos).**  
- **Puede cambiar de estado (Listo, Ejecutando, Esperando, Terminado).**  
- **El kernel se encarga de gestionarlo (crearlo, pausarlo, terminarlo).**  
- **Los procesos pueden comunicarse entre sí mediante pipes o señales.**  

**Ejemplo práctico:**  
Cada pestaña de tu navegador es un **proceso separado**, para que si una falla, no cierre todo el navegador.  


## File Descriptors y Process Table 
Ahora vamos a ver dos conceptos clave en la gestión de procesos:  

- **File Descriptor (FD)** → Maneja archivos y recursos en un proceso.  
- **Process Table** → Es la estructura del kernel que almacena información de cada proceso.  


### File Descriptors (FD)  
**¿Qué es un File Descriptor?**  
Un **File Descriptor (FD)** es un número entero que el **sistema operativo asigna a un archivo o recurso** cuando un proceso lo abre.  
- Es como un "ticket" o "identificador" para acceder al recurso.  
- No solo sirve para archivos, sino también para **sockets, pipes, dispositivos de entrada/salida (I/O)**, etc.  
 
Imaginá que entrás a un cine . Cuando comprás un boleto, te asignan un número de asiento.  
- **El cine** → Es el sistema operativo.  
- **El asiento** → Es el archivo o recurso.  
- **El número de asiento (FD)** → Es el identificador que usás para acceder al asiento.  

Así funciona un FD: cuando un programa abre un archivo, el SO le da un número (File Descriptor) para que lo use.  



### ¿Cómo funcionan los File Descriptors? 
Cada proceso tiene una **File Descriptor Table** que guarda todos los archivos y recursos abiertos por ese proceso.  

 **File Descriptors estándar**  
Cada proceso tiene **tres FD iniciales** que siempre existen:  
| FD | Nombre | Descripción |
|----|--------|------------|
| 0  | **stdin** | Entrada estándar (teclado) |
| 1  | **stdout** | Salida estándar (pantalla) |
| 2  | **stderr** | Salida de errores estándar (pantalla) |

Si ejecutás en la terminal:  
```bash
echo "Hola" > salida.txt
```
 **¿Qué hace esto?**  
1. `echo "Hola"` → Escribe "Hola" en **stdout (FD = 1)**.  
2. `>` → Redirige la salida **de stdout a un archivo**.  
3. `salida.txt` → Se asigna a un nuevo **File Descriptor** en la File Descriptor Table del proceso.  

- **Con esto, stdout en lugar de imprimir en pantalla, escribe en el archivo**  

 **Comprobación en C**  
```c
#include <stdio.h>
#include <unistd.h>
#include <fcntl.h>

int main() {
    int fd = open("salida.txt", O_CREAT | O_WRONLY, 0644);
    dup2(fd, 1);  // Redirigimos stdout (FD=1) al archivo

    printf("Este texto se guardará en salida.txt\n");
    close(fd);
    return 0;
}
```
- **Aquí `stdout` ya no imprime en pantalla, sino en `salida.txt`!**  



### Process Table (Tabla de Procesos)  
**¿Qué es la Process Table?**  
Es una **estructura del kernel** que **almacena información sobre todos los procesos activos** en el sistema.  

**¿Para qué sirve?**  
El sistema operativo usa esta tabla para:  
- Identificar cada proceso (**PID**).  
- Asignar recursos como **memoria, CPU y archivos abiertos**.  
- Saber en qué **estado** está cada proceso (**listo, ejecutando, esperando, terminado**).  

 **¿Cómo funciona?**  
Cada vez que se ejecuta un programa, el SO:  
1. **Crea una nueva entrada en la Process Table.**  
2. **Asigna un PID (Process ID).**  
3. **Le da recursos (memoria, CPU, archivos abiertos).**  
4. **Lo agrega a la lista de procesos en ejecución.**  

 **Ejemplo visual de Process Table**  
| PID | Nombre | Estado | Memoria | File Descriptors |
|-----|--------|--------|---------|-----------------|
| 1001 | Chrome | Running | 120MB | 3 archivos abiertos |
| 1002 | VSCode | Waiting | 200MB | 5 archivos abiertos |
| 1003 | Terminal | Ready | 50MB | 2 archivos abiertos |

---

### Relación entre File Descriptors y Process Table 
**¿Cómo se conectan?**  
Cada **proceso** tiene su propia **tabla de File Descriptors**, y esta tabla es administrada dentro de la **Process Table** del sistema.  

**Ejemplo:**  
1. Abrís **tres archivos** en un editor de texto → Se crean **tres File Descriptors**.  
2. Cada uno se almacena en la **File Descriptor Table** del proceso.  
3. El proceso tiene una entrada en la **Process Table** con esos FD asociados.  

 **Diagrama de relación**  
```
Process Table  
┌───────────────┐  
│ PID = 1001    │  → File Descriptor Table  
│ Estado: Run   │  ┌───────────────┐  
│ Memoria: 120MB│  │ FD 0 → stdin  │  
│ FD Table:     │  │ FD 1 → stdout │  
│               │  │ FD 2 → stderr │  
│               │  │ FD 3 → archivo.txt │  
└───────────────┘  └───────────────┘  
```
 **Así es como el SO gestiona archivos y procesos juntos.**  



### Acomodando los conceptos queda:  
- **File Descriptor (FD):**  
  - Número que identifica archivos abiertos por un proceso.  
  - Permite acceder a **archivos, sockets, pipes y dispositivos I/O**.  
  - Cada proceso tiene su propia **File Descriptor Table**.  

- **Process Table:**  
  - **Estructura del kernel** que almacena información de **todos los procesos activos**.  
  - Guarda datos como **PID, memoria usada, estado y File Descriptors abiertos**.  
  - Es usada por el sistema operativo para **gestionar y planificar procesos**.  


### System Calls más importantes
Los system calls permiten a los programas solicitar servicios del sistema operativo.


## `fork()` – Crear un nuevo proceso  
 **¿Qué hace?**  
`fork()` crea un **proceso hijo** idéntico al proceso padre, pero con un **nuevo PID**. Ambos procesos ejecutan el mismo código, pero con PIDs diferentes.  

 **Para entenderlo mejor imaginá: Clonar un chef en la cocina**  
- Imagina que hay **un solo chef** en un restaurante, cocinando platos.  
- De repente, el chef **clona una copia exacta de sí mismo**. Ahora hay **dos chefs trabajando al mismo tiempo**, pero con pequeñas diferencias (uno puede empezar a hacer postres mientras el otro sigue con los platos principales).  

 **Ejemplo en C**  
```c
#include <stdio.h>
#include <unistd.h>

int main() {
    int pid = fork();  // Se crea un proceso hijo

    if (pid == 0) {  
        printf("Soy el proceso hijo con PID: %d\n", getpid());
    } else {  
        printf("Soy el proceso padre con PID: %d y mi hijo es: %d\n", getpid(), pid);
    }

    return 0;
}
```
 **Salida esperada:**  
```
Soy el proceso padre con PID: 1234 y mi hijo es: 1235  
Soy el proceso hijo con PID: 1235  
```
Se crean dos procesos: el padre y el hijo, cada uno con su propio PID.

## `wait()` – Esperar a que termine un proceso hijo  
 **¿Qué hace?**  
`wait()` **hace que el proceso padre espere** hasta que su proceso hijo termine.  

**Para entenderlo mejor imaginá: Un padre esperando a su hijo en la escuela**  
- Un padre deja a su hijo en la escuela y no puede irse hasta que el niño salga de clases.  
- **El padre (proceso principal) espera al hijo (proceso secundario) antes de continuar.**  

 **Ejemplo en C**  
```c
#include <stdio.h>
#include <stdlib.h>
#include <sys/wait.h>
#include <unistd.h>

int main() {
    int pid = fork();

    if (pid == 0) {  // Proceso hijo
        printf("Proceso hijo (PID %d) ejecutándose...\n", getpid());
        sleep(2);
        printf("Proceso hijo terminado.\n");
        exit(0);
    } else {  // Proceso padre
        printf("Esperando a que el hijo termine...\n");
        wait(NULL);  // Espera a que el hijo termine
        printf("El proceso hijo ha terminado.\n");
    }

    return 0;
}
```
 **Salida esperada:**  
```
Esperando a que el hijo termine...  
Proceso hijo (PID 1235) ejecutándose...  
Proceso hijo terminado.  
El proceso hijo ha terminado.  
```
El proceso padre no continúa hasta que el hijo termina.



## `exec(filename, argv)` – Ejecutar un nuevo programa en el mismo proceso 
**¿Qué hace?**  
`exec()` **reemplaza el proceso actual con otro programa**.  

**Para entenderlo mejor imaginá: Cambiar de ropa en lugar de clonarte**  
- `fork()` es como **clonar una persona**.  
- `exec()` es como **quitarte la ropa y ponerte otra completamente diferente**. Sigues siendo la misma persona, pero te ves distinto.  
- **El proceso no cambia su PID, pero su contenido es completamente nuevo.**  

 **Ejemplo en C – Ejecutar `ls -l` dentro del proceso actual**  
```c
#include <stdio.h>
#include <unistd.h>

int main() {
    char *args[] = {"ls", "-l", NULL};  // Comando a ejecutar
    printf("Ejecutando ls -l...\n");
    execvp("ls", args);

    // Si execvp() funciona correctamente, esta línea nunca se ejecuta
    printf("Esto no debería imprimirse.\n");
    return 0;
}
```
 **Salida esperada:**  
```
Ejecutando ls -l...  
(total de archivos en el directorio)  
```
El proceso original desaparece y es reemplazado por `ls -l`. 



## `exit()` – Terminar un proceso 
 **¿Qué hace?**  
`exit()` finaliza un proceso y devuelve un código de salida.  

**Para entenderlo mejor imaginá: Cerrar sesión en una computadora**  
- Cuando terminas de usar la PC, **cierras sesión** y liberas los recursos.  
- Un proceso hace lo mismo con `exit()`: **libera la memoria y notifica al SO que terminó.**  

**Ejemplo en C**  
```c
#include <stdio.h>
#include <stdlib.h>

int main() {
    printf("Este proceso va a terminar ahora.\n");
    exit(0);
}
```
**Salida esperada:**  
```
Este proceso va a terminar ahora.
```
El proceso termina correctamente y libera los recursos.



## `kill(pid)` – Enviar una señal a un proceso (como terminarlo)  
 **¿Qué hace?**  
`kill(pid, SIGTERM)` envía una señal para **terminar un proceso específico**.  

**Para entenderlo mejor imaginá:Un árbitro sacando una tarjeta roja en un partido**  
- Si un jugador (proceso) **se porta mal**, el árbitro (SO) **le da una tarjeta roja (señal) y lo expulsa (mata el proceso)**.  

 **Ejemplo en C – Terminar un proceso hijo**  
```c
#include <stdio.h>
#include <stdlib.h>
#include <unistd.h>
#include <signal.h>

int main() {
    int pid = fork();

    if (pid == 0) {  // Proceso hijo
        printf("Proceso hijo ejecutándose (PID %d)\n", getpid());
        while (1);  // Bucle infinito
    } else {  // Proceso padre
        sleep(2);
        printf("Terminando proceso hijo...\n");
        kill(pid, SIGTERM);  // Mata al hijo
    }

    return 0;
}
```
 **Salida esperada:**  
```
Proceso hijo ejecutándose (PID 1234)  
Terminando proceso hijo...  
```
El proceso padre envía una señal para matar al hijo. 



## `pipe()` – Comunicación entre procesos  
 **¿Qué hace?**  
`pipe()` crea un **canal de comunicación unidireccional** entre dos procesos.  

 **Para entenderlo mejor imaginá: Un tubo de mensajes**  
- Imagina dos habitaciones separadas.  
- Hay **un tubo** por el que puedes enviar mensajes de una habitación a otra.  
- Un proceso escribe en un extremo del **pipe**, y el otro proceso lo lee en el otro extremo.  

 **Ejemplo en C**  
```c
#include <stdio.h>
#include <unistd.h>

int main() {
    int fds[2];
    pipe(fds);  // Crear un pipe

    int pid = fork();

    if (pid == 0) {  // Proceso hijo
        close(fds[0]);  // Cierra lectura
        char mensaje[] = "Hola desde el hijo";
        write(fds[1], mensaje, sizeof(mensaje));  // Escribe en el pipe
        close(fds[1]);  
    } else {  // Proceso padre
        close(fds[1]);  // Cierra escritura
        char buffer[100];
        read(fds[0], buffer, sizeof(buffer));  // Lee mensaje
        printf("Padre recibió: %s\n", buffer);
        close(fds[0]);  
    }

    return 0;
}
```
 **Salida esperada:**  
```
Padre recibió: Hola desde el hijo
```
El hijo escribe en el pipe y el padre lo lee.  
 
## Para entender el comportamiento de `dup()` y `dup2()` – imaginemos El buzón de cartas   

Imaginá que en un edificio hay **tres buzones de correo** donde llegan cartas:  
-  **Buzón 0** → Recibe las cartas que la gente envía (Entrada estándar – `stdin`).  
-  **Buzón 1** → Envía las cartas que se envían normalmente (Salida estándar – `stdout`).  
-  **Buzón 2** → Recibe cartas con quejas o problemas (Salida de errores – `stderr`).  

Ahora, imagina que queremos hacer **copias o redirigir estos buzones** a otro lugar.  

---

###  `dup()` – Hacer una copia automática de un buzón  
 `dup(fd)` **duplica un buzón en otro vacío automáticamente**. Ejemplo:  
- Tienes el **buzón 1** (`stdout`) donde normalmente se dejan cartas.  
- Quieres hacer una **copia de ese buzón**, pero el **cartero elige automáticamente el primer buzón vacío** para la copia.  

- **Código en C**  
```c
int nuevo_fd = dup(1);  // Copia stdout en el primer FD libre
```
- **Ejemplo real:**  
  - **El SO encuentra el primer buzón vacío** (ejemplo: `FD = 3`).  
  - Ahora **todo lo que envíes a `FD 1` también se podrá enviar a `FD 3`**.  

 
Antes de `dup(1)`:  
```
FD 0 → stdin  (teclado)
FD 1 → stdout (pantalla)
FD 2 → stderr (pantalla)
FD 3 → (vacío)
```
Después de `dup(1)`, ahora `FD 3` también es `stdout`:  
```
FD 0 → stdin  (teclado)
FD 1 → stdout (pantalla)
FD 2 → stderr (pantalla)
FD 3 → stdout (pantalla)
```
Ambos FD apuntan a la pantalla, y los dos sirven para escribir allí. 

 **Ejemplo en C:**  
```c
#include <stdio.h>
#include <unistd.h>

int main() {
    int fd_copia = dup(1);  // Copia stdout (FD 1) en el primer FD libre
    printf("Este mensaje va a stdout (pantalla)\n");
    write(fd_copia, "Este mensaje también va a stdout\n", 34);
    return 0;
}
```
 **Salida esperada en la terminal:**  
```
Este mensaje va a stdout (pantalla)
Este mensaje también va a stdout
```
Ambos FD (`1` y `fd_copia`) apuntan a la pantalla.  



###  `dup2()` – Copiar un buzón en un número específico 
 `dup2(old_fd, new_fd)` **duplica un FD pero en un número específico**. Ejemplo: 
- Tienes el **buzón 1 (`stdout`)**, pero ahora **quieres que el buzón 5 reciba la misma información**.  
- **Con `dup2(1, 5)`, ahora `FD 5` también actúa como `stdout`**.  
- **Si `FD 5` ya estaba en uso, se borra antes de redirigirlo**.  

 
Antes de `dup2(1, 5)`:  
```
FD 0 → stdin  (teclado)
FD 1 → stdout (pantalla)
FD 2 → stderr (pantalla)
FD 5 → archivo.txt
```
Después de `dup2(1, 5)`, ahora `FD 5` apunta a la pantalla:  
```
FD 0 → stdin  (teclado)
FD 1 → stdout (pantalla)
FD 2 → stderr (pantalla)
FD 5 → stdout (pantalla)
```
Ahora `FD 5` también actúa como `stdout` y los mensajes que iban a `FD 1` pueden ir a `FD 5`.  

 **Ejemplo en C – Redirigir `stdout` a un archivo**  
```c
#include <stdio.h>
#include <fcntl.h>
#include <unistd.h>

int main() {
    int fd = open("output.txt", O_CREAT | O_WRONLY | O_TRUNC, 0644);

    dup2(fd, 1);  // Ahora stdout (FD 1) se dirige a output.txt

    printf("Este mensaje se guardará en output.txt\n");  // Se escribe en el archivo, no en pantalla

    close(fd);
    return 0;
}
```
 **Salida esperada en `output.txt` (no en pantalla):**  
```
Este mensaje se guardará en output.txt
```
Ya no se imprime en la pantalla, sino en el archivo.  

---

###  Diferencias clave entre `dup()` y `dup2()`
| **Función** | **¿Qué hace?** | **Ejemplo** |
|------------|---------------|------------|
| `dup(fd)` | Duplica `fd` en el **primer número disponible**. | `dup(1) → 3` |
| `dup2(fd, 5)` | Duplica `fd` en `5` (cierra `5` si ya estaba en uso). | `dup2(1, 5) // Redirige stdout a 5` |

---

### Analogía Final – Comparando `dup()` y `dup2()`**
| **Función** | **Analogía (Buzón de cartas)** |
|------------|----------------------------------|
| `dup(fd)` | Copias una carta a otro buzón, pero **el cartero elige el buzón vacío** más cercano. |
| `dup2(fd, 5)` | Copias una carta a **un buzón específico** (si el buzón `5` tenía cartas, las destruye antes). |

---

### En conclusion:
- `dup(fd)` → **Copia un FD al primer número libre disponible.**  
- `dup2(fd, new_fd)` → **Copia un FD en `new_fd` específicamente, reemplazándolo si ya estaba en uso.**  
- **Se usan mucho en redirecciones de entrada/salida en procesos.**  

 **Ejemplo real:**  
Si ejecutás en la terminal:  
```bash
ls -l > salida.txt 2>&1
```
- **Equivalente en C:**  
```c
int fd = open("salida.txt", O_CREAT | O_WRONLY, 0644);
dup2(fd, 1);  // stdout → salida.txt
dup2(fd, 2);  // stderr → salida.txt
close(fd);
```
Redirige stdout y stderr a `salida.txt`.  

---

