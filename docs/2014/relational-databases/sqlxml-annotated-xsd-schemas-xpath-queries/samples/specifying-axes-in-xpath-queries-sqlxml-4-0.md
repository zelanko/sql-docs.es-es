---
title: Especificar ejes en consultas XPath (SQLXML 4,0) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: xml
ms.topic: reference
helpviewer_keywords:
- XPath queries [SQLXML], axes
- context node [SQLXML]
- attribute axis [SQLXML]
- axis [SQLXML]
- child axis
- parent axis
- axes [SQLXML]
ms.assetid: d17b8278-da58-4576-95b4-7a92772566d8
author: rothja
ms.author: jroth
ms.openlocfilehash: 89e63d07d362e6d810db746fa5828ad07aa5870c
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/18/2020
ms.locfileid: "85062846"
---
# <a name="specifying-axes-in-xpath-queries-sqlxml-40"></a>Especificar ejes en consultas XPath (SQLXML 4.0)
  Los ejemplos siguientes muestran cómo se especifican los ejes en las consultas XPath.  
  
 Las consultas XPath de estos ejemplos se especifican en el esquema de asignación que se incluye en SampleSchema1.xml. Para obtener información acerca de este esquema de ejemplo, vea [ejemplo de esquema XSD anotado para los ejemplos de XPath &#40;SQLXML 4,0&#41;](sample-annotated-xsd-schema-for-xpath-examples-sqlxml-4-0.md).  
  
## <a name="examples"></a>Ejemplos  
  
### <a name="a-retrieve-child-elements-of-the-context-node"></a>A. Recuperar elementos secundarios del nodo de contexto  
 La consulta XPath siguiente selecciona todos los **\<Contact>** elementos secundarios del nodo de contexto:  
  
```  
/child::Contact  
```  
  
 En la consulta, `child` es el eje y `Contact` es la prueba de nodo (true si `Contact` es un **\<element>** nodo, porque \<element> es el tipo de nodo principal asociado al `child` eje).  
  
 El eje `child` es el valor predeterminado. Por tanto, la consulta puede escribirse como:  
  
```  
/Contact  
```  
  
##### <a name="to-test-the-xpath-query-against-the-mapping-schema"></a>Para probar la consulta XPath en el esquema de asignación  
  
1.  Copie el [código de esquema de ejemplo](sample-annotated-xsd-schema-for-xpath-examples-sqlxml-4-0.md) y péguelo en un archivo de texto. Guarde el archivo como SampleSchema1.xml.  
  
2.  Cree la siguiente plantilla (XPathAxesSampleA.xml) y guárdela en el mismo directorio en el que esté guardado el archivo SampleSchema1.xml.  
  
    ```  
    <ROOT xmlns:sql="urn:schemas-microsoft-com:xml-sql">  
      <sql:xpath-query mapping-schema="SampleSchema1.xml">  
        /Contact  
      </sql:xpath-query>  
    </ROOT>  
    ```  
  
     La ruta de acceso al directorio especificada para el esquema de asignación (SampleSchema1.xml) es relativa al directorio donde se guarda la plantilla. También puede especificarse una ruta de acceso absoluta como, por ejemplo:  
  
    ```  
    mapping-schema="C:\MyDir\SampleSchema1.xml"  
    ```  
  
3.  Cree y use el script de prueba SQLXML 4.0 (Sqlxml4test.vbs) para ejecutar la plantilla.  
  
     Para obtener más información, vea [usar ado para ejecutar consultas SQLXML 4,0](../../sqlxml/using-ado-to-execute-sqlxml-4-0-queries.md).  
  
 Este es el conjunto parcial de resultados de ejecución de la plantilla:  
  
```  
<ROOT xmlns:sql="urn:schemas-microsoft-com:xml-sql">   
  <Contact ContactID="1" LastName="Achong" FirstName="Gustavo" Title="Mr." />   
  <Contact ContactID="2" LastName="Abel" FirstName="Catherine" Title="Ms." />   
  <Contact ContactID="3" LastName="Abercrombie" FirstName="Kim" Title="Ms." />   
  <Contact ContactID="4" LastName="Acevedo" FirstName="Humberto" Title="Sr." />  
  ...  
</ROOT>  
```  
  
### <a name="b-retrieve-grandchildren-of-the-context-node"></a>B. Recuperar descendientes del nodo de contexto  
 La consulta XPath siguiente selecciona todos los elementos **\<Order>** secundarios del elemento **\<Customer>** secundarios del nodo de contexto:  
  
```  
/child::Customer/child::Order  
```  
  
 En la consulta, `child` es el eje y `Customer` y `Order` son las pruebas de nodo (estas pruebas de nodo son verdaderas si Customer y Order son **\<element>** nodos, porque el **\<element>** nodo es el nodo principal del `child` eje). Para cada nodo que coincide con **\<Customer>** , los nodos que coinciden con **\<Orders>** se agregan al resultado. Solo **\<Order>** se devuelve en el conjunto de resultados.  
  
 El eje `child` es el valor predeterminado. Por lo tanto, la consulta puede especificarse como:  
  
```  
/Customer/Order  
```  
  
##### <a name="to-test-the-xpath-query-against-the-mapping-schema"></a>Para probar la consulta XPath en el esquema de asignación  
  
1.  Copie el [código de esquema de ejemplo](sample-annotated-xsd-schema-for-xpath-examples-sqlxml-4-0.md) y péguelo en un archivo de texto. Guarde el archivo como SampleSchema1.xml.  
  
2.  Cree la plantilla siguiente (XPathAxesSampleB.xml) y guárdela en el directorio donde:  
  
    ```  
    <ROOT xmlns:sql="urn:schemas-microsoft-com:xml-sql">  
      <sql:xpath-query mapping-schema="SampleSchema1.xml">  
        /Customer/Order  
      </sql:xpath-query>  
    </ROOT>  
    ```  
  
     La ruta de acceso al directorio especificada para el esquema de asignación (SampleSchema1.xml) es relativa al directorio donde se guarda la plantilla. También puede especificarse una ruta de acceso absoluta como, por ejemplo:  
  
    ```  
    mapping-schema="C:\MyDir\SampleSchema1.xml"  
    ```  
  
3.  Cree y use el script de prueba SQLXML 4.0 (Sqlxml4test.vbs) para ejecutar la plantilla.  
  
     Para obtener más información, vea [usar ado para ejecutar consultas SQLXML 4,0](../../sqlxml/using-ado-to-execute-sqlxml-4-0-queries.md).  
  
 Este es el conjunto parcial de resultados de ejecución de la plantilla:  
  
```  
<ROOT xmlns:sql="urn:schemas-microsoft-com:xml-sql">  
  <Order SalesOrderID="Ord-43860" SalesPersonID="280"   
         OrderDate="2001-08-01T00:00:00"   
         DueDate="2001-08-13T00:00:00"   
         ShipDate="2001-08-08T00:00:00">  
  <OrderDetail ProductID="Prod-729" UnitPrice="226.8571"   
               OrderQty="1" UnitPriceDiscount="0" />   
  <OrderDetail ProductID="Prod-732" UnitPrice="440.1742"   
               OrderQty="1" UnitPriceDiscount="0" />   
  <OrderDetail ProductID="Prod-738" UnitPrice="220.2496"   
               OrderQty="1" UnitPriceDiscount="0" />   
  <OrderDetail ProductID="Prod-753" UnitPrice="2576.3544"   
               OrderQty="2" UnitPriceDiscount="0" />   
  <OrderDetail ProductID="Prod-756" UnitPrice="1049.7528"   
               OrderQty="1" UnitPriceDiscount="0" />   
  <OrderDetail ProductID="Prod-758" UnitPrice="1049.7528"   
               OrderQty="2" UnitPriceDiscount="0" />   
  <OrderDetail ProductID="Prod-761" UnitPrice="503.3507"   
               OrderQty="2" UnitPriceDiscount="0" />   
  <OrderDetail ProductID="Prod-762" UnitPrice="503.3507"   
               OrderQty="1" UnitPriceDiscount="0" />   
  <OrderDetail ProductID="Prod-763" UnitPrice="503.3507"   
               OrderQty="1" UnitPriceDiscount="0" />   
  <OrderDetail ProductID="Prod-765" UnitPrice="503.3507"   
               OrderQty="2" UnitPriceDiscount="0" />   
  <OrderDetail ProductID="Prod-768" UnitPrice="503.3507"   
               OrderQty="1" UnitPriceDiscount="0" />   
  <OrderDetail ProductID="Prod-770" UnitPrice="503.3507"   
               OrderQty="1" UnitPriceDiscount="0" />   
  </Order>  
   ...  
</ROOT>  
```  
  
 Si la consulta XPath se especifica como `Customer/Order/OrderDetail` , de cada nodo que coincida con **\<Customer>** la consulta navega a sus **\<Order>** elementos. Y para cada nodo coincidente **\<Order>** , la consulta agrega los nodos **\<OrderDetail>** al resultado. Solo **\<OrderDetail>** se devuelve en el conjunto de resultados.  
  
### <a name="c-use--to-specify-the-parent-axis"></a>C. Usar . para especificar el eje primario  
 La consulta siguiente recupera todos los **\<Order>** elementos con un elemento primario **\<Customer>** con un valor de atributo **CustomerID** de 1. La consulta usa el `child` eje en el predicado para buscar el elemento primario del **\<Order>** elemento.  
  
```  
/child::Customer/child::Order[../@CustomerID="1"]  
```  
  
 El eje `child` es el eje predeterminado. Por lo tanto, la consulta puede especificarse como:  
  
```  
/Customer/Order[../@CustomerID="1"]  
```  
  
 La consulta XPath es equivalente a:  
  
```  
/Customer[@CustomerID="1"]/Order.  
```  
  
> [!NOTE]  
>  La consulta XPath `/Order[../@CustomerID="1"]` devolverá un error porque no hay ningún elemento primario de **\<Order>** . Aunque puede haber elementos en el esquema de asignación que contengan **\<Order>** , el XPath no comenzó en ninguno de ellos; por lo tanto, **\<Order>** se considera que es el tipo de elemento de nivel superior del documento.  
  
##### <a name="to-test-the-xpath-query-against-the-mapping-schema"></a>Para probar la consulta XPath en el esquema de asignación  
  
1.  Copie el [código de esquema de ejemplo](sample-annotated-xsd-schema-for-xpath-examples-sqlxml-4-0.md) y péguelo en un archivo de texto. Guarde el archivo como SampleSchema1.xml.  
  
2.  Cree la plantilla siguiente (XPathAxesSampleC.xml) y guárdela en el directorio donde:  
  
    ```  
    <ROOT xmlns:sql="urn:schemas-microsoft-com:xml-sql">  
      <sql:xpath-query mapping-schema="SampleSchema1.xml">  
        /Customer/Order[../@CustomerID="1"]  
      </sql:xpath-query>  
    </ROOT>  
    ```  
  
     La ruta de acceso al directorio especificada para el esquema de asignación (SampleSchema1.xml) es relativa al directorio donde se guarda la plantilla. También puede especificarse una ruta de acceso absoluta como, por ejemplo:  
  
    ```  
    mapping-schema="C:\MyDir\SampleSchema1.xml"  
    ```  
  
3.  Cree y use el script de prueba SQLXML 4.0 (Sqlxml4test.vbs) para ejecutar la plantilla.  
  
     Para obtener más información, vea [usar ado para ejecutar consultas SQLXML 4,0](../../sqlxml/using-ado-to-execute-sqlxml-4-0-queries.md).  
  
 Este es el conjunto parcial de resultados de ejecución de la plantilla:  
  
```  
<ROOT xmlns:sql="urn:schemas-microsoft-com:xml-sql">  
  <Order SalesOrderID="Ord-43860" SalesPersonID="280"   
         OrderDate="2001-08-01T00:00:00"   
         DueDate="2001-08-13T00:00:00"   
         ShipDate="2001-08-08T00:00:00">  
  <OrderDetail ProductID="Prod-729" UnitPrice="226.8571"   
               OrderQty="1" UnitPriceDiscount="0" />   
  <OrderDetail ProductID="Prod-732" UnitPrice="440.1742"   
               OrderQty="1" UnitPriceDiscount="0" />   
  <OrderDetail ProductID="Prod-738" UnitPrice="220.2496"   
               OrderQty="1" UnitPriceDiscount="0" />   
  <OrderDetail ProductID="Prod-753" UnitPrice="2576.3544"   
               OrderQty="2" UnitPriceDiscount="0" />   
  <OrderDetail ProductID="Prod-756" UnitPrice="1049.7528"   
               OrderQty="1" UnitPriceDiscount="0" />   
  <OrderDetail ProductID="Prod-758" UnitPrice="1049.7528"   
               OrderQty="2" UnitPriceDiscount="0" />   
  <OrderDetail ProductID="Prod-761" UnitPrice="503.3507"   
               OrderQty="2" UnitPriceDiscount="0" />   
  <OrderDetail ProductID="Prod-762" UnitPrice="503.3507"   
               OrderQty="1" UnitPriceDiscount="0" />   
  <OrderDetail ProductID="Prod-763" UnitPrice="503.3507"   
               OrderQty="1" UnitPriceDiscount="0" />   
  <OrderDetail ProductID="Prod-765" UnitPrice="503.3507"   
               OrderQty="2" UnitPriceDiscount="0" />   
  <OrderDetail ProductID="Prod-768" UnitPrice="503.3507"   
               OrderQty="1" UnitPriceDiscount="0" />   
  <OrderDetail ProductID="Prod-770" UnitPrice="503.3507"   
               OrderQty="1" UnitPriceDiscount="0" />   
  </Order>  
   ...  
</Order>  
</ROOT>  
```  
  
### <a name="d-specify-the-attribute-axis"></a>D. Especificar el eje de atributo  
 La consulta XPath siguiente selecciona todos los **\<Customer>** elementos secundarios del nodo de contexto con un valor de atributo **CustomerID** de 1:  
  
```  
/child::Customer[attribute::CustomerID="1"]  
```  
  
 En el predicado `attribute::CustomerID` , `attribute` es el eje y `CustomerID` es la prueba de nodo (si `CustomerID` es un atributo, la prueba de nodo es true, porque el **\<attribute>** nodo es el nodo principal del `attribute` eje).  
  
 Se puede especificar un acceso directo al eje `attribute` (@) y, puesto que el eje `child` es el eje predeterminado, puede omitirse en la consulta:  
  
```  
/Customer[@CustomerID="1"]  
```  
  
##### <a name="to-test-the-xpath-query-against-the-mapping-schema"></a>Para probar la consulta XPath en el esquema de asignación  
  
1.  Copie el [código de esquema de ejemplo](sample-annotated-xsd-schema-for-xpath-examples-sqlxml-4-0.md) y péguelo en un archivo de texto. Guarde el archivo como SampleSchema1.xml.  
  
2.  Cree la siguiente plantilla (XPathAxesSampleD.xml) y guárdela en el mismo directorio en el que esté guardado el archivo SampleSchema1.xml.  
  
    ```  
    <ROOT xmlns:sql="urn:schemas-microsoft-com:xml-sql">  
      <sql:xpath-query mapping-schema="SampleSchema1.xml">  
        child::Customer[attribute::CustomerID="1"]  
      </sql:xpath-query>  
    </ROOT>  
    ```  
  
     La ruta de acceso al directorio especificada para el esquema de asignación (SampleSchema1.xml) es relativa al directorio donde se guarda la plantilla. También puede especificarse una ruta de acceso absoluta como, por ejemplo:  
  
    ```  
    mapping-schema="C:\MyDir\SampleSchema1.xml"  
    ```  
  
3.  Cree y use el script de prueba SQLXML 4.0 (Sqlxml4test.vbs) para ejecutar la plantilla.  
  
     Para obtener más información, vea [usar ado para ejecutar consultas SQLXML 4,0](../../sqlxml/using-ado-to-execute-sqlxml-4-0-queries.md).  
  
 Este es el conjunto parcial de resultados de ejecución de la plantilla:  
  
```  
<ROOT xmlns:sql="urn:schemas-microsoft-com:xml-sql">  
  <Customer CustomerID="1" SalesPersonID="280"   
            TerritoryID="1" AccountNumber="1"   
            CustomerType="S" Orders="Ord-43860 Ord-44501 Ord-45283 Ord-46042">  
    <Order SalesOrderID="Ord-43860" SalesPersonID="280"   
           OrderDate="2001-08-01T00:00:00"   
           DueDate="2001-08-13T00:00:00"   
           ShipDate="2001-08-08T00:00:00">  
       <OrderDetail ProductID="Prod-729" UnitPrice="226.8571"   
                    OrderQty="1" UnitPriceDiscount="0" />   
       <OrderDetail ProductID="Prod-732" UnitPrice="440.1742"   
                    OrderQty="1" UnitPriceDiscount="0" />   
       <OrderDetail ProductID="Prod-738" UnitPrice="220.2496"   
                    OrderQty="1" UnitPriceDiscount="0" />   
      ...   
    </Order>  
   ...  
  </Customer>  
</ROOT>  
```  
  
  
