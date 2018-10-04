---
title: Compatibilidad de FOR XML con el tipo de datos xml | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: xml
ms.topic: conceptual
helpviewer_keywords:
- user-defined functions [SQL Server], XML
- xml data type [SQL Server], FOR XML clause
ms.assetid: 365de07d-694c-4c8b-b671-8825be27f87c
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 1a3a4cea6424f8bfb89207050719ec0db554fdd7
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/02/2018
ms.locfileid: "48130285"
---
# <a name="for-xml-support-for-the-xml-data-type"></a>Compatibilidad de FOR XML con el tipo de datos xml
  Si una consulta FOR XML especifica una columna de `xml` tipo en la cláusula SELECT, los valores de columna se asignan como elementos en el XML devuelto, independientemente de si especifica la directiva Elements. Las declaraciones XML en la columna de tipo `xml` no se serializan.  
  
 Por ejemplo, la consulta siguiente recupera información de contacto de cliente, como el `BusinessEntityID`, `FirstName`, y `LastName` columnas y los números de teléfono desde el `AdditionalContactInfo` columna de `xml` tipo.  
  
```  
USE AdventureWorks2012;  
GO  
SELECT BusinessEntityID, FirstName, LastName, AdditionalContactInfo.query('  
declare namespace act="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ContactTypes";  
 //act:telephoneNumber/act:number  
') AS PhoneNumber  
FROM Person.Person  
WHERE AdditionalContactInfo.query('  
declare namespace act="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ContactTypes";  
 //act:telephoneNumber/act:number  
')IS NOT NULL  
FOR XML AUTO, TYPE;  
```  
  
 Dado que la consulta no especifica la directiva Elements, los valores de columna se devuelven como atributos, excepto los valores de información de contacto adicional recuperados de la `xml` columna de tipo. Estos se devuelven como elementos.  
  
 Éste es el resultado parcial:  
  
 `<Person.Person BusinessEntityID="291" FirstName="Gustavo" LastName="Achong">`  
  
 `<PhoneNumber>`  
  
 `<act:number xmlns:act="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ContactTypes">425-555-1112</act:number>`  
  
 `<act:number xmlns:act="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ContactTypes">425-555-1111</act:number>`  
  
 `</PhoneNumber>`  
  
 `</Person.Person>`  
  
 `<Person.Person BusinessEntityID="293" FirstName="Catherine" LastName="Abel">`  
  
 `<PhoneNumber>`  
  
 `<act:number xmlns:act="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ContactTypes">206-555-2222</act:number>`  
  
 `<act:number xmlns:act="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ContactTypes">206-555-1234</act:number>`  
  
 `</PhoneNumber>`  
  
```  
</Person.Person>  
...  
```  
  
 Si se especifica un alias de columna para la columna XML generada por la consulta XQuery, se utiliza ese alias para agregar un elemento contenedor alrededor del XML generado. Por ejemplo, la consulta siguiente especifica `MorePhoneNumbers` como alias de columna:  
  
```  
SELECT BusinessEntityID, FirstName, LastName, AdditionalContactInfo.query('  
declare namespace act="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ContactTypes";  
 //act:telephoneNumber/act:number  
') AS PhoneNumber  
FROM Person.Person  
WHERE AdditionalContactInfo.query('  
declare namespace act="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ContactTypes";  
 //act:telephoneNumber/act:number  
')IS NOT NULL  
FOR XML AUTO, TYPE;  
```  
  
 El XML devuelto por la consulta XQuery se incluye dentro del elemento <`MorePhoneNumbers`>, como se muestra en el siguiente resultado parcial:  
  
 `<Person.Person BusinessEntityID="291" FirstName="Gustavo" LastName="Achong">`  
  
 `<MorePhoneNumbers>`  
  
 `<act:number xmlns:act="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ContactTypes">425-555-1112</act:number>`  
  
 `<act:number xmlns:act="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ContactTypes">425-555-1111</act:number>`  
  
 `</MorePhoneNumbers>`  
  
 `</Person.Person>`  
  
 `<Person.Person BusinessEntityID="293" FirstName="Catherine" LastName="Abel">`  
  
 `<MorePhoneNumbers>`  
  
 `<act:number xmlns:act="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ContactTypes">206-555-2222</act:number>`  
  
 `<act:number xmlns:act="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ContactTypes">206-555-1234</act:number>`  
  
 `</MorePhoneNumbers>`  
  
