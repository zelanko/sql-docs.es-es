---
title: Establecer predicados de selección en la ruta de acceso de ubicación (SQLXML)
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: xml
ms.topic: reference
helpviewer_keywords:
- XPath queries [SQLXML], predicates
- predicates [SQLXML]
- position-based filtering [SQLXML]
- XPath queries [SQLXML], location paths
- filtering [SQLXML]
- location path for XPath query
ms.assetid: dbef4cf4-a89b-4d7e-b72b-4062f7b29a80
author: MightyPen
ms.author: genemi
ms.custom: seo-lt-2019
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 84a3eade8a706e95b3ddba72d96e37d8fabf1fd3
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "75255998"
---
# <a name="specifying-selection-predicates-in-the-location-path-sqlxml-40"></a>Especificar predicados de selección en la ruta de acceso de ubicación (SQLXML 4.0)
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  Un predicado filtra un conjunto de nodos con respecto a un eje (similar a una cláusula WHERE en una instrucción SELECT). El predicado se especifica entre corchetes. Para cada nodo del conjunto de nodos que se va a filtrar, la expresión de predicado se evalúa con ese nodo como el nodo de contexto, con el número de nodos del conjunto de nodos como tamaño de contexto. Si la expresión de predicado se evalúa como TRUE para ese nodo, el nodo se incluye en el conjunto de nodos resultante.  
  
 XPath también permite el filtrado basado en posición. Una expresión de predicado que se evalúa como un número selecciona ese nodo ordinal. Por ejemplo, la ruta de acceso de la ubicación `Customer[3]` devuelve el tercer cliente. No se admiten tales predicados numéricos. Solo se admiten expresiones de predicado que devuelven un resultado Booleano.  
  
