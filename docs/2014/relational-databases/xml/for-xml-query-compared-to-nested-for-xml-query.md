---
title: Comparación de la consulta FOR XML con la consulta FOR XML anidada | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: xml
ms.topic: conceptual
helpviewer_keywords:
- FOR XML query
- queries [XML in SQL Server], comparing query types
ms.assetid: 19225b4a-ee3f-47cf-8bcc-52699eeda32c
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 491c0a0084e334cabe7b0eb7648b50aed46a3abc
ms.sourcegitcommit: 2429fbcdb751211313bd655a4825ffb33354bda3
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/28/2018
ms.locfileid: "52545570"
---
# <a name="for-xml-query-compared-to-nested-for-xml-query"></a>Comparación de la consulta FOR XML con la consulta FOR XML anidada
  En este tema se compara una consulta FOR XML de nivel único con una consulta FOR XML anidada. Una de las ventajas de usar consultas FOR XML anidadas es que puede especificar una combinación de XML centrado en atributos y un XML centrado en elementos para los resultados de la consulta. En este ejemplo se demuestra.  
  
## <a name="example"></a>Ejemplo  
 La siguiente consulta `SELECT` recupera información de categoría y subcategoría de productos de la base de datos [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] . No hay FOR XML anidado en la consulta.  
  
```  
USE AdventureWorks2012;  
GO  
SELECT   ProductCategory.ProductCategoryID,   
         ProductCategory.Name as CategoryName,  
         ProductSubCategory.ProductSubCategoryID,   
         ProductSubCategory.Name  
FROM     Production.ProductCategory, Production.ProductSubCategory  
WHERE    ProductCategory.ProductCategoryID = ProductSubCategory.ProductCategoryID  
ORDER BY ProductCategoryID  
FOR XML AUTO, TYPE  
GO  
```  
  
 Éste es el resultado parcial:  
  
```  
<ProductCategory ProductCategoryID="1" CategoryName="Bike">  
  <ProductSubCategory ProductSubCategoryID="1" Name="Mountain Bike"/>  
  <ProductSubCategory ProductSubCategoryID="2" Name="Road Bike"/>  
  <ProductSubCategory ProductSubCategoryID="3" Name="Touring Bike"/>  
</ProductCategory>  
...  
```  
  
 Si especifica la directiva `ELEMENTS` en la consulta, recibirá un resultado centrado en elementos, como se muestra en el siguiente fragmento de resultados:  
  
```  
<ProductCategory>  
  <ProductCategoryID>1</ProductCategoryID>  
  <CategoryName>Bike</CategoryName>  
  <ProductSubCategory>  
    <ProductSubCategoryID>1</ProductSubCategoryID>  
    <Name>Mountain Bike</Name>  
  </ProductSubCategory>  
  <ProductSubCategory>  
     ...  
  </ProductSubCategory>  
</ProductCategory>  
```  
  
 A continuación, imagine que desea generar una jerarquía XML que sea una combinación de XML centrado en atributos y centrado en elementos, como se muestra en el siguiente fragmento:  
  
```  
<ProductCategory ProductCategoryID="1" CategoryName="Bike">  
  <ProductSubCategory>  
    <ProductSubCategoryID>1</ProductSubCategoryID>  
    <SubCategoryName>Mountain Bike</SubCategoryName></ProductSubCategory>  
  <ProductSubCategory>  
     ...  
  <ProductSubCategory>  
     ...  
</ProductCategory>  
```  
  
 En el fragmento anterior, la información de categoría de productos, como el Id. y el nombre de categoría, son atributos. Sin embargo, la información de subcategoría está centrada en elementos. Para construir el elemento <`ProductCategory`>, puede escribir una consulta `FOR XML` como se muestra a continuación:  
  
```  
SELECT ProductCategoryID, Name as CategoryName  
FROM Production.ProductCategory ProdCat  
ORDER BY ProductCategoryID  
FOR XML AUTO, TYPE  
```  
  
 Éste es el resultado:  
  
```  
< ProdCat ProductCategoryID="1" CategoryName="Bikes" />  
< ProdCat ProductCategoryID="2" CategoryName="Components" />  
< ProdCat ProductCategoryID="3" CategoryName="Clothing" />  
< ProdCat ProductCategoryID="4" CategoryName="Accessories" />  
```  
  
 Para construir los elementos <`ProductSubCategory`> anidados en el XML que desee, debe agregar una consulta `FOR XML` anidada, como se muestra a continuación:  
  
