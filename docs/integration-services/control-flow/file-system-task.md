---
title: Tarea sistema de archivos | Documentos de Microsoft
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
- sql13.dts.designer.filesystemtask.f1
helpviewer_keywords:
- File System task [Integration Services]
ms.assetid: 7dd79a6a-e066-4028-a385-1d40f31056f8
caps.latest.revision: 58
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: c3e47e4a5ae297202ba43679fba393421880a7ea
ms.openlocfilehash: 0c10a9020fe4fd03e9d71df19a9b16223e3031ea
ms.contentlocale: es-es
ms.lasthandoff: 08/03/2017

---
# <a name="file-system-task"></a>Tarea Sistema de archivos
  La tarea Sistema de archivos realiza operaciones en archivos y directorios del sistema de archivos. Por ejemplo, un paquete puede utilizar la tarea Sistema de archivos para crear, mover o eliminar directorios y archivos. También puede utilizar la tarea Sistema de archivos para establecer atributos en archivos y directorios. Por ejemplo, la tarea Sistema de archivos puede convertir los archivos en archivos ocultos o de solo lectura.  
  
 Todas las operaciones de la tarea Sistema de archivos usan un origen, que puede ser un archivo o un directorio. Por ejemplo, el archivo que la tarea copia o el directorio que elimina es un origen. El origen puede especificarse mediante un administrador de conexiones de archivos que señala al directorio o archivo, o proporcionando el nombre de una variable que contiene la ruta de origen. Para más información, vea [Administrador de conexiones de archivos](../../integration-services/connection-manager/file-connection-manager.md) e [Variables de Integration Services &#40;SSIS&#41;](../../integration-services/integration-services-ssis-variables.md).  
  
 Las operaciones que copian y mueven archivos y directorios, y cambian nombres de archivos, usan un destino y un origen. El destino se especifica mediante un administrador de conexiones de archivos o una variable. Las operaciones de la tarea Sistema de archivos pueden configurarse para permitir la sobrescritura de los archivos y directorios de destino. La operación que crea un nuevo directorio puede configurarse para usar un directorio existente que tiene el nombre especificado en lugar de generar un error si el directorio ya existe.  
  
## <a name="predefined-file-system-operations"></a>Operaciones de sistema de archivos predefinidas  
 La tarea Sistema de archivos incluye un conjunto predefinido de operaciones. Estas operaciones se describen en la siguiente tabla.  
  
|Operación|Description|  
|---------------|-----------------|  
|Copiar directorio|Copia una carpeta de una ubicación a otra.|  
|Copiar archivo|Copia un archivo de una ubicación a otra.|  
|Crear directorio|Crea una carpeta en una ubicación especificada.|  
|Eliminar directorio|Elimina una carpeta de una ubicación especificada.|  
|Eliminar contenido de directorio|Elimina todos los archivos y carpetas de una carpeta.|  
|Eliminar archivo|Elimina un archivo de una ubicación especificada.|  
|Mover directorio|Mueve una carpeta de una ubicación a otra.|  
|Mover archivo|Mueve un archivo de una ubicación a otra.|  
|Cambiar nombre de archivo|Cambia el nombre de un archivo de una ubicación especificada.|  
|Establecer atributos|Establece atributos de archivos y carpetas. Estos atributos son Archivar, Oculto, Normal, Solo lectura y Sistema. El atributo Normal indica que no hay atributos establecidos; no se puede combinar con otros atributos. Todos los demás atributos se pueden usar en combinación.|  
  
 La tarea Sistema de archivos trabaja con un solo archivo o directorio. Por consiguiente, esta tarea no admite el uso de caracteres comodín para realizar la misma operación en varios archivos. Para hacer que la tarea Sistema de archivos realice una determinada operación sobre varios archivos o directorios, coloque la tarea Sistema de archivos en un contenedor de bucles Foreach, como se describe en los pasos siguientes.  
  
-   **Configure el contenedor de bucles Foreach** En la página **Colección** del Editor de bucles Foreach, establezca el enumerador en **Enumerador de archivos para Foreach** y escriba la expresión comodín como configuración del enumerador para **Archivos**. En la página **Asignaciones de variables** del Editor de bucles Foreach, asigne una variable que desee utilizar para pasar los nombres de archivo a la tarea Sistema de archivos de uno en uno.  
  
-   **Agregue y configure una tarea Sistema de archivos** Agregue una tarea Sistema de archivos al contenedor de bucles Foreach. En la página **General** del Editor de la tarea sistema de archivos, establezca la propiedad **SourceVariable** o **DestinationVariable** en la variable que ha definido en el contenedor de bucles Foreach.  
  
## <a name="custom-log-entries-available-on-the-file-system-task"></a>Entradas del registro personalizadas disponibles en la tarea Sistema de archivos  
 La siguiente tabla contiene las entradas de registro personalizadas para la tarea Sistema de archivos. Para obtener más información, vea [Registro de Integration Services &#40;SSIS&#41;](../../integration-services/performance/integration-services-ssis-logging.md).  
  
|Entrada del registro|Description|  
|---------------|-----------------|  
|**FileSystemOperation**|Informa sobre la operación que realiza la tarea. La entrada del registro se escribe cuando se inicia la operación del sistema de archivos e incluye información sobre el origen y el destino.|  
  
## <a name="configuring-the-file-system-task"></a>Configurar la tarea Sistema de archivos  
 Puede establecer propiedades a través del Diseñador de [!INCLUDE[ssIS](../../includes/ssis-md.md)] o mediante programación.  
  
 Para obtener más información acerca de las propiedades que puede establecer en el Diseñador [!INCLUDE[ssIS](../../includes/ssis-md.md)] , vea los temas siguientes:  
  
-   [Editor de la tarea Sistema de archivos &#40;página General&#41;](../../integration-services/control-flow/file-system-task-editor-general-page.md)  
  
-   [Página Expresiones](../../integration-services/expressions/expressions-page.md)  
  
 Para obtener más información sobre cómo establecer estas propiedades en el Diseñador [!INCLUDE[ssIS](../../includes/ssis-md.md)] , vea el siguiente tema:  
  
-   [Establecer las propiedades de tareas o contenedores](http://msdn.microsoft.com/library/52d47ca4-fb8c-493d-8b2b-48bb269f859b)  
  
 Para obtener más información sobre cómo establecer estas propiedades mediante programación , vea el siguiente tema:  
  
-   <xref:Microsoft.SqlServer.Dts.Tasks.FileSystemTask.FileSystemTask>  
  
## <a name="related-tasks"></a>Tareas relacionadas  
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] incluye una tarea que descarga y carga archivos de datos, y administra directorios en servidores. Para más información, consulte [FTP Task](../../integration-services/control-flow/ftp-task.md).  
  
## <a name="see-also"></a>Vea también  
 [Tareas de Integration Services](../../integration-services/control-flow/integration-services-tasks.md)   
 [Flujo de control](../../integration-services/control-flow/control-flow.md)  
  
  
