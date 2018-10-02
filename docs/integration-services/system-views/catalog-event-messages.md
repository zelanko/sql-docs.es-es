---
title: catalog.event_messages | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: language-reference
ms.assetid: a31a654f-31e9-4da1-aabf-182b07848e36
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: ac1c56583d59c44d77a3fe6e35454f0527d94c30
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 10/01/2018
ms.locfileid: "47808783"
---
# <a name="catalogeventmessages"></a>catalog.event_messages
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  Muestra información sobre los mensajes que se registraron durante las operaciones.  
  
|Nombre de columna|Tipo de datos|Descripción|  
|-----------------|---------------|-----------------|  
|Event_message_ID|BIGINT|Identificador único del mensaje de evento.|  
|Operation_id|BIGINT|Tipo de operación.<br /><br /> Para obtener una lista de los tipos de operaciones, consulte [catalog.operations &#40;base de datos de SSISDB&#41;](../../integration-services/system-views/catalog-operations-ssisdb-database.md).|  
|Message_time|datetimeoffset(7)|Hora de creación del mensaje.|  
|Message_type|SMALLINT|Tipo del mensaje mostrado. Para obtener más información acerca de los tipos de mensaje, consulte [catalog.operation_messages &#40;base de datos de SSISDB&#41;](../../integration-services/system-views/catalog-operation-messages-ssisdb-database.md).|  
|Message_source_type|SMALLINT|Origen del mensaje.|  
|message|nvarchar(max)|Texto del mensaje.|  
|Extended_info_id|BIGINT|Es el id. de la información adicional relacionada con el mensaje de la operación, que se encuentra en la vista [catalog.extended_operation_info &#40;base de datos de SSISDB&#41;](../../integration-services/system-views/catalog-extended-operation-info-ssisdb-database.md).|  
|Package_name|nvarchar(260)|Nombre del archivo de paquete.|  
|Event_name|nvarchar(1024)|Evento de tiempo de ejecución asociado al mensaje.|  
|Message_source_name|nvarchar(4000)|Componente del paquete que constituye el origen del mensaje.|  
|Message_source_id|nvarchar(38)|Identificador único del origen del mensaje.|  
|Subcomponent_name|nvarchar(4000)|Componente de flujo de datos que es el origen del mensaje.<br /><br /> Cuando el motor de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] devuelve mensajes, aparece SSIS.Pipeline en esta columna.|  
|Package_path|nvarchar(max)|Ruta de acceso del componente dentro del paquete.|  
|Execution_path|nvarchar(max)|Ruta de acceso completa del paquete primario al punto en el que se ejecuta el componente.<br /><br /> Esta ruta de acceso también captura iteraciones de un componente.|  
|threadID|INT|Identificador del subproceso que se ejecuta cuando se registra el mensaje.|  
|Message_code|INT|Código asociado al mensaje.|  
  
## <a name="remarks"></a>Notas  
 Esta vista muestra los siguientes tipos de origen de mensaje:  
  
|**message_source_type**|Descripción|  
|-------------------------------|-----------------|  
|10|API de entrada, como procedimientos almacenados de T-SQL y CLR|  
|20|Proceso externo para ejecutar paquetes (ISServerExec.exe)|  
|30|Objetos de nivel de paquete|  
|40|Tareas de flujo de control|  
|50|Contenedores de flujo de control|  
|60|Tarea Flujo de datos|  
  
## <a name="permissions"></a>Permisos  
 Esta vista exige uno de los siguientes permisos:  
  
-   Permiso de lectura en la operación  
  
-   Pertenencia al rol de base de datos de **ssis_admin**  
  
-   Pertenencia al rol del servidor de **sysadmin**  
  
## <a name="see-also"></a>Ver también  
 [catalog.event_message_context](../../integration-services/system-views/catalog-event-message-context.md)  
  
  
