---
title: Directiva TYPE en consultas FOR XML | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: xml
ms.reviewer: 
ms.suite: sql
ms.technology:
- dbe-xml
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- FOR XML clause, TYPE directive
- TYPE directive
ms.assetid: a3df6c30-1f25-45dc-b5a9-bd0e41921293
caps.latest.revision: 
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 20d3894f0f2eecbf491e20f10b0258686848b401
ms.sourcegitcommit: 37f0b59e648251be673389fa486b0a984ce22c81
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 02/12/2018
---
# <a name="type-directive-in-for-xml-queries"></a>Directiva TYPE en consultas FOR XML
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]
  La compatibilidad de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] con [xml &#40;Transact-SQL&#41;](../../t-sql/xml/xml-transact-sql.md) ofrece la posibilidad de solicitar la devolución del resultado de una consulta FOR XML como tipo de datos **xml** mediante la especificación de la directiva TYPE. Esto permite procesar el resultado de una consulta FOR XML en el servidor. Por ejemplo, puede especificar una XQuery en el mismo, asignar el resultado a una variable de tipo **xml** o escribir consultas [FOR XML anidadas](../../relational-databases/xml/use-nested-for-xml-queries.md).  
  
> [!NOTE]  
>  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] devuelve al cliente datos de instancia de tipo XML como resultado de distintas construcciones de servidor, como por ejemplo consultas FOR XML que usan la directiva TYPE o en las que se usa el tipo de datos **xml** para devolver valores de datos de instancia XML procedentes de columnas de tablas SQL y parámetros de salida. En el código de las aplicaciones cliente, el proveedor ADO.NET solicita que se envíe esta información de tipo de datos XML con una codificación binaria desde el servidor. Sin embargo, si utiliza FOR XML sin la directiva TYPE, se devolverán los datos XML en forma de cadena. En cualquier caso, el proveedor del cliente siempre podrá controlar cualquier formato de tipo XML. Tenga en cuenta que la cláusula FOR XML de nivel superior sin la directiva TYPE no puede utilizarse con cursores.  
  
## <a name="examples"></a>Ejemplos  
 En los ejemplos siguientes se muestra el uso de la directiva TYPE con consultas FOR XML.  
  
### <a name="retrieving-for-xml-query-results-as-xml-type"></a>Recuperar resultados de consultas FOR XML en forma de xml  
 En la consulta siguiente se recupera información de contacto de clientes de la tabla `Contacts` . Puesto que se especifica la directiva `TYPE` en `FOR XML`, el resultado se devuelve como de tipo **xml** .  
  
```  
USE AdventureWorks2012;  
Go  
SELECT BusinessEntityID, FirstName, LastName  
FROM Person.Person  
ORDER BY BusinessEntityID  
FOR XML AUTO, TYPE;  
```  
  
 Éste es el resultado parcial:  
  
 `<Person.Person BusinessEntityID="1" FirstName="Ken" LastName="Sánchez"/>`  
  
 `<Person.Person BusinessEntityID="2" FirstName="Terri" LastName="Duffy"/>`  
  
 `...`  
  
### <a name="assigning-for-xml-query-results-to-an-xml-type-variable"></a>Asignar resultados de consultas FOR XML a una variable de tipo xml  
 En el ejemplo siguiente, se asigna un resultado de FOR XML a una variable de tipo **xml**, `@x`. La consulta recupera información de contacto, como `BusinessEntityID`, `FirstName` o `LastName`, y números de teléfono adicionales, de la columna `AdditionalContactInfo` de **xml** `TYPE`. Puesto que la cláusula `FOR XML` especifica la directiva `TYPE`, se devuelve XML en forma de tipo **xml** y se asigna a una variable.  
  
```  
USE AdventureWorks2012;  
GO  
DECLARE @x xml;  
SET @x = (  
   SELECT BusinessEntityID,   
          FirstName,   
          LastName,   
          AdditionalContactInfo.query('  
declare namespace aci="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ContactInfo";  
declare namespace act="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ContactTypes";  
              //act:telephoneNumber/act:number') as MorePhoneNumbers  
   FROM Person.Person  
   FOR XML AUTO, TYPE);  
SELECT @x;  
GO  
```  
  
