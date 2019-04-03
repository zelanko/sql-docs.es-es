---
title: Empezar a trabajar con el Asistente para experimentación de base de datos para las actualizaciones de SQL Server
description: Empezar a trabajar con el Asistente para experimentación de base de datos
ms.custom: ''
ms.date: 10/22/2018
ms.prod: sql
ms.prod_service: dea
ms.suite: sql
ms.technology: dea
ms.tgt_pltfrm: ''
ms.topic: conceptual
author: HJToland3
ms.author: ajaykar
ms.reviewer: douglasl
manager: craigg
ms.openlocfilehash: 7630aee7ab39f98f372af7c33f277e7272042f43
ms.sourcegitcommit: 1a4aa8d2bdebeb3be911406fc19dfb6085d30b04
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/03/2019
ms.locfileid: "58872245"
---
# <a name="get-started-with-database-experimentation-assistant"></a>Empezar a trabajar con el Asistente para experimentación de base de datos

Ayudante para la base de datos de experimentación (DEA) es una solución para los cambios de pruebas A/b en entornos de SQL Server, como las actualizaciones o los nuevos índices. DEA le ayudará a evaluar cómo se realizará la carga de trabajo en el servidor de origen (en su entorno actual) en el nuevo entorno. DEA le guiará a través de ejecución de una A o B de pruebas mediante tres pasos: 

- Capturar
- reproducción
- Análisis

Este artículo le guiará a través de estos pasos.

## <a name="capture"></a>Capturar

El primer paso de SQL Server A / B pruebas son capturar un seguimiento del servidor de origen. Normalmente, el servidor de origen es el servidor de producción. Los archivos de seguimiento capturan la carga de trabajo de consulta completa en ese servidor, incluidas las marcas de tiempo. Más adelante, este seguimiento se reproduce en los servidores de destino para el análisis. El informe de análisis proporciona información sobre la diferencia de rendimiento de la carga de trabajo entre los dos servidores de destino.

Consideraciones:

- Antes de iniciar la captura de seguimiento, asegúrese de que se realice una de las bases de datos desde el que está capturando un seguimiento.
- Un usuario DEA debe estar configurado para conectarse a la base de datos mediante la autenticación de Windows.
- Una cuenta de servicio de SQL Server requiere acceso a la ruta de acceso de archivo de seguimiento de origen.

Para capturar un seguimiento del servidor de origen:

1. En DEA, vaya a **captura todos los** seleccionando el icono de cámara en el menú izquierdo.

   ![Menú de navegación izquierdo](./media/database-experimentation-assistant-get-started/dea-get-started-leftnav.png)

1. Escriba o seleccione la siguiente información:

   - **Nombre de seguimiento**: El nombre de archivo para el nuevo archivo de seguimiento que se va a crear. Evitar un nombre de seguimiento que utiliza la convención de nomenclatura de archivos sustitución, por ejemplo, CaptureName\_NNN.
   - **Duración**: La duración de la captura.
   - **Nombre de instancia de SQL Server**: La instancia de SQL Server desde el que quiere capturar un seguimiento.
   - **Nombre de la base de datos**: El nombre de la base de datos en el equipo que ejecuta a SQL Server que desee capturar un seguimiento de. Si se deja en blanco, se captura seguimiento de todas las bases de datos en el servidor.
   - **Ruta de acceso para almacenar el archivo de seguimiento de origen en la máquina de SQL Server**: La ruta de acceso de carpeta donde desea guardar el archivo de seguimiento.

1. Asegúrese de que la base de datos de destino es una copia de seguridad. A continuación, seleccione la casilla de verificación de la base de datos.
1. Seleccione **iniciar** para iniciar la captura.

Puede ver el progreso de la captura, incluida la hora de inicio, la duración y el tiempo restante. También puede iniciar una nueva captura mientras se espera para que finalice esta captura. Cuando haya finalizado la captura, use el archivo de seguimiento de salida para iniciar la segunda fase: reproducir el archivo de seguimiento en los servidores de destino.

