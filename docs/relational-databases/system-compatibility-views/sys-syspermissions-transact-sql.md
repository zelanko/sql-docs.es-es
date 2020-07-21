---
title: Permisos de sys.sys(Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.syspermissions_TSQL
- syspermissions_TSQL
- sys.syspermissions
- syspermissions
dev_langs:
- TSQL
helpviewer_keywords:
- syspermissions system table
- sys.syspermissions compatibility view
ms.assetid: ba9a9a88-55d2-41a7-b09b-342e8b9a54c5
author: rothja
ms.author: jroth
ms.openlocfilehash: f28ff4a642b1772d7aee921b6047e81a3b306a5b
ms.sourcegitcommit: f7ac1976d4bfa224332edd9ef2f4377a4d55a2c9
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/02/2020
ms.locfileid: "85897352"
---
# <a name="syssyspermissions-transact-sql"></a>sys.syspermissions (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  Contiene información sobre los permisos concedidos y denegados a los usuarios, grupos y roles de la base de datos.  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssnoteCompView](../../includes/ssnotecompview-md.md)]  
  
|Nombre de la columna|Tipo de datos|Descripción|  
|-----------------|---------------|-----------------|  
|**id**|**int**|Id. del objeto para los permisos de objeto.<br /><br /> 0 = Permisos de instrucciones.|  
|**receptores**|**smallint**|Id. del usuario, grupo o rol afectado por el permiso.|  
|**otorgante**|**smallint**|Id. del usuario, grupo o rol que concede o deniega el permiso.|  
|**actadd**|**smallint**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**actmod**|**smallint**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**seladd**|**varbinary (4000)**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**selmod**|**varbinary (4000)**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**updadd**|**varbinary (4000)**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**updmod**|**varbinary (4000)**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**refadd**|**varbinary (4000)**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**refmod**|**varbinary (4000)**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
  
## <a name="see-also"></a>Consulte también  
 [Asignar tablas del sistema a vistas del sistema &#40;Transact-SQL&#41;](../../relational-databases/system-tables/mapping-system-tables-to-system-views-transact-sql.md)   
 [Vistas de compatibilidad &#40;Transact-SQL&#41;](~/relational-databases/system-compatibility-views/system-compatibility-views-transact-sql.md)  
  
  
