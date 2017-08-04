---
title: "Editor de tareas del sistema de archivos (página General) | Documentos de Microsoft"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.dts.designer.filesystemtask.general.f1
helpviewer_keywords:
- File System Task Editor
ms.assetid: 51fe6614-3418-4eff-a28d-02ea31cc9aa9
caps.latest.revision: 43
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: ab4f38b627ab6fdc566e9ba452d3bf83f9630bb9
ms.contentlocale: es-es
ms.lasthandoff: 08/03/2017

---
# <a name="file-system-task-editor-general-page"></a>Editor de la tarea Sistema de archivos (página General)
  Use la página **General** del cuadro de diálogo **Editor de la tarea Sistema de archivos** para configurar la operación del sistema de archivos que lleva a cabo la tarea.  
  
 Para obtener información acerca de esta tarea, vea [File System Task](../../integration-services/control-flow/file-system-task.md).  
  
 Debe especificar un administrador de conexiones de origen y destino mediante las propiedades SourceConnection y DestinationConnection. Puede proporcionar los nombres de los administradores de conexión de archivos que señalan a los archivos que utiliza la tarea como origen o destino, o bien proporcionar los nombres de las variables si las rutas de acceso de los archivos están almacenadas en variables. Si quiere usar variables para almacenar rutas de acceso de archivo, primero debe establecer la opción IsSourcePathVariable para la conexión de origen y la opción IsDestinationPatheVariable para la conexión de destino en **True**. A continuación, puede elegir las variables definidas por el usuario o del sistema existentes que se utilizarán, o bien puede crear nuevas variables. En el cuadro de diálogo **Agregar variable** , puede configurar y especificar el ámbito de las variables. El ámbito debe ser la tarea Sistema de archivos o un contenedor principal. Para obtener más información, vea [Variables de Integration Services &#40;SSIS&#41;](../../integration-services/integration-services-ssis-variables.md) y [Usar variables en paquetes](http://msdn.microsoft.com/library/7742e92d-46c5-4cc4-b9a3-45b688ddb787).  
  
> [!NOTE]  
>  Para invalidar las variables seleccionadas para las propiedades **SourceConnection** y **DestinationConnection** , especifique una expresión para las propiedades **Source** y **Destination** . Las expresiones se especifican en la página **Expresiones** del **Editor de la tarea Sistema de archivos**. Por ejemplo, para establecer la ruta de acceso de los archivos que usa la tarea como destino, tal vez desee utilizar una variable A en determinadas condiciones y una variable B, en otras.  
  
> [!NOTE]  
>  La tarea Sistema de archivos trabaja con un solo archivo o directorio. Por consiguiente, esta tarea no admite el uso de caracteres comodín para realizar la misma operación en varios archivos o directorios. Para hacer que la tarea Sistema de archivos realice una determinada operación sobre varios archivos o directorios, coloque la tarea Sistema de archivos en un contenedor de bucles Foreach. Para más información, consulte [File System Task](../../integration-services/control-flow/file-system-task.md).  
  
 Puede usar expresiones para utilizar distintas variables para  
  
## <a name="options"></a>Opciones  
 **IsDestinationPathVariable**  
 Indica si la ruta de acceso de destino está almacenada en una variable. Esta propiedad presenta las opciones indicadas en la siguiente tabla.  
  
|Value|Description|  
|-----------|-----------------|  
|**True**|La ruta de destino está almacenada en una variable. Al seleccionar este valor se muestra la opción dinámica, **DestinationVariable**.|  
|**False**|La ruta de destino se especifica en un administrador de conexiones de archivos. Al seleccionar este valor se muestra la opción dinámica, **DestinationConnection**.|  
  
 **OverwriteDestination**  
 Especifique si la operación puede sobrescribir archivos en el directorio de destino.  
  
 **Nombre**  
 Proporcione un nombre único para la tarea Sistema de archivos. Este nombre se utiliza como etiqueta en el icono de tarea.  
  
> [!NOTE]  
>  Los nombres de tarea deben ser únicos en un paquete.  
  
 **Description**  
 Escriba una descripción de la tarea Sistema de archivos.  
  
 **Operación**  
 Seleccione la operación del sistema de archivos que se debe llevar a cabo. Esta propiedad presenta las opciones indicadas en la siguiente tabla.  
  
|Value|Description|  
|-----------|-----------------|  
|**Copiar directorio**|Copie un directorio. Al seleccionar este valor se muestran las opciones dinámicas para un origen y un destino.|  
|**Copiar archivo**|Copie un archivo. Al seleccionar este valor se muestran las opciones dinámicas para un origen y un destino.|  
|**Crear directorio**|Cree un directorio. Al seleccionar este valor se muestran las opciones dinámicas para un directorio de origen y destino.|  
|**Eliminar directorio**|Elimine un directorio. Al seleccionar este valor se muestran las opciones dinámicas para un origen.|  
|**Eliminar contenido de directorio**|Elimine el contenido de un directorio. Al seleccionar este valor se muestran las opciones dinámicas para un origen.|  
|**Eliminar archivo**|Elimine un archivo. Al seleccionar este valor se muestran las opciones dinámicas para un origen.|  
|**Mover directorio**|Mueva un directorio. Al seleccionar este valor se muestran las opciones dinámicas para un origen y un destino.|  
|**Mover archivo**|Mueva un archivo. Al seleccionar este valor se muestran las opciones dinámicas para un origen y un destino. Al mover un archivo, no incluya el nombre del archivo en la ruta de acceso del directorio que proporcione como destino.|  
|**Cambiar nombre de archivo**|Cambie el nombre de un archivo. Al seleccionar este valor se muestran las opciones dinámicas para un origen y un destino. Al cambiar el nombre de un archivo, incluya el nuevo nombre del archivo en la ruta de acceso del directorio que proporcione como destino.|  
|**Establecer atributos**|Establezca los atributos de un archivo o un directorio. Al seleccionar este valor se muestran las opciones dinámicas para un origen y una operación.|  
  
 **IsSourcePathVariable**  
 Indica si la ruta de acceso de destino está almacenada en una variable. Esta propiedad presenta las opciones indicadas en la siguiente tabla.  
  
|Value||  
|-----------|-|  
|**True**|La ruta de destino está almacenada en una variable. Si selecciona este valor, se mostrará la opción dinámica **SourceVariable**.|  
|**False**|La ruta de destino se especifica en un administrador de conexiones de archivos. Al seleccionar este valor se muestra la opción dinámica, **DestinationVariable**.|  
  
## <a name="isdestinationpathvariable-dynamic-options"></a>Opciones dinámicas de IsDestinationPathVariable  
  
### <a name="isdestinationpathvariable--true"></a>IsDestinationPathVariable = True  
 **DestinationVariable**  
 Seleccione el nombre de variable en la lista o haga clic en \< **nueva variable...** > para crear una nueva variable.  
  
 **Temas relacionados:** [Variables de Integration Services &#40;SSIS&#41;](../../integration-services/integration-services-ssis-variables.md), [Agregar variable](http://msdn.microsoft.com/library/d09b5d31-433f-4f7c-8c68-9df3a97785d5).  
  
### <a name="isdestinationpathvariable--false"></a>IsDestinationPathVariable = False  
 **DestinationConnection**  
 Seleccione un administrador de conexión de archivos en la lista o haga clic en \< **nueva conexión...** > para crear una nueva conexión de administrador.  
  
 **Temas relacionados:** [File Connection Manager](../../integration-services/connection-manager/file-connection-manager.md), [File Connection Manager Editor](../../integration-services/connection-manager/file-connection-manager-editor.md)  
  
## <a name="issourcepathvariable-dynamic-options"></a>Opciones dinámicas de IsSourcePathVariable  
  
### <a name="issourcepathvariable--true"></a>IsSourcePathVariable = True  
 **SourceVariable**  
 Seleccione el nombre de variable en la lista o haga clic en \< **nueva variable...** > para crear una nueva variable.  
  
 **Temas relacionados:** [Variables de Integration Services &#40;SSIS&#41;](../../integration-services/integration-services-ssis-variables.md), [Agregar variable](http://msdn.microsoft.com/library/d09b5d31-433f-4f7c-8c68-9df3a97785d5).  
  
### <a name="issourcepathvariable--false"></a>IsSourcePathVariable = False  
 **SourceConnection**  
 Seleccione un administrador de conexión de archivos en la lista o haga clic en \< **nueva conexión...** > para crear una nueva conexión de administrador.  
  
 **Temas relacionados:** [File Connection Manager](../../integration-services/connection-manager/file-connection-manager.md), [File Connection Manager Editor](../../integration-services/connection-manager/file-connection-manager-editor.md)  
  
## <a name="operation-dynamic-options"></a>Opciones dinámicas de Operación  
  
### <a name="operation--set-attributes"></a>Operación = Establecer atributos  
 **Oculto**  
 Indique si el archivo o el directorio está visible.  
  
 **Solo lectura**  
 Indique si el archivo es de solo lectura.  
  
 **Archive**  
 Indique si el archivo o el directorio está listo para archivar.  
  
 **Sistema**  
 Indique si el archivo es un archivo del sistema operativo.  
  
### <a name="operation--create-directory"></a>Operación = Crear directorio  
 **UseDirectoryIfExists**  
 Indica si la operación **Crear directorio** usa un directorio existente con el nombre especificado, en lugar de crear un directorio.  
  
## <a name="see-also"></a>Vea también  
 [Referencia de mensajes y Error de Integration Services](../../integration-services/integration-services-error-and-message-reference.md)   
 [Página Expresiones](../../integration-services/expressions/expressions-page.md)  
  
  