Para ver las preguntas comunes acerca de la captura de seguimiento, el [capturar las preguntas más frecuentes sobre](database-experimentation-assistant-capture-trace.md#frequently-asked-questions-about-trace-capture).

## <a name="replay"></a>reproducción

El segundo paso de SQL Server A / B pruebas son reproducir el archivo de seguimiento que se captura en los servidores de destino. A continuación, recopilar seguimientos amplia de las reproducciones para el análisis. 

Reproducir el archivo de seguimiento en dos servidores de destino: una que imita el servidor de origen (target1) y otra que imita el cambio propuesto (2 de destino). Las configuraciones de hardware de destino 1 y 2 de destino deben ser lo más parecidas posible para que SQL Server puede analizar con precisión el efecto de rendimiento de los cambios propuestos.

Consideraciones:

- Para ejecutar la reproducción, las máquinas deben configurarse para ejecutar seguimientos de Distributed Replay (DReplay). Para obtener más información, consulte [el programa de instalación de controlador y el cliente de Distributed Replay](https://blogs.msdn.microsoft.com/datamigration/distributed-replay-controller-and-client-setup/).
- Asegúrese de restaurar las bases de datos en los servidores de destino mediante el uso de la copia de seguridad del servidor de origen.
- Almacenamiento en caché de consulta en SQL Server puede afectar a los resultados de evaluación. Se recomienda que reinicie el servicio de SQL Server (MSSQLSERVER) en la aplicación de servicios para mejorar la coherencia en los resultados de evaluación.

Para reproducir el archivo de seguimiento:

1. En DEA, seleccione el icono de reproducción en el menú izquierdo para ir a **todas las reproducciones**. La lista de últimos reproducciones que se ejecutan durante la sesión, si existe, aparece. Para iniciar una reproducción nuevo, seleccione **reproducir nuevo**.

1. Escriba o seleccione la siguiente información:

   - **Nombre de la reproducción**: El nombre de archivo para el seguimiento de reproducción.
   - **Nombre del equipo controlador**: El nombre de la máquina del controlador de Distributed Replay.
   - **Ruta de acceso al archivo de seguimiento de origen en el controlador**: La ruta de acceso del archivo de seguimiento de origen de [capturar](#capture).
   - **Nombre de instancia de SQL Server**: El nombre de la instancia de SQL Server en el que se va a reproducir el seguimiento de origen.
   - **Ruta de acceso para almacenar el archivo de seguimiento de destino en la máquina de SQL Server**: La ruta de acceso de carpeta para el archivo de seguimiento de reproducción resultante.

1. Seleccione la casilla de verificación para restaurar la copia de seguridad desde el primer paso.

1. Seleccione **iniciar** para iniciar la reproducción. 

Puede ver el estado de la reproducción. Después de volver a reproducir el seguimiento de origen en dos de los servidores de destino, está listo para generar un informe de análisis.

Para preguntas habituales sobre reproducción, consulte el [reproducir preguntas más frecuentes sobre](database-experimentation-assistant-replay-trace.md#frequently-asked-questions-about-trace-replay).

## <a name="analysis"></a>Análisis

El último paso es generar un informe de análisis mediante la reproducción de seguimientos. El informe de análisis puede ayudarle a obtener información acerca de las implicaciones de rendimiento del cambio propuesto.

Consideraciones:

- Si faltan uno o varios componentes, aparece una página de requisitos previos con vínculos para descargas cuando intenta generar un nuevo informe de análisis (requerido conexión a internet).
- Para ver un informe que se generó en una versión anterior de la herramienta, primero debe actualizar el esquema.

Para generar un informe de análisis:

1. En el menú izquierdo, vaya a **informes de análisis**. Conéctese al equipo que ejecuta SQL Server donde se almacenan las bases de datos de informe. Aparece una lista de todos los informes en el servidor. Para crear un nuevo informe, seleccione **nuevo informe**.

1. Escriba o seleccione la información necesaria para generar un informe:

   - **Nombre del informe**: El nombre del informe de análisis para crear.
   - **Seguimiento de SQL Server de destino 1**: La ruta de acceso del archivo de seguimiento de la reproducción en el destino 1.
   - **Seguimiento de SQL Server de destino 2**: La ruta de acceso del archivo de seguimiento de la reproducción de destino 2.

1. Seleccione **iniciar** para generar el informe. El nuevo informe aparece en la parte superior de la lista. El icono junto al informe se convierte en una marca de verificación verde cuando se ha generado el informe.

Ahora, ver el informe de análisis para obtener información detallada proporcionada por su prueba A/b.

Para ver las preguntas comunes acerca de los informes de análisis, el [preguntas más frecuentes sobre análisis](database-experimentation-assistant-create-report.md#frequently-asked-questions-about-analysis-reports).

### <a name="analysis-report"></a>Informe de análisis

En la primera página del informe, se muestra información de versión y compilación para los servidores de destino en el que se ejecute el experimento. Puede usar para ajustar la confidencialidad o la tolerancia de su umbral / análisis B pruebas. De forma predeterminada, el umbral se establece en 5%. Cualquier mejora del rendimiento que es mayor o igual a % 5 se clasifica por categorías como **mejorada**. Seleccione las opciones en el menú desplegable para evaluar el informe mediante el uso de los umbrales de rendimiento diferentes.

![Umbral](https://msdnshared.blob.core.windows.net/media/2017/03/threshold.jpg)

Dos gráficos circulares muestran las implicaciones de rendimiento de la diferencia entre los dos servidores de destino para la carga de trabajo. El gráfico de la izquierda se basa en el recuento de ejecuciones. El gráfico adecuado se basa en consultas distintivas. Existen cinco categorías posibles:

- **Mejorado**:  Estadísticamente, la consulta se ejecutó mejor en 2 de destino que en el destino 1.
- **Degradado**: Estadísticamente, la consulta se ejecutó peor en 2 de destino que en el destino 1.
- **Mismo**: No hay ninguna diferencia estadística para la consulta entre destino 1 y 2 de destino.
- **No se puede evaluar**: El tamaño de muestra para la consulta es demasiado pequeño para realizar análisis estadísticos. Para A / B pruebas análisis, DEA requiere las mismas consultas con al menos 30 ejecuciones en cada destino.
- **Error**: La consulta cerrada por al menos una vez en uno de los destinos.

![Gráfico circular](./media/database-experimentation-assistant-get-started/dea-get-started-piechart.png)

Seleccione un sector para explorar en profundidad una categoría determinada y obtener las métricas de rendimiento, incluida la **no se puede evaluar** gráfico circular.

La página de exploración en profundidad para un rendimiento cambiar categoría muestra una lista de consultas de esa categoría. El **Error** página tiene tres pestañas:

- **Nuevos errores**: Errores que aparecieron en 2 de destino pero no en el destino 1.
- **Los errores existentes**: Errores que aparecieron en el destino 1 y 2 de destino.
- **Resolver errores**: Errores que aparecieron en el destino 1 pero no en 2 de destino.

   ![Página de error](./media/database-experimentation-assistant-get-started/dea-get-started-errorpage.png)

Seleccione una consulta para ir a un **resumen de comparación** página para esa consulta.

El **resumen de comparación** página muestra las estadísticas de resumen para esa consulta. El resumen incluye el número de ejecuciones, duración media, promedio de CPU, promedio de lecturas y escrituras y el recuento de errores.

![Estadísticas de resumen](./media/database-experimentation-assistant-get-started/dea-get-started-summarystats.png)

Si la consulta es un error, el **información de Error** ficha muestra más información sobre el error. El **información del Plan de consulta** ficha muestra información acerca de los planes de consulta que se usan para la consulta en el destino 1 y 2 de destino.

![Plan de consulta](./media/database-experimentation-assistant-get-started/dea-get-started-queryplan.png)

En cualquier página del informe del análisis, seleccione el **imprimir** botón en la parte superior derecha para imprimir todo lo que está visible.

## <a name="next-steps"></a>Pasos siguientes

- Para obtener información sobre cómo generar un archivo de seguimiento que tiene un registro de eventos que se producen en un servidor, consulte [capturar seguimiento](database-experimentation-assistant-capture-trace.md).

- Para obtener una introducción minutos 19 DEA y demostración, vea el vídeo siguiente:

  > [!VIDEO https://channel9.msdn.com/Shows/Data-Exposed/Introducing-the-Database-Experimentation-Assistant/player]
