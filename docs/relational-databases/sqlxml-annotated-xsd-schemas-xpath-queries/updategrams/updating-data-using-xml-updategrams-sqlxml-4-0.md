---
title: Actualizar datos con diagramas de actualización XML (SQLXML 4.0) | Documentos de Microsoft
ms.custom: ''
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
author: douglaslMS
ms.author: douglasl
manager: craigg
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: f0d627b294281e5022cbc2dec34de884ab658318
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/01/2018
ms.locfileid: "47705563"
---
# <a name="updating-data-using-xml-updategrams-sqlxml-40"></a>Actualizar datos con diagramas de actualización XML (SQLXML 4.0)
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  Al actualizar los datos existentes, debe especificar tanto el  **\<antes >** y  **\<después >** bloques. Los elementos especificados en el  **\<antes >** y  **\<después >** bloques describen el cambio deseado. El diagrama de actualización utiliza los elementos que se especifican en el  **\<antes >** bloque para identificar los registros existentes en la base de datos. Los elementos correspondientes en el  **\<después >** bloque indicar cómo deberían quedar los registros después de ejecutar la operación de actualización. De esta información, el diagrama de actualización crea una instrucción SQL que coincida con el  **\<después >** bloque. A continuación, el diagrama de actualización utiliza esta instrucción para actualizar la base de datos.  
  
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
  
 **\<updg: antes de >**  
 Los elementos de la  **\<antes >** bloque identifican los registros existentes en las tablas de base de datos.  
  
 **\<updg: una vez >**  
 Los elementos de la  **\<después >** se describe cómo especifican los registros en bloque el  **\<antes de >** bloque tendrá un aspecto después de aplican las actualizaciones.  
  
 El **esquema de asignación** atributo identifica el esquema de asignación que va a usar el diagrama de actualización. Si el diagrama de actualización especifica un esquema de asignación, los nombres de elementos y atributos especificados en el  **\<antes >** y  **\<después >** bloques deben coincidir con los nombres del esquema. El esquema de asignación asigna estos nombres de elementos o atributos a los nombres de columnas y tablas de base de datos.  
  
 Si un diagrama de actualización no especifica un esquema, utilizará la asignación predeterminada. En la asignación predeterminada, el  **\<ElementName >** especificado en el diagrama de actualización se asigna a la tabla de base de datos y la asignación de elementos o atributos secundarios a las columnas de la base de datos.  
  
 Un elemento en el  **\<antes >** bloque debe coincidir con la fila de una única tabla en la base de datos. Si el elemento coincide con varias filas de tabla o no coincide con ninguna fila de tabla, el diagrama de actualización devuelve un error y cancela todo el  **\<sincronización >** bloque.  
  
 Un diagrama de actualización puede incluir varios  **\<sincronización >** bloques. Cada  **\<sincronización >** bloque se trata como una transacción. Cada  **\<sincronización >** bloque puede tener varios  **\<antes >** y  **\<después >** bloques. Por ejemplo, si va a actualizar dos de los registros existentes, podría especificar dos  **\<antes >** y  **\<después >** pares, uno para cada registro que se está actualizando.  
  
## <a name="using-the-updgid-attribute"></a>Utilizar el atributo updg:id  
 Cuando se especifican varios elementos en el  **\<antes >** y  **\<después >** bloques, utilice el **updg: ID** atributo para marcar filas en el  **\<antes >** y  **\<después >** bloques. La lógica de procesamiento utiliza esta información para determinar qué registro el  **\<antes >** pares con qué registro de bloques el  **\<después >** bloque.  
  
 El **updg: ID** atributo no es necesario (aunque se recomienda) si existe alguna de las siguientes acciones:  
  
-   Los elementos del esquema de asignación especificado tienen el **SQL: Key-campos** atributo definido en ellos.  
  
-   Hay uno o más valores concretos proporcionados para los campos de clave del diagrama de actualización.  
  
 Si cualquiera de los casos, el diagrama de actualización utiliza las columnas de clave que se especifican en el **SQL: Key-campos** para emparejar los elementos de la  **\<antes >** y  **\< una vez >** bloques.  
  
 Si el esquema de asignación no identifica las columnas de clave (mediante el uso de **SQL: Key-campos**) o si el diagrama de actualización está actualizando un valor de columna de clave, se debe especificar **updg: ID**.  
  
 Los registros que se identifican en el  **\<antes >** y  **\<después >** bloques no tiene que estar en el mismo orden. El **updg: ID** atributo fuerza la asociación entre los elementos que se especifican en el  **\<antes >** y  **\<después >** se bloquea.  
  
 Si especifica un elemento en el  **\<antes >** bloque y solo un elemento correspondiente en el  **\<después >** bloquear, mediante **updg: ID** no es necesario. Sin embargo, se recomienda que especifique **updg: ID** de todos modos para evitar la ambigüedad.  
  
## <a name="examples"></a>Ejemplos  
 Antes de utilizar los ejemplos del diagrama de actualización, tenga en cuenta lo siguiente:  
  
