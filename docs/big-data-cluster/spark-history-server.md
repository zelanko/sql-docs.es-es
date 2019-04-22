---
title: Depuración y diagnóstico de aplicaciones de Spark
titleSuffix: SQL Server big data clusters
description: Utilice el servidor de historial de Spark para depurar y diagnosticar aplicaciones de Spark que se ejecutan en clústeres de macrodatos de SQL Server 2019.
author: jejiang
ms.author: jejiang
ms.reviewer: jroth
manager: craigg
ms.date: 12/06/2018
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.custom: seodec18
ms.openlocfilehash: e7444a9f5bcdc480425ba02c8a068831c081b47a
ms.sourcegitcommit: 323d2ea9cb812c688cfb7918ab651cce3246c296
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/18/2019
ms.locfileid: "58860337"
---
# <a name="debug-and-diagnose-spark-applications-on-sql-server-big-data-clusters-in-spark-history-server"></a>Depuración y diagnóstico de aplicaciones de Spark en clústeres de macrodatos de SQL Server en el servidor de historial de Spark

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

Este artículo proporcionan instrucciones sobre cómo usar el servidor de historial de Spark extendido para depurar y diagnosticar aplicaciones de Spark en un clúster de macrodatos de 2019 de SQL Server (versión preliminar). Estas funcionalidades de depuración y diagnóstico están integradas en el servidor de historial de Spark y con tecnología de Microsoft. La extensión incluye datos fichas y pestaña gráfico y un diagnóstico más detallado. En la pestaña datos, los usuarios pueden comprobar los datos de entrada y salida del trabajo de Spark. En la pestaña gráfico, los usuarios pueden comprobar el flujo de datos y reproducir el gráfico del trabajo. En la pestaña de diagnóstico, pueden hacer referencia a los usuarios asimetría de datos, el desfase temporal y análisis de uso de ejecutor.

## <a name="get-access-to-spark-history-server"></a>Obtener acceso al servidor de historial de Spark

Se ha mejorado la experiencia de usuario de servidor historial de Spark de código abierto con información que incluye datos específicos del trabajo y visualización interactiva de flujos de trabajo gráfico y los datos para el clúster de macrodatos. 

### <a name="open-the-spark-history-server-web-ui-by-url"></a>Abre el sitio Web del servidor de historial Spark mediante la dirección URL de la interfaz de usuario
Abra el servidor de historial de Spark, vaya a la siguiente dirección URL, reemplace `<Ipaddress>` y `<Port>` con información específica del clúster de macrodatos. Puede hacer referencia más información: [Implementar el clúster de macrodatos de SQL Server](quickstart-big-data-cluster-deploy.md)

```
https://<Ipaddress>:<Port>/gateway/default/sparkhistory
```

La web del servidor de historial de Spark se parece a la interfaz de usuario:

![Servidor de historial de Spark](./media/apache-azure-spark-history-server/spark-history-server.png)


## <a name="data-tab-in-spark-history-server"></a>Pestaña datos de servidor de historial de Spark
Seleccione el Id. de trabajo, a continuación, haga clic en **datos** en el menú de herramienta para obtener la vista de datos.

+ Compruebe el **entradas**, **salidas**, y **las operaciones de tabla** seleccionando las pestañas por separado.

    ![Fichas de datos del servidor de historial de Spark](./media/apache-azure-spark-history-server/sparkui-data-tabs.png)

+ Copie todas las filas, haga clic en botón **copia**.

    ![Copie todas las filas](./media/apache-azure-spark-history-server/sparkui-data-copy.png)

+ Guardar todos los datos como archivo CSV, haga clic en botón **csv**.

    ![Guardar los datos como archivos CSV](./media/apache-azure-spark-history-server/sparkui-data-save.png)

+ Búsqueda, escriba palabras clave en el campo **búsqueda**, el resultado de la búsqueda mostrará inmediatamente.

    ![Buscar por palabras clave](./media/apache-azure-spark-history-server/sparkui-data-search.png)