### <a name="querying-results-of-a-for-xml-query"></a>Consultar los resultados de una consulta FOR XML  
 Las consultas FOR XML devuelven XML. Por tanto, puede aplicar métodos del tipo **xml** , como **query()** y **value()**, al resultado XML devuelto por las consultas FOR XML.  
  
 En la consulta siguiente, se usa el método `query()` del tipo de datos **xml** para consultar el resultado de la consulta `FOR XML`. Para obtener más información, vea [query&#40;&#41; &#40;método de tipo de datos xml&#41;](../../t-sql/xml/query-method-xml-data-type.md).  
  
```  
USE AdventureWorks2012;  
GO  
SELECT (SELECT BusinessEntityID, FirstName, LastName, AdditionalContactInfo.query('  
DECLARE namespace aci="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ContactInfo";  
DECLARE namespace act="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ContactTypes";  
 //act:telephoneNumber/act:number  
') AS PhoneNumbers  
FROM Person.Person  
FOR XML AUTO, TYPE).query('/Person.Person[1]');  
```  
  
 La consulta `SELECT … FOR XML` interna devuelve un resultado de tipo **xml** al que la instrucción `SELECT` externa aplica el método `query()` al tipo **xml**. Observe la directiva `TYPE` especificada.  
  
 El resultado es el siguiente:  
  
 `<Person.Person BusinessEntityID="1" FirstName="Ken" LastName="Sánchez">`  
  
 `<PhoneNumbers>`  
  
 `<act:number xmlns:act="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ContactTypes">111-111-1111</act:number>`  
  
 `<act:number xmlns:act="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ContactTypes">112-111-1111</act:number>`  
  
 `</PhoneNumbers>`  
  
 `</Person.Person>`  
  
 En la consulta siguiente, el método `value()` del tipo de datos **xml** se usa para recuperar un valor del resultado XML devuelto por la consulta `SELECT…FOR XML`. Para obtener más información, vea [value&#40;&#41; &#40;método de tipo de datos xml&#41;](../../t-sql/xml/value-method-xml-data-type.md).  
  
```  
USE AdventureWorks2012;  
GO  
DECLARE @FirstPhoneFromAdditionalContactInfo varchar(40);  
SELECT @FirstPhoneFromAdditionalContactInfo =   
 ( SELECT BusinessEntityID, FirstName, LastName, AdditionalContactInfo.query('  
declare namespace aci="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ContactInfo";  
declare namespace act="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ContactTypes";  
   //act:telephoneNumber/act:number  
   ') AS PhoneNumbers  
   FROM Person.Person Contact  
   FOR XML AUTO, TYPE).value('  
declare namespace act="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ContactTypes";  
  /Contact[@BusinessEntityID="1"][1]/PhoneNumbers[1]/act:number[1]', 'varchar(40)'  
 )  
SELECT @FirstPhoneFromAdditionalContactInfo;  
```  
  
 La expresión de ruta de acceso XQuery del método `value()` recupera el primer número de teléfono de un contacto de cliente cuyo `BusinessEntityID` es `1`.  
  
> [!NOTE]  
>  Si no se especifica la directiva TYPE, se devolverá el resultado de la consulta FOR XML con el tipo **nvarchar(max)**.  
  
### <a name="using-for-xml-query-results-in-insert-update-and-delete-transact-sql-dml"></a>Utilizar resultados de consultas FOR XML en INSERT, UPDATE y DELETE (DML de Transact-SQL)  
 En el ejemplo siguiente se muestra el modo en el que se pueden utilizar las consultas FOR XML en instrucciones del lenguaje de manipulación de datos (DML). En este ejemplo, `FOR XML` devuelve una instancia del tipo **xml** . La instrucción `INSERT` inserta esta instancia de tipo XML en una tabla.  
  
```  
CREATE TABLE T1(intCol int, XmlCol xml);  
GO  
INSERT INTO T1   
VALUES(1, '<Root><ProductDescription ProductModelID="1" /></Root>');  
GO  
  
CREATE TABLE T2(XmlCol xml)  
GO  
INSERT INTO T2(XmlCol)   
SELECT (SELECT XmlCol.query('/Root')   
        FROM T1   
        FOR XML AUTO,TYPE);   
GO  
```  
  
## <a name="see-also"></a>Ver también  
 [FOR XML &#40;SQL Server&#41;](../../relational-databases/xml/for-xml-sql-server.md)  
  
  
