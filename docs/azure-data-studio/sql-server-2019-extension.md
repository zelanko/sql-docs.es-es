---
title: Extensión de SQL Server 2019 (versión preliminar)
titleSuffix: Azure Data Studio
description: Extensión de la versión preliminar de SQL Server de 2019 para Azure Data Studio
ms.custom: seodec18
ms.date: 06/25/2019
ms.reviewer: alayu; sstein
ms.prod: sql
ms.technology: azure-data-studio
ms.topic: conceptual
author: yualan
ms.author: alayu
ms.openlocfilehash: 9b25fd044b94e21151b687d428c469a12d8c8a5d
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "67959215"
---
# <a name="sql-server-2019-extension-preview"></a>Extensión de SQL Server 2019 (versión preliminar)

La extensión de SQL Server 2019 (versión preliminar) proporciona compatibilidad de versión preliminar para las nuevas características y herramientas de apoyo de envío [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)]. Esto incluye compatibilidad con la versión preliminar [clústeres de SQL Server 2019 macrodatos](../big-data-cluster/big-data-cluster-overview.md), un enfoque integrado [experiencia de cuaderno](../big-data-cluster/notebooks-guidance.md)y un PolyBase [asistente Create External Table](../relational-databases/polybase/data-virtualization.md?toc=/sql/toc/toc.json).

## <a name="install-the-sql-server-2019-extension-preview"></a>Instalar la extensión de SQL Server 2019 (versión preliminar)

Para instalar la extensión de SQL Server 2019 (versión preliminar), descargue e instale el archivo .vsix asociado.

