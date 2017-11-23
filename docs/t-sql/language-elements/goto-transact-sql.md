---
title: GOTO (Transact-SQL) | Documentos de Microsoft
ms.custom: 
ms.date: 03/15/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: t-sql|language-elements
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- GOTO
- GOTO_TSQL
dev_langs: TSQL
helpviewer_keywords:
- skipping statements
- Transact-SQL statements, skipping
- labels [SQL Server]
- statements [SQL Server], skipping
- GOTO statement
ms.assetid: 589b6f8e-dc80-416f-9e74-48bed5337f58
caps.latest.revision: "33"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: 9dbabcc0fe5f9573554384549023ab8395b87762
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/17/2017
---
# <a name="goto-transact-sql"></a>GOTO (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Altera el flujo de ejecución y lo dirige a una etiqueta. Las instrucciones [!INCLUDE[tsql](../../includes/tsql-md.md)] que siguen a una instrucción GOTO se pasan por alto y el procesamiento continúa en el punto que marca la etiqueta. Las instrucciones GOTO y las etiquetas se pueden utilizar en cualquier punto de un procedimiento, lote o bloque de instrucciones. Las instrucciones GOTO se pueden anidar.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
Define the label:   
label:   
Alter the execution:  
GOTO label   
```  
  
## <a name="arguments"></a>Argumentos  
 *etiqueta*  
 Es el punto tras el que comienza el procesamiento cuando una instrucción GOTO especifica esa etiqueta. Las etiquetas deben cumplir las reglas de [identificadores](../../relational-databases/databases/database-identifiers.md). Una etiqueta puede servir para comentar si se utiliza GOTO.  
  
## <a name="remarks"></a>Comentarios  
 GOTO puede aparecer dentro de las instrucciones de control de flujo condicional, en bloques de instrucciones o en procedimientos, pero no se puede dirigir a una etiqueta externa al lote. La ramificación con GOTO se puede dirigir a una etiqueta definida antes o después de la instrucción GOTO.  
  
## <a name="permissions"></a>Permissions  
 De forma predeterminada, cualquier usuario válido puede utilizar GOTO.  
  
## <a name="examples"></a>Ejemplos  
 En el ejemplo siguiente se muestra cómo usar `GOTO` como mecanismo de bifurcación.  
  
```  
DECLARE @Counter int;  
SET @Counter = 1;  
WHILE @Counter < 10  
BEGIN   
    SELECT @Counter  
    SET @Counter = @Counter + 1  
    IF @Counter = 4 GOTO Branch_One --Jumps to the first branch.  
    IF @Counter = 5 GOTO Branch_Two  --This will never execute.  
END  
Branch_One:  
    SELECT 'Jumping To Branch One.'  
    GOTO Branch_Three; --This will prevent Branch_Two from executing.  
Branch_Two:  
    SELECT 'Jumping To Branch Two.'  
Branch_Three:  
    SELECT 'Jumping To Branch Three.';  
```  
  
## <a name="see-also"></a>Vea también  
 [Lenguaje de control de flujo &#40; Transact-SQL &#41;](~/t-sql/language-elements/control-of-flow.md)   
 [BEGIN... Terminar &#40; Transact-SQL &#41;](../../t-sql/language-elements/begin-end-transact-sql.md)   
 [SALTO de &#40; Transact-SQL &#41;](../../t-sql/language-elements/break-transact-sql.md)   
 [Continuar &#40; Transact-SQL &#41;](../../t-sql/language-elements/continue-transact-sql.md)   
 [IF... ELSE &#40; Transact-SQL &#41;](../../t-sql/language-elements/if-else-transact-sql.md)   
 [WAITFOR &#40; Transact-SQL &#41;](../../t-sql/language-elements/waitfor-transact-sql.md)   
 [WHILE &#40;Transact-SQL&#41;](../../t-sql/language-elements/while-transact-sql.md)  
  
  
