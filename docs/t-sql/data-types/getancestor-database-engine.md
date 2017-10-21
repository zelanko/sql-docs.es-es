---
title: GetAncestor (motor de base de datos) | Documentos de Microsoft
ms.custom: 
ms.date: 7/22/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- GetAncestor_TSQL
- GetAncestor
dev_langs:
- TSQL
helpviewer_keywords:
- GetAncestor [Database Engine]
ms.assetid: b96a986f-d5e4-4034-8013-de7974594ee9
caps.latest.revision: 26
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: b7649b3290175787b293ea1b720bb299ead89971
ms.contentlocale: es-es
ms.lasthandoff: 09/01/2017

---
# <a name="getancestor-database-engine"></a>GetAncestor (motor de base de datos)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

Devuelve un **hierarchyid** que representa el  *n* antepasado número de *esto*.
  
## <a name="syntax"></a>Sintaxis  
  
```sql
-- Transact-SQL syntax  
child.GetAncestor ( n )   
```  
  
```sql
-- CLR syntax  
SqlHierarchyId GetAncestor ( int n )  
```  
  
## <a name="arguments"></a>Argumentos  
*n*  
Un **int**, que representa el número de niveles que subir en la jerarquía.
  
## <a name="return-types"></a>Tipos de valor devuelto
**Tipo: hierarchyid devuelto de SQL Server**
  
**Tipo: SqlHierarchyId devuelto de CLR**
  
## <a name="remarks"></a>Comentarios  
Se usa para probar si cada nodo de la salida tiene el nodo actual como antecesor en el nivel especificado.
  
Si un número mayor que [GetLevel()](../../t-sql/data-types/getlevel-database-engine.md) es pasa, se devuelve NULL.
  
Si se pasa un número negativo, se produce una excepción.
  
## <a name="examples"></a>Ejemplos  
  
### <a name="a-finding-the-child-nodes-of-a-parent"></a>A. Encontrar los nodos secundarios de un elemento primario  
`GetAncestor(1)` devuelve los empleados que tienen `david0` como su antecesor inmediato (su elemento primario). En el ejemplo siguiente se utiliza `GetAncestor(1)`.
  
```sql
DECLARE @CurrentEmployee hierarchyid  
SELECT @CurrentEmployee = OrgNode FROM HumanResources.EmployeeDemo  
WHERE LoginID = 'adventure-works\david0'  
  
SELECT OrgNode.ToString() AS Text_OrgNode, *  
FROM HumanResources.EmployeeDemo  
WHERE OrgNode.GetAncestor(1) = @CurrentEmployee ;  
```  
  
### <a name="b-returning-the-grandchildren-of-a-parent"></a>B. Devolución de los elementos descendientes del secundario de un elemento primario  
`GetAncestor(2)` devuelve los empleados que están dos niveles por debajo en la jerarquía del nodo actual. Éstos son los descendientes de los secundarios del nodo actual. En el ejemplo siguiente se utiliza `GetAncestor(2)`.
  
```sql
DECLARE @CurrentEmployee hierarchyid  
SELECT @CurrentEmployee = OrgNode FROM HumanResources.EmployeeDemo  
WHERE LoginID = 'adventure-works\ken0'  
  
SELECT OrgNode.ToString() AS Text_OrgNode, *  
FROM HumanResources.EmployeeDemo  
WHERE OrgNode.GetAncestor(2) = @CurrentEmployee ;  
```  
  
### <a name="c-returning-the-current-row"></a>C. Devolución de la fila actual  
Para devolver el nodo actual mediante el uso de `GetAncestor(0)`, ejecute el código siguiente.
  
```sql
DECLARE @CurrentEmployee hierarchyid  
SELECT @CurrentEmployee = OrgNode FROM HumanResources.EmployeeDemo  
WHERE LoginID = 'adventure-works\david0'  
  
SELECT OrgNode.ToString() AS Text_OrgNode, *  
FROM HumanResources.EmployeeDemo  
WHERE OrgNode.GetAncestor(0) = @CurrentEmployee ;  
```  
  
### <a name="d-returning-a-hierarchy-level-if-a-table-is-not-present"></a>D. Devolución de un nivel de la jerarquía si una tabla no está presente  
`GetAncestor` devuelve el nivel seleccionado en la jerarquía incluso si una tabla no está presente. Por ejemplo, el código siguiente designa a un empleado actual y devuelve el identificador `hierarchyid` del antecesor del empleado actual sin hacer referencia a una tabla.
  
```sql
DECLARE @CurrentEmployee hierarchyid ;  
DECLARE @TargetEmployee hierarchyid ;  
SELECT @CurrentEmployee = '/2/3/1.2/5/3/' ;  
SELECT @TargetEmployee = @CurrentEmployee.GetAncestor(2) ;  
SELECT @TargetEmployee.ToString(), @TargetEmployee ;  
```  
  
### <a name="e-calling-a-common-language-runtime-method"></a>E. Llamada de un método del Common Language Runtime  
En el fragmento de código siguiente se llama al método `GetAncestor()`.
  
```sql
this.GetAncestor(1)  
```  
  
## <a name="see-also"></a>Vea también
[IsDescendantOf &#40; motor de base de datos &#41;](../../t-sql/data-types/isdescendantof-database-engine.md)  
[Referencia de los métodos del tipo de datos hierarchyid](http://msdn.microsoft.com/library/01a050f5-7580-4d5f-807c-7f11423cbb06)  
[Datos jerárquicos &#40;SQL Server&#41;](../../relational-databases/hierarchical-data-sql-server.md)  
[hierarchyid &#40;Transact-SQL&#41;](../../t-sql/data-types/hierarchyid-data-type-method-reference.md)
  
  

