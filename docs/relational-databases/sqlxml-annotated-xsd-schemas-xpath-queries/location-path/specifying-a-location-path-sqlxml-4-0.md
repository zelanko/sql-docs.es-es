---
title: Especificar una ruta de acceso de ubicación (SQLXML 4.0) | Microsoft Docs
ms.custom: ''
ms.date: 03/17/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.component: sqlxml
ms.reviewer: ''
ms.suite: sql
ms.technology: xml
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- absolute location path
- node-set [SQLXML]
- XPath queries [SQLXML], location paths
- relative location path [SQLXML]
- location path for XPath query
ms.assetid: a23a2b75-bc69-49f0-99db-05e14dc15bc0
caps.latest.revision: 24
author: douglaslMS
ms.author: douglasl
manager: craigg
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 8033000aab35da02b5d06a57462730cc74263322
ms.sourcegitcommit: 4183dc18999ad243c40c907ce736f0b7b7f98235
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/27/2018
ms.locfileid: "43082157"
---
# <a name="specifying-a-location-path-sqlxml-40"></a>Especificar una ruta de acceso de ubicación (SQLXML 4.0)
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  Las consultas XPath se especifican en forma de expresión. Existen varios tipos de expresiones. Una ruta de acceso de ubicación es una expresión que selecciona un conjunto de nodos relativos al nodo de contexto. El resultado de evaluar una ruta de acceso de ubicación es un conjunto de nodos.  
  
## <a name="types-of-location-paths"></a>Tipos de rutas de acceso de ubicación  
 Una ruta de acceso de ubicación puede usar cualquiera de estos formatos:  
  
-   **Ruta de acceso de ubicación absoluta**  
  
     Una ruta de acceso de ubicación absoluta comienza en el nodo raíz del documento. Consta de una barra diagonal (/) que puede ir seguida de una ruta de acceso de ubicación relativa. La barra diagonal (/) selecciona el nodo raíz del documento.  
  
-   **Ruta de acceso de ubicación relativa**  
  
     Una ruta de acceso de ubicación relativa comienza en el nodo de contexto del documento. Una ruta de acceso de ubicación consta de un flujo de uno o más pasos de ubicación separados por una barra diagonal (/). Cada paso selecciona un conjunto de nodos relativos al nodo de contexto. La secuencia inicial de pasos selecciona un conjunto de nodos relativo a un nodo de contexto. Cada uno de los nodos de este conjunto se utiliza como un nodo de contexto en el paso siguiente. Los conjuntos de nodos identificados por este paso se unen. Por ejemplo, **child:: Order/child:: OrderDetail** selecciona el  **\<OrderDetail >** elementos secundarios de la  **\<orden >** elemento elementos secundarios del nodo de contexto.  
  
    > [!NOTE]  
    >  En la implementación SQLXML 4.0 de XPath, cada consulta XPath comienza en el contexto raíz, aunque la consulta XPath no sea explícitamente absoluta. Por ejemplo, una consulta XPath que comienza por "Customer" se trata como "/Customer". En la consulta XPath **Customer [Order]**, Customer comienza en el contexto raíz, pero Order comienza en el contexto de cliente. Para obtener más información, consulte [Introducción a las consultas de XPath utilizando &#40;SQLXML 4.0&#41;](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/introduction-to-using-xpath-queries-sqlxml-4-0.md).  
  
## <a name="location-steps"></a>Pasos de ubicación  
 Una ruta de acceso de ubicación (absoluta o relativa) está compuesta por pasos de ubicación que contienen tres partes:  
  
-   **Axis**  
  
     El eje especifica la relación jerárquica entre los nodos seleccionados por el paso de ubicación y el nodo de contexto. El **primario**, **secundarios**, **atributo**, y **self** se admiten los ejes. Si un **secundarios** eje especificado en la ruta de acceso de ubicación, todos los nodos seleccionados por la consulta son elementos secundarios del nodo de contexto. Si un **primario** eje se especifica, el nodo seleccionado es el nodo primario del nodo de contexto. Si un **atributo** eje se especifica, los nodos seleccionados son los atributos del nodo de contexto.  
  
-   **prueba de nodo**  
  
     Una prueba de nodo especifica el tipo de nodo seleccionado por el paso de ubicación. Cada eje (**secundarios**, **primario**, **atributo**, y **self**) tiene un tipo de nodo principal. Para el **atributo** eje, el tipo de nodo principal es  **\<atributo >**. Para el **primario**, **secundarios**, y **self** ejes, el tipo de nodo principal es  **\<elemento >**.  
  
     Por ejemplo, si especifica la ruta de acceso de ubicación **child:: Customer**,  **\<cliente >** se seleccionan los elementos secundarios del nodo de contexto. Dado que el **secundarios** eje tiene  **\<elemento >** como su tipo de nodo principal, la prueba de nodo, Customer, es TRUE si el cliente es un  **\<elemento >** nodo.  
  
-   **Predicados de selección (cero o más)**  
  
     Un predicado filtra un conjunto de nodos con respecto a un eje. La especificación de predicados de selección en una expresión XPath es similar a especificar una cláusula WHERE en una instrucción SELECT. El predicado se especifica entre corchetes. Al aplicar la prueba especificada en los predicados de selección, se filtran los nodos devueltos por la prueba de nodo. Para cada nodo del conjunto de nodos que se va a filtrar, la expresión de predicado se evalúa con ese nodo como el nodo de contexto, con el número de nodos del conjunto de nodos como tamaño de contexto. Si la expresión de predicado se evalúa como TRUE para ese nodo, el nodo se incluye en el conjunto de nodos resultante.  
  
     La sintaxis de un paso de ubicación es el nombre de eje y la prueba de nodo separados por dos signos de dos puntos (::), seguidos de cero o más expresiones, cada una de ellas entre corchetes. Por ejemplo, la expresión XPath (ruta de acceso de ubicación) **child:: Customer [@CustomerID= 'ALFKI']** selecciona todos los  **\<cliente >** elementos secundarios del nodo de contexto. La prueba del predicado se aplica al conjunto de nodos, que devuelve solo el  **\<cliente >** nodos de elemento con el atributo de valor 'ALFKI' para su **CustomerID** atributo.  
  
## <a name="in-this-section"></a>En esta sección  
 [Especificar un eje &#40;SQLXML 4.0&#41;](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/location-path/specifying-an-axis-sqlxml-4-0.md)  
 Proporciona ejemplos sobre la forma de especificar un eje.  
  
 [Especificar una prueba de nodo en la ruta de acceso de ubicación &#40;SQLXML 4.0&#41;](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/location-path/specifying-a-node-test-in-the-location-path-sqlxml-4-0.md)  
 Proporciona ejemplos sobre la forma de especificar una prueba de nodo.  
  
 [Especificar predicados de selección en la ruta de acceso de ubicación &#40;SQLXML 4.0&#41;](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/location-path/specifying-selection-predicates-in-the-location-path-sqlxml-4-0.md)  
 Proporciona ejemplos sobre la forma de especificar predicados de selección.  
  
  
