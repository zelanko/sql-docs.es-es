---
title: IsDescendantOf (motor de base de datos) | Documentos de Microsoft
ms.custom: 
ms.date: 7/22/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: t-sql|data-types
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- IsDescendant_TSQL
- IsDescendant
dev_langs: TSQL
helpviewer_keywords: IsDescendantOf [Database Engine]
ms.assetid: edc80444-b697-410f-9419-0f63c9b5618d
caps.latest.revision: "27"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 291a38e51da8e342d96b3a5feac90fbbc2a00d46
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/21/2017
---
# <a name="isdescendantof-database-engine"></a>IsDescendantOf (motor de base de datos)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

Devuelve true si *esto* es un descendiente del elemento primario.
  
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
*elemento primario*  
El **hierarchyid** nodo para el que se debe realizar la prueba IsDescendantOf.
  
## <a name="return-types"></a>Tipos devueltos  
**Tipo: bit devuelto de SQL Server**
  
**Tipo: SqlBoolean devuelto de CLR**
  
## <a name="remarks"></a>Comentarios  
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
  
## <a name="see-also"></a>Vea también
[Referencia de los métodos del tipo de datos hierarchyid](http://msdn.microsoft.com/library/01a050f5-7580-4d5f-807c-7f11423cbb06)  
[Datos jerárquicos &#40;SQL Server&#41;](../../relational-databases/hierarchical-data-sql-server.md)  
[hierarchyid &#40;Transact-SQL&#41;](../../t-sql/data-types/hierarchyid-data-type-method-reference.md)
  
  
