---
title: Especificar un Namespace de destino mediante el atributo (SQLXML 4.0) targetNamespace | Documentos de Microsoft
ms.custom: 
ms.date: 03/16/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: sqlxml
ms.reviewer: 
ms.suite: sql
ms.technology:
- dbe-xml
ms.tgt_pltfrm: 
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
caps.latest.revision: 
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 9b0b325cea845e82519752b04591c2c7724b1acf
ms.sourcegitcommit: 37f0b59e648251be673389fa486b0a984ce22c81
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/12/2018
---
# <a name="specifying-a-target-namespace-using-the-targetnamespace-attribute-sqlxml-40"></a>Especificar un espacio de nombres de destino mediante el atributo targetNamespace (SQLXML 4.0)
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
Crear esquemas XSD, puede utilizar el esquema XSD **targetNamespace** atributo para especificar un espacio de nombres de destino. Este tema se describe cómo el XSD **targetNamespace**, **elementFormDefault**, y **attributeFormDefault** funcionan los atributos, cómo afectan a la instancia XML que es genera, y cómo se especifican consultas XPath con espacios de nombres.  
  
 Puede usar el **xsd: targetNamespace** atributo para colocar elementos y atributos del espacio de nombres predeterminado en otro espacio de nombres. También puede especificar si los elementos y los atributos del esquema declarados localmente deben estar certificados por un espacio de nombres, ya sea explícitamente mediante un prefijo o implícitamente de forma predeterminada. Puede usar el **elementFormDefault** y **attributeFormDefault** atributos en el  **\<xsd: schema >** elemento para especificar globalmente la calificación de locales elementos y atributos o puede usar el **formulario** atributo para especificar los atributos y elementos individuales por separado.  
  
## <a name="examples"></a>Ejemplos  
 Para crear muestras funcionales mediante los ejemplos siguientes, debe cumplir determinados requisitos. Para obtener más información, consulte [requisitos para ejecutar los ejemplos de SQLXML](../../relational-databases/sqlxml/requirements-for-running-sqlxml-examples.md).  
  
### <a name="a-specifying-a-target-namespace"></a>A. Especificar un espacio de nombres de destino  
 El siguiente esquema XSD especifica un espacio de nombres de destino mediante el **xsd: targetNamespace** atributo. El esquema establece también el **elementFormDefault** y **attributeFormDefault** valores de atributo **"unqualified"** (el valor predeterminado para estos atributos). Esto es una declaración global y afecta a todos los elementos locales (**\<orden >** en el esquema) y atributos (**CustomerID**, **ContactName**y  **OrderID** en el esquema).  
  
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
  
-   El **CustomerType** y **OrderType** declaraciones de tipos son globales y, por lo tanto, se incluyen en el espacio de nombres de destino del esquema. Como resultado, cuando estos tipos se hace referencia en la declaración de  **\<cliente >** elemento y su  **\<orden >** elemento secundario, se especifica un prefijo que está asociado con el espacio de nombres de destino.  
  
-   El  **\<cliente >** elemento también se incluye en el espacio de nombres de destino del esquema porque es un elemento global en el esquema.  
  
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
  
 Este documento de instancia define el espacio de nombres urn: MyNamespace y asocia un prefijo (y0) a él. El prefijo se aplica solo a la  **\<cliente >** elemento global. (El elemento es global porque se declara como un elemento secundario de  **\<xsd: schema >** elemento en el esquema.)  
  
 El prefijo no se aplica a los elementos y atributos locales porque el valor de **elementFormDefault** y **attributeFormDefault** atributos se establece en **"unqualified"**en el esquema. Tenga en cuenta que la  **\<orden >** elemento es local porque su declaración aparece como un elemento secundario de la  **\<complexType >** elemento que define la  **\< CustomerType >** elemento. Asimismo, los atributos (**CustomerID**, **OrderID**, y **ContactName**) son locales y no globales.  
  
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
  
     La consulta XPath de la plantilla devuelve el  **\<cliente >** elemento para el cliente con un CustomerID de 1. Observe que la consulta XPath especifica el prefijo de espacio de nombres del elemento en la consulta y no del atributo. (Los atributos locales, tal y como se especifican en el esquema, no se certifican).  
  
     La ruta de acceso al directorio especificada para el esquema de asignación (targetNamespace.xml) es una ubicación relativa con respecto al directorio donde se guarda la plantilla. También puede especificarse una ruta de acceso absoluta como, por ejemplo:  
  
    ```  
    mapping-schema="C:\MyDir\targetNamepsace.xml"  
    ```  
  
3.  Cree y use el script de prueba SQLXML 4.0 (Sqlxml4test.vbs) para ejecutar la plantilla.  
  
     Para obtener más información, consulte [utilizar ADO para ejecutar consultas SQLXML](../../relational-databases/sqlxml/using-ado-to-execute-sqlxml-4-0-queries.md).  
  
 Si el esquema especifica **elementFormDefault** y **attributeFormDefault** atributos con valor **"qualified"**, el documento de instancia tendrá todos de la variable local califican elementos y atributos. Puede cambiar el esquema anterior para incluir estos atributos en el  **\<xsd: schema >** elemento y ejecutar la plantilla de nuevo. Como los atributos están ahora certificados en la instancia, la consulta XPath cambiará e incluirá el prefijo de espacio de nombres.  
  
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
  
  
