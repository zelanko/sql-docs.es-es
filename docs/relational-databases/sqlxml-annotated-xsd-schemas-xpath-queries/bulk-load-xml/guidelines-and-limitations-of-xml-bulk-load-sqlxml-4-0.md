---
title: Instrucciones y limitaciones de XML realizar la carga masiva (SQLXML 4.0) | Documentos de Microsoft
ms.custom: 
ms.date: 03/16/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: sqlxml
ms.reviewer: 
ms.suite: sql
ms.technology: dbe-xml
ms.tgt_pltfrm: 
ms.topic: reference
helpviewer_keywords:
- XML Bulk Load [SQLXML], about XML Bulk Load
- bulk load [SQLXML], about bulk load
ms.assetid: c5885d14-c7c1-47b3-a389-455e99a7ece1
caps.latest.revision: "26"
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 453ce7fe955af4ffe25d13b1ab1abfef0f48cf59
ms.sourcegitcommit: 7673ad0e84a6de69420e19247a59e39ca751a8aa
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 01/03/2018
---
# <a name="guidelines-and-limitations-of-xml-bulk-load-sqlxml-40"></a>Instrucciones y limitaciones de la carga masiva XML (SQLXML 4.0)
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]Cuando se utiliza la carga masiva XML, debe estar familiarizado con las siguientes directrices y limitaciones:  
  
-   No se admiten los esquemas insertados.  
  
     Si tiene un esquema insertado en el documento XML de origen, la carga masiva XML omite dicho esquema. Debe especificar el esquema de asignación para la carga masiva XML de forma externa con respecto a los datos XML. No se puede especificar el esquema de asignación en un nodo mediante el uso de la **xmlns = "x: schema"** atributo.  
  
-   Se comprueba que el formato de un documento XML sea correcto, pero no se valida el documento.  
  
     La carga masiva XML comprueba el documento XML para determinar si el formato es correcto, es decir, para asegurarse de que el XML cumple los requisitos de sintaxis de la recomendación XML 1.0 de World Wide Web Consortium. Si el documento no tiene el formato correcto, la carga masiva XML cancela el procesamiento y devuelve un error. La única excepción a esta regla es que el documento sea un fragmento (por ejemplo, el documento no tiene ningún elemento raíz único), en cuyo caso la carga masiva XML cargará el documento.  
  
     La carga masiva XML no valida el documento con respecto a cualquier esquema de datos XML o esquema DTD que se defina o al que se haga referencia dentro del archivo de datos XML. Además, la carga masiva XML no valida el archivo de datos XML en el esquema de asignación proporcionado.  
  
-   Se omite cualquier información de prólogo XML.  
  
     Carga masiva XML omite toda la información antes y después de la \<raíz > elemento en el documento XML. Por ejemplo, la carga masiva XML omite todas las declaraciones XML, definiciones DTD internas, referencias DTD externas, todos los comentarios, etc.  
  
-   Si tiene un esquema de asignación que define una relación de clave principal y clave externa entre dos tablas (como Customer y CustOrder), la tabla con la clave principal debe describirse en primer lugar en el esquema. La tabla con la columna de clave externa debe aparecer posteriormente en el esquema. La razón de ello es que el orden en que se identifican las tablas en el esquema es el orden en que se usa para cargarlos en la base de datos. Por ejemplo, el esquema XDR siguiente generará un error cuando se utiliza en la carga masiva XML porque el  **\<orden >** descrito elemento antes de la  **\<cliente >** elemento. La columna CustomerID de CustOrder es una columna de clave externa que hace referencia a la columna de clave principal CustomerID de la tabla Cust.  
  
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
  
-   Si el esquema no especifica las columnas de desbordamiento mediante el uso de la **SQL: overflow-campo** anotación, carga masiva XML omite todos los datos que está presente en el documento XML, pero no se describen en el esquema de asignación.  
  
     La carga masiva XML aplica el esquema de asignación especificado cada vez que encuentra etiquetas conocidas en el flujo de datos XML. Omite los datos presentes en el documento XML que no se describen en el esquema. Por ejemplo, suponga que tiene un esquema de asignación que describe un  **\<cliente >** elemento. El archivo de datos XML tiene un  **\<AllCustomers >** raíz etiqueta (que no se describe en el esquema) que incluye todos los  **\<cliente >** elementos:  
  
    ```  
    <AllCustomers>  
      <Customer>...</Customer>  
      <Customer>...</Customer>  
       ...  
    </AllCustomers>  
    ```  
  
     En este caso, carga masiva XML omite el  **\<AllCustomers >** elemento y comienza la asignación en el  **\<cliente >** elemento. La carga masiva XML omite los elementos que no se describen en el esquema pero que están presentes en el documento XML.  
  
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
  
     Carga masiva XML omite estos  **\<orden >** elementos. Sin embargo, si usas el **SQL: overflow-campo**anotación en el esquema para identificar una columna como una columna de desbordamiento, carga masiva XML almacena todos los datos no consumidos en esta columna.  
  
