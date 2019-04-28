---
title: Sección de esquema | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- Schema section [ADO]
ms.assetid: 4ac6e524-2c92-48e8-b871-0a4b5c8fda18
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 45e8e37d8bb85e727771072abda9249b8155076f
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "62802676"
---
# <a name="schema-section"></a>Sección de esquema
La sección de esquema es necesaria. Como se muestra en el ejemplo anterior, ADO escribe metadatos detallados sobre cada columna para conservar la semántica de los valores de datos tanto como sea posible para la actualización. Sin embargo, para cargar el XML, ADO requiere sólo los nombres de las columnas y el conjunto de filas al que pertenecen. Este es un ejemplo de un esquema mínimo:  
  
```  
<xml xmlns:s="uuid:BDC6E3F0-6DA3-11d1-A2A3-00AA00C14882"  
    xmlns:rs="urn:schemas-microsoft-com:rowset"  
    xmlns:z="#RowsetSchema">  
  <s:Schema id="RowsetSchema">  
    <s:ElementType name="row" content="eltOnly">  
      <s:AttributeType name="ShipperID"/>  
      <s:AttributeType name="CompanyName"/>  
      <s:AttributeType name="Phone"/>  
      <s:Extends type="rs:rowbase"/>  
    </s:ElementType>  
  </s:Schema>  
  <rs:data>  
...  
  </rs:data>  
</xml>  
```  
  
 En el ejemplo anterior, ADO tratará los datos como cadenas de longitud variable porque no hay información de tipo se incluye en el esquema.  
  
## <a name="creating-aliases-for-column-names"></a>Creación de alias para nombres de columna  
 El atributo rs: name permite crear un alias para un nombre de columna para que aparezca un nombre descriptivo en la información de la columna expuesta por el conjunto de filas y un nombre más corto puede usarse en la sección de datos. Por ejemplo, el esquema anterior podría modificarse para asignar ShipperID a s1, s2, CompanyName y Phone a s3 como sigue:  
  
```  
<s:Schema id="RowsetSchema">   
<s:ElementType name="row" content="eltOnly" rs:updatable="true">   
<s:AttributeType name="s1" rs:name="ShipperID" rs:number="1" ...>   
...  
</s:AttributeType>   
<s:AttributeType name="s2" rs:name="CompanyName" rs:number="2" ...>   
...  
</s:AttributeType>   
<s:AttributeType name="s3" rs:name="Phone" rs:number="3" ...>   
...  
</s:AttributeType>   
...  
</s:ElementType>   
</s:Schema>  
```  
  
 A continuación, en la sección de datos, la fila utilizaría el atributo name (no rs: name) para hacer referencia a esa columna:  
  
```  
"<row s1="1" s2="Speedy Express" s3="(503) 555-9831"/>  
```  
  
 Es necesario crear alias para nombres de columna, siempre que sea un nombre de columna no es un atributo válido o el nombre de etiqueta en XML. Por ejemplo, "LastName" debe tener un alias porque los nombres con espacios incrustados son atributos no válidos. La línea siguiente no se correctamente controlará el analizador XML, por lo que debe crear un alias para otro nombre que no tiene un espacio incrustado.  
  
```  
<row last name="Jones"/>  
```  
  
 Cualquier valor que se usa para el atributo name debe usarse de forma coherente en cada lugar que se hace referencia a la columna en el esquema y los datos de las secciones del documento XML. El ejemplo siguiente muestra el uso coherente de s1:  
  
```  
<s:Schema id="RowsetSchema">  
  <s:ElementType name="row" content="eltOnly">  
    <s:attribute type="s1"/>  
    <s:attribute type="CompanyName"/>  
    <s:attribute type="s3"/>  
    <s:extends type="rs:rowbase"/>  
  </s:ElementType>  
  <s:AttributeType name="s1" rs:name="ShipperID" rs:number="1"   
    rs:maydefer="true" rs:writeunknown="true">  
    <s:datatype dt:type="i4" dt:maxLength="4" rs:precision="10"   
      rs:fixedlength="true" rs:maybenull="true"/>  
  </s:AttributeType>  
</s:Schema>  
<rs:data>  
  <z:row s1="1" CompanyName="Speedy Express" s3="(503) 555-9831"/>  
</rs:data>  
```  
  
 De forma similar, porque no hay no definido ningún alias para `CompanyName` en el ejemplo anterior, `CompanyName` debe usarse de forma coherente en todo el documento.  
  
