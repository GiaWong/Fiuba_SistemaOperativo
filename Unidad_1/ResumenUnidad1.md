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

📌 **Diagrama de estados de un proceso:**  
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

📌 **Diagrama de memoria de un proceso:**  
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
