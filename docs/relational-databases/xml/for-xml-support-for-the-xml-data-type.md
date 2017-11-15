---
title: Compatibilidad de FOR XML con el tipo de datos xml | Microsoft Docs
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: dbe-xml
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- user-defined functions [SQL Server], XML
- xml data type [SQL Server], FOR XML clause
ms.assetid: 365de07d-694c-4c8b-b671-8825be27f87c
caps.latest.revision: "24"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 47b118396533dc8152dc28a15c067d8ecebe7ea5
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/09/2017
---
# <a name="for-xml-support-for-the-xml-data-type"></a>Compatibilidad de FOR XML con el tipo de datos xml
  Si una consulta FOR XML especifica una columna de tipo **xml** en la cláusula SELECT, los valores de columna se asignan como elementos en el XML devuelto, aunque no se especifique la directiva ELEMENTS. Las declaraciones XML en la columna de tipo **xml** no se serializan.  
  
 Por ejemplo, la consulta siguiente recupera información de contacto de clientes, como las columnas `BusinessEntityID`, `FirstName`y `LastName` , y los números de teléfono de la columna `AdditionalContactInfo` de tipo **xml** .  
  
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
  
 Como la consulta no especifica la directiva ELEMENTS, los valores de columna se devuelven como atributos, excepto en el caso de los valores de información de contacto adicional recuperados de la columna de tipo **xml** . Estos se devuelven como elementos.  
  
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
  
 En el ejemplo siguiente se muestra cómo la lógica de procesamiento de FOR XML no serializa las declaraciones XML de los datos XML de una columna de tipo **xml** :  
  
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
  
-   Una tabla con una sola columna de tipo **xml**  
  
-   Una instancia del tipo **xml**  
  
 Por ejemplo, la siguiente función definida por el usuario devuelve una tabla con una sola columna de tipo **xm**:  
  
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
  
 Se puede ejecutar la función definida por el usuario y consultar la tabla que devuelve. En este ejemplo, el XML devuelto al consultar la tabla se asigna a una variable de tipo **xml** .  
  
```  
declare @x xml;  
set @x = (SELECT * FROM MyUDF(19));  
select @x;  
```  
  
 Este es otro ejemplo de función definida por el usuario. Esta función definida por el usuario devuelve una instancia de tipo **xml** . En este ejemplo, la función definida por el usuario devuelve una instancia XML con tipo, porque se especifica el espacio de nombres del esquema.  
  
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
  
 El XML devuelto por la función definida por el usuario se puede asignar a una variable de tipo **xml** , como se indica a continuación:  
  
```  
declare @x xml;  
SELECT @x= dbo.MyUDF4 (19) ;  
select @x;  
```  
  
## <a name="see-also"></a>Vea también  
 [Compatibilidad con FOR XML para varios tipos de datos de SQL Server](../../relational-databases/xml/for-xml-support-for-various-sql-server-data-types.md)  
  
  
