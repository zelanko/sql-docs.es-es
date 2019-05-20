---
title: catalog.event_message_context | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: language-reference
ms.assetid: 273a54f8-b107-4f36-9461-2b475644760d
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: d230b60b204d775e4a5329392960917c28b7c32d
ms.sourcegitcommit: fd71d04a9d30a9927cbfff645750ac9d5d5e5ee7
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/16/2019
ms.locfileid: "65715121"
---
# <a name="catalogeventmessagecontext"></a>catalog.event_message_context 

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  Muestra información sobre las condiciones asociadas a los mensajes de eventos de ejecución, para las ejecuciones en el servidor [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)].  
  
|Nombre de columna|Tipo de datos|Descripción|  
|-----------------|---------------|-----------------|  
|Context_id|BIGINT|Identificador único del contexto del error.|  
|Event_message_id|BIGINT|Identificador único del mensaje con el que el contexto se relaciona.|  
|Context_depth|INT|A medida que la profundidad aumenta, el contexto se elija del error. Cuando se produce un error, la profundidad del contexto comienza en 1. El valor 0 indica el estado del paquete antes de que se inicie la ejecución.|  
|Package_path|Nvarchar(max)|Ruta de acceso del origen del contexto.|  
|Context_type|SMALLINT|Tipo del objeto que es el origen del contexto. Consulte la sección **Comentarios** para obtener una lista de tipos de contexto.|  
|Context_source_name|Nvarchar(4000)|Nombre del objeto que es el origen del contexto.|  
|Context_source_id|Nvarchar(38)|Identificador único del objeto que es el origen del contexto.|  
|Property_name|Nvarchar(4000)|Nombre de la propiedad asociada al origen del contexto.|  
|Property_value|Sql_variant|Valor de la propiedad asociada al origen del contexto.|  
  
## <a name="remarks"></a>Notas  
 En la tabla siguiente se muestran los tipos de contexto.  
  
||||  
|-|-|-|  
|Valor de tipo de contexto|Nombre del tipo|Descripción|  
|10|Tarea|Estado de una tarea cuando se produjo un error.|  
|20|Canalización|Error de un componente de canalización: componente de origen, de destino o de transformación.|  
|30|Secuencia|Estado de una secuencia.|  
|40|Bucle For|Estado de un bucle For.|  
|50|Bucle Foreach|Estado de un bucle Foreach.|  
|60|Paquete|Estado del paquete cuando se produjo un error.|  
|70|Variable|Valor variable|  
|80|Administrador de conexiones|Propiedades de un administrador de conexiones.|  
  
## <a name="permissions"></a>Permisos  
 Esta vista exige uno de los siguientes permisos:  
  
-   Permiso de lectura en la operación  
  
-   Pertenencia al rol de base de datos de **ssis_admin**  
  
-   Pertenencia al rol del servidor de **sysadmin**  
  
  
