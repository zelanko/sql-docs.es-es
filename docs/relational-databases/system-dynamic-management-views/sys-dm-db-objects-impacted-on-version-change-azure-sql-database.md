---
title: Sys.dm_db_objects_impacted_on_version_change (base de datos de SQL Azure) | Documentos de Microsoft
ms.custom: ''
ms.date: 03/03/2017
ms.prod: ''
ms.prod_service: sql-database
ms.reviewer: ''
ms.service: sql-database
ms.component: dmv's
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sys.dm_db_objects_impacted_on_version_change_TSQL
- dm_db_objects_impacted_on_version_change
- dm_db_objects_impacted_on_version_change_TSQL
- sys.dm_db_objects_impacted_on_version_change
dev_langs:
- TSQL
helpviewer_keywords:
- dm_db_objects_impacted_on_version_change
- sys.dm_db_objects_impacted_on_version_change
ms.assetid: b94af834-c4f6-4a27-80a6-e8e71fa8793a
caps.latest.revision: 9
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
monikerRange: = azuresqldb-current || = sqlallproducts-allversions
ms.openlocfilehash: 404b686128406f912908e1b27d8e4e05f22be42f
ms.sourcegitcommit: bb044a48a6af9b9d8edb178dc8c8bd5658b9ff68
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/18/2018
---
# <a name="sysdmdbobjectsimpactedonversionchange-azure-sql-database"></a>sys.dm_db_objects_impacted_on_version_change (Azure SQL Database)
[!INCLUDE[tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md.md)]

  Esta vista del sistema con ámbito de base de datos está diseñada para proporcionar un sistema de alerta rápida que permita determinar los objetos que se verán afectados por una actualización de versión importante en [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]. Puede utilizar la vista antes o después de la actualización para obtener una enumeración completa de los objetos afectados. Tendrá que consultar esta vista en cada base de datos para obtener una perspectiva completa de todo el servidor.  
  
|Nombre de columna|Tipo de datos|Description|  
|-----------------|---------------|-----------------|  
|class|**int** NOT NULL|La clase del objeto que se verá afectado:<br /><br /> **1** = restricción<br /><br /> **7** = índices y montones|  
|class_desc|**nvarchar (60)** no NULL|Descripción de la clase:<br /><br /> **OBJECT_OR_COLUMN**<br /><br /> **INDEX**|  
|major_id|**int** NOT NULL|Identificador de objeto de la restricción, o identificador de objeto de la tabla que contiene el índice o el montón.|  
|minor_id|**int** NULL|**NULL** para restricciones<br /><br /> Index_id para índices y montones|  
|dependency|**nvarchar (60)** no NULL|Descripción de la dependencia que está afectando a una restricción o a un índice. El mismo valor también se utiliza para las advertencias generadas durante la actualización.<br /><br /> Ejemplos:<br /><br /> **espacio** (para la función intrínseca)<br /><br /> **geometría** (para UDT del sistema)<br /><br /> **Geography:: Parse** (para el método UDT del sistema)|  
  
## <a name="permissions"></a>Permissions  
 Necesita el permiso VIEW DATABASE STATE.  
  
## <a name="example"></a>Ejemplo  
 En el ejemplo siguiente se muestra una consulta en **sys.dm_db_objects_impacted_on_version_change** para buscar los objetos afectados por una actualización a la siguiente versión principal del servidor  
  
```  
SELECT * FROM sys.dm_db_objects_disabled_on_version_change;  
GO  
```  
  
```  
class  class_desc        major_id    minor_id    dependency                       
------ ----------------- ----------- ----------- ----------   
1      OBJECT_OR_COLUMN  181575685   NULL        geometry                        
7      INDEX             37575172    1           geometry                        
7      INDEX             2121058592  1           geometry                        
1      OBJECT_OR_COLUMN  101575400   NULL        geometry     
```  
  
## <a name="remarks"></a>Comentarios  
  
### <a name="how-to-update-impacted-objects"></a>Cómo actualizar los objetos afectados  
 Los pasos ordenados siguientes describen la acción correctiva que se deberá realizar después de la próxima actualización de versión de servicio del mes de junio.  
  
|Pedido de|Objeto afectado|Acción correctora|  
|-----------|---------------------|-----------------------|  
|1|**Índices**|Volver a generar los índices identificados mediante **sys.dm_db_objects_impacted_on_version_change** por ejemplo:  `ALTER INDEX ALL ON <table> REBUILD`<br />o bien<br />`ALTER TABLE <table> REBUILD`|  
|2|**Objeto**|Todas las restricciones identificadas por **sys.dm_db_objects_impacted_on_version_change** debe volver a validarse tras se vuelve a calcular los datos de geometría y geografía de la tabla subyacente. Para las restricciones, vuelva a realizar la validación mediante ALTER TABLE. <br />Por ejemplo: <br />`ALTER TABLE <tab> WITH CHECK CHECK CONSTRAINT <constraint name>`<br />o bien<br />`ALTER TABLE <tab> WITH CHECK CONSTRAINT ALL`|  
  
  