-   Las secciones CDATA y las referencias a entidades se traducen a sus cadenas equivalentes antes de almacenarse en la base de datos.  
  
     En este ejemplo, una sección CDATA ajusta el valor de la  **\<Ciudad >** elemento. Carga masiva XML extrae el valor de cadena ("NY") antes de insertar el  **\<Ciudad >** elemento en la base de datos.  
  
    ```  
    <City><![CDATA[NY]]> </City>  
    ```  
  
     La carga masiva XML no conserva las referencias a entidades.  
  
-   Si el esquema de asignación especifica el valor predeterminado de un atributo y los datos de origen XML no contienen dicho atributo, la carga masiva XML usa el valor predeterminado.  
  
     El siguiente esquema XDR de ejemplo asigna un valor predeterminado para la **HireDate** atributo:  
  
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
  
     En estos datos XML, la **HireDate** atributo no está presente en el segundo  **\<clientes >** elemento. Cuando la carga masiva XML inserta el segundo  **\<clientes >** elemento en la base de datos, utiliza el valor predeterminado que se especifica en el esquema.  
  
    ```  
    <ROOT>  
      <Customers CustomerID="1" HireDate="1999-01-01" Salary="10000" />  
      <Customers CustomerID="2" Salary="10000" />  
    </ROOT>  
    ```  
  
-   El **SQL-codificar** anotación no se admite:  
  
     No puede especificar una dirección URL en la entrada de datos XML y esperar que la carga masiva lea los datos de dicha ubicación.  
  
     Se crean las tablas que se identifican en el esquema de asignación (la base de datos debe existir). Si ya existen una o varias de las tablas en la base de datos, sgdroptables, propiedad determina si estas tablas preexistentes se quitará y volver a crear.  
  
-   Si especifica schemagen, propiedad (por ejemplo, SchemaGen = true), se crean las tablas que se identifican en el esquema de asignación. Pero SchemaGen no crea ninguna restricción (por ejemplo, las restricciones PRIMARY KEY/FOREIGN KEY) en estas tablas con una excepción: si los nodos XML que constituyen la clave principal de una relación se definen como si tuvieran un tipo de XML del identificador (es decir, **tipo = "xsd: ID"** para XSD) y sguseid, propiedad se establece en True para SchemaGen, a continuación, no solo se crean claves principales en el Id. de escribir nodos, aunque las relaciones de clave principales/clave externa se crean a partir de las relaciones de esquema de asignación.  
  
-   SchemaGen no usa extensiones ni facetas del esquema XSD para generar el relacional [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] esquema.  
  
-   Si especifica schemagen, propiedad (por ejemplo, SchemaGen = true) en la carga masiva, solo las tablas (y no las vistas de nombre de recurso compartido) que se especifican se actualizan.  
  
-   SchemaGen solamente proporciona funcionalidad básica para generar el esquema relacional de XSD anotado. El usuario debe modificar las tablas generadas manualmente si es preciso.  
  
-   Donde existe más de una relación entre tablas, SchemaGen intenta crear una relación única que incluye todas las claves implicadas entre las dos tablas. Esta limitación podría dar lugar a un error [!INCLUDE[tsql](../../../includes/tsql-md.md)].  
  
-   Al realizar cargas masivas de datos XML en una base de datos, debe haber al menos un atributo o elemento secundario en el esquema de asignación que esté asignado a una columna de base de datos.  
  
-   Si está insertando valores de fecha mediante la carga masiva XML, estos valores deben especificarse con el formato (-)CCYY-MM-DD((+-)TZ). Se trata del formato XSD estándar para la fecha.  
  
-   Algunas marcas de propiedad no son compatibles con otras. Por ejemplo, la carga masiva no admite **Ignoreduplicatekeys = true** junto con **Keepidentity = false**. Cuando **Keepidentity = false**, carga masiva espera que el servidor para generar los valores de clave. Las tablas deben tener un **identidad** restricción en la clave. El servidor no generará claves duplicadas, lo que significa que no es necesario para **Ignoreduplicatekeys** se establezca en **true**. **IgnoreDuplicateKeys** debe establecerse en **true** solo cuando se cargan los valores de clave principal de los datos entrantes en una tabla que tiene filas y no hay posibilidad de un conflicto de valores de clave principal.  
  
  
