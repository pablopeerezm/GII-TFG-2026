# Conclusiones

El objetivo general del proyecto consistía en diseñar y desarrollar una solución software 
integrada en Visual Tracking que permitiera el cálculo, análisis y visualización del indicador 
OEE y de sus componentes dentro de un entorno industrial. A partir del desarrollo realizado, 
puede concluirse que este objetivo se ha alcanzado de forma satisfactoria, ya que se ha 
incorporado una funcionalidad capaz de obtener, procesar y devolver al frontend la información 
necesaria para representar el rendimiento productivo de una partición concreta de una orden de 
trabajo. 

La solución desarrollada se apoya en la integración de datos teóricos y datos reales de 
ejecución. Por un lado, se utilizan datos procedentes de la planificación y configuración del 
proceso productivo, como los tiempos de ciclo teóricos, los materiales, las ejecuciones y la 
información asociada al puesto de trabajo. Por otro lado, se incorporan datos reales registrados 
durante la producción, como salidas de producción (outputs), rechazos, paradas y microparadas. 
Esta combinación permite obtener una visión más completa del estado real de la producción y 
calcular indicadores que reflejan no sólo cuánto se ha producido, sino también cómo ha ido el 
proceso respecto a lo esperado. 

En relación con el primer objetivo específico, se ha analizado el funcionamiento de 
Visual Tracking y se han identificado las fuentes de información necesarias para el cálculo del 
OEE. Este análisis ha sido especialmente importante, ya que el indicador no puede calcularse a 
partir de un único dato aislado, sino que requiere combinar información procedente de distintos 
servicios y entidades del sistema. La partición de la orden, identificada mediante el splitId, actúa 
como punto de entrada para recuperar el conjunto de datos necesarios y construir una respuesta 
coherente para el frontend.

Respecto al segundo objetivo específico, se han definido los requisitos funcionales 
necesarios para que la pestaña de rendimiento pueda mostrar la información necesaria que permita al usuario analizar y de forma clara la productividad durante la partición seleccionada. 
La estructura adoptada facilita que el frontend pueda consumir los datos de forma clara y 
representar cada bloque en el componente correspondiente. 

En cuanto al diseño de la arquitectura y del modelo de datos, la solución respeta la 
separación de responsabilidades de la aplicación. La lógica de negocio permanece en el 
backend, mientras que el frontend se encarga de solicitar los datos y representarlos visualmente 
mediante los componentes implementados. 

El cuarto objetivo específico, relacionado con la implementación de los mecanismos de 
cálculo automático del OEE y sus componentes, también se ha cumplido. La solución calcula 
los indicadores principales a partir de la información productiva disponible. Estos valores 
permiten evaluar el comportamiento de la producción desde varias perspectivas. La 
disponibilidad refleja el impacto de las paradas sobre el tiempo disponible; el rendimiento 
compara el comportamiento real con el esperado según los tiempos teóricos; la calidad relaciona 
piezas correctas con la producción total y el OEE ofrece una visión global del rendimiento 
operativo. 

Por último, en relación con el análisis temporal del rendimiento productivo, se ha 
incorporado la generación de la curva de velocidad, que permite observar la evolución de la 
producción por hora. Aunque el proyecto no ha consistido en crear un nuevo sistema 
independiente de almacenamiento histórico, sí utiliza información histórica y real ya registrada 
por Visual Tracking para obtener tendencias y facilitar la interpretación temporal de la 
producción. Esta funcionalidad resulta especialmente útil para detectar momentos concretos de 
bajo rendimiento, interrupciones o variaciones en la producción. 

En conjunto, el desarrollo realizado aporta una mejora funcional al módulo Visual 
Tracking, ya que transforma datos dispersos del sistema en información estructurada y útil para 
el usuario final. La pestaña de rendimiento no se limita a mostrar valores aislados, sino que permite interpretar el estado de una partición mediante indicadores, tiempos, producción y 
evolución temporal. 


## Discusión de resultados

Uno de los aspectos más relevantes del desarrollo ha sido la decisión de utilizar el 
splitId como punto de entrada para el cálculo de la información de rendimiento. Esta decisión 
resulta coherente con el funcionamiento de Visual Tracking, ya que permite al usuario 
(generalmente responsable de producción) analizar el funcionamiento de la mínima unidad 
divisible de una orden de trabajo, ya que una orden se divide en actividades y cada actividad se 
secuencia en particiones. 

Otro aspecto importante ha sido separar la información enviada y recibida en nuevos 
DTOs. El uso de ManufacturingInfoBySplitToCalculateDto con distintos elementos a parte del 
splitId, como fecha de inicio y fin, facilita la implementación a futuro de funcionalidades como 
filtro 
por turnos, información de la última hora… La implementación de 
ManufacturingIndexInfoBySplitDto organiza la respuesta en distintos bloques de información 
facilitando la navegación y extracción de valores en el frontend. Esta estructura mejora la 
mantenibilidad del sistema, ya que evita respuestas desordenadas o dependientes de la lógica 
interna del backend. Además, permite que el frontend pueda utilizar únicamente la información 
que necesita cada componente visual. 

