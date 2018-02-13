---
title: "Introducción al uso de consultas XPath (SQLXML 4.0) | Documentos de Microsoft"
ms.custom: 
ms.date: 03/17/2017
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
- XPath queries [SQLXML], about XPath queries
- W3C XPath specification
- XPath queries [SQLXML], functionality
ms.assetid: 01050a8e-0ccc-4a02-a4eb-b48be5c3f4f3
caps.latest.revision: 
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: b08c314d50376e55d9825658aabc75385bbbe0be
ms.sourcegitcommit: 37f0b59e648251be673389fa486b0a984ce22c81
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/12/2018
---
# <a name="introduction-to-using-xpath-queries-sqlxml-40"></a>Introducción al uso de consultas XPath (SQLXML 4.0)
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
Una consulta XPath (Lenguaje de rutas XML) puede especificarse como parte de una dirección URL o dentro de una plantilla. El esquema de asignación determina la estructura de este fragmento resultante y los valores se recuperan de la base de datos. Este proceso es conceptualmente similar a crear vistas utilizando la instrucción CREATE VIEW y escribir consultas SQL en ellas.  
  
> [!NOTE]  
>  Para entender las consultas XPath en SQLXML 4.0, debe estar familiarizado con las vistas XML y otros conceptos relacionados, como las plantillas y el esquema de asignación. Para obtener más información, vea [Introducción a los esquemas XSD anotados &#40; SQLXML 4.0 &#41; ](../../relational-databases/sqlxml/annotated-xsd-schemas/introduction-to-annotated-xsd-schemas-sqlxml-4-0.md)y la norma XPath definida por el World Wide Web Consortium (W3C).  
  
 Un documento XML consta de nodos, como un nodo de elemento, un nodo de atributo, un nodo de texto, etc. Por ejemplo, fíjese en este documento XML:  
  
```  
<root>  
  <Customer cid= "C1" name="Janine" city="Issaquah">  
      <Order oid="O1" date="1/20/1996" amount="3.5" />  
      <Order oid="O2" date="4/30/1997" amount="13.4">Customer was  
          very satisfied</Order>  
   </Customer>  
   <Customer cid="C2" name="Ursula" city="Oelde" >  
      <Order oid="O3" date="7/14/1999" amount="100" note="Wrap it blue white red">  
          <Urgency>Important</Urgency>  
      </Order>  
      <Order oid="O4" date="1/20/1996" amount="10000"/>  
   </Customer>  
</root>  
```  
  
 En este documento,  **\<cliente >** es un nodo element, **cid** es un nodo de atributo, y **"Importante"** es un nodo de texto.  
  
 XPath es un lenguaje de navegación de grafos que se usa para seleccionar un conjunto de nodos de un documento XML. Cada operador XPath selecciona un conjunto de nodos basándose en un conjunto de nodos seleccionado por un operador XPath anterior. Por ejemplo, dado un conjunto de  **\<cliente >** nodos, XPath pueden seleccionar todo  **\<orden >** nodos con el **fecha** valor de atributo de **"7/14/1999"**. El conjunto de nodos resultante contiene todos los pedidos con la fecha de pedido 7/14/1999.  
  
 World Wide Web Consortium (W3C) define el lenguaje XPath como un lenguaje de navegación estándar. SQLXML 4.0 implementa un subconjunto de la especificación XPath de W3C, que se encuentra en http://www.w3.org/TR/1999/PR-xpath-19991008.html.  
  
 A continuación se muestran las diferencias que existen entre la implementación XPath de W3C y la implementación SQLXML 4.0.  
  
-   **Consultas raíz**  
  
     SQLXML 4.0 no admite la consulta raíz (/). Todas las consultas XPath deben comenzar en un nivel superior  **\<ElementType >** en el esquema.  
  
-   **Informar de errores**  
  
     La especificación XPath de W3C no define ninguna condición de error. Las consultas XPath que no pueden seleccionar ningún nodo devuelven un conjunto de nodos vacío. En SQLXML 4.0, una consulta puede devolver muchos tipos de mensajes de error.  
  
-   **Orden del documento**  
  
     En SQLXML 4.0, el orden del documento no siempre viene determinado. Por lo tanto, los predicados numéricos y ejes que use el orden del documento (como **siguiente**) no se implementan.  
  
     La falta de orden del documento también significa que el valor de cadena de un nodo solamente puede evaluarse cuando ese nodo se asigna a una única columna en una única fila. Un elemento con elementos secundarios o un nodo NMTOKENS o IDREFS no puede convertirse en una cadena.  
  
    > [!NOTE]  
    >  En algunos casos, el **key-fields** anotación o las claves de la **relación** anotación puede dar lugar a un orden de documento determinista. Sin embargo, esto no es el uso principal de estas anotaciones para obtener más información, vea [identificar columnas de clave mediante SQL: de Key-campos &#40; SQLXML 4.0 &#41; ](../../relational-databases/sqlxml-annotated-xsd-schemas-using/identifying-key-columns-using-sql-key-fields-sqlxml-4-0.md) y [especificar relaciones mediante SQL: Relationship &#40; SQLXML 4.0 &#41; ](../../relational-databases/sqlxml-annotated-xsd-schemas-using/specifying-relationships-using-sql-relationship-sqlxml-4-0.md).  
  
-   **Tipos de datos**  
  
     SQLXML 4.0 tiene limitaciones en la implementación de la expresión XPath **cadena**, **número**, y **booleano** tipos de datos. Para obtener más información, vea [tipos de datos de XPath &#40; SQLXML 4.0 &#41; ](../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/xpath-data-types-sqlxml-4-0.md).  
  
-   **Consultas entre productos**  
  
     SQLXML 4.0 no admite consultas XPath de varios productos, como `Customers[Order/@OrderDate=Order/@ShipDate]`. Esta consulta selecciona todos los clientes (Customers) con algún pedido (Order) para el que la fecha de pedido (OrderDate) sea igual a la fecha de envío (ShipDate) de algún pedido (Order).  
  
     Sin embargo, SQLXML 4.0 sí admite consultas como `Customer[Order[@OrderDate=@ShippedDate]]`, que selecciona los clientes (Customers) con algún pedido (Order) para el que la fecha de pedido (OrderDate) sea igual a la fecha de envío (ShipDate).  
  
-   **Seguridad y control de errores**  
  
     En función del esquema y de la expresión de consulta XPath que se utilicen, los errores de [!INCLUDE[tsql](../../includes/tsql-md.md)] pueden exponerse a los usuarios en determinadas condiciones.  
  
 En las tablas de las siguientes secciones se proporcionan detalles sobre las diferencias que existen entre la implementación de consultas XPath en SQLXML 4.0 y la especificación W3C en lo que respecta estas áreas.  
  
## <a name="supported-functionality"></a>Funcionalidad compatible  
 En la siguiente tabla se muestran las características del lenguaje XPath que se implementan en SQLXML 4.0.  
  
|Característica|Elemento|Vínculo a consultas de ejemplo|  
|-------------|----------|----------------------------|  
|Ejes|**atributo**, **secundarios**, **primario**, y **en sí mismo** ejes|[Especificar ejes en consultas XPath &#40; SQLXML 4.0 &#41;](../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/samples/specifying-axes-in-xpath-queries-sqlxml-4-0.md)|  
|Predicados con valores booleanos que incluyen predicados sucesivos y anidados||[Especificar operadores aritméticos en consultas XPath &#40; SQLXML 4.0 &#41;](../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/samples/specifying-arithmetic-operators-in-xpath-queries-sqlxml-4-0.md)|  
|Todos los operadores relacionales|=, !=, <, \<=, >, >=|[Especificar operadores relacionales en consultas XPath &#40; SQLXML 4.0 &#41;](../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/samples/specifying-relational-operators-in-xpath-queries-sqlxml-4-0.md)|  
|Operadores aritméticos|+, -, *, div|[Especificar operadores aritméticos en consultas XPath &#40; SQLXML 4.0 &#41;](../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/samples/specifying-arithmetic-operators-in-xpath-queries-sqlxml-4-0.md)|  
|Funciones de conversión explícita|**number()**, **string()**, **Boolean()**|[Especificar funciones de conversión explícita en consultas XPath &#40; SQLXML 4.0 &#41;](../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/samples/specifying-explicit-conversion-functions-in-xpath-queries-sqlxml-4-0.md)|  
|operadores booleanos|AND, OR|[Especificar operadores booleanos en consultas XPath &#40; SQLXML 4.0 &#41;](../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/samples/specifying-boolean-operators-in-xpath-queries-sqlxml-4-0.md)|  
|funciones booleanas|**true()**, **false()**, **not()**|[Especificar funciones booleanas en consultas XPath &#40; SQLXML 4.0 &#41;](../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/samples/specifying-boolean-functions-in-xpath-queries-sqlxml-4-0.md)|  
|variables de XPath||[Especificar Variables XPath en las consultas XPath &#40; SQLXML 4.0 &#41;](../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/samples/specifying-xpath-variables-in-xpath-queries-sqlxml-4-0.md)|  
  
## <a name="unsupported-functionality"></a>Funcionalidad incompatible  
 En la siguiente tabla se muestran las características del lenguaje XPath que no se implementan en SQLXML 4.0.  
  
|Característica|Elemento|  
|-------------|----------|  
|Ejes|**antecesor**, **ancestor-or-self**, **descendientes**, **descendant-or-self (/ /)**, **siguiente**,  **siguiente**, **espacio de nombres**, **anterior**, **elemento anterior**|  
|Predicados con valores numéricos||  
|Operadores aritméticos|mod|  
|Funciones de nodo|**antecesor**, **ancestor-or-self**, **descendientes**, **descendant-or-self (/ /)**, **siguiente**,  **siguiente**, **espacio de nombres**, **anterior**, **elemento anterior**|  
|Funciones de cadena|**string()**, **concat()**, **starts-with()**, **contains()**, **substring-before()**, **substring-after()**, **substring()**, **string-length()**, **normalize()**, **translate()**|  
|funciones booleanas|**lang()**|  
|Funciones numéricas|**sum()**, **floor()**, **ceiling()**, **round()**|  
|Operador de unión|&#124;|  
  
 Cuando especifique consultas XPath en una plantilla, tenga en cuenta el siguiente comportamiento:  
  
-   XPath puede incluir caracteres como < o & que tienen significados especiales en XML (y una plantilla es un documento XML). Debe definir estos caracteres como caracteres de escape mediante la codificación de & en XML o especificar XPath en la dirección URL.  
  
## <a name="see-also"></a>Vea también  
 [Utilizar consultas XPath en SQLXML 4.0](../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/using-xpath-queries-in-sqlxml-4-0.md)  
  
  
