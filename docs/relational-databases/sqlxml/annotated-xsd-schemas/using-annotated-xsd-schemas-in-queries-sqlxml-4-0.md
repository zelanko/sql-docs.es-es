---
title: Mediante los esquemas XSD en consultas (SQLXML 4.0) anotados | Microsoft Docs
ms.custom: ''
ms.date: 01/11/2019
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: xml
ms.topic: reference
helpviewer_keywords:
- queries [SQLXML]
- inline schemas [SQLXML]
- XPath queries [SQLXML], annotated XSD schemas in queries
- queries [SQLXML], annotated XSD schemas
- retrieving data
- mapping schema [SQLXML], queries
- multiple inline schemas
- annotated XSD schemas, queries
- XSD schemas [SQLXML], queries
- templates [SQLXML], annotated XSD schemas in queries
ms.assetid: 927a30a2-eae8-420d-851d-551c5f884f3c
author: MightyPen
ms.author: genemi
manager: craigg
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 9af0e0c5a843ecf475b28dd873ecfedc5d2f6472
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "62677945"
---
# <a name="using-annotated-xsd-schemas-in-queries-sqlxml-40"></a>Usar esquemas XSD anotados en consultas (SQLXML 4.0)
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  Puede especificar consultas en un esquema anotado para recuperar datos de la base de datos especificando consultas XPath en una plantilla en el esquema XSD.  
  
 El  **\<sql:xpath-consulta >** elemento le permite especificar una consulta XPath en la vista XML definida por el esquema anotado. El esquema anotado en la que se se ejecuta la consulta XPath se identifica mediante el **esquema de asignación** atributo de la  **\<sql:xpath-consulta >** elemento.  
  
 Las plantillas son documentos XML válidos que contienen una o varias consultas. Las consultas FOR XML y XPath devuelven un fragmento de documento. Las plantillas actúan como contenedores para los fragmentos de documento; de esta forma, las plantillas proporcionan un modo de especificar un elemento único de nivel superior.  
  
 En los ejemplos de este tema se usan plantillas para especificar una consulta XPath en un esquema anotado con objeto de recuperar datos de la base de datos.  
  
 Por ejemplo, fíjese este esquema anotado:  
  
```  
<xsd:schema xmlns:xsd="http://www.w3.org/2001/XMLSchema"   
            xmlns:sql="urn:schemas-microsoft-com:mapping-schema">  
  <xsd:element name="Person.Contact" >  
     <xsd:complexType>  
       <xsd:attribute name="ContactID" type="xsd:string" />   
       <xsd:attribute name="FirstName" type="xsd:string" />   
       <xsd:attribute name="LastName"  type="xsd:string" />   
     </xsd:complexType>  
  </xsd:element>  
</xsd:schema>  
```  
  
 Con fines meramente ilustrativos, este esquema XSD se almacena en un archivo denominado Schema2.xml. A continuación, podría incluir una consulta XPath en el esquema anotado especificado en el siguiente archivo de plantilla (Schema2T.xml):  
  
