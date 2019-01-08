---
title: Instrucciones y limitaciones de XML de realizar la carga masiva (SQLXML 4.0) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: xml
ms.topic: reference
helpviewer_keywords:
- XML Bulk Load [SQLXML], about XML Bulk Load
- bulk load [SQLXML], about bulk load
ms.assetid: c5885d14-c7c1-47b3-a389-455e99a7ece1
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: b7a569bbc5672b0fc5996507e37ed250721bd2fe
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/03/2018
ms.locfileid: "52774927"
---
# <a name="guidelines-and-limitations-of-xml-bulk-load-sqlxml-40"></a>Instrucciones y limitaciones de la carga masiva XML (SQLXML 4.0)
  Antes de usar la carga masiva XML, debe familiarizarse con las siguientes limitaciones e instrucciones:  
  
-   No se admiten los esquemas insertados.  
  
     Si tiene un esquema insertado en el documento XML de origen, la carga masiva XML omite dicho esquema. Debe especificar el esquema de asignación para la carga masiva XML de forma externa con respecto a los datos XML. No se puede especificar el esquema de asignación en un nodo mediante el uso de la **xmlns = "x: schema"** atributo.  
  
-   Se comprueba que el formato de un documento XML sea correcto, pero no se valida el documento.  
  
     Carga masiva XML comprueba el documento XML para determinar si se trata bien-formed-que es, para asegurarse de que el XML cumple los requisitos de sintaxis de la recomendación de XML 1.0 del World Wide Web Consortium. Si el documento no tiene el formato correcto, la carga masiva XML cancela el procesamiento y devuelve un error. La única excepción a esta regla es que el documento sea un fragmento (por ejemplo, el documento no tiene ningún elemento raíz único), en cuyo caso la carga masiva XML cargará el documento.  
  
     La carga masiva XML no valida el documento con respecto a cualquier esquema de datos XML o esquema DTD que se defina o al que se haga referencia dentro del archivo de datos XML. Además, la carga masiva XML no valida el archivo de datos XML en el esquema de asignación proporcionado.  
  
-   Se omite cualquier información de prólogo XML.  
  
     Carga masiva XML omite toda la información antes y después el \<raíz > elemento en el documento XML. Por ejemplo, la carga masiva XML omite todas las declaraciones XML, definiciones DTD internas, referencias DTD externas, todos los comentarios, etc.  
  
-   Si tiene un esquema de asignación que define una relación de clave principal y clave externa entre dos tablas (como Customer y CustOrder), la tabla con la clave principal debe describirse en primer lugar en el esquema. La tabla con la columna de clave externa debe aparecer posteriormente en el esquema. La razón de esto es que el orden en que se identifican las tablas en el esquema es el orden en que se usa para cargarlos en la base de datos. Por ejemplo, el esquema XDR siguiente generará un error cuando se usa en la carga masiva XML porque el  **\<orden >** se describe el elemento antes de la  **\<cliente >** elemento. La columna CustomerID de CustOrder es una columna de clave externa que hace referencia a la columna de clave principal CustomerID de la tabla Cust.  
  
    ```  
    <?xml version="1.0" ?>  
    <Schema xmlns="urn:schemas-microsoft-com:xml-data"   
            xmlns:dt="urn:schemas-microsoft-com:xml:datatypes"    
            xmlns:sql="urn:schemas-microsoft-com:xml-sql" >  
  
        <ElementType name="Order" sql:relation="CustOrder" >  
          <AttributeType name="OrderID" />  
          <AttributeType name="CustomerID" />  
          <attribute type="OrderID" />  
          <attribute type="CustomerID" />  
        </ElementType>  
  
       <ElementType name="CustomerID" dt:type="int" />  
       <ElementType name="CompanyName" dt:type="string" />  
       <ElementType name="City" dt:type="string" />  
  
       <ElementType name="root" sql:is-constant="1">  
          <element type="Customers" />  
       </ElementType>  
       <ElementType name="Customers" sql:relation="Cust"   
                         sql:overflow-field="OverflowColumn"  >  
          <element type="CustomerID" sql:field="CustomerID" />  
          <element type="CompanyName" sql:field="CompanyName" />  
          <element type="City" sql:field="City" />  
          <element type="Order" >   
               <sql:relationship  
                   key-relation="Cust"  
                    key="CustomerID"  
                    foreign-key="CustomerID"  
                    foreign-relation="CustOrder" />  
          </element>  
       </ElementType>  
    </Schema>  
    ```  
  
-   Si el esquema no especifica las columnas de desbordamiento mediante la anotación `sql:overflow-field`, la carga masiva XML omite todos los datos presentes en el documento XML que no se describen en el esquema de asignación.  
  
     La carga masiva XML aplica el esquema de asignación especificado cada vez que encuentra etiquetas conocidas en el flujo de datos XML. Omite los datos presentes en el documento XML que no se describen en el esquema. Por ejemplo, suponga que tiene un esquema de asignación que describe un  **\<cliente >** elemento. El archivo de datos XML tiene una  **\<AllCustomers >** raíz de etiqueta (que no se describe en el esquema) que abarque todos los  **\<cliente >** elementos:  
  
    ```  
    <AllCustomers>  
      <Customer>...</Customer>  
      <Customer>...</Customer>  
       ...  
    </AllCustomers>  
    ```  
  
     En este caso, la carga masiva XML omite el  **\<AllCustomers >** elemento y comienza la asignación en el  **\<cliente >** elemento. La carga masiva XML omite los elementos que no se describen en el esquema pero que están presentes en el documento XML.  
  
     Considere la posibilidad de otro archivo de datos de origen XML que contiene  **\<orden >** elementos. Estos elementos no se describen en el esquema de asignación:  
  
    ```  
    <AllCustomers>  
      <Customer>...</Customer>  
        <Order> ... </Order>  
        <Order> ... </Order>  
         ...  
      <Customer>...</Customer>  
        <Order> ... </Order>  
        <Order> ... </Order>  
         ...  
      ...  
    </AllCustomers>  
    ```  
  
     Carga masiva XML omite estos  **\<orden >** elementos. Pero si usa el `sql:overflow-field`anotación en el esquema para identificar una columna como una columna de desbordamiento, carga masiva XML almacena todos los datos no consumidos en esta columna.  
  
