---
title: 'Establecer relaciones de profundidad recursiva con SQL: Max-Depth'
description: 'Obtenga información sobre cómo especificar la profundidad al consultar las tablas que tienen una relación recursiva mediante la anotación sql: Max-Depth en una XQuery.'
ms.date: 03/17/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.technology: xml
ms.topic: reference
helpviewer_keywords:
- max-depth annotation
- XPath queries [SQLXML], recursive relationships
- depth in recursive relationships [SQLXML]
- annotated XSD schemas, recursive relationships
- relationships [SQLXML], recursive relationships
- self joins
- recursive relationships [SQLXML]
- recursion [SQLXML]
- sql:max-depth
- recursive joins [SQLXML]
ms.assetid: 0ffdd57d-dc30-44d9-a8a0-f21cadedb327
author: MightyPen
ms.author: genemi
ms.reviewer: ''
ms.custom: seo-lt-2019
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 70bc2eebfcf6e0a6d84b8d8610549bff144bb51f
ms.sourcegitcommit: 5c7634b007f6808c87094174b80376cb20545d5f
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/17/2020
ms.locfileid: "84884573"
---
# <a name="specifying-depth-in-recursive-relationships-by-using-sqlmax-depth"></a>Especificar la profundidad en relaciones recursivas utilizando sql:max-depth
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  En las bases de datos relacionales, cuando una tabla se relaciona consigo misma, este tipo de relación recibe el nombre de relación recursiva. Por ejemplo, en una relación supervisor-supervisado, una tabla que almacena los registros de empleados se relaciona consigo misma. En este caso, la tabla de empleados desempeña un rol de supervisor en uno de los lados de la relación y un rol de supervisado en el otro lado.  
  
 Los esquemas de asignación pueden incluir relaciones recursivas donde un elemento y su antecesor son del mismo tipo.  
  
## <a name="example-a"></a>Ejemplo A  
 Fíjese en la siguiente tabla:  
  
```  
Emp (EmployeeID, FirstName, LastName, ReportsTo)  
```  
  
 En esta tabla, la columna ReportsTo almacena el identificador de empleado del director.  
  
 Supongamos que desea crear una jerarquía XML de empleados en la que el empleado director se sitúa en la parte superior de la jerarquía y los empleados que son subordinados directos de ese director aparecen en la jerarquía correspondiente tal y como se muestra en el siguiente fragmento XML de ejemplo. Lo que muestra este fragmento es el *árbol recursivo* del empleado 1.  
  
```  
<?xml version="1.0" encoding="utf-8" ?>   
<root>  
  <Emp FirstName="Nancy" EmployeeID="1" LastName="Devolio">  
     <Emp FirstName="Andrew" EmployeeID="2" LastName="Fuller" />   
     <Emp FirstName="Janet" EmployeeID="3" LastName="Leverling">  
        <Emp FirstName="Margaret" EmployeeID="4" LastName="Peacock">  
          <Emp FirstName="Steven" EmployeeID="5" LastName="Devolio">  
...  
...  
</root>  
```  
  
 En este fragmento, el empleado 5 es subordinado directo del empleado 4, el empleado 4 es subordinado directo del empleado 3 y los empleados 3 y 2 son subordinados directos del empleado 1.  
  
 Para generar este resultado, puede usar el siguiente esquema XSD y especificar una consulta XPath en él. El esquema describe un **\<Emp>** elemento de tipo EmployeeType, que consta de un **\<Emp>** elemento secundario del mismo tipo, EmployeeType. Se trata de una relación recursiva (el elemento y su antecesor son del mismo tipo). Además, el esquema utiliza **\<sql:relationship>** para describir la relación de elementos primarios y secundarios entre el supervisor y el supervisado. Tenga en cuenta que **\<sql:relationship>** , en este, EMP es la tabla primaria y la secundaria.  
  
