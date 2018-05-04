---
title: Especificar predicados de selección en la ruta de acceso de ubicación (SQLXML 4.0) | Documentos de Microsoft
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.service: ''
ms.component: sqlxml
ms.reviewer: ''
ms.suite: sql
ms.technology: xml
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- XPath queries [SQLXML], predicates
- predicates [SQLXML]
- position-based filtering [SQLXML]
- XPath queries [SQLXML], location paths
- filtering [SQLXML]
- location path for XPath query
ms.assetid: dbef4cf4-a89b-4d7e-b72b-4062f7b29a80
caps.latest.revision: 28
author: douglaslMS
ms.author: douglasl
manager: craigg
monikerRange: = azuresqldb-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 1b20a8f5f8957aa26fbb0f5ccce9f4955cd63f25
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="specifying-selection-predicates-in-the-location-path-sqlxml-40"></a>Especificar predicados de selección en la ruta de acceso de ubicación (SQLXML 4.0)
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  Un predicado filtra un conjunto de nodos con respecto a un eje (similar a una cláusula WHERE en una instrucción SELECT). El predicado se especifica entre corchetes. Para cada nodo del conjunto de nodos que se va a filtrar, la expresión de predicado se evalúa con ese nodo como el nodo de contexto, con el número de nodos del conjunto de nodos como tamaño de contexto. Si la expresión de predicado se evalúa como TRUE para ese nodo, el nodo se incluye en el conjunto de nodos resultante.  
  
 XPath también permite el filtrado basado en posición. Una expresión de predicado que se evalúa como un número selecciona ese nodo ordinal. Por ejemplo, la ruta de acceso de la ubicación `Customer[3]` devuelve el tercer cliente. No se admiten tales predicados numéricos. Solo se admiten expresiones de predicado que devuelven un resultado Booleano.  
  
> [!NOTE]  
>  Para obtener información acerca de las limitaciones de esta implementación de XPath y las diferencias entre ella y la especificación W3C, vea [Introducción a las consultas de XPath utilizando &#40;SQLXML 4.0&#41;](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/introduction-to-using-xpath-queries-sqlxml-4-0.md).  
  
## <a name="selection-predicate-example-1"></a>Predicado de selección: Ejemplo 1  
 La expresión XPath siguiente (ruta de acceso de ubicación) selecciona del nodo de contexto actual todos los  **\<cliente >** elementos secundarios que tienen el **CustomerID** atributo con el valor de ALFKI:  
  
```  
/child::Customer[attribute::CustomerID="ALFKI"]  
```  
  
 En esta consulta XPath, `child` y `attribute` son nombres de eje. `Customer` es la prueba de nodo (TRUE si `Customer` es un  **\<nodo element >**, porque  **\<elemento >** es el tipo de nodo principal para el `child` eje). `attribute::CustomerID="ALFKI"` es el predicado. En el predicado, `attribute` es el eje y `CustomerID` es la prueba de nodo (TRUE si **CustomerID** es un atributo del nodo de contexto, porque  **\<atributo >** es la entidad de seguridad tipo de nodo de **atributo** eje).  
  
 Con la sintaxis abreviada, la consulta XPath también se puede especificar como:  
  
```  
/Customer[@CustomerID="ALFKI"]  
```  
  
## <a name="selection-predicate-example-2"></a>Predicado de selección: Ejemplo 2  
 La expresión XPath siguiente (ruta de acceso de ubicación) selecciona del nodo de contexto actual todos los  **\<orden >** descendientes que tienen el **SalesOrderID** atributo con el valor 1:  
  
```  
/child::Customer/child::Order[attribute::SalesOrderID="1"]  
```  
  
 En esta expresión XPath, `child` y `attribute` son los nombres del eje. `Customer`, `Order` y `SalesOrderID` son las pruebas de nodo. `attribute::OrderID="1"` es el predicado.  
  
 Con la sintaxis abreviada, la consulta XPath también se puede especificar como:  
  
```  
/Customer/Order[@SalesOrderID="1"]  
```  
  
## <a name="selection-predicate-example-3"></a>Predicado de selección: Ejemplo 3  
 La expresión XPath siguiente (ruta de acceso de ubicación) selecciona del nodo de contexto actual todos los  **\<cliente >** secundarios que tienen uno o varios  **\<ContactName >** elementos secundarios:  
  
```  
child::Customer[child::ContactName]  
```  
  
 En este ejemplo se da por supuesto que el  **\<ContactName >** es un elemento secundario de la  **\<cliente >** elemento en el documento XML, que se conoce como  *asignación centrada en elementos* en un esquema XSD anotado.  
  
 En esta expresión XPath, `child` es el nombre de eje. `Customer` es la prueba de nodo (TRUE si `Customer` es un  **\<elemento >** nodo, porque  **\<elemento >** es el tipo de nodo principal para `child` eje). `child::ContactName` es el predicado. En el predicado, `child` es el eje y `ContactName` es la prueba de nodo (TRUE si `ContactName` es un  **\<elemento >** nodo).  
  
 Esta expresión devuelve solo el  **\<cliente >** elementos secundarios del nodo de contexto que tienen  **\<ContactName >** elementos secundarios.  
  
 Con la sintaxis abreviada, la consulta XPath también se puede especificar como:  
  
```  
Customer[ContactName]  
```  
  
## <a name="selection-predicate-example-4"></a>Predicado de selección: Ejemplo 4  
 La expresión XPath siguiente selecciona  **\<cliente >** elementos secundarios del nodo de contexto que no tiene  **\<ContactName >** elementos secundarios:  
  
```  
child::Customer[not(child::ContactName)]  
```  
  
 En este ejemplo se da por supuesto que  **\<ContactName >** es un elemento secundario de la  **\<cliente >** elemento en el documento XML y el campo ContactName no es necesario en el base de datos.  
  
 En este ejemplo, `child` es el eje. `Customer` es la prueba de nodo (TRUE si `Customer` es un \<elemento > nodo). `not(child::ContactName)` es el predicado. En el predicado, `child` es el eje y `ContactName` es la prueba de nodo (TRUE si `ContactName` es un \<elemento > nodo).  
  
 Con la sintaxis abreviada, la consulta XPath también se puede especificar como:  
  
```  
Customer[not(ContactName)]  
```  
  
## <a name="selection-predicate-example-5"></a>Predicado de selección: Ejemplo 5  
 La expresión XPath siguiente selecciona del nodo de contexto actual todos los  **\<cliente >** secundarios que tienen el **CustomerID** atributo:  
  
```  
child::Customer[attribute::CustomerID]  
```  
  
 En este ejemplo, `child` es el eje y `Customer` es la prueba de nodo (TRUE si `Customer` es un \<elemento > nodo). `attribute::CustomerID` es el predicado. En el predicado, `attribute` es el eje y `CustomerID` es el predicado (TRUE si `CustomerID` es un  **\<atributo >** nodo).  
  
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
  
## <a name="see-also"></a>Vea también  
 [Introducción a los esquemas XSD anotados &#40;SQLXML 4.0&#41;](../../../relational-databases/sqlxml/annotated-xsd-schemas/introduction-to-annotated-xsd-schemas-sqlxml-4-0.md)   
 [Formato XML del lado cliente & #40; SQLXML 4.0 & #41;](../../../relational-databases/sqlxml/formatting/client-side-xml-formatting-sqlxml-4-0.md)  
  
  
