---
title: "Asignación de referencias a la colección de esquemas XML integrada (sys) | Microsoft Docs"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: xml
ms.reviewer: 
ms.suite: sql
ms.technology: dbe-xml
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- sys XML schema collections [SQL Server]
- schema collections [SQL Server], predefined
- predefined XML schema collections [SQL Server]
- XML schema collections [SQL Server], predefined
- built-in XML schema collections [SQL Server]
ms.assetid: 1e118303-5df0-4ee4-bd8d-14ced7544144
caps.latest.revision: "18"
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 2bcdb9f2df0955ff0bb30f9b55d0080b9446391e
ms.sourcegitcommit: 6c54e67818ec7b0a2e3c1f6e8aca0fdf65e6625f
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 01/19/2018
---
# <a name="reference-the-built-in-xml-schema-collection-sys"></a>Hacer referencia a la colección de esquemas XML integrada (sys)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)] Cada base de datos que se crea posee una colección de esquemas XML **sys** predefinida en el esquema relacional **sys**. Estos esquemas predefinidos se reservan, y son accesibles desde cualquier otra colección de esquemas XML creada por el usuario. Los prefijos utilizados en estos esquemas predefinidos son significativos en XQuery. El único prefijo reservado es **xml** .  
  
```  
xml = http://www.w3.org/XML/1998/namespace  
xs = http://www.w3.org/2001/XMLSchema  
xsi = http://www.w3.org/2001/XMLSchema-instance  
fn = http://www.w3.org/2004/07/xpath-functions  
sqltypes = http://schemas.microsoft.com/sqlserver/2004/sqltypes  
xdt = http://www.w3.org/2004/07/xpath-datatypes  
(no prefix) = urn:schemas-microsoft-com:xml-sql  
(no prefix) = http://schemas.microsoft.com/sqlserver/2004/SOAP  
```  
  
 Debe tenerse en cuenta que el espacio de nombres **sqltypes** contiene componentes a los que se puede hacer referencia desde cualquier colección de esquemas XML creada por el usuario. Puede descargar el esquema **sqltypes** de el [sitio web de Microsoft](http://go.microsoft.com/fwlink/?linkid=31850). Los componentes integrados son los siguientes:  
  
-   Tipos XSD  
  
-   Atributos XML **lang**, **base**y **space**  
  
-   Componentes del espacio de nombres **sqltypes**   
  
 La consulta siguiente devuelve los componentes integrados a los que se puede hacer referencia desde una colección de esquemas XML creada por el usuario:  
  
```  
SELECT C.name, N.name, C.symbol_space_desc from sys.xml_schema_components C join sys.xml_schema_namespaces N  
on ((C.xml_namespace_id = N.xml_namespace_id) AND (C.xml_collection_id = N.xml_collection_id))  
join sys.xml_schema_collections SC  
on SC.xml_collection_id = C.xml_collection_id  
where ((C.xml_collection_id = 1) AND (C.name is not null) AND (C.scoping_xml_component_id is null)   
AND (SC.schema_id = 4))  
GO  
```  
  
 En el ejemplo siguiente se muestra cómo se hace referencia a estos componentes en un esquema de usuario. `CREATE XML SCHEMA COLLECTION` crea una colección de esquemas XML que hace referencia al tipo `varchar` definido en el espacio de nombres `sqltypes` . En el ejemplo también se hace referencia al atributo `lang` que está definido en el espacio de nombres `xml` .  
  
```  
CREATE XML SCHEMA COLLECTION SC AS '  
<schema   
   xmlns="http://www.w3.org/2001/XMLSchema"   
   targetNamespace="myNS"  
   xmlns:ns="myNS"  
   xmlns:s="http://schemas.microsoft.com/sqlserver/2004/sqltypes" >   
   <import namespace="http://www.w3.org/XML/1998/namespace"/>  
   <import namespace="http://schemas.microsoft.com/sqlserver/2004/sqltypes"/>  
   <element name="root">  
      <complexType>  
          <sequence>  
             <element name="a" type="string"/>  
             <element name="b" type="string"/>  
             <!-- varchar type is defined in the sys.sys collection and   
                  can be referenced in any user-defined schema -->  
             <element name="c" type="s:varchar"/>  
          </sequence>  
          <attribute name="att" type="int"/>  
          <!-- xml:lang attribute is defined in the sys.sys collection   
               and can be referenced in any user-defined schema -->  
          <attribute ref="xml:lang"/>  
      </complexType>  
    </element>  
 </schema>'  
GO  
 -- Cleanup  
DROP xml schema collection SC   
GO  
```  
  
 Se debe tener en cuenta lo siguiente:  
  
-   No se pueden modificar esquemas XML con estos espacios de nombres en ninguna colección de esquemas XML definida por el usuario. Por ejemplo, la siguiente colección de esquemas XML genera un error porque agrega un componente al espacio de nombres protegido `sqltypes` :  
  
    ```  
    CREATE XML SCHEMA COLLECTION SC AS '  
    <schema xmlns="http://www.w3.org/2001/XMLSchema"   
    targetNamespace    
        ="http://schemas.microsoft.com/sqlserver/2004/sqltypes" >   
          <element name="root" type="string"/>  
    </schema>'  
    GO  
    ```  
  
-   No se puede utilizar la colección de esquemas XML `sys` para escribir columnas, variables o parámetros `xml` . Por ejemplo, el siguiente código genera un error:  
  
    ```  
    DECLARE @x xml (sys.sys)  
    ```  
  
-   No se admite la serialización de estos esquemas integrados. Por ejemplo, el siguiente código genera un error:  
  
    ```  
    SELECT XML_SCHEMA_NAMESPACE(N'sys',N'sys')  
    GO  
    ```  
  
 A continuación se ofrece otro ejemplo de código en el que se crea una colección de esquemas XML que utiliza el tipo `varchar` definido en el espacio de nombres `sqltypes`:  
  
```  
CREATE XML SCHEMA COLLECTION SC AS '  
<schema xmlns="http://www.w3.org/2001/XMLSchema"   
        targetNamespace="myNS" xmlns:ns="myNS"  
        xmlns:s="http://schemas.microsoft.com/sqlserver/2004/sqltypes">  
   <import     
     namespace="http://schemas.microsoft.com/sqlserver/2004/sqltypes"/>  
      <simpleType name="myType">  
            <restriction base="s:varchar">  
                  <maxLength value="20"/>  
            </restriction>  
      </simpleType>  
      <element name="root" type="ns:myType"/>  
</schema>'  
go  
```  
  
 Como se observa a continuación, se puede crear una variable `XML` con tipo, asignarle una instancia XML y comprobar que el valor del tipo de elemento <`root`> sea `varchar`.  
  
```  
DECLARE @var XML(SC)  
SET @var = '<root xmlns="myNS">My data</root>'  
SELECT @var.query('declare namespace sqltypes = "http://schemas.microsoft.com/sqlserver/2004/sqltypes";  
declare namespace ns="myNS";   
data(/ns:root[1]) instance of sqltypes:varchar?')  
GO  
```  
  
 La expresión `instance of sqltypes:varchar?` devuelve TRUE, porque el valor del elemento <`root`> es de un tipo derivado de **varchar** según el esquema asociado a la variable `@var`.  
  
## <a name="see-also"></a>Ver también  
 [Colecciones de esquemas XML &#40;SQL Server&#41;](../../relational-databases/xml/xml-schema-collections-sql-server.md)  
  
  
