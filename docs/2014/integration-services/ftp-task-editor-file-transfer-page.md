---
title: Editor de la tarea FTP (página transferencia de archivos) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.ftptask.filetransfer.f1
helpviewer_keywords:
- File Transfer Protocol Task Editor
ms.assetid: 37e52220-feb2-474c-ad88-fa1b1059acd4
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: a7797245901cd4d01f82995defcf44498fba1e1f
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "62894073"
---
# <a name="ftp-task-editor-file-transfer-page"></a>Editor de la tarea FTP (página Transferencia de archivos)
  Use la página **Transferencia de archivos** del cuadro de diálogo **Editor de la tarea FTP** para configurar la operación de FTP que realiza la tarea.  
  
 Para más información sobre esta tarea, vea [Tarea FTP](control-flow/ftp-task.md).  
  
## <a name="options"></a>Opciones  
 **IsRemotePathVariable**  
 Indica si la ruta remota se almacena en una variable. Esta propiedad presenta las opciones indicadas en la siguiente tabla.  
  
|Valor|Descripción|  
|-----------|-----------------|  
|**True**|La ruta de destino está almacenada en una variable. Al seleccionar este valor se muestra la opción dinámica **RemoteVariable**.|  
|**False**|La ruta de destino se especifica en un administrador de conexiones de archivos. Al seleccionar este valor se muestra la opción dinámica **RemotePath**.|  
  
 **OverwriteFileAtDestination**  
 Especifica si se puede sobrescribir un archivo del destino.  
  
 **IsLocalPathVariable**  
 Indica si la ruta de acceso local está almacenada en una variable. Esta propiedad presenta las opciones indicadas en la siguiente tabla.  
  
|Valor|Descripción|  
|-----------|-----------------|  
|**True**|La ruta de destino está almacenada en una variable. Al seleccionar este valor se muestra la opción dinámica **LocalVariable**.|  
|**False**|La ruta de destino se especifica en un administrador de conexiones de archivos. Al seleccionar este valor se muestra la opción dinámica **LocalPath**.|  
  
 **Operación**  
 Seleccione la operación de FTP que se realizará. Esta propiedad presenta las opciones indicadas en la siguiente tabla.  
  
|Valor|Descripción|  
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
 Seleccione una variable existente definida por el usuario o haga clic en \<**Nueva variable...**> para crear una.  
  
 **Temas relacionados:** [Variables de Integration Services &#40;SSIS&#41;](integration-services-ssis-variables.md), Agregar variable  
  
### <a name="isremotepathvariable--false"></a>IsRemotePathVariable = False  
 **RemotePath**  
 Seleccione un administrador de conexiones FTP existente o haga clic en \<**Nueva conexión...**> para crear uno nuevo.  
  
 **Temas relacionados:** [Administrador de conexiones FTP](connection-manager/ftp-connection-manager.md), [Editor del administrador de conexiones FTP](../../2014/integration-services/ftp-connection-manager-editor.md)  
  
## <a name="islocalpathvariable-dynamic-options"></a>Opciones dinámicas de IsLocalPathVariable  
  
### <a name="islocalpathvariable--true"></a>IsLocalPathVariable = True  
 **LocalVariable**  
 Seleccione una variable existente definida por el usuario o haga clic en \<**Nueva variable...**> para crear una.  
  
 **Temas relacionados:** [Variables de Integration Services &#40;SSIS&#41;](integration-services-ssis-variables.md), Agregar variable  
  
### <a name="islocalpathvariable--false"></a>IsLocalPathVariable = False  
 **LocalPath**  
 Seleccione un administrador de conexiones de archivos existente, o bien haga clic en \<**Nueva conexión…**> para crear uno.  
  
 **Temas relacionados**: [Administrador de conexiones de archivos planos](connection-manager/file-connection-manager.md), [Editor del Administrador de conexiones de archivos](../../2014/integration-services/file-connection-manager-editor.md)  
  
## <a name="see-also"></a>Vea también  
 [Referencia de errores y mensajes de Integration Services](../../2014/integration-services/integration-services-error-and-message-reference.md)   
 [Editor de la tarea FTP &#40;página General&#41;](general-page-of-integration-services-designers-options.md)   
 [Página Expresiones](expressions/expressions-page.md)  
  
  