-   En la mayoría de los ejemplos se usa una asignación predeterminada (es decir, no se especifica ningún esquema de asignación en el diagrama de actualización). Para obtener más ejemplos de diagramas de actualización que utilizan los esquemas de asignación, consulte [especificar un esquema de asignación anotados en un diagrama de actualización &#40;SQLXML 4.0&#41;](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/updategrams/specifying-an-annotated-mapping-schema-in-an-updategram-sqlxml-4-0.md).  
  
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
  
 El registro descrito en la  **\<antes >** bloque representa el registro actual en la base de datos. El diagrama de actualización utiliza todos los valores de columna especificados en el  **\<antes >** bloque para buscar el registro. En este diagrama de actualización, el  **\<antes >** bloque proporciona sólo la columna ContactID; por lo tanto, el diagrama de actualización utiliza solo el valor para buscar el registro. Si fuera a agregar el valor LastName a este bloque, el diagrama de actualización utilizaría los valores ContactID y LastName para buscar.  
  
 En este diagrama de actualización, el  **\<después >** bloque proporciona solo el valor de la columna LastName porque este es el único valor que se va a cambiar.  
  
##### <a name="to-test-the-updategram"></a>Para probar el diagrama de actualización  
  
1.  Copie la plantilla de diagrama de actualización anterior y péguela en un archivo de texto. Guarde el archivo como UpdateLastName.xml.  
  
2.  Cree y use el script de prueba de SQLXML 4.0 (Sqlxml4test.vbs) para ejecutar el diagrama de actualización.  
  
     Para obtener más información, consulte [utilizar ADO para ejecutar consultas de SQLXML 4.0](../../../relational-databases/sqlxml/using-ado-to-execute-sqlxml-4-0-queries.md).  
  
### <a name="b-updating-multiple-records-by-using-the-updgid-attribute"></a>B. Actualizar varios registros utilizando el atributo updg:id  
 En este ejemplo, el diagrama de actualización realiza dos actualizaciones en la tabla HumanResources.Shift de la base de datos AdventureWorks:  
  
-   Cambia el nombre del turno de día original, que empieza a las 7:00 a. m., de "Day" a "Early Morning".  
  
-   Inserta un nuevo turno denominado "Late Morning" que empieza a las 10:00 a. m.  
  
 En el diagrama de actualización, el **updg: ID** atributo crea asociaciones entre los elementos de la  **\<antes >** y  **\<después >** bloques.  
  
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
  
 Observe cómo el **updg: ID** atributo empareja la primera instancia de la \<HumanResources.Shift > elemento en el  **\<antes >** bloque con la segunda instancia de la \< HumanResources.Shift > elemento en el  **\<después >** bloque.  
  
##### <a name="to-test-the-updategram"></a>Para probar el diagrama de actualización  
  
1.  Copie la plantilla de diagrama de actualización anterior y péguela en un archivo de texto. Guarde el archivo como UpdateMultipleRecords.xml.  
  
2.  Cree y use el script de prueba de SQLXML 4.0 (Sqlxml4test.vbs) para ejecutar el diagrama de actualización.  
  
     Para obtener más información, consulte [utilizar ADO para ejecutar consultas de SQLXML 4.0](../../../relational-databases/sqlxml/using-ado-to-execute-sqlxml-4-0-queries.md).  
  
### <a name="c-specifying-multiple-before-and-after-blocks"></a>C. Especificar varias \<antes > y \<después > bloques  
 Para evitar ambigüedades, puede escribir el diagrama de actualización del ejemplo B utilizando varias  **\<antes >** y  **\<después >** pares de bloques. Especificar  **\<antes >** y  **\<después >** pares es una manera de especificar varias actualizaciones con un mínimo de confusión. También, si cada uno de los  **\<antes de >** y  **\<después de >** bloques especifican al menos un elemento, no es necesario utilizar el **updg: ID** atributo .  
  
> [!NOTE]  
>  Para formar un par, el  **\<después >** etiqueta a la que debe seguir inmediatamente a su correspondiente  **\<antes >** etiqueta.  
  
 En el siguiente diagrama de actualización, la primera  **\<antes >** y  **\<después >** par actualiza el nombre del turno de día. El segundo par inserta un nuevo registro de turno.  
  
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
  
     Para obtener más información, consulte [utilizar ADO para ejecutar consultas de SQLXML 4.0](../../../relational-databases/sqlxml/using-ado-to-execute-sqlxml-4-0-queries.md).  
  
### <a name="d-specifying-multiple-sync-blocks"></a>D. Especificar varias \<sincronización > bloques  
 Puede especificar varios  **\<sincronización >** bloques en un diagrama de actualización. Cada  **\<sincronización >** bloque especificado es una transacción independiente.  
  
 En el siguiente diagrama de actualización, la primera  **\<sincronización >** bloque actualiza un registro en la tabla Sales.Customer. Para que resulte más sencillo, el diagrama de actualización especifica solamente los valores de columna necesarios; el valor de identidad (CustomerID) y el valor que se está actualizando (SalesPersonID).  
  
 El segundo  **\<sincronización >** bloque agrega dos registros a la tabla Sales.SalesOrderHeader. En esta tabla, SalesOrderID es una columna de tipo IDENTITY. Por lo tanto, el diagrama de actualización no especifica el valor de SalesOrderID en cada uno de los \<Sales.SalesOrderHeader > elementos.  
  
 Especificar varias  **\<sincronización >** bloques es útil porque si el segundo  **\<sincronización >** bloque (una transacción) no agrega registros a la tabla Sales.SalesOrderHeader, el primera  **\<sincronización >** bloque todavía puede actualizar el registro del cliente en la tabla Sales.Customer.  
  
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
  
     Para obtener más información, consulte [utilizar ADO para ejecutar consultas de SQLXML 4.0](../../../relational-databases/sqlxml/using-ado-to-execute-sqlxml-4-0-queries.md).  
  
### <a name="e-using-a-mapping-schema"></a>E. Usar un esquema de asignación  
 En este ejemplo, el diagrama de actualización especifica un esquema de asignación utilizando la **esquema de asignación** atributo. (No hay ninguna asignación predeterminada; es decir, el esquema de asignación proporciona la asignación necesaria de elementos y atributos en el diagrama de actualización a las tablas y columnas de base de datos.)  
  
 Los elementos y atributos especificados en el diagrama de actualización hacen referencia a los elementos y atributos del esquema de asignación.  
  
 El esquema de asignación XSD siguiente tiene  **\<cliente >**,  **\<orden >**, y  **\<OD >** elementos que se asignan a las Tablas Sales.Customer, Sales.SalesOrderHeader y Sales.SalesOrderDetail de la base de datos.  
  
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
  
 Este esquema de asignación (UpdategramMappingSchema.xml) se especifica en el siguiente diagrama de actualización. El diagrama de actualización agrega un elemento de detalle de pedido en la tabla Sales.SalesOrderDetail para un pedido concreto. El diagrama de actualización incluye elementos anidados: un  **\<OD >** elemento anidado dentro de un  **\<orden >** elemento. La relación de clave principal/clave externa entre estos dos elementos se especifica en el esquema de asignación.  
  
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
  
     Para obtener más información, consulte [utilizar ADO para ejecutar consultas de SQLXML 4.0](../../../relational-databases/sqlxml/using-ado-to-execute-sqlxml-4-0-queries.md).  
  
 Para obtener más ejemplos de diagramas de actualización que utilizan los esquemas de asignación, consulte [especificar un esquema de asignación anotados en un diagrama de actualización &#40;SQLXML 4.0&#41;](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/updategrams/specifying-an-annotated-mapping-schema-in-an-updategram-sqlxml-4-0.md).  
  
### <a name="f-using-a-mapping-schema-with-idrefs-attributes"></a>F. Usar un esquema de asignación con atributos IDREFS  
 En este ejemplo se muestra cómo los diagramas de actualización utilizan los atributos IDREFS en el esquema de asignación para actualizar registros en varias tablas. En este ejemplo, suponga que la base de datos está compuesta de las tablas siguientes:  
  
-   Student(StudentID, LastName)  
  
-   Course(CourseID, CourseName)  
  
-   Enrollment(StudentID, CourseID)  
  
 Dado que un alumno se puede inscribir en muchos cursos y un curso puede tener muchos alumnos, hace falta una tercera tabla, la tabla Enrollment, que represente esta relación M:N.  
  
 El siguiente esquema de asignación XSD proporciona una vista XML de las tablas mediante el  **\<Student >**,  **\<curso >**, y  **\<inscripción >** elementos. El **IDREFS** atributos en el esquema de asignación especifican la relación entre estos elementos. El **StudentIDList** atributo el  **\<curso >** elemento es un **IDREFS** atributo de tipo que hace referencia a la columna StudentID de la tabla Enrollment. Del mismo modo, el **EnrolledIn** atributo el  **\<Student >** elemento es un **IDREFS** atributo de tipo que hace referencia a la columna CourseID de la inscripción tabla.  
  
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
  
     Para obtener más información, consulte [utilizar ADO para ejecutar consultas de SQLXML 4.0](../../../relational-databases/sqlxml/using-ado-to-execute-sqlxml-4-0-queries.md).  
  
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
  
7.  Guarde y ejecute este diagrama de actualización siguiente como se describe en los pasos anteriores. Este diagrama de actualización inserta tres nuevos alumnos y los inscribe en el curso CS101. De nuevo, la relación IDREFS inserta registros en la tabla Enrollment.  
  
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
  
 Para obtener más ejemplos de diagramas de actualización que utilizan los esquemas de asignación, consulte [especificar un esquema de asignación anotados en un diagrama de actualización &#40;SQLXML 4.0&#41;](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/updategrams/specifying-an-annotated-mapping-schema-in-an-updategram-sqlxml-4-0.md).  
  
## <a name="see-also"></a>Vea también  
 [Consideraciones de seguridad de updategram &#40;SQLXML 4.0&#41;](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/security/updategram-security-considerations-sqlxml-4-0.md)  
  
  