-   Las secciones CDATA y las referencias a entidades se traducen a sus cadenas equivalentes antes de almacenarse en la base de datos.  
  
     En este ejemplo, una sección CDATA ajusta el valor de la  **\<Ciudad >** elemento. Carga masiva XML extrae el valor de cadena ("NY") antes de insertar el  **\<Ciudad >** elemento en la base de datos.  
  
    ```  
    <City><![CDATA[NY]]> </City>  
    ```  
  
     La carga masiva XML no conserva las referencias a entidades.  
  
-   Si el esquema de asignación especifica el valor predeterminado de un atributo y los datos de origen XML no contienen dicho atributo, la carga masiva XML usa el valor predeterminado.  
  
     El esquema XDR de ejemplo siguiente asigna un valor predeterminado para el **HireDate** atributo:  
  
    ```  
    <?xml version="1.0" ?>  
    <Schema xmlns="urn:schemas-microsoft-com:xml-data"   
            xmlns:dt="urn:schemas-microsoft-com:xml:datatypes"    
            xmlns:sql="urn:schemas-microsoft-com:xml-sql" >  
       <ElementType name="root" sql:is-constant="1">  
          <element type="Customers" />  
       </ElementType>  
  
       <ElementType name="Customers" sql:relation="Cust3" >  
          <AttributeType name="CustomerID" dt:type="int"  />  
          <AttributeType name="HireDate"  default="2000-01-01" />  
          <AttributeType name="Salary"   />  
  
          <attribute type="CustomerID" sql:field="CustomerID" />  
          <attribute type="HireDate"   sql:field="HireDate"  />  
          <attribute type="Salary"     sql:field="Salary"    />  
       </ElementType>  
    </Schema>  
    ```  
  
     En estos datos XML, el **HireDate** falta el atributo de la segunda  **\<clientes >** elemento. Cuando la carga masiva XML inserta el segundo  **\<clientes >** elemento en la base de datos, utiliza el valor predeterminado que se especifica en el esquema.  
  
    ```  
    <ROOT>  
      <Customers CustomerID="1" HireDate="1999-01-01" Salary="10000" />  
      <Customers CustomerID="2" Salary="10000" />  
    </ROOT>  
    ```  
  
-   No se admite la anotación `sql:url-encode`:  
  
     No puede especificar una dirección URL en la entrada de datos XML y esperar que la carga masiva lea los datos de dicha ubicación.  
  
     Se crean las tablas que se identifican en el esquema de asignación (la base de datos debe existir). Si ya existen una o varias de las tablas en la base de datos, el sgdroptables, propiedad determina si estas tablas preexistentes se elimina y vuelve a crear.  
  
-   Si especifica la propiedad SchemaGen (por ejemplo, SchemaGen = true), se crean las tablas que se identifican en el esquema de asignación. Pero SchemaGen crea ninguna restricción (por ejemplo, las restricciones PRIMARY KEY/FOREIGN KEY) en estas tablas con una excepción: Si los nodos XML que constituyen la clave principal en una relación se definen como si tuviera un tipo XML del Id. de (es decir, `type="xsd:ID"` para XSD) y el sguseid, propiedad se establece en True para SchemaGen, no solo se crean claves principales en el identificador con el tipo de nodos , pero se crean relaciones de clave principal/clave externa de las relaciones del esquema de asignación.  
  
-   SchemaGen no usa extensiones ni facetas del esquema XSD para generar el relacional [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] esquema.  
  
-   Si especifica la propiedad SchemaGen (por ejemplo, SchemaGen = true) en la carga masiva, solo las tablas (y no las vistas de nombre compartido) que se especifican se actualizan.  
  
-   SchemaGen solamente proporciona funcionalidad básica para generar el esquema relacional de XSD anotado. El usuario debe modificar las tablas generadas manualmente si es preciso.  
  
-   Cuando más de una relación existe entre las tablas, SchemaGen intenta crear una relación única que incluye todas las claves implicadas entre las dos tablas. Esta limitación podría dar lugar a un error [!INCLUDE[tsql](../../../includes/tsql-md.md)].  
  
-   Al realizar cargas masivas de datos XML en una base de datos, debe haber al menos un atributo o elemento secundario en el esquema de asignación que esté asignado a una columna de base de datos.  
  
-   Si está insertando valores de fecha mediante la carga masiva XML, estos valores deben especificarse con el formato (-)CCYY-MM-DD((+-)TZ). Se trata del formato XSD estándar para la fecha.  
  
-   Algunas marcas de propiedad no son compatibles con otras. Por ejemplo, la carga masiva no admite `Ignoreduplicatekeys=true` junto con `Keepidentity=false`. Cuando `Keepidentity=false`, la carga masiva espera que el servidor genere los valores clave. Las tablas deberían tener una limitación de `IDENTITY` en la clave. El servidor no generará claves duplicadas, lo que significa que no es necesario que `Ignoreduplicatekeys` se establezca en `true`. `Ignoreduplicatekeys` debe establecerse en `true` solo cuando se cargan valores de clave principales de los datos entrantes en una tabla que tiene filas y existe la posibilidad de un conflicto de los valores de clave principales.  
  
  
