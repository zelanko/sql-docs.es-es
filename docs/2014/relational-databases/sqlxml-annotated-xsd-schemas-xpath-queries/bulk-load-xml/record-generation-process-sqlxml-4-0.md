---
title: Registrar el proceso de generación (SQLXML 4.0) | Documentos de Microsoft
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- XML Bulk Load [SQLXML], record generation process
- node scopes [SQLXML]
- record subsets [SQLXML]
- scope [SQLXML]
- key ordering rules [SQLXML]
- record generation process for bulk loads [SQLXML]
- entering node scope [SQLXML]
- bulk load [SQLXML], record generation process
- leaving node scope [SQLXML]
- schema mapping [SQLXML]
ms.assetid: d8885bbe-6f15-4fb9-9684-ca7883cfe9ac
caps.latest.revision: 23
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: 066dd7d143c57f06240a74aa058dec3588db0f55
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36113337"
---
# <a name="record-generation-process-sqlxml-40"></a>Proceso de generación de registros (SQLXML 4.0)
  La carga masiva XML procesa los datos de entrada XML y prepara los registros para las tablas adecuadas de Microsoft [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. La lógica de la carga masiva XML determina cuándo generar un nuevo registro, qué elemento secundario o valores de atributo copiar en los campos del registro y cuándo está completo y preparado el registro para enviarse a [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] para su inserción.  
  
 La carga masiva XML no carga los datos de entrada XML completos en la memoria y no genera conjuntos de registros completos antes de enviar los datos a [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. Esto ocurre porque los datos de entrada XML pueden ser un documento de gran tamaño y cargar todo el documento en la memoria puede resultar costoso. En lugar de ello, la carga masiva XML hace lo siguiente:  
  
1.  Analiza el esquema de asignación y prepara el plan de ejecución necesario.  
  
2.  Aplica el plan de ejecución a los datos del flujo de entrada.  
  
 Este procesamiento secuencial hace que sea importante proporcionar los datos de entrada XML de un modo específico. Debe entender la forma en que la carga masiva XML analiza el esquema de asignación y la forma en que se produce el proceso de generación de registros. Sabiendo esto, podrá proporcionar un esquema de asignación para la carga masiva XML que genere los resultados que desee.  
  
 La carga masiva XML administra anotaciones comunes del esquema de asignación, incluidas las asignaciones de columna y tabla (que se especifican de forma explícita mediante anotaciones o de forma implícita a través de la asignación predeterminada), así como relaciones de unión.  
  
> [!NOTE]  
>  Se supone que está familiarizado con los esquemas de asignación XSD o XDR anotados. Para obtener más información acerca de los esquemas, vea [Introducción a los esquemas XSD anotados &#40;SQLXML 4.0&#41; ](../../sqlxml/annotated-xsd-schemas/introduction-to-annotated-xsd-schemas-sqlxml-4-0.md) o [esquemas XDR anotados &#40;desusado en SQLXML 4.0&#41;](../../sqlxml/annotated-xsd-schemas/annotated-xdr-schemas-deprecated-in-sqlxml-4-0.md).  
  
 Para entender el proceso de generación de registros es necesario comprender los conceptos siguientes:  
  
-   Ámbito de un nodo  
  
-   Regla de generación de registros  
  
-   Subconjunto de registros y la regla de orden de clave  
  
-   Excepciones a la regla de generación de registros  
  
## <a name="scope-of-a-node"></a>Ámbito de un nodo  
 Entra en un nodo (un elemento o atributo) en un documento XML *en el ámbito* cuando la carga masiva XML se encuentra en el flujo de datos de entrada XML. En el caso de un nodo de elemento, la etiqueta inicial del elemento introduce el elemento en el ámbito. En el caso de un nodo de atributo, el nombre de atributo introduce el atributo en el ámbito.  
  
 Un nodo sale del ámbito cuando no hay más datos de él, ya sea en la etiqueta final (en el caso de un nodo de elemento) o al final de un valor de atributo (en el caso de un nodo de atributo).  
  
## <a name="record-generation-rule"></a>Regla de generación de registros  
 Cuando un nodo (elemento o atributo) entra en el ámbito, significa que existe el potencial de generar un registro a partir de ese nodo. El período de vida del registro termina cuando el nodo asociado sale del ámbito. Cuando el nodo sale del ámbito, la carga masiva XML considera que el registro generado está completo (de datos) y lo envía a [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] para insertarlo.  
  
 Por ejemplo, fíjese en el siguiente fragmento de esquema XSD:  
  
```  
<xsd:schema xmlns:xsd="http://www.w3.org/2001/XMLSchema"  
            xmlns:sql="urn:schemas-microsoft-com:mapping-schema">  
  <xsd:element name="Customer" sql:relation="Customers" >  
   <xsd:complexType>  
     <xsd:attribute name="CustomerID" type="xsd:string" />  
     <xsd:attribute name="CompanyName" type="xsd:string" />  
    </xsd:complexType>  
  </xsd:element>  
</xsd:schema>  
```  
  
 El esquema especifica un  **\<cliente >** elemento con **CustomerID** y **CompanyName** atributos. El `sql:relation` anotación asigna el  **\<cliente >** elemento a la tabla Customers.  
  
 Fíjese en este fragmento de un documento XML:  
  
```  
<Customer CustomerID="1" CompanyName="xyz" />  
<Customer CustomerID="2" CompanyName="abc" />  
...  
```  
  
 Cuando la carga masiva XML se proporciona con el esquema descrito en los párrafos anteriores y con datos XML como entrada, procesa los nodos (elementos y atributos) en los datos de origen, tal y como se indica a continuación:  
  
-   La etiqueta de apertura del primer  **\<cliente >** elemento introduce ese elemento en el ámbito. Este nodo se asigna a la tabla Customers. Por lo tanto, la carga masiva XML genera un registro para la tabla Customers.  
  
-   En el esquema, todos los atributos de la  **\<cliente >** se asignan a las columnas de la tabla Customers. A medida que estos atributos entran en el ámbito, la carga masiva XML copia sus valores en el registro del cliente ya generado por el ámbito primario.  
  
-   Cuando la carga masiva XML alcanza la etiqueta de cierre para el  **\<cliente >** elemento, el elemento sale del ámbito. Esto hace que la carga masiva XML considere el registro completo y lo envíe a [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
 Carga masiva XML sigue este proceso para cada posteriores  **\<cliente >** elemento.  
  
> [!IMPORTANT]  
>  En este modelo, dado que se inserta un registro cuando se alcanza la etiqueta final (o cuando el nodo sale del ámbito), deberá definir todos los datos asociados al registro dentro del ámbito del nodo.  
  
## <a name="record-subset-and-the-key-ordering-rule"></a>Subconjunto de registros y la clave de ordenación de la regla  
 Cuando se especifica un esquema de asignación que usa `<sql:relationship>`, el término subconjunto hace referencia al conjunto de registros generado en el lado externo de la relación. En el ejemplo siguiente, los registros de CustOrder están en el lado externo, `<sql:relationship>`.  
  
 Por ejemplo, supongamos que una base de datos contiene las tablas siguientes:  
  
-   Cust (CustomerID, CompanyName, City)  
  
-   CustOrder (CustomerID, OrderID)  
  
 La columna CustomerID de la tabla CustOrder es una clave externa que hace referencia a la clave principal CustomerID de la tabla Cust.  
  
 Ahora, fíjese en la vista XML tal y como se especifica en el siguiente esquema XSD anotado. Este esquema usa `<sql:relationship>` para especificar la relación entre las tablas Cust y CustOrder.  
  
```  
<xsd:schema xmlns:xsd="http://www.w3.org/2001/XMLSchema"  
            xmlns:sql="urn:schemas-microsoft-com:mapping-schema">  
<xsd:annotation>  
  <xsd:appinfo>  
    <sql:relationship name="CustCustOrder"  
          parent="Cust"  
          parent-key="CustomerID"  
          child="CustOrder"  
          child-key="CustomerID" />  
  </xsd:appinfo>  
</xsd:annotation>  
  
  <xsd:element name="Customers" sql:relation="Cust" >  
   <xsd:complexType>  
     <xsd:sequence>  
       <xsd:element name="CustomerID"  type="xsd:integer" />  
       <xsd:element name="CompanyName" type="xsd:string" />  
       <xsd:element name="City"        type="xsd:string" />  
       <xsd:element name="Order"   
                          sql:relation="CustOrder"  
                          sql:relationship="CustCustOrder" >  
         <xsd:complexType>  
          <xsd:attribute name="OrderID" type="xsd:integer" />  
         </xsd:complexType>  
       </xsd:element>  
     </xsd:sequence>  
    </xsd:complexType>  
  </xsd:element>  
</xsd:schema>  
```  
  
 Los datos XML de ejemplo y los pasos para crear un ejemplo funcional se proporcionan a continuación.  
  
-   Cuando un  **\<cliente >** nodo de elemento en el archivo de datos XML entra en el ámbito, la carga masiva XML genera un registro de la tabla Cust. Carga masiva XML, a continuación, copia los valores de columna necesarios (CustomerID, CompanyName y City) de la  **\<CustomerID >**,  **\<CompanyName >** y el  **\<Ciudad >** los elementos secundarios como estos elementos entran en el ámbito.  
  
-   Cuando un  **\<orden >** nodo de elemento entra en el ámbito, la carga masiva XML genera un registro para la tabla CustOrder. Carga masiva XML copia el valor de la **OrderID** atributo para este registro. El valor necesario para la columna CustomerID se obtiene de la  **\<CustomerID >** elemento secundario de la  **\<cliente >** elemento. Carga masiva XML utiliza la información que se especifica en `<sql:relationship>` para obtener el valor de clave externa CustomerID para este registro, a menos que la **CustomerID** atributo se especificó en el  **\<orden >** elemento. La regla general es que si el elemento secundario especifica explícitamente un valor para el atributo de clave externa, la carga masiva XML usa ese valor y no obtiene el valor del elemento primario usando la etiqueta `<sql:relationship>` especificada. Como esto  **\<orden >** nodo de elemento sale del ámbito, la carga masiva XML envía el registro a [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] y, a continuación, procesa todas las posteriores  **\<orden >** nodos de elemento de la misma manera.  
  
-   Por último, el  **\<cliente >** nodo de elemento sale del ámbito. En ese momento, la carga masiva XML envía el registro del cliente a [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. La carga masiva XML sigue este proceso para todos los clientes subsiguientes del flujo de datos XML.  
  
 A continuación se indican dos observaciones sobre el esquema de asignación:  
  
-   Cuando el esquema cumple la regla de "contención" (por ejemplo, todos los datos que está asociados con el cliente y el orden se define dentro del ámbito del asociado  **\<cliente >** y  **\<Orden >** nodos element), la carga masiva se realiza correctamente.  
  
-   En la descripción de la  **\<cliente >** elemento, su elemento secundario se especifican elementos en el orden adecuado. En este caso, el  **\<CustomerID >** elemento secundario se ha especificado antes la  **\<orden >** elemento secundario. Esto significa que, en el archivo de datos de entrada XML, el  **\<CustomerID >** valor del elemento está disponible como la clave externa valor cuando la  **\<orden >** elemento entra en el ámbito. Primero se especifican los atributos de clave; ésta es la "regla de orden de clave".  
  
     Si especifica la  **\<CustomerID >** elemento secundario después de la  **\<orden >** elemento secundario, el valor no está disponible cuando la  **\< Orden >** elemento entra en el ámbito. Cuando el  **\</orden >** , a continuación, se lee la etiqueta de cierre, el registro de la tabla CustOrder se considera completando y se inserta en la tabla CustOrder con un valor NULL para la columna CustomerID, que no es el resultado deseado.  
  
#### <a name="to-create-a-working-sample"></a>Para crear un ejemplo funcional  
  
1.  Guarde el esquema que se proporciona en este ejemplo como SampleSchema.xml.  
  
2.  Cree estas tablas:  
  
    ```  
    CREATE TABLE Cust (  
                  CustomerID     int         PRIMARY KEY,  
                  CompanyName    varchar(20) NOT NULL,  
                  City           varchar(20) DEFAULT 'Seattle')  
    GO  
    CREATE TABLE CustOrder (  
                 OrderID        int         PRIMARY KEY,  
                 CustomerID     int         FOREIGN KEY REFERENCES                                          Cust(CustomerID))  
    GO  
    ```  
  
3.  Guarde los siguientes datos de entrada XML de ejemplo como SampleXMLData.xml:  
  
    ```  
    <ROOT>  
      <Customers>  
        <CustomerID>1111</CustomerID>  
        <CompanyName>Hanari Carnes</CompanyName>  
        <City>NY</City>   
        <Order OrderID="1" />  
        <Order OrderID="2" />  
      </Customers>  
  
      <Customers>  
        <CustomerID>1112</CustomerID>  
        <CompanyName>Toms Spezialitten</CompanyName>  
        <City>LA</City>  
        <Order OrderID="3" />  
      </Customers>  
      <Customers>  
        <CustomerID>1113</CustomerID>  
        <CompanyName>Victuailles en stock</CompanyName>  
        <Order OrderID="4" />  
    </Customers>  
    </ROOT>  
    ```  
  
4.  Para ejecutar la carga masiva XML, guarde y ejecute el ejemplo de [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Visual Basic Scripting Edition (VBScript) siguiente (BulkLoad.vbs):  
  
    ```  
    set objBL = CreateObject("SQLXMLBulkLoad.SQLXMLBulkload.4.0")  
    objBL.ConnectionString = "provider=SQLOLEDB;data source=localhost;database=tempdb;integrated security=SSPI"  
    objBL.ErrorLogFile = "c:\error.log"  
    objBL.CheckConstraints = True  
    objBL.Execute "c:\SampleSchema.xml", "c:\SampleXMLData.xml"  
    set objBL=Nothing  
    ```  
  
## <a name="exceptions-to-the-record-generation-rule"></a>Excepciones a la regla de generación de registros  
 La carga masiva XML no genera ningún registro para un nodo cuando entra en el ámbito si ese nodo es de tipo IDREF o IDREFS. Debe asegurarse de que se realice una descripción completa del registro en algún lugar del esquema. Las anotaciones `dt:type="nmtokens"` se omiten, al igual que el tipo IDREFS.  
  
 Por ejemplo, considere el siguiente esquema XSD que describe  **\<cliente >** y  **\<orden >** elementos. El  **\<cliente >** elemento incluye un **OrderList** atributo de tipo IDREFS. La etiqueta `<sql:relationship>` especifica la relación de uno a varios entre el cliente y lista de pedidos.  
  
 Éste es el esquema:  
  
```  
<xsd:schema xmlns:xsd="http://www.w3.org/2001/XMLSchema"  
            xmlns:sql="urn:schemas-microsoft-com:mapping-schema">  
<xsd:annotation>  
  <xsd:appinfo>  
    <sql:relationship name="CustCustOrder"  
                 parent="Cust"  
                 parent-key="CustomerID"  
                 child="CustOrder"  
                 child-key="CustomerID" />  
  </xsd:appinfo>  
</xsd:annotation>  
  
  <xsd:element name="Customers" sql:relation="Cust" >  
   <xsd:complexType>  
    <xsd:attribute name="CustomerID" type="xsd:integer" />  
    <xsd:attribute name="CompanyName" type="xsd:string" />  
    <xsd:attribute name="City" type="xsd:string" />  
    <xsd:attribute name="OrderList"   
                       type="xsd:IDREFS"   
                       sql:relation="CustOrder"   
                       sql:field="OrderID"  
                       sql:relationship="CustCustOrder" >  
    </xsd:attribute>  
  </xsd:complexType>  
 </xsd:element>  
  
  <xsd:element name="Order" sql:relation="CustOrder" >  
   <xsd:complexType>  
    <xsd:attribute name="OrderID" type="xsd:string" />  
    <xsd:attribute name="CustomerID" type="xsd:integer" />  
    <xsd:attribute name="OrderDate" type="xsd:date" />  
  </xsd:complexType>  
 </xsd:element>  
</xsd:schema>  
```  
  
 Puesto que la carga masiva omite los nodos de tipo IDREFS, no hay ninguna generación de registros cuando el **OrderList** nodo de atributo entra en el ámbito. Por lo tanto, si desea que los registros de pedidos se agreguen a la tabla Orders, debe describir estos pedidos en alguna parte del esquema. En este esquema, especificar el  **\<orden >** elemento garantiza que la carga masiva XML agrega los registros del pedido a la tabla Orders. El  **\<orden >** elemento describe todos los atributos que se necesitan para completar el registro de la tabla CustOrder.  
  
 Debe asegurarse de que el **CustomerID** y **OrderID** valores en el  **\<cliente >** elemento coinciden con los valores en el  **\<Orden >** elemento. Mantener la integridad referencial es responsabilidad suya.  
  
#### <a name="to-test-a-working-sample"></a>Para probar un ejemplo funcional  
  
1.  Cree estas tablas:  
  
    ```  
    CREATE TABLE Cust (  
                  CustomerID     int          PRIMARY KEY,  
                  CompanyName    varchar(20)  NOT NULL,  
                  City           varchar(20)  DEFAULT 'Seattle')  
    GO  
    CREATE TABLE CustOrder (  
                  OrderID        varchar(10) PRIMARY KEY,  
                  CustomerID     int         FOREIGN KEY REFERENCES                                          Cust(CustomerID),  
                  OrderDate      datetime DEFAULT '2000-01-01')  
    GO  
    ```  
  
2.  Guarde el esquema de asignación que se proporciona en este ejemplo como SampleSchema.xml.  
  
3.  Guarde los siguientes datos XML de ejemplo como SampleXMLData.xml:  
  
    ```  
    <ROOT>  
      <Customers CustomerID="1111" CompanyName="Sean Chai" City="NY"  
                 OrderList="Ord1 Ord2" />  
      <Customers CustomerID="1112" CompanyName="Dont Know" City="LA"  
                 OrderList="Ord3 Ord4" />  
      <Order OrderID="Ord1" CustomerID="1111" OrderDate="1999-01-01" />  
      <Order OrderID="Ord2" CustomerID="1111" OrderDate="1999-02-01" />  
      <Order OrderID="Ord3" CustomerID="1112" OrderDate="1999-03-01" />  
      <Order OrderID="Ord4" CustomerID="1112" OrderDate="1999-04-01" />  
    </ROOT>  
    ```  
  
4.  Para ejecutar la carga masiva XML, guarde y ejecute este ejemplo de VBScript (SampleVB.vbs):  
  
    ```  
    set objBL = CreateObject("SQLXMLBulkLoad.SQLXMLBulkload.4.0")  
    objBL.ConnectionString = "provider=SQLOLEDB;data source=localhost;database=tempdb;integrated security=SSPI"  
    objBL.ErrorLogFile = "c:\error.log"  
    objBL.CheckConstraints=True  
    objBL.Execute "c:\SampleSchema.xml", "c:\SampleXMLData.xml"  
    set objBL=Nothing  
    ```  
  
  