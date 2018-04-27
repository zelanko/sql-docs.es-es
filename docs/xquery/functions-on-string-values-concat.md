---
title: concat (función de XQuery) | Documentos de Microsoft
ms.custom: ''
ms.date: 03/09/2017
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
- fn:concat function
- concat function [XQuery]
ms.assetid: d50afd20-a297-445e-be9e-13b48017e7ca
caps.latest.revision: 32
author: rothja
ms.author: jroth
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: f7d63904e613f399e4f66b9fcd3547f57a0e5175
ms.sourcegitcommit: a85a46312acf8b5a59a8a900310cf088369c4150
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/26/2018
---
# <a name="functions-on-string-values---concat"></a>Funciones en valores de cadena - concat
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  Acepta cero o más cadenas como argumentos y devuelve una cadena creada mediante la concatenación de los valores de cada uno de estos argumentos.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
fn:concat ($string as xs:string?  
           ,$string as xs:string?  
           [, ...]) as xs:string  
```  
  
## <a name="arguments"></a>Argumentos  
 *$string*  
 Cadena opcional que se concatenará.  
  
## <a name="remarks"></a>Comentarios  
 La función requiere al menos dos argumentos. Si un argumento es una secuencia vacía, se tratará como una cadena de longitud cero.  
  
## <a name="supplementary-characters-surrogate-pairs"></a>Caracteres adicionales (pares suplentes)  
 El comportamiento de pares suplentes en las funciones XQuery depende del nivel de compatibilidad de la base de datos y, en algunos casos, del URI del espacio de nombres predeterminado de las funciones. Para obtener más información, vea la sección "XQuery funciones son los caracteres suplentes" en el tema [cambios recientes en las características del motor de base de datos en SQL Server 2016](../database-engine/breaking-changes-to-database-engine-features-in-sql-server-2016.md). Consulte también [nivel de compatibilidad de ALTER DATABASE &#40;Transact-SQL&#41; ](../t-sql/statements/alter-database-transact-sql-compatibility-level.md) y [Collation and Unicode Support](../relational-databases/collations/collation-and-unicode-support.md).  
  
## <a name="examples"></a>Ejemplos  
 Este tema ofrecen ejemplos de XQuery con instancias XML almacenadas en varias **xml** columnas de tipo en la base de datos de ejemplo AdventureWorks.  
  
### <a name="a-using-the-concat-xquery-function-to-concatenate-strings"></a>A. Usar la función de XQuery concat() para concatenar cadenas  
 Para un modelo de producto determinado, esta consulta devuelve una cadena creada mediante la concatenación del período de garantía y la descripción de la misma. En el documento de descripción del catálogo, el elemento <`Warranty`> está formado por los elementos secundarios <`WarrantyPeriod`> y <`Description`>.  
  
```  
WITH XMLNAMESPACES (  
'http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription' AS pd,  
'http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelWarrAndMain' AS wm)  
SELECT CatalogDescription.query('  
    <Product   
        ProductModelID= "{ (/pd:ProductDescription/@ProductModelID)[1] }"  
        ProductModelName = "{ sql:column("PD.Name") }" >  
        {   
          concat( string((/pd:ProductDescription/pd:Features/wm:Warranty/wm:WarrantyPeriod)[1]), "-",  
                  string((/pd:ProductDescription/pd:Features/wm:Warranty/wm:Description)[1]))   
         }   
     </Product>  
 ') as Result  
FROM Production.ProductModel PD  
WHERE  PD.ProductModelID=28  
  
```  
  
 Observe lo siguiente en la consulta anterior:  
  
-   En la cláusula SELECT, CatalogDescription es una **xml** columna de tipo. Por lo tanto, la [método query() (tipo de datos XML)](../t-sql/xml/query-method-xml-data-type.md), instructions.Query, se utiliza. La instrucción de XQuery se especifica como el argumento para el método de consulta.  
  
-   El documento en el que se ejecuta la consulta utiliza espacios de nombres. Por lo tanto, la **espacio de nombres** palabra clave se utiliza para definir el prefijo del espacio de nombres. Para obtener más información, consulte [prólogo de XQuery](../xquery/modules-and-prologs-xquery-prolog.md).  
  
 El resultado es el siguiente:  
  
```  
<Product ProductModelID="28" ProductModelName="Road-450">1 year-parts and labor</Product>  
```  
  
 La consulta anterior recupera información para un producto determinado. La consulta siguiente recupera la misma información para todos los productos para los que se almacenan descripciones del catálogo XML. El **exist()** método de la **xml** tipo de datos en la cláusula WHERE devuelve True si el documento XML en las filas tiene un <`ProductDescription`> elemento.  
  
```  
WITH XMLNAMESPACES (  
'http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription' AS pd,  
'http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelWarrAndMain' AS wm)  
  
SELECT CatalogDescription.query('  
    <Product   
        ProductModelID= "{ (/pd:ProductDescription/@ProductModelID)[1] }"   
        ProductName = "{ sql:column("PD.Name") }" >  
        {   
          concat( string((/pd:ProductDescription/pd:Features/wm:Warranty/wm:WarrantyPeriod)[1]), "-",  
                  string((/pd:ProductDescription/pd:Features/wm:Warranty/wm:Description)[1]))   
         }   
     </Product>  
 ') as Result  
FROM Production.ProductModel PD  
WHERE CatalogDescription.exist('//pd:ProductDescription ') = 1  
  
```  
  
 Tenga en cuenta que el valor booleano que devuelve el **exist()** método de la **xml** tipo se compara con 1.  
  
### <a name="implementation-limitations"></a>Limitaciones de la implementación  
 Éstas son las limitaciones:  
  
-   El **concat()** función en SQL Server sólo acepta valores de tipo xs: String. Los demás valores se deben convertir explícitamente a xs:string o xdt:untypedAtomic.  
  
## <a name="see-also"></a>Vea también  
 [Funciones de XQuery con el tipo de datos xml](../xquery/xquery-functions-against-the-xml-data-type.md)  
  
  
