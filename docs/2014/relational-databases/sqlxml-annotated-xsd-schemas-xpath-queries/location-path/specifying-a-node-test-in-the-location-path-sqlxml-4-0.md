---
title: Especificar una prueba de nodo en la ruta de acceso de ubicación (SQLXML 4,0) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: xml
ms.topic: reference
helpviewer_keywords:
- XPath queries [SQLXML], location paths
- principal node types [SQLXML]
- node tests [SQLXML]
- location path for XPath query
ms.assetid: f46c30bf-1e24-4435-9ac2-f8ba43a8ff94
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 1d0a3dd41259bcbf2567d34a86527865de011faf
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/26/2020
ms.locfileid: "66012672"
---
# <a name="specifying-a-node-test-in-the-location-path-sqlxml-40"></a>Especificar una prueba de nodo en la ruta de acceso de ubicación (SQLXML 4.0)
  Una prueba de nodo especifica el tipo de nodo seleccionado por el paso de ubicación. Cada eje (`child`, `parent`, `attribute` o `self`) tiene un tipo de nodo principal. Para el `attribute` eje, el tipo de nodo principal es ** \<>de atributo **. En el `parent`caso `child`de los `self` ejes, y, el tipo de nodo principal es ** \<>del elemento **.  
  
> [!NOTE]  
>  La prueba de nodo de carácter comodín * (por ejemplo, `child::*`) no se admite.  
  
## <a name="node-test-example-1"></a>Prueba de nodo: ejemplo 1  
 La ruta de `child::Customer` acceso de la ubicación selecciona ** \<Customer>** elemento secundario del nodo de contexto.  
  
 En este ejemplo, `child` es el eje y `Customer` es la prueba de nodo. El tipo de nodo principal del `child` eje es ** \<>del elemento **. Por lo tanto, la prueba de nodo es true si el>el nodo del ** \<cliente** es un ** \<elemento>** nodo. Si el nodo de contexto no tiene ningún ** \<cliente>** los elementos secundarios, se devuelve un conjunto vacío de nodos.  
  
## <a name="node-test-example-2"></a>Prueba de nodo: Ejemplo 2  
 La ruta de `attribute::CustomerID` acceso de ubicación selecciona el atributo **CustomerID** del nodo de contexto.  
  
 En el ejemplo, `attribute` es el eje y `CustomerID` es la prueba de nodo. El tipo de nodo principal del `attribute` eje es ** \<>de atributo **. Por lo tanto, la prueba de nodo es true si **CustomerID** es un ** \<atributo>** nodo. Si el nodo de contexto no tiene **CustomerID**, se devuelve un conjunto vacío de nodos.  
  
> [!NOTE]  
>  En esta implementación de XPath, si un paso de ubicación hace referencia a un ** \<elemento>** o un ** \<atributo>** tipo que no está declarado en el esquema, se genera un error. Este comportamiento es diferente al de la implementación de XPath en MSXML, que devuelve un conjunto de nodos vacío.  
  
## <a name="abbreviated-syntax-for-the-axes"></a>Sintaxis abreviada para los ejes  
 Se admite la sintaxis abreviada siguiente para la ruta de acceso de ubicación:  
  
-   `attribute::` se puede abreviar como `@`.  
  
     La ruta de acceso de ubicación `Customer[@CustomerID="ALFKI"]` es la misma que `child::Customer[attribute::CustomerID="ALFKI"]`.  
  
-   `child::` se puede omitir en un paso de ubicación.  
  
     Por tanto, `child` es el eje predeterminado. La ruta de acceso de ubicación `Customer/Order` es la misma que `child::Customer/child::Order`.  
  
-   `self::node()` se puede abreviar en un punto (.) y `parent::node()` se puede abreviar en dos puntos (..).  
  
  