```  
<xsd:schema xmlns:xsd="http://www.w3.org/2001/XMLSchema"  
            xmlns:dt="urn:schemas-microsoft-com:datatypes"  
            xmlns:sql="urn:schemas-microsoft-com:mapping-schema">  
  <xsd:annotation>  
    <xsd:appinfo>  
      <sql:relationship name="SupervisorSupervisee"  
                                  parent="Emp"  
                                  parent-key="EmployeeID"  
                                  child="Emp"  
                                  child-key="ReportsTo" />  
    </xsd:appinfo>  
  </xsd:annotation>  
  <xsd:element name="Emp" type="EmployeeType"   
                          sql:relation="Emp"   
                          sql:key-fields="EmployeeID"   
                          sql:limit-field="ReportsTo" />  
  <xsd:complexType name="EmployeeType">  
    <xsd:sequence>  
      <xsd:element name="Emp" type="EmployeeType"   
                              sql:relation="Emp"   
                              sql:key-fields="EmployeeID"  
                              sql:relationship="SupervisorSupervisee"  
                              sql:max-depth="6" />  
    </xsd:sequence>   
    <xsd:attribute name="EmployeeID" type="xsd:ID" />  
    <xsd:attribute name="FirstName" type="xsd:string"/>  
    <xsd:attribute name="LastName" type="xsd:string"/>  
  </xsd:complexType>  
</xsd:schema>  
```  
  
 Dado que la relación es recursiva, necesita algún modo de especificar la profundidad de recursión del esquema. De lo contrario, el resultado será una recursión sin fin (empleado subordinado directo de empleado subordinado directo de empleado, etc.). La anotación **SQL: Max-Depth** permite especificar la profundidad de la recursividad. En este ejemplo concreto, para especificar un valor para **SQL: Max-Depth**, debe saber la profundidad de la jerarquía de administración en la empresa.  
  
> [!NOTE]  
>  El esquema especifica la anotación **SQL: limit-field** , pero no especifica la anotación **SQL: Limit-Value** . Esto limita el nodo superior de la jerarquía resultante únicamente a los empleados que no son subordinados directos de nadie. (Reportto es NULL). Al especificar **SQL: limit-field** y no especificar **SQL: Limit-Value** (que tiene como valor predeterminado NULL), la anotación logra esto. Si desea que el XML resultante incluya todos los árboles de informes posibles (el árbol de informes de cada empleado de la tabla), quite la anotación **SQL: limit-field** del esquema.  
  
> [!NOTE]  
>  El siguiente procedimiento usa la base de datos tempdb.  
  
#### <a name="to-test-a-sample-xpath-query-against-the-schema"></a>Para probar una consulta XPath de ejemplo en el esquema  
  
1.  Cree una tabla de ejemplo denominada Emp en la base de datos tempdb a la que apunta la raíz virtual.  
  
    ```  
    USE tempdb  
    CREATE TABLE Emp (  
           EmployeeID int primary key,   
           FirstName  varchar(20),   
           LastName   varchar(20),   
           ReportsTo int)  
    ```  
  
2.  Agregue estos datos de ejemplo:  
  
    ```  
    INSERT INTO Emp values (1, 'Nancy', 'Devolio',NULL)  
    INSERT INTO Emp values (2, 'Andrew', 'Fuller',1)  
    INSERT INTO Emp values (3, 'Janet', 'Leverling',1)  
    INSERT INTO Emp values (4, 'Margaret', 'Peacock',3)  
    INSERT INTO Emp values (5, 'Steven', 'Devolio',4)  
    INSERT INTO Emp values (6, 'Nancy', 'Buchanan',5)  
    INSERT INTO Emp values (7, 'Michael', 'Suyama',6)  
    ```  
  
3.  Copie el código de esquema anterior y péguelo en un archivo de texto. Guarde el archivo como maxDepth.xml.  
  
4.  Copie la plantilla siguiente y péguela en un archivo de texto. Guarde el archivo como maxDepthT.xml en el mismo directorio donde guardó maxDepth.xml. La consulta de la plantilla devuelve todos los empleados de la tabla Emp.  
  
    ```  
    <ROOT xmlns:sql="urn:schemas-microsoft-com:xml-sql">  
      <sql:xpath-query mapping-schema="maxDepth.xml">  
        /Emp  
      </sql:xpath-query>  
    </ROOT>  
    ```  
  
     La ruta de acceso al directorio especificada para el esquema de asignación (maxDepth.xml) es relativa al directorio donde se guarda la plantilla. También puede especificarse una ruta de acceso absoluta como, por ejemplo:  
  
    ```  
    mapping-schema="C:\MyDir\maxDepth.xml"  
    ```  
  
5.  Cree y use el script de prueba SQLXML 4.0 (Sqlxml4test.vbs) para ejecutar la plantilla. Para obtener más información, vea [usar ado para ejecutar consultas SQLXML 4,0](../../relational-databases/sqlxml/using-ado-to-execute-sqlxml-4-0-queries.md).  

 El resultado es el siguiente:  
  
