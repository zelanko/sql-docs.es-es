---
title: Comparar XML con tipo y XML sin tipo | Microsoft Docs
description: Obtenga información sobre las principales diferencias entre XML con tipo y sin tipo.
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: xml
ms.topic: conceptual
helpviewer_keywords:
- xml data type [SQL Server], variables
- parameters [XML in SQL Server]
- facets [XML in SQL Server]
- xml data type [SQL Server], columns
- untyped XML
- xml data type [SQL Server], typed xml
- XML [SQL Server], typed
- variables [XML in SQL Server], creating
- xml data type [SQL Server], untyped xml
- columns [XML in SQL Server], creating
- typed XML
- document mode processing [SQL Server]
- XML [SQL Server], untyped
- xml data type [SQL Server], parameters
ms.assetid: 4bc50af9-2f7d-49df-bb01-854d080c72c7
author: MightyPen
ms.author: genemi
ms.openlocfilehash: a31b8e27147f0c9b06c79bf56c1b8ae34f4e8e14
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/01/2020
ms.locfileid: "85775557"
---
# <a name="compare-typed-xml-to-untyped-xml"></a>Comparar XML con tipo y XML sin tipo
[!INCLUDE [SQL Server Azure SQL Database](../../includes/applies-to-version/sql-asdb.md)]
  Se pueden crear variables, parámetros y columnas del tipo de datos **xml** . Opcionalmente, se puede asociar una colección de esquemas XML a una variable, a un parámetro o a una columna de tipo **xml** . En este caso, se dice que la instancia del tipo de datos **xml** es una instancia *con tipo*. En los demás casos, se dice que la instancia XML es una instancia *sin tipo*.  
  
## <a name="well-formed-xml-and-the-xml-data-type"></a>XML correcto y tipo de datos XML  
 El tipo de datos **xml** implementa el tipo de datos **xml** del estándar ISO. Por lo tanto, puede almacenar documentos XML versión 1.0 correctos, así como los denominados fragmentos de contenido XML con nodos de texto y un número arbitrario de elementos de nivel superior en una columna XML sin tipo. El sistema comprueba que todos los datos tienen un formato correcto, no requiere que la columna esté enlazada a esquemas XML y rechaza los datos que no tienen un formato correcto en sentido amplio. Esto también se cumple para parámetros y variables XML sin tipo.  
  
## <a name="xml-schemas"></a>Esquemas XML  
 Un esquema XML proporciona lo siguiente:  
  
-   **Restricciones de validación.** Siempre que se asigna o modifica una instancia XML con tipo, SQL Server valida la instancia.  
  
-   **Información sobre el tipo de datos.** Los esquemas proporcionan información sobre los tipos de atributos y elementos de la instancia de tipo de datos **xml** . La información de tipo proporciona una semántica operacional más precisa para los valores contenidos en la instancia que es posible con **xml**sin tipo. Por ejemplo, se pueden realizar operaciones aritméticas con decimales en un valor decimal, pero no en un valor de cadena. Por este motivo, el almacenamiento de XML con tipo puede ser mucho más compacto que el de XML sin tipo.  
  
## <a name="choosing-typed-or-untyped-xml"></a>Elegir XML con tipo o sin tipo  
 El tipo de datos **xml** sin tipo se emplea en las siguientes situaciones:  
  
-   No tiene un esquema para los datos XML.  
  
-   Tiene esquemas pero no desea que el servidor valide los datos. Esto a veces ocurre cuando una aplicación realiza la validación del lado cliente antes de almacenar los datos en el servidor, almacena temporalmente datos XML que no son válidos según el esquema, o usa componentes del esquema que no son compatibles con el servidor.  
  
 El tipo de datos **xml** con tipo se emplea en las siguientes situaciones:  
  
-   Tiene esquemas para los datos XML y desea que el servidor valide estos datos según los esquemas XML.  
  
-   Desea aprovechar las optimizaciones del almacenamiento y de las consultas en función de la información del tipo.  
  
-   Desea aprovechar mejor la información del tipo durante la compilación de las consultas.  
  
 Columnas, parámetros y variables XML con tipo pueden almacenar documentos o contenido XML. No obstante, hay que especificar con una marca si se va a almacenar un documento o contenido en el momento de la declaración. Además, hay que proporcionar la colección de esquemas XML. Especifique DOCUMENT si cada instancia XML tiene exactamente un elemento de nivel superior. En caso contrario, use CONTENT. El compilador de consultas usa la marca DOCUMENT en comprobaciones de tipo durante la compilación de consultas para inferir elementos singleton de nivel superior.  
  
