---
title: DROP SYNONYM (Transact-SQL) | Documentos de Microsoft
ms.custom:
- SQL2016_New_Updated
ms.date: 07/26/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- DROP SYNONYM
- DROP_SYNONYM_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- deleting synonyms
- synonyms [SQL Server], removing
- removing synonyms
- DROP SYNONYM statement
- dropping synonyms
ms.assetid: 23578932-e4de-4c39-a5a0-ce45139c4269
caps.latest.revision: 24
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 5f781dd3557dadcda49e2089bf98195f5adde32e
ms.contentlocale: es-es
ms.lasthandoff: 09/01/2017

---
# <a name="drop-synonym-transact-sql"></a>DROP SYNONYM (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Quita un sinónimo de un esquema especificado.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
DROP SYNONYM [ IF EXISTS ] [ schema. ] synonym_name  
```  
  
## <a name="arguments"></a>Argumentos  
 *IF EXISTE*  
**Se aplica a**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] a través de [versión actual](http://go.microsoft.com/fwlink/p/?LinkId=299658))
  
 Quita condicionalmente el sinónimo solo si ya existe.  
  
 *esquema*  
 Especifica el esquema en el que existe el sinónimo. Si no se especifica, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] utiliza el esquema predeterminado del usuario actual.  
  
 *synonym_name*  
 Es el nombre del sinónimo que se va a quitar.  
  
## <a name="remarks"></a>Comentarios  
 Las referencias a sinónimos no están enlazadas al esquema, por lo que un sinónimo se puede quitar cuando se desee. Las referencias a sinónimos quitados solo se encontrarán en tiempo de ejecución.  
  
 Es posible crear, quitar y hacer referencia a sinónimos en SQL dinámico.  
  
## <a name="permissions"></a>Permissions  
 Para quitar un sinónimo, un usuario debe cumplir al menos una de las condiciones siguientes. El usuario debe ser:  
  
-   El propietario actual del sinónimo.  
  
-   Receptor del permiso CONTROL en el sinónimo.  
  
-   Receptor del permiso ALTER SCHEMA en el esquema contenedor.  
  
## <a name="examples"></a>Ejemplos  
 En el ejemplo siguiente, primero se crea el sinónimo `MyProduct` y después se quita.  
  
```  
USE tempdb;  
GO  
-- Create a synonym for the Product table in AdventureWorks2012.  
CREATE SYNONYM MyProduct  
FOR AdventureWorks2012.Production.Product;  
GO  
-- Drop synonym MyProduct.  
USE tempdb;  
GO  
DROP SYNONYM MyProduct;  
GO  
```  
  
## <a name="see-also"></a>Vea también  
 [CREAR el sinónimo &#40; Transact-SQL &#41;](../../t-sql/statements/create-synonym-transact-sql.md)   
 [EVENTDATA &#40;Transact-SQL&#41;](../../t-sql/functions/eventdata-transact-sql.md)  
  
  