```  
<?xml version="1.0" encoding="utf-8" ?>   
<root>  
  <Emp FirstName="Nancy" EmployeeID="1" LastName="Devolio">  
  <Emp FirstName="Andrew" EmployeeID="2" LastName="Fuller" />   
    <Emp FirstName="Janet" EmployeeID="3" LastName="Leverling">  
      <Emp FirstName="Margaret" EmployeeID="4" LastName="Peacock">  
        <Emp FirstName="Steven" EmployeeID="5" LastName="Devolio">  
          <Emp FirstName="Nancy" EmployeeID="6" LastName="Buchanan">  
            <Emp FirstName="Michael" EmployeeID="7" LastName="Suyama" />   
          </Emp>  
        </Emp>  
      </Emp>  
    </Emp>  
  </Emp>  
</root>  
```  
  
> [!NOTE]  
>  Para generar diferentes profundidades de jerarquías en el resultado, cambie el valor de la anotación **SQL: Max-Depth** en el esquema y vuelva a ejecutar la plantilla después de cada cambio.  
  
 En el esquema anterior, todos los **\<Emp>** elementos tenían exactamente el mismo conjunto de atributos (**EmployeeID**, **FirstName**y **LastName**). El esquema siguiente se ha modificado ligeramente para devolver un atributo **Reportto** adicional para todos los **\<Emp>** elementos que informan a un administrador.  
  
 Por ejemplo, este fragmento XML muestra los subordinados del empleado 1:  
  
```  
<?xml version="1.0" encoding="utf-8" ?>   
<root>  
<Emp FirstName="Nancy" EmployeeID="1" LastName="Devolio">  
  <Emp FirstName="Andrew" EmployeeID="2"   
       ReportsTo="1" LastName="Fuller" />   
  <Emp FirstName="Janet" EmployeeID="3"   
       ReportsTo="1" LastName="Leverling">  
...  
...  
```  
  
 Éste es el esquema revisado:  
  
```  
<xsd:schema xmlns:xsd="http://www.w3.org/2001/XMLSchema"  
            xmlns:dt="urn:schemas-microsoft-com:datatypes"  
            xmlns:sql="urn:schemas-microsoft-com:mapping-schema">  
  <xsd:annotation>  
    <xsd:documentation>  
      Customer-Order-Order Details Schema  
      Copyright 2000 Microsoft. All rights reserved.  
    </xsd:documentation>  
    <xsd:appinfo>  
      <sql:relationship name="SupervisorSupervisee"   
                  parent="Emp"  
                  parent-key="EmployeeID"  
                  child="Emp"  
                  child-key="ReportsTo" />  
    </xsd:appinfo>  
  </xsd:annotation>  
  <xsd:element name="Emp"   
                   type="EmpType"   
                   sql:relation="Emp"   
                   sql:key-fields="EmployeeID"   
                   sql:limit-field="ReportsTo" />  
  <xsd:complexType name="EmpType">  
    <xsd:sequence>  
       <xsd:element name="Emp"   
                    type="EmpType"   
                    sql:relation="Emp"   
                    sql:key-fields="EmployeeID"  
                    sql:relationship="SupervisorSupervisee"  
                    sql:max-depth="6"/>  
    </xsd:sequence>   
    <xsd:attribute name="EmployeeID" type="xsd:int" />  
    <xsd:attribute name="FirstName" type="xsd:string"/>  
    <xsd:attribute name="LastName" type="xsd:string"/>  
    <xsd:attribute name="ReportsTo" type="xsd:int" />  
  </xsd:complexType>  
</xsd:schema>  
```  
  
## <a name="sqlmax-depth-annotation"></a>Anotación sql:max-depth  
 En un esquema compuesto de relaciones recursivas, la profundidad de recursión debe especificarse de forma explícita en el esquema. Esto es necesario para generar correctamente la consulta FOR XML EXPLICIT correspondiente que devuelve los resultados solicitados.  
  
 Use la anotación **SQL: Max-Depth** en el esquema para especificar la profundidad de recursividad en una relación recursiva que se describe en el esquema. El valor de la anotación **SQL: Max-Depth** es un entero positivo (de 1 a 50) que indica el número de repeticiones: un valor de 1 detiene la recursividad en el elemento para el que se especifica la anotación **SQL: Max-Depth** ; un valor de 2 detiene la recursividad en el siguiente nivel del elemento en el que se especifica **SQL: Max-Depth** ; etc.  
  
