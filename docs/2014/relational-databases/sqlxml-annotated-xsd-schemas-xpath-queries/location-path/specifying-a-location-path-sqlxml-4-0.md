---
title: Especificar una ruta de acceso de ubicación (SQLXML 4,0) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: xml
ms.topic: reference
helpviewer_keywords:
- absolute location path
- node-set [SQLXML]
- XPath queries [SQLXML], location paths
- relative location path [SQLXML]
- location path for XPath query
ms.assetid: a23a2b75-bc69-49f0-99db-05e14dc15bc0
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 795e27c020c9ea4c80c858da734ebd315d56615c
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "66012656"
---
# <a name="specifying-a-location-path-sqlxml-40"></a>Especificar una ruta de acceso de ubicación (SQLXML 4.0)
  Las consultas XPath se especifican en forma de expresión. Existen varios tipos de expresiones. Una ruta de acceso de ubicación es una expresión que selecciona un conjunto de nodos relativos al nodo de contexto. El resultado de evaluar una ruta de acceso de ubicación es un conjunto de nodos.  
  
## <a name="types-of-location-paths"></a>Tipos de rutas de acceso de ubicación  
 Una ruta de acceso de ubicación puede usar cualquiera de estos formatos:  
  
-   **Ruta de acceso de ubicación absoluta**  
  
     Una ruta de acceso de ubicación absoluta comienza en el nodo raíz del documento. Consta de una barra diagonal (/) que puede ir seguida de una ruta de acceso de ubicación relativa. La barra diagonal (/) selecciona el nodo raíz del documento.  
  
-   **Ruta de acceso de ubicación relativa**  
  
     Una ruta de acceso de ubicación relativa comienza en el nodo de contexto del documento. Una ruta de acceso de ubicación consta de un flujo de uno o más pasos de ubicación separados por una barra diagonal (/). Cada paso selecciona un conjunto de nodos relativos al nodo de contexto. La secuencia inicial de pasos selecciona un conjunto de nodos relativo a un nodo de contexto. Cada uno de los nodos de este conjunto se utiliza como un nodo de contexto en el paso siguiente. Los conjuntos de nodos identificados por este paso se unen. Por ejemplo, **Child:: order/Child:: OrderDetail** selecciona el ** \<elemento de OrderDetail>** elementos secundarios del elemento ** \<Order>** elementos secundarios del nodo de contexto.  
  
    > [!NOTE]  
    >  En la implementación SQLXML 4.0 de XPath, cada consulta XPath comienza en el contexto raíz, aunque la consulta XPath no sea explícitamente absoluta. Por ejemplo, una consulta XPath que comienza por "Customer" se trata como "/Customer". En el cliente de consulta XPath **[order]**, Customer comienza en el contexto raíz, pero el orden comienza en el contexto del cliente. Para obtener más información, vea [Introducción al uso de consultas XPath &#40;SQLXML 4,0&#41;](../introduction-to-using-xpath-queries-sqlxml-4-0.md).  
  
## <a name="location-steps"></a>Pasos de ubicación  
 Una ruta de acceso de ubicación (absoluta o relativa) está compuesta por pasos de ubicación que contienen tres partes:  
  
-   **Eje**  
  
     El eje especifica la relación jerárquica entre los nodos seleccionados por el paso de ubicación y el nodo de contexto. Se admiten los ejes `parent`, `child`, `attribute` y `self`. Si se especifica un eje `child` en la ruta de acceso de ubicación, todos los nodos seleccionados por la consulta son elementos secundarios del nodo de contexto. Si se especifica un eje `parent`, el nodo seleccionado es el nodo primario del nodo de contexto. Si se especifica un eje `attribute`, los nodos seleccionados son los atributos del nodo de contexto.  
  
-   **Prueba de nodo**  
  
     Una prueba de nodo especifica el tipo de nodo seleccionado por el paso de ubicación. Cada eje (`child`, `parent`, `attribute` y `self`) tiene un tipo de nodo principal. Para el `attribute` eje, el tipo de nodo principal es ** \<>de atributo **. En el `parent`caso `child`de los `self` ejes, y, el tipo de nodo principal es ** \<>del elemento **.  
  
     Por ejemplo, si la ruta de acceso de ubicación especifica **Child:: Customer**, se seleccionan los ** \<** elementos secundarios del cliente>del nodo de contexto. Dado que `child` el eje tiene ** \<el elemento>** como su tipo de nodo principal, la prueba de nodo, Customer, es true si Customer es un ** \<elemento>** nodo.  
  
-   **Predicados de selección (cero o más)**  
  
     Un predicado filtra un conjunto de nodos con respecto a un eje. La especificación de predicados de selección en una expresión XPath es similar a especificar una cláusula WHERE en una instrucción SELECT. El predicado se especifica entre corchetes. Al aplicar la prueba especificada en los predicados de selección, se filtran los nodos devueltos por la prueba de nodo. Para cada nodo del conjunto de nodos que se va a filtrar, la expresión de predicado se evalúa con ese nodo como el nodo de contexto, con el número de nodos del conjunto de nodos como tamaño de contexto. Si la expresión de predicado se evalúa como TRUE para ese nodo, el nodo se incluye en el conjunto de nodos resultante.  
  
     La sintaxis de un paso de ubicación es el nombre de eje y la prueba de nodo separados por dos signos de dos puntos (::), seguidos de cero o más expresiones, cada una de ellas entre corchetes. Por ejemplo, la expresión XPath (ruta de acceso de ubicación) **Child:@CustomerID: Customer [= ' ALFKI ']** selecciona todos los ** \<elementos del cliente>** elemento secundario del nodo de contexto. A continuación, la prueba del predicado se aplica al conjunto de nodos, que solo devuelve ** \<** los nodos de elemento de>de cliente con el valor de atributo ' ALFKI ' para su atributo **CustomerID** .  
  
## <a name="in-this-section"></a>En esta sección  
 [Especificar un eje &#40;SQLXML 4,0&#41;](specifying-an-axis-sqlxml-4-0.md)  
 Proporciona ejemplos sobre la forma de especificar un eje.  
  
 [Especificar una prueba de nodo en la ruta de acceso de ubicación &#40;SQLXML 4,0&#41;](specifying-a-node-test-in-the-location-path-sqlxml-4-0.md)  
 Proporciona ejemplos sobre la forma de especificar una prueba de nodo.  
  
 [Especificar predicados de selección en la ruta de acceso de ubicación &#40;SQLXML 4,0&#41;](specifying-selection-predicates-in-the-location-path-sqlxml-4-0.md)  
 Proporciona ejemplos sobre la forma de especificar predicados de selección.  
  
  
