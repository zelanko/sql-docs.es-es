---
title: Parse (motor de base de datos) | Documentos de Microsoft
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
- Parse
- Parse_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- Parse [Database Engine]
ms.assetid: b37e28b6-6e2e-470a-945b-ce5252da743a
caps.latest.revision: 17
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 027940c7575f3c7901cd8668879064ff375d9986
ms.contentlocale: es-es
ms.lasthandoff: 09/01/2017

---
# <a name="parse-database-engine"></a>Parse (motor de base de datos)
[!INCLUDE[tsql-appliesto-ss2012-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-asdb-xxxx-xxx-md.md)]

Parse convierte la representación de cadena canónica de un **hierarchyid** a una **hierarchyid** valor. El análisis se llama implícitamente cuando una conversión de un tipo de cadena para **hierarchyid** se produce. Tiene el efecto contrario de [ToString](../../t-sql/data-types/tostring-database-engine.md). Parse() es un método estático.
  
## <a name="syntax"></a>Sintaxis  
  
```sql
-- Transact-SQL syntax  
hierarchyid::Parse ( input )  
-- This is functionally equivalent to the following syntax   
-- which implicitly calls Parse():  
CAST ( input AS hierarchyid )  
```  
  
```sql
-- CLR syntax  
static SqlHierarchyId Parse ( SqlString input )   
```  
  
## <a name="arguments"></a>Argumentos  
*entrada*  
[!INCLUDE[tsql](../../includes/tsql-md.md)]: Valor de tipo de datos de carácter que se va a convertir.
  
CLR: Valor de cadena que se va a evaluar.
  
## <a name="return-types"></a>Tipos devueltos  
**Tipo: hierarchyid devuelto de SQL Server**
  
**Tipo: SqlHierarchyId devuelto de CLR**
  
## <a name="remarks"></a>Comentarios  
Si el análisis recibe un valor que no es una representación de cadena válida de un **hierarchyid**, se produce una excepción. Por ejemplo, si **char** tipos de datos contienen espacios finales, se produce una excepción.
  
## <a name="examples"></a>Ejemplos  
  
### <a name="a-converting-transact-sql-values-without-a-table"></a>A. Convertir valores de Transact-SQL sin una tabla  
El siguiente ejemplo de código usa `ToString` para convertir un **hierarchyid** valor en una cadena, y `Parse` para convertir un valor de cadena a un **hierarchyid**.
  
```sql
DECLARE @StringValue AS nvarchar(4000), @hierarchyidValue AS hierarchyid  
SET @StringValue = '/1/1/3/'  
SET @hierarchyidValue = 0x5ADE  
  
SELECT hierarchyid::Parse(@StringValue) AS hierarchyidRepresentation,  
@hierarchyidValue.ToString() AS StringRepresentation ;
GO  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```
hierarchyidRepresentation    StringRepresentation
-------------------------    -----------------------
0x5ADE                       /1/1/3/
```
  
### <a name="b-clr-example"></a>B. Ejemplo de CLR  
El fragmento de código siguiente llama al método de Parse():
  
```sql
string input = “/1/2/”;  
SqlHierarchyId.Parse(input);  
```  
  
## <a name="see-also"></a>Vea también
[Referencia de los métodos del tipo de datos hierarchyid](http://msdn.microsoft.com/library/01a050f5-7580-4d5f-807c-7f11423cbb06)  
[Datos jerárquicos &#40;SQL Server&#41;](../../relational-databases/hierarchical-data-sql-server.md)  
[hierarchyid &#40;Transact-SQL&#41;](../../t-sql/data-types/hierarchyid-data-type-method-reference.md)
  
  

