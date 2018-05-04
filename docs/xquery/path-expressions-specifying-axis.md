---
title: Especificar ejes en un paso de expresión de ruta de acceso | Documentos de Microsoft
ms.custom: ''
ms.date: 03/17/2017
ms.prod: sql
ms.prod_service: sql
ms.service: ''
ms.component: xquery
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
applies_to:
- SQL Server
dev_langs:
- XML
helpviewer_keywords:
- attribute axis [SQL Server]
- axis step [XQuery]
- descendant axis
- self axis
- path expressions [XQuery]
- child axis
- descendant-or-self axis
- parent axis
ms.assetid: c44fb843-0626-4496-bde0-52ca0bac0a9e
caps.latest.revision: 30
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 508dfa681a0a7e100b22c91cbd32486039cc1520
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="path-expressions---specifying-axis"></a>Expresiones de ruta de acceso: especificación de eje
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  Un paso de eje de una expresión de ruta de acceso incluye los siguientes componentes:  
  
-   Un eje  
  
-   Un [prueba de nodo](../xquery/path-expressions-specifying-node-test.md)  
  
-   [Cero o más calificadores de paso (opcionales)](../xquery/path-expressions-specifying-predicates.md)  
  
 Para obtener más información, consulte [expresiones de ruta de acceso &#40;XQuery&#41;](../xquery/path-expressions-xquery.md).  
  
 La implementación de XQuery en [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] admite los pasos de eje siguientes:  
  
|Eje|Description|  
|----------|-----------------|  
|**Elemento secundario**|Devuelve elementos secundarios del nodo de contexto.|  
|**descendiente**|Devuelve todos los descendientes del nodo de contexto.|  
|**parent**|Devuelve el elemento primario del nodo de contexto.|  
|**Atributo**|Devuelve atributos del nodo de contexto.|  
|**En sí mismo**|Devuelve el propio nodo de contexto.|  
|**descendant-or-self**|Devuelve el nodo de contexto y todos los descendientes del mismo.|  
  
 Todos estos ejes, excepto el **primario** eje, son ejes directos. El **primario** eje es un eje inverso, pues realiza búsquedas hacia atrás en la jerarquía del documento. Por ejemplo, la expresión de ruta de acceso relativa `child::ProductDescription/child::Summary` tiene dos pasos, y cada uno especifica un eje `child`. El primer paso recupera los \<ProductDescription > elementos secundarios del nodo de contexto. Para cada \<ProductDescription > nodo de elemento, el segundo paso recupera los \<resumen > elementos secundarios del nodo de elemento.  
  
 La expresión de ruta de acceso relativa, `child::root/child::Location/attribute::LocationID`, tiene tres pasos. Cada uno de los dos primeros especifica un eje `child` y el tercero especifica el eje `attribute`. Cuando se ejecutan en las instrucciones de fabricación documentos XML en el **Production.ProductModel** de tabla, la expresión devuelve el `LocationID` atributo de la \<ubicación > nodo de elemento secundario de la \<raíz > elemento.  
  
## <a name="examples"></a>Ejemplos  
 Los ejemplos de consulta en este tema se especifican con **xml** escriba columnas en la **AdventureWorks** base de datos.  
  
### <a name="a-specifying-a-child-axis"></a>A. Especificar un eje child  
 Para un modelo de producto determinado, la consulta siguiente recupera el \<características > elementos secundarios del nodo de elemento de la \<ProductDescription > nodo de elemento de la descripción del catálogo de productos almacenada en el `Production.ProductModel` tabla.  
  
```  
SELECT CatalogDescription.query('  
declare namespace PD="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription";  
  /child::PD:ProductDescription/child::PD:Features')  
FROM Production.ProductModel  
WHERE ProductModelID=19  
```  
  
 Observe lo siguiente en la consulta anterior:  
  
-   El `query()` método de la **xml** tipo de datos especifica la expresión de ruta de acceso.  
  
-   Ambos pasos de la expresión de ruta de acceso especifican un eje `child` y los nombres de nodo, `ProductDescription` y `Features`, como pruebas de nodo. Para obtener información acerca de las pruebas de nodo, vea [especificar la prueba de nodo en un paso de expresión de ruta de acceso](../xquery/path-expressions-specifying-node-test.md).  
  
### <a name="b-specifying-descendant-and-descendant-or-self-axes"></a>B. Especificar ejes descendant y descendant-or-self  
 En el ejemplo siguiente se utilizan ejes descendant y descendant-or-self. La consulta en este ejemplo se especifica con un **xml** variable de tipo. Se ha simplificado la instancia XML para ilustrar claramente la diferencia en los resultados generados.  
  
```  
declare @x xml  
set @x='  
<a>  
 <b>text1  
   <c>text2  
     <d>text3</d>  
   </c>  
 </b>  
</a>'  
declare @y xml  
set @y = @x.query('  
  /child::a/child::b  
')  
select @y  
```  
  
 En el resultado siguiente, la expresión devuelve el nodo de elemento secundario `<b>` del nodo de elemento `<a>`:  
  
```  
<b>text1  
   <c>text2  
     <d>text3</d>  
   </c>  
</b>  
```  
  
 En esta expresión, si especifica un eje descendant para la expresión de ruta de acceso,  
  
 `/child::a/child::b/descendant::*`, está solicitando todos los descendientes del nodo de elemento <`b`>.  
  
 El asterisco (*) en la prueba de nodo representa el nombre del nodo como prueba de nodo. Por tanto, el tipo de nodo principal del eje descendant, el nodo de elemento, determina los tipos de nodos devueltos. Es decir, la expresión devuelve todos los nodos de elemento. No se devuelven los nodos de texto. Para obtener más información sobre el tipo de nodo principal y su relación con la prueba de nodo, vea [especificación de prueba de nodo en un paso de expresión de ruta de acceso](../xquery/path-expressions-specifying-node-test.md) tema.  
  
 Los nodos de elemento <`c`> y <`d`> se devuelven, tal como se muestra en el resultado siguiente:  
  
```  
<c>text2  
     <d>text3</d>  
</c>  
<d>text3</d>  
```  
  
 Si se especifica un eje descendant-or-self en lugar de un eje descendant, `/child::a/child::b/descendant-or-self::*` devolverá el nodo de contexto, el elemento <`b`> y su descendiente.  
  
 El resultado es el siguiente:  
  
```  
<b>text1  
   <c>text2  
     <d>text3</d>  
   </c>  
</b>  
  
<c>text2  
     <d>text3</d>  
</c>  
  
<d>text3</d>   
```  
  
 La siguiente consulta de ejemplo en el **AdventureWorks** base de datos recupera todos los nodos de elemento descendiente de la <`Features`> elemento secundario de la <`ProductDescription`> elemento:  
  
```  
SELECT CatalogDescription.query('  
declare namespace PD="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription";  
  /child::PD:ProductDescription/child::PD:Features/descendant::*  
')  
FROM  Production.ProductModel  
WHERE ProductModelID=19  
```  
  
### <a name="c-specifying-a-parent-axis"></a>C. Especificar un eje parent  
 La consulta siguiente devuelve el elemento secundario <`Summary`> del elemento <`ProductDescription`> en el documento XML del catálogo de productos almacenado en la tabla `Production.ProductModel`.  
  
 En este ejemplo se utiliza el eje parent para volver al elemento primario del elemento <`Feature`> y recuperar el elemento secundario <`Summary`> del elemento <`ProductDescription`>.  
  
```  
SELECT CatalogDescription.query('  
declare namespace PD="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription";  
  
/child::PD:ProductDescription/child::PD:Features/parent::PD:ProductDescription/child::PD:Summary  
')  
FROM   Production.ProductModel  
WHERE  ProductModelID=19  
  
```  
  
 En este ejemplo de consulta, la expresión de ruta de acceso utiliza el eje `parent`. Puede volver a escribir la expresión sin el eje parent, tal como se muestra a continuación:  
  
```  
/child::PD:ProductDescription[child::PD:Features]/child::PD:Summary  
```  
  
 A continuación se ofrece un ejemplo más útil del eje parent.  
  
 Cada descripción de catálogo de modelos de productos almacenada en el **CatalogDescription** columna de la **ProductModel** tabla tiene un `<ProductDescription>` elemento que tiene el `ProductModelID` atributo y `<Features>`elemento secundario, tal como se muestra en el siguiente fragmento:  
  
```  
<ProductDescription ProductModelID="..." >  
  ...  
  <Features>  
    <Feature1>...</Feature1>  
    <Feature2>...</Feature2>  
   ...  
</ProductDescription>  
```  
  
 La consulta establece una variable de iteración, `$f`, en la instrucción FLWOR para devolver el elemento secundario del elemento `<Features>`. Para obtener más información, consulte [FLWOR instrucción e iteración &#40;XQuery&#41;](../xquery/flwor-statement-and-iteration-xquery.md). Por cada característica, la cláusula `return` construye un XML de la forma siguiente:  
  
```  
<Feature ProductModelID="...">...</Feature>  
<Feature ProductModelID="...">...</Feature>  
```  
  
 Para agregar el `ProductModelID` de cada elemento `<Feature`>, se especifica el eje `parent`:  
  
```  
SELECT CatalogDescription.query('  
declare namespace PD="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription";  
declare namespace wm="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelWarrAndMain";  
  for $f in /child::PD:ProductDescription/child::PD:Features/child::*  
  return  
   <Feature  
     ProductModelID="{ ($f/parent::PD:Features/parent::PD:ProductDescription/attribute::ProductModelID)[1]}" >  
          { $f }  
   </Feature>  
')  
FROM  Production.ProductModel  
WHERE ProductModelID=19  
```  
  
 Éste es el resultado parcial:  
  
```  
<Feature ProductModelID="19">  
  <wm:Warranty   
   xmlns:wm="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelWarrAndMain">  
    <wm:WarrantyPeriod>3 years</wm:WarrantyPeriod>  
    <wm:Description>parts and labor</wm:Description>  
  </wm:Warranty>  
</Feature>  
<Feature ProductModelID="19">  
  <wm:Maintenance   
   xmlns:wm="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelWarrAndMain">  
    <wm:NoOfYears>10 years</wm:NoOfYears>  
    <wm:Description>maintenance contract available through your dealer   
                  or any AdventureWorks retail store.</wm:Description>  
  </wm:Maintenance>  
</Feature>  
<Feature ProductModelID="19">  
  <p1:wheel   
   xmlns:p1="http://www.adventure-works.com/schemas/OtherFeatures">  
      High performance wheels.  
  </p1:wheel>  
</Feature>  
```  
  
 Tenga en cuenta que se agrega el predicado `[1]` en la expresión de ruta de acceso para garantizar que se devuelve un valor singleton.  
  
  
