---
title: 'Excluir elementos de esquema de documento XML con SQL: asignado'
ms.date: 03/17/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.technology: xml
ms.topic: reference
helpviewer_keywords:
- element does not map [SQLXML]
- annotated XSD schemas, excluding schema elements
- mapped annotation
- table mapping [SQLXML], excluding schema elements
- sql:mapped
- excluding schema elements
- element mapping [SQLXML], excluding schema elements
- column mapping [SQLXML]
- XSD schemas [SQLXML], excluding schema elements
- attribute mapping [SQLXML], excluding schema elements
- table/view mapping [SQLXML], excluding schema elements
ms.assetid: 7d2649dd-0038-4a2c-b16d-f80f7c306966
author: MightyPen
ms.author: genemi
ms.reviewer: ''
ms.custom: seo-lt-2019
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 6cf2f3302d4e609975ebb993e5388cbd6561c2bc
ms.sourcegitcommit: 792c7548e9a07b5cd166e0007d06f64241a161f8
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/19/2019
ms.locfileid: "75257442"
---
# <a name="excluding-schema-elements-from-the-xml-document-using-sqlmapped"></a>Excluir elementos de esquema del documento XML mediante sql:mapped
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  Cada elemento y atributo del esquema XSD se asigna a una tabla/vista y columna de base de datos debido a la asignación predeterminada. Si desea crear un elemento en el esquema XSD que no se asigne a ninguna tabla de base de datos (vista) o columna y que no aparezca en el XML, puede especificar la anotación **SQL:** asvisad.  
  
 La anotación **SQL: alpped** es especialmente útil si no se puede modificar el esquema o si el esquema se usa para validar XML de otros orígenes y, además, contiene datos que no están almacenados en la base de datos. La anotación **SQL: aspped** difiere de **SQL: is-Constant** en que los elementos y atributos no asignados no aparecen en el documento XML.  
  
 La anotación **SQL: alpped** toma un valor booleano (0 = false, 1 = true). Los valores permitidos son 0, 1, true y false.  
  
## <a name="examples"></a>Ejemplos  
 Para crear muestras funcionales mediante los ejemplos siguientes, debe cumplir determinados requisitos. Para obtener más información, vea [Requirements for Running SQLXML examples](../../relational-databases/sqlxml/requirements-for-running-sqlxml-examples.md).  
  
### <a name="a-specifying-the-sqlmapped-annotation"></a>a. Especificar la anotación sql:mapped  
 Suponga que tiene un esquema XSD de algún otro origen. Este esquema XSD está compuesto de un ** \<elemento person. contact>** con los atributos **ContactID**, **FirstName**, **LastName**y **HomeAddress** .  
  
 Al asignar este esquema XSD a la tabla person. contact de la base de datos AdventureWorks, se especifica **SQL: alpped** en el atributo **HomeAddress** porque la tabla Employees no almacena las direcciones particulares de los empleados. Por consiguiente, este atributo no se asigna a la base de datos y no se devuelve en el documento XML resultante cuando se especifica una consulta XPath en el esquema de asignación.  
  
 Para el resto del esquema se produce una asignación predeterminada. El ** \<elemento person. contact>** se asigna a la tabla person. contact y todos los atributos se asignan a las columnas con el mismo nombre en la tabla person. contact.  
  
```  
<xsd:schema xmlns:xsd="http://www.w3.org/2001/XMLSchema"  
            xmlns:sql="urn:schemas-microsoft-com:mapping-schema">  
  <xsd:element name="Person.Contact">  
    <xsd:complexType>  
      <xsd:attribute name="ContactID"   type="xsd:string"/>  
      <xsd:attribute name="FirstName"    type="xsd:string" />  
      <xsd:attribute name="LastName"     type="xsd:string" />  
      <xsd:attribute name="HomeAddress" type="xsd:string"   
                     sql:mapped="false" />  
    </xsd:complexType>  
  </xsd:element>  
</xsd:schema>  
```  
  
##### <a name="to-test-a-sample-xpath-query-against-the-schema"></a>Para probar una consulta XPath de ejemplo en el esquema  
  
1.  Copie el código de esquema anterior y péguelo en un archivo de texto. Guarde el archivo como sql-mapped.xml.  
  
2.  Copie la plantilla siguiente y péguela en un archivo de texto. Guarde el archivo como sql-mappedT.xml en el mismo directorio donde guardó sql-mapped.xml.  
  
    ```  
    <ROOT xmlns:sql="urn:schemas-microsoft-com:xml-sql">  
        <sql:xpath-query mapping-schema="sql-mapped.xml">  
            /Person.Contact[@ContactID < 10]  
        </sql:xpath-query>  
    </ROOT>  
    ```  
  
     La ruta de acceso al directorio especificada para el esquema de asignación (MySchema.xml) es relativa al directorio donde se guarda la plantilla. También puede especificarse una ruta de acceso absoluta como, por ejemplo:  
  
    ```  
    mapping-schema="C:\MyDir\sql-mapped.xml"  
    ```  
  
3.  Cree y use el script de prueba SQLXML 4.0 (Sqlxml4test.vbs) para ejecutar la plantilla.  

     Para obtener más información, vea [usar ado para ejecutar consultas SQLXML](../../relational-databases/sqlxml/using-ado-to-execute-sqlxml-4-0-queries.md).  
  
 Éste es el conjunto de resultados:  
  
```  
<ROOT xmlns:sql="urn:schemas-microsoft-com:xml-sql">  
  <Person.Contact ContactID="1" FirstName="Gustavo" LastName="Achong" />   
  <Person.Contact ContactID="2" FirstName="Catherine" LastName="Abel" />   
  <Person.Contact ContactID="3" FirstName="Kim" LastName="Abercrombie" />   
  <Person.Contact ContactID="4" FirstName="Humberto" LastName="Acevedo" />   
  <Person.Contact ContactID="5" FirstName="Pilar" LastName="Ackerman" />   
  <Person.Contact ContactID="6" FirstName="Frances" LastName="Adams" />   
  <Person.Contact ContactID="7" FirstName="Margaret" LastName="Smith" />   
  <Person.Contact ContactID="8" FirstName="Carla" LastName="Adams" />   
  <Person.Contact ContactID="9" FirstName="Jay" LastName="Adams" />   
</ROOT>  
```  
  
 Tenga en cuenta que los ContactID, FirstName y LastName están presentes, pero HomeAddress no es porque el esquema de asignación especificó 0 para el atributo **SQL: alpped** .  
  
## <a name="see-also"></a>Véase también  
 [Asignación predeterminada de elementos y atributos XSD a tablas y columnas &#40;SQLXML 4,0&#41;](../../relational-databases/sqlxml-annotated-xsd-schemas-using/default-mapping-of-xsd-elements-and-attributes-to-tables-and-columns-sqlxml-4-0.md)  
  
  
