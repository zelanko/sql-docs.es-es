---
title: Casos de uso generales de XQuery | Microsoft Docs
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql
ms.prod_service: sql
ms.reviewer: ''
ms.technology: xml
ms.topic: language-reference
dev_langs:
- XML
helpviewer_keywords:
- XQuery, general usage cases
ms.assetid: 5187c97b-6866-474d-8bdb-a082634039cc
author: rothja
ms.author: jroth
ms.openlocfilehash: 1e844425f0c512cfe7c15354bf1aeb100d6104e2
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "68004524"
---
# <a name="general-xquery-use-cases"></a>Casos de uso generales de XQuery
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  En este tema se proporcionan ejemplos generales del uso de XQuery.  
  
## <a name="examples"></a>Ejemplos  
  
### <a name="a-query-catalog-descriptions-to-find-products-and-weights"></a>A. Consultar descripciones del catálogo para encontrar productos y pesos  
 La siguiente consulta devuelve los Id. de modelo de producto y los pesos, si existen, de la descripción del catálogo de productos. La consulta crea XML con el formato siguiente:  
  
```  
<Product ProductModelID="...">  
  <Weight>...</Weight>  
</Product>  
```  
  
 Esta es la consulta:  
  
```  
SELECT CatalogDescription.query('  
declare namespace p1="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription";  
  <Product  ProductModelID="{ (/p1:ProductDescription/@ProductModelID)[1] }">  
     {   
       /p1:ProductDescription/p1:Specifications/Weight   
     }   
  </Product>  
') as Result  
FROM Production.ProductModel  
WHERE CatalogDescription is not null  
```  
  
 Observe lo siguiente en la consulta anterior:  
  
-   El **espacio de nombres** palabra clave en el prólogo de XQuery define un prefijo de espacio de nombres que se usa en el cuerpo de la consulta.  
  
-   El cuerpo de la consulta genera el XML requerido.  
  
-   En la cláusula WHERE, el **exist()** método se utiliza para buscar únicamente las filas que contienen descripciones de catálogo de productos. Es decir, el XML que contiene la <`ProductDescription`> elemento.  
  
 Éste es el resultado:  
  
```  
<Product ProductModelID="19"/>  
<Product ProductModelID="23"/>   
<Product ProductModelID="25"/>   
<Product ProductModelID="28"><Weight>Varies with size.</Weight></Product>  
<Product ProductModelID="34"/>  
<Product ProductModelID="35"/>  
```  
  
 La consulta siguiente recupera la misma información, pero solo para los modelos de productos cuya descripción de catálogo incluya el peso, el <`Weight`> elemento, en las especificaciones, el <`Specifications`> elemento. En este ejemplo se utiliza WITH XMLNAMESPACES para declarar el prefijo pd y su enlace de espacio de nombres. De este modo, no se describe el enlace tanto en el **query()** método y en el **exist()** método.  
  
```  
WITH XMLNAMESPACES ('https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription' AS pd)  
SELECT CatalogDescription.query('  
          <Product  ProductModelID="{ (/pd:ProductDescription/@ProductModelID)[1] }">  
                 {   
                      /pd:ProductDescription/pd:Specifications/Weight   
                 }   
          </Product>  
') as x  
FROM Production.ProductModel  
WHERE CatalogDescription.exist('/pd:ProductDescription/pd:Specifications//Weight ') = 1  
```  
  
 En la consulta anterior, el **exist()** método de la **xml** tipo de datos en la cláusula WHERE comprueba si hay una <`Weight`> elemento en el <`Specifications`> elemento.  
  
### <a name="b-find-product-model-ids-for-product-models-whose-catalog-descriptions-include-front-angle-and-small-size-pictures"></a>b. Encontrar identificadores de modelos de productos para modelos de productos en cuyas descripciones de catálogo se incluyan imágenes de pequeño tamaño y ángulo frontal  
 La descripción del catálogo de productos XML incluye las imágenes de producto, el <`Picture`> elemento. Cada imagen tiene varias propiedades. Estos incluyen el ángulo de la imagen, el <`Angle`> elemento y el tamaño de la <`Size`> elemento.  
  
 Para los modelos de productos en cuyas descripciones de catálogo se incluyen imágenes de pequeño tamaño y ángulo frontal, la consulta genera XML con el siguiente formato:  
  