```  
</Person.Person>  
...  
```  
  
 Si se especifica la directiva ELEMENTS en la consulta, se devolverán BusinessEntityID, LastName y FirstName como elementos en el XML resultante.  
  
 El ejemplo siguiente se muestra que la lógica de procesamiento de FOR XML no serializa las declaraciones XML de los datos XML desde un `xml` columna de tipo:  
  
```  
create table t(i int, x xml)  
go  
insert into t values(1, '<?xml version="1.0" encoding="UTF-8" ?>  
                             <Root SomeID="10" />')  
select i, x  
from   t  
for xml auto;  
```  
  
 Éste es el resultado. En el resultado, no se serializa la declaración XML <`?xml version="1.0" encoding="UTF-8" ?`>.  
  
```  
<root>  
  <t i="1">  
    <x>  
      <Root SomeID="10" />  
    </x>  
  </t>  
</root>  
```  
  
## <a name="returning-xml-from-a-user-defined-function"></a>Devolver XML con una función definida por el usuario  
 Se pueden utilizar consultas FOR XML para obtener XML utilizando una función definida por el usuario que devuelva alguno de los siguientes resultados:  
  
-   Una tabla con una sola columna de tipo `xml`  
  
-   Una instancia de la `xml` tipo  
  
 Por ejemplo, la siguiente función definida por el usuario devuelve una tabla con una sola columna de `xm`tipo l:  
  
```  
USE AdventureWorks2012;  
GO  
CREATE FUNCTION dbo.MyUDF (@ProudctModelID int)  
RETURNS @T TABLE  
  (  
     ProductDescription xml  
  )  
AS  
BEGIN  
  INSERT @T  
     SELECT CatalogDescription.query('  
declare namespace PD="http://www.adventure-works.com/schemas/products/description";  
                    //PD:ProductDescription  ')  
     FROM Production.ProductModel  
     WHERE ProductModelID = @ProudctModelID  
  RETURN  
END;  
```  
  
 Se puede ejecutar la función definida por el usuario y consultar la tabla que devuelve. En este ejemplo, el XML devuelto al consultar la tabla se asigna a un `xml` variable de tipo.  
  
```  
declare @x xml;  
set @x = (SELECT * FROM MyUDF(19));  
select @x;  
```  
  
 Este es otro ejemplo de función definida por el usuario. Esta función definida por el usuario devuelve una instancia del tipo `xml`. En este ejemplo, la función definida por el usuario devuelve una instancia XML con tipo, porque se especifica el espacio de nombres del esquema.  
  
```  
DROP FUNCTION dbo.MyUDF;  
GO  
CREATE FUNCTION MyUDF (@ProductModelID int)   
RETURNS xml ([Production].[ProductDescriptionSchemaCollection])  
AS  
BEGIN  
  declare @x xml  
  set @x =   ( SELECT CatalogDescription  
          FROM Production.ProductModel  
          WHERE ProductModelID = @ProductModelID )  
  return @x  
END;  
```  
  
 El resultado XML devuelto por la función definida por el usuario se puede asignar a una variable de tipo `xml`, como se indica a continuación:  
  
```  
declare @x xml;  
SELECT @x= dbo.MyUDF4 (19) ;  
select @x;  
```  
  
## <a name="see-also"></a>Vea también  
 [Compatibilidad con FOR XML para varios tipos de datos de SQL Server](for-xml-support-for-various-sql-server-data-types.md)  
  
  
