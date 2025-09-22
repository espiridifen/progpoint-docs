Bienvenido al manual de Progpoint. Aquí encontrarás todo lo necesario para entender el uso de la aplicación y las funcionalidades que tiene
# Empezando con Progpoint

La última versión de Progpoint está accesible desde [su página web](https://progpoint.espi.top/).

> [!NOTE] Compilar en local
>
> Si se quiere, se puede compilar desde el repositorio principal para su ejecución en local.
>
> Para la compilación, se requiere como mínimo la versión de NodeJS 22.13.1 y la versión de npm 10.9.2. Dentro de la carpeta progpoint-app, se necesitan ejecutar los siguientes comandos:
> ```
> npm install
> npm run dev
> ```

Una vez iniciada la aplicación, se nos mostrará la ventana de Agent Blueprints en vacío.
# Las interfaces

## Agent Blueprints

Puedes añadir nuevos nodos arrastrándolos desde los acordeones de la derecha, y puede seleccionar qué Plano de Agente modificar con el selector de arriba a la derecha. El buscador de la esquina superior izquierda te permite seleccionar qué plano de agente editar, o si se quiere crear un plano de agente nuevo.

Para diseñar los planos, se han de arrastrar nodos básicos y de estadística al plano de nodos, y conectándolos entre ellos para formar diseños de progresión. Las instancias de agente calcularán sus estadísticas a partir de los valores que le lleguen a los nodos de estadísticas. Si hay varios nodos de la misma estadística en el plano, el valor final de esa estadística será la suma de todos sus nodos de estadística.


> [!WARNING] Errores conocidos
> Es posible que algunos nodos de estadísticas se dupliquen o tripliquen. Si al instanciar agentes ves valores que no te cuadran con tu diseño, borra los nodos estadística del plano de agente relacionado y colócalos de nuevo.

### Acordeón de Nodos básicos

Acordeón donde se incluyen los nodos básicos. Con un plano abierto, se pueden arrastrar a la zona del mapa de nodos para crear nodos nuevos:
- **Nodo Nota**: Un nodo con un cuadro de texto en el que escribir notas y apuntes sobre el plano. Todos los planos de agentes nuevos tienen un nodo de nota en el que te anima a arrastrar nodos de los acordeones.
- **Nodo Parámetro**: Simboliza uno de los parámetros definidos en el acordeón de parámetros. Usado para servir de entrada a nodos de función o de matemáticas para realizar cálculos.
- **Nodo de Matemáticas**: Define un cálculo (suma, resta, multiplicación o división) entre dos nodos de entrada, devolviendo el resultado como salida.
- **Nodo Función**: Simboliza una función previamente definida en el diseñador de funciones, recibiendo un valor de entrada para X y devolviendo el valor de esa función.
### Acordeón de Estadísticas

Acordeón donde se incluyen todas las estadísticas definidas en el proyecto. Se pueden arrastrar a la zona del mapa de nodos para crear instancias de estadística en el plano de agente abierto. Si hay varios nodos de la misma estadística en el plano, el valor de esa estadística para ese plano será la suma de todos los nodos. También se pueden crear, modificar y borrar estadísticas, así como definir su mutabilidad.

### Acordeón de Parámetros

Acordeón que aparece con un plano de agente seleccionado. Incluye un botón para crear parámetros nuevos. También se encuentran aquí todos los parámetros creados para el plano seleccionado, así como los valores que se les da por defecto al crear una instancia nueva.

## Diseñador de Funciones

En esta interfaz, puedes crear funciones matemáticas. En el selector de la izquierda puedes ver las funciones que has creado, así como crear funciones nuevas. Para la función selecionada, puedes escribir en la caja de texto superior izquierda qué forma debe tomar. Progpoint acepta funciones simples de una variable, y si la función es aceptable aparecerá una previsualización en la gráfica de debajo.

## Instanciador de Agentes

En esta interfaz, puedes utilizar los planos de agente previamente diseñados para crear instancias de agente para utilizar en el simulador. Con el buscador de la parte superior, puedes buscar instancias de agente por nombre.

Para cada instancia de agente, se pueden modificar los siguientes valores:

- **Parámetros**: Todos los parámetros empiezan con los valores iniciales asignados en el Diseñador, pero puedes modificarlos a tu gusto para cada instancia.
- **Acciones de Agente**: Puedes añadir acciones a la instancia para que las utilice en el simulador. El agente realizará acciones en orden de asignación, intentando realizar la acción más alta, y bajando por la lista si no tiene los requerimientos para lanzarla.
- **Otras acciones**: Puedes modificar el plano de donde viene la instancia de agente, duplicarla y borrar la instancia si lo necesitas.

## Diseñador de Acciones

En esta interfaz puedes diseñar las acciones que utilizan las instancias de agentes en el simulador. Cuenta con un buscador de acciones, que funciona de la misma manera que el que se encuentra en el Instanciador. Cada acción está definida por los siguientes valores:

- **Estadística de coste**: La estadística que se consumirá al lanzar la habilidad.
- **Coste**: El valor que consume la acción al usarse. Puede ser positiva, negativa o 0.
- **Calculadores**: Factores numéricos que indican la efectividad de la acción, p.ej el daño que realiza. Para cada calculador, se tiene que determinar:
	- **Origen**: Agente origen de la estadística ya sea el agente actor o el agente objetivo
	- **Estadística**: Estadística que da el valor a la función cálculo.
	- **Función**: Función cálculo.
	- **Tipo**: Determina si el resultado de este calculador de efectividad es aditivo o multiplicativo en respecto a los demás.


> [!NOTE] Sobre los calculadores
> Los calculadores se calculan en orden de creación, de arriba hacia abajo. El valor inicial de la acción antes de ningún calculador es 0, así que ningún calculador multiplicativo modificará el valor hasta el primer calculador aditivo.

## Simulador

Dentro de la interfaz de simulador puedes definir y crear nuevas simualciones. Al crear una simulación, tienes que definir las siguientes propiedades:

- **Estadística de HP**: La estadística que determina si un agente está incapacitado y no puede seguir combatiendo.
- **Orden de turno**: Decide si el turno se decide de manera aleatoria o si se ordenan por el valor en una estadística.

Una vez creada la simulación, se le tienen que asignar agentes a los equipos aliados y enemigos y se les crea reglas de simulación.


> [!IMPORTANT] Reglas de simulación.
> Las reglas de simulación son lo que definen las iteraciones de las simulaciones. Por cada regla de simulación, se realizan 50 combates.

Las reglas de simulación tienen los siguientes componentes:
- **Objetivos**: Los agentes a los que hace efecto la regla
- Parámetro: El parámetro que modifica la regla. Todos los **agentes** objetivos deben tener el parámetro para que este sea seleccionable
- **Rango**: Rango numérico por el que pasa la regla.
- **Incremento**: Valor que aumenta el parámetro en cada iteración.

Una vez se tiene preparada la simulación, haz click en Batch Simulation para simular. Los resultados aparecerán abajo una vez terminen.


> [!TODO] Sobre la simulación
> Al hacer click en Batch Simulation, la UI de la aplicación deja de responder. Ahora mismo, si abres la consola (generalmente con F12) puedes ver el progreso de la simulación. En siguientes actualizaciones se añadirá una confirmación del progreso de la simulación
