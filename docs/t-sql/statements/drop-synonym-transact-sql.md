---
title: DROP SYNONYM (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 07/26/2017
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
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 25af262ddc5655bc42e4893daecefe0cd8fb85d9
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 11/21/2017
---
# <a name="drop-synonym-transact-sql"></a>DROP SYNONYM (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Quita un sinónimo de un esquema especificado.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
DROP SYNONYM [ IF EXISTS ] [ schema. ] synonym_name  
```  
  
## <a name="arguments"></a>Argumentos  
 *IF EXISTS*  
**Se aplica a**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (desde [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] hasta la [versión actual](http://go.microsoft.com/fwlink/p/?LinkId=299658)).
  
 Quita condicionalmente el sinónimo solo si ya existe.  
  
 *schema*  
 Especifica el esquema en el que existe el sinónimo. Si no se especifica, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] utiliza el esquema predeterminado del usuario actual.  
  
 *synonym_name*  
 Es el nombre del sinónimo que se va a quitar.  
  
## <a name="remarks"></a>Notas  
 Las referencias a sinónimos no están enlazadas al esquema, por lo que un sinónimo se puede quitar cuando se desee. Las referencias a sinónimos quitados solo se encontrarán en tiempo de ejecución.  
  
 Es posible crear, quitar y hacer referencia a sinónimos en SQL dinámico.  
  
## <a name="permissions"></a>Permisos  
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
  
## <a name="see-also"></a>Ver también  
 [CREATE SYNONYM &#40;Transact-SQL&#41;](../../t-sql/statements/create-synonym-transact-sql.md)   
 [EVENTDATA &#40;Transact-SQL&#41;](../../t-sql/functions/eventdata-transact-sql.md)  
  
  
