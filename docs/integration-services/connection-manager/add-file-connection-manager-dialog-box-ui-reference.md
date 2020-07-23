---
title: Referencia de la interfaz de usuario del cuadro de diálogo Agregar administrador de conexiones de archivos | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.dts.designer.fileconnection.f1
helpviewer_keywords:
- Add File Connection Manager
ms.assetid: 9370bfb5-5993-4ad8-a9cd-2de53f320f34
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 226dd6c94787af8c32d17cd7bf923a860645c5ac
ms.sourcegitcommit: c8e1553ff3fdf295e8dc6ce30d1c454d6fde8088
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/22/2020
ms.locfileid: "86921726"
---
# <a name="add-file-connection-manager-dialog-box-ui-reference"></a>Referencia de la interfaz de usuario del cuadro de diálogo Agregar administrador de conexiones de archivos

[!INCLUDE[sqlserver-ssis](../../includes/applies-to-version/sqlserver-ssis.md)]


  Utilice el cuadro de diálogo **Agregar administrador de conexiones de archivos** para definir una conexión a un grupo de archivos o carpetas.  
  
 Para obtener más información acerca del administrador de conexiones de varios archivos, vea [Multiple Files Connection Manager](../../integration-services/connection-manager/multiple-files-connection-manager.md).  
  
> [!NOTE]  
>  Las tareas integradas y componentes de flujo de datos en [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] no usan el administrador de conexiones de varios archivos. Sin embargo, puede usar este administrador de conexiones en la tarea Script o en el componente de script.  
  
## <a name="options"></a>Opciones  
 **Tipo de uso**  
 Especifique el tipo de archivo que va a utilizar para el administrador de conexiones de varios archivos.  
  
|Value|Descripción|  
|-----------|-----------------|  
|**Crear archivos**|El administrador de conexiones creará los archivos.|  
|**Archivos existentes**|El administrador de conexiones utilizará archivos existentes.|  
|**Crear carpetas**|El administrador de conexiones creará las carpetas.|  
|**Carpetas existentes**|El administrador de conexiones utilizará carpetas existentes.|  
  
 **Archivos/Carpetas**  
 Muestra los archivos o carpetas que se han agregado mediante los botones descritos a continuación.  
  
 **Add (Agregar)**  
 Agregue un archivo desde el cuadro de diálogo **Seleccionar archivos** o agregue una carpeta desde el cuadro de diálogo **Buscar carpeta** .  
  
 **Edición**  
 Seleccione un archivo o una carpeta y reemplácelos con un archivo o una carpeta diferentes desde el cuadro de diálogo **Seleccionar archivos** o **Buscar carpeta** , respectivamente.  
  
 **Remove**  
 Seleccione un archivo o una carpeta y quítelos de la lista con el botón **Quitar** .  
  
 **Botones de flecha**  
 Seleccione un archivo o una carpeta y utilice los botones de flecha para subirlos o bajarlos y especificar la secuencia de acceso.  
  
## <a name="see-also"></a>Consulte también  
 [Referencia de errores y mensajes de Integration Services](../../integration-services/integration-services-error-and-message-reference.md)  
  
  
