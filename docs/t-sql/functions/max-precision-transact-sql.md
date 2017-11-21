---
title: '@@MAX_PRECISION (Transact-SQL) | Documentos de Microsoft'
ms.custom: 
ms.date: 09/18/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: t-sql|functions
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- '@@MAX_PRECISION_TSQL'
- '@@MAX_PRECISION'
dev_langs:
- TSQL
helpviewer_keywords:
- precision [SQL Server], @@MAX_PRECISION
- numeric data type, precision level
- decimal data type, precision level
- '@@MAX_PRECISION function'
- data types [SQL Server], precision
ms.assetid: 9e7158a1-e503-422a-b326-3c9b06e181b2
caps.latest.revision: 30
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: c6ea46c5187f00190cb39ba9a502b3ecb6a28bc6
ms.openlocfilehash: 530dc9cd780d9dae2df1c326fcd1cc070450290a
ms.contentlocale: es-es
ms.lasthandoff: 09/19/2017

---
# <a name="x40x40maxprecision-transact-sql"></a>& #x 40; & #x 40; MAX_PRECISION (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Devuelve el nivel de precisión utilizado por **decimal** y **numérico** tipos de datos según lo establecen actualmente en el servidor.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
@@MAX_PRECISION  
```  
  
## <a name="return-types"></a>Tipos devueltos  
 **tinyint**  
  
## <a name="remarks"></a>Comentarios  
 De manera predeterminada, la precisión máxima devuelve 38.  
  
## <a name="examples"></a>Ejemplos  
  
```  
SELECT @@MAX_PRECISION AS 'Max Precision'  
```  
  
## <a name="see-also"></a>Vea también  
 [Funciones de configuración &#40;Transact-SQL&#41;](../../t-sql/functions/configuration-functions-transact-sql.md)   
 [decimal y numeric &#40; Transact-SQL &#41;](../../t-sql/data-types/decimal-and-numeric-transact-sql.md)   
 [Precisión, escala y longitud &#40; Transact-SQL &#41;](../../t-sql/data-types/precision-scale-and-length-transact-sql.md)  
  
  

