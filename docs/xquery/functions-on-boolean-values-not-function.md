---
title: no (función de XQuery) | Microsoft Docs
ms.custom: ''
ms.date: 03/09/2017
ms.prod: sql
ms.prod_service: sql
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: language-reference
dev_langs:
- XML
helpviewer_keywords:
- effective Boolean value [XQuery]
- fn:not function
- not function [XQuery]
- EBV
ms.assetid: 93dfc377-45f1-4384-9392-560d9331a915
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 7961b6daed4db42095e6d8a0856b3e99c6ca6041
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/01/2018
ms.locfileid: "47849813"
---
# <a name="functions-on-boolean-values---not-function"></a>Funciones usadas en valores booleanos: función not 
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  Devuelve TRUE si el valor booleano efectivo de *$arg* es false y devuelve FALSE si el valor booleano efectivo de *$arg* es true.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
fn:not($arg as item()*) as xs:boolean  
```  
  
## <a name="arguments"></a>Argumentos  
 *$arg*  
 Secuencia de elementos para los que existe un valor booleano efectivo.  
  
## <a name="examples"></a>Ejemplos  
 En este tema se proporciona ejemplos de XQuery con instancias XML almacenadas en varias **xml** columnas de tipo en la base de datos AdventureWorks.  
  
### <a name="a-using-the-not-xquery-function-to-find-product-models-whose-catalog-descriptions-do-not-include-the-specifications-element"></a>A. Usar la función not() de XQuery para buscar modelos de producto cuyas descripciones de catálogo no incluyen el \<especificaciones > elemento.  
 La siguiente consulta genera XML que contiene identificadores correspondientes a modelos de producto cuyas descripciones de catálogo no incluyen el elemento <`Specifications`>.  
  
```  
WITH XMLNAMESPACES ('http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription' AS pd)  
SELECT ProductModelID, CatalogDescription.query('  
       <Product   
           ProductModelID="{ sql:column("ProductModelID") }"  
        />  
') as Result  
FROM Production.ProductModel  
WHERE CatalogDescription.exist('  
     /pd:ProductDescription[not(pd:Specifications/*)]  '  
     ) = 0  
```  
  
 Observe lo siguiente en la consulta anterior:  
  
-   Dado que el documento utiliza espacios de nombres, en el ejemplo se utiliza la instrucción WITH NAMESPACES. Otra opción consiste en usar el **declarar el espacio de nombres** palabra clave en el [prólogo de XQuery](../xquery/modules-and-prologs-xquery-prolog.md) para definir el prefijo.  
  
-   La consulta, a continuación, genera el XML que incluye el <`Product`> elemento y su **ProductModelID** atributo.  
  
-   La cláusula WHERE utiliza el [método exist() (tipo de datos XML)](../t-sql/xml/exist-method-xml-data-type.md) para filtrar las filas. El **exist()** método devuelve True si hay \<ProductDescription > elementos que no tienen \<especificación > elementos secundarios. Tenga en cuenta el uso de la **not()** función.  
  
 Este conjunto de resultados está vacío, porque cada descripción de catálogo del modelo de producto se incluye la \<especificaciones > elemento.  
  
### <a name="b-using-the-not-xquery-function-to-retrieve-work-center-locations-that-do-not-have-a-machinehours-attribute"></a>B. Usar la función not() de XQuery para recuperar ubicaciones de centros de trabajo que no contienen el atributo MachineHours.  
 La siguiente consulta se especifica para la columna Instructions. En esta columna, se almacenan las instrucciones de fabricación de los modelos de producto.  
  
 Para un modelo de producto determinado, la consulta recupera las ubicaciones de los centros de trabajo para las que no se ha especificado MachineHours. Es decir, el atributo **MachineHours** no se especifica para el \<ubicación > elemento.  
  
```  
SELECT ProductModelID, Instructions.query('  
declare namespace AWMI="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelManuInstructions" ;  
     for $i in /AWMI:root/AWMI:Location[not(@MachineHours)]  
     return  
       <Location LocationID="{ $i/@LocationID }"   
                   LaborHrs="{ $i/@LaborHours }" >  
        </Location>  
') as Result  
FROM Production.ProductModel  
WHERE ProductModelID=7   
```  
  
 En la consulta anterior, observe lo siguiente:  
  
-   El **declarenamespace** en [prólogo de XQuery](../xquery/modules-and-prologs-xquery-prolog.md) define el prefijo de espacio de nombres de las instrucciones de fabricación de Adventure Works. Representa el mismo espacio de nombres utilizado en el documento de instrucciones de fabricación.  
  
-   En la consulta, el **no (@MachineHours)** predicado devuelve True si no hay ningún **MachineHours** atributo.  
  
 El resultado es el siguiente:  
  
```  
ProductModelID Result   
-------------- --------------------------------------------  
7              <Location LocationID="30" LaborHrs="1"/>  
               <Location LocationID="50" LaborHrs="3"/>  
               <Location LocationID="60" LaborHrs="4"/>  
```  
  
### <a name="implementation-limitations"></a>Limitaciones de la implementación  
 Éstas son las limitaciones:  
  
-   El **not()** función solo es compatible con los argumentos de tipo xs: Boolean, o node() * o una secuencia vacía.  
  
## <a name="see-also"></a>Vea también  
 [Funciones de XQuery con el tipo de datos xml](../xquery/xquery-functions-against-the-xml-data-type.md)  
  
  