## <a name="creating-typed-xml"></a>Crear XML con tipo  
 Para poder crear variables, parámetros o columnas **xml** con tipo, primero es necesario registrar la colección de esquemas XML mediante [CREATE XML SCHEMA COLLECTION &#40;Transact-SQL&#41;](../../t-sql/statements/create-xml-schema-collection-transact-sql.md). Después, se puede asociar la colección de esquemas XML a variables, parámetros o columnas del tipo de datos **xml** .  
  
 En los ejemplos siguientes se usa una convención de nomenclatura de dos partes para especificar el nombre de la recopilación de esquemas XML. La primera parte corresponde al nombre de esquema y la segunda al nombre de la colección de esquemas XML.  
  
### <a name="example-associating-a-schema-collection-with-an-xml-type-variable"></a>Ejemplo: Asociación de una colección de esquemas con una variable de tipo XML  
 En el ejemplo siguiente se crea una variable de tipo **xml** y se le asocia una colección de esquemas. La colección de esquemas especificada en el ejemplo ya se ha importado a la base de datos **AdventureWorks** .  
  
```  
DECLARE @x xml (Production.ProductDescriptionSchemaCollection);   
```  
  
### <a name="example-specifying-a-schema-for-an-xml-type-column"></a>Ejemplo: Especificación de un esquema para una columna de tipo XML  
 En el ejemplo siguiente se crea una tabla con una columna de tipo **xml** y se especifica un esquema para la columna:  
  
```  
CREATE TABLE T1(  
 Col1 int,   
 Col2 xml (Production.ProductDescriptionSchemaCollection)) ;  
```  
  
### <a name="example-passing-an-xml-type-parameter-to-a-stored-procedure"></a>Ejemplo: Cómo pasar un parámetro de tipo XML a un procedimiento almacenado  
 En el ejemplo siguiente se pasa un parámetro de tipo **xml** a un procedimiento almacenado y se especifica un esquema para la variable:  
  
```  
CREATE PROCEDURE SampleProc   
  @ProdDescription xml (Production.ProductDescriptionSchemaCollection)   
AS   
...  
```  
  
 Tenga en cuenta lo siguiente sobre la colección de esquemas XML:  
  
-   Una colección de esquemas XML solo está disponible en la base de datos en la que se ha registrado mediante [CREATE XML SCHEMA COLLECTION](../../t-sql/statements/create-xml-schema-collection-transact-sql.md).  
  
-   Si se realiza la conversión de una cadena a un tipo de datos **xml** con tipo, el análisis también realiza la validación y la conversión de tipos, de acuerdo con los espacios de nombres de los esquemas XML de la colección especificada.  
  
-   Es posible convertir un tipo de datos **xml** con tipo en un tipo de datos **xml** sin tipo, y viceversa.  
  
 Para obtener más información sobre otras maneras de generar XML en SQL Server, vea [Crear instancias de datos XML](../../relational-databases/xml/create-instances-of-xml-data.md). Una vez generado el XML, se puede asignar a una variable del tipo de datos **xml** o se puede almacenar en columnas de tipo **xml** para su posterior procesamiento.  
  
 En la jerarquía de tipos de datos, el tipo de datos **xml** aparece por debajo de **sql_variant** y los tipos definidos por el usuario, pero por encima de los tipos integrados.  
  
### <a name="example-specifying-facets-to-constrain-a-typed-xml-column"></a>Ejemplo: Especificación de facetas para restringir una columna XML con tipo  
 En las columnas **xml** con tipo se puede restringir la columna para permitir que solo se almacenen en ella elementos únicos de nivel superior para cada instancia. Para ello, se especifica la faceta opcional `DOCUMENT` cuando se crea una tabla, como se muestra en el ejemplo siguiente:  
  
```  
CREATE TABLE T(Col1 xml   
   (DOCUMENT Production.ProductDescriptionSchemaCollection));  
GO  
DROP TABLE T;  
GO  
```  
  
 De manera predeterminada, las instancias se almacenan en la columna **xml** con tipo como contenido XML y no como documentos XML. Esto permite lo siguiente:  
  
-   Cero o varios elementos de nivel superior  
  
-   Nodos de texto en elementos de nivel superior  
  
 Este comportamiento también se puede especificar explícitamente, agregando la faceta `CONTENT` , tal y como se muestra en el ejemplo siguiente:  
  
```  
CREATE TABLE T(Col1 xml(CONTENT Production.ProductDescriptionSchemaCollection));  
GO -- Default  
```  
  
 Tenga en cuenta que puede especificar las facetas DOCUMENT/CONTENT opcionales en cualquier lugar en que defina un tipo **xml** (XML con tipo). Por ejemplo, cuando se crea una variable **xml** con tipo, se puede agregar la faceta DOCUMENT/CONTENT, como se muestra a continuación:  
  
```  
declare @x xml (DOCUMENT Production.ProductDescriptionSchemaCollection);  
```  
  
## <a name="document-type-definition-dtd"></a>Definición de tipo de documento (DTD)  
 Las columnas de tipo de datos **xml** , las variables y los parámetros pueden obtener tipos utilizando un esquema XML, pero no mediante DTD. Sin embargo, se puede usar DTD insertado para XML con o sin tipo, para suministrar valores predeterminados y reemplazar referencias a entidades por su forma expandida.  
  
 Puede convertir las DTD en documentos de esquemas XML mediante herramientas de otros fabricantes y cargar los esquemas XML en la base de datos.  
  
## <a name="upgrading-typed-xml-from-sql-server-2005"></a>Actualizar XML con tipos desde SQL Server 2005  
 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] ha realizado varias extensiones a la compatibilidad con esquemas XML, incluyendo la compatibilidad para la validación lax, el control mejorado de **xs:date**, **xs:time** y datos de instancia **xs:dateTime** , y compatibilidad agregada para tipos de lista y tipos de unión. En la mayoría de los casos, los cambios no afectan a la experiencia de actualización. Pero si usó una colección de esquemas XML en [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] que permitía valores del tipo **xs:date**, **xs:time**o **xs:dateTime** (o cualquier subtipo), los pasos de actualización siguientes se producen al adjuntar la base de datos de [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] o una versión posterior de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]:  
  
