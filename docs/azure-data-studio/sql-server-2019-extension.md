---
title: Extensión de SQL Server 2019 (versión preliminar)
titleSuffix: Azure Data Studio
description: Extensión de SQL Server 2019 (versión preliminar) para Azure Data Studio
ms.custom: seodec18
ms.date: 09/11/2019
ms.reviewer: alayu; sstein
ms.prod: sql
ms.technology: azure-data-studio
ms.topic: conceptual
author: yualan
ms.author: alayu
ms.openlocfilehash: 3d47ea0bc1c905516504c25e3a1f05ca5b74c28d
ms.sourcegitcommit: dacf6c57f6a2e3cf2005f3268116f3c609639905
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 09/11/2019
ms.locfileid: "70878615"
---
# <a name="sql-server-2019-extension-preview"></a>Extensión de SQL Server 2019 (versión preliminar)

La extensión de SQL Server 2019 (versión preliminar) proporciona compatibilidad en versión preliminar con las nuevas características y herramientas que se distribuyen para [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)]. Esto incluye compatibilidad en versión preliminar con [clústeres de macrodatos de SQL Server 2019](../big-data-cluster/big-data-cluster-overview.md), una [experiencia de cuadernos](../big-data-cluster/notebooks-guidance.md) integrada y un [Asistente para crear tablas externas](../relational-databases/polybase/data-virtualization.md?toc=/sql/toc/toc.json) de PolyBase.

## <a name="install-the-sql-server-2019-extension-preview"></a>Instalación de la extensión de SQL Server 2019 (versión preliminar)

Para instalar la extensión de SQL Server 2019 (versión preliminar) descargue e instale el archivo .vsix asociado.

