---
title: Columnas con un nombre | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: xml
ms.topic: conceptual
helpviewer_keywords:
- names [SQL Server], columns with
ms.assetid: c994e089-4cfc-4e9b-b7fc-e74f6014b51a
author: rothja
ms.author: jroth
ms.openlocfilehash: 9b0dcfa4a7aa7341a7365e90a8bb4b1d9f81e816
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/18/2020
ms.locfileid: "85059503"
---
# <a name="columns-with-a-name"></a>Columnas con nombre
  A continuación se exponen las condiciones específicas en las que se asignan al XML resultante las columnas con nombre de los conjuntos de filas, con distinción entre mayúsculas de minúsculas:  
  
-   El nombre de la columna empieza por \@.  
  
-   El nombre de la columna no empieza por \@.  
  
-   El nombre de la columna no empieza por \@ y contiene una barra diagonal (/).  
  
-   Varias columnas comparten el mismo prefijo.  
  
-   Una columna tiene un nombre distinto.  
  
## <a name="column-name-starts-with-an-at-sign-"></a>El nombre de la columna empieza por \@  
 Si el nombre de columna comienza con un signo de arroba ( \@ ) y no contiene una barra diagonal (/), se crea un atributo del <`row`> elemento que tiene el valor de columna correspondiente. Por ejemplo, la consulta siguiente devuelve un conjunto de filas con dos columnas (\@PmId y Name). En el XML resultante, se agrega un atributo **PmId** al elemento <`row`> correspondiente y se le asigna un valor de ProductModelID.  
  
```  
  
SELECT ProductModelID as "@PmId",  
       Name  
FROM Production.ProductModel  
WHERE ProductModelID=7  
FOR XML PATH   
go  
  
```  
  
 El resultado es el siguiente:  
  
```  
<row PmId="7">  
  <Name>HL Touring Frame</Name>  
</row>  
```  
  
 Tenga en cuenta que los atributos deben aparecer antes de cualquier otro tipo de nodo, como los de elemento y texto, del mismo nivel. La consulta siguiente devolverá un error:  
  
```  
SELECT Name,  
       ProductModelID as "@PmId"  
FROM Production.ProductModel  
WHERE ProductModelID=7  
FOR XML PATH   
go  
```  
  
## <a name="column-name-does-not-start-with-an-at-sign-"></a>El nombre de la columna no empieza por \@  
 Si el nombre de la columna no empieza con un signo de arroba ( \@ ), no es una de las pruebas de nodo XPath y no contiene una barra diagonal (/), se crea un elemento XML que es un subelemento del elemento row <`row`> de forma predeterminada.  
  
 La consulta siguiente especifica el nombre de la columna, el resultado. Por tanto, se agrega un elemento secundario <`result`> al elemento <`row`>.  
  
```  
SELECT 2+2 as result  
for xml PATH  
```  
  
 El resultado es el siguiente:  
  
```  
<row>  
  <result>4</result>  
</row>  
```  
  
 La consulta siguiente especifica el nombre de la columna, ManuWorkCenterInformation, para el XML devuelto por la expresión XQuery especificada con la columna Instructions de tipo **xml** . Por tanto, se agrega un elemento <`ManuWorkCenterInformation`> como elemento secundario del elemento <`row`>.  
  
```  
SELECT   
       ProductModelID,  
       Name,  
       Instructions.query('declare namespace MI="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelManuInstructions";  
                /MI:root/MI:Location   
              ') as ManuWorkCenterInformation  
FROM Production.ProductModel  
WHERE ProductModelID=7  
FOR XML PATH   
go  
```  
  
 El resultado es el siguiente:  
  
```  
<row>  
  <ProductModelID>7</ProductModelID>  
  <Name>HL Touring Frame</Name>  
  <ManuWorkCenterInformation>  
    <MI:Location ...LocationID="10" ...></MI:Location>  
    <MI:Location ...LocationID="20" ...></MI:Location>  
     ...  
  </ManuWorkCenterInformation>  
</row>  
```  
  
## <a name="column-name-does-not-start-with-an-at-sign--and-contains-a-slash-mark-"></a>El nombre de la columna no empieza por \@ y contiene una barra diagonal (/)  
 Si el nombre de la columna no empieza por \@ pero incluye una barra diagonal (/), el nombre de la columna indica una jerarquía XML. Por ejemplo, si el nombre de la columna es "Name1/Name2/Name3.../Name***n*** ", cada Name***i*** representa un nombre de elemento que está anidado en el elemento de fila actual (para i=1) o que se encuentra debajo del elemento con el nombre Name***i-1***. Si Name***n*** empieza por "\@", se asignará a un atributo del elemento Name***n-1***.  
  
 Por ejemplo, la consulta siguiente devuelve un Id. y un nombre de empleado que están representados como un elemento EmpName complejo que incluye nombre, inicial y apellidos.  
  
```  
SELECT EmployeeID "@EmpID",   
       FirstName  "EmpName/First",   
       MiddleName "EmpName/Middle",   
       LastName   "EmpName/Last"  
FROM   HumanResources.Employee E, Person.Contact C  
WHERE  E.EmployeeID = C.ContactID  
AND    E.EmployeeID=1  
FOR XML PATH  
```  
  
 Los nombres de columna se utilizan como una ruta de acceso en la creación de XML en el modo PATH. El nombre de columna que contiene los valores de ID. de empleado comienza por ' \@ '. Por lo tanto, se agrega un atributo, **empid**, al `row` elemento <>. Todas las demás columnas incluyen una barra diagonal ('/') en el nombre de columna que indica la jerarquía. El XML resultante tendrá el elemento secundario <`EmpName`> debajo del elemento <`row`>, y el elemento secundario <`EmpName`> tendrá los elementos secundarios <`First`>, <`Middle`> y <`Last`>.  
  