+ Haga clic en el encabezado de columna para ordenar la tabla, haga clic en el signo más para expandir una fila para mostrar más detalles o haga clic en el signo menos para contraer una fila.

    ![Funcionalidad de la tabla de datos](./media/apache-azure-spark-history-server/sparkui-data-table.png)

+ Descargar archivo único haciendo clic en botón **descarga parcial** que colocar a la derecha, a continuación, se descarga el archivo seleccionado en un contexto local. Si el archivo no existe más, se abrirá una nueva pestaña para mostrar los mensajes de error.

    ![Descargue una fila de datos](./media/apache-azure-spark-history-server/sparkui-data-download-row.png)

+ Copiar ruta de acceso completa o relativa seleccionando el **Copiar ruta de acceso completa**, **Copiar ruta de acceso relativa** que se expande en el menú de descarga. Para archivos de almacenamiento de azure data lake, **abierto en el Explorador de Azure Storage** se iniciará el Explorador de Azure Storage. Y busque la carpeta exacta al iniciar sesión.

    ![Copiar una ruta de acceso completa o relativa](./media/apache-azure-spark-history-server/sparkui-data-copy-path.png)

+ Haga clic en el número de la tabla siguiente para navegar por páginas cuando demasiado muchas filas para mostrar en una sola página. 

    ![Página de datos](./media/apache-azure-spark-history-server/sparkui-data-page.png)

+ Mantenga el mouse sobre el signo de interrogación junto a los datos para mostrar la información sobre herramientas o haga clic en el signo de interrogación para obtener más información.

    ![Datos más información](./media/apache-azure-spark-history-server/sparkui-data-more-info.png)

+ Enviar comentarios con problemas haciendo **nos proporcione comentarios**.

    ![comentarios de Graph](./media/apache-azure-spark-history-server/sparkui-graph-feedback.png)

## <a name="graph-tab-in-spark-history-server"></a>Pestaña gráfico de servidor de historial de Spark

Seleccione el Id. de trabajo, a continuación, haga clic en **Graph** en el menú de herramienta para obtener la vista de gráfico del trabajo.

+ Comprobar información general de su trabajo, el gráfico del trabajo generado. 

+ De forma predeterminada, mostrará todos los trabajos, y se puede filtrar por **Id. de trabajo**.

    ![Id. de trabajo de gráfico](./media/apache-azure-spark-history-server/sparkui-graph-jobid.png)

+ Dejamos **progreso** como valor predeterminado. Usuario puede comprobar el flujo de datos seleccionando **lectura** o ** escrito *** en la lista desplegable de **mostrar**.

    ![visualización del gráfico](./media/apache-azure-spark-history-server/sparkui-graph-display.png)

    La visualización del nodo de gráfico en el color que se muestra el mapa térmico.

    ![mapa térmico de Graph](./media/apache-azure-spark-history-server/sparkui-graph-heatmap.png)

+ Reproducir el trabajo haciendo clic en el **reproducción** botón y detener en cualquier momento haciendo clic en el botón Detener. La presentación de la tarea en el color que se mostrará un estado diferente al reproducir:

    + Verde significa correcto: El trabajo se completó correctamente.
    + Color naranja para reintenta: Instancias de las tareas que no se pudo pero no influyen en el resultado final del trabajo. Estas tareas tenían duplicar o vuelva a intentar las instancias que pueden realizar correctamente más tarde.
    + Azul para ejecutar: Se está ejecutando la tarea.
    + Blanco para esperar u omitidos: La tarea está esperando para ejecutarse, o se ha omitido la fase.
    + Error en rojo para: Error de la tarea.

    ![muestra de color del gráfico, ejecución](./media/apache-azure-spark-history-server/sparkui-graph-color-running.png)
 
    La presentación de la fase se omitió en blanco.
    ![ejemplo de color del gráfico, omitir](./media/apache-azure-spark-history-server/sparkui-graph-color-skip.png)

    ![muestra de color del gráfico, que no se pudo](./media/apache-azure-spark-history-server/sparkui-graph-color-failed.png)
 
    > [!NOTE]
    > Se permite la reproducción de cada trabajo. Trabajo incompleto, no se admite la reproducción.


