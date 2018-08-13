---
title: Recuperar datos no consumidos mediante overflow-field (SQLXML 4.0) | Documentos de Microsoft
ms.custom: ''
ms.date: 03/17/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.component: sqlxml
ms.reviewer: ''
ms.suite: sql
ms.technology: xml
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- unconsumed data
- storing unconsumed data
- retrieving unconsumed data
- annotated XSD schemas, unconsumed data
- overflow data [SQLXML]
- sql:overflow-field
ms.assetid: 8526998d-b47d-4a32-8dc2-7f50a8d11097
caps.latest.revision: 30
author: douglaslMS
ms.author: douglasl
manager: craigg
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017
ms.openlocfilehash: 51f9fe6c3e8053b1a03174d5e9ba3fce738c5231
ms.sourcegitcommit: 4cd008a77f456b35204989bbdd31db352716bbe6
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/06/2018
ms.locfileid: "39559215"
---
# <a name="retrieving-unconsumed-data-using-the-sqloverflow-field-sqlxml-40"></a>Recuperar datos no utilizados mediante sql:overflow-field (SQLXML 4.0)
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  Cuando se insertan registros en una base de datos de un documento XML utilizando la función [!INCLUDE[tsql](../../includes/tsql-md.md)] OPENXML, se pueden almacenar todos los datos no consumidos del documento XML en una columna. Al recuperar datos de una base de datos mediante esquemas anotados, puede especificar el **Overflow-campo** atributo para identificar la columna en la tabla en la que se almacenan los datos de desbordamiento. El **Overflow-campo** atributo puede especificarse en  **\<elemento >**.  
  
 Este dato se recupera después de las siguientes maneras:  
  
-   Atributos que se almacenan en la columna de desbordamiento se agregan al elemento que contiene el **Overflow-campo** anotación.  
  
-   Los elementos secundarios y sus descendientes, almacenados en la columna de desbordamiento de la base de datos, se agregan como elementos secundarios que siguen al contenido que se especifica explícitamente en el esquema. (No se mantiene ningún orden.)  
  
## <a name="examples"></a>Ejemplos  
 Para crear muestras funcionales mediante los ejemplos siguientes, debe cumplir determinados requisitos. Para obtener más información, consulte [requisitos para ejecutar los ejemplos de SQLXML](../../relational-databases/sqlxml/requirements-for-running-sqlxml-examples.md).  
  
### <a name="a-specifying-sqloverflow-field-for-an-element"></a>A. Especificar SQL:OVERFLOW-FIELD para un elemento  
 En este ejemplo se entiende que se ha ejecutado el siguiente script para que exista una tabla denominada Customers2 en la base de datos tempdb:  
  
```  
USE tempdb  
CREATE TABLE Customers2 (  
CustomerID       VARCHAR(10),   
ContactName    VARCHAR(30),   
AddressOverflow    NVARCHAR(500))  
  
GO  
INSERT INTO Customers2 VALUES (  
'ALFKI',   
'Joe',  
'<Address>  
  <Address1>Maple St.</Address1>  
  <Address2>Apt. E105</Address2>  
  <City>Seattle</City>  
  <State>WA</State>  
  <Zip>98147</Zip>  
 </Address>')  
GO  
```  
  
 Además, debe crear un directorio virtual para la base de datos tempdb y un nombre virtual de la plantilla de **plantilla** tipo denominado "template".  
  
 En el ejemplo siguiente, el esquema de asignación recupera los datos no consumidos que están almacenados en la columna AddressOverflow de la tabla Customers2:  
  
```  
<xsd:schema xmlns:xsd="http://www.w3.org/2001/XMLSchema"  
            xmlns:sql="urn:schemas-microsoft-com:mapping-schema">  
  
  <xsd:element name="Customers2" sql:overflow-field="AddressOverflow" >  
    <xsd:complexType>  
      <xsd:attribute name="CustomerID"  type="xsd:integer"/>  
      <xsd:attribute name="ContactName"  type="xsd:string" />  
    </xsd:complexType>  
  </xsd:element>  
</xsd:schema>  
```  
  
##### <a name="to-test-a-sample-xpath-query-against-the-schema"></a>Para probar una consulta de XPath de ejemplo con respecto al esquema  
  
1.  Copie el código de esquema anterior y péguelo en un archivo de texto. Guarde el archivo como Overflow.xml.  
  
2.  Copie la plantilla siguiente y péguela en un archivo de texto. Guarde el archivo como OverflowT.xml en el mismo directorio donde guardó Overflow.xml. La consulta de la plantilla selecciona los registros de la tabla Customers2.  
  
    ```  
    <ROOT xmlns:sql="urn:schemas-microsoft-com:xml-sql">  
        <sql:xpath-query mapping-schema="Overflow.xml">  
            /Customers2  
        </sql:xpath-query>  
    </ROOT>  
    ```  
  
     La ruta de acceso al directorio especificada para el esquema de asignación (Overflow.xml) es relativa al directorio donde se guarda la plantilla. También puede especificarse una ruta de acceso absoluta como, por ejemplo:  
  
    ```  
    mapping-schema="C:\SqlXmlTest\Overflow.xml"  
    ```  
  
3.  Cree y use el script de prueba SQLXML 4.0 (Sqlxml4test.vbs) para ejecutar la plantilla.  
  
     Para obtener más información, consulte [utilizar ADO para ejecutar consultas de SQLXML 4.0](../../relational-databases/sqlxml/using-ado-to-execute-sqlxml-4-0-queries.md).  
  
 El conjunto de resultados es:  
  
```  
<ROOT xmlns:sql="urn:schemas-microsoft-com:xml-sql">  
  <Customers2 CustomerID="ALFKI" ContactName="Joe">  
    <Address1>Maple St.</Address1>   
    <Address2>Apt. E105</Address2>   
    <City>Seattle</City>   
    <State>WA</State>   
    <Zip>98147</Zip>   
  </Customers2>  
</ROOT>  
```  
  
  