> [!NOTE]  
>  Para obtener información acerca de las limitaciones de esta implementación XPath de XPath y las diferencias entre ella y la especificación W3C, vea [Introducción al uso de consultas xpath &#40;SQLXML 4,0&#41;](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/introduction-to-using-xpath-queries-sqlxml-4-0.md).  
  
## <a name="selection-predicate-example-1"></a>Predicado de selección: ejemplo 1  
 La expresión XPath siguiente (ruta de acceso de ubicación) selecciona del nodo de contexto actual todos los elementos del ** \<cliente>** elementos secundarios que tienen el atributo **CustomerID** con el valor ALFKI:  
  
```  
/child::Customer[attribute::CustomerID="ALFKI"]  
```  
  
 En esta consulta XPath, `child` y `attribute` son nombres de eje. `Customer`es la prueba de nodo (true `Customer` si es un ** \<nodo de elemento>**, porque ** \<el elemento>** es el tipo de `child` nodo principal del eje). 
  `attribute::CustomerID="ALFKI"` es el predicado. En el predicado `attribute` , es el eje `CustomerID` y es la prueba de nodo (true si **CustomerID** es un atributo del nodo de contexto, porque ** \<el atributo>** es el tipo de nodo principal del eje de **atributo** ).  
  
 Con la sintaxis abreviada, la consulta XPath también se puede especificar como:  
  
```  
/Customer[@CustomerID="ALFKI"]  
```  
  
## <a name="selection-predicate-example-2"></a>Predicado de selección: ejemplo 2  
 La expresión XPath siguiente (ruta de acceso de ubicación) selecciona del nodo de contexto actual todo el ** \<orden>** descendientes que tienen el atributo **SalesOrderID** con el valor 1:  
  
```  
/child::Customer/child::Order[attribute::SalesOrderID="1"]  
```  
  
 En esta expresión XPath, `child` y `attribute` son los nombres del eje. 
  `Customer`, `Order` y `SalesOrderID` son las pruebas de nodo. 
  `attribute::OrderID="1"` es el predicado.  
  
 Con la sintaxis abreviada, la consulta XPath también se puede especificar como:  
  
```  
/Customer/Order[@SalesOrderID="1"]  
```  
  
## <a name="selection-predicate-example-3"></a>Predicado de selección: ejemplo 3  
 La expresión XPath siguiente (ruta de acceso de ubicación) selecciona del nodo de contexto actual todo el ** \<cliente>** los elementos secundarios que tienen uno o más ** \<** elementos secundarios de ContactName>:  
  
```  
child::Customer[child::ContactName]  
```  
  
 En este ejemplo se da por supuesto que ** \<ContactName>** es un elemento secundario del elemento ** \<>del cliente** en el documento XML, que se conoce como *asignación centrada en elementos* en un esquema XSD anotado.  
  
 En esta expresión XPath, `child` es el nombre de eje. `Customer`es la prueba de nodo (true `Customer` si es un ** \<elemento>** nodo, porque ** \<el elemento>** es el tipo de `child` nodo principal del eje). 
  `child::ContactName` es el predicado. En el predicado `child` , es el eje `ContactName` y es la prueba de nodo ( `ContactName` true si es un ** \<elemento>** nodo).  
  
 Esta expresión devuelve solo los ** \<** elementos secundarios del elemento>Customer del nodo de contexto que tiene ** \<ContactName>** elemento Children.  
  
 Con la sintaxis abreviada, la consulta XPath también se puede especificar como:  
  
```  
Customer[ContactName]  
```  
  
## <a name="selection-predicate-example-4"></a>Predicado de selección: ejemplo 4  
 La expresión XPath siguiente selecciona ** \<** los elementos secundarios del elemento>Customer del nodo de contexto que ** \<** no tienen los elementos secundarios del elemento ContactName>:  
  
```  
child::Customer[not(child::ContactName)]  
```  
  
 En este ejemplo se da por supuesto que ** \<ContactName>** es un elemento secundario del elemento ** \<>del cliente** en el documento XML y el campo ContactName no es necesario en la base de datos.  
  
 En este ejemplo, `child` es el eje. `Customer`es la prueba de nodo (TRUE `Customer` si es \<un elemento> nodo). 
  `not(child::ContactName)` es el predicado. En el predicado `child` , es el eje `ContactName` y es la prueba de nodo ( `ContactName` true si \<es un elemento> nodo).  
  
 Con la sintaxis abreviada, la consulta XPath también se puede especificar como:  
  
```  
Customer[not(ContactName)]  
```  
  
## <a name="selection-predicate-example-5"></a>Predicado de selección: ejemplo 5  
 La expresión XPath siguiente selecciona del nodo de contexto actual todos los ** \<usuarios>** elementos secundarios que tienen el atributo **CustomerID** :  
  
```  
child::Customer[attribute::CustomerID]  
```  
  
 En este ejemplo, `child` es el eje y `Customer` es la prueba de nodo ( `Customer` true si \<es un elemento> nodo). 
  `attribute::CustomerID` es el predicado. En el predicado `attribute` , es el eje `CustomerID` y es el predicado ( `CustomerID` true si es un ** \<atributo>** nodo).  
  
 Con la sintaxis abreviada, la consulta XPath también se puede especificar como:  
  
```  
Customer[@CustomerID]  
```  
  
## <a name="selection-predicate-example-6"></a>Predicado de selección: Ejemplo 6  
 
  [!INCLUDE[msCoName](../../../includes/msconame-md.md)] SQLXML 4.0 incluye compatibilidad para las consultas XPath que contienen un producto cruzado en el predicado, como se muestra en el ejemplo siguiente:  
  
```  
Customer[Order/@OrderDate=Order/@ShipDate]  
```  
  
 Esta consulta selecciona todos los clientes con algún elemento `Order` para el que `OrderDate` sea igual a `ShipDate` de cualquier `Order`.  
  
## <a name="see-also"></a>Consulte también  
 [Introducción a los esquemas XSD anotados &#40;SQLXML 4,0&#41;](../../../relational-databases/sqlxml/annotated-xsd-schemas/introduction-to-annotated-xsd-schemas-sqlxml-4-0.md)   
 [Formato XML del lado cliente &#40;SQLXML 4,0&#41;](../../../relational-databases/sqlxml/formatting/client-side-xml-formatting-sqlxml-4-0.md)  
  
  
