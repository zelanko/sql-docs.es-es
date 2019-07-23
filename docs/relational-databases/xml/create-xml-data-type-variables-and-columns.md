---
title: Creación de variables y columnas del tipo de datos XML | Microsoft Docs
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: xml
ms.topic: conceptual
helpviewer_keywords:
- xml data type [SQL Server], variables
- xml data type [SQL Server], columns
ms.assetid: 8994ab6e-5519-4ba2-97a1-fac8af6f72db
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 16cb419ef7cc893575e91c695158e9d7b66ce2c0
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "67984869"
---
# <a name="create-xml-data-type-variables-and-columns"></a>Crear variables y columnas del tipo de datos XML
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]
  El tipo de datos **xml** es un tipo de datos integrado en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] y es de algún modo similar a otros tipos integrados, como **int** y **varchar**. Al igual que ocurre con otros tipos integrados, se puede usar el tipo de datos **xml** como un tipo de columna al crear una tabla como un tipo de variable, un tipo de parámetro, un tipo de valor devuelto por una función o en [CAST y CONVERT](../../t-sql/functions/cast-and-convert-transact-sql.md).  
  
## <a name="creating-columns-and-variables"></a>Crear columnas y variables  
 Para crear una columna de tipo `xml` como parte de una tabla, utilice una instrucción `CREATE TABLE` , como se muestra en el ejemplo siguiente:  
  
```  
CREATE TABLE T1(Col1 int primary key, Col2 xml)   
```  
  
 Puede utilizar una instrucción `DECLARE statement` para crear una variable de tipo `xml` , como se muestra en el ejemplo siguiente.  
  
```  
DECLARE @x xml   
```  
  
 Para crear una variable de tipo `xml` , especifique una colección de esquemas XML, como se muestra en el ejemplo siguiente.  
  
```  
DECLARE @x xml (Sales.StoreSurveySchemaCollection)  
```  
  
 Para pasar un parámetro de tipo `xml` a un procedimiento almacenado, utilice una instrucción `CREATE PROCEDURE` , como se muestra en el ejemplo siguiente.  
  
```  
CREATE PROCEDURE SampleProc(@XmlDoc xml) AS ...   
```  
  
 Puede utilizar XQuery para consultar instancias XML almacenadas en columnas, parámetros o variables. También puede utilizar el Lenguaje de manipulación de datos XML (XML DML) para aplicar actualizaciones a las instancias XML. Puesto que el estándar XQuery no definió el DML de XQuery cuando se desarrolló, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] incluye las extensiones del [Lenguaje de manipulación de datos XML (XML DML)](../../t-sql/xml/xml-data-modification-language-xml-dml.md) en XQuery. Estas extensiones permiten realizar operaciones de inserción, actualización y eliminación.  
  
## <a name="assigning-defaults"></a>Asignar valores predeterminados  
 En una tabla, puede asignar una instancia XML predeterminada a una columna de tipo **xml** . Puede proporcionar el XML predeterminado de una de estas dos maneras: con una constante XML o con una conversión explícita al tipo **xml** .  
  
 Para proporcionar el XML predeterminado como una constante XML, utilice la sintaxis como se muestra en el ejemplo siguiente. Observe que la cadena se convierte implícitamente al tipo **xml** .  
  
```  
CREATE TABLE T (XmlColumn xml default N'<element1/><element2/>')  
```  
  
 Para proporcionar el XML predeterminado mediante una operación de conversión ( `CAST` ) explícita a `xml`, utilice la sintaxis como se muestra en el ejemplo siguiente.  
  
```  
CREATE TABLE T (XmlColumn xml   
                  default CAST(N'<element1/><element2/>' AS xml))  
```  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] también admite restricciones NULL y NOT NULL en columnas de tipo **xml** . Por ejemplo:  
  
```  
CREATE TABLE T (XmlColumn xml NOT NULL)  
```  
  
## <a name="specifying-constraints"></a>Especificar restricciones  
 Al crear columnas de tipo **xml** , puede definir restricciones de nivel de columna o de nivel de tabla. Las restricciones se emplean en estas situaciones:  
  