+ Desplaza el mouse para acercar/alejar el gráfico del trabajo, o haga clic en **ajustar al** para ajustarlo a la pantalla.
 
    ![zoom del gráfico para que quepa](./media/apache-azure-spark-history-server/sparkui-graph-zoom2fit.png)

+ Mantenga el mouse sobre el nodo de gráfico para ver las tareas con error de la información sobre herramientas cuando hay y haga clic en el escenario para abrir la página de la fase.

    ![información sobre herramientas del gráfico](./media/apache-azure-spark-history-server/sparkui-graph-tooltip.png)

+ En la pestaña gráfico de trabajo, fases tendrá información sobre herramientas y el icono pequeño que se muestran si tienen tareas cumplir la siguientes condiciones:
    + Asimetría de datos: tamaño de lectura de datos > tamaño de todas las tareas dentro de esta fase de lectura de datos Media * > 10 MB de tamaño de 2 y los datos leídos
    + Desfase horario: tiempo de ejecución > tiempo de ejecución promedio de todas las tareas dentro de esta fase * 2 y minutos de tiempo de ejecución 2 >

    ![icono de sesgo de gráfico](./media/apache-azure-spark-history-server/sparkui-graph-skew-icon.png)

+ El nodo de trabajo gráfico mostrará la siguiente información de cada fase:
    + ID.
    + Nombre o descripción.
    + Número total de la tarea.
    + Datos leídos: tamaño de lectura de las sumas de tamaño de entrada y orden aleatorio.
    + Escritura de datos: tamaño de escritura de las sumas de tamaño de salida y orden aleatorio.
    + Tiempo de ejecución: el tiempo transcurrido entre la hora de inicio del primer intento y la hora de finalización del último intento.
    + Recuento de filas: la suma de los registros de entrada, registros de salida, ordenar aleatoriamente los registros de lectura y mezclar los registros de escritura.
    + Progreso.

    > [!NOTE]
    > De forma predeterminada, el nodo del gráfico de trabajo mostrará la información del último intento de cada fase (excepto el tiempo de ejecución de la fase), pero durante el gráfico de reproducción de nodo muestra información de cada intento.

    > [!NOTE]
    > Para el tamaño de los datos de lectura y escritura que se utilice 1 MB = 1000 KB = 1000 * 1000 Bytes.

+ Enviar comentarios con problemas haciendo **nos proporcione comentarios**.

    ![comentarios de Graph](./media/apache-azure-spark-history-server/sparkui-graph-feedback.png)


## <a name="diagnosis-tab-in-spark-history-server"></a>Pestaña de diagnóstico en el servidor de historial de Spark
Seleccione el Id. de trabajo, a continuación, haga clic en **diagnóstico** en el menú de la herramienta para realizar el trabajo de vista de diagnóstico. La pestaña de diagnóstico incluye **asimetría de datos**, **sesgo horario**, y **análisis de uso de ejecutor**.
    
+ Compruebe el **asimetría de datos**, **sesgo horario**, y **análisis de uso de ejecutor** seleccionando las pestañas, respectivamente.

    ![Pestañas de diagnóstico](./media/apache-azure-spark-history-server/sparkui-diagnosis-tabs.png)

### <a name="data-skew"></a>Asimetría de datos
Haga clic en **asimetría de datos** ficha correspondiente se muestran tareas sesgadas según los parámetros especificados. 

+ **Especificar parámetros** -la primera sección muestra los parámetros, que se usan para detectar la asimetría de datos. La regla integrada es: Lectura de datos de tarea es mayor que tres veces el promedio de datos de tarea leer y leer los datos de la tarea están más de 10 MB. Si desea definir su propia regla para tareas sesgadas, puede elegir los parámetros, el **fase sesgada**, y **sesgar Char** sección se actualizará según corresponda. 

