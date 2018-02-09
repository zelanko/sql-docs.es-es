---
title: Sys.sysprotects (Transact-SQL) | Documentos de Microsoft
ms.custom: 
ms.date: 03/15/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-compatibility-views
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sysprotects
- sys.sysprotects_TSQL
- sys.sysprotects
- sysprotects_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.sysprotects compatibility view
- sysprotects system table
ms.assetid: 49c9658d-fb51-4c77-94a0-fba699b0102d
caps.latest.revision: 
author: rothja
ms.author: jroth
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: abde43e1d699c32b2a9cd21459d823692952e059
ms.sourcegitcommit: acab4bcab1385d645fafe2925130f102e114f122
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/09/2018
---
# <a name="syssysprotects-transact-sql"></a>sys.sysprotects (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Contiene información sobre los permisos aplicados a las cuentas de seguridad de la base de datos mediante las instrucciones GRANT y DENY.  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssnoteCompView](../../includes/ssnotecompview-md.md)]  
  
|Nombre de columna|Tipo de datos|Description|  
|-----------------|---------------|-----------------|  
|**id**|**int**|Id. del objeto al que se aplican estos permisos.|  
|**uid**|**smallint**|Id. del usuario o grupo al que se aplican estos permisos. Produce un desbordamiento o devuelve NULL si el número de usuarios y roles es superior a 32.767.|  
|**acción**|**tinyint**|Puede tener uno de los permisos siguientes:<br /><br /> 26 = REFERENCES <br /><br /> 178 = CREATE FUNCTION <br /><br /> 193 = SELECT <br /><br /> 195 = INSERCIÓN<br /><br /> 196 = ELIMINAR<br /><br /> 197 = ACTUALIZAR<br /><br /> 198 = CREATE TABLE <br /><br /> 203 = CREATE DATABASE <br /><br /> 207 = CREATE VIEW <br /><br /> 222 = CREATE PROCEDURE <br /><br /> 224 = EXECUTE <br /><br /> 228 = BACKUP DATABASE <br /><br /> 233 = CREATE DEFAULT <br /><br /> 235 = BACKUP LOG <br /><br /> 236 = CREATE RULE|  
|**protecttype**|**tinyint**|Puede tener los valores siguientes:<br /><br /> 204 = GRANT_W_GRANT <br /><br /> 205 = GRANT <br /><br /> 206 = DENY|  
|**columns**|**varbinary(8000)**|Mapa de bits de las columnas a las que se aplican estos permisos SELECT o UPDATE.<br /><br /> Bit 0 = Todas las columnas.<br /><br /> Bit 1 = Los permisos se aplican a esa columna.<br /><br /> NULL = No hay información.|  
|**grantor**|**smallint**|Id. del usuario que ha concedido los permisos GRANT o DENY. Produce un desbordamiento o devuelve NULL si el número de usuarios y roles es superior a 32.767.|  
  
## <a name="see-also"></a>Vea también  
 [Asignar tablas del sistema a vistas del sistema &#40; Transact-SQL &#41;](../../relational-databases/system-tables/mapping-system-tables-to-system-views-transact-sql.md)   
 [Vistas de compatibilidad &#40;Transact-SQL&#41;](~/relational-databases/system-compatibility-views/system-compatibility-views-transact-sql.md)  
  
  
