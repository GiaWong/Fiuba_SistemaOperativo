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

---

### Entonces queda claro que:  
- **Un proceso es un programa en ejecución.**  
- **Tiene su propia memoria y recursos (PID, memoria, archivos abiertos).**  
- **Puede cambiar de estado (Listo, Ejecutando, Esperando, Terminado).**  
- **El kernel se encarga de gestionarlo (crearlo, pausarlo, terminarlo).**  
- **Los procesos pueden comunicarse entre sí mediante pipes o señales.**  

**Ejemplo práctico:**  
Cada pestaña de tu navegador es un **proceso separado**, para que si una falla, no cierre todo el navegador.  

---


# File Descriptors y Process Table 
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

📌 **Comprobación en C**  
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

---