```  
< Product ProductModelID="...">  
  <Picture>  
    <Angle>front</Angle>  
    <Size>small</Size>  
  </Picture>  
</Product>  
WITH XMLNAMESPACES ('https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription' AS pd)  
SELECT CatalogDescription.query('  
   <pd:Product  ProductModelID="{ (/pd:ProductDescription/@ProductModelID)[1] }">  
      <Picture>  
         {  /pd:ProductDescription/pd:Picture/pd:Angle }   
         {  /pd:ProductDescription/pd:Picture/pd:Size }   
      </Picture>  
   </pd:Product>  
') as Result  
FROM  Production.ProductModel  
WHERE CatalogDescription.exist('/pd:ProductDescription/pd:Picture') = 1  
AND   CatalogDescription.value('(/pd:ProductDescription/pd:Picture/pd:Angle)[1]', 'varchar(20)')  = 'front'  
AND   CatalogDescription.value('(/pd:ProductDescription/pd:Picture/pd:Size)[1]', 'varchar(20)')  = 'small'  
```  
  
 Observe lo siguiente en la consulta anterior:  
  
-   En la cláusula WHERE, el **exist()** método se usa para recuperar únicamente las filas que tengan descripciones de catálogo de productos con el <`Picture`> elemento.  
  
-   La cláusula WHERE utiliza el **value()** método dos veces para comparar los valores de la <`Size`> y <`Angle`> elementos.  
  
 Éste es un resultado parcial:  
  
```  
<p1:Product   
  xmlns:p1="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription"   
  ProductModelID="19">  
  <Picture>  
    <p1:Angle>front</p1:Angle>  
    <p1:Size>small</p1:Size>  
  </Picture>  
</p1:Product>  
...  
```  
  
### <a name="c-create-a-flat-list-of-the-product-model-name-and-feature-pairs-with-each-pair-enclosed-in-the-features-element"></a>C. Crear una lista plana del producto pares de nombre y la característica de modelo, con cada par incluido dentro del \<características > elemento  
 En la descripción de catálogo del modelo de producto, el XML incluye varias características del producto. Todas estas características se incluyen en el <`Features`> elemento. La consulta usa [construcción XML (XQuery)](../xquery/xml-construction-xquery.md) para construir el XML requerido. La expresión incluida entre llaves se reemplaza por el resultado.  
  
```  
SELECT CatalogDescription.query('  
declare namespace p1="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription";  
  for $pd in /p1:ProductDescription,  
   $f in $pd/p1:Features/*  
  return  
   <Feature>  
     <ProductModelName> { data($pd/@ProductModelName) } </ProductModelName>  
     { $f }  
  </Feature>          
') as x  
FROM Production.ProductModel  
WHERE ProductModelID=19  
```  
  
 Observe lo siguiente en la consulta anterior:  
  
-   $pd / P1: Features / * devuelve solo el elemento nodos secundarios de <`Features`>, pero $pd / P1:Features/Node() devuelve todos los nodos. donde se incluyen los nodos de elemento, nodos de texto, instrucciones de procesamiento y comentarios.  
  
-   Los dos bucles FOR generan un producto cartesiano a partir del que se devuelven el nombre de producto y la característica individual.  
  
-   El **ProductName** es un atributo. La construcción XML de esta consulta lo devuelve como un elemento.  
  
 Éste es un resultado parcial:  
  
```  
<Feature>  
 <ProductModelName>Mountain 100</ProductModelName>  
 <ProductModelID>19</ProductModelID>  
 <p1:Warranty   
   xmlns:p1="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelWarrAndMain">  
    <p1:WarrantyPeriod>3 year</p1:WarrantyPeriod>  
    <p1:Description>parts and labor</p1:Description>  
 </p1:Warranty>  
</Feature>  
<Feature>  
 <ProductModelName>Mountain 100</ProductModelName>  
 <ProductModelID>19</ProductModelID>  
 <p2:Maintenance xmlns:p2="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelWarrAndMain">  
    <p2:NoOfYears>10</p2:NoOfYears>  
    <p2:Description>maintenance contact available through your dealer   
           or any AdventureWorks retail store.</p2:Description>  
    </p2:Maintenance>  
</Feature>  
...  
...      
```  
  
