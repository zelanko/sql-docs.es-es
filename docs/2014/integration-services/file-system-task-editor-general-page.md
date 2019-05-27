---
title: Editor de tareas del sistema de archivos (página General) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.filesystemtask.general.f1
helpviewer_keywords:
- File System Task Editor
ms.assetid: 51fe6614-3418-4eff-a28d-02ea31cc9aa9
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 594b87b3e2d58ffe60bd3c31324811a66038c82b
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/23/2019
ms.locfileid: "66058811"
---
# <a name="file-system-task-editor-general-page"></a>Editor de la tarea Sistema de archivos (página General)
  Use la página **General** del cuadro de diálogo **Editor de la tarea Sistema de archivos** para configurar la operación del sistema de archivos que lleva a cabo la tarea.  
  
 Para obtener información acerca de esta tarea, vea [File System Task](control-flow/file-system-task.md).  
  
 Debe especificar un administrador de conexiones de origen y destino mediante las propiedades SourceConnection y DestinationConnection. Puede proporcionar los nombres de los administradores de conexión de archivos que señalan a los archivos que utiliza la tarea como origen o destino, o bien proporcionar los nombres de las variables si las rutas de acceso de los archivos están almacenadas en variables. Si quiere usar variables para almacenar rutas de acceso de archivo, primero debe establecer la opción IsSourcePathVariable para la conexión de origen y la opción IsDestinationPatheVariable para la conexión de destino en **True**. A continuación, puede elegir las variables definidas por el usuario o del sistema existentes que se utilizarán, o bien puede crear nuevas variables. En el cuadro de diálogo **Agregar variable** , puede configurar y especificar el ámbito de las variables. El ámbito debe ser la tarea Sistema de archivos o un contenedor principal. Para obtener más información, vea [Variables de Integration Services &#40;SSIS&#41;](integration-services-ssis-variables.md) y [Usar variables en paquetes](../../2014/integration-services/use-variables-in-packages.md).  
  
> [!NOTE]  
>  Para invalidar las variables seleccionadas para la `SourceConnection` y `DestinationConnection` propiedades, escriba una expresión para el **origen** y **destino** propiedades. Las expresiones se especifican en la página **Expresiones** del **Editor de la tarea Sistema de archivos**. Por ejemplo, para establecer la ruta de acceso de los archivos que usa la tarea como destino, tal vez desee utilizar una variable A en determinadas condiciones y una variable B, en otras.  
  
> [!NOTE]  
>  La tarea Sistema de archivos trabaja con un solo archivo o directorio. Por consiguiente, esta tarea no admite el uso de caracteres comodín para realizar la misma operación en varios archivos o directorios. Para hacer que la tarea Sistema de archivos realice una determinada operación sobre varios archivos o directorios, coloque la tarea Sistema de archivos en un contenedor de bucles Foreach. Para más información, consulte [File System Task](control-flow/file-system-task.md).  
  
 Puede usar expresiones para utilizar distintas variables para  
  
## <a name="options"></a>Opciones  
 **IsDestinationPathVariable**  
 Indica si la ruta de acceso de destino está almacenada en una variable. Esta propiedad presenta las opciones indicadas en la siguiente tabla.  
  
|Valor|Descripción|  
|-----------|-----------------|  
|**True**|La ruta de destino está almacenada en una variable. Al seleccionar este valor se muestra la opción dinámica, **DestinationVariable**.|  
|**False**|La ruta de destino se especifica en un administrador de conexiones de archivos. Al seleccionar este valor muestra la opción dinámica `DestinationConnection`.|  
  
 **OverwriteDestination**  
 Especifique si la operación puede sobrescribir archivos en el directorio de destino.  
  
 **Name**  
 Proporcione un nombre único para la tarea Sistema de archivos. Este nombre se utiliza como etiqueta en el icono de tarea.  
  
> [!NOTE]  
>  Los nombres de tarea deben ser únicos en un paquete.  
  
 **Descripción**  
 Escriba una descripción de la tarea Sistema de archivos.  
  
 **Operación**  
 Seleccione la operación del sistema de archivos que se debe llevar a cabo. Esta propiedad presenta las opciones indicadas en la siguiente tabla.  
  
|Valor|Descripción|  
|-----------|-----------------|  
|**Copiar directorio**|Copie un directorio. Al seleccionar este valor se muestran las opciones dinámicas para un origen y un destino.|  
|**Copiar archivo**|Copie un archivo. Al seleccionar este valor se muestran las opciones dinámicas para un origen y un destino.|  
|**Crear directorio**|Cree un directorio. Al seleccionar este valor se muestran las opciones dinámicas para un directorio de origen y destino.|  
|**Eliminar directorio**|Elimine un directorio. Al seleccionar este valor se muestran las opciones dinámicas para un origen.|  
|**Eliminar contenido de directorio**|Elimine el contenido de un directorio. Al seleccionar este valor se muestran las opciones dinámicas para un origen.|  
|**Eliminar archivo**|Elimine un archivo. Al seleccionar este valor se muestran las opciones dinámicas para un origen.|  
|**Mover directorio**|Mueva un directorio. Al seleccionar este valor se muestran las opciones dinámicas para un origen y un destino.|  
|**Mover archivo**|Mueva un archivo. Al seleccionar este valor se muestran las opciones dinámicas para un origen y un destino.<br /><br /> Nota: Al mover un archivo, no incluya el nombre del archivo en la ruta de acceso del directorio que proporcione como destino.|  
|**Cambiar nombre de archivo**|Cambie el nombre de un archivo. Al seleccionar este valor se muestran las opciones dinámicas para un origen y un destino.<br /><br /> Nota: Al cambiar el nombre de un archivo, incluya el nuevo nombre del archivo en la ruta de acceso del directorio que proporcione como destino.|  
|**Establecer atributos**|Establezca los atributos de un archivo o un directorio. Al seleccionar este valor se muestran las opciones dinámicas para un origen y una operación.|  
  
 `IsSourcePathVariable`  
 Indica si la ruta de acceso de destino está almacenada en una variable. Esta propiedad presenta las opciones indicadas en la siguiente tabla.  
  
|Valor||  
|-----------|-|  
|**True**|La ruta de destino está almacenada en una variable. Si selecciona este valor, se mostrará la opción dinámica **SourceVariable**.|  
|**False**|La ruta de destino se especifica en un administrador de conexiones de archivos. Al seleccionar este valor se muestra la opción dinámica, **DestinationVariable**.|  
  
## <a name="isdestinationpathvariable-dynamic-options"></a>Opciones dinámicas de IsDestinationPathVariable  
  
### <a name="isdestinationpathvariable--true"></a>IsDestinationPathVariable = True  
 **DestinationVariable**  
 Seleccione el nombre de la variable en la lista o haga clic en \<**Nueva variable…**> para crear una.  
  
 **Temas relacionados:** [Variables de Integration Services &#40;SSIS&#41;](integration-services-ssis-variables.md), [Agregar variable](../../2014/integration-services/add-variable.md)  
  
### <a name="isdestinationpathvariable--false"></a>IsDestinationPathVariable = False  
 `DestinationConnection`  
 Seleccione un administrador de conexiones de archivos de la lista, o bien haga clic en \<**Nueva conexión…**> para crear un administrador de conexiones.  
  
 **Temas relacionados:** [Administrador de conexiones de archivos](connection-manager/file-connection-manager.md), [Editor de administrador de conexiones de archivos](../../2014/integration-services/file-connection-manager-editor.md)  
  
## <a name="issourcepathvariable-dynamic-options"></a>Opciones dinámicas de IsSourcePathVariable  
  
### <a name="issourcepathvariable--true"></a>IsSourcePathVariable = True  
 **SourceVariable**  
 Seleccione el nombre de la variable en la lista o haga clic en \<**Nueva variable…**> para crear una.  
  
 **Temas relacionados:** [Variables de Integration Services &#40;SSIS&#41;](integration-services-ssis-variables.md), [Agregar variable](../../2014/integration-services/add-variable.md)  
  
### <a name="issourcepathvariable--false"></a>IsSourcePathVariable = False  
 `SourceConnection`  
 Seleccione un administrador de conexiones de archivos de la lista, o bien haga clic en \<**Nueva conexión…**> para crear un administrador de conexiones.  
  
 **Temas relacionados:** [Administrador de conexiones de archivos](connection-manager/file-connection-manager.md), [Editor de administrador de conexiones de archivos](../../2014/integration-services/file-connection-manager-editor.md)  
  
## <a name="operation-dynamic-options"></a>Opciones dinámicas de Operación  
  
### <a name="operation--set-attributes"></a>Operación = Establecer atributos  
 **Hidden**  
 Indique si el archivo o el directorio está visible.  
  
 **Solo lectura**  
 Indique si el archivo es de solo lectura.  
  
 **Archive**  
 Indique si el archivo o el directorio está listo para archivar.  
  
 **Sistema**  
 Indique si el archivo es un archivo del sistema operativo.  
  
### <a name="operation--create-directory"></a>Operación = Crear directorio  
 `UseDirectoryIfExists`  
 Indica si la operación **Crear directorio** usa un directorio existente con el nombre especificado, en lugar de crear un directorio.  
  
## <a name="see-also"></a>Vea también  
 [Referencia de errores y mensajes de Integration Services](../../2014/integration-services/integration-services-error-and-message-reference.md)   
 [Página Expresiones](expressions/expressions-page.md)  
  
  
