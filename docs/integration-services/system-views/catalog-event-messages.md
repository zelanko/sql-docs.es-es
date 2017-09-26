---
title: Catalog.event_messages | Documentos de Microsoft
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: language-reference
ms.assetid: a31a654f-31e9-4da1-aabf-182b07848e36
caps.latest.revision: 7
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: a0db5ace2a95bea93189cb48378b01a4ba599942
ms.contentlocale: es-es
ms.lasthandoff: 09/26/2017

---
# <a name="catalogeventmessages"></a>catalog.event_messages
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  Muestra información sobre los mensajes que se registraron durante las operaciones.  
  
|Nombre de columna|Tipo de datos|Description|  
|-----------------|---------------|-----------------|  
|Event_message_ID|bigint|Identificador único del mensaje de evento.|  
|Operation_id|bigint|El tipo de operación.<br /><br /> Para obtener una lista de tipos de operación, vea [catalog.operations &#40; Base de datos SSISDB &#41; ](../../integration-services/system-views/catalog-operations-ssisdb-database.md).|  
|Message_time|datetimeoffset(7)|Hora de creación del mensaje.|  
|Message_type|smallint|Tipo del mensaje mostrado. Para obtener más información acerca de los tipos de mensaje, consulte [catalog.operation_messages &#40; Base de datos SSISDB &#41; ](../../integration-services/system-views/catalog-operation-messages-ssisdb-database.md).|  
|Message_source_type|smallint|Origen del mensaje.|  
|message|nvarchar(max)|Texto del mensaje.|  
|Extended_info_id|bigint|El identificador de la información adicional relacionada con el mensaje de operación, se encuentra en la [catalog.extended_operation_info &#40; Base de datos SSISDB &#41; ](../../integration-services/system-views/catalog-extended-operation-info-ssisdb-database.md) vista.|  
|Package_name|nvarchar(260)|Nombre del archivo de paquete.|  
|Event_name|nvarchar (1024)|Evento de tiempo de ejecución asociado al mensaje.|  
|Message_source_name|nvarchar(4000)|Componente del paquete que constituye el origen del mensaje.|  
|Message_source_id|nvarchar(38)|Identificador único del origen del mensaje.|  
|Subcomponent_name|nvarchar(4000)|Componente de flujo de datos que es el origen del mensaje.<br /><br /> Cuando el motor de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] devuelve mensajes, aparece SSIS.Pipeline en esta columna.|  
|Package_path|nvarchar(max)|Ruta de acceso del componente dentro del paquete.|  
|Execution_path|nvarchar(max)|Ruta de acceso completa del paquete primario al punto en el que se ejecuta el componente.<br /><br /> Esta ruta de acceso también captura iteraciones de un componente.|  
|threadID|int|Identificador del subproceso que se ejecuta cuando se registra el mensaje.|  
|Message_code|int|Código asociado al mensaje.|  
  
## <a name="remarks"></a>Comentarios  
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
  
-   La pertenencia a la **ssis_admin** rol de base de datos.  
  
-   La pertenencia a la **sysadmin** rol de servidor.  
  
## <a name="see-also"></a>Vea también  
 [catalog.event_message_context](../../integration-services/system-views/catalog-event-message-context.md)  
  
  
