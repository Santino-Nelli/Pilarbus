# Pilarbus: ecosistema móvil de transporte publico 
Proyecto Pilarbus: Planificación con Scrum, gestión de tareas y control de versiones para una aplicación de transporte publico de Pilar

## Integrantes 
- Juan Vizgarra
- Lautaro Olmedo
- Vanesa Pavia
- 

## Descripción del proyecto 
Pilarbus es una propuesta de aplicación móvil y plataforma web para consultar recorridos y la ubicación de los colectivos en tiempo real. tambien contempla funcionalidades como alertas de desvíos y envio de reclamos.

## Justificación metodológica 
El proyecto "Pilarbus" presenta características que hacen que un enfoque tradicional, no sea el más adecuado, ya que existe alta incertidumbre sobre los requisitos: las funcionalidades se irán definiendo y modificando según la retroalimentación de los usuarios beta. En este contexto, Scrum resulta la metodología ideal, porque trabaja en ciclos cortos e iterativos llamados Sprints, lo que permite incorporar cambios en cualquier momento sin alterar todo el proyecto.
A diferencia de los modelos tradicionales, donde se intenta definir todo desde el inicio y los cambios tienen costos adicionales, el flujo de trabajo continuo que propone Scrum permite entregar valor de forma progresiva, recibir comentarios y mejorar el producto paso a paso. Este se ajusta perfectamente a las necesidades del proyecto, ya que además requiere actualizaciones constantes sin interrumpir el servicio.

## Estimación de esfuerzo y costos (Ágil)
Para estimar el esfuerzo de las las funcionalidades principales de Pilarbus, se pueden utilizar técnicas ágiles como los puntos de historia y el planning poker. En lugar de medir en horas, los puntos de historia evaluan el tamaño, la complejidad, el riesgo y la incertidumbre de cada funcionalidad en relación con otras que el equipo ya conoce. Por otra parte, el Planning poker es una técnica participativa en la que cada miembro del equipo opina sobre la estimación, lo que aprovecha el conocimiento colectivo.
Este tipo de estimación es dinámica y progresiva: no pretende predecir todo desde el principio, sino refinar las estimaciones a medida que el equipo avanza y comprende mejor lo que hay que hacer. Ésto es valioso en el proyecto porque los requisitos cambian con frecuencia; si una funcionalidad se modifica, se vuelve a estimar rápidamente sin afectar a todo el plan. Asi el equipo puede ajustar el alcance y las prioridades sin perder el rumbo.

## Trabajo en ramas y pull requests
La rama principal del repositorio denominada **`Main`**, contendría los cambio revisados y validados del proyecto.
Para poder desarrollar una funcionalidad o corregir un error, el encargado de la tarea creara una rama independiente para trabajar en ella. por ejemplo: se crea la rama `feature/alertas-desvíos` y en esta se desarrollaran las notificaciones sobre cambios de recorrido para luego agregarlas a la rama principal.
Estos avances se registraran mediante commits (registros de los cambios del proyecto) con mensajes claros que describan las modificaciones realizadas.
Una vez preparado el cambio, el integrante abrirá un **Pull requests** para solicitar la incorporación al **`Main`**. este PR incluirá: 
- Una descripción del cambio y su objetivo.
- La tarjeta de trello relacionada.
- Las pruebas realizadas.
Con este mecanismo se puede hacer una revisión del trabajo antes de incorporarlo de la versión principal y mantener un registro de las deciciones que toma el equipo.

## revisión y aprobación de cambios  
Cada pull requests debe ser revisado por al menos un integrante del grupo, diferente a quien hizo el cambio. Esta persona tiene que comprobar que el cambio responda a la tarea planteada y cuente con las pruebas necesarias, en caso de encontrar errores se deben solicitar correcciones y dejar comentarios.
la incorporación a `Main` denominada **Marge** (la incorporacion de una rama a la rama principal) se permite cuando: 
- El cambio cumpla con los criterios que pide la tarea
- Las observaciones de la revisión estén resueltas
- Exista una aprobacion de otro integrante
- Los controles automaticos de build y test finalicen correctamente