+ **Sesgar fase** -la segunda sección muestra las fases, que se han sesgado las tareas que cumplen los criterios especificados anteriormente. Si hay más de una tarea sesgada de una fase, la tabla de fase sesgada muestra solo la tarea más sesgada (por ejemplo, los datos más grandes de asimetría de datos). 

    ![Section2 de asimetría de datos](./media/apache-azure-spark-history-server/sparkui-diagnosis-dataskew-section2.png)

+ **Sesgar gráfico** : cuando se selecciona una fila en la tabla de la fase de sesgo, el sesgo del gráfico se muestra más detalles de las distribuciones de tareas basados en tiempo de ejecución y lectura de datos. Las tareas de la sesgados se marcan en rojo y se marcan las tareas normales en azul. Por motivos de rendimiento, el gráfico sólo muestra hasta 100 tareas de ejemplo. Los detalles de la tarea se muestran en el panel inferior derecho.

    ![Sección3 de asimetría de datos](./media/apache-azure-spark-history-server/sparkui-diagnosis-dataskew-section3.png)

### <a name="time-skew"></a>Desfase temporal
El **sesgo horario** pestaña muestra la sesgados tareas basadas en tiempo de ejecución de tareas. 

+ **Especificar parámetros** -la primera sección muestra los parámetros, que se usan para detectar el desfase temporal. Los criterios predeterminados para detectar el sesgo horario es: tiempo de ejecución de tareas es superior a tres veces promedio de tiempo de ejecución y tiempo de ejecución de tareas es superior a 30 segundos. Puede cambiar los parámetros según sus necesidades. El **fase sesgada** y **sesgar gráfico** mostrar la información de las tareas y fases correspondientes al igual que el **asimetría de datos** pestaña anterior.

+ Haga clic en **sesgo horario**, a continuación, se muestran resultados filtrados en **fase sesgada** sección según los parámetros establecidos en la sección **especificar parámetros**. Haga clic en un elemento **fase sesgada** sección, a continuación, el gráfico correspondiente está redactado en Sección3, y los detalles de la tarea se muestran en el panel inferior derecho.

    ![Section2 desfase de tiempo](./media/apache-azure-spark-history-server/sparkui-diagnosis-timeskew-section2.png)

### <a name="executor-usage-analysis"></a>Análisis de uso de ejecutor
El gráfico de uso de ejecutor visualiza el estado de asignación y ejecución del ejecutor real de trabajo de Spark.  

+ Haga clic en **análisis de uso de ejecutor**, a continuación, nos cuatro curvas de tipos sobre el uso del ejecutor de borrador. Incluyen **asignado ejecutores**, **ejecutando ejecutores**, **inactivo ejecutores**, y **instancias de ejecutor Max**. Con respecto a los ejecutores asignados, cada "Ejecutor agregado" o "Ejecutor quitado" evento aumentará o disminuirá los ejecutores asignados. Puede comprobar "Escala de tiempo del evento" en la ficha "Trabajos" para la comparación más.

    ![Pestaña de ejecutores](./media/apache-azure-spark-history-server/sparkui-diagnosis-executors.png)

+ Haga clic en el icono de color para seleccionar o anular la selección del contenido correspondiente en todos los borradores.

    ![Seleccione el gráfico](./media/apache-azure-spark-history-server/sparkui-diagnosis-select-chart.png)


## <a name="known-issues"></a>Problemas conocidos
El servidor de historial de Spark tiene los siguientes problemas conocidos:

+ Actualmente, solo funciona para el clúster de Spark 2.3.

+ Datos de entrada y salida mediante RDD no se mostrará en la pestaña datos.

## <a name="next-steps"></a>Pasos siguientes

* [Administración de recursos para un clúster Spark en HDInsight](https://docs.microsoft.com/azure/hdinsight/spark/apache-spark-resource-manager)
* [Configuración de Spark](https://docs.microsoft.com/azure/hdinsight/spark/apache-spark-settings)
