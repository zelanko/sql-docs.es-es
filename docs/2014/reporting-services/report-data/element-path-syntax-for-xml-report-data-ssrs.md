---
title: Sintaxis de ruta de acceso de elemento para datos de informe XML (SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- reporting-services-native
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- ElementPath syntax
- XML [Reporting Services], data retrieval
ms.assetid: 07bd7a4e-fd7a-4a72-9344-3258f7c286d1
caps.latest.revision: 42
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: bcb0036fbf6d0c3f5af18d044d389bc8673cd5ce
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/02/2018
ms.locfileid: "37238509"
---
# <a name="element-path-syntax-for-xml-report-data-ssrs"></a>Sintaxis de ruta de acceso de elemento para datos de informe XML (SSRS)
  En el Diseñador de informes, se define una ruta de acceso de elemento que distingue mayúsculas de minúsculas para especificar los datos que se van a utilizar en un informe desde un origen de datos XML. Una ruta de acceso de elemento indica cómo se deben recorrer los nodos jerárquicos XML y sus atributos en el origen de datos XML. Para utilizar la ruta de acceso de elemento predeterminada, mantenga vacía la consulta del conjunto de datos o el elemento XML `ElementPath` del elemento XML `Query`. Cuando se recuperan datos del origen de datos XML, los nodos de elemento que tienen valores de texto y atributos de nodo de elemento se convierten en columnas en el conjunto de resultados. Los valores de los nodos y atributos pasan a ser datos de fila al ejecutar la consulta. Las columnas aparecen como la colección de campos del conjunto de datos en el panel Datos de informe. En este tema se describe la sintaxis de la ruta de acceso de elemento.  
  
> [!NOTE]  
>  La sintaxis de ruta de acceso de elemento es independiente del espacio de nombres. Para usar espacios de nombres en una ruta de acceso de elemento, use la sintaxis de consulta XML que incluye un archivo XML `ElementPath` descrito en [sintaxis de consulta XML para datos de informe XML &#40;SSRS&#41;](report-data-ssrs.md).  
  
 En la tabla siguiente se describen las convenciones que se aplican para definir una ruta de acceso de elemento.  
  
|Convención|Se usa para|  
|----------------|--------------|  
|**Negrita**|Texto que debe escribirse exactamente como se muestra.|  
|&#124; (barra vertical)|Separa los elementos de sintaxis. Solo se puede elegir uno de los elementos.|  
|`[ ] (brackets)`|Elementos opcionales de sintaxis. No escriba los corchetes.|  
|**{ }** (llaves)|Delimita los parámetros de los elementos de sintaxis.|  
|[**,**…*n*]|Indica que el elemento anterior puede repetirse *n* veces. Cada repetición se separa de la siguiente con una coma.|  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
Element path ::=  
    ElementNode[/Element path]  
ElementNode ::=  
    XMLName[(Encoding)][{[FieldList]}]  
XMLName ::=  
    [NamespacePrefix:]XMLLocalName  
Encoding ::=  
        HTMLEncoded | Base64Encoded  
FieldList ::=  
    Field[,FieldList]  
Field ::=  
    Attribute | Value | Element | ElementNode  
Attribute ::=  
        @XMLName[(Type)]  
Value ::=  
        @[(Type)]  
Element ::=  
    XMLName[(Type)]  
Type ::=  
        String | Integer | Boolean | Float | Decimal | Date | XML   
NamespacePrefix ::=  
    Identifier that specifies the namespace.  
XMLLocalName :: =  
    Identifier in the XML tag.   
```  
  
## <a name="remarks"></a>Notas  
 En la tabla siguiente se resumen los términos de ruta de acceso de elemento. Los ejemplos de la tabla hacen referencia al documento XML de ejemplo Customers.xml, que se incluye en la sección Ejemplos de este tema.  
  
> [!NOTE]  
>  En las etiquetas XML se distingue entre mayúsculas y minúsculas. Cuando se especifica ElementNode en la ruta de acceso de elemento, debe haber una correspondencia exacta con las etiquetas XML del origen de datos.  
  
|Término|Definición|  
|----------|----------------|  
|Ruta de acceso de elemento|Define la secuencia de nodos que deben recorrerse en el documento XML para recuperar los datos de campo de un conjunto de datos con un origen de datos XML.|  
|`ElementNode`|Nodo XML en el documento XML. Los nodos se designan mediante etiquetas y existen en una relación jerárquica con otros nodos. Por ejemplo, \<Customers> es el nodo de elemento raíz. \<Customer> es un subelemento de \<Customers>.|  
|`XMLName`|Nombre del nodo. Por ejemplo, el nombre del nodo Customers es Customers. Un `XMLName` puede agregarse como prefijo un identificador de espacio de nombres al nombre único a cada nodo.|  
|`Encoding`|Indica que el `Value` para este elemento está codificado XML y debe descodificarse e incluirse como un subelemento de este elemento.|  
|`FieldList`|Define el conjunto de elementos y atributos que se van a utilizar para recuperar datos.<br /><br /> Si no se especifica, se usan como campos todos los atributos y subelementos. Si se especifica la lista de campos vacíos (**{}**), no se usará ningún campo de este nodo.<br /><br /> Un `FieldList` no puede contener tanto un `Value` y un `Element` o `ElementNode`.|  
|`Field`|Especifica los datos que se recuperan como campo de conjunto de datos.|  
|`Attribute`|Un par de nombre y valor dentro de la `ElementNode`. Por ejemplo, en el nodo de elemento \<Customer ID = "1" >, `ID` es un atributo y `@ID(Integer)` devuelve "1" como un tipo entero en el campo de datos correspondiente `ID`.|  
|`Value`|El valor del elemento. `Value` solo se puede usar en el último `ElementNode` de la ruta de acceso del elemento. Por ejemplo, porque \<devolver > es un nodo hoja, si se incluye al final de una ruta de acceso de elemento, el valor de `Return {@}` es `Chair`.|  
|`Element`|Valor del subelemento con nombre. Por ejemplo, Customers {}/Customer {}/LastName recupera valores únicamente para el elemento LastName.|  
|`Type`|Tipo de datos opcional que se usa para el campo creado a partir de este elemento.|  
|`NamespacePrefix`|`NamespacePrefix` se define en el elemento XML Query. Si no existe ningún elemento de consulta XML, espacios de nombres en el XML `ElementPath` se omiten. Si hay un elemento XML Query, el elemento XML `ElementPath` tiene un atributo `IgnoreNamespaces` opcional. Si IgnoreNamespaces es `true`, espacios de nombres en el XML `ElementPath` y se pasan por alto el documento XML. Para más información, vea [Sintaxis de consulta XML para los datos de informe XML &#40;SSRS&#41;](report-data-ssrs.md).|  
  
## <a name="example---no-namespaces"></a>Ejemplo: sin espacios de nombres  
 En los ejemplos siguientes se usa el documento XML Customers.xml. En esta tabla se muestran ejemplos de sintaxis de ruta de acceso de elemento y los resultados que se obtienen al utilizar la ruta de acceso de elemento en una consulta que define un conjunto de datos, basándose en el documento XML como origen de datos.  
  
 Tenga en cuenta que, cuando la ruta de acceso de elemento está vacío, la consulta utiliza la ruta de acceso de elemento predeterminada: la primera ruta de acceso a una colección de nodos hoja. En el primer ejemplo, dejar la ruta de acceso de elemento vacía equivale a especificar la ruta de acceso de elemento /Customers/Customer/Orders/Order. Todos los valores de nodo y atributos de la ruta se devuelven en el conjunto de resultados, y los nombres de nodo y nombres de atributo aparecen como campos de conjunto de datos.  
  
-   *Vacía*  
  
    |Pedido de|Qty|Id.|FirstName|LastName|Customer.ID|xmlns|  
    |-----------|---------|--------|---------------|--------------|-----------------|-----------|  
    |Chair|6|1|Bobby|Moore|11|http://www.adventure-works.com|  
    |Table|1|2|Bobby|Moore|11|http://www.adventure-works.com|  
    |Sofa|2|8|Crystal|Hu|20|http://www.adventure-works.com|  
    |EndTables|2|15|Wyatt|Diaz|33|http://www.adventure-works.com|  
  
-   `Customers {}/Customer`  
  
    |FirstName|LastName|Id.|  
    |---------------|--------------|--------|  
    |Bobby|Moore|11|  
    |Crystal|Hu|20|  
    |Wyatt|Diaz|33|  
  
-   `Customers {}/Customer {}/LastName`  
  
    |LastName|  
    |--------------|  
    |Moore|  
    |Hu|  
    |Diaz|  
  
-   `Customers {}/Customer {}/Orders/Order {@,@Qty}`  
  
    |Pedido de|Qty|  
    |-----------|---------|  
    |Chair|6|  
    |Table|1|  
    |Sofa|2|  
    |EndTables|2|  
  
-   `Customers {}/Customer/Orders/Order{ @ID(Integer)}`  
  
    |Order.ID|FirstName|LastName|Id.|  
    |--------------|---------------|--------------|--------|  
    |1|Bobby|Moore|11|  
    |2|Bobby|Moore|11|  
    |8|Crystal|Hu|20|  
    |15|Wyatt|Diaz|33|  
  
#### <a name="xml-document-customersxml"></a>Documento XML: Customers.xml  
 Para probar los ejemplos de ruta de acceso de elemento de la sección anterior, puede copiar este XML, guardarlo en una dirección URL a la que tenga acceso el Diseñador de informes y, a continuación, usar el documento XML como origen de datos XML: por ejemplo, `http://localhost/Customers.xml`.  
  
```  
<?xml version="1.0"?>  
<Customers xmlns="http://www.adventure-works.com">  
   <Customer ID="11">  
      <FirstName>Bobby</FirstName>  
      <LastName>Moore</LastName>  
      <Orders>  
         <Order ID="1" Qty="6">Chair</Order>  
         <Order ID="2" Qty="1">Table</Order>  
      </Orders>  
      <Returns>  
         <Return ID="1" Qty="2">Chair</Return>  
      </Returns>  
   </Customer>  
   <Customer ID="20">  
      <FirstName>Crystal</FirstName>  
      <LastName>Hu</LastName>  
      <Orders>  
         <Order ID="8" Qty="2">Sofa</Order>  
      </Orders>  
      <Returns/>  
   </Customer>  
   <Customer ID="33">  
      <FirstName>Wyatt</FirstName>  
      <LastName>Diaz</LastName>  
      <Orders>  
         <Order ID="15" Qty="2">EndTables</Order>  
      </Orders>  
      <Returns/>  
   </Customer>  
</Customers>  
```  
  
 O bien, puede crear un origen de datos XML que no tenga ninguna cadena de conexión e incrustar Customers.XML en la consulta mediante el procedimiento siguiente:  
  
###### <a name="to-embed-customersxml-in-a-query"></a>Para incrustar Customers.XML en una consulta  
  
1.  Cree un origen de datos XML con una cadena de conexión en blanco.  
  
2.  Cree un nuevo conjunto de datos para el origen de datos XML.  
  
3.  En el cuadro de diálogo **Propiedades del conjunto de datos** , haga clic en **Diseñador de consultas**. Se abre el cuadro de diálogo del diseñador de consultas basado en texto.  
  
4.  Escriba las dos líneas siguientes en el panel de consulta:  
  
     `<Query>`  
  
     `<XmlData>`  
  
5.  Copie Customers.XML y pegue el texto en el panel de consulta después de `<XmlData>`.  
  
6.  En el panel de consulta, elimine la primera línea que copió de Customers.XML: `<?xml version="1.0"?>`  
  
7.  Al final de la consulta, agregue las dos líneas siguientes:  
  
     `<XmlData>`  
  
     `<Query>`  
  
8.  Haga clic en **Ejecutar consulta** (!).  
  
     El conjunto de resultados muestra 4 líneas de datos con las columnas siguientes: `xmlns`, `Customer.ID`, `FirstName`, `LastName`, `ID`, `Qty`, `Order`.  
  
9. [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
## <a name="see-also"></a>Vea también  
 [Tipo de conexión XML &#40;SSRS&#41;](xml-connection-type-ssrs.md)   
 [Tutoriales de Reporting Services &#40;SSRS&#41;](../reporting-services-tutorials-ssrs.md)   
 [Agregar, editar y actualizar campos en el panel Datos de informe &#40;Generador de informes y SSRS&#41;](add-edit-refresh-fields-in-the-report-data-pane-report-builder-and-ssrs.md)  
  
  
