---
title: Sys.sysconstraints (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sysconstraints
- sys.sysconstraints
- sysconstraints_TSQL
- sys.sysconstraints_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.sysconstraints compatibility view
- sysconstraints system table
ms.assetid: f2b2e2ad-ba24-48a1-913c-8ee4e0895dc4
author: rothja
ms.author: jroth
ms.openlocfilehash: dfd88dec92d2707b72c829aa53f2798d3d64fee3
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "68089194"
---
# <a name="syssysconstraints-transact-sql"></a>sys.sysconstraints (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  Contiene correspondencias entre restricciones y los objetos que las poseen en la base de datos.  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssnoteCompView](../../includes/ssnotecompview-md.md)]  
  
|Nombre de columna|Tipo de datos|Descripción|  
|-----------------|---------------|-----------------|  
|**constid**|**int**|Número de restricción.|  
|**id**|**int**|Id. de la tabla que posee la restricción.|  
|**colid**|**smallint**|Id. de la columna en la que se define la restricción.<br /><br /> 0 = Restricción de tabla|  
|**spare1**|**tinyint**|Reservado|  
|**status**|**int**|Pseudomáscara de bits que indica el estado. Entre los valores posibles figuran los siguientes:<br /><br /> 1 = Restricción PRIMARY KEY<br /><br /> 2 = Restricción UNIQUE KEY<br /><br /> 3 = Restricción FOREIGN KEY<br /><br /> 4 = Restricción CHECK<br /><br /> 5 = Restricción DEFAULT<br /><br /> 16 = Restricción de nivel de columna<br /><br /> 32 = Restricción de nivel de tabla|  
|**Acciones**|**int**|Reservado|  
|**error**|**int**|Reservado|  
  
## <a name="see-also"></a>Vea también  
 [Asignar tablas del sistema a vistas del sistema &#40;Transact-SQL&#41;](../../relational-databases/system-tables/mapping-system-tables-to-system-views-transact-sql.md)   
 [Vistas de compatibilidad &#40;Transact-SQL&#41;](~/relational-databases/system-compatibility-views/system-compatibility-views-transact-sql.md)  
  
  
