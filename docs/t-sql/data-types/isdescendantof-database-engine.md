---
title: IsDescendantOf (motor de base de datos) | Microsoft Docs
ms.custom: ''
ms.date: 07/22/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- IsDescendant_TSQL
- IsDescendant
dev_langs:
- TSQL
helpviewer_keywords:
- IsDescendantOf [Database Engine]
ms.assetid: edc80444-b697-410f-9419-0f63c9b5618d
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 286e318eed678eda21259d87d477829d5704e8d9
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/01/2020
ms.locfileid: "85757214"
---
# <a name="isdescendantof-database-engine"></a>IsDescendantOf (motor de base de datos)
[!INCLUDE [SQL Server SQL Database](../../includes/applies-to-version/sql-asdb.md)]

Devuelve true si *this* es descendiente del elemento primario.
  
## <a name="syntax"></a>Sintaxis  
  
```sql
-- Transact-SQL syntax  
child. IsDescendantOf ( parent )  
```  
  
```sql
-- CLR syntax  
SqlHierarchyId IsDescendantOf (SqlHierarchyId parent )  
```  
  
## <a name="arguments"></a>Argumentos  
*parent*  
El nodo **hierarchyid** para el que se debe realizar la prueba IsDescendantOf.
  
## <a name="return-types"></a>Tipos de valor devuelto  
**Tipo de valor devuelto de SQL Server:bit**
  
**Tipo de valor devuelto de CLR:SqlBoolean**
  
## <a name="remarks"></a>Observaciones  
Devuelve true para todos los nodos del subárbol con la raíz en el elemento primario y false para todos los demás nodos.
  
El elemento primario se considera su propio descendiente.
  
## <a name="examples"></a>Ejemplos  
  
### <a name="a-using-isdescendantof-in-a-where-clause"></a>A. Usar IsDescendantOf en una cláusula WHERE  
El ejemplo siguiente devuelve un administrador y los empleados que dependen de él:
  
```sql
DECLARE @Manager hierarchyid  
SELECT @Manager = OrgNode FROM HumanResources.EmployeeDemo  
  WHERE LoginID = 'adventure-works\dylan0'  
  
SELECT * FROM HumanResources.EmployeeDemo  
WHERE OrgNode.IsDescendantOf(@Manager) = 1  
```  
  
### <a name="b-using-isdescendantof-to-evaluate-a-relationship"></a>B. Usar IsDescendantOf para evaluar una relación  
En el código siguiente se declaran y rellenan tres variables. A continuación se evalúa la relación jerárquica y se devuelve uno de dos resultados impresos según la comparación:
  
```sql
DECLARE @Manager hierarchyid, @Employee hierarchyid, @LoginID nvarchar(256)  
SELECT @Manager = OrgNode FROM HumanResources.EmployeeDemo  
WHERE LoginID = 'adventure-works\terri0' ;  
  
SELECT @Employee = OrgNode, @LoginID = LoginID FROM HumanResources.EmployeeDemo  
  WHERE LoginID = 'adventure-works\rob0'  
  
IF @Employee.IsDescendantOf(@Manager) = 1  
   BEGIN  
    PRINT 'LoginID ' + @LoginID + ' is a subordinate of the selected Manager.'  
   END  
ELSE  
   BEGIN  
    PRINT 'LoginID ' + @LoginID + ' is not a subordinate of the selected Manager.' ;  
   END  
```  
  
### <a name="c-calling-a-common-language-runtime-method"></a>C. Llamada de un método del Common Language Runtime  
En el fragmento de código siguiente se llama al método `IsDescendantOf()`.
  
```sql
this.IsDescendantOf(Parent)  
```  
  
## <a name="see-also"></a>Consulte también
[Referencia de los métodos del tipo de datos hierarchyid](https://msdn.microsoft.com/library/01a050f5-7580-4d5f-807c-7f11423cbb06)  
[Datos jerárquicos &#40;SQL Server&#41;](../../relational-databases/hierarchical-data-sql-server.md)  
[hierarchyid &#40;Transact-SQL&#41;](../../t-sql/data-types/hierarchyid-data-type-method-reference.md)
  
  