Desde el punto de vista del backend, el principal reto ha sido reunir datos procedentes 
de distintas fuentes y transformarlos en indicadores comprensibles. El cálculo del OEE no 
depende únicamente de las piezas producidas, sino también de los tiempos, las paradas, los 
rechazos, las ejecuciones y los valores teóricos de referencia. Por este motivo, la solución 
coordina información de diferentes servicios y aplica una lógica de cálculo coherente. 

La integración con el frontend también ha sido un aspecto clave. Aunque el núcleo del 
proyecto se ha centrado en la parte backend del cálculo y estructuración de la información, la 
solución se ha desarrollado pensando en su consumo desde la pestaña de rendimiento. 

No obstante, el desarrollo también ha estado condicionado por las características del 
entorno existente. Al tratarse de una solución integrada en una aplicación empresarial ya 
desarrollada, no se partía de una arquitectura desde cero, sino que ha sido necesario adaptarse a 
los servicios, entidades, contratos y criterios técnicos definidos previamente por la empresa. 
Esto ha supuesto una limitación en algunos aspectos, pero también ha permitido trabajar en un 
contexto realista. 

En general, los resultados obtenidos muestran que la solución cumple con el propósito 
de transformar datos productivos en indicadores útiles para la toma de decisiones. El trabajo no 
solo ha requerido implementar métodos de cálculo, sino también comprender el dominio 
industrial, interpretar la estructura de VT y diseñar una comunicación adecuada y eficiente entre 
frontend y backend.  

## Evaluación cuantitativa de la mejora aportada por la solución

Con el fin de valorar si la solución desarrollada supone una mejora respecto a la forma 
anterior de consultar la información de rendimiento, se plantea una evaluación basada en la 
utilidad percibida por el usuario. 

Para evaluar esta mejora, se propone utilizar un cuestionario breve dirigido a 
responsables de producción (los usuarios que interactúan con esta pestaña en la fase de 
producción). 

El cuestionario se basa en una escala de valoración del 1 al 5, donde 1 representa una 
valoración muy baja y 5 una valoración muy alta. Los criterios evaluados se centran en la 
utilidad de la pestaña rendimiento, la claridad de la información, la utilidad de la curva de 
velocidad, la utilidad de las gráficas de barras y la utilidad de la tabla de indicadores. 

Además de la valoración numérica, el cuestionario incluye una pregunta abierta 
opcional para recoger propuestas de mejora, permitiendo al usuario añadir posibles 
ampliaciones a implementar en la pestaña de VT. 


## Futuras líneas de actuación
A partir del desarrollo realizado, una de las principales recomendaciones es mantener la 
separación de responsabilidades entre las distintas capas de la aplicación. La lógica de 
obtención, procesamiento y cálculo de la información de rendimiento debe permanecer en el 
backend, mientras que el frontend debe centrarse en solicitar los datos y representarlos de forma 
clara para el usuario. Esta separación facilita el mantenimiento de la solución, evita duplicidades 
y permite que futuras ampliaciones puedan incorporarse sin alterar de forma innecesaria la 
estructura general del sistema. 

Una posible línea de evolución sería ampliar el nivel de análisis más allá de una 
partición concreta. En el desarrollo actual, el cálculo se realiza a partir del splitId, lo que permite 
obtener una visión detallada de la partición, pero no permite visualizar los datos de forma 
general de toda una orden o separadas por las distintas actividades. 

Desde el punto de vista de análisis temporal, se podría implementar en el frontend un 
botón para filtrar de forma temporal, filtrando por última hora o turnos, utilizando así las fechas 
de inicio y fin añadidas al DTO de entrada para la realización del cálculo. 

Otra mejora interesante es evolucionar la curva de velocidad incorporando distintos 
niveles temporales, permitiendo al usuario elegir si desea ver las unidades fabricadas por horas, 
minutos, segundos, turnos, días… 

Otra futura línea de trabajo sería ampliar la pestaña de rendimiento con funcionalidades 
orientadas a la toma de decisiones, como la definición de umbrales o alertas cuando el OEE o 
sus indicadores se sitúen por debajo de un valor objetivo. Esta evolución permitiría que la 
pestaña de rendimiento no sea solo un panel de consulta, sino un alertador para detectar 
desviaciones en el proceso productivo. 

Por último, se podría permitir exportar los datos calculados a un fichero externo en 
formato pdf o excell, lo que facilitaría la generación de informes o el seguimiento de resultados.

En definitiva, la solución desarrollada constituye una base funcional sobre la que 
pueden incorporarse nuevas capacidades de análisis. El trabajo realizado permite realizar y 
estructurar información clave de rendimiento a nivel de partición, respetando la arquitectura 
existente de VT y las indicaciones de la empresa. A partir de esta base, futuras ampliaciones 
podrían orientarse hacia un análisis más completo, configurable e interactivo del rendimiento 
productivo.