```  
<row EmpID="1">  
  <EmpName>  
    <First>Gustavo</First>  
    <Last>Achong</Last>  
  </EmpName>  
</row>  
```  
  
 El valor de la inicial del empleado es Null y, de forma predeterminada, el valor Null se asigna a la ausencia del elemento o atributo. Si desea que se generen elementos para los valores NULL, puede especificar la directiva ELEMENTS con XSINIL tal y como se muestra en esta consulta.  
  
```  
SELECT EmployeeID "@EmpID",   
       FirstName  "EmpName/First",   
       MiddleName "EmpName/Middle",   
       LastName   "EmpName/Last"  
FROM   HumanResources.Employee E, Person.Contact C  
WHERE  E.EmployeeID = C.ContactID  
AND    E.EmployeeID=1  
FOR XML PATH, ELEMENTS XSINIL  
```  
  
 El resultado es el siguiente:  
  
```  
<row xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"   
      EmpID="1">  
  <EmpName>  
    <First>Gustavo</First>  
    <Middle xsi:nil="true" />  
    <Last>Achong</Last>  
  </EmpName>  
</row>  
```  
  
 De forma predeterminada, el modo PATH genera XML centrado en elementos. Por tanto, la especificación de la directiva ELEMENTS en una consulta de modo PATH no tiene ningún efecto. No obstante, tal y como se muestra en el ejemplo anterior, la directiva ELEMENTS resulta útil con XSINIL a fin de generar elementos para valores Null.  
  
 Además del Id. y el nombre, la consulta siguiente recupera una dirección del empleado. Según la ruta de acceso de los nombres de las columnas de direcciones, se agregará un elemento secundario <`Address`> al elemento <`row`> y los detalles de la dirección se agregarán como elemento secundario del elemento <`Address`>.  
  
```  
SELECT EmployeeID   "@EmpID",   
       FirstName    "EmpName/First",   
       MiddleName   "EmpName/Middle",   
       LastName     "EmpName/Last",  
       AddressLine1 "Address/AddrLine1",  
       AddressLine2 "Address/AddrLIne2",  
       City         "Address/City"  
FROM   HumanResources.Employee E, Person.Contact C, Person.Address A  
WHERE  E.EmployeeID = C.ContactID  
AND    E.AddressID = A.AddressID  
AND    E.EmployeeID=1  
FOR XML PATH  
```  
  
 El resultado es el siguiente:  
  
```  
<row EmpID="1">  
  <EmpName>  
    <First>Gustavo</First>  
    <Last>Achong</Last>  
  </EmpName>  
  <Address>  
    <AddrLine1>7726 Driftwood Drive</AddrLine1>  
    <City>Monroe</City>  
  </Address>  
</row>  
```  
  
## <a name="several-columns-share-the-same-path-prefix"></a>Varias columnas comparten el mismo prefijo de ruta de acceso  
 Si varias columnas consecutivas comparten el mismo prefijo de ruta de acceso, se agruparán con el mismo nombre. Si se utilizan distintos prefijos de espacio de nombres aunque estén enlazados al mismo espacio de nombres, una ruta de acceso se considerará diferente. En la consulta anterior, las columnas FirstName, MiddleName y LastName comparten el mismo prefijo EmpName. Por tanto, se agregarán como elementos secundarios del elemento <`EmpName`>. Lo mismo ocurrió al crear el elemento <`Address`> en el ejemplo anterior.  
  
## <a name="one-column-has-a-different-name"></a>Una columna tiene un nombre distinto  
 Si aparece una columna con un nombre distinto, interrumpirá la agrupación, tal y como se muestra en la siguiente consulta modificada. La consulta interrumpe la agrupación de FirstName, MiddleName y LastName, tal y como se especificaba en la consulta anterior, al agregar columnas de dirección entre las columnas FirstName y MiddleName.  
  
```  
SELECT EmployeeID "@EmpID",   
       FirstName "EmpName/First",   
       AddressLine1 "Address/AddrLine1",  
       AddressLine2 "Address/AddrLIne2",  
       City "Address/City",  
       MiddleName "EmpName/Middle",   
       LastName "EmpName/Last"  
FROM   HumanResources.EmployeeAddress E, Person.Contact C, Person.Address A  
WHERE  E.EmployeeID = C.ContactID  
AND    E.AddressID = A.AddressID  
AND    E.EmployeeID=1  
FOR XML PATH  
```  
  
 Como resultado, la consulta crea dos elementos <`EmpName`>. El primer elemento <`EmpName`> tiene el elemento secundario <`FirstName`> y el segundo elemento <`EmpName`> tiene los elementos secundarios <`MiddleName`> y <`LastName`>.  
  
 El resultado es el siguiente:  
  
```  
<row EmpID="1">  
  <EmpName>  
    <First>Gustavo</First>  
  </EmpName>  
  <Address>  
    <AddrLine1>7726 Driftwood Drive</AddrLine1>  
    <City>Monroe</City>  
  </Address>  
  <EmpName>  
    <Last>Achong</Last>  
  </EmpName>  
</row>  
```  
  
## <a name="see-also"></a>Consulte también  
 [Usar el modo PATH con FOR XML](use-path-mode-with-for-xml.md)  
  
  
