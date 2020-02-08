---
title: Extensión de virtualización de datos
titleSuffix: Azure Data Studio
description: Extensión de virtualización de datos para Azure Data Studio
ms.reviewer: alayu; sstein
ms.prod: sql
ms.technology: azure-data-studio
ms.topic: conceptual
author: rajmera3
ms.author: raajmera
ms.custom: seodec18
ms.date: 11/04/2019
ms.openlocfilehash: 98a93895b8f552bf7506880a612ab2ae68c48afb
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 02/01/2020
ms.locfileid: "73801129"
---
# <a name="data-virtualization-extension-for-azure-data-studio"></a>Extensión de virtualización de datos para Azure Data Studio

La extensión de virtualización de datos para Azure Data Studio proporciona compatibilidad con el [Asistente para crear tablas externas](../relational-databases/polybase/data-virtualization.md?toc=/sql/toc/toc.json) de PolyBase.

## <a name="install-the-data-virtualization-extension"></a>Instalación de la extensión de virtualización de datos

Para instalar la extensión de virtualización de datos, abra Azure Data Studio y descárguela desde la pestaña Extensiones. Siga las instrucciones que encontrará [aquí](extensions.md).

## <a name="changes-in-release-10"></a>Cambios en la versión 1.0
* Se ha cambiado el nombre de la extensión a Virtualización de datos.
* Asistente para crear tablas externas:
    * Se han incluido cuadernos guiados para la virtualización de orígenes de MongoDB y Teradata.
    * Se ha agregado un cuadro de diálogo para rellenar las variables en los cuadernos de virtualización de MongoDB y Teradata. 

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
  * Control mejorado de los nombres de objeto con caracteres especiales En algunos casos, provocaban errores en el asistente
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
Se ha actualizado la compatibilidad con SQL Server 2019. Después de conectarse a una instancia de clúster de macrodatos de SQL Server, aparece una nueva carpeta _Data Services_ en el árbol del explorador. La carpeta dispone de puntos de inicio para acciones como abrir un nuevo cuaderno en la conexión, enviar trabajos de Spark y trabajar con HDFS. Para algunas acciones, como _crear datos externos_ en un archivo o carpeta de HDFS, se debe instalar la extensión de _SQL Server 2019_.

### <a name="notebook-support"></a>Compatibilidad con Notebook
En esta versión hemos realizado actualizaciones considerables en la interfaz de usuario de Notebook. Nuestro objetivo consistía en facilitar la lectura de los cuadernos que se comparten con usted. Esto conllevaba, entre otras cosas, quitar todos los cuadros de contorno alrededor de las celdas (a menos que se seleccionen o que se mueva el puntero por encima), agregar compatibilidad con el desplazamiento del puntero para facilitar las acciones de nivel de celda sin necesidad de seleccionar una celda y aclarar el estado de ejecución mediante la adición de un recuento de ejecuciones, y un botón animado para _detener la ejecución_. También hemos agregado métodos abreviados de teclado para _nuevo cuaderno_ (`Ctrl+Shift+N`), _ejecutar celda_ (`F5`), _nueva celda de código_ (`Ctrl+Shift+C`) y _nueva celda de texto_ (`Ctrl+Shift+T`). En un futuro intentaremos que todas las acciones clave se puedan iniciar mediante métodos abreviados, por lo que no dude en comentarnos qué echa en falta.

Entre otras mejoras y correcciones se incluyen las siguientes:
* La extensión de _SQL Server 2019_ ahora solicita a los usuarios que seleccionen un directorio de instalación para las dependencias de Python. Además, ya no incluye Python en `.vsix file`, lo que reduce el tamaño total de la extensión. Las dependencias de Python admiten kernels de Spark y Python3.
* Se ha agregado compatibilidad con el inicio de un nuevo cuaderno desde la línea de comandos. Si se inicia con los argumentos `--command=notebook.command.new --server=myservername`, debería abrirse un nuevo cuaderno y conectarse a este servidor.
* Se han realizado correcciones en el rendimiento de los cuadernos con gran longitud de código en las celdas. Si las celdas de código superan las 250 líneas, se agrega una barra de desplazamiento.
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