## Integración Continua: CI
La integración continua permite comprobar frecuentemente los cambios y detectar errores antes de su publicación. Esta etapa incluye fases de Build y Test:

### Build: construcción 
El Build prepara la aplicación a partir del código y sus dependencias. Permite detectar problemas que impidan construir una versión ejecutable, como errores de compilación o componentes faltantes.
Un Build correcto indicaría que la aplicación pudo construirse, pero no garantizaría por sí solo que todas sus funcionalidades se comporten correctamente.

### Test: Pruebas automáticas
Los Test comprobarían comportamientos esperados de la aplicación. Para PilarBus, podrían verificar que:
- Las consultas devuelvan el recorrido de la linea seleccionada
- Una alerta de desvio se asocie a la linea correspondiente
- Un reclamo no pueda enviarse sin completar los campos obligatorios
- Los errores de conexion se gestionan de forma controlada

### Que sucedería si falla un control 
Si el build o algún test, el flujo informaría el error y el cambio no estaría habilitado para incorporarse a `Main` según las reglas propuestas.
El responsable debe revisar el resultado, corregir el problema y enviar un nuevo commit. los controles se ejecutan otra vez hasta obtener un resultado que cumpla con las condiciones.

## Entrega continua: CD y Deploy a producción 
La entrega continua permite mantener una versión valida y preparada para su publicación. 
Después de superar los controles sobre `main`, se genera una version identificable de la aplicación y se despliega en un entorno de pruebas, separado del utilizado por los pasajeros. Ahi es donde se realizan las verificaciones adicionales.
Una vez aprobada la versión por el integrante responsable de la entrega, se autoriza el Deploy a producción, es decir, su publicación en el entorno real de servicios.
La propuesta contempla una aprobación humana antes de publicar. por lo tanto se trata de entrega continua y no de despliegue automatico a produccion de todos lo cambios.

## Actualización del servicio sin interrupciones
Antes de publicar la nueva version, se comprueba que supere los controles de build y test y se verifica su funcionamiento en un entorno de pruebas.
Una vez aprobada, se realiza el deploy a producción, planificando la actualización para evitar interrupciones del servicio. Luego de publicarla se debe revisar que las funciones principales sigan funcionando correctamente. La versión anterior es guardada para poder ser recuperada ante cualquier incombeniente.

## Ejemplo de incorporacion: Alerta de desvios
1) El equipo selecciona en el Trello la tarea "implementar alertas de desvío"
2) El desarrollador crea la rama `feature/alertas-desvios`.
3) Implementa la función y agrega pruebas para comprobar que cada alerta se muestre en la linea correspondiente.
4) Registra los cambios mediante Commit y crea el Pull request hacia Main.
5) Al abrir o actualizar el Pull request, se ejecuta automáticamente el Build, que comprueba que la aplicación pueda construirse con los cambios, y los Test, verifican que la alerta aparezca en la linea correcta.
6) Otro integrante revisa le código. Si pide alguna corrección, el desarrollador corrige el problema y actualiza el pull request.
7) Cuando el revisor aprueba los cambios, se hace el marge para incorporarlo al Main.
8) Se repiten el Build y el Test sobre la versión incorporada. Si pasan, el equipo comprueba las alertas en un entorno de prueba. La entrega continua (CD) deja la version lista para publicarse.
9) antes de cada Deploy a producción, el responsable revisa que la versión que se va a publicar haya superado los controles. Si alguno falla, la publicación queda pendiente hasta corregir los errores y volver a probarla.
10) Con la publicación autorizada, el equipo pone la nueva versión a disposición de los pasajeros y comprueba que las alertas funcionen correctamente.

## Tablero de Trello
enlace:

Este documento describe como proponemos organizar el desarrollo, las tareas, responsables, estimaciones y estados del trabajo de PilarBus.