1. Descargue el archivo .vsix de la extensión de SQL Server 2019 (versión preliminar) en un directorio local:

   |Plataforma|Descargar|Fecha de la versión|Versión
   |:---|:---|:---|:---|
   |Windows|[.vsix](https://go.microsoft.com/fwlink/?linkid=2103613)|11 de septiembre de 2019 |0.16.0
   |macOS|[.vsix](https://go.microsoft.com/fwlink/?linkid=2103612)|11 de septiembre de 2019 |0.16.0
   |Linux|[.vsix](https://go.microsoft.com/fwlink/?linkid=2103709)|11 de septiembre de 2019 |0.16.0

1. En Azure Data Studio, elija **Install Extension from VSIX Package** (Instalar extensión desde el paquete VSIX) en el menú **Archivo** y seleccione el archivo .vsix descargado.

1. Elija **Sí** cuando se le pida que confirme la instalación y espere a que aparezca la notificación que le indique que la instalación se ha realizado correctamente.

1. Seleccione **Recargar** para habilitar la extensión (solo es necesario la primera vez que se instala una extensión).

1. Después de recargar, la extensión instalará las dependencias. El progreso, que podría tardar varios minutos, puede verse en la ventana Salida.

1. Una vez finalizada la instalación de las dependencias, cierre y vuelva a abrir Azure Data Studio. El tipo de conexión **SQL Server big data cluster** (Clúster de macrodatos de SQL Server) no estará disponible mientras no reinicie Azure Data Studio.

## <a name="changes-in-release-016"></a>Cambios en la versión 0.16
* Asistente para crear tablas externas:
  * Se ha mejorado el control de errores al cargar tablas y vistas en la página de asignación de objetos.

## <a name="changes-in-release-015"></a>Cambios en la versión 0.15
* Asistente para crear tablas externas:
  * Se redujo el tiempo necesario para cargar la información de tabla y columna en la página de asignación de objetos.
  * Se corrigió un error al cargar las credenciales con ámbito de base de datos existentes en la página de detalles de la conexión.
* Asistente para la creación de una tabla externa a partir de archivos .csv:
  * Se aumentó el tamaño de ejemplo predeterminado que se usa para el análisis de PROSE.

## <a name="changes-in-release-0141"></a>Cambios en la versión 0.14.1
* Compatibilidad con el origen de datos CTP 3.1.

## <a name="changes-in-release-0121"></a>Cambios en la versión 0.12.1

* En esta versión, se ha quitado el tipo de conexión del **clúster de macrodatos de SQL Server**. Todas las funcionalidades que antes estaban disponibles en la conexión del clúster de macrodatos de SQL Server ahora están disponibles en la conexión de SQL Server.
* La exploración de HDFS se encuentra en la carpeta **Data Services**.
* En el caso de los cuadernos, PySpark y otros kernels de macrodatos funcionan cuando se conectan a la instancia maestra de SQL Server en el clúster de macrodatos de SQL Server.
* Asistente para crear tablas externas:
  * Compatibilidad con la creación de una tabla externa mediante el origen de datos externos existente.
  * Mejoras de rendimiento en el asistente.
  * Control mejorado de los nombres de objeto con caracteres especiales (en algunos casos, provocaban errores en el asistente).
  * Mejoras de confiabilidad para la página de asignación de objetos.
  * Se han quitado las bases de datos del sistema ("DWConfiguration", "DWDiagnostics", "DWQueue") de la lista desplegable de bases de datos.
  * Compatibilidad para establecer el nombre del objeto con formato de archivo externo en el Asistente para **crear tablas externas a partir de archivos CSV**.
  * Se ha agregado un botón de actualización a la primera página del Asistente para **crear tablas externas a partir de archivos CSV**.

## <a name="release-notes-v0110"></a>Notas de la versión (v0.11.0)

* La compatibilidad con Jupyter Notebook (en concreto, con los kernels de Python3 y Spark) se ha pasado a Azure Data Studio. Esta extensión ya no es necesaria para poder usar cuadernos.
* Varias correcciones de errores en los asistentes para datos externos:
  * Las asignaciones de tipo Oracle se han actualizado para que coincidan con los cambios incluidos en SQL Server 2019 CTP 2.3.
  * Se ha corregido un problema que hacía que se perdiesen los nuevos esquemas introducidos en los controles de asignación de tablas.
  * Se ha corregido un problema que hacía que la comprobación de un nodo de base de datos en las asignaciones de tabla no verificara todas las tablas y vistas.


## <a name="release-notes-v0102"></a>Notas de la versión (v0.10.2)
### <a name="sql-server-2019-support"></a>Compatibilidad con SQL Server 2019
Se ha actualizado la compatibilidad con SQL Server 2019. Al conectarse a una instancia de clúster de macrodatos de SQL Server, aparecerá una nueva carpeta _Data Services_ en el árbol del explorador. Dispone de puntos de inicio para acciones como abrir un nuevo cuaderno en la conexión, enviar trabajos de Spark y trabajar con HDFS. Tenga en cuenta que, para algunas acciones como _crear datos externos_ en un archivo o carpeta de HDFS, se debe instalar la extensión de _SQL Server 2019 (versión preliminar)_ .

### <a name="notebook-support"></a>Compatibilidad con Notebook
En esta versión hemos realizado actualizaciones considerables en la interfaz de usuario de Notebook. Nuestro objetivo consistía en facilitar la lectura de los cuadernos que se comparten con usted. Esto conllevaba, entre otras cosas, quitar todos los cuadros de contorno alrededor de las celdas (a menos que se seleccionen o que se mueva el puntero por encima), agregar compatibilidad con el desplazamiento del puntero para facilitar las acciones de nivel de celda sin necesidad de seleccionar una celda y aclarar el estado de ejecución mediante la adición de un recuento de ejecuciones, y un botón animado para _detener la ejecución_. También hemos agregado métodos abreviados de teclado para _nuevo cuaderno_ (`Ctrl+Shift+N`), _ejecutar celda_ (`F5`), _nueva celda de código_ (`Ctrl+Shift+C`) y _nueva celda de texto_ (`Ctrl+Shift+T`). En un futuro intentaremos que todas las acciones clave se puedan iniciar mediante métodos abreviados, por lo que no dude en comentarnos qué echa en falta.

Entre otras mejoras y correcciones se incluyen las siguientes:
* La extensión de _SQL Server 2019 (versión preliminar)_ ahora solicita que se seleccione un directorio de instalación para las dependencias de Python. Además, ya no incluye Python en `.vsix file`, lo que reduce el tamaño total de la extensión. Las dependencias de Python son necesarias para admitir los kernels de Spark y Python3, por lo que es necesario instalar esta extensión para usarlos.
* Se ha agregado compatibilidad con el inicio de un nuevo cuaderno desde la línea de comandos. Si se inicia con los argumentos `--command=notebook.command.new --server=myservername`, debería abrirse un nuevo cuaderno y conectarse a este servidor.
* Se han realizado correcciones en el rendimiento de los cuadernos con gran longitud de código en las celdas. Si las celdas de código superan las 250 líneas, se les agregará una barra de desplazamiento.
* Se ha mejorado la compatibilidad con el archivo .ipynb. Ahora se admite la versión 3 o posterior. Tenga en cuenta que, al guardar los archivos, se actualizará a la versión 4 o superior.
* Ahora que el visor de Notebook integrado es estable, se ha quitado la configuración de usuario `notebook.enabled`.
* Ahora se admite el tema de contraste alto con una serie de correcciones en el diseño de objetos en este caso.
* Se ha corregido el error 3680, que hacía que a veces las salidas mostraran una serie de caracteres `,,,` incorrectamente.
* Se ha corregido el error 3602, que hacía que el editor desapareciera para las celdas después de salir de Azure Data Studio.
* Se ha agregado compatibilidad con el uso de vistas de cuadrícula para el tipo MIME de salida `application/vnd.dataresource+json`. Esto significa que muchos cuadernos que lo usan (por ejemplo, mediante el establecimiento de `pd.options.display.html.table_schema` en un cuaderno de Python) tendrán salidas tabulares más atractivas. Se ha corregido el error 3959, que hacía que Azure Data Studio intentase apagar el servidor de cuadernos dos veces después de cerrar el cuaderno.

#### <a name="known-issues"></a>Problemas conocidos
* Al abrir un cuaderno, aparece el cuadro de diálogo para instalar Python. Si se cancela esta instalación, las listas desplegables Kernels y Adjuntar a no mostrarán los valores esperados. La solución consiste en completar la instalación de Python.
* Cuando se abre un cuaderno con un kernel que no es compatible, las listas desplegables Kernels y _Adjuntar a_ harán que Azure Data Studio deje de responder. Tendrá que cerrar Azure Data Studio y asegurarse de usar un kernel compatible (Python3, Spark | R, Spark | Scala, PySpark, PySpark3).
* Se produce un error en el vínculo de la interfaz de usuario de Spark al usar PySpark3 u otros kernels de Spark en el punto de conexión de SQL Server. Como solución alternativa, haga clic en la interfaz de usuario de Spark en el panel, o bien conéctese mediante el tipo de conexión del clúster de macrodatos de SQL Server, ya que tendrá el hipervínculo correcto de la interfaz de usuario de Spark.

### <a name="extensibility-improvements"></a>Mejoras en la extensibilidad
Se han agregado a esta versión varias mejoras de ayuda a los extensores.
* Una nueva API `ObjectExplorerNodeProvider` permite que las extensiones contribuyan con carpetas en SQL Server u otros nodos de conexión. Así es como se agrega el nodo `Data Services` en instancias de SQL Server 2019, pero se podía usar para agregar Supervisión u otras carpetas fácilmente a la interfaz de usuario.
* Hay disponibles dos nuevos valores de clave de contexto para ayudar a mostrar u ocultar las contribuciones al panel.
  * `mssql:iscluster` indica si se trata de un clúster de macrodatos de SQL Server 2019.
  * `mssql:servermajorversion` tiene la versión del servidor (15 para SQL Server 2019, 14 para SQL Server 2017, etc.). Por ejemplo, esto puede resultar de ayuda si las características solo deben mostrarse para SQL Server 2017 o versiones superiores.


## <a name="release-notes-v080"></a>Notas de la versión (v0.8.0)
*Cuadernos*:
* Ahora se admite la adición de celdas antes o después de celdas existentes si se hace clic en el botón de celda "Más acciones".
* Se ha agregado la opción **Agregar nueva conexión** a las conexiones en la lista desplegable "Adjuntar a".
* Se ha agregado el comando **Reinstall Notebook Dependencies** (Reinstalar dependencias de Notebook) a fin de ayudar en las actualizaciones de paquetes de Python y en la resolución de los casos en los que la instalación se interrumpe a mitad de proceso mediante el cierre de la aplicación. Se puede ejecutar desde la paleta de comandos (use `Ctrl/Cmd+Shift+P` y escriba `Reinstall Notebook Dependencies`).
* El paquete de Python de PROSE se ha actualizado a 1.1.0 e incluye una serie de correcciones de errores. Use el comando **Reinstall Notebook Dependencies** (Reinstalar dependencias de Notebook) para actualizar este paquete.
* Ahora se admite un comando **Clear Output** (Borrar salida) si se hace clic en el botón de celda **Más acciones**.
* Se han corregido los siguientes problemas detectados por los clientes:
  * No se podía iniciar la sesión de Notebook en Windows debido a problemas con la ruta de acceso.
  * No se podía iniciar Notebook desde la carpeta raíz de una unidad, como C:\ o D:\.
  * [Error 2820](https://github.com/Microsoft/azuredatastudio/issues/2820): No se pueden editar los cuadernos creados desde ADS en VS Code.
  * Ahora, el vínculo de la interfaz de usuario de Spark funciona cuando se ejecuta un kernel de Spark.
  * Se ha cambiado el nombre de "Paquetes administrados" a "Instalación de paquetes".

*Creación de datos externos*:

* Los mensajes de error se pueden copiar y se han separado en una vista de resumen y de detalles por motivos de comodidad.
* Se ha mejorado el diseño de la interfaz de usuario y se han optimizado considerablemente el control de errores y la confiabilidad.
* Se han corregido los siguientes problemas detectados por los clientes:
  * Las tablas con asignaciones de columnas no válidas se muestran como deshabilitadas y una advertencia explica el error.

## <a name="release-notes-v072"></a>Notas de la versión (v0.7.2)
* Azure Resource Explorer ahora está integrado en Azure Data Studio y se ha quitado de esta extensión. Gracias por sus comentarios al respecto.
* Se ha mejorado el rendimiento de los cuadernos con muchas celdas de Markdown.
* Las celdas de código ajustan el tamaño automáticamente en Notebook, pero siguen teniendo un tamaño mínimo basado en la barra de herramientas de la celda.
* Se notifica al usuario cuando se instalan las dependencias de Notebook. Sobre todo en Windows, esto puede tardar mucho tiempo, por lo que las notificaciones se muestran ahora en la vista de tareas.
* Se admite la reinstalación de las dependencias de Notebook. Esto resulta útil si el usuario cerró Azure Data Studio a mitad de la instalación.
* Se permite cancelar la ejecución de celdas en Notebook.
* Se ha mejorado la confiabilidad al usar el Asistente para crear datos externos, sobre todo cuando se producen errores de conexión.
* Se ha bloqueado el uso del Asistente para crear datos externos si PolyBase no está habilitado o no se ejecuta en el servidor de destino.
* Se han realizado correcciones ortográficas y de nomenclatura relacionadas con SQL Server 2019 y la creación de datos externos.
* Se ha eliminado un gran número de errores de la consola de depuración de Azure Data Studio.

##  <a name="sql-server-2019-big-data-cluster-support"></a>Compatibilidad con clústeres de macrodatos de SQL Server 2019

* Haga clic en **Agregar conexión** en el *Explorador de objetos* y elija **SQL Server big data cluster** (Clúster de macrodatos de SQL Server) como tipo de conexión.

   > [!TIP]
   > Si no ve el tipo de conexión **SQL Server big data cluster** (Clúster de macrodatos de SQL Server), reinicie Azure Data Studio.

* Escriba el nombre de host o la dirección IP del punto de conexión del clúster, más el nombre de usuario y la contraseña que use para conectarse.
* Opcionalmente, incluya un nombre para mostrar que sea descriptivo en el campo **Nombre**.
* Después de hacer clic en **Conectar**, ya puede iniciar tareas comunes desde el panel, examinar **HDFS** en el Explorador de objetos y ejecutar tareas en contexto desde allí.
* Para enviar un trabajo de Spark al clúster, haga clic con el botón derecho en el nodo de servidor en el *Explorador de objetos* y elija **Submit Spark Job** (Enviar trabajo de Spark) para que aparezca el cuadro de diálogo de envío.
* Para abrir un cuaderno, consulte la sección siguiente.

Para obtener más información, consulte [Clústeres de macrodatos](../big-data-cluster/big-data-cluster-overview.md).


## <a name="azure-data-studio-notebooks"></a>Cuadernos de Azure Data Studio

* Abra un cuaderno de una de las siguientes maneras:
  * Abra un nuevo cuaderno desde la *paleta de comandos*.
  * Abra el árbol del Explorador de objetos de HDFS para un clúster de macrodatos de SQL Server 2019 y después:
    * Haga clic con el botón derecho en el nodo del servidor y seleccione **New Jupyter Notebook** (Nuevo cuaderno de Jupyter).
    * Haga clic con el botón derecho en un archivo CSV y elija **Analyze in Notebook** (Analizar en Notebook).
  * Abra un archivo .ipynb existente desde el menú **Archivo** o el explorador de archivos *(los archivos .ipynb deben actualizarse a la versión 4 o posterior para que se carguen correctamente)* .
* Seleccione un kernel. Para la ejecución de un cuaderno local, elija Python 3. Para la ejecución remota, seleccione PySpark o Spark | Scala.
* Elija un punto de conexión de clúster de macrodatos de SQL Server al que conectarse si se ejecuta de forma remota (esto no es necesario para el desarrollo local con Python 3).
* Agregue código o celdas de Markdown con los botones del encabezado del cuaderno. Elimine celdas con el icono de papelera situado a la izquierda de cada celda.
* Ejecute celdas con el botón de reproducción para las celdas de código y alterne la edición y la vista previa de Markdown con el icono de ojo.

## <a name="polybase-create-external-table-wizard"></a>Asistente para crear tablas externas de PolyBase

* En una instancia de SQL Server 2019, puede abrir el *Asistente para crear tablas externas* de tres maneras:
  * Haga clic con el botón derecho en un servidor, seleccione **Administrar**, haga clic en la pestaña de SQL Server 2019 (versión preliminar) y elija **Create External Table** (Crear una tabla externa).
  * Con una instancia de SQL Server 2019 seleccionada en el *Explorador de objetos*, abra el *Asistente para crear tablas externas* con la *paleta de comandos*.
  * Haga clic con el botón derecho en una base de datos de SQL Server 2019 en el *Explorador de objetos* y elija **Create External Table** (Crear una tabla externa).
* En esta versión de la extensión, se pueden crear tablas externas para acceder a tablas remotas de SQL Server y Oracle.

  > [!NOTE]
  > Aunque la funcionalidad de tabla externa es una característica de SQL 2019, puede que la instancia remota de SQL Server ejecute una versión anterior de SQL Server.

* Elija si va a acceder a SQL Server o a Oracle en la primera página del asistente y continúe.
* Se le pedirá que cree una clave maestra de base de datos si todavía no se ha creado una (se bloquearán las contraseñas con una complejidad insuficiente).
* Cree una conexión de origen de datos y una credencial con nombre para el servidor remoto.
* Elija los objetos que se van a asignar a la nueva tabla externa.
* Elija **Generar script** o **Crear** para finalizar el asistente.
* Después de crear la tabla externa, aparece inmediatamente en el árbol de objetos de la base de datos donde se creó.


## <a name="known-issues"></a>Problemas conocidos

* Si no se guarda la contraseña al crear una conexión, es posible que algunas acciones como enviar un trabajo de Spark no se realicen correctamente.
* Los cuadernos .ipynb existentes deben actualizarse a la versión 4 o superior para que se cargue el contenido en el visor.
* La ejecución del comando **Reinstall Notebook Dependencies** (Reinstalar dependencias de Notebook) puede mostrar dos tareas en la vista tareas, una de las cuales produce un error. Esto no hace que se produzca un error en la instalación.
* Si selecciona **Agregar nueva conexión** en un cuaderno y hace clic en cancelar, se mostrará la opción **Seleccionar conexión**, incluso si ya estaba conectado.
