---
title: Actualizar datos mediante diagramas XML (SQLXML)
ms.date: 03/17/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: xml
ms.topic: reference
helpviewer_keywords:
- IDREF type attribute [SQLXML]
- before attribute
- <sync> block
- <after> block
- id attribute
- <before> block
- updg:after attribute
- mapping-schema attribute
- IDREFS type attribute [SQLXML]
- updg:id attribute
- multiple record updates
- after attribute
- updategrams [SQLXML], updating data
- updg:before attribute
- record updates [SQLXML]
ms.assetid: 90ef8a33-5ae3-4984-8259-608d2f1d727f
author: MightyPen
ms.author: genemi
ms.custom: seo-lt-2019
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 3526595d169f5283f849017f1fabec24f33d553c
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/27/2020
ms.locfileid: "75255991"
---
# <a name="updating-data-using-xml-updategrams-sqlxml-40"></a>Actualizar datos con diagramas de actualización XML (SQLXML 4.0)
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  Al actualizar los datos existentes, debe especificar los ** \<bloques antes>** y ** \<después de>** . Los elementos especificados en los ** \<bloques Before>** y ** \<After>** describen el cambio deseado. Diagrama usa los elementos que se especifican en el ** \<bloque Before>** para identificar los registros existentes en la base de datos. Los elementos correspondientes del bloque ** \<After>** indican cómo deben ser los registros después de ejecutar la operación de actualización. A partir de esta información, diagrama crea una instrucción SQL que coincide con el ** \<bloque After>** . A continuación, el diagrama de actualización utiliza esta instrucción para actualizar la base de datos.  
  
 Este es el formato del diagrama de actualización para una operación de actualización:  
  
```  
<ROOT xmlns:updg="urn:schemas-microsoft-com:xml-updategram">  
<updg:sync [mapping-schema="SampleSchema.xml"]  >  
   <updg:before>  
      <ElementName [updg:id="value"] .../>  
      [<ElementName [updg:id="value"] .../> ... ]  
   </updg:before>  
   <updg:after>  
      <ElementName [updg:id="value"] ... />  
      [<ElementName [updg:id="value"] .../> ...]  
   </updg:after>  
</updg:sync>  
</ROOT>  
```  
  
 **\<atributo updg: Before>**  
 Los elementos del bloque ** \<Before>** identifican los registros existentes en las tablas de base de datos.  
  
 **\<atributo updg: después>**  
 Los elementos del bloque ** \<After>** describen cómo deben ser los registros especificados en el ** \<bloque Before>** después de aplicar las actualizaciones.  
  
 El atributo **mapping-schema** identifica el esquema de asignación que va a usar diagrama. Si diagrama especifica un esquema de asignación, los nombres de elemento y atributo especificados ** \<** en los bloques antes de>y ** \<después de>** deben coincidir con los nombres del esquema. El esquema de asignación asigna estos nombres de elementos o atributos a los nombres de columnas y tablas de base de datos.  
  
 Si un diagrama de actualización no especifica un esquema, utilizará la asignación predeterminada. En la asignación predeterminada, el ** \<>ElementName** especificado en diagrama se asigna a la tabla de base de datos y los elementos secundarios o atributos se asignan a las columnas de la base de datos.  
  
 Un elemento del bloque ** \<Before>** debe coincidir con solo una fila de la tabla en la base de datos. Si el elemento coincide con varias filas de la tabla o no coincide con ninguna fila de la tabla, diagrama devuelve un error y cancela ** \<** todo el bloque de>de sincronización.  
  
 Un diagrama puede incluir varios ** \<** bloques de>de sincronización. Cada bloque de ** \<>de sincronización** se trata como una transacción. Cada ** \<** bloque de>de sincronización puede tener varios ** \<bloques Before>** y ** \<After>** . Por ejemplo, si está actualizando dos de los registros existentes, puede especificar dos ** \<antes de>** y ** \<después de>** pares, uno para cada registro que se está actualizando.  
  
