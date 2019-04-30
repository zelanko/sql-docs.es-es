---
title: Especificar una prueba de nodo en la ruta de acceso de ubicación (SQLXML 4.0) | Microsoft Docs
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
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 7450810f45d81dd1530699677a80a052840ed867
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "63127595"
---
# <a name="specifying-a-node-test-in-the-location-path-sqlxml-40"></a>Especificar una prueba de nodo en la ruta de acceso de ubicación (SQLXML 4.0)
  Una prueba de nodo especifica el tipo de nodo seleccionado por el paso de ubicación. Cada eje (`child`, `parent`, `attribute` o `self`) tiene un tipo de nodo principal. Para el `attribute` eje, el tipo de nodo principal es  **\<atributo >**. Para el `parent`, `child`, y `self` ejes, el tipo de nodo principal es  **\<elemento >**.  
  
> [!NOTE]  
>  La prueba de nodo de carácter comodín * (por ejemplo, `child::*`) no se admite.  
  
## <a name="node-test-example-1"></a>Prueba de nodo: Ejemplo 1  
 La ruta de acceso de ubicación `child::Customer` selecciona  **\<cliente >** elementos secundarios del nodo de contexto.  
  
 En este ejemplo, `child` es el eje y `Customer` es la prueba de nodo. El tipo de nodo principal para el `child` eje es  **\<elemento >**. Por lo tanto, la prueba de nodo es TRUE si el  **\<cliente >** nodo es un  **\<elemento >** nodo. Si el nodo de contexto no tiene ningún  **\<cliente >** elementos secundarios, se devuelve un conjunto de nodos vacío.  
  
## <a name="node-test-example-2"></a>Prueba de nodo: Ejemplo 2  
 La ruta de acceso de ubicación `attribute::CustomerID` selecciona el **CustomerID** atributo del nodo de contexto.  
  
 En el ejemplo, `attribute` es el eje y `CustomerID` es la prueba de nodo. El tipo de nodo principal de la `attribute` eje es  **\<atributo >**. Por lo tanto, la prueba de nodo es TRUE si **CustomerID** es un  **\<atributo >** nodo. Si el nodo de contexto no tiene ningún **CustomerID**, se devuelve un conjunto de nodos vacío.  
  
> [!NOTE]  
>  En esta implementación de XPath, si un paso de ubicación hace referencia a un  **\<elemento >** o un  **\<atributo >** tipo que no se ha declarado en el esquema, se genera un error. Este comportamiento es diferente al de la implementación de XPath en MSXML, que devuelve un conjunto de nodos vacío.  
  
## <a name="abbreviated-syntax-for-the-axes"></a>Sintaxis abreviada para los ejes  
 Se admite la sintaxis abreviada siguiente para la ruta de acceso de ubicación:  
  
-   `attribute::` se puede abreviar como `@`.  
  
     La ruta de acceso de ubicación `Customer[@CustomerID="ALFKI"]` es la misma que `child::Customer[attribute::CustomerID="ALFKI"]`.  
  
-   `child::` se puede omitir en un paso de ubicación.  
  
     Por tanto, `child` es el eje predeterminado. La ruta de acceso de ubicación `Customer/Order` es la misma que `child::Customer/child::Order`.  
  
-   `self::node()` se puede abreviar en un punto (.) y `parent::node()` se puede abreviar en dos puntos (..).  
  
  
