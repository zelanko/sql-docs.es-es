---
title: "Editor de la tarea FTP (página de transferencia de archivos) | Documentos de Microsoft"
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
- sql13.dts.designer.ftptask.filetransfer.f1
helpviewer_keywords:
- File Transfer Protocol Task Editor
ms.assetid: 37e52220-feb2-474c-ad88-fa1b1059acd4
caps.latest.revision: 26
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: ca75f79962fcf7b7cae067a7d841f80f9c4c2032
ms.contentlocale: es-es
ms.lasthandoff: 08/03/2017

---
# <a name="ftp-task-editor-file-transfer-page"></a>Editor de la tarea FTP (página Transferencia de archivos)
  Use la página **Transferencia de archivos** del cuadro de diálogo **Editor de la tarea FTP** para configurar la operación de FTP que realiza la tarea.  
  
 Para más información sobre esta tarea, vea [Tarea FTP](../../integration-services/control-flow/ftp-task.md).  
  
## <a name="options"></a>Opciones  
 **IsRemotePathVariable**  
 Indica si la ruta remota se almacena en una variable. Esta propiedad presenta las opciones indicadas en la siguiente tabla.  
  
|Value|Description|  
|-----------|-----------------|  
|**True**|La ruta de destino está almacenada en una variable. Al seleccionar este valor se muestra la opción dinámica **RemoteVariable**.|  
|**False**|La ruta de destino se especifica en un administrador de conexiones de archivos. Al seleccionar este valor se muestra la opción dinámica **RemotePath**.|  
  
 **OverwriteFileAtDestination**  
 Especifica si se puede sobrescribir un archivo del destino.  
  
 **IsLocalPathVariable**  
 Indica si la ruta de acceso local está almacenada en una variable. Esta propiedad presenta las opciones indicadas en la siguiente tabla.  
  
|Value|Description|  
|-----------|-----------------|  
|**True**|La ruta de destino está almacenada en una variable. Al seleccionar este valor se muestra la opción dinámica **LocalVariable**.|  
|**False**|La ruta de destino se especifica en un administrador de conexiones de archivos. Al seleccionar este valor se muestra la opción dinámica **LocalPath**.|  
  
 **Operación**  
 Seleccione la operación de FTP que se realizará. Esta propiedad presenta las opciones indicadas en la siguiente tabla.  
  
|Value|Description|  
|-----------|-----------------|  
|**Enviar archivos**|Envía archivos. Al seleccionar este valor se muestran las opciones dinámicas **LocalVariable**, **LocalPathRemoteVariable** y **RemotePath**.|  
|**Recibir archivos**|Recibe archivos. Al seleccionar este valor se muestran las opciones dinámicas **LocalVariable**, **LocalPathRemoteVariable** y **RemotePath**.|  
|**Crear directorio local**|Crea un directorio local. Al seleccionar este valor se muestran las opciones dinámicas **LocalVariable** y **LocalPath**.|  
|**Crear directorio remoto**|Crea un directorio remoto. Al seleccionar este valor se muestran las opciones dinámicas **RemoteVariable** y **RemotePath**.|  
|**Quitar directorio local**|Quita un directorio local. Al seleccionar este valor se muestran las opciones dinámicas **LocalVariable** y **LocalPath**.|  
|**Quitar directorio remoto**|Quita un directorio remoto. Al seleccionar este valor se muestran las opciones dinámicas **RemoteVariable** y **RemotePath**.|  
|**Eliminar archivos locales**|Elimina archivos locales. Al seleccionar este valor se muestran las opciones dinámicas **LocalVariable** y **LocalPath**.|  
|**Eliminar archivos remotos**|Elimina archivos remotos. Al seleccionar este valor se muestran las opciones dinámicas **RemoteVariable** y **RemotePath**.|  
  
 **IsTransferASCII**  
 Indica si los archivos transferidos a y desde el servidor FTP remoto deben transferirse en modo ASCII.  
  
## <a name="isremotepathvariable-dynamic-options"></a>Opciones dinámicas de IsRemotePathVariable  
  
### <a name="isremotepathvariable--true"></a>IsRemotePathVariable = True  
 **RemoteVariable**  
 Seleccione una variable definida por el usuario existente o haga clic en \< **nueva variable...** > para crear una variable definida por el usuario.  
  
 **Temas relacionados:** [Variables de Integration Services &#40;SSIS&#41;](../../integration-services/integration-services-ssis-variables.md), Agregar variable  
  
### <a name="isremotepathvariable--false"></a>IsRemotePathVariable = False  
 **RemotePath**  
 Seleccione un administrador de conexiones FTP existente o haga clic en \< **nueva conexión...** > para crear una conexión de administrador.  
  
 **Temas relacionados**: [Administrador de conexiones FTP](../../integration-services/connection-manager/ftp-connection-manager.md), [Editor del administrador de conexiones FTP](../../integration-services/connection-manager/ftp-connection-manager-editor.md)  
  
## <a name="islocalpathvariable-dynamic-options"></a>Opciones dinámicas de IsLocalPathVariable  
  
### <a name="islocalpathvariable--true"></a>IsLocalPathVariable = True  
 **LocalVariable**  
 Seleccione una variable definida por el usuario existente o haga clic en \< **nueva variable...** > para crear una variable.  
  
 **Temas relacionados:** [Variables de Integration Services &#40;SSIS&#41;](../../integration-services/integration-services-ssis-variables.md), Agregar variable  
  
### <a name="islocalpathvariable--false"></a>IsLocalPathVariable = False  
 **LocalPath**  
 Seleccione un administrador de conexión de archivos existente o haga clic en \< **nueva conexión...** > para crear una conexión de administrador.  
  
 **Temas relacionados**: [Flat File Connection Manager](../../integration-services/connection-manager/flat-file-connection-manager.md), [File Connection Manager Editor](../../integration-services/connection-manager/file-connection-manager-editor.md)  
  
## <a name="see-also"></a>Vea también  
 [Referencia de mensajes y Error de Integration Services](../../integration-services/integration-services-error-and-message-reference.md)   
 [Editor de la tarea FTP &#40; Página general &#41;](../../integration-services/control-flow/ftp-task-editor-general-page.md)   
 [Página Expresiones](../../integration-services/expressions/expressions-page.md)  
  
  
