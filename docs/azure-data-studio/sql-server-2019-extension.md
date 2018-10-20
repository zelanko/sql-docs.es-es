---
title: Extensión de datos Studio SQL Server 2019 Azure (versión preliminar) | Microsoft Docs
description: Extensión de la versión preliminar de SQL Server de 2019 para Azure Data Studio
ms.custom: tools|sos
ms.date: 10/11/2018
ms.reviewer: alayu; sstein
ms.prod: sql
ms.technology: azure-data-studio
ms.topic: conceptual
author: yualan
ms.author: alayu
manager: craigg
monikerRange: '>=sql-server-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 6624f2efb14f5d056ee0ac052fa9396535ebb239
ms.sourcegitcommit: ef115025e57ec342c14ed3151ce006f484d1fadc
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/18/2018
ms.locfileid: "49411172"
---
# <a name="sql-server-2019-extension-preview"></a>Extensión de SQL Server 2019 (versión preliminar)

La extensión de SQL Server 2019 (versión preliminar) proporciona compatibilidad de versión preliminar para las nuevas características y herramientas de apoyo de envío [!INCLUDE [sql-server-2019](..\includes\sssqlv15-md.md)]. Esto incluye compatibilidad con la versión preliminar [clústeres de SQL Server 2019 macrodatos](../big-data-cluster/big-data-cluster-overview.md), un enfoque integrado [experiencia de cuaderno](../big-data-cluster/notebooks-guidance.md), un PolyBase [asistente Create External Table](../relational-databases/polybase/data-virtualization.md?toc=%2fsql%2fbig-data-cluster%2ftoc.json)y [Azure Resource Explorer](azure-resource-explorer.md).

## <a name="install-the-sql-server-2019-extension-preview"></a>Instalar la extensión de SQL Server 2019 (versión preliminar)

Para instalar la extensión de SQL Server 2019 (versión preliminar), descargue e instale el archivo .vsix asociado.

1. Descargue el archivo .vsix de extensión (versión preliminar) de SQL Server 2019 en un directorio local:

   |Plataforma|Descargar|Fecha de la versión|Versión
   |:---|:---|:---|:---|
   |Windows|[.vsix](https://go.microsoft.com/fwlink/?LinkId=2031539)|18 de octubre de 2018|0.7.2
   |macOS|[.vsix](https://go.microsoft.com/fwlink/?LinkId=2031717)|18 de octubre de 2018 |0.7.2
   |Linux|[.vsix](https://go.microsoft.com/fwlink/?LinkId=2031538)|18 de octubre de 2018 |0.7.2

1. En Azure Data Studio elija **la extensión de instalación de paquete VSIX** desde el **archivo** menú y seleccione el archivo .vsix descargado.

1. Elija **Sí** cuando le pida que confirme la instalación y espere a que la notificación de que la instalación se realizó correctamente.

1. Seleccione **recarga** para habilitar la extensión (solo es necesario instalar una extensión por primera vez).

1. Después de volver a cargar, la extensión instalará las dependencias. Puede ver el progreso en la ventana de salida, y puede tardar varios minutos.

## <a name="release-notes-v072"></a>Notas de la versión (v0.7.2)
* Explorador de recursos de Azure ahora está integrado en Azure Data Studio y se ha quitado de esta extensión. Le agradecemos sus comentarios sobre este.
* Rendimiento mejorado de blocs de notas con muchas de las celdas de Markdown.
* Celdas de código de ajuste de tamaño automático en el Bloc de notas. Esto todavía tiene un tamaño mínimo basado en la barra de herramientas de la celda.
* Notifique al usuario al instalar las dependencias del Bloc de notas. En Windows en particular Esto puede tardar mucho tiempo, por lo que las notificaciones se muestran ahora en la vista de tareas.
* Compatibilidad con volver a instalar las dependencias del Bloc de notas. Esto es útil si el usuario cerró anteriormente Azure Data Studio mitad a través de la instalación.
* Compatibilidad con cancelar la ejecución de la celda en el Bloc de notas.
* Confiabilidad mejorada cuando se usa el Asistente para crear datos externos, específicamente cuando conexión se producen errores.
* Bloquea el uso del Asistente para crear datos externos si Polybase no está habilitada o se ejecutan en el servidor de destino.
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

## <a name="polybase-create-external-table-wizard"></a>Asistente para la tabla externa de la creación de Polybase

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