-   Sus reglas de negocios no se pueden expresar en esquemas XML. Por ejemplo, la dirección de entrega de una floristería debe estar a menos de 75 kilómetros de su ubicación. Esto se puede escribir como una restricción en la columna XML. La restricción puede afectar a métodos de tipo de datos **xml** .  
  
-   La restricción afecta a otras columnas XML o no XML de la tabla. Un ejemplo puede ser obligar a que el Id. de un cliente (`/Customer/@CustId`) existente en una instancia XML coincida con el valor de una columna relacional CustomerID.  
  
 Puede especificar restricciones para columnas de tipo de datos **xml** con o sin tipo. Sin embargo, no puede usar los [métodos de tipo de datos XML](../../t-sql/xml/xml-data-type-methods.md) al especificar restricciones. También debe tener en cuenta que el tipo de datos **xml** no admite las restricciones de columna y de tabla siguientes:  
  
-   PRIMARY KEY / FOREIGN KEY  
  
-   UNIQUE  
  
-   COLLATE  
  
     XML proporciona su propia codificación. Las intercalaciones solo se aplican a los tipos de cadena. El tipo de datos **xml** no es un tipo de cadena. No obstante, tiene una representación de cadena y permite la conversión a tipos de datos de cadena y desde tipos de datos de cadena.  
  
-   RULE  
  
 Una alternativa al uso de restricciones consiste en crear una función de contenedor definida por el usuario para ajustar el método de tipo de datos **xml** y especificar una función definida por el usuario en la restricción CHECK, como se muestra en el siguiente ejemplo.  
  
 En el siguiente ejemplo, la restricción de `Col2` especifica que cada instancia XML almacenada en esta columna debe tener un elemento `<ProductDescription>` con un atributo `ProductID` . Esta restricción se exige mediante la siguiente función definida por el usuario:  
  
```  
CREATE FUNCTION my_udf(@var xml) returns bit  
AS BEGIN   
RETURN @var.exist('/ProductDescription/@ProductID')  
END  
GO  
```  
  
 Observe que el método `exist()` del tipo de datos `xml` devuelve `1` si el elemento `<ProductDescription>` de la instancia contiene el atributo `ProductID` . En caso contrario, devuelve `0`.  
  
 En este momento, puede crear una tabla con una restricción de columna del modo siguiente:  
  
```  
CREATE TABLE T (  
    Col1 int primary key,   
    Col2 xml check(dbo.my_udf(Col2)=1))  
GO  
```  
  
 La inserción siguiente se realiza correctamente:  
  
```  
INSERT INTO T values(1,'<ProductDescription ProductID="1" />')  
```  
  
 La inserción siguiente no se realiza correctamente a causa de la restricción:  
  
```  
INSERT INTO T values(1,'<Product />')  
```  
  
## <a name="same-or-different-table"></a>La misma tabla o una tabla diferente  
 Es posible crear una columna de tipo de datos **xml** en una tabla que contenga otras columnas relacionales o en otra tabla con una relación de clave externa con una tabla principal.  
  
 Puede crear una columna de tipo de datos **xml** en la misma tabla si se cumple una de las condiciones siguientes:  
  
-   La aplicación efectúa una recuperación de datos en la columna XML y no requiere un índice XML en la columna XML.  
  
-   Desea generar un índice XML en la columna de tipo de datos **xml** y la clave principal de la tabla principal es la misma que su clave de agrupación en clústeres. Para obtener más información, vea [Índices XML &#40;SQL Server&#41;](../../relational-databases/xml/xml-indexes-sql-server.md).  
  
 Puede crear la columna de tipo de datos **xml** en otra tabla si se cumplen las condiciones siguientes:  
  
-   Quiere generar un índice XML en la columna de tipo de datos **xml** , pero la clave principal de la tabla principal es distinta de su clave de agrupación en clústeres, la tabla principal no tiene una clave principal, o la tabla principal es un montón (sin clave de agrupación en clústeres). Esto puede ser cierto si la tabla principal ya existe.  
  
-   No desea que se ralenticen los recorridos de las tablas por la presencia de la columna XML en la tabla. Ésta usa espacio independientemente de si está o no almacenada de manera consecutiva.  
  
  
