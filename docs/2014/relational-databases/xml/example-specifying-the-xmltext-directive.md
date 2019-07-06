---
title: 'Ejemplo: Especificación de la directiva XMLTEXT | Microsoft Docs'
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: xml
ms.topic: conceptual
helpviewer_keywords:
- XMLTEXT directive
ms.assetid: e78008ec-51e8-4fd1-b86f-1058a781de17
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 56ccb1e8a25b7d9f138c2900422d301919fef039
ms.sourcegitcommit: d9c5b9ab3c282775ed61712892eeb3e150ccc808
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/05/2019
ms.locfileid: "67597552"
---
# <a name="example-specifying-the-xmltext-directive"></a>Ejemplo: Especificación de la directiva XMLTEXT
  En este ejemplo se muestra cómo se tratan los datos de la columna de desbordamiento mediante la directiva `XMLTEXT` en una instrucción `SELECT` con el modo EXPLICIT.  
  
 Considere la tabla `Person` . Esta tabla dispone de una columna `Overflow` que almacena la parte no utilizada del documento XML.  
  
```  
USE tempdb;  
GO  
CREATE TABLE Person(PersonID varchar(5), PersonName varchar(20), Overflow nvarchar(200));  
GO  
INSERT INTO Person VALUES   
    ('P1','Joe',N'<SomeTag attr1="data">content</SomeTag>')  
   ,('P2','Joe',N'<SomeTag attr2="data"/>')  
   ,('P3','Joe',N'<SomeTag attr3="data" PersonID="P">content</SomeTag>');  
```  
  
 Esta consulta recupera columnas de la tabla `Person` . En la columna `Overflow` no se especifica *AttributeName* , sino que *directive* se establece en `XMLTEXT` como parte del proceso destinado a proporcionar un nombre de columna de la tabla universal.  
  
```  
SELECT 1 as Tag, NULL as parent,  
       PersonID as [Parent!1!PersonID],  
       PersonName as [Parent!1!PersonName],  
       Overflow as [Parent!1!!XMLTEST] -- No AttributeName; XMLTEXT directive  
FROM Person  
FOR XML EXPLICIT;  
```  
  
 En el documento XML resultante:  
  
-   Puesto que no se especifica *AttributeName* para la columna `Overflow` y se especifica la directiva `xmltext`, los atributos del elemento <`overflow`> se anexan a la lista de atributos del elemento <`Parent`> que los incluye.  
  
-   Dado que el atributo `PersonID` del elemento <`xmltext`> está en conflicto con el atributo `PersonID` recuperado en el mismo nivel de elementos, se omite el atributo del elemento <`xmltext`>, incluso aunque `PersonID` sea NULL. En general, un atributo invalida un atributo del mismo nombre en el desbordamiento.  
  
 Éste es el resultado:  
  
 `<Parent PersonID="P1" PersonName="Joe" attr1="data">content</Parent>`  
  
 `<Parent PersonID="P2" PersonName="Joe" attr2="data"></Parent>`  
  
 `<Parent PersonID="P3" PersonName="Joe" attr3="data">content</Parent>`  
  
 Si los datos de desbordamiento contienen subelementos y se especifica la misma consulta, se agregan los subelementos en la columna `Overflow` como subelementos del elemento <`Parent`> que los incluye.  
  
 Por ejemplo, puede cambiar los datos de la tabla `Person` para que la columna `Overflow` disponga ahora de subelementos.  
  
```  
USE tempdb;  
GO  
TRUNCATE TABLE Person;  
GO  
INSERT INTO Person VALUES   
    ('P1','Joe',N'<SomeTag attr1="data">content</SomeTag>')  
   ,('P2','Joe',N'<SomeTag attr2="data"/>')  
    ,('P3','Joe',N'<SomeTag attr3="data" PersonID="P"><name>PersonName</name></SomeTag>');  
```  
  
 Si se ejecuta la misma consulta, se agregan los subelementos del elemento <`xmltext`> como subelementos del elemento <`Parent`> que los incluye.  
  
