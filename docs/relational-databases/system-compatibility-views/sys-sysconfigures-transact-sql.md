---
description: sys.sysconfigures (Transact-SQL)
title: sys.sysconfigura (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.sysconfigures
- sysconfigures
- sys.sysconfigures_TSQL
- sysconfigures_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.sysconfigures compatibility view
- sysconfigures system table
ms.assetid: 146bf10a-c898-4676-a2a1-673fb1cee7a2
author: rothja
ms.author: jroth
ms.openlocfilehash: f67d5742c5de1f806194090ebe366693cc8c9457
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/17/2020
ms.locfileid: "88482206"
---
# <a name="syssysconfigures-transact-sql"></a>sys.sysconfigures (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  Contiene una fila por cada opción de configuración establecida por un usuario. debajo **contiene las** opciones de configuración que se definen antes del inicio más reciente de, además de las [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Opciones de configuración dinámicas establecidas desde entonces.  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssnoteCompView](../../includes/ssnotecompview-md.md)]  
  
|Nombre de la columna|Tipo de datos|Descripción|  
|-----------------|---------------|-----------------|  
|**value**|**int**|Valor de la variable, que el usuario puede modificar. [!INCLUDE[ssDE](../../includes/ssde-md.md)] lo utiliza solo si se ha ejecutado RECONFIGURE.|  
|**config**|**int**|Número de la variable de configuración.|  
|**comment**|**nvarchar(255)**|Explicación de la opción de configuración.|  
|**status**|**smallint**|Mapa de bits que indica el estado de la opción. Entre los valores posibles figuran los siguientes:<br /><br /> 0 = Estático. La configuración surte efecto cuando se reinicia el servidor.<br /><br /> 1 = Dinámico. La variable surte efecto cuando se ejecuta la instrucción RECONFIGURE.<br /><br /> 2 = Avanzado. La variable solo se muestra cuando se establece la **opción Mostrar opciones avanzadas** . La configuración surte efecto cuando se reinicia el servidor.<br /><br /> 3 = Dinámico y avanzado.|  
  
## <a name="see-also"></a>Consulte también  
 [Asignar tablas del sistema a vistas del sistema &#40;Transact-SQL&#41;](../../relational-databases/system-tables/mapping-system-tables-to-system-views-transact-sql.md)   
 [Vistas de compatibilidad &#40;Transact-SQL&#41;](~/relational-databases/system-compatibility-views/system-compatibility-views-transact-sql.md)  
  
  
