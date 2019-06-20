---
title: Especificar una prueba de nodo en la ruta de acceso de ubicación (SQLXML 4.0) | Microsoft Docs
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
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
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 15d5389f9a16d676aa5d644b030455d4c63adf7b
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "62720005"
---
# <a name="specifying-a-node-test-in-the-location-path-sqlxml-40"></a>Especificar una prueba de nodo en la ruta de acceso de ubicación (SQLXML 4.0)
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  Una prueba de nodo especifica el tipo de nodo seleccionado por el paso de ubicación. Cada eje (**secundarios**, **primario**, **atributo**, o **self**) tiene un tipo de nodo principal. Para el **atributo** eje, el tipo de nodo principal es  **\<atributo >** . Para el **primario**, **secundarios**, y **self** ejes, el tipo de nodo principal es  **\<elemento >** .  
  
> [!NOTE]  
>  La prueba de nodo de carácter comodín * (por ejemplo, `child::*`) no se admite.  
  
## <a name="node-test-example-1"></a>Prueba de nodo: Ejemplo 1  
 La ruta de acceso de ubicación `child::Customer` selecciona  **\<cliente >** elementos secundarios del nodo de contexto.  
  
 En este ejemplo, `child` es el eje y `Customer` es la prueba de nodo. El tipo de nodo principal para el **secundarios** eje es  **\<elemento >** . Por lo tanto, la prueba de nodo es TRUE si el  **\<cliente >** nodo es un  **\<elemento >** nodo. Si el nodo de contexto no tiene ningún  **\<cliente >** elementos secundarios, se devuelve un conjunto de nodos vacío.  
  
## <a name="node-test-example-2"></a>Prueba de nodo: Ejemplo 2  
 La ruta de acceso de ubicación `attribute::CustomerID` selecciona el **CustomerID** atributo del nodo de contexto.  
  
 En el ejemplo, `attribute` es el eje y `CustomerID` es la prueba de nodo. El tipo de nodo principal de la **atributo** eje es  **\<atributo >** . Por lo tanto, la prueba de nodo es TRUE si **CustomerID** es un  **\<atributo >** nodo. Si el nodo de contexto no tiene ningún **CustomerID**, se devuelve un conjunto de nodos vacío.  
  
> [!NOTE]  
>  En esta implementación de XPath, si un paso de ubicación hace referencia a un  **\<elemento >** o un  **\<atributo >** tipo que no se ha declarado en el esquema, se genera un error. Este comportamiento es diferente al de la implementación de XPath en MSXML, que devuelve un conjunto de nodos vacío.  
  
## <a name="abbreviated-syntax-for-the-axes"></a>Sintaxis abreviada para los ejes  
 Se admite la sintaxis abreviada siguiente para la ruta de acceso de ubicación:  
  
-   `attribute::` se puede abreviar como `@`.  
  
     La ruta de acceso de ubicación `Customer[@CustomerID="ALFKI"]` es la misma que `child::Customer[attribute::CustomerID="ALFKI"]`.  
  
-   `child::` se puede omitir en un paso de ubicación.  
  
     Por lo tanto, **secundarios** es el eje predeterminado. La ruta de acceso de ubicación `Customer/Order` es la misma que `child::Customer/child::Order`.  
  
-   `self::node()` se puede abreviar en un punto (.) y `parent::node()` se puede abreviar en dos puntos (..).  
  
  