### <a name="d-from-the-catalog-description-of-a-product-model-list-the-product-model-name-model-id-and-features-grouped-inside-a-product-element"></a>D. Desde la descripción del catálogo de un modelo de producto, el producto de la lista de modelos Id. de nombre, modelo y las características se agrupan dentro de un \<producto > elemento  
 Con la información almacenada en la descripción del catálogo del modelo de producto, la consulta siguiente muestra el nombre del modelo de producto, Id. de modelo, y características se agrupan dentro de un \<producto > elemento.  
  
```  
SELECT ProductModelID, CatalogDescription.query('  
     declare namespace pd="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription";  
     <Product>  
         <ProductModelName>   
           { data(/pd:ProductDescription/@ProductModelName) }   
         </ProductModelName>  
         <ProductModelID>   
           { data(/pd:ProductDescription/@ProductModelID) }   
         </ProductModelID>  
         { /pd:ProductDescription/pd:Features/* }  
     </Product>          
') as x  
FROM Production.ProductModel  
WHERE ProductModelID=19  
```  
  
 Éste es un resultado parcial:  
  
```  
<Product>  
  <ProductModelName>Mountain 100</ProductModelName>  
  <ProductModelID>19</ProductModelID>  
  <p1:Warranty>... </p1:Warranty>  
  <p2:Maintenance>...  </p2:Maintenance>  
  <p3:wheel xmlns:p3="https://www.adventure-works.com/schemas/OtherFeatures">High performance wheels.</p3:wheel>  
  <p4:saddle xmlns:p4="https://www.adventure-works.com/schemas/OtherFeatures">  
    <p5:i xmlns:p5="http://www.w3.org/1999/xhtml">Anatomic design</p5:i> and made from durable leather for a full-day of riding in comfort.</p4:saddle>  
  <p6:pedal xmlns:p6="https://www.adventure-works.com/schemas/OtherFeatures">  
    <p7:b xmlns:p7="http://www.w3.org/1999/xhtml">Top-of-the-line</p7:b> clipless pedals with adjustable tension.</p6:pedal>  
   ...  
```  
  
### <a name="e-retrieve-product-model-feature-descriptions"></a>E. Recuperar descripciones de características de modelos de productos  
 La siguiente consulta genera XML que incluye un <`Product`> elemento que tiene **ProducModelID**, **ProductModelName** atributos y las primeros dos características del producto. En concreto, las primeros dos características de producto son los dos primeros elementos secundarios de la <`Features`> elemento. Si hay más características, devuelve un valor vacío <`There-is-more/`> elemento.  
  
```  
SELECT CatalogDescription.query('  
declare namespace pd="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription";  
     <Product>   
          { /pd:ProductDescription/@ProductModelID }  
          { /pd:ProductDescription/@ProductModelName }   
          {  
            for $f in /pd:ProductDescription/pd:Features/*[position()<=2]  
            return  
            $f   
          }  
          {  
            if (count(/pd:ProductDescription/pd:Features/*) > 2)  
            then <there-is-more/>  
            else ()  
          }   
     </Product>          
') as Result  
FROM Production.ProductModel  
WHERE CatalogDescription is not NULL  
```  
  
 Observe lo siguiente en la consulta anterior:  
  
-   El bucle FOR... Return recupera la primera dos características del producto. El **position()** función se utiliza para buscar la posición de los elementos de la secuencia.  
  
### <a name="f-find-element-names-from-the-product-catalog-description-that-end-with-ons"></a>F. Buscar nombres de elementos que terminen en "ons" en la descripción del catálogo de productos  
 La siguiente consulta busca en las descripciones del catálogo y devuelve todos los elementos en el <`ProductDescription`> elemento cuyo nombre termina en "ons".  
  
```  
SELECT ProductModelID, CatalogDescription.query('  
     declare namespace p1="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription";  
      for $pd in /p1:ProductDescription/*[substring(local-name(.),string-length(local-name(.))-2,3)="ons"]  
      return   
          <Root>  
             { $pd }  
          </Root>  
') as Result  
FROM Production.ProductModel  
WHERE CatalogDescription is not NULL  
```  
  
 Éste es un resultado parcial:  
  