> [!NOTE]  
>  En la implementación subyacente, una consulta XPath que se especifica en un esquema de asignación se convierte en una consulta SELECT ... FOR XML EXPLICIT. Esta consulta exige que se especifique una profundidad finita de recursión. Cuanto mayor sea el valor que especifique para **SQL: Max-Depth**, mayor será la consulta for XML EXPLICIT que se genera. Esto puede ralentizar el tiempo de recuperación.  
  
> [!NOTE]  
>  Los diagramas de actualización y la carga masiva XML omiten la anotación max-depth. Esto significa que se llevarán a cabo inserciones o actualizaciones recursivas independientemente del valor que se especifique para max-depth.  
  
## <a name="specifying-sqlmax-depth-on-complex-elements"></a>Especificar sql:max-depth en elementos complejos  
 La anotación **SQL: Max-Depth** se puede especificar en cualquier elemento de contenido complejo.  
  
### <a name="recursive-elements"></a>Elementos recursivos  
 Si se especifica **SQL: Max-Depth** en el elemento primario y en el elemento secundario de una relación recursiva, la anotación **SQL: Max-Depth** especificada en el elemento primario tiene prioridad. Por ejemplo, en el esquema siguiente, la anotación **SQL: Max-Depth** se especifica en los elementos primarios y secundarios. En este caso, **SQL: Max-Depth = 4**, especificado en el **\<Emp>** elemento primario (que desempeña un rol de supervisor), tiene prioridad. Se omite **SQL: Max-Depth** especificada en el **\<Emp>** elemento secundario (que desempeña un rol de supervisado).  
  
#### <a name="example-b"></a>Ejemplo B  
  
```  
<xsd:schema xmlns:xsd="http://www.w3.org/2001/XMLSchema"  
            xmlns:dt="urn:schemas-microsoft-com:datatypes"  
            xmlns:sql="urn:schemas-microsoft-com:mapping-schema">  
  <xsd:annotation>  
    <xsd:appinfo>  
      <sql:relationship name="SupervisorSupervisee"  
                                  parent="Emp"  
                                  parent-key="EmployeeID"  
                                  child="Emp"  
                                  child-key="ReportsTo" />  
    </xsd:appinfo>  
  </xsd:annotation>  
  <xsd:element name="Emp" type="EmployeeType"   
                          sql:relation="Emp"   
                          sql:key-fields="EmployeeID"   
                          sql:limit-field="ReportsTo"   
                          sql:max-depth="3" />  
  <xsd:complexType name="EmployeeType">  
    <xsd:sequence>  
      <xsd:element name="Emp" type="EmployeeType"   
                              sql:relation="Emp"   
                              sql:key-fields="EmployeeID"  
                              sql:relationship="SupervisorSupervisee"  
                              sql:max-depth="2" />  
    </xsd:sequence>   
    <xsd:attribute name="EmployeeID" type="xsd:ID" />  
    <xsd:attribute name="FirstName" type="xsd:string"/>  
    <xsd:attribute name="LastName" type="xsd:string"/>  
  </xsd:complexType>  
</xsd:schema>  
```  
  
 Para probar este esquema, siga los pasos proporcionados para el ejemplo A, anteriormente en este tema.  
  
### <a name="nonrecursive-elements"></a>Elementos no recursivos  
 Si la anotación **SQL: Max-Depth** se especifica en un elemento del esquema que no produce ninguna recursividad, se omite. En el esquema siguiente, un **\<Emp>** elemento consta de un **\<Constant>** elemento secundario, que, a su vez, tiene un **\<Emp>** elemento secundario.  
  
 En este esquema, la anotación **SQL: Max-Depth** especificada en el **\<Constant>** elemento se omite porque no hay ninguna recursividad entre el **\<Emp>** elemento primario y el **\<Constant>** elemento secundario. Pero hay recursividad entre el **\<Emp>** antecesor y el **\<Emp>** secundario. El esquema especifica la anotación **SQL: Max-Depth** en ambos. Por lo tanto, la anotación **SQL: Max-Depth** que se especifica en el antecesor ( **\<Emp>** en el rol supervisor) tiene prioridad.  
  
#### <a name="example-c"></a>Ejemplo C  
  