1.  Para cada columna XML, que se escribe con una Colección de esquemas XML que contiene elementos o atributos escritos como **xs:anyType**, **xs:anySimpleType**, **xs:date** o cualquiera de sus subtipos, **xs:time** o cualquier subtipo, o **xs:dateTime** o cualquiera de sus subtipos ,o son tipos de unión o de lista que contienen cualquiera de estos tipos, se produce lo siguiente:  
  
    1.  Se deshabilitarán todos los índices XML de la columna.  
  
    2.  Todos los valores de [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] continuarán representándose en la zona horaria Z porque se han normalizado a dicha zona horaria.  
  
    3.  Cualquier valor **xs:date** o **xs:dateTime** que sea menor que el 1 de enero del año 1 llevará a un error en tiempo de ejecución cuando el índice se regenere o se ejecute una XQuery, o instrucciones XML-DML, con el tipo de datos XML que contiene dicho valor.  
  
2.  Cualquier año negativo en las facetas o valores predeterminados **xs:date** o **xs:dateTime** de una colección de esquemas XML se actualizará automáticamente al valor más pequeño permitido por el tipo base **xs:date** o **xs:dateTime** (por ejemplo, 0001-01-01T00:00:00.0000000Z para **xs:dateTime**).  

 Observe que todavía puede usar una instrucción SELECT de SQL para recuperar todo el tipo de datos XML, aun cuando contiene años negativos. Se recomienda que reemplace los años negativos por un año dentro del intervalo recientemente admitido o cambie el tipo del elemento o atributo a **xs:string**.  
  
## <a name="see-also"></a>Consulte también  
 [Crear instancias de datos XML](../../relational-databases/xml/create-instances-of-xml-data.md)   
 [métodos del tipo de datos xml](../../t-sql/xml/xml-data-type-methods.md)   
 [Lenguaje de manipulación de datos XML &#40;XML DML&#41;](../../t-sql/xml/xml-data-modification-language-xml-dml.md)   
 [Datos XML &#40;SQL Server&#41;](../../relational-databases/xml/xml-data-sql-server.md)  
  
  
