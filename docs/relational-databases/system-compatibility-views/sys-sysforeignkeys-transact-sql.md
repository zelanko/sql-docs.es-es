---
description: sys.sysforeignkeys (Transact-SQL)
title: sys.sysforeignkeys (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sysforeignkeys
- sys.sysforeignkeys
- sys.sysforeignkeys_TSQL
- sysforeignkeys_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sysforeignkeys system table
- sys.sysforeignkeys compatibility view
ms.assetid: 41544236-1c46-4501-be88-18c06963b6e8
author: rothja
ms.author: jroth
ms.openlocfilehash: 15a02ec0dc5b6b1e5b376876b18e36863468e59e
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/17/2020
ms.locfileid: "88455108"
---
# <a name="syssysforeignkeys-transact-sql"></a>sys.sysforeignkeys (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  Contiene información sobre las restricciones FOREIGN KEY que se incluyen en las definiciones de las tablas de la base de datos.  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssnoteCompView](../../includes/ssnotecompview-md.md)]  
  
|Nombre de la columna|Tipo de datos|Descripción|  
|-----------------|---------------|-----------------|  
|**constid**|**int**|Id. de la restricción FOREIGN KEY.|  
|**fkeyid**|**int**|Id. de objeto de la tabla con la restricción FOREIGN KEY.|  
|**rkeyid**|**int**|Id. de objeto de la tabla a la que se hace referencia en la restricción FOREIGN KEY.|  
|**fkey**|**smallint**|Id. de la columna que hace la referencia.|  
|**rkey**|**smallint**|Id. de la columna a la que se hace referencia.|  
|**keyno**|**smallint**|Posición de la columna en la lista de columnas de referencia.|  
  
## <a name="see-also"></a>Consulte también  
 [Asignar tablas del sistema a vistas del sistema &#40;Transact-SQL&#41;](../../relational-databases/system-tables/mapping-system-tables-to-system-views-transact-sql.md)   
 [Vistas de compatibilidad &#40;Transact-SQL&#41;](~/relational-databases/system-compatibility-views/system-compatibility-views-transact-sql.md)  
  
  