## <a name="using-the-updgid-attribute"></a>Utilizar el atributo updg:id  
 Cuando se especifican varios elementos en los ** \<bloques Before>** y ** \<After>** , utilice el atributo **atributo updg: ID** para marcar las filas en los ** \<** ** \<** bloques de>antes>y after. La lógica de procesamiento usa esta información para determinar qué registro del bloque ** \<Before>** pares con qué registro del bloque ** \<After>** .  
  
 El atributo **atributo updg: ID** no es necesario (aunque se recomienda) si se cumple alguna de las siguientes acciones:  
  
-   Los elementos del esquema de asignación especificado tienen definido el atributo **SQL: Key-Fields** .  
  
-   Hay uno o más valores concretos proporcionados para los campos de clave del diagrama de actualización.  
  
 Si es así, el diagrama usa las columnas de clave que se especifican en **SQL: Key-Fields** para emparejar los elementos de los ** \<bloques antes>** y ** \<After>** .  
  
 Si el esquema de asignación no identifica las columnas de clave (mediante **SQL: Key-Fields**) o si diagrama está actualizando un valor de columna de clave, debe especificar **atributo updg: ID**.  
  
 Los registros que se identifican en los ** \<bloques Before>** y ** \<After>** no tienen que estar en el mismo orden. El atributo **atributo updg: ID** fuerza la asociación entre los elementos que se especifican en los ** \<bloques antes de>** y ** \<después de>** .  
  
 Si especifica un elemento en el ** \<bloque Before>** y solo un elemento correspondiente en el ** \<bloque After>** , no es necesario usar **atributo updg: ID** . Sin embargo, se recomienda que especifique **atributo updg: ID** de todos modos para evitar la ambigüedad.  
  
## <a name="examples"></a>Ejemplos  
 Antes de utilizar los ejemplos del diagrama de actualización, tenga en cuenta lo siguiente:  
  