```  
<xsd:schema xmlns:xsd="http://www.w3.org/2001/XMLSchema"   
xmlns:sql="urn:schemas-microsoft-com:mapping-schema">  
  <xsd:annotation>  
    <xsd:appinfo>  
      <sql:relationship name="SupervisorSupervisee"   
                  parent="Emp"   
                  child="Emp"   
                  parent-key="EmployeeID"   
                  child-key="ReportsTo"/>  
    </xsd:appinfo>  
  </xsd:annotation>  
  <xsd:element name="Emp"   
               sql:relation="Emp"   
               type="EmpType"  
               sql:limit-field="ReportsTo"  
               sql:max-depth="1" />  
    <xsd:complexType name="EmpType" >  
      <xsd:sequence>  
       <xsd:element name="Constant"   
                    sql:is-constant="1"   
                    sql:max-depth="20" >  
         <xsd:complexType >  
           <xsd:sequence>  
            <xsd:element name="Emp"   
                         sql:relation="Emp" type="EmpType"  
                         sql:relationship="SupervisorSupervisee"   
                         sql:max-depth="3" />  
         </xsd:sequence>  
         </xsd:complexType>  
         </xsd:element>  
      </xsd:sequence>  
      <xsd:attribute name="EmployeeID" type="xsd:int" />  
    </xsd:complexType>  
</xsd:schema>  
```  
  
 Para probar este esquema, siga los pasos que se proporcionaron para el Ejemplo A anteriormente en este tema.  
  
## <a name="complex-types-derived-by-restriction"></a>Tipos complejos derivados por restricción  
 Si tiene una derivación de tipo complejo por **\<restriction>** , los elementos del tipo complejo base correspondiente no pueden especificar la anotación **SQL: Max-Depth** . En estos casos, se puede Agregar la anotación **SQL: Max-Depth** al elemento del tipo derivado.  
  
 Por otro lado, si tiene una derivación de tipo complejo por **\<extension>** , los elementos del tipo complejo base correspondiente pueden especificar la anotación **SQL: Max-Depth** .  
  
 Por ejemplo, el esquema XSD siguiente genera un error porque la anotación **SQL: Max-Depth** se especifica en el tipo base. Esta anotación no se admite en un tipo derivado **\<restriction>** de desde otro tipo. Para corregir este problema, debe cambiar el esquema y especificar la anotación **SQL: Max-Depth** en el elemento del tipo derivado.  
  
#### <a name="example-d"></a>Ejemplo D  
  
```  
<xsd:schema xmlns:xsd="http://www.w3.org/2001/XMLSchema"  
            xmlns:dt="urn:schemas-microsoft-com:datatypes"  
            xmlns:msdata="urn:schemas-microsoft-com:mapping-schema">  
  <xsd:complexType name="CustomerBaseType">   
    <xsd:sequence>  
       <xsd:element name="CID" msdata:field="CustomerID" />  
       <xsd:element name="CompanyName"/>  
       <xsd:element name="Customers" msdata:max-depth="3">  
         <xsd:annotation>  
           <xsd:appinfo>  
             <msdata:relationship  
                     parent="Customers"  
                     parent-key="CustomerID"  
                     child-key="CustomerID"  
                     child="Customers" />  
           </xsd:appinfo>  
         </xsd:annotation>  
       </xsd:element>  
    </xsd:sequence>  
  </xsd:complexType>  
  <xsd:element name="Customers" type="CustomerType"/>  
  <xsd:complexType name="CustomerType">  
    <xsd:complexContent>  
       <xsd:restriction base="CustomerBaseType">  
          <xsd:sequence>  
            <xsd:element name="CID"   
                         type="xsd:string"/>  
            <xsd:element name="CompanyName"   
                         type="xsd:string"  
                         msdata:field="CName" />  
            <xsd:element name="Customers"   
                         type="CustomerType" />  
          </xsd:sequence>  
       </xsd:restriction>  
    </xsd:complexContent>  
  </xsd:complexType>  
</xsd:schema>   
```  
  
 En el esquema, **SQL: Max-Depth** se especifica en un tipo complejo de **CustomerBaseType** . El esquema también especifica un **\<Customer>** elemento de tipo **CustomerType**, que se deriva de **CustomerBaseType**. Una consulta XPath especificada en este tipo de esquema generará un error, porque **SQL: Max-Depth** no se admite en un elemento que se define en un tipo base de restricción.  
  
## <a name="schemas-with-a-deep-hierarchy"></a>Esquemas con una jerarquía profunda  
 Puede tener un esquema que incluya una jerarquía profunda en la que un elemento contiene un elemento secundario, que a su vez contiene otro elemento secundario, y así sucesivamente. Si la anotación **SQL: Max-Depth** especificada en un esquema de este tipo genera un documento XML que incluye una jerarquía de más de 500 niveles (con un elemento de nivel superior en el nivel 1, su secundario en el nivel 2, etc.), se devuelve un error.  
  
  
