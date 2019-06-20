---
title: Especificar la profundidad en relaciones recursivas utilizando SQL-profundidad | Microsoft Docs
ms.custom: ''
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
manager: craigg
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 84011f13a222ee66fdbfe5bf57d3ef74dd41a052
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "65980752"
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
  
 Supongamos que desea crear una jerarquía XML de empleados en la que el empleado director se sitúa en la parte superior de la jerarquía y los empleados que son subordinados directos de ese director aparecen en la jerarquía correspondiente tal y como se muestra en el siguiente fragmento XML de ejemplo. Este fragmento que se muestra es el *árbol recursivo* del empleado 1.  
  
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
  
 Para generar este resultado, puede usar el siguiente esquema XSD y especificar una consulta XPath en él. El esquema describe un  **\<Emp >** elemento de tipo EmployeeType, que consta de un  **\<Emp >** elemento secundario del mismo tipo, EmployeeType. Se trata de una relación recursiva (el elemento y su antecesor son del mismo tipo). Además, el esquema usa un  **\<SQL: Relationship >** para describir la relación de elementos primarios y secundarios entre el supervisor y el supervisado. Tenga en cuenta que en este  **\<SQL: Relationship >** , Emp es el elemento primario y la tabla secundaria.  
  
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
  
 Dado que la relación es recursiva, necesita algún modo de especificar la profundidad de recursión del esquema. De lo contrario, el resultado será una recursión sin fin (empleado subordinado directo de empleado subordinado directo de empleado, etc.). El **SQL-profundidad** anotación le permite especificar la profundidad de la recursión. En este ejemplo concreto, para especificar un valor para **SQL-profundidad**, debe conocer la dirección de la jerarquía de administración de profundidad de la compañía.  
  
> [!NOTE]  
>  El esquema especifica la **SQL: limit-campo** anotación, pero no especifica la **SQL: limit-valor** anotación. Esto limita el nodo superior de la jerarquía resultante únicamente a los empleados que no son subordinados directos de nadie. (ReportsTo es NULL). Especificar **SQL: limit-campo** y no especificar **SQL: limit-valor** (cuyo valor predeterminado es null) anotación lleva a cabo. Si desea que el código XML resultante incluya cada posible reporting árbol (el árbol de informes para todos los empleados en la tabla), quite el **SQL: limit-campo** anotación del esquema.  
  
> [!NOTE]  
>  El siguiente procedimiento usa la base de datos tempdb.  
  
#### <a name="to-test-a-sample-xpath-query-against-the-schema"></a>Para probar una consulta de XPath de ejemplo con respecto al esquema  
  
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
  
5.  Cree y use el script de prueba SQLXML 4.0 (Sqlxml4test.vbs) para ejecutar la plantilla. Para obtener más información, consulte [utilizar ADO para ejecutar consultas de SQLXML 4.0](../../relational-databases/sqlxml/using-ado-to-execute-sqlxml-4-0-queries.md).  
  
 Éste es el resultado:  
  
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
>  Para crear distintas profundidades de jerarquías en el resultado, cambie el valor de la **SQL-profundidad** anotación en el esquema y ejecutar la plantilla de nuevo después de cada cambio.  
  
 En el esquema anterior, todas las  **\<Emp >** elementos tenían exactamente el mismo conjunto de atributos (**EmployeeID**, **FirstName**, y  **LastName**). El siguiente esquema se ha modificado ligeramente para que devuelva más **ReportsTo** atributo para todos los  **\<Emp >** elementos que se comunican con un administrador de.  
  
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
  
 Use la **SQL-profundidad** anotación en el esquema para especificar la profundidad de recursión de una relación recursiva que se describe en el esquema. El valor de la **SQL-profundidad** anotación es un entero positivo (de 1 a 50) que indica el número de recursiones:  Un valor de 1 detiene la recursión en el elemento para el que el **SQL-profundidad** anotación se especifica; un valor de 2 detiene la recursión en el siguiente nivel del elemento en el que **SQL-profundidad** se especifica ; y así sucesivamente.  
  
