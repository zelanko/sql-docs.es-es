---
title: ¿Forma de metadatos utiliza? | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- result sets [ODBC], metadata
- metadata [ODBC]
ms.assetid: 70fb976c-9342-4edd-b066-1140696fd0fa
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: fbbba96fa2e99a2ccc0618f31e3b29e7d479f703
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/14/2020
ms.locfileid: "81300175"
---
# <a name="how-is-metadata-used"></a>¿Forma de metadatos utiliza?
Las aplicaciones requieren metadatos para la mayoría de las operaciones de conjunto de resultados. Por ejemplo, la aplicación utiliza el tipo de datos de una columna para determinar qué tipo de variable se ha de enlazar a esa columna. Utiliza la longitud de bytes de una columna de caracteres para determinar cuánto espacio necesita para mostrar los datos de esa columna. El modo en que una aplicación determina los metadatos de una columna depende del tipo de la aplicación.  
  
 Las aplicaciones verticales funcionan con tablas predefinidas y realizan operaciones predefinidas en esas tablas. Dado que los metadatos del conjunto de resultados para estas aplicaciones se definen antes de que la aplicación se escriba y esté controlada por el desarrollador de la aplicación, se puede codificar de forma rígida en la aplicación. Por ejemplo, si una columna Id. de pedido se define como un entero de 4 bytes en el origen de datos, la aplicación siempre puede enlazar un entero de 4 bytes a esa columna. Cuando los metadatos están codificados de forma rígida en la aplicación, un cambio en las tablas utilizadas por la aplicación suele implicar un cambio en el código de la aplicación. Esto rara vez es un problema, porque estos cambios se realizan normalmente como parte de una nueva versión de la aplicación.  
  
 Al igual que las aplicaciones verticales, las aplicaciones personalizadas generalmente funcionan con tablas predefinidas y realizan operaciones predefinidas en esas tablas. Por ejemplo, una aplicación podría escribirse para transferir datos entre tres orígenes de datos diferentes; los datos que se van a transferir se conocen generalmente cuando se escribe la solicitud. Por lo tanto, las aplicaciones personalizadas también tienden a tener metadatos codificados de forma rígida.  
  
 Las aplicaciones genéricas, especialmente las que admiten consultas ad hoc, casi nunca conocen los metadatos de los conjuntos de resultados que crean. Por lo tanto, deben detectar los metadatos en tiempo de ejecución mediante las **funciones SQLNumResultCols**, **SQLDescribeCol**y **SQLColAttribute**, que se describen en la sección siguiente, [SQLDescribeCol y SQLColAttribute](../../../odbc/reference/develop-app/sqldescribecol-and-sqlcolattribute.md).  
  
 Todas las aplicaciones, independientemente de su tipo, pueden codificar de forma rígida los metadatos de los conjuntos de resultados devueltos por las funciones de catálogo. Estos conjuntos de resultados se definen en la sección de referencia de este manual.
