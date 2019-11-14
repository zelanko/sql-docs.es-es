---
title: Introducción a Asistente para experimentación con bases de datos
description: Asistente para experimentación con bases de datos (DEA) es una solución de prueba A/B para los cambios en entornos SQL Server, como actualizaciones o nuevos índices.
ms.date: 10/22/2018
ms.prod: sql
ms.prod_service: dea
ms.suite: sql
ms.technology: dea
ms.tgt_pltfrm: ''
ms.topic: conceptual
author: HJToland3
ms.author: ajaykar
ms.reviewer: mathoma
ms.custom: seo-lt-2019
ms.openlocfilehash: 43f8c6bff909716bdd85a798dfd4e5a7431e31af
ms.sourcegitcommit: d00ba0b4696ef7dee31cd0b293a3f54a1beaf458
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/13/2019
ms.locfileid: "74056711"
---
# <a name="get-started-with-database-experimentation-assistant-sql-server"></a>Introducción a Asistente para experimentación con bases de datos (SQL Server)

Asistente para experimentación con bases de datos (DEA) es una solución de prueba A/B para los cambios en entornos SQL Server, como actualizaciones o nuevos índices. DEA le ayuda a evaluar cómo realizará la carga de trabajo en el servidor de origen (en su entorno actual) en el nuevo entorno. DEA le guía a través de la ejecución de una prueba A/B realizando tres pasos: 

- Capturar
- Reproducción
- Análisis

Este artículo le guiará a través de estos pasos.

## <a name="capture"></a>Capturar

El primer paso de las pruebas A/B SQL Server es capturar un seguimiento en el servidor de origen. El servidor de origen suele ser el servidor de producción. Los archivos de seguimiento capturan toda la carga de trabajo de consultas en ese servidor, incluidas las marcas de tiempo. Más adelante, este seguimiento se reproduce en los servidores de destino para su análisis. El informe de análisis proporciona información sobre la diferencia en el rendimiento de la carga de trabajo entre los dos servidores de destino.

Consideraciones:

- Antes de iniciar la captura de seguimiento, asegúrese de hacer una copia de seguridad de las bases de datos desde las que va a capturar un seguimiento.
- Un usuario de DEA debe estar configurado para conectarse a la base de datos mediante la autenticación de Windows.
- Una cuenta de servicio de SQL Server requiere acceso a la ruta de acceso del archivo de seguimiento de origen.
- Para que DEA determine si el rendimiento de una consulta se ha mejorado o degradado, dicha consulta debe ejecutarse al menos 15 veces durante el período de captura.  

Para capturar un seguimiento en el servidor de origen:

1. En DEA, vaya a **todas las capturas** seleccionando el icono de cámara en el menú de la izquierda.

   ![Menú de navegación izquierdo](./media/database-experimentation-assistant-get-started/dea-get-started-leftnav.png)

1. Escriba o seleccione la siguiente información:

   - **Nombre de seguimiento**: el nombre de archivo del nuevo archivo de seguimiento que está creando. Evite un nombre de seguimiento que use la Convención de nomenclatura de archivos de sustitución incremental, por ejemplo, CaptureName\_NNN.
   - **Duration**: la duración de la captura.
   - **SQL Server nombre de instancia**: la instancia de SQL Server de la que desea capturar un seguimiento.
   - **Nombre**de la base de datos: el nombre de la base de datos del equipo en el que se ejecuta SQL Server el que desea capturar un seguimiento. Si se deja en blanco, el seguimiento se captura de todas las bases de datos en el servidor.
   - **Ruta de acceso para almacenar el archivo de seguimiento de origen en SQL Server máquina**: la ruta de acceso de la carpeta donde desea guardar el archivo de seguimiento.

1. Asegúrese de que se realiza una copia de seguridad de la base de datos de destino. A continuación, active la casilla base de datos.
1. Seleccione **iniciar** para iniciar la captura.

Puede ver el progreso de la captura, incluida la hora de inicio, la duración y el tiempo restante. También puede iniciar una nueva captura mientras espera a que finalice esta captura. Una vez finalizada la captura, use el archivo de seguimiento de salida para iniciar la segunda fase: reproducir el archivo de seguimiento en los servidores de destino.

