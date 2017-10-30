---
title: Catalog.operation_messages (base de datos de SSISDB) | Documentos de Microsoft
ms.custom: 
ms.date: 03/03/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: language-reference
helpviewer_keywords:
- catalog.operation_messages view [Integration Services]
- operation_messages view [Integration Services]
ms.assetid: 0b3cbe38-ce24-47ca-83ef-6538a5299d1a
caps.latest.revision: 27
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 235e9896cbf075bdc26e3df120b23091b8e82d6d
ms.contentlocale: es-es
ms.lasthandoff: 09/26/2017

---
# <a name="catalogoperationmessages-ssisdb-database"></a>catalog.operation_messages (base de datos de SSISDB)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  Muestra los mensajes registrados durante las operaciones del catálogo de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)].  
  
|Nombre de columna|Tipo de datos|Description|  
|-----------------|---------------|-----------------|  
|operation_message_id|**bigint**|El identificador único (ID) del mensaje.|  
|operation_id|**bigint**|El identificador único de la operación.|  
|message_time|**DateTimeOffset(7)**|La hora cuando se creó el mensaje.|  
|message_type|**smallint**|Tipo del mensaje mostrado.|  
|message_source_type|**smallint**|El identificador del tipo de origen del mensaje.|  
|message|**nvarchar(max)**|Texto del mensaje.|  
|extended_info_id|**bigint**|El identificador de la información adicional relacionada con el mensaje de operación, se encuentra en la [extended_operation_info](../../integration-services/system-views/catalog-extended-operation-info-ssisdb-database.md) vista.|  
  
## <a name="remarks"></a>Comentarios  
 Esta vista muestra una fila para cada mensaje registrado durante una operación en el catálogo. El mensaje lo puede genera el servidor, el proceso de ejecución del paquete o el motor de ejecución.  
  
 Esta vista muestra los siguientes tipos de mensaje:  
  
|**message_type** valor|Description|  
|-----------------------------|-----------------|  
|-1|Desconocido|  
|120|Error|  
|110|Advertencia|  
|70|Información|  
|10|Validación previa|  
|20|Validación posterior|  
|30|Ejecución previa|  
|40|Ejecución posterior|  
|60|Progreso|  
|50|StatusChange|  
|100|QueryCancel|  
|130|TaskFailed|  
|90|Diagnostic|  
|200|Personalizado|  
|140|DiagnosticEx<br /><br /> Siempre que una tarea Ejecutar paquete ejecuta un paquete secundario, registra este evento. El mensaje de evento consta de los valores de los parámetros pasados a los paquetes secundarios.<br /><br /> El valor de la columna de mensaje para DiagnosticEx es texto XML.|  
|400|NonDiagnostic|  
|80|VariableValueChanged|  
  
 Esta vista muestra los siguientes tipos de origen de mensaje:  
  
|**message_source_type**|Description|  
|-------------------------------|-----------------|  
|10|API de entrada, como procedimientos almacenados de T-SQL y CLR|  
|20|Proceso externo para ejecutar paquetes (ISServerExec.exe)|  
|30|Objetos de nivel de paquete|  
|40|Tareas de flujo de control|  
|50|Contenedores de flujo de control|  
|60|Tarea flujo de datos|  
  
## <a name="permissions"></a>Permissions  
 Esta vista exige uno de los siguientes permisos:  
  
-   Permiso de lectura en la operación  
  
-   La pertenencia a la **ssis_admin** rol de base de datos  
  
-   La pertenencia a la **sysadmin** rol de servidor  
  
> [!NOTE]  
>  Cuando se dispone de permiso para realizar una operación en el servidor, también se dispone de permiso para ver información sobre la operación. Se aplica la seguridad en el nivel de fila; solo se muestran las filas para las que disponga de permiso para ver.  
  
  