```  
<sql:xpath-query   
     xmlns:sql="urn:schemas-microsoft-com:xmlsql"  
     >  
          Person.Contact[@ContactID="1"]  
</sql:xpath-query>  
```  
  
 Después, puede crear y usar el script de prueba SQLXML 4.0 (Sqlxml4test.vbs) para ejecutar la consulta como parte de un archivo de plantilla. Para obtener más información, consulte [esquemas XDR anotados &#40;desusado en SQLXML 4.0&#41;](../../../relational-databases/sqlxml/annotated-xsd-schemas/annotated-xdr-schemas-deprecated-in-sqlxml-4-0.md).  
  
## <a name="using-inline-mapping-schemas"></a>Usar esquemas de asignación insertados  
 Un esquema anotado puede incluirse directamente en una plantilla y, después, puede especificarse una consulta XPath en la plantilla en el esquema insertado. La plantilla también puede ser un diagrama de actualización.  
  
 Una plantilla puede incluir varios esquemas insertados. Para usar un esquema en línea que se incluye en una plantilla, especifique la **id** atributo con un valor único en la  **\<xsd: schema >** elemento y, a continuación, utilice **#idvalue**para hacer referencia al esquema en línea. El **id** atributo es un comportamiento idéntico a la **SQL: ID** ({urn: schemas-microsoft-com-sql} id) utilizados en los esquemas XDR.  
  
 Por ejemplo, la plantilla siguiente especifica dos esquemas anotados insertados:  
  
```  
<ROOT xmlns:sql='urn:schemas-microsoft-com:xml-sql'>  
<xsd:schema xmlns:xsd='http://www.w3.org/2001/XMLSchema'  
        xmlns:ms='urn:schemas-microsoft-com:mapping-schema'  
        id='InLineSchema1' sql:is-mapping-schema='1'>  
  <xsd:element name='Employees' ms:relation='HumanResources.Employee'>  
    <xsd:complexType>  
      <xsd:attribute name='LoginID'   
                     type='xsd:string'/>  
      <xsd:attribute name='Title'   
                     type='xsd:string'/>  
    </xsd:complexType>  
  </xsd:element>  
</xsd:schema>  
  
<xsd:schema xmlns:xsd='http://www.w3.org/2001/XMLSchema'  
        xmlns:ms='urn:schemas-microsoft-com:mapping-schema'  
        id='InLineSchema2' sql:is-mapping-schema='1'>  
  <xsd:element name='Contacts' ms:relation='Person.Contact'>  
    <xsd:complexType>  
  
      <xsd:attribute name='ContactID'   
                     type='xsd:string' />  
      <xsd:attribute name='FirstName'   
                     type='xsd:string' />  
      <xsd:attribute name='LastName'   
                     type='xsd:string' />  
    </xsd:complexType>  
  </xsd:element>  
</xsd:schema>  
  
<sql:xpath-query xmlns:sql='urn:schemas-microsoft-com:xml-sql'   
        mapping-schema='#InLineSchema1'>  
    /Employees[@LoginID='adventure-works\guy1']  
</sql:xpath-query>  
  
<sql:xpath-query xmlns:sql='urn:schemas-microsoft-com:xml-sql'   
        mapping-schema='#InLineSchema2'>  
    /Contacts[@ContactID='1']  
</sql:xpath-query>  
</ROOT>  
```  
  
 La plantilla también especifica dos consultas XPath. Cada uno de los  **\<consulta de xpath >** elementos identifica el esquema de asignación especificando el **esquema de asignación** atributo.  
  
 Cuando se especifica un esquema insertado en la plantilla, el **sql: is-mapping-schema** anotación debe especificarse en el  **\<xsd: schema >** elemento. El **sql: is-mapping-schema** toma un valor booleano (0 = false, 1 = true). Un esquema insertado con **sql: is-mapping-schema = "1"** se trata como un esquema anotado insertado y no se devuelve en el documento XML.  
  
 El **sql: is-mapping-schema** anotación pertenece al espacio de nombres de plantilla **urn: schemas-microsoft-com: sql**.  
  
 Para probar este ejemplo, guarde la plantilla (InlineSchemaTemplate.xml) en un directorio local y, a continuación, cree y use el script de prueba SQLXML 4.0 (Sqlxml4test.vbs) para ejecutar la plantilla. Para obtener más información, consulte [utilizar ADO para ejecutar consultas de SQLXML 4.0](../../../relational-databases/sqlxml/using-ado-to-execute-sqlxml-4-0-queries.md).  
  
 Además de especificar el **esquema de asignación** atributo el  **\<sql:xpath-consulta >** elemento en una plantilla (cuando hay una consulta XPath) o en  **\< updg:Sync >** elemento en un diagrama de actualización, puede hacer lo siguiente:  
  
-   Especifique el **esquema de asignación** atributo el  **\<raíz >** elemento (declaración global) en la plantilla. Este esquema de asignación, a continuación, se convierte en el esquema predeterminado que se usará en todos los nodos de XPath y diagrama de actualización que tienen no explícita **esquema de asignación** anotación.  
  
-   Especifique el **esquema de asignación** atributo utilizando ADO **comando** objeto.  
  
 El **esquema de asignación** atributo que se especifica en el  **\<consulta de xpath >** o  **\<updg:sync >** elemento tiene la más alta prioridad; ADO **comando** objeto tiene la prioridad más baja.  
  
 Tenga en cuenta que si especifica una consulta XPath en una plantilla y no especifica un esquema de asignación en la que se ejecutó la consulta XPath, la consulta XPath se trata como un **dbobject** consulta de tipo. Por ejemplo, fíjese en esta plantilla:  
  
```  
<sql:xpath-query   
     xmlns:sql="urn:schemas-microsoft-com:xmlsql">  
          Production.ProductPhoto[@ProductPhotoID='100']/@LargePhoto  
</sql:xpath-query>  
```  
  
 La plantilla especifica una consulta XPath, pero no especifica ningún esquema de asignación. Por lo tanto, esta consulta se considera un **dbobject** donde Production.ProductPhoto es el nombre de tabla de consulta de tipo y @ProductPhotoID= '100' es un predicado que busca una fotografía del producto con el valor de identificador de 100. @LargePhoto es la columna desde la que se va a recuperar el valor.  
  
  