> [!NOTE]  
>  En la implementación subyacente, una consulta XPath que se especifica en un esquema de asignación se convierte en una instrucción SELECT... Consulta FOR XML EXPLICIT. Esta consulta exige que se especifique una profundidad finita de recursión. Cuanto mayor sea el valor que especifique para **SQL-profundidad**, cuanto mayor sea la consulta FOR XML EXPLICIT que se genera. Esto puede ralentizar el tiempo de recuperación.  
  
> [!NOTE]  
>  Los diagramas de actualización y la carga masiva XML omiten la anotación max-depth. Esto significa que se llevarán a cabo inserciones o actualizaciones recursivas independientemente del valor que se especifique para max-depth.  
  
## <a name="specifying-sqlmax-depth-on-complex-elements"></a>Especificar sql:max-depth en elementos complejos  
 El **SQL-profundidad** anotación puede especificarse en cualquier elemento de contenido complejo.  
  
### <a name="recursive-elements"></a>Elementos recursivos  
 Si **SQL-profundidad** se especifica en el elemento primario y el elemento secundario de una relación recursiva, la **SQL-profundidad** la anotación especificada en el elemento primario tiene prioridad. Por ejemplo, en el esquema siguiente, el **SQL-profundidad** anotación se especifica en el elemento primario y los elementos de empleado secundarios. En este caso, **SQL-profundidad = 4**, especificado en el  **\<Emp >** elemento primario (que desempeña el rol de supervisor) tiene prioridad. El **SQL-profundidad** especificado en el elemento secundario  **\<Emp >** se omite el elemento (que desempeña un rol de supervisado).  
  
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
  
 Para probar este esquema, siga los pasos indicados para un ejemplo, anteriormente en este tema.  
  
### <a name="nonrecursive-elements"></a>Elementos no recursivos  
 Si el **SQL-profundidad** anotación se especifica en un elemento en el esquema que no presenta ninguna recursión, se omite. En el siguiente esquema, un  **\<Emp >** elemento consta de un  **\<constante >** elemento secundario, que, a su vez, tiene un  **\<Emp >** elemento secundario.  
  
 En este esquema, el **SQL-profundidad** la anotación especificada en el  **\<constante >** se omite el elemento porque no hay ninguna recursión entre el  **\<Emp >** primario y el  **\<constante >** elemento secundario. Pero hay recursión entre el  **\<Emp >** antecesor y  **\<Emp >** secundarios. El esquema especifica la **SQL-profundidad** anotación en ambos. Por lo tanto, el **SQL-profundidad** anotación que se especifica en el antecesor ( **\<Emp >** en el rol de supervisor) tiene prioridad.  
  
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
 Si tiene una derivación de tipo complejo por  **\<restricción >** , elementos de tipo complejo base correspondiente no se pueden especificar el **SQL-profundidad** anotación. En estos casos, el **SQL-profundidad** anotación puede agregarse al elemento del tipo derivado.  
  
 Por otro lado, si tiene una derivación de tipo complejo por  **\<extensión >** , pueden especificar los elementos de tipo complejo base correspondiente el **SQL-profundidad** anotación.  
  
 Por ejemplo, el siguiente esquema XSD genera un error porque el **SQL-profundidad** anotación se especifica en el tipo base. Esta anotación no se admite en un tipo que se deriva por  **\<restricción >** de otro tipo. Para corregir este problema, debe cambiar el esquema y especificar el **SQL-profundidad** anotación en el elemento en el tipo derivado.  
  
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
  
 En el esquema, **SQL-profundidad** se especifica en un **CustomerBaseType** tipo complejo. El esquema también especifica un  **\<cliente >** elemento de tipo **CustomerType**, que se deriva **CustomerBaseType**. Una consulta XPath especificada en este tipo de esquema generará un error, porque **SQL-profundidad** no se admite en un elemento que se define en un tipo de base de restricción.  
  
## <a name="schemas-with-a-deep-hierarchy"></a>Esquemas con una jerarquía profunda  
 Puede tener un esquema que incluya una jerarquía profunda en la que un elemento contiene un elemento secundario, que a su vez contiene otro elemento secundario, y así sucesivamente. Si el **SQL-profundidad** la anotación especificada en un esquema de este tipo genera un documento XML que incluye una jerarquía de más de 500 niveles (con el elemento de nivel superior en el nivel 1, su elemento secundario en el nivel 2 y así sucesivamente), se devuelve un error.  
  
  
