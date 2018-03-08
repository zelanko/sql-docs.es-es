---
title: SET PARSEONLY (Transact-SQL) | Documentos de Microsoft
ms.custom: 
ms.date: 11/27/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: t-sql|statements
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- PARSEONLY_TSQL
- SET_PARSEONLY_TSQL
- PARSEONLY
- SET PARSEONLY
dev_langs:
- TSQL
helpviewer_keywords:
- parsing [SQL Server], SET PARSEONLY statement
- checking syntax
- PARSEONLY option
- syntax [SQL Server], verifying
- verifying syntax
- SET PARSEONLY statement
ms.assetid: 514ab042-c53e-4d96-be71-fb08fcc6ef3c
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: eb009b23f9d4a751f6850218f4845c6c70c3bbd3
ms.sourcegitcommit: 531d0245f4b2730fad623a7aa61df1422c255edc
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 12/01/2017
---
# <a name="set-parseonly-transact-sql"></a>SET PARSEONLY (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-asdw-pdw-md](../../includes/tsql-appliesto-ss2008-asdb-asdw-pdw-md.md)]

  Examina la sintaxis de cada instrucción [!INCLUDE[tsql](../../includes/tsql-md.md)] y devuelve los mensajes de error sin compilar ni ejecutar la instrucción.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
SET PARSEONLY { ON | OFF }  
```  
  
## <a name="remarks"></a>Comentarios  
 Cuando SET PARSEONLY es ON, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] solo analiza la instrucción. Cuando SET PARSEONLY es OFF, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] compila y ejecuta la instrucción.  
  
 La opción SET PARSEONLY se establece en tiempo de análisis, no en tiempo de ejecución.  
  
 No debe utilizar PARSEONLY en procedimientos almacenados ni en desencadenadores. SET PARSEONLY devuelve los desplazamientos si la opción OFFSETS es ON y no hay errores.  
  
## <a name="permissions"></a>Permissions  
 Debe pertenecer al rol **public** .  
  
## <a name="see-also"></a>Vea también  
 [Instrucciones SET &#40;Transact-SQL&#41;](../../t-sql/statements/set-statements-transact-sql.md)   
 [CONJUNTO de DESPLAZAMIENTOS &#40; Transact-SQL &#41;](../../t-sql/statements/set-offsets-transact-sql.md)  
  
  