-   En la mayoría de los ejemplos se usa una asignación predeterminada (es decir, no se especifica ningún esquema de asignación en el diagrama de actualización). Para obtener más ejemplos de diagramas que usan esquemas de asignación, vea [especificar un esquema de asignación anotado en un diagrama &#40;SQLXML 4,0&#41;](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/updategrams/specifying-an-annotated-mapping-schema-in-an-updategram-sqlxml-4-0.md).  
  
-   La mayoría de los ejemplos utilizan la base de datos de ejemplo AdventureWorks. Todas las actualizaciones se aplican a las tablas de esta base de datos. Puede restaurar la base de datos AdventureWorks.  
  
### <a name="a-updating-a-record"></a>A. Actualizar un registro  
 El siguiente diagrama de actualización actualiza el apellido del empleado a Fuller en la tabla Person.Contact de la base de datos AdventureWorks. El diagrama de actualización no especifica ningún esquema de asignación, por lo que utilizará la asignación predeterminada.  
  
```  
<ROOT xmlns:updg="urn:schemas-microsoft-com:xml-updategram">  
<updg:sync >  
<updg:before>  
   <Person.Contact ContactID="1" />  
</updg:before>  
<updg:after>  
   <Person.Contact LastName="Abel-Achong" />  
</updg:after>  
</updg:sync>  
</ROOT>  
```  
  
 El registro descrito en el ** \<bloque Before>** representa el registro actual de la base de datos. Diagrama usa todos los valores de columna especificados en el ** \<bloque Before>** para buscar el registro. En este diagrama, el ** \<bloque Before>** solo proporciona la columna ContactID; por lo tanto, diagrama usa solo el valor para buscar el registro. Si fuera a agregar el valor LastName a este bloque, el diagrama de actualización utilizaría los valores ContactID y LastName para buscar.  
  
 En este diagrama, el ** \<bloque After>** solo proporciona el valor de la columna LastName porque es el único valor que se va a cambiar.  
  
##### <a name="to-test-the-updategram"></a>Para probar el diagrama de actualización  
  
1.  Copie la plantilla de diagrama de actualización anterior y péguela en un archivo de texto. Guarde el archivo como UpdateLastName.xml.  
  
2.  Cree y use el script de prueba de SQLXML 4.0 (Sqlxml4test.vbs) para ejecutar el diagrama de actualización.  

     Para obtener más información, vea [usar ado para ejecutar consultas SQLXML 4,0](../../../relational-databases/sqlxml/using-ado-to-execute-sqlxml-4-0-queries.md).  
  
### <a name="b-updating-multiple-records-by-using-the-updgid-attribute"></a>B. Actualizar varios registros utilizando el atributo updg:id  
 En este ejemplo, el diagrama de actualización realiza dos actualizaciones en la tabla HumanResources.Shift de la base de datos AdventureWorks:  
  
-   Cambia el nombre del turno de día original, que empieza a las 7:00 a. m., de "Day" a "Early Morning".  
  
-   Inserta un nuevo turno denominado "Late Morning" que empieza a las 10:00 a. m.  
  
 En diagrama, el atributo **atributo updg: ID** crea asociaciones entre los elementos de los ** \<bloques antes>** y ** \<After>** .  
  
```  
<ROOT xmlns:updg="urn:schemas-microsoft-com:xml-updategram">  
  <updg:sync >  
    <updg:before>  
       <HumanResources.Shift updg:id="x" Name="Day" />  
    </updg:before>  
    <updg:after>  
      <HumanResources.Shift updg:id="y" Name="Late Morning"   
                            StartTime="1900-01-01 10:00:00.000"  
                            EndTime="1900-01-01 18:00:00.000"  
                            ModifiedDate="2004-06-01 00:00:00.000"/>  
      <HumanResources.Shift updg:id="x" Name="Early Morning" />  
    </updg:after>  
  </updg:sync>  
</ROOT>  
```  
  
 Observe cómo el atributo **atributo updg: ID** empareja la primera instancia del elemento \<rehumanresources. Shift> del bloque ** \<Before>** por la segunda instancia del elemento \<> humanresources. Shift en el ** \<bloque After>** .  
  
##### <a name="to-test-the-updategram"></a>Para probar el diagrama de actualización  
  
1.  Copie la plantilla de diagrama de actualización anterior y péguela en un archivo de texto. Guarde el archivo como UpdateMultipleRecords.xml.  
  
2.  Cree y use el script de prueba de SQLXML 4.0 (Sqlxml4test.vbs) para ejecutar el diagrama de actualización.  
  
     Para obtener más información, vea [usar ado para ejecutar consultas SQLXML 4,0](../../../relational-databases/sqlxml/using-ado-to-execute-sqlxml-4-0-queries.md).  
  
### <a name="c-specifying-multiple-before-and-after-blocks"></a>C. Especificar varias \<antes de> y \<después de> bloques  
 Para evitar ambigüedades, puede escribir diagrama en el ejemplo B mediante el uso de multiple ** \<antes>** y ** \<después de>** pares de bloques. Especificar ** \<antes de>** y ** \<después de>** pares es una manera de especificar varias actualizaciones con un mínimo de confusión. Además, si cada uno de los ** \<bloques Before>** y ** \<After>** especifica como máximo un elemento, no es necesario usar el atributo **atributo updg: ID** .  
  
> [!NOTE]  
>  Para formar un par, la etiqueta ** \<After>** debe seguir inmediatamente a su correspondiente ** \<antes de>** etiqueta.  
  
 En el siguiente diagrama, el primer ** \<par>** y ** \<After>** actualiza el nombre del turno para el turno de día. El segundo par inserta un nuevo registro de turno.  
  
```  
<ROOT xmlns:updg="urn:schemas-microsoft-com:xml-updategram">  
  <updg:sync >  
    <updg:before>  
       <HumanResources.Shift ShiftID="1" Name="Day" />  
    </updg:before>  
    <updg:after>  
      <HumanResources.Shift Name="Early Morning" />  
    </updg:after>  
    <updg:before>  
    </updg:before>  
    <updg:after>  
      <HumanResources.Shift Name="Late Morning"   
                            StartTime="1900-01-01 10:00:00.000"  
                            EndTime="1900-01-01 18:00:00.000"  
                            ModifiedDate="2004-06-01 00:00:00.000"/>  
    </updg:after>  
  </updg:sync>  
</ROOT>  
```  
  
##### <a name="to-test-the-updategram"></a>Para probar el diagrama de actualización  
  
1.  Copie la plantilla de diagrama de actualización anterior y péguela en un archivo de texto. Guarde el archivo como UpdateMultipleBeforeAfter.xml.  
  
2.  Cree y use el script de prueba de SQLXML 4.0 (Sqlxml4test.vbs) para ejecutar el diagrama de actualización.  
  
     Para obtener más información, vea [usar ado para ejecutar consultas SQLXML 4,0](../../../relational-databases/sqlxml/using-ado-to-execute-sqlxml-4-0-queries.md).  
  
### <a name="d-specifying-multiple-sync-blocks"></a>D. Especificar varios \<bloques de> de sincronización  
 Puede especificar varios ** \<** bloques de>de sincronización en un diagrama. Cada bloque de ** \<>de sincronización** que se especifica es una transacción independiente.  
  
 En el siguiente diagrama, el primer ** \<** bloque de>de sincronización actualiza un registro en la tabla sales. Customer. Para que resulte más sencillo, el diagrama de actualización especifica solamente los valores de columna necesarios; el valor de identidad (CustomerID) y el valor que se está actualizando (SalesPersonID).  
  
 El segundo ** \<** bloque de>de sincronización agrega dos registros a la tabla sales. SalesOrderHeader. En esta tabla, SalesOrderID es una columna de tipo IDENTITY. Por lo tanto, diagrama no especifica el valor de SalesOrderID en cada uno de \<los elementos sales. SalesOrderHeader>.  
  
 Especificar varios ** \<** bloques de>de sincronización es útil porque si el ** \<** segundo bloque de>de sincronización (una transacción) no agrega registros a la tabla sales. SalesOrderHeader, el primer ** \<** bloque de>de sincronización todavía puede actualizar el registro del cliente en la tabla sales. Customer.  
  
```  
<ROOT xmlns:updg="urn:schemas-microsoft-com:xml-updategram">  
  <updg:sync >  
    <updg:before>  
      <Sales.Customer CustomerID="1" SalesPersonID="280" />  
    </updg:before>  
    <updg:after>  
      <Sales.Customer CustomerID="1" SalesPersonID="283" />  
    </updg:after>  
  </updg:sync>  
  <updg:sync >  
    <updg:before>  
    </updg:before>  
    <updg:after>  
   <Sales.SalesOrderHeader   
             CustomerID="1"  
             RevisionNumber="1"  
             OrderDate="2004-07-01 00:00:00.000"  
             DueDate="2004-07-13 00:00:00.000"  
             OnlineOrderFlag="0"  
             ContactID="378"  
             BillToAddressID="985"  
             ShipToAddressID="985"  
             ShipMethodID="5"  
             SubTotal="24643.9362"  
             TaxAmt="1971.5149"  
             Freight="616.0984"  
             rowguid="01010101-2222-3333-4444-556677889900"  
             ModifiedDate="2004-07-08 00:00:00.000" />  
   <Sales.SalesOrderHeader  
             CustomerID="1"  
             RevisionNumber="1"  
             OrderDate="2004-07-01 00:00:00.000"  
             DueDate="2004-07-13 00:00:00.000"  
             OnlineOrderFlag="0"  
             ContactID="378"  
             BillToAddressID="985"  
             ShipToAddressID="985"  
             ShipMethodID="5"  
             SubTotal="1000.0000"  
             TaxAmt="0.0000"  
             Freight="0.0000"  
             rowguid="10101010-2222-3333-4444-556677889900"  
             ModifiedDate="2004-07-09 00:00:00.000" />  
    </updg:after>  
  </updg:sync>  
</ROOT>  
```  
  
##### <a name="to-test-the-updategram"></a>Para probar el diagrama de actualización  
  
1.  Copie la plantilla de diagrama de actualización anterior y péguela en un archivo de texto. Guarde el archivo como UpdateMultipleSyncs.xml.  
  
2.  Cree y use el script de prueba de SQLXML 4.0 (Sqlxml4test.vbs) para ejecutar el diagrama de actualización.  
  
     Para obtener más información, vea [usar ado para ejecutar consultas SQLXML 4,0](../../../relational-databases/sqlxml/using-ado-to-execute-sqlxml-4-0-queries.md).  
  
### <a name="e-using-a-mapping-schema"></a>E. Usar un esquema de asignación  
 En este ejemplo, diagrama especifica un esquema de asignación mediante el atributo **mapping-schema** . (No hay ninguna asignación predeterminada; es decir, el esquema de asignación proporciona la asignación necesaria de elementos y atributos en el diagrama de actualización a las tablas y columnas de base de datos.)  
  
 Los elementos y atributos especificados en el diagrama de actualización hacen referencia a los elementos y atributos del esquema de asignación.  
  
 El siguiente esquema de asignación XSD tiene ** \<elementos Customer>**, ** \<Order>** y ** \<OD>** que se asignan a las tablas sales. Customer, sales. SalesOrderHeader y sales. SalesOrderDetail de la base de datos.  
  
```  
<xsd:schema xmlns:xsd="http://www.w3.org/2001/XMLSchema"  
            xmlns:sql="urn:schemas-microsoft-com:mapping-schema">  
<xsd:annotation>  
  <xsd:appinfo>  
    <sql:relationship name="CustomerOrder"  
          parent="Sales.Customer"  
          parent-key="CustomerID"  
          child="Sales.SalesOrderHeader"  
          child-key="CustomerID" />  
  
    <sql:relationship name="OrderOD"  
          parent="Sales.SalesOrderHeader"  
          parent-key="SalesOrderID"  
          child="Sales.SalesOrderDetail"  
          child-key="SalesOrderID" />  
  </xsd:appinfo>  
</xsd:annotation>  
  
  <xsd:element name="Customer" sql:relation="Sales.Customer" >  
   <xsd:complexType>  
     <xsd:sequence>  
        <xsd:element name="Order"   
                     sql:relation="Sales.SalesOrderHeader"  
                     sql:relationship="CustomerOrder" >  
           <xsd:complexType>  
              <xsd:sequence>  
                <xsd:element name="OD"   
                             sql:relation="Sales.SalesOrderDetail"  
                             sql:relationship="OrderOD" >  
                 <xsd:complexType>  
                  <xsd:attribute name="SalesOrderID" type="xsd:integer" />  
                  <xsd:attribute name="ProductID" type="xsd:integer" />  
                  <xsd:attribute name="UnitPrice" type="xsd:decimal" />  
                  <xsd:attribute name="OrderQty" type="xsd:integer" />  
                  <xsd:attribute name="UnitPriceDiscount" type="xsd:decimal" />   
                 </xsd:complexType>  
                </xsd:element>  
              </xsd:sequence>  
              <xsd:attribute name="CustomerID" type="xsd:string" />  
              <xsd:attribute name="SalesOrderID" type="xsd:integer" />  
              <xsd:attribute name="OrderDate" type="xsd:date" />  
           </xsd:complexType>  
        </xsd:element>  
      </xsd:sequence>  
      <xsd:attribute name="CustomerID"   type="xsd:string" />   
    </xsd:complexType>  
  </xsd:element>  
</xsd:schema>  
```  
  
 Este esquema de asignación (UpdategramMappingSchema.xml) se especifica en el siguiente diagrama de actualización. El diagrama de actualización agrega un elemento de detalle de pedido en la tabla Sales.SalesOrderDetail para un pedido concreto. Diagrama incluye elementos anidados: un ** \<elemento do>** anidado dentro de un ** \<elemento Order>** . La relación de clave principal/clave externa entre estos dos elementos se especifica en el esquema de asignación.  
  
```  
<ROOT xmlns:updg="urn:schemas-microsoft-com:xml-updategram">  
  <updg:sync mapping-schema="UpdategramMappingSchema.xml" >  
    <updg:before>  
       <Order SalesOrderID="43659" />  
    </updg:before>  
    <updg:after>  
      <Order SalesOrderID="43659" >  
          <OD ProductID="776" UnitPrice="2329.0000"  
              OrderQty="2" UnitPriceDiscount="0.0" />  
      </Order>  
    </updg:after>  
  </updg:sync>  
</ROOT>  
```  
  
##### <a name="to-test-the-updategram"></a>Para probar el diagrama de actualización  
  
1.  Copie el esquema de asignación anterior y péguelo en un archivo de texto. Guarde el archivo como UpdategramMappingSchema.xml.  
  
2.  Copie la plantilla de diagrama de actualización anterior y péguela en un archivo de texto. Guarde el archivo como UpdateWithMappingSchema.xml en la misma carpeta que se utilizó para guardar el esquema de asignación (UpdategramMappingSchema.xml).  
  
3.  Cree y use el script de prueba de SQLXML 4.0 (Sqlxml4test.vbs) para ejecutar el diagrama de actualización.  
  
     Para obtener más información, vea [usar ado para ejecutar consultas SQLXML 4,0](../../../relational-databases/sqlxml/using-ado-to-execute-sqlxml-4-0-queries.md).  
  
 Para obtener más ejemplos de diagramas que usan esquemas de asignación, vea [especificar un esquema de asignación anotado en un diagrama &#40;SQLXML 4,0&#41;](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/updategrams/specifying-an-annotated-mapping-schema-in-an-updategram-sqlxml-4-0.md).  
  
### <a name="f-using-a-mapping-schema-with-idrefs-attributes"></a>F. Usar un esquema de asignación con atributos IDREFS  
 En este ejemplo se muestra cómo los diagramas de actualización utilizan los atributos IDREFS en el esquema de asignación para actualizar registros en varias tablas. En este ejemplo, suponga que la base de datos está compuesta de las tablas siguientes:  
  
-   Student(StudentID, LastName)  
  
-   Course(CourseID, CourseName)  
  
-   Enrollment(StudentID, CourseID)  
  
 Dado que un alumno se puede inscribir en muchos cursos y un curso puede tener muchos alumnos, hace falta una tercera tabla, la tabla Enrollment, que represente esta relación M:N.  
  
 El siguiente esquema de asignación XSD proporciona una vista XML de las tablas mediante los ** \<elementos Student>**, ** \<Course>** y ** \<Enrollment>** . Los atributos **IDREFS** en el esquema de asignación especifican la relación entre estos elementos. El atributo **StudentIDList** del elemento ** \<Course>** es un atributo de tipo **IDREFS** que hace referencia a la columna StudentID de la tabla Enrollment. Del mismo modo **, el atributo** inscrito en el ** \<elemento Student>** es un atributo de tipo **IDREFS** que hace referencia a la columna CourseID de la tabla Enrollment.  
  
```  
<xsd:schema xmlns:xsd="http://www.w3.org/2001/XMLSchema"  
            xmlns:sql="urn:schemas-microsoft-com:mapping-schema">  
<xsd:annotation>  
  <xsd:appinfo>  
    <sql:relationship name="StudentEnrollment"  
          parent="Student"  
          parent-key="StudentID"  
          child="Enrollment"  
          child-key="StudentID" />  
  
    <sql:relationship name="CourseEnrollment"  
          parent="Course"  
          parent-key="CourseID"  
          child="Enrollment"  
          child-key="CourseID" />  
  </xsd:appinfo>  
</xsd:annotation>  
  
  <xsd:element name="Course" sql:relation="Course"   
                             sql:key-fields="CourseID" >  
    <xsd:complexType>  
    <xsd:attribute name="CourseID"  type="xsd:string" />   
    <xsd:attribute name="CourseName"   type="xsd:string" />   
    <xsd:attribute name="StudentIDList" sql:relation="Enrollment"  
                 sql:field="StudentID"  
                 sql:relationship="CourseEnrollment"   
                                     type="xsd:IDREFS" />  
  
    </xsd:complexType>  
  </xsd:element>  
  <xsd:element name="Student" sql:relation="Student" >  
    <xsd:complexType>  
    <xsd:attribute name="StudentID"  type="xsd:string" />   
    <xsd:attribute name="LastName"   type="xsd:string" />   
    <xsd:attribute name="EnrolledIn" sql:relation="Enrollment"  
                 sql:field="CourseID"  
                 sql:relationship="StudentEnrollment"   
                                     type="xsd:IDREFS" />  
    </xsd:complexType>  
  </xsd:element>  
</xsd:schema>  
```  
  
 Cada vez que especifique este esquema en un diagrama de actualización e inserte un registro en la tabla Course, el diagrama de actualización insertará un nuevo registro de curso en la tabla Course. Si especifica uno o más identificadores de alumnos nuevos para el atributo StudentIDList, el diagrama de actualización también insertará un registro en la tabla Enrollment para cada nuevo alumno. El diagrama de actualización asegura que no se agregan registros duplicados a la tabla Enrollment.  
  
##### <a name="to-test-the-updategram"></a>Para probar el diagrama de actualización  
  
1.  Cree estas tablas en la base de datos especificada en la raíz virtual:  
  
    ```  
    CREATE TABLE Student(StudentID varchar(10) primary key,   
                         LastName varchar(25))  
    CREATE TABLE Course(CourseID varchar(10) primary key,   
                        CourseName varchar(25))  
    CREATE TABLE Enrollment(StudentID varchar(10)   
                                      references Student(StudentID),  
                           CourseID varchar(10)   
                                      references Course(CourseID))  
    ```  
  
2.  Agregue estos datos de ejemplo:  
  
    ```  
    INSERT INTO Student VALUES ('S1','Davoli')  
    INSERT INTO Student VALUES ('S2','Fuller')  
  
    INSERT INTO Course VALUES  ('CS101', 'C Programming')  
    INSERT INTO Course VALUES  ('CS102', 'Understanding XML')  
  
    INSERT INTO Enrollment VALUES ('S1', 'CS101')  
    INSERT INTO Enrollment VALUES ('S1', 'CS102')  
    ```  
  
3.  Copie el esquema de asignación anterior y péguelo en un archivo de texto. Guarde el archivo como SampleSchema.xml.  
  
4.  Guarde el diagrama de actualización (SampleUpdategram) en la misma carpeta utilizada para guardar el esquema de asignación en el paso anterior. (Este diagrama de actualización quita un alumno con StudentID = "1" del curso CS102.)  
  
    ```  
    <ROOT xmlns:updg="urn:schemas-microsoft-com:xml-updategram">  
      <updg:sync mapping-schema="SampleSchema.xml" >  
        <updg:before>  
            <Student updg:id="x" StudentID="S1" LastName="Davolio"  
                                 EnrolledIn="CS101 CS102" />  
        </updg:before>  
        <updg:after >  
            <Student updg:id="x" StudentID="S1" LastName="Davolio"  
                                 EnrolledIn="CS101" />  
        </updg:after>  
      </updg:sync>  
    </ROOT>  
    ```  
  
5.  Cree y use el script de prueba de SQLXML 4.0 (Sqlxml4test.vbs) para ejecutar el diagrama de actualización.  
  
     Para obtener más información, vea [usar ado para ejecutar consultas SQLXML 4,0](../../../relational-databases/sqlxml/using-ado-to-execute-sqlxml-4-0-queries.md).  
  
6.  Guarde y ejecute el siguiente diagrama de actualización tal y como se describe en los pasos anteriores. El diagrama de actualización vuelve a incluir al alumno con StudentID = "1" en el curso CS102 agregando un registro en la tabla Enrollment.  
  
    ```  
    <ROOT xmlns:updg="urn:schemas-microsoft-com:xml-updategram">  
      <updg:sync mapping-schema="SampleSchema.xml" >  
        <updg:before>  
            <Student updg:id="x" StudentID="S1" LastName="Davolio"  
                                 EnrolledIn="CS101" />  
        </updg:before>  
        <updg:after >  
            <Student updg:id="x" StudentID="S1" LastName="Davolio"  
                                 EnrolledIn="CS101 CS102" />  
        </updg:after>  
      </updg:sync>  
    </ROOT>  
    ```  
  
7.  Guarde y ejecute este siguiente diagrama como se describe en los pasos anteriores. Este diagrama de actualización inserta tres nuevos alumnos y los inscribe en el curso CS101. De nuevo, la relación IDREFS inserta registros en la tabla Enrollment.  
  
    ```  
    <ROOT xmlns:updg="urn:schemas-microsoft-com:xml-updategram">  
      <updg:sync mapping-schema="SampleSchema.xml" >  
        <updg:before>  
           <Course updg:id="y" CourseID="CS101"   
                               CourseName="C Programming" />  
        </updg:before>  
        <updg:after >  
           <Student updg:id="x1" StudentID="S3" LastName="Leverling" />  
           <Student updg:id="x2" StudentID="S4" LastName="Pecock" />  
           <Student updg:id="x3" StudentID="S5" LastName="Buchanan" />  
           <Course updg:id="y" CourseID="CS101"  
                               CourseName="C Programming"  
                               StudentIDList="S3 S4 S5" />  
        </updg:after>  
      </updg:sync>  
    </ROOT>  
    ```  
  
 Éste es el esquema XDR equivalente:  
  
```  
<?xml version="1.0" ?>  
<Schema xmlns="urn:schemas-microsoft-com:xml-data"  
        xmlns:dt="urn:schemas-microsoft-com:datatypes"  
        xmlns:sql="urn:schemas-microsoft-com:xml-sql">  
  <ElementType name="Enrollment" sql:relation="Enrollment" sql:key-fields="StudentID CourseID">  
    <AttributeType name="StudentID" dt:type="id" />  
    <AttributeType name="CourseID" dt:type="id" />  
  
    <attribute type="StudentID" />  
    <attribute type="CourseID" />  
  </ElementType>  
  <ElementType name="Course" sql:relation="Course" sql:key-fields="CourseID">  
    <AttributeType name="CourseID" dt:type="id" />  
    <AttributeType name="CourseName" />  
  
    <attribute type="CourseID" />  
    <attribute type="CourseName" />  
  
    <AttributeType name="StudentIDList" dt:type="idrefs" />  
    <attribute type="StudentIDList" sql:relation="Enrollment" sql:field="StudentID" >  
        <sql:relationship  
                key-relation="Course"  
                key="CourseID"  
                foreign-relation="Enrollment"  
                foreign-key="CourseID" />  
    </attribute>  
  
  </ElementType>  
  <ElementType name="Student" sql:relation="Student">  
    <AttributeType name="StudentID" dt:type="id" />  
     <AttributeType name="LastName" />  
  
    <attribute type="StudentID" />  
    <attribute type="LastName" />  
  
    <AttributeType name="EnrolledIn" dt:type="idrefs" />  
    <attribute type="EnrolledIn" sql:relation="Enrollment" sql:field="CourseID" >  
        <sql:relationship  
                key-relation="Student"  
                key="StudentID"  
                foreign-relation="Enrollment"  
                foreign-key="StudentID" />  
    </attribute>  
  
    <element type="Enrollment" sql:relation="Enrollment" >  
        <sql:relationship key-relation="Student"  
                          key="StudentID"  
                          foreign-relation="Enrollment"  
                          foreign-key="StudentID" />  
    </element>  
  </ElementType>  
  
</Schema>  
```  
  
 Para obtener más ejemplos de diagramas que usan esquemas de asignación, vea [especificar un esquema de asignación anotado en un diagrama &#40;SQLXML 4,0&#41;](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/updategrams/specifying-an-annotated-mapping-schema-in-an-updategram-sqlxml-4-0.md).  
  
## <a name="see-also"></a>Consulte también  
 [Consideraciones de seguridad de diagrama &#40;SQLXML 4,0&#41;](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/security/updategram-security-considerations-sqlxml-4-0.md)  
  
  