## <a name="data-types"></a>Tipos de datos  
 Puede aplicar un tipo de datos a una columna con el atributo dt: Type. Para obtener la guía definitiva para los tipos permitidos de XML, vea la sección tipos de datos de la [especificación W3C XML-Data](http://www.w3.org/TR/1998/NOTE-XML-data/). Puede especificar un tipo de datos de dos maneras: especificar el atributo dt: Type directamente en la propia definición de columna o utilizar la construcción s: DataType como un elemento anidado de la definición de columna. Por ejemplo,  
  
```  
<s:AttributeType name="Phone" >  
  <s:datatype dt:type="string"/>  
</s:AttributeType>  
```  
  
 es equivalente a  
  
```  
<s:AttributeType name="Phone" dt:type="string"/>  
```  
  
 Si se omite el atributo dt: Type completamente de la definición de fila, de forma predeterminada, el tipo de la columna será una cadena de longitud variable.  
  
 Si tiene más información de tipos que simplemente el nombre de tipo (por ejemplo, dt: MaxLength), resulta más legible para usar el elemento secundario de s: DataType. Esto es simplemente una convención, sin embargo y no es un requisito.  
  
 Los ejemplos siguientes muestran aún más cómo incluir información de tipo en el esquema.  
  
```  
<!-- 1. String with no max length -->  
<s:AttributeType name="title_id"/>  
<!-or -->  
<s:AttributeType name="title_id" dt:type="string"/>  
  
<!-- 2. Fixed length string with max length of 6 -->  
<s:AttributeType name="title_id">  
    <s:datatype dt:type="string" dt:maxLength="6" rs:fixedlength="true" />  
</s:AttributeType>  
  
<!-- 3. Variable length string with max length of 6 -->  
<s:AttributeType name="title_id">  
    <s:datatype dt:type="string" dt:maxLength="6" />  
</s:AttributeType>  
  
<!-- 4. Integer -->  
<s:AttributeType name="title_id" dt:type="int"/>  
```  
  
 Hay un uso sutil del atributo rs: fixedlength en el segundo ejemplo. Una columna con el atributo rs: fixedlength se establece en true significa que los datos deben tener la longitud definida en el esquema. En este caso, un valor válido para title_id es "123456", tal como está "123". Sin embargo, "123" no sería válido porque su longitud es 3, no 6. Ver Guía del programador de OLE DB para obtener la descripción de la propiedad fixedlength completa.  
  
## <a name="handling-nulls"></a>Controlar los valores null  
 Los valores NULL se controlan mediante el atributo rs: maybenull. Si este atributo se establece en true, el contenido de la columna puede contener un valor null. Además, si la columna no se encuentra en una fila de datos, el usuario que lee los datos desde el conjunto de filas obtendrá un estado null desde IRowset::GetData(). Tenga en cuenta las siguientes definiciones de columna de la tabla de distribuidores.  
  
```  
<s:AttributeType name="ShipperID">  
  <s:datatype dt:type="int" dt:maxLength="4"/>  
</s:AttributeType>  
<s:AttributeType name="CompanyName">  
  <s:datatype dt:type="string" dt:maxLength="40" rs:maybenull="true"/>  
</s:AttributeType>  
```  
  
 Permite la definición de `CompanyName` sea null, pero `ShipperID` no puede contener un valor null. Si la sección de datos contiene la fila siguiente, el proveedor de persistencia establecería el estado de los datos para el `CompanyName` columna a la constante de estado DBSTATUS_S_ISNULL de OLE DB:  
  
```  
<z:row ShipperID="1"/>  
```  
  
 Si la fila estaba totalmente vacía, como se indica a continuación, el proveedor de persistencia devolvería un estado de OLE DB de DBSTATUS_E_UNAVAILABLE para `ShipperID` y DBSTATUS_S_ISNULL para CompanyName.  
  
```  
<z:row/>   
```  
  
 Tenga en cuenta que una cadena de longitud cero no es igual a null.  
  
```  
<z:row ShipperID="1" CompanyName=""/>  
```  
  
 Para la fila anterior, el proveedor de persistencia devolverá un estado de OLE DB de DBSTATUS_S_OK para ambas columnas. El `CompanyName` en este caso es simplemente "" (una cadena de longitud cero).  
  
 Para obtener más información acerca de OLE DB construye disponibles para su uso dentro del esquema de un documento XML para OLE DB, consulte la definición de "urn: schemas-microsoft-Rowset" y la Guía de la base de datos del programador de OLE.  
  
## <a name="see-also"></a>Vea también  
 [Almacenar registros en formato XML](../../../ado/guide/data/persisting-records-in-xml-format.md)
