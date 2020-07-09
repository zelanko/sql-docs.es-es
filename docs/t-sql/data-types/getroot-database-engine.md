---
title: GetRoot (motor de base de datos) | Microsoft Docs
ms.custom: ''
ms.date: 07/22/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- GetRoot
- GetRoot_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- GetRoot [Database Engine]
ms.assetid: 240b70f1-eeda-44ab-b4bb-9e4af80fa7c0
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: fbc5bd95c10c89da4fb6fc6cbd1400f2e310927b
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/01/2020
ms.locfileid: "85738196"
---
# <a name="getroot-database-engine"></a>GetRoot (motor de base de datos)
[!INCLUDE [SQL Server SQL Database](../../includes/applies-to-version/sql-asdb.md)]

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
  
## <a name="return-types"></a>Tipos de valor devuelto  
**Tipo de valor devuelto de SQL Server: hierarchyid**
  
**Tipo devuelto de CLR: SqlHierarchyId**
  
## <a name="remarks"></a>Observaciones  
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
En el fragmento de código siguiente se llama al método GetRoot():
  
```sql
SqlHierarchyId.GetRoot()  
```  
  
## <a name="see-also"></a>Consulte también
[Referencia de los métodos del tipo de datos hierarchyid](https://msdn.microsoft.com/library/01a050f5-7580-4d5f-807c-7f11423cbb06)  
[Datos jerárquicos &#40;SQL Server&#41;](../../relational-databases/hierarchical-data-sql-server.md)  
[hierarchyid &#40;Transact-SQL&#41;](../../t-sql/data-types/hierarchyid-data-type-method-reference.md)
  
  
