---
title: Usar esquemas XSD anotados en consultas (SQLXML 4,0) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
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
author: rothja
ms.author: jroth
ms.openlocfilehash: caee73995b56e248a91872117a51e809c6eea976
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/18/2020
ms.locfileid: "85065683"
---
# <a name="using-annotated-xsd-schemas-in-queries-sqlxml-40"></a>Usar esquemas XSD anotados en consultas (SQLXML 4.0)
  Puede especificar consultas en un esquema anotado para recuperar datos de la base de datos especificando consultas XPath en una plantilla en el esquema XSD.  
  
 El **\<sql:xpath-query>** elemento permite especificar una consulta XPath en la vista XML definida por el esquema anotado. El esquema anotado en el que se va a ejecutar la consulta XPath se identifica mediante el `mapping-schema` atributo del **\<sql:xpath-query>** elemento.  
  
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
  
 Después, puede crear y usar el script de prueba SQLXML 4.0 (Sqlxml4test.vbs) para ejecutar la consulta como parte de un archivo de plantilla. Para obtener más información, consulte [esquemas XDR anotados &#40;en desuso en SQLXML 4,0&#41;](annotated-xdr-schemas-deprecated-in-sqlxml-4-0.md).  
  
## <a name="using-inline-mapping-schemas"></a>Usar esquemas de asignación insertados  
 Un esquema anotado puede incluirse directamente en una plantilla y, después, puede especificarse una consulta XPath en la plantilla en el esquema insertado. La plantilla también puede ser un diagrama de actualización.  
  
 Una plantilla puede incluir varios esquemas insertados. Para usar un esquema insertado que esté incluido en una plantilla, especifique el atributo **ID** con un valor único en el **\<xsd:schema>** elemento y, a continuación, utilice **#idvalue** para hacer referencia al esquema en línea. El atributo **ID** es idéntico en comportamiento al **SQL: ID** ({urn: schemas-microsoft-com: XML-SQL} ID) que se usa en los esquemas XDR.  
  
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
  
 La plantilla también especifica dos consultas XPath. Cada uno de los **\<xpath-query>** elementos identifica de forma única el esquema de asignación especificando el `mapping-schema` atributo.  
  
 Cuando se especifica un esquema insertado en la plantilla, la `sql:is-mapping-schema` anotación también debe especificarse en el **\<xsd:schema>** elemento. `sql:is-mapping-schema` toma un valor booleano (0=false, 1=true). Un esquema insertado con **SQL: is-mapping-schema = "1"** se trata como esquema anotado insertado y no se devuelve en el documento XML.  
  
 La anotación `sql:is-mapping-schema` pertenece al espacio de nombres de plantilla `urn:schemas-microsoft-com:xml-sql`.  
  
 Para probar este ejemplo, guarde la plantilla (InlineSchemaTemplate.xml) en un directorio local y, a continuación, cree y use el script de prueba SQLXML 4.0 (Sqlxml4test.vbs) para ejecutar la plantilla. Para obtener más información, vea [usar ado para ejecutar consultas SQLXML 4,0](../using-ado-to-execute-sqlxml-4-0-queries.md).  
  
 Además de especificar el `mapping-schema` atributo en el **\<sql:xpath-query>** elemento de una plantilla (cuando hay una consulta XPath) o en un **\<updg:sync>** elemento de un diagrama, puede hacer lo siguiente:  
  
-   Especifique el `mapping-schema` atributo en el **\<ROOT>** elemento (declaración global) de la plantilla. Este esquema de asignación se convierte en el esquema predeterminado que utilizarán todos los nodos XPath y de diagrama de actualización que no tengan ninguna anotación `mapping-schema` explícita.  
  
-   Especificar el atributo `mapping schema` mediante el objeto ADO `Command`.  
  
 El `mapping-schema` atributo que se especifica en el **\<xpath-query>** **\<updg:sync>** elemento o tiene la prioridad más alta; el `Command` objeto ADO tiene la prioridad más baja.  
  
 Tenga en cuenta que si especifica una consulta XPath en una plantilla y no especifica un esquema de asignación en el que se ejecuta la consulta XPath, la consulta XPath se trata como una consulta de tipo **dbobject** . Por ejemplo, fíjese en esta plantilla:  
  
```  
<sql:xpath-query   
     xmlns:sql="urn:schemas-microsoft-com:xmlsql">  
          Production.ProductPhoto[@ProductPhotoID='100']/@LargePhoto  
</sql:xpath-query>  
```  
  
 La plantilla especifica una consulta XPath, pero no especifica ningún esquema de asignación. Por lo tanto, esta consulta se trata como una consulta de tipo **dbobject** en la que production. ProductPhoto es el nombre de tabla y @ProductPhotoID = ' 100 ' es un predicado que busca una fotografía de producto con el valor de identificador de 100. @LargePhotoes la columna de la que se va a recuperar el valor.  
  
  
