---
title: -- (Comentarios) (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 07/25/2019
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- --_TSQL
- Comment
- --
dev_langs:
- TSQL
helpviewer_keywords:
- nonexecuting text strings [SQL Server]
- remarks [SQL Server]
- -- (comment character)
- comments [SQL Server]
ms.assetid: 676ea8c2-52c1-4ef6-9354-320f1a091153
author: rothja
ms.author: jroth
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: c2c799aeb38088baacc6110459d42db6138f3575
ms.sourcegitcommit: c8e1553ff3fdf295e8dc6ce30d1c454d6fde8088
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/22/2020
ms.locfileid: "86922994"
---
# <a name="---comment-transact-sql"></a>-- (Comentarios) (Transact-SQL)
[!INCLUDE [sql-asdb-asdbmi-asa-pdw](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

  Indica texto proporcionado por el usuario. Los comentarios se pueden insertar en una línea independiente, anidada al final de una línea de comandos de [!INCLUDE[tsql](../../includes/tsql-md.md)] o dentro de una instrucción de [!INCLUDE[tsql](../../includes/tsql-md.md)] El servidor no evalúa el comentario.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
-- text_of_comment  
```  
  
[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="arguments"></a>Argumentos
 *text_of_comment*  
 Cadena de caracteres que contiene el texto del comentario.  
  
## <a name="remarks"></a>Observaciones  
Use dos guiones ( **--** ) para comentarios de una línea o anidados. Los comentarios insertados con **--** terminan en una nueva línea, que se especifica con un carácter de retorno de carro (U + 000A), un carácter de avance de línea (U + 000D) o una combinación de ambos. No hay límite de longitud para los comentarios. En la tabla siguiente se enumeran los métodos abreviados de teclado que puede utilizar para acotar un texto como comentario o quitar los comentarios.
  
|Acción|Estándar|  
|------------|--------------|  
|Hacer un comentario al texto seleccionado|CTRL+K, CTRL+C|  
|Quitar un comentario del texto seleccionado|CTRL+K, CTRL+U|  
  
 Para más información sobre las teclas de método abreviado, vea [Métodos abreviados de teclado de SQL Server Management Studio](../../ssms/sql-server-management-studio-keyboard-shortcuts.md).  
  
 Para más información sobre los comentarios de varias líneas, vea [Slash Star &#40;Block Comment&#41; &#40;Transact-SQL&#41;](../../t-sql/language-elements/slash-star-comment-transact-sql.md) (Barra diagonal y asterisco [comentario de bloque] [Transact-SQL]).  
  
## <a name="examples"></a>Ejemplos  
 En este ejemplo se utilizan los caracteres -- de comentario.  
  
```  
-- Choose the AdventureWorks2012 database.  
USE AdventureWorks2012;  
GO  
-- Choose all columns and all rows from the Address table.  
SELECT *  
FROM Person.Address  
ORDER BY PostalCode ASC; -- We do not have to specify ASC because   
-- that is the default.  
GO  
```  
  
## <a name="see-also"></a>Consulte también  
 [Lenguaje de control de flujo &#40;Transact-SQL&#41;](~/t-sql/language-elements/control-of-flow.md)  
  
  
