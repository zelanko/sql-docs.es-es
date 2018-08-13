---
title: sp_prepare (Transact SQL) | Microsoft Docs
ms.custom: ''
ms.date: 02/28/2018
ms.prod: sql
ms.prod_service: database-engine, sql-data-warehouse, pdw
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sp_cursor_prepare_TSQL
- sp_cursor_prepare
dev_langs:
- TSQL
helpviewer_keywords:
- sp_prepare
ms.assetid: f328c9eb-8211-4863-bafa-347e1bf7bb3f
caps.latest.revision: 9
author: edmacauley
ms.author: edmaca
manager: craigg
monikerRange: '>=aps-pdw-2016||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017'
ms.openlocfilehash: 896894b05823cdfeaa1efa3cda7c341a7fa9f010
ms.sourcegitcommit: 4cd008a77f456b35204989bbdd31db352716bbe6
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/06/2018
ms.locfileid: "39535355"
---
# <a name="spprepare-transact-sql"></a>sp_prepare (Transact SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-ss2008-xxxx-asdw-pdw-md.md)]

  Prepara un parametrizada [!INCLUDE[tsql](../../includes/tsql-md.md)] instrucción y devuelve una instrucción *controlar* para su ejecución. sp_prepare se invoca especificando el identificador 11 en un paquete de flujo TDS.  
  
 ![Icono de vínculo de artículo](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
sp_prepare handle OUTPUT, params, stmt, options  
```  
  
## <a name="arguments"></a>Argumentos  
 *identificador*  
 Es un generado por SQL Server *identificador preparado* identificador. *controlar* es un parámetro necesario con un **int** valor devuelto.  
  
 *params*  
 Identifica instrucciones con parámetros. El *params* definición de las variables se sustituye por marcadores de parámetros en la instrucción. *params* es un parámetro necesario que requiere un **ntext**, **nchar**, o **nvarchar** valor de entrada. Escriba un valor NULL si la instrucción no tiene parámetros.  
  
 *stmt*  
 Define el conjunto de resultados del cursor. El *stmt* parámetro es necesario y requiere un **ntext**, **nchar**, o **nvarchar** valor de entrada.  
  
 *options*  
 Parámetro opcional que devuelve una descripción de las columnas del conjunto de resultados del cursor. *Opciones de* requiere el siguiente valor de entrada de tipo int:  
  
|Valor|Descripción|  
|-----------|-----------------|  
|0x0001|RETURN_METADATA|  
  
## <a name="examples"></a>Ejemplos  
 En el ejemplo siguiente se prepara y se ejecuta una instrucción sencilla.  
  
```  
Declare @P1 int;  
Exec sp_prepare @P1 output,   
    N'@P1 nvarchar(128), @P2 nvarchar(100)',  
    N'SELECT database_id, name FROM sys.databases WHERE name=@P1 AND state_desc = @P2';  
Exec sp_execute @P1, N'tempdb', N'ONLINE';  
EXEC sp_unprepare @P1;  
```  

  
## <a name="see-also"></a>Vea también  
 [Procedimientos almacenados del sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  