Para preguntas comunes sobre la captura de seguimiento, consulte las [preguntas más frecuentes sobre capturas](database-experimentation-assistant-capture-trace.md#frequently-asked-questions-about-trace-capture).

## <a name="replay"></a>Reproducción

El segundo paso de las pruebas A/B de SQL Server es reproducir el archivo de seguimiento capturado en los servidores de destino. A continuación, recopile extensas trazas de las reproducciones para su análisis. 

Reproduce el archivo de seguimiento en dos servidores de destino: uno que imita el servidor de origen (destino 1) y otro que imita el cambio propuesto (destino 2). Las configuraciones de hardware de destino 1 y destino 2 deben ser lo más parecidas posible, por lo que SQL Server puede analizar con precisión el impacto en el rendimiento de los cambios propuestos.

Consideraciones:

- Para ejecutar la reproducción, los equipos deben estar configurados para ejecutar los seguimientos de Distributed Replay (DReplay). Para obtener más información, consulte [controlador de Distributed Replay y configuración de cliente](https://blogs.msdn.microsoft.com/datamigration/distributed-replay-controller-and-client-setup/).
- Asegúrese de restaurar las bases de datos en los servidores de destino mediante la copia de seguridad del servidor de origen.
- El almacenamiento en caché de consultas en SQL Server puede afectar a los resultados de la evaluación. Se recomienda reiniciar el servicio de SQL Server (MSSQLSERVER) en la aplicación de servicios para mejorar la coherencia en los resultados de la evaluación.

Para reproducir el archivo de seguimiento:

1. En DEA, seleccione el icono de reproducción en el menú de la izquierda para ir a **todas las reproducciones**. Aparece la lista de las reproducciones anteriores que se ejecutan durante la sesión, si existe. Para iniciar una nueva reproducción, seleccione **nueva reproducción**.

1. Escriba o seleccione la siguiente información:

   - **Nombre de reproducción**: nombre de archivo del seguimiento de reproducción.
   - **Nombre del equipo del controlador**: nombre del equipo del controlador de Distributed Replay.
   - **Ruta de acceso al archivo de seguimiento de origen en el controlador**: la ruta de acceso del archivo de seguimiento de origen de la [captura](#capture).
   - **SQL Server nombre de instancia**: el nombre de la instancia de SQL Server en la que se va a reproducir el seguimiento de origen.
   - **Ruta de acceso para almacenar el archivo de seguimiento de destino en SQL Server máquina**: la ruta de acceso de la carpeta para el archivo de seguimiento de reproducción resultante.

1. Active la casilla para restaurar la copia de seguridad desde el primer paso.

1. Seleccione **iniciar** para iniciar la reproducción. 

Puede ver el estado de la reproducción. Después de reproducir el seguimiento de origen en ambos servidores de destino, está listo para generar un informe de análisis.

Para preguntas comunes sobre la reproducción, consulte las [preguntas más frecuentes](database-experimentation-assistant-replay-trace.md#frequently-asked-questions-about-trace-replay)sobre la reproducción.

## <a name="analysis"></a>Análisis

El último paso es generar un informe de análisis mediante los seguimientos de reproducción. El informe de análisis puede ayudarle a obtener información sobre las implicaciones de rendimiento del cambio propuesto.

Consideraciones:

- Si faltan uno o más componentes, aparecerá una página de requisitos previos con vínculos para descargas al intentar generar un nuevo informe de análisis (se requiere conexión a Internet).
- Para ver un informe generado en una versión anterior de la herramienta, primero debe actualizar el esquema.

Para generar un informe de análisis:

1. En el menú de la izquierda, vaya a **informes de análisis**. Conéctese al equipo que ejecuta SQL Server donde almacena las bases de datos de informes. Aparece una lista de todos los informes del servidor. Para crear un nuevo informe, seleccione **nuevo informe**.

1. Escriba o seleccione la información necesaria para generar un informe:

   - **Nombre del informe**: nombre del informe de análisis que se va a crear.
   - **Seguimiento de destino 1 SQL Server**: ruta de acceso del archivo de seguimiento que se va a reproducir en el destino 1.
   - **Seguimiento del destino 2 SQL Server**: ruta de acceso del archivo de seguimiento que se va a reproducir en el destino 2.

1. Seleccione **iniciar** para generar el informe. El nuevo informe aparece en la parte superior de la lista. El icono situado al lado del informe se convierte en una marca de verificación verde cuando se genera el informe.

Ahora, vea el informe de análisis para obtener información detallada proporcionada por la prueba A/B.

Para obtener preguntas comunes sobre los informes de análisis, vea las [preguntas más frecuentes sobre análisis](database-experimentation-assistant-create-report.md#frequently-asked-questions-about-analysis-reports).

### <a name="analysis-report"></a>Informe de análisis

En la primera página del informe, se muestra la versión y la información de compilación de los servidores de destino en los que se ejecutó el experimento. Puede usar umbral para ajustar la sensibilidad o la tolerancia del análisis de prueba A/B. De forma predeterminada, el umbral se establece en el 5%. Cualquier mejora en el rendimiento mayor o igual que el 5% se clasifica como **mejorada**. Seleccione opciones en el menú desplegable para evaluar el informe con distintos umbrales de rendimiento.

![Umbral](https://msdnshared.blob.core.windows.net/media/2017/03/threshold.jpg)

Dos gráficos circulares demuestran las implicaciones de rendimiento de la diferencia entre los dos servidores de destino de la carga de trabajo. El gráfico izquierdo se basa en el recuento de ejecuciones. El gráfico de la derecha se basa en consultas distintas. Existen cinco categorías posibles:

- **Mejorado**: estadísticamente, la consulta se ejecutó mejor en el destino 2 que en el destino 1.
- **Degradado**: estadísticamente, la consulta se ejecutó peor en el destino 2 que en el destino 1.
- **Igual**: no hay ninguna diferencia estadística para la consulta entre el destino 1 y el destino 2.
- **No se puede evaluar**: el tamaño de la consulta es demasiado pequeño para el análisis estadístico. Para el análisis de pruebas A/B, DEA requiere que las mismas consultas tengan al menos 30 ejecuciones en cada destino.
- **Error**: la consulta ha dado error al menos una vez en uno de los destinos.

![Gráfico circular](./media/database-experimentation-assistant-get-started/dea-get-started-piechart.png)

Seleccione un segmento para explorar en profundidad una categoría determinada y obtener las métricas de rendimiento, incluida la **no se puede evaluar** el segmento del gráfico circular.

En la página de exploración en profundidad de una categoría de cambio de rendimiento se muestra una lista de las consultas de esa categoría. La página de **error** tiene tres pestañas:

- **Nuevos errores**: errores que aparecían en el destino 2 pero no en el destino 1.
- **Errores existentes**: errores que aparecían en el destino 1 y el destino 2.
- **Errores resueltos**: errores que aparecían en el destino 1 pero no en el destino 2.

   ![Página de error](./media/database-experimentation-assistant-get-started/dea-get-started-errorpage.png)

Seleccione una consulta para ir a una página de **Resumen de comparación** para esa consulta.

La página **Resumen de comparación** muestra las estadísticas de Resumen de la consulta. El resumen incluye el número de ejecuciones, la duración media, la CPU media, las lecturas y escrituras medias y el recuento de errores.

![Estadísticas de Resumen](./media/database-experimentation-assistant-get-started/dea-get-started-summarystats.png)

Si la consulta es una consulta de error, en la pestaña **información de error** se muestra más información sobre el error. La pestaña **información del plan de consulta** muestra información sobre los planes de consulta que se usan para la consulta en el destino 1 y el destino 2.

![Plan de consulta](./media/database-experimentation-assistant-get-started/dea-get-started-queryplan.png)

En cualquier página del informe de análisis, seleccione el botón **Imprimir** de la esquina superior derecha para imprimir todo lo que esté visible.

## <a name="next-steps"></a>Pasos siguientes

- Para obtener información sobre cómo generar un archivo de seguimiento que tenga un registro de eventos que se producen en un servidor, consulte [Capture Trace](database-experimentation-assistant-capture-trace.md).

- Para obtener una introducción de 19 minutos a DEA y demostraciones, vea el siguiente vídeo:

  > [!VIDEO https://channel9.msdn.com/Shows/Data-Exposed/Introducing-the-Database-Experimentation-Assistant/player]