```  
SELECT ProductCategoryID, Name as CategoryName,  
       (SELECT ProductSubCategoryID, Name SubCategoryName  
        FROM   Production.ProductSubCategory  
        WHERE ProductSubCategory.ProductCategoryID =   
              ProductCategory.ProductCategoryID  
        FOR XML AUTO, TYPE, ELEMENTS  
       )  
FROM Production.ProductCategory  
ORDER BY ProductCategoryID  
FOR XML AUTO, TYPE  
```  
  
 Observe lo siguiente en la consulta anterior:    
  
-   La consulta `FOR XML` interna recupera información de subcategoría de productos. La directiva `ELEMENTS` se agrega a la consulta `FOR XML` interna para generar el XML centrado en elementos que se agrega al XML generado por la consulta externa. De manera predeterminada, la consulta externa genera XML centrado en atributos.  
  
-   En la consulta interna, se especifica la directiva `TYPE` para que el resultado sea de tipo **xml** . Si no se especifica `TYPE`, el resultado se devuelve como tipo `nvarchar(max)` y los datos XML se devuelven como entidades.  
  
-   La consulta externa especifica también la directiva `TYPE` . Por tanto, el resultado de esta consulta se devuelve al cliente como tipo **xml** .  
  
 Éste es el resultado parcial:  
  
```  
<ProductCategory ProductCategoryID="1" CategoryName="Bike">  
  <ProductSubCategory>  
    <ProductSubCategoryID>1</ProductSubCategoryID>  
    <SubCategoryName>Mountain Bike</SubCategoryName></ProductSubCategory>  
  <ProductSubCategory>  
     ...  
  <ProductSubCategory>  
     ...  
</ProductCategory>  
```  
  
 La consulta siguiente es solo una extensión de la anterior. Muestra la jerarquía de productos completa de la base de datos [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] . Incluye lo siguiente:  
  
-   Categorías de productos  
  
-   Subcategorías de productos de cada categoría  
  
-   Modelos de productos en cada subcategoría  
  
-   Productos en cada modelo  
  
 Quizá encuentre útil la siguiente consulta para comprender la base de datos [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] :  
  
```  
SELECT ProductCategoryID, Name as CategoryName,  
       (SELECT ProductSubCategoryID, Name SubCategoryName,  
               (SELECT ProductModel.ProductModelID,   
                       ProductModel.Name as ModelName,  
                       (SELECT ProductID, Name as ProductName, Color  
                        FROM   Production.Product  
                        WHERE  Product.ProductModelID =   
                               ProductModel.ProductModelID  
                        FOR XML AUTO, TYPE)  
                FROM   (SELECT distinct ProductModel.ProductModelID,   
                               ProductModel.Name  
                        FROM   Production.ProductModel,   
                               Production.Product  
                        WHERE  ProductModel.ProductModelID =   
                               Product.ProductModelID  
                        AND    Product.ProductSubCategoryID =   
                               ProductSubCategory.ProductSubCategoryID)   
                                  ProductModel  
                FOR XML AUTO, type  
               )  
        FROM Production.ProductSubCategory  
        WHERE ProductSubCategory.ProductCategoryID =   
              ProductCategory.ProductCategoryID  
        FOR XML AUTO, TYPE, ELEMENTS  
       )  
FROM Production.ProductCategory  
ORDER BY ProductCategoryID  
FOR XML AUTO, TYPE  
```  
  
 Éste es el resultado parcial:  
  
```  
<Production.ProductCategory ProductCategoryID="1" CategoryName="Bikes">  
  <Production.ProductSubCategory>  
    <ProductSubCategoryID>1</ProductSubCategoryID>  
    <SubCategoryName>Mountain Bikes</SubCategoryName>  
    <ProductModel ProductModelID="19" ModelName="Mountain-100">  
      <Production.Product ProductID="771"   
                ProductName="Mountain-100 Silver, 38" Color="Silver" />  
      <Production.Product ProductID="772"   
                ProductName="Mountain-100 Silver, 42" Color="Silver" />  
      <Production.Product ProductID="773"   
                ProductName="Mountain-100 Silver, 44" Color="Silver" />  
        ...  
    </ProductModel>  
     ...  
```  
  
 Si quita la directiva `ELEMENTS` de la consulta `FOR XML` anidada que genera subcategorías de productos, todo el resultado está centrado en atributos. Después puede escribir esta consulta sin anidar. La adición de `ELEMENTS` da lugar a un XML parcialmente centrado en atributos y parcialmente centrado en elementos. Este resultado no se puede generar en un solo nivel, consulta FOR XML.  
  
## <a name="see-also"></a>Vea también  
 [Usar consultas FOR XML anidadas](use-nested-for-xml-queries.md)  
  
  
