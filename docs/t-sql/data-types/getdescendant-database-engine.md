---
title: GetDescendant (motor de base de datos) | Documentos de Microsoft
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
- GetDescendant_TSQL
- GetDescendant
dev_langs:
- TSQL
helpviewer_keywords:
- GetDescendant [Database Engine]
ms.assetid: f5f39596-033e-4243-acbc-caa188b45b03
caps.latest.revision: 23
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: ced4a5518ce7d58785a1d2954c4f131b66a5ddb0
ms.contentlocale: es-es
ms.lasthandoff: 09/01/2017

---
# <a name="getdescendant-database-engine"></a>GetDescendant (motor de base de datos)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

Devuelve el nodo secundario del nodo primario.
  
## <a name="syntax"></a>Sintaxis  
  
```sql
-- Transact-SQL syntax  
parent.GetDescendant ( child1 , child2 )   
```  
  
```sql
-- CLR syntax  
SqlHierarchyId GetDescendant ( SqlHierarchyId child1 , SqlHierarchyId child2 )   
```  
  
## <a name="arguments"></a>Argumentos  
*Child1*  
NULL o **hierarchyid** de un elemento secundario del nodo actual.
  
*Child2*  
NULL o **hierarchyid** de un elemento secundario del nodo actual.
  
## <a name="return-types"></a>Tipos devueltos  
**Tipo: hierarchyid devuelto de SQL Server**
  
**Tipo: SqlHierarchyId devuelto de CLR**
  
## <a name="remarks"></a>Comentarios  
Devuelve un nodo secundario que es un descendiente del nodo primario.
-   Si el elemento primario es NULL, devolverá NULL.  
-   Si el elemento primario no es NULL, y child1 y child2 son NULL, devuelve un elemento secundario del elemento primario.  
-   Si el elemento primario y child1 no son NULL y, a su vez, child2 es NULL, devuelve un elemento secundario del elemento primario mayor que child1.  
-   Si el elemento primario y child2 no son NULL y, a su vez, child1 es NULL, devuelve un elemento secundario del elemento primario menor que child2.  
-   Si el elemento primario, child1 y child2 no son NULL, devuelve un elemento secundario del elemento primario mayor que child1 y menor que child2.  
-   Si child1 o child2 no son NULL y no son un elemento secundario del elemento primario, se producirá una excepción.  
-   Si child2 no es NULL ni es un elemento secundario del elemento primario, se producirá una excepción.  
-   Si child1 >= child2, se producirá una excepción.  
  
GetDescendant es determinista. Por lo tanto, si se llama a GetDescendant con las mismas entradas, siempre se producirá el mismo resultado. Sin embargo, la identidad exacta del nodo secundario producido puede variar en función de su relación con los demás nodos, como se muestra en el ejemplo C.
  
## <a name="examples"></a>Ejemplos  
  
### <a name="a-inserting-a-row-as-the-least-descendant-node"></a>A. Insertar una fila como el nodo menos descendiente  
Se contrata a un nuevo empleado, que es subordinado de un empleado ya existente en el nodo `/3/1/`. Ejecute el siguiente código para insertar la nueva fila mediante el método GetDescendant sin argumentos para especificar el nuevo nodo de filas como `/3/1/1/`:
  
```sql
DECLARE @Manager hierarchyid;   
SET @Manager = CAST('/3/1/' AS hierarchyid);  
  
INSERT HumanResources.EmployeeDemo (OrgNode, LoginID, Title, HireDate)  
VALUES  
(@Manager.GetDescendant(NULL, NULL),  
'adventure-works\FirstNewEmployee', 'Application Intern', '3/11/07') ;  
```  
  
### <a name="b-inserting-a-row-as-a-greater-descendant-node"></a>B. Insertar una fila como un nodo más descendiente  
Se contrata a otro empleado nuevo, informes del mismo jefe que en el ejemplo A. ejecute el siguiente código para insertar la nueva fila mediante el método GetDescendant mediante el argumento Child1 para especificar que el nodo de la nueva fila vendrá a continuación el nodo del ejemplo A , pase a ser `/3/1/2/`:
  