```  
ProductModelID   Result  
-----------------------------------------  
         19        <Root>         
                     <p1:Specifications xmlns:p1="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription">          
                          ...         
                     </p1:Specifications>         
                   </Root>          
```  
  
### <a name="g-find-summary-descriptions-that-contain-the-word-aerodynamic"></a>G. Buscar descripciones resumidas que contengan la palabra "Aerodynamic"  
 La siguiente consulta recupera los modelos de productos cuyas descripciones de catálogo incluyen la palabra "Aerodynamic" en la descripción resumida:  
  
```  
WITH XMLNAMESPACES ('https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription' AS pd)  
SELECT ProductModelID, CatalogDescription.query('  
          <Prod >  
             { /pd:ProductDescription/@ProductModelID }  
             { /pd:ProductDescription/pd:Summary }  
          </Prod>  
 ') as Result  
FROM Production.ProductModel  
WHERE CatalogDescription.value('  
     contains( string( (/pd:ProductDescription/pd:Summary)[1] ),"Aerodynamic")','bit') = 1  
```  
  
 Tenga en cuenta que la consulta SELECT especifica **query()** y **value()** métodos de la **xml** tipo de datos. Por lo tanto, en lugar de repetir la declaración de espacios de nombres dos veces en dos prólogos de consulta distintos, se utiliza el prefijo pd en la consulta y se define una sola vez mediante WITH XMLNAMESPACES.  
  
 Observe lo siguiente en la consulta anterior:  
  
-   La cláusula WHERE se usa para recuperar solo las filas donde la descripción de catálogo contiene la palabra "Aerodynamic" en el <`Summary`> elemento.  
  
-   El **contains()** función se usa para ver si la palabra está incluida en el texto.  
  
-   El **value()** método de la **xml** tipo de datos compara el valor devuelto por **contains()** en 1.  
  
 Éste es el resultado:  
  
```  
ProductModelID Result        
-------------- ------------------------------------------  
28     <Prod ProductModelID="28">  
        <pd:Summary xmlns:pd="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription">  
       <p1:p xmlns:p1="http://www.w3.org/1999/xhtml">  
         A TRUE multi-sport bike that offers streamlined riding and a  
         revolutionary design. Aerodynamic design lets you ride with the   
         pros, and the gearing will conquer hilly roads.</p1:p>  
       </pd:Summary>  
      </Prod>    
```  
  
### <a name="h-find-product-models-whose-catalog-descriptions-do-not-include-product-model-pictures"></a>H. Buscar modelos de productos en cuyas descripciones de catálogo no se incluyan imágenes del modelo de producto  
 La siguiente consulta recupera Productmodelid para modelos de producto cuyas descripciones de catálogo no no incluye un <`Picture`> elemento.  
  
```  
SELECT  ProductModelID  
FROM    Production.ProductModel  
WHERE   CatalogDescription is not NULL  
AND     CatalogDescription.exist('declare namespace p1="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription";  
     /p1:ProductDescription/p1:Picture  
') = 0  
```  
  
 Observe lo siguiente en la consulta anterior:  
  
-   Si el **exist()** método en la cláusula WHERE devuelve False (0), se devuelve el identificador de modelo de producto. De lo contrario, no se devuelve.  
  
-   Dado que todas las descripciones del producto incluyen un <`Picture`> elemento, el conjunto de resultados está vacío en este caso.  
  
## <a name="see-also"></a>Vea también  
 [Consultas XQuery con jerarquía](../xquery/xqueries-involving-hierarchy.md)   
 [Consultas XQuery con orden](../xquery/xqueries-involving-order.md)   
 [Funciones de XQuery para controlar datos relacionales](../xquery/xqueries-handling-relational-data.md)   
 [Buscar cadenas en XQuery](../xquery/string-search-in-xquery.md)   
 [Controlar espacios de nombres en XQuery](../xquery/handling-namespaces-in-xquery.md)   
 [Agregar espacios de nombres a consultas con WITH XMLNAMESPACES](../relational-databases/xml/add-namespaces-to-queries-with-with-xmlnamespaces.md)   
 [Datos XML &#40;SQL Server&#41;](../relational-databases/xml/xml-data-sql-server.md)   
 [Referencia del lenguaje XQuery &#40;SQL Server&#41;](../xquery/xquery-language-reference-sql-server.md)  
  
  
