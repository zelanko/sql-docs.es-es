---
title: GetLevel (motor de base de datos) | Documentos de Microsoft
ms.custom: 
ms.date: 07/22/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- GetLevel
- GetLevel_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- GetLevel [Database Engine]
ms.assetid: 81577d7e-8ff6-4e73-b7f4-94c03d4921e7
caps.latest.revision: 17
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: aac401d8fbe9546404f44f5fa2455f9e9c5dfe9d
ms.contentlocale: es-es
ms.lasthandoff: 09/01/2017

---
# <a name="getlevel-database-engine"></a>GetLevel (motor de base de datos)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

Devuelve un entero que representa la profundidad del nodo *esto* en el árbol.
  
## <a name="syntax"></a>Sintaxis  
  
```sql
-- Transact-SQL syntax  
node.GetLevel ( )   
```  
  
```sql
-- CLR syntax  
SqlInt16 GetLevel ( )   
```  
  
## <a name="return-types"></a>Tipos devueltos  
**Tipo: smallint devuelto de SQL Server**
  
**Tipo: SqlInt16 devuelto de CLR**
  
## <a name="remarks"></a>Comentarios  
Se utiliza para determinar el nivel de uno o más nodos o para filtrar los nodos a los miembros de un nivel especificado. La raíz del árbol de jerarquía tiene el nivel 0.
  
GetLevel es muy útil para los índices de búsqueda de amplitud. Para obtener más información, vea [datos jerárquicos &#40; SQL Server &#41; ](../../relational-databases/hierarchical-data-sql-server.md).
  
## <a name="examples"></a>Ejemplos  
  
### <a name="a-returning-the-hierarchy-level-as-a-column"></a>A. Devolver el nivel de jerarquía como una columna  
En el ejemplo siguiente se devuelve una representación de texto de la **hierarchyid**y, a continuación, el nivel de jerarquía como la **EmpLevel** columna para todas las filas de la tabla:
  
```sql
SELECT OrgNode.ToString() AS Text_OrgNode,   
OrgNode.GetLevel() AS EmpLevel, *  
FROM HumanResources.EmployeeDemo;  
```  
  
### <a name="b-returning-all-members-of-a-hierarchy-level"></a>B. Devolver todos los miembros de un nivel de jerarquía  
El ejemplo siguiente devuelve todas las filas de la tabla que están en el nivel de jerarquía 2:
  
```sql
SELECT OrgNode.ToString() AS Text_OrgNode,   
OrgNode.GetLevel() AS EmpLevel, *  
FROM HumanResources.EmployeeDemo  
WHERE OrgNode.GetLevel() = 2;  
```  
  
### <a name="c-returning-the-root-of-the-hierarchy"></a>C. Devolver la raíz de la jerarquía  
El ejemplo siguiente devuelve la raíz del nivel de jerarquía:
  
```sql
SELECT OrgNode.ToString() AS Text_OrgNode,   
OrgNode.GetLevel() AS EmpLevel, *  
FROM HumanResources.EmployeeDemo  
WHERE OrgNode.GetLevel() = 0;  
```  
  
### <a name="d-clr-example"></a>D. Ejemplo de CLR  
El fragmento de código siguiente llama al método GetLevel():
  
```sql
this.GetLevel()  
```  
  
## <a name="see-also"></a>Vea también
[Referencia de los métodos del tipo de datos hierarchyid](http://msdn.microsoft.com/library/01a050f5-7580-4d5f-807c-7f11423cbb06)  
[Datos jerárquicos &#40;SQL Server&#41;](../../relational-databases/hierarchical-data-sql-server.md)  
[hierarchyid &#40;Transact-SQL&#41;](../../t-sql/data-types/hierarchyid-data-type-method-reference.md)
  
  