```sql
DECLARE @Manager hierarchyid, @Child1 hierarchyid;  
  
SET @Manager = CAST('/3/1/' AS hierarchyid);  
SET @Child1 = CAST('/3/1/1/' AS hierarchyid);  
  
INSERT HumanResources.EmployeeDemo (OrgNode, LoginID, Title, HireDate)  
VALUES  
(@Manager.GetDescendant(@Child1, NULL),  
'adventure-works\SecondNewEmployee', 'Application Intern', '3/11/07') ;  
```  
  
### <a name="c-inserting-a-row-between-two-existing-nodes"></a>C. Insertar una fila entre dos nodos existentes  
Se contrata a un tercer empleado, subordinado del mismo jefe como en el ejemplo A. Este ejemplo inserta la nueva fila a un nodo mayor que el `FirstNewEmployee` en el ejemplo A, y menor que el `SecondNewEmployee` del ejemplo B. ejecute el siguiente código mediante el método GetDescendant. Use los argumentos child1 y child2 para especificar que el nodo de la nueva fila se convertirá en el nodo `/3/1/1.1/`:
  
```sql
DECLARE @Manager hierarchyid, @Child1 hierarchyid, @Child2 hierarchyid;  
  
SET @Manager = CAST('/3/1/' AS hierarchyid);  
SET @Child1 = CAST('/3/1/1/' AS hierarchyid);  
SET @Child2 = CAST('/3/1/2/' AS hierarchyid);  
  
INSERT HumanResources.EmployeeDemo (OrgNode, LoginID, Title, HireDate)  
VALUES  
(@Manager.GetDescendant(@Child1, @Child2),  
'adventure-works\ThirdNewEmployee', 'Application Intern', '3/11/07') ;  
  
```  
  
Después de completar los ejemplos A, B y C, los nodos agregados a la tabla será equipos del mismo nivel con el siguiente **hierarchyid** valores:
  
`/3/1/1/`
  
`/3/1/1.1/`
  
`/3/1/2/`
  
El nodo `/3/1/1.1/` es mayor que el nodo `/3/1/1/`, pero está en el mismo nivel de la jerarquía.
  
### <a name="d-scalar-examples"></a>D. Ejemplos escalares  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]admite inserciones y eliminaciones de cualquier arbitrarias **hierarchyid** nodos. Mediante el uso de GetDescendant(), siempre es posible generar un nodo entre dos **hierarchyid** nodos. Ejecute el código siguiente para generar nodos de ejemplo mediante `GetDescendant`:
  
```sql
DECLARE @h hierarchyid = hierarchyid::GetRoot();  
DECLARE @c hierarchyid = @h.GetDescendant(NULL, NULL);  
SELECT @c.ToString();  
DECLARE @c2 hierarchyid = @h.GetDescendant(@c, NULL);  
SELECT @c2.ToString();  
SET @c2 = @h.GetDescendant(@c, @c2);  
SELECT @c2.ToString();  
SET @c = @h.GetDescendant(@c, @c2);  
SELECT @c.ToString();  
SET @c2 = @h.GetDescendant(@c, @c2);  
SELECT @c2.ToString();  
```  
  
### <a name="e-clr-example"></a>E. Ejemplo de CLR  
En el fragmento de código siguiente se llama al método `GetDescendant()`:
  
```sql
SqlHierarchyId parent, child1, child2;  
parent = SqlHierarchyId.GetRoot();  
child1 = parent.GetDescendant(SqlHierarchyId.Null, SqlHierarchyId.Null);  
child2 = parent.GetDescendant(child1, SqlHierarchyId.Null);  
Console.Write(parent.GetDescendant(child1, child2).ToString());  
```  
  
## <a name="see-also"></a>Vea también
[Referencia de los métodos del tipo de datos hierarchyid](http://msdn.microsoft.com/library/01a050f5-7580-4d5f-807c-7f11423cbb06)  
[Datos jerárquicos &#40;SQL Server&#41;](../../relational-databases/hierarchical-data-sql-server.md)  
[hierarchyid &#40;Transact-SQL&#41;](../../t-sql/data-types/hierarchyid-data-type-method-reference.md)
  
  