```  
SELECT 1 as Tag, NULL as parent,  
       PersonID as [Parent!1!PersonID],  
       PersonName as [Parent!1!PersonName],  
       Overflow as [Parent!1!!XMLTEXT] -- no AttributeName, XMLTEXT directive  
FROM Person  
FOR XML EXPLICIT;  
```  
  
 Éste es el resultado:  
  
 `<Parent PersonID="P1" PersonName="Joe" attr1="data">content</Parent>`  
  
 `<Parent PersonID="P2" PersonName="Joe" attr2="data"></Parent>`  
  
 `<Parent PersonID="P3" PersonName="Joe" attr3="data">`  
  
 `<name>PersonName</name>`  
  
 `</Parent>`  
  
 Si se especifica *AttributeName* con la directiva `xmltext`, se agregan los atributos del elemento <`overflow`> como atributos de los subelementos del elemento <`Parent`> que los incluye. El nombre especificado para *AttributeName* se convierte en el nombre del subelemento.  
  
 En esta consulta, *AttributeName*, <`overflow`>, se especifica junto con el `xmltext` directiva:  
  
```  
SELECT 1 as Tag, NULL as parent,  
       PersonID as [Parent!1!PersonID],  
       PersonName as [Parent!1!PersonName],  
       Overflow as [Parent!1!overflow!XMLTEXT] -- Overflow is AttributeName  
                      -- XMLTEXT is a directive  
FROM Person  
FOR XML EXPLICIT  
```  
  
 Éste es el resultado:  
  
 `<Parent PersonID="P1" PersonName="Joe">`  
  
 `<overflow attr1="data">content</overflow>`  
  
 `</Parent>`  
  
 `<Parent PersonID="P2" PersonName="Joe">`  
  
 `<overflow attr2="data" />`  
  
 `</Parent>`  
  
 `<Parent PersonID="P3" PersonName="Joe">`  
  
 `<overflow attr3="data" PersonID="P">`  
  
 `<name>PersonName</name>`  
  
 `</overflow>`  
  
 `</Parent>`  
  
 En este elemento de consulta, se especifica *directive* para el atributo `PersonName`. De este modo, `PersonName` se agrega como subelemento del elemento <`Parent`> que lo incluye. Los atributos de <`xmltext`> se siguen agregando al elemento <`Parent`> que lo incluye. El contenido del elemento <`overflow`> (los subelementos) se antepone a otros subelementos de los elementos <`Parent`> que lo incluyen.  
  
```  
SELECT 1      AS Tag, NULL as parent,  
       PersonID   AS [Parent!1!PersonID],  
       PersonName AS [Parent!1!PersonName!element], -- element directive  
       Overflow   AS [Parent!1!!XMLTEXT]  
FROM Person  
FOR XML EXPLICIT;  
```  
  
 Éste es el resultado:  
  
 `<Parent PersonID="P1" attr1="data">content<PersonName>Joe</PersonName>`  
  
 `</Parent>`  
  
 `<Parent PersonID="P2" attr2="data">`  
  
 `<PersonName>Joe</PersonName>`  
  
 `</Parent>`  
  
 `<Parent PersonID="P3" attr3="data">`  
  
 `<name>PersonName</name>`  
  
 `<PersonName>Joe</PersonName>`  
  
 `</Parent>`  
  
 Si la columna de datos `XMLTEXT` contiene atributos en el elemento raíz, estos atributos no se muestran en el esquema de datos XML y el analizador de MSXML no valida el fragmento del documento XML resultante. Por ejemplo:  
  
```  
SELECT 1 AS Tag,  
       0 ASParent,  
       N'<overflow a="1"/>' AS 'overflow!1!!xmltext'  
FOR XML EXPLICIT, xmldata;  
```  
  
 Éste es el resultado. Observe que el atributo de desbordamiento `a` no aparece en el esquema devuelto:  
  
 `<Schema name="Schema2"`  
  
 `xmlns="urn:schemas-microsoft-com:xml-data"`  
  
 `xmlns:dt="urn:schemas-microsoft-com:datatypes">`  
  
 `<ElementType name="overflow" content="mixed" model="open">`  
  
 `</ElementType>`  
  
 `</Schema>`  
  
 `<overflow xmlns="x-schema:#Schema2" a="1">`  
  
 `</overflow>`  
  
## <a name="see-also"></a>Vea también  
 [Usar el modo EXPLICIT con FOR XML](use-explicit-mode-with-for-xml.md)  
  
  