1. Descargue el archivo .vsix de extensión (versión preliminar) de SQL Server 2019 en un directorio local:

   |Plataforma|Descargar|Fecha de la versión|Versión
   |:---|:---|:---|:---|
   |Windows|[.vsix](https://go.microsoft.com/fwlink/?linkid=2097803)|25 de junio de 2019 |0.14.1
   |macOS|[.vsix](https://go.microsoft.com/fwlink/?linkid=2097802)|25 de junio de 2019 |0.14.1
   |Linux|[.vsix](https://go.microsoft.com/fwlink/?linkid=2097801)|25 de junio de 2019 |0.14.1

1. En Azure Data Studio elija **la extensión de instalación de paquete VSIX** desde el **archivo** menú y seleccione el archivo .vsix descargado.

1. Elija **Sí** cuando le pida que confirme la instalación y espere a que la notificación de que la instalación se realizó correctamente.

1. Seleccione **recarga** para habilitar la extensión (solo es necesario instalar una extensión por primera vez).

1. Después de volver a cargar, la extensión instalará las dependencias. Puede ver el progreso en la ventana de salida, y puede tardar varios minutos.

1. Las dependencias después de finalizar la instalación, cierre y vuelva a abrir Azure Data Studio. El **clúster de SQL Server macrodatos** tipo de conexión no está disponible hasta que reinicie Azure Data Studio.

## <a name="changes-in-release-0141"></a>Cambios en la versión 0.14.1
* Compatibilidad con el soporte técnico de origen de datos de CTP 3.1

## <a name="changes-in-release-0121"></a>Cambios de versión de la 0.12.1

* El **clúster de SQL Server macrodatos** tipo de conexión se ha quitado en esta versión. Toda la funcionalidad disponible anteriormente desde la conexión del clúster de macrodatos de SQL Server ahora está disponible en la conexión de SQL Server.
* Exploración de HDFS se puede encontrar en el **Data Services** carpeta
* Para equipos portátiles el PySpark y kernels macrodatos funcionan cuando se conecta a la instancia principal de SQL Server en el clúster de macrodatos de SQL Server.
* Crear a Asistente para la tabla externa:
  * Compatibilidad para crear la tabla externa mediante el origen de datos externo existente.
  * Mejoras de rendimiento en el asistente.
  * Mejora del tratamiento de nombres de objeto con caracteres especiales. En algunos casos ocasionados producirá un error en el Asistente
  * Mejoras de confiabilidad de la página de asignación de objeto.
  * Sistema quita las bases de datos - ': DWConfiguration', 'DWDiagnostics', 'DWQueue' - en la lista desplegable de bases de datos.
  * Soporte técnico para establecer el nombre del objeto de formato de archivo externo el **Create External Table desde archivos CSV** asistente.
  * Agrega un botón de actualización a la primera página de la **Create External Table desde archivos CSV** asistente.

## <a name="release-notes-v0110"></a>Notas de la versión (v0.11.0)

* Compatibilidad con Jupyter Notebook, específicamente el soporte técnico para los kernels de Python3 y Spark, se ha movido a Azure Data Studio. Esta extensión ya no es necesaria para poder usar los blocs de notas.
* Varias correcciones de errores en los asistentes para datos externos:
  * Se actualizaron las asignaciones de tipos de Oracle para que coincida con los cambios que se incluye en SQL Server 2019 CTP 2.3.
  * Se corrigió un problema donde estaban que se pierdan nuevos esquemas escritos en los controles de la asignación de tabla.
  * Se ha corregido un problema donde la comprobación de un nodo de base de datos en las asignaciones de tabla no se ha producido en todas las tablas y vistas que se está comprueba.


## <a name="release-notes-v0102"></a>Notas de la versión (v0.10.2)
### <a name="sql-server-2019-support"></a>Compatibilidad con SQL Server 2019
Se ha actualizado la compatibilidad con SQL Server 2019. Acerca de cómo conectarse a un clúster grande de datos de SQL Server, instancia de un nuevo _Data Services_ carpeta aparecerá en el árbol del explorador. Esto tiene puntos de inicio para acciones como abrir un nuevo cuaderno en la conexión, envío de trabajos de Spark y trabajar con HDFS. Tenga en cuenta que para algunas acciones como _Create External Data_ a través de un archivo o carpeta HDFS, el _versión preliminar de SQL Server de 2019_ debe instalarse la extensión.

### <a name="notebook-support"></a>Soporte técnico de Bloc de notas
Se han realizado actualizaciones importantes para la interfaz de usuario de Bloc de notas en esta versión. Nuestro objetivo era lo que facilita leer blocs de notas que se comparten con usted. Esto significaba quitando todos los cuadros de las celdas de esquema a menos que o mantuve el mouse, adición de soporte técnico al mantener el mouse para acciones de nivel de celda fácil sin necesitan seleccionar una celda y aclarar el estado de ejecución mediante la adición de recuento de ejecuciones, un elemento animado _Detener ejecución_ botón y mucho más. También agregamos métodos abreviados de teclado para _nuevo cuaderno_ (`Ctrl+Shift+N`), _ejecutar celda_ (`F5`), _nueva celda de código_ (`Ctrl+Shift+C`),  _Nueva celda de texto_ (`Ctrl+Shift+T`). Queremos tener todas las acciones claves que se puede iniciar mediante acceso directo nos sabe lo que se encuentra en adelante!

Otras mejoras y correcciones se incluyen:
* El _versión preliminar de SQL Server de 2019_ extensión ahora usa indicaciones para elegir un directorio de instalación de dependencias de Python. También incluye Python en ya no la `.vsix file`, lo que reduce el tamaño general de la extensión. Las dependencias de Python son necesarios para admitir los kernels de Spark y Python3, para instalar esta extensión es necesaria para usar estos.
* Se agregó compatibilidad para iniciar un nuevo cuaderno desde la línea de comandos. Iniciar con los argumentos `--command=notebook.command.new --server=myservername` debería abrir un nuevo cuaderno y conectarse a este servidor.
* Revisiones de rendimiento para equipos portátiles con una longitud de código de gran tamaño en las celdas. Si las celdas de código son más de 250 líneas tendrán un agregado de la barra de desplazamiento.
* Compatibilidad de archivo .ipynb mejorada. Ahora se admite la versión 3 o posterior. Tenga en cuenta que al guardar los archivos se actualizarán a la versión 4 o superior.
* El `notebook.enabled` configuración de usuario ha sido quitado ahora que la compilación en el Bloc de notas es estable Visor
* El tema de contraste alto ahora es compatible con una serie de correcciones a disposición de los objetos en este caso.
* Se ha corregido 3680 # donde salidas a veces se ha mostrado un número de `,,,` caracteres incorrectamente
* Editor de #3602 fijo desaparece para celdas después de salir de studio datos de azure
* Se agregó compatibilidad para utilizar las vistas de cuadrícula para el `application/vnd.dataresource+json` tipo MIME de salida. Esto significa que muchos portátiles que usan este (por ejemplo, configurando `pd.options.display.html.table_schema` en un cuaderno de Python) tendrá resultados tabulares más bonito fijo #3959 Azure Data Studio intenta apagar el servidor de Bloc de notas dos veces después de cerrar el Bloc de notas

#### <a name="known-issues"></a>Problemas conocidos
* Al abrir un cuaderno aparecerá el cuadro de diálogo de instalación de python. Cancelar la instalación dará como resultado los Kernels y adjuntar a las listas desplegables no se muestran los valores esperados. La solución consiste en completar la instalación de Python.
* Cuando se abre un bloc de notas con un kernel que no es compatible, los kernels y _adjuntar a_ listas desplegables hará que Azure Data Studio deje de responder. Deberá cerrar Data Studio de Azure y asegúrese de usar un kernel compatible (Python3, Spark | R, Spark | Scala, PySpark, PySpark3)
* Se produce un error en el vínculo de la interfaz de usuario de Spark al usar PySpark3 o kernels Spark en el punto de conexión de SQL Server. Como alternativa, haga clic en la interfaz de usuario de Spark desde el panel, o conectarse con el tipo de conexión del clúster de macrodatos de SQL Server, ya que esto tendrá el hipervínculo correcto de la interfaz de usuario de Spark

### <a name="extensibility-improvements"></a>Mejoras de extensibilidad
En esta versión se ha agregado una serie de mejoras que ayudan a los extensores
* Un nuevo `ObjectExplorerNodeProvider` API permite que las extensiones contribuir a las carpetas en SQL Server o en otros nodos de conexión. Se trata cómo el `Data Services` nodo se agrega debajo de las instancias de SQL Server 2019 pero se puede usar para agregar supervisión u otras carpetas fácilmente a la interfaz de usuario.
* Dos nuevos valores clave de contexto están disponibles para ayudar a las contribuciones de mostrar u ocultar en el panel.
  * `mssql:iscluster` indica si se trata de un clúster grande de datos de SQL Server de 2019
  * `mssql:servermajorversion` tiene la versión del servidor (15 para SQL Server 2019, 14 para SQL Server 2017 y así sucesivamente). Esto puede ayudar si características solo se deben mostrar para SQL Server 2017 o superior, por ejemplo.


## <a name="release-notes-v080"></a>Notas de la versión (v0.8.0)
*Blocs de notas*:
* Agregar celdas antes y después existente ahora se admite celdas, haga clic en el botón de celda "Más acciones"
* **Agregar nueva conexión** ha agregado la opción para las conexiones en la lista desplegable "Conectar a"
* Un **volver a instalar las dependencias de Bloc de notas** comando se ha agregado a ayudar con las actualizaciones de paquetes de Python y resolver casos donde se detuvo la instalación cuelga a medio camino cerrando la aplicación. Esto se puede ejecutar desde la paleta de comandos (use `Ctrl/Cmd+Shift+P` y tipo `Reinstall Notebook Dependencies`)
* El paquete de python PROSE se ha actualizado a la versión 1.1.0 e incluye una serie de correcciones de errores. Use la **volver a instalar las dependencias de Bloc de notas** comando para actualizar este paquete
* Un **borrar resultado** ahora se admite el comando, haga clic en el **más acciones** botón de celda
* Se ha corregido los siguientes problemas notificados por los clientes:
  * No se pudo iniciar sesión de Bloc de notas en Windows debido a problemas de la ruta de acceso
  * No se pudo iniciar el Bloc de notas de la carpeta raíz de una unidad, como C:\ o D:\
  * [#2820](https://github.com/Microsoft/azuredatastudio/issues/2820) no se puede modificar los blocs de notas creados a partir de anuncios en VS Code
  * Vínculo de la interfaz de usuario de Spark ahora funciona cuando se ejecuta un kernel de Spark
  * Cambiar el nombre "Administrados paquetes" a "Instalar los paquetes"

*Crear datos externos*:

* Los mensajes de error son que se puede copiar y se han dividido en una vista resumida y detallada para sea más fácil
* Diseño de interfaz de usuario mejorada y mejorar significativamente la confiabilidad y control de errores
* Se ha corregido los siguientes problemas notificados por los clientes:
  * Las tablas con asignaciones de columnas no válido se muestran como deshabilitado y una advertencia, explica el error

## <a name="release-notes-v072"></a>Notas de la versión (v0.7.2)
* Explorador de recursos de Azure ahora está integrado en Azure Data Studio y se ha quitado de esta extensión. Le agradecemos sus comentarios sobre este.
* Rendimiento mejorado de blocs de notas con muchas de las celdas de Markdown.
* Celdas de código de ajuste de tamaño automático en el Bloc de notas. Esto todavía tiene un tamaño mínimo basado en la barra de herramientas de la celda.
* Notifique al usuario al instalar las dependencias del Bloc de notas. En Windows en particular Esto puede tardar mucho tiempo, por lo que las notificaciones se muestran ahora en la vista de tareas.
* Compatibilidad con volver a instalar las dependencias del Bloc de notas. Esto es útil si el usuario cerró anteriormente Azure Data Studio mitad a través de la instalación.
* Compatibilidad con cancelar la ejecución de la celda en el Bloc de notas.
* Confiabilidad mejorada cuando se usa el Asistente para crear datos externos, específicamente cuando conexión se producen errores.
* Bloquea el uso del Asistente para crear datos externos si PolyBase no está habilitada o se ejecutan en el servidor de destino.
* Corrector ortográfico y correcciones relacionados con SQL Server 2019 y crear datos externos de nomenclatura.
* Quita un gran número de errores de la consola de depuración de Azure Data Studio.

##  <a name="sql-server-2019-big-data-cluster-support"></a>Compatibilidad con clúster grande de datos de SQL Server de 2019

* Haga clic en **Agregar conexión** en *Explorador de objetos* y elija **clúster de SQL Server macrodatos** como el tipo de conexión.

   > [!TIP]
   > Si no ve el **clúster de SQL Server macrodatos** tipo de conexión, reinicie Azure Studio datos.

* Escriba el nombre de host o dirección IP del punto de conexión de clúster plus el nombre de usuario y contraseña usada para conectarse.
* Opcionalmente, puede incluir un nombre para mostrar descriptivo en el **nombre** campo.
* Haga clic en **Connect** y, a continuación, se pueden iniciar las tareas comunes en el panel, examinar **HDFS** en el Explorador de objetos y tareas de ejecución en el contexto a partir de ahí.
* Para enviar un trabajo de Spark en el clúster, haga doble clic en el nodo del servidor en *Explorador de objetos* y elija **Submit Spark Job** para que aparezca el cuadro de diálogo de envío.
* Para abrir un cuaderno, consulte la sección siguiente.

Para obtener más información, consulte [clústeres grandes de datos](../big-data-cluster/big-data-cluster-overview.md).


## <a name="azure-data-studio-notebooks"></a>Datos de Azure Notebooks de Studio

* Abrir un cuaderno en una de las maneras siguientes:
  * Abra un nuevo bloc de notas de la *paleta de comandos*.
  * Abra el árbol del explorador de objetos de HDFS para un clúster de macrodatos de 2019 de SQL Server y, o bien:
    * Haga clic con el botón derecho en el nodo del servidor y elija **nuevo cuaderno de Jupyter**.
    * Haga clic con el botón derecho en un archivo CSV y elija **analizar en el Bloc de notas**.
  * Abrir un archivo .ipynb existente desde el **archivo** explorer menú o archivo *(archivos .ipynb deben actualizarse a la versión 4 o posterior para cargar correctamente)*
* Elija un núcleo. Para la ejecución local de Bloc de notas, elija Python 3. Para la ejecución remota, elija PySpark o Spark | Scala.
* Elija un punto de conexión de clúster de macrodatos de SQL Server para conectarse a si la ejecución de forma remota (Esto no es necesario para el desarrollo local con Python 3).
* Las celdas de código o marcado mediante los botones se agregan en el encabezado del cuaderno. Eliminación de las celdas con el icono de Papelera a la izquierda de cada celda.
* Ejecutar las celdas con el botón Reproducir para las celdas de código y activar o desactivar la edición de markdown y obtener una vista previa con el icono de ojo

## <a name="polybase-create-external-table-wizard"></a>Asistente para la tabla externa de la creación de PolyBase

* Desde una instancia de SQL Server 2019 el *crear Asistente para la tabla externa* se puede abrir de tres maneras:
  * Haga clic con el botón derecho en un servidor, elija **administrar**, haga clic en la pestaña para SQL Server 2019 (versión preliminar) y elija **Create External Table**.
  * Con una instancia de SQL Server 2019 seleccionada en *Explorador de objetos*, aparezca *crear Asistente externo* a través de la *paleta de comandos*.
  * Haga clic con el botón derecho en una base de datos SQL Server 2019 *Explorador de objetos* y elija **Create External Table**.
* En esta versión de la extensión, se pueden crear tablas externas para tener acceso a tablas remotas de SQL Server y Oracle.

  > [!NOTE]
  > Aunque la funcionalidad de la tabla externa es una característica de 2019 SQL, SQL Server remoto puede ejecutar una versión anterior de SQL Server.

* Elija si tienen acceso a SQL Server u Oracle en la primera página del asistente y continuar.
* Se le pedirá que cree una clave maestra de base de datos si no se ha creado uno ya (se bloquearán las contraseñas de complejidad insuficiente).
* Crear una conexión de origen de datos y con el nombre de credencial para el servidor remoto.
* Elija los objetos que desea asignar a la nueva tabla externa.
* Elija **generar Script** o **crear** para finalizar el asistente.
* Después de la creación de la tabla externa, lo aparece inmediatamente en el árbol de objetos de la base de datos donde se creó.


## <a name="known-issues"></a>Problemas conocidos

* Si no se guarda la contraseña al crear una conexión, algunas acciones como enviar trabajo de Spark pueden no realizarse correctamente.
* Blocs de notas .ipynb existentes deben actualizarse a la versión 4 o posterior para cargar contenido en el Visor.
* Ejecuta el **volver a instalar las dependencias de Bloc de notas** comando puede mostrar 2 tareas en la vista de tareas, uno de los cuales se produce un error. Esto hace que no se instale correctamente
* Elegir **agregar nueva conexión** en un bloc de notas y haga clic en Cancelar, se producirán **Seleccionar conexión** van a mostrar, incluso si ya se han conectado.
