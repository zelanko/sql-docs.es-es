---
title: GETANSINULL (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- GETANSINULL
- GETANSINULL_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- null values [SQL Server], default
- GETANSINULL function
- default nullability
- database nullability [SQL Server]
ms.assetid: 189399e4-428d-4902-b3a8-94f07fdefc6a
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: c8343a24f892c5b0058f1bd1a7c001221c8ff65f
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "67940112"
---
# <a name="getansinull-transact-sql"></a>GETANSINULL (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Devuelve la nulabilidad predeterminada para la base de datos para esta sesión.  
  
 ![Icono de vínculo de artículo](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
GETANSINULL ( [ 'database' ] )  
```  
  
## <a name="arguments"></a>Argumentos  
 "*database*"  
 Es el nombre de la base de datos para la que se devuelve información sobre nulabilidad. *database es **char** o **nchar**. Si **char**, *database* se convierte implícitamente en **nchar**.  
  
## <a name="return-types"></a>Tipos devueltos  
 **int**  
  
## <a name="remarks"></a>Notas  
GETANSINULL devuelve 1 si la nulabilidad de la base de datos permite valores null. Este valor devuelto también requiere que la nulabilidad del tipo de dato o columna no se defina explícitamente. El valor predeterminado NULL de ANSI es 1. 
  
 Para habilitar el comportamiento predeterminado de ANSI NULL, se debe establecer una de las siguientes condiciones:  
  
-   ALTER DATABASE *database_name* SET ANSI_NULL_DEFAULT ON  
  
-   SET ANSI_NULL_DFLT_ON ON  
  
-   SET ANSI_NULL_DFLT_OFF OFF  
  
## <a name="examples"></a>Ejemplos  
 En el siguiente ejemplo se devuelve la nulabilidad predeterminada para la base de datos `AdventureWorks2012`.  
  
```  
USE AdventureWorks2012;  
GO  
SELECT GETANSINULL('AdventureWorks2012')  
GO  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
 ```
 ------  
1  

(1 row(s) affected)
 ```  
  
## <a name="see-also"></a>Consulte también  
 [Funciones del sistema &#40;Transact-SQL&#41;](../../relational-databases/system-functions/system-functions-for-transact-sql.md)  
  
  
