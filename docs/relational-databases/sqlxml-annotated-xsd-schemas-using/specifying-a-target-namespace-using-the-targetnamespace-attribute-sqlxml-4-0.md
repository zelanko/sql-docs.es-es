---
title: Especificar un espacio de nombres de destino con targetNamespace (SQLXML)
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.technology: xml
ms.topic: reference
helpviewer_keywords:
- namespaces [SQLXML], annotated XSD schemas
- targetNamespace attribute
- XSD schemas [SQLXML], target namespaces
- annotated XSD schemas, target namespaces
- xsd:targetNamespace
- attributeFormDefault attribute
- elementFormDefault attribute
- target namespaces [SQLXML]
ms.assetid: f3df9877-6672-4444-8245-2670063c9310
author: MightyPen
ms.author: genemi
ms.reviewer: ''
ms.custom: seo-lt-2019
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 39469073a8affe82ee5231a71676d7046f712f9f
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/27/2020
ms.locfileid: "75257361"
---
# <a name="specifying-a-target-namespace-using-the-targetnamespace-attribute-sqlxml-40"></a>Especificar un espacio de nombres de destino mediante el atributo targetNamespace (SQLXML 4.0)
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  Al escribir esquemas XSD, puede usar el atributo **targetNamespace** de XSD para especificar un espacio de nombres de destino. En este tema se describe cómo funcionan los atributos XSD **targetNamespace**, **elementFormDefault**y **attributeFormDefault** , cómo afectan a la instancia XML que se genera y cómo se especifican las consultas XPath con espacios de nombres.  
  
 Puede usar el atributo **xsd: targetNamespace** para colocar elementos y atributos del espacio de nombres predeterminado en un espacio de nombres diferente. También puede especificar si los elementos y los atributos del esquema declarados localmente deben estar certificados por un espacio de nombres, ya sea explícitamente mediante un prefijo o implícitamente de forma predeterminada. Puede usar los atributos **elementFormDefault** y **attributeFormDefault** en el ** \<elemento xsd: Schema>** para especificar globalmente la calificación de elementos y atributos locales, o puede usar el atributo **Form** para especificar elementos y atributos individuales por separado.  
  
## <a name="examples"></a>Ejemplos  
 Para crear muestras funcionales mediante los ejemplos siguientes, debe cumplir determinados requisitos. Para obtener más información, vea [Requirements for Running SQLXML examples](../../relational-databases/sqlxml/requirements-for-running-sqlxml-examples.md).  
  
### <a name="a-specifying-a-target-namespace"></a>A. Especificar un espacio de nombres de destino  
 El siguiente esquema XSD especifica un espacio de nombres de destino mediante el atributo **xsd: targetNamespace** . El esquema también establece los valores de atributo **elementFormDefault** y **attributeFormDefault** en **"Unqualified"** (el valor predeterminado de estos atributos). Se trata de una declaración global que afecta a todos los elementos locales (**\<Order>** del esquema) y atributos (**CustomerID**, **ContactName**y **OrderID** en el esquema).  
  
```  
<xsd:schema xmlns:xsd="http://www.w3.org/2001/XMLSchema"  
            xmlns:sql="urn:schemas-microsoft-com:mapping-schema"  
            xmlns:CO="urn:MyNamespace"   
            targetNamespace="urn:MyNamespace" >  
<xsd:annotation>  
  <xsd:appinfo>  
    <sql:relationship name="CustOrders"  
          parent="Sales.Customer"  
          parent-key="CustomerID"  
          child="Sales.SalesOrderHeader"  
          child-key="CustomerID" />  
  </xsd:appinfo>  
</xsd:annotation>  
  
  <xsd:element name="Customer"   
               sql:relation="Sales.Customer"   
               type="CO:CustomerType" />  
  
  <xsd:complexType name="CustomerType" >  
     <xsd:sequence>  
        <xsd:element name="Order"   
                     sql:relation="Sales.SalesOrderHeader"  
                     sql:relationship="CustOrders"  
                     type="CO:OrderType" />  
     </xsd:sequence>  
        <xsd:attribute name="CustomerID"   type="xsd:string" />   
        <xsd:attribute name="SalesPersonID"  type="xsd:string" />  
  </xsd:complexType>  
  <xsd:complexType name="OrderType" >  
     <xsd:attribute name="SalesOrderID" type="xsd:integer" />  
     <xsd:attribute name="CustomerID" type="xsd:string" />  
  </xsd:complexType>  
</xsd:schema>  
```  
  
 En el esquema:  
  
-   Las declaraciones de tipos **CustomerType** y **OrderType** son globales y, por lo tanto, se incluyen en el espacio de nombres de destino del esquema. Como resultado, cuando se hace referencia a estos tipos en la declaración del ** \<elemento Customer>** y su ** \<orden>** elemento secundario, se especifica un prefijo que está asociado al espacio de nombres de destino.  
  
