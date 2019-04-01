---
title: Colecciones de esquemas XML (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: xml
ms.topic: conceptual
helpviewer_keywords:
- XSD schemas [SQL Server]
- xml_schema_namespace function
- XML schema collections [SQL Server], about XML schema collections
- metadata [SQL Server], XML schema collections
- queries [XML in SQL Server], XML schema collections
- schema collections [SQL Server]
- schemas [SQL Server], XML
- XML [SQL Server], schema collections
- XML schema collections [SQL Server]
- schema collections [SQL Server], about XML schema collections
ms.assetid: 659d41aa-ccec-4554-804a-722a96ef25c2
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: dab6f53c5b75e1ef78eab346d2b0dd96a42e5861
ms.sourcegitcommit: 2827d19393c8060eafac18db3155a9bd230df423
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 03/27/2019
ms.locfileid: "58510152"
---
# <a name="xml-schema-collections-sql-server"></a>Colecciones de esquemas XML (SQL Server)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]
  Como se describe en el tema [xml &#40;Transact-SQL&#41;](../../t-sql/xml/xml-transact-sql.md), SQL Server ofrece almacenamiento nativo de datos XML a través del tipo de datos **xml**. Opcionalmente, puede asociar esquemas XSD a una variable o una columna de tipo **xml** a través de una colección de esquemas XML. Esta colección almacena los esquemas XML importados y luego se usa para lo siguiente:  
  
-   Validar instancias XML  
  
-   Asignar un tipo a los datos XML cuando se almacenan en la base de datos  
  
 Tenga en cuenta que la colección de esquemas XML es una entidad de metadatos como una tabla de la base de datos. Se pueden crear, modificar y arrastrar. Los esquemas especificados en una instrucción [CREATE XML SCHEMA COLLECTION (Transact-SQL)](../../t-sql/statements/create-xml-schema-collection-transact-sql.md) se importan automáticamente en el objeto de la colección de esquemas XML recién creado. Se pueden importar otros esquemas o componentes de esquemas en un objeto de la colección existente de la base de datos usando la instrucción [ALTER XML SCHEMA COLLECTION (Transact-SQL)](../../t-sql/statements/alter-xml-schema-collection-transact-sql.md).  
  
 Como se describe en el tema [Comparar XML con tipo y XML sin tipo](../../relational-databases/xml/compare-typed-xml-to-untyped-xml.md), el XML almacenado en una columna o variable al que está asociado un esquema se conoce como XML **con tipo**, porque el esquema indica la información del tipo de datos necesaria para los datos de la instancia. SQL Server usa esta información del tipo para optimizar el almacenamiento de datos.  
  
 El motor de procesamiento de consultas también usa el esquema para la comprobación de los tipos y para optimizar las consultas y la modificación de datos.  
  
 Además, SQL Server utiliza la colección de esquemas XML asociada, en el caso de **xml**con tipo, para validar la instancia XML. Si la instancia XML es compatible con el esquema, la base de datos permite que se almacene la instancia en el sistema con su información de tipos. De lo contrario, rechaza la instancia.  
  
 Se puede usar la función intrínseca XML_SCHEMA_NAMESPACE para recuperar la colección de esquemas que está almacenada en la base de datos. Para obtener más información, vea [Ver una colección de esquemas XML almacenada](../../relational-databases/xml/view-a-stored-xml-schema-collection.md).  
  
 También puede usar la colección de esquemas XML para escribir variables, parámetros y columnas XML.  
  
##  <a name="ddl"></a> DDL para administrar colecciones de esquemas  
 Se pueden crear colecciones de esquemas XML en la base de datos y asociarlas a variables y columnas de tipo **xml** . Para administrar las colecciones de esquemas de la base de datos, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] proporciona las siguientes instrucciones DDL:  
  
-   [CREATE XML SCHEMA COLLECTION &#40;Transact-SQL&#41;](../../t-sql/statements/create-xml-schema-collection-transact-sql.md) Importa los componentes del esquema en una base de datos.  
  
-   [ALTER XML SCHEMA COLLECTION &#40;Transact-SQL&#41;](../../t-sql/statements/alter-xml-schema-collection-transact-sql.md) Modifica los componentes de esquema en una colección de esquemas XML existente.  
  
-   [DROP XML SCHEMA COLLECTION &#40;Transact-SQL&#41;](../../t-sql/statements/drop-xml-schema-collection-transact-sql.md) Elimina toda la colección de esquemas XML y todos sus componentes.  
  
 Para utilizar una colección de esquemas XML y los esquemas que contiene, primero es necesario crear la colección y los esquemas mediante la instrucción CREATE XML SCHEMA COLLECTION. Una vez creada la colección de esquemas, se pueden crear variables y columnas de tipo **xml** y asociarles la colección. Tenga en cuenta que, después de crear una colección de esquemas, varios componentes de esquema se almacenan en los metadatos. Se puede utilizar también ALTER XML SCHEMA COLLECTION para agregar más componentes a los esquemas existentes o agregar esquemas nuevos a la colección.  
  
 Para quitar la colección de esquemas, utilice la instrucción DROP XML SCHEMA COLLECTION. Se quitarán todos los esquemas contenidos en la colección, así como el objeto de colección. Tenga en cuenta que, para quitar una colección de esquemas, deben cumplirse las condiciones descritas en [DROP XML SCHEMA COLLECTION &#40;Transact-SQL&#41;](../../t-sql/statements/drop-xml-schema-collection-transact-sql.md).  
  
##  <a name="components"></a> Descripción de los componentes de esquema  
 Cuando se utiliza la instrucción CREATE XML SCHEMA COLLECTION, se importan varios componentes de esquema a la base de datos. Los componentes de esquema son los elementos de esquema, los atributos y las definiciones de tipo. Cuando se utiliza la instrucción DROP XML SCHEMA COLLECTION, se quita toda la colección.  
  
 CREATE XML SCHEMA COLLECTION guarda los componentes de esquema en varias tablas del sistema.  
  
 Considere, por ejemplo, el siguiente esquema:  
  
```xml
<?xml version="1.0"?>  
<xsd:schema xmlns:xsd="http://www.w3.org/2001/XMLSchema"  
            targetNamespace="uri:Cust_Orders2"  
            xmlns="uri:Cust_Orders2" >  
  <xsd:attribute name="SomeAttribute" type="xsd:int" />  
  <xsd:complexType name="SomeType" />  
  <xsd:complexType name="OrderType" >  
    <xsd:sequence>  
      <xsd:element name="OrderDate" type="xsd:date" />  
      <xsd:element name="RequiredDate" type="xsd:date" />  
      <xsd:element name="ShippedDate" type="xsd:date" />  
    </xsd:sequence>  
    <xsd:attribute name="OrderID" type="xsd:ID" />  
    <xsd:attribute name="CustomerID"  />  
    <xsd:attribute name="EmployeeID"  />  
  </xsd:complexType>  
  <xsd:complexType name="CustomerType" >  
     <xsd:sequence>  
        <xsd:element name="Order" type="OrderType"  
                     maxOccurs="unbounded" />  
       </xsd:sequence>  
      <xsd:attribute name="CustomerID" type="xsd:string" />  
      <xsd:attribute name="OrderIDList" type="xsd:IDREFS" />  
  </xsd:complexType>  
  <xsd:element name="Customer" type="CustomerType" />  
</xsd:schema>  
```  
  
 El esquema anterior muestra los distintos tipos de componentes que se pueden almacenar en la base de datos. Incluyen `SomeAttribute`, `SomeType`, `OrderType`, `CustomerType`, `Customer`, `Order`, `CustomerID`, `OrderID`, `OrderDate`, `RequiredDate`y `ShippedDate`.  
  
### <a name="component-categories"></a>Categorías del componente  
 Los componentes de esquema que se almacenan en la base de datos se incluyen en estas categorías:  
  
-   ELEMENT  
  
-   ATTRIBUTE  
  
-   TYPE (para tipos simples o complejos)  
  
-   ATTRIBUTEGROUP  
  
-   MODELGROUP  
  
 Por ejemplo:  
  
-   **SomeAttribute** es un componente ATTRIBUTE.  
  
-   **SomeType**, **OrderType**y **CustomerType** son componentes TYPE.  
  
-   **Customer** es un componente ELEMENT.  
  
 Cuando se importa un esquema a la base de datos, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] no almacena el propio esquema. En su lugar, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] almacena sus distintos componentes individuales. En otras palabras, no se almacena la etiqueta \<Schema>, sino que solo se conservan los componentes definidos en ella. No se conservan todos los elementos del esquema. Si la etiqueta \<Schema> contiene atributos que especifican el comportamiento predeterminado de sus componentes, estos atributos se trasladan a esos componentes de esquema durante el proceso de importación, como se muestra en la siguiente tabla.  
  
|Nombre del atributo|Comportamiento|  
|--------------------|--------------|  
|**attributeFormDefault**|El atributo **form** se aplica a todas las declaraciones de atributo del esquema donde todavía no está presente y el valor se establece en el valor del atributo **attributeFormDefault** .|  
|**elementFormDefault**|El atributo **form** se aplica a todas las declaraciones de elemento del esquema donde todavía no está presente y el valor se establece en el valor del atributo **elementFormDefault** .|  
|**blockDefault**|El atributo **block** se aplica a todas las declaraciones de elemento y definiciones de tipo donde todavía no está presente y el valor se establece en el valor del atributo **blockDefault** .|  
|**finalDefault**|El atributo **final** se aplica a todas las declaraciones de elemento y definiciones de tipo donde todavía no está presente y el valor se establece en el valor del atributo **finalDefault** .|  
|**targetNamespace**|La información acerca de los componentes que pertenecen al espacio de nombres de destino se almacena en los metadatos.|  
| &nbsp; | &nbsp; |
  
##  <a name="perms"></a> Permisos en una colección de esquemas XML  
 Deberá tener los permisos necesarios para realizar las operaciones siguientes:  
  
-   Crear o cargar la colección de esquemas XML  
  
-   Modificar la colección de esquemas XML  
  
-   Quitar la colección de esquemas XML  
  
-   Utilizar la colección de esquemas XML para escribir columnas, variables y parámetros de tipo **xml** , o utilizarla en restricciones de tabla o columna  
  
 El modelo de seguridad de SQL Server concede el permiso CONTROL para todos los objetos. El receptor de este permiso obtiene todos los demás permisos para el objeto. El propietario del objeto también dispone de todos los permisos para el objeto.  
  
 El propietario y el receptor del permiso CONTROL para un objeto puede conceder cualquier permiso para ese objeto. Un usuario que no sea el propietario del objeto ni disponga del permiso CONTROL todavía puede conceder permisos para un objeto si se especifica WITH GRANT OPTION. Supongamos, por ejemplo, que el usuario A tiene permiso REFERENCES en la colección de esquemas XML S, por medio de WITH GRANT OPTION, pero no posee ningún otro permiso en S. El usuario A podría conceder el permiso REFERENCES para la colección de esquemas S al usuario B.  
  
 El modelo de seguridad también otorga permisos para crear y utilizar colecciones de esquemas XML o transferir la propiedad de un usuario a otro. En los temas siguientes se describen los permisos de las colecciones de esquemas XML.  
  
-   [Conceder permisos para una colección de esquemas XML](../../relational-databases/xml/grant-permissions-on-an-xml-schema-collection.md)  
  
     Este tema explica cómo conceder permisos para crear una colección de esquemas XML y cómo conceder permisos para un objeto de colección de esquemas XML.  
  
-   [Revocar los permisos en una colección de esquemas XML](../../relational-databases/xml/revoke-permissions-on-an-xml-schema-collection.md)  
  
     Este tema explica cómo se pueden revocar permisos para impedir la creación de una colección de esquemas XML y cómo revocar los permisos en un objeto de colección de esquemas XML.  
  
-   [Denegar permisos en una colección de esquemas XML](../../relational-databases/xml/deny-permissions-on-an-xml-schema-collection.md)  
  
     Este tema explica cómo negar permisos para crear una colección de esquemas XML y cómo negar los permisos en un objeto de colección de esquemas XML.  
  
##  <a name="info"></a> Obtener información acerca de los esquemas XML y las colecciones de esquemas  
 Las colecciones de esquemas XML se enumeran en la vista de catálogo sys.xml_schema_collections. La colección de esquemas XML "sys" la define el sistema. Contiene los espacios de nombres predefinidos que se pueden usar en todas las colecciones de esquemas XML definidas por el usuario, sin tener que cargarlos explícitamente. Esta lista contiene los espacios de nombres para xml, xs, xsi, fn y xdt. Otras dos vistas de catálogo son sys.xml_schema_namespaces, que enumera todos los espacios de nombres incluidos en una colección de esquemas XML, y sys.xml_components, que enumera todos los componentes de esquemas XML dentro de cada esquema XML.  
  
 La función integrada **XML_SCHEMA_NAMESPACE**, *schemaName, XmlSchemacollectionName, namespace-uri*, genera una instancia de tipo de datos **xml**. Esta instancia contiene fragmentos de esquemas XML correspondientes a esquemas incluidos en una colección de esquemas XML, excepto los esquemas XML predefinidos.  
  
 Puede enumerar el contenido de una colección de esquemas XML de las siguientes maneras:  
  
-   Escriba consultas Transact-SQL sobre las vistas de catálogo apropiadas para colecciones de esquemas XML.  
  
-   Use la función integrada **XML_SCHEMA_NAMESPACE()**. Puede aplicar métodos de tipo de datos **xml** al resultado de esta función. Sin embargo, no puede modificar los esquemas XML subyacentes.  
  
 Los ejemplos siguientes ilustran lo comentado.  
  
### <a name="example-enumerate-the-xml-namespaces-in-an-xml-schema-collection"></a>Ejemplo: Enumerar los espacios de nombres XML en una colección de esquemas XML  
 Use la siguiente consulta para la colección de esquemas XML "myCollection".  
  
```sql
SELECT XSN.name  
FROM    sys.xml_schema_collections XSC JOIN sys.xml_schema_namespaces XSN  
    ON (XSC.xml_collection_id = XSN.xml_collection_id)  
WHERE    XSC.name = 'myCollection'     
```  
  
### <a name="example-enumerate-the-contents-of-an-xml-schema-collection"></a>Ejemplo: Enumerar el contenido de una colección de esquemas XML  
 La instrucción siguiente enumera el contenido de la colección de esquemas XML "myCollection" dentro del esquema relacional dbo.  
  
```sql
SELECT XML_SCHEMA_NAMESPACE (N'dbo', N'myCollection')  
```  
  
 Es posible obtener esquemas XML individuales incluidos en la colección como instancias de tipo de datos **xml** ; para ello, especifique el espacio de nombres de destino como tercer argumento de **XML_SCHEMA_NAMESPACE()**. Esto se muestra en el ejemplo siguiente.  
  
### <a name="example-output-a-specified-schema-from-an-xml-schema-collection"></a>Ejemplo: Obtener un esquema especificado a partir de una colección de esquemas XML  
 La instrucción siguiente genera como resultado el esquema XML con el espacio de nombres de destino _pretend_ http:/\/www.microsoft.com/books" a partir de la colección de esquemas XML "myCollection" dentro del esquema relacional dbo.  
  
```sql
SELECT XML_SCHEMA_NAMESPACE (N'dbo', N'myCollection',   
N'https://www.microsoft.com/was-books')  
```  
  
### <a name="querying-xml-schemas"></a>Consultar esquemas XML  
 Los siguientes procedimientos permiten consultar esquemas XML que se hayan cargado en colecciones de esquemas XML:  
  
-   Escriba consultas Transact-SQL sobre vistas de catálogo para espacios de nombres de esquemas XML.  
  
-   Cree una tabla que contenga una columna de tipo de datos **xml** para almacenar los esquemas XML y también cargarlos en el sistema de tipo XML. Puede consultar la columna XML mediante los métodos de tipo de datos **xml** . Además, puede crear un índice XML en esta columna. Sin embargo, con este enfoque, la aplicación debe mantener la coherencia entre los esquemas XML almacenados en la columna XML y el sistema de tipo XML. Por ejemplo, si se quita el espacio de nombres de esquemas XML del sistema de tipo XML, también se tiene que quitar de la tabla para preservar la coherencia.  
  
## <a name="see-also"></a>Consulte también  
 [Ver una colección de esquemas XML almacenada](../../relational-databases/xml/view-a-stored-xml-schema-collection.md)   
 [Preprocesar un esquema para combinar esquemas incluidos](../../relational-databases/xml/preprocess-a-schema-to-merge-included-schemas.md)   
 [Requisitos y limitaciones de las colecciones de esquemas XML en el servidor](../../relational-databases/xml/requirements-and-limitations-for-xml-schema-collections-on-the-server.md)  
  
  
