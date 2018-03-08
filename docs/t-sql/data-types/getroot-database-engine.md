---
title: GetRoot (motor de base de datos) | Documentos de Microsoft
ms.custom: 
ms.date: 7/22/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: t-sql|data-types
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- GetRoot
- GetRoot_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- GetRoot [Database Engine]
ms.assetid: 240b70f1-eeda-44ab-b4bb-9e4af80fa7c0
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 643eb8274a47220a1dd8c6cc76f822c18dbcf849
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 11/21/2017
---
# <a name="getroot-database-engine"></a>GetRoot (motor de base de datos)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

Devuelve la raíz del árbol de jerarquía. GetRoot() es un método estático.
  
## <a name="syntax"></a>Sintaxis  
  
```sql
-- Transact-SQL syntax  
hierarchyid::GetRoot ( )   
```  
  
```sql
-- CLR syntax  
static SqlHierarchyId GetRoot ( )   
```  
  
## <a name="return-types"></a>Tipos devueltos  
**Tipo: hierarchyid devuelto de SQL Server**
  
**Tipo: SqlHierarchyId devuelto de CLR**
  
## <a name="remarks"></a>Comentarios  
Se utiliza para determinar el nodo raíz de un árbol de jerarquía.
  
## <a name="examples"></a>Ejemplos  
  
### <a name="a-transact-sql-example"></a>A. Ejemplo de Transact-SQL  
El ejemplo siguiente devuelve la raíz del árbol de jerarquía:
  
```sql
SELECT OrgNode.ToString() AS Text_OrgNode, *  
FROM HumanResources.EmployeeDemo  
WHERE OrgNode = hierarchyid::GetRoot()  
```  
  
### <a name="b-clr-example"></a>B. Ejemplo de CLR  
El fragmento de código siguiente llama al método de GetRoot():
  
```sql
SqlHierarchyId.GetRoot()  
```  
  
## <a name="see-also"></a>Vea también
[Referencia de los métodos del tipo de datos hierarchyid](http://msdn.microsoft.com/library/01a050f5-7580-4d5f-807c-7f11423cbb06)  
[Datos jerárquicos &#40;SQL Server&#41;](../../relational-databases/hierarchical-data-sql-server.md)  
[hierarchyid &#40;Transact-SQL&#41;](../../t-sql/data-types/hierarchyid-data-type-method-reference.md)
  
  
