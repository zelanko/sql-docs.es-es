---
title: Sys.sysconfigures (Transact-SQL) | Microsoft Docs
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
manager: craigg
ms.openlocfilehash: 61936891ecd31b3bf5421a8cac49aad9f0dd37f7
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/01/2018
ms.locfileid: "47635323"
---
# <a name="syssysconfigures-transact-sql"></a>sys.sysconfigures (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Contiene una fila por cada opción de configuración establecida por un usuario. **sysconfigures** contiene las opciones de configuración definidas antes de la última operación de inicio de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], además de las opciones de configuración dinámicas establecen desde ese momento.  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssnoteCompView](../../includes/ssnotecompview-md.md)]  
  
|Nombre de columna|Tipo de datos|Descripción|  
|-----------------|---------------|-----------------|  
|**Valor**|**int**|Valor de la variable, que el usuario puede modificar. [!INCLUDE[ssDE](../../includes/ssde-md.md)] lo utiliza solo si se ha ejecutado RECONFIGURE.|  
|**configuración**|**int**|Número de la variable de configuración.|  
|**Comentario**|**nvarchar(255)**|Explicación de la opción de configuración.|  
|**status**|**smallint**|Mapa de bits que indica el estado de la opción. Entre los valores posibles figuran los siguientes:<br /><br /> 0 = Estático. Configuración surte efecto cuando se reinicia el servidor.<br /><br /> 1 = Dinámico. La variable surte efecto cuando se ejecuta la instrucción RECONFIGURE.<br /><br /> 2 = Avanzado. Se muestra la variable solo cuando el **Mostrar opciones avanzadas** está establecido. Configuración surte efecto cuando se reinicia el servidor.<br /><br /> 3 = Dinámico y avanzado.|  
  
## <a name="see-also"></a>Vea también  
 [Asignar tablas del sistema a vistas del sistema &#40;Transact-SQL&#41;](../../relational-databases/system-tables/mapping-system-tables-to-system-views-transact-sql.md)   
 [Vistas de compatibilidad &#40;Transact-SQL&#41;](~/relational-databases/system-compatibility-views/system-compatibility-views-transact-sql.md)  
  
  
