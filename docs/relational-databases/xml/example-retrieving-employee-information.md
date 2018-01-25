---
title: "Ejemplo: Recuperar información de los empleados | Microsoft Docs"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: xml
ms.reviewer: 
ms.suite: sql
ms.technology: dbe-xml
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords: EXPLICIT mode
ms.assetid: 63cd6569-2600-485b-92b4-1f6ba09db219
caps.latest.revision: "9"
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 069bf210891435de0cdd60e5c715ebbdd16ecc19
ms.sourcegitcommit: 6c54e67818ec7b0a2e3c1f6e8aca0fdf65e6625f
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 01/19/2018
---
# <a name="example-retrieving-employee-information"></a>Ejemplo: Recuperar información de los empleados
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)] En este ejemplo, se recupera el identificador y el nombre de cada empleado. En la base de datos [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] , el identificador de empleado se puede obtener de la columna BusinessEntityID de la tabla Employee. Los nombres de los empleados se pueden obtener de la tabla Person. Para combinar las tablas, se puede usar la columna BusinessEntityID.  
  
 Supongamos que desea una transformación FOR XML EXPLICIT para generar XML como se indica a continuación:  
  
```  
<Employee EmpID="1" >  
  <Name FName="Ken" LName="Sánchez" />  
</Employee>  
...  
```  
  
 Dado que hay dos niveles en la jerarquía, habría que escribir dos consultas `SELECT` y aplicar UNION ALL. Esta es la primera consulta, que recupera los valores correspondientes al elemento <`Employee`> y sus atributos. La consulta asigna `1` como valor `Tag` para el elemento <`Employee`> y NULL como `Parent`, puesto que se trata del elemento de nivel superior.  
  
```  
SELECT 1    as Tag,  
       NULL as Parent,  
       E.BusinessEntityID AS [Employee!1!EmpID],  
       NULL       as [Name!2!FName],  
       NULL       as [Name!2!LName]  
FROM   HumanResources.Employee AS E  
INNER JOIN Person.Person AS P  
ON  E.BusinessEntityID = P.BusinessEntityID;  
```  
  
 Esta es la segunda consulta. Recupera los valores correspondientes al elemento <`Name`>. Asigna `2` como valor de `Tag` para el elemento <`Name`> y 1 como valor de etiqueta en `1` como valor de etiqueta `Parent` que identifica <`Employee`> como elemento primario.  
  
```  
SELECT 2 as Tag,  
       1 as Parent,  
       E.BusinessEntityID,  
       FirstName,   
       LastName   
FROM   HumanResources.Employee AS E  
INNER JOIN Person.Person AS P  
ON  E.BusinessEntityID = P.BusinessEntityID;  
```  
  
 Combina estas consultas con `UNION AL`L, aplica `FOR XML EXPLICIT` y especifica la cláusula `ORDER BY` querida. El conjunto de filas se debe ordenar primero según el valor de `BusinessEntityID` y, a continuación, por nombre, de modo que los valores NULL en el nombre aparezcan al principio. Si ejecuta la siguiente consulta sin la cláusula FOR XML, podrá ver la tabla universal generada.  
  
 Esta es la consulta final:  
  
```  
SELECT 1    as Tag,  
       NULL as Parent,  
       E.BusinessEntityID as [Employee!1!EmpID],  
       NULL       as [Name!2!FName],  
       NULL       as [Name!2!LName]  
FROM   HumanResources.Employee AS E  
INNER JOIN Person.Person AS P  
ON  E.BusinessEntityID = P.BusinessEntityID  
UNION ALL  
SELECT 2 as Tag,  
       1 as Parent,  
       E.BusinessEntityID,  
       FirstName,   
       LastName   
FROM   HumanResources.Employee AS E  
INNER JOIN Person.Person AS P  
ON  E.BusinessEntityID = P.BusinessEntityID  
ORDER BY [Employee!1!EmpID],[Name!2!FName]  
FOR XML EXPLICIT;  
```  
  
 Éste es el resultado parcial:  
  
 `<Employee EmpID="1">`  
  
 `<Name FName="Ken" LName="Sánchez" />`  
  
 `</Employee>`  
  
 `<Employee EmpID="2">`  
  
 `<Name FName="Terri" LName="Duffy" />`  
  
 `</Employee>`  
  
 `...`  
  
 El primer `SELECT` especifica los nombres para las columnas del conjunto de filas resultante. Estos nombres forman dos grupos de columnas. El grupo con el valor `Tag` de `1` en el nombre de columna identifica `Employee` como elemento y `EmpID` como atributo. El otro grupo de columnas tiene el valor `Tag` de `2` en la columna e identifica <`Name`> como elemento, y `FName` y `LName` como atributos.  
  
 La siguiente tabla muestra el conjunto de filas parcial generado por la consulta:  
  
 `Tag Parent  Employee!1!EmpID Name!2!FName Name!2!LName`  
  
 `--- ------  ---------------- ------------ ------------`  
  
 `1   NULL    1                NULL         NULL`  
  
 `2   1       1                Ken          Sánchez`  
  
 `1   NULL    2                NULL         NULL`  
  
 `2   1       2                Terri        Duffy`  
  
 `1   NULL    3                NULL         NULL`  
  
 `2   1       3                Roberto      Tamburello`  
  
 `...`  
  
 Así es como se procesan las filas de la tabla universal para crear el árbol XML resultante:  
  
 La primera fila identifica el valor `Tag` en `1`. Por consiguiente, se identifica el grupo de columnas que tiene el valor `Tag` en `1` , `Employee!1!EmpID`. Esta columna identifica `Employee` como nombre de elemento. A continuación, se crea un elemento <`Employee`> que tenga atributos `EmpID`. Los valores de columna correspondientes se asignan a estos atributos.  
  
 La segunda fila tiene en `Tag` en valor `2`. Por consiguiente, el grupo de columnas que tiene el valor `Tag` en `2` en el nombre de columna, `Name!2!FName`, se identifica: `Name!2!LName`. Estos nombres de columna identifican `Name` como nombre de elemento. Se crea un elemento <`Name`> con atributos `FName` y `LName`. A continuación, se asignan los valores de columna correspondientes a estos atributos. Esta fila identifica `1` como `Parent`. Este elemento secundario se agrega al elemento <`Employee`> anterior.  
  
 Este proceso se repite con el resto de filas del conjunto. Observe la importancia de ordenar las filas de la tabla universal para que FOR XML EXPLICIT pueda procesar el conjunto de filas por orden y generar el XML deseado.  
  
## <a name="see-also"></a>Ver también  
 [Usar el modo EXPLICIT con FOR XML](../../relational-databases/xml/use-explicit-mode-with-for-xml.md)  
  
  
