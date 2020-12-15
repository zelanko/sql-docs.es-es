---
title: Especificar una prueba de nodo en la ruta de acceso de ubicación (SQLXML)
description: Obtenga información sobre cómo especificar una prueba de nodo en la ruta de acceso de ubicación de una consulta XPath de SQLXML 4,0.
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
ms.custom: seo-lt-2019
monikerRange: =azuresqldb-current||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: b8fdee8bdc7f3fbc3281ecab7682efdc8378bbdf
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/14/2020
ms.locfileid: "97414918"
---
# <a name="specifying-a-node-test-in-the-location-path-sqlxml-40"></a>Especificar una prueba de nodo en la ruta de acceso de ubicación (SQLXML 4.0)
[!INCLUDE [SQL Server Azure SQL Database](../../../includes/applies-to-version/sql-asdb.md)]
  Una prueba de nodo especifica el tipo de nodo seleccionado por el paso de ubicación. Cada eje (**secundario**, **primario**, **atributo** o **Self**) tiene un tipo de nodo principal. Para el eje de **atributo** , el tipo de nodo principal es **\<attribute>** . En el caso de los ejes **primario**, **secundario** y **propio** , el tipo de nodo principal es **\<element>** .  
  
> [!NOTE]  
>  La prueba de nodo de carácter comodín * (por ejemplo, `child::*`) no se admite.  
  
## <a name="node-test-example-1"></a>Prueba de nodo: ejemplo 1  
 La ruta de acceso `child::Customer` de ubicación selecciona elementos **\<Customer>** secundarios del nodo de contexto.  
  
 En este ejemplo, `child` es el eje y `Customer` es la prueba de nodo. El tipo de nodo principal para el eje **secundario** es **\<element>** . Por lo tanto, la prueba de nodo es TRUE si el **\<Customer>** nodo es un **\<element>** nodo. Si el nodo de contexto no tiene ningún **\<Customer>** elemento secundario, se devuelve un conjunto de nodos vacío.  
  
## <a name="node-test-example-2"></a>Prueba de nodo: Ejemplo 2  
 La ruta `attribute::CustomerID` de acceso de ubicación selecciona el atributo **CustomerID** del nodo de contexto.  
  
 En el ejemplo, `attribute` es el eje y `CustomerID` es la prueba de nodo. El tipo de nodo principal del eje de **atributo** es **\<attribute>** . Por lo tanto, la prueba de nodo es TRUE si **CustomerID** es un **\<attribute>** nodo. Si el nodo de contexto no tiene **CustomerID**, se devuelve un conjunto vacío de nodos.  
  
> [!NOTE]  
>  En esta implementación de XPath, si un paso de ubicación hace referencia a un **\<element>** **\<attribute>** tipo o que no está declarado en el esquema, se genera un error. Este comportamiento es diferente al de la implementación de XPath en MSXML, que devuelve un conjunto de nodos vacío.  
  
## <a name="abbreviated-syntax-for-the-axes"></a>Sintaxis abreviada para los ejes  
 Se admite la sintaxis abreviada siguiente para la ruta de acceso de ubicación:  
  
-   `attribute::` se puede abreviar como `@`.  
  
     La ruta de acceso de ubicación `Customer[@CustomerID="ALFKI"]` es la misma que `child::Customer[attribute::CustomerID="ALFKI"]`.  
  
-   `child::` se puede omitir en un paso de ubicación.  
  
     Por lo tanto, **Child** es el eje predeterminado. La ruta de acceso de ubicación `Customer/Order` es la misma que `child::Customer/child::Order`.  
  
-   `self::node()` se puede abreviar en un punto (.) y `parent::node()` se puede abreviar en dos puntos (..).  
  
  