-   El ** \<elemento Customer>** también se incluye en el espacio de nombres de destino del esquema porque es un elemento global del esquema.  
  
 Ejecute la siguiente consulta XPath en el esquema:  
  
```  
(/CO:Customer[@CustomerID=1)   
```  
  
 La consulta XPath genera este documento de instancia (solo se muestran algunos pedidos):  
  
```  
<ROOT xmlns:sql="urn:schemas-microsoft-com:xml-sql">  
  <y0:Customer xmlns:y0="urn:MyNamespace"   
      CustomerID="ALFKI" ContactName="Maria Anders">  
        <Order CustomerID="ALFKI" OrderID="10643" />   
        <Order CustomerID="ALFKI" OrderID="10692" />   
        ...  
  </y0:Customer>  
  </ROOT>  
```  
  
 Este documento de instancia define el espacio de nombres urn: myNameSpace y le asocia un prefijo (Y0). El prefijo solo se aplica al elemento global ** \<Customer>** . (El elemento es global porque se declara como un elemento secundario del ** \<elemento xsd: Schema>** en el esquema).  
  
 El prefijo no se aplica a los elementos y atributos locales porque el valor de los atributos **elementFormDefault** y **attributeFormDefault** se establece en **"Unqualified"** en el esquema. Tenga en cuenta que el ** \<elemento Order>** es local porque su declaración aparece como un elemento secundario del elemento ** \<>complexType** que define el elemento de ** \<>CustomerType** . Del mismo modo, los atributos (**CustomerID**, **OrderID**y **ContactName**) son locales, no globales.  
  
##### <a name="to-create-a-working-sample-of-this-schema"></a>Para crear un ejemplo funcional de este esquema  
  
1.  Copie el código de esquema anterior y péguelo en un archivo de texto. Guarde el archivo como targetNameSpace.xml.  
  
2.  Copie la plantilla siguiente y péguela en un archivo de texto. Guarde el archivo como targetNameSpaceT.xml en el mismo directorio donde guardó targetNamespace.xml.  
  
    ```  
    <ROOT xmlns:sql="urn:schemas-microsoft-com:xml-sql">  
      <sql:xpath-query mapping-schema="targetNamespace.xml"  
                       xmlns:CO="urn:MyNamespace" >  
        /CO:Customer[@CustomerID=1]  
      </sql:xpath-query>  
    </ROOT>  
    ```  
  
     La consulta XPath de la plantilla devuelve el ** \<elemento Customer>** del cliente con un CustomerID de 1. Observe que la consulta XPath especifica el prefijo de espacio de nombres del elemento en la consulta y no del atributo. (Los atributos locales, tal y como se especifican en el esquema, no se certifican).  
  
     La ruta de acceso al directorio especificada para el esquema de asignación (targetNamespace.xml) es una ubicación relativa con respecto al directorio donde se guarda la plantilla. También puede especificarse una ruta de acceso absoluta como, por ejemplo:  
  
    ```  
    mapping-schema="C:\MyDir\targetNamepsace.xml"  
    ```  
  
3.  Cree y use el script de prueba SQLXML 4.0 (Sqlxml4test.vbs) para ejecutar la plantilla.  
  
     Para obtener más información, vea [usar ado para ejecutar consultas SQLXML](../../relational-databases/sqlxml/using-ado-to-execute-sqlxml-4-0-queries.md).  
  
 Si el esquema especifica atributos **elementFormDefault** y **attributeFormDefault** con el valor **"Qualified"**, el documento de instancia tendrá todos los elementos y atributos locales calificados. Puede cambiar el esquema anterior para incluir estos atributos en el ** \<elemento xsd: Schema>** y volver a ejecutar la plantilla. Como los atributos están ahora certificados en la instancia, la consulta XPath cambiará e incluirá el prefijo de espacio de nombres.  
  
 Esta es la consulta XPath modificada:  
  
```  
/CO:Customer[@CO:CustomerID=1]  
```  
  
 Este el documento XML devuelto:  
  
```  
<ROOT xmlns:sql="urn:schemas-microsoft-com:xml-sql">  
   <y0:Customer xmlns:y0="urn:MyNamespace" CustomerID="1" SalesPersonID="280">  
      <Order SalesOrderID="43860" CustomerID="1" />   
      <Order SalesOrderID="44501" CustomerID="1" />   
      <Order SalesOrderID="45283" CustomerID="1" />   
      <Order SalesOrderID="46042" CustomerID="1" />   
   </y0:Customer>  
</ROOT>  
```  
  
  
