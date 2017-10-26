---
title: "¿Forma de metadatos utiliza? | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- result sets [ODBC], metadata
- metadata [ODBC]
ms.assetid: 70fb976c-9342-4edd-b066-1140696fd0fa
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 4723b48732065ccc2f307d9eeef46f8b35574c2d
ms.contentlocale: es-es
ms.lasthandoff: 09/09/2017

---
# <a name="how-is-metadata-used"></a>¿Forma de metadatos utiliza?
Las aplicaciones requieren metadatos para la mayoría de las operaciones de conjunto de resultados. Por ejemplo, la aplicación utiliza el tipo de datos de una columna para determinar qué tipo de variable se ha de enlazar a esa columna. La longitud en bytes de una columna de caracteres usa para determinar cuánto espacio necesita para mostrar los datos de esa columna. El modo en que una aplicación determina los metadatos de una columna depende del tipo de la aplicación.  
  
 Las aplicaciones verticales funcionan con tablas predefinidas y realizan operaciones predefinidas en esas tablas. Dado que los metadatos del conjunto de resultados para dichas aplicaciones se definen antes de que la aplicación incluso se escribe y se controla mediante el programador de aplicaciones, puede ser codificados de forma rígida en la aplicación. Por ejemplo, si una columna Id. de pedido se define como un entero de 4 bytes en el origen de datos, la aplicación siempre puede enlazar un entero de 4 bytes a esa columna. Cuando los metadatos están codificados de forma rígida en la aplicación, un cambio en las tablas utilizadas por la aplicación suele implicar un cambio en el código de la aplicación. Rara vez es un problema, ya que estos cambios se realizan normalmente como parte de una nueva versión de la aplicación.  
  
 Al igual que las aplicaciones verticales, aplicaciones personalizadas generalmente trabajar con tablas predefinidas y realizan operaciones predefinidas en esas tablas. Por ejemplo, una aplicación podría escribirse para transferir datos entre tres orígenes de datos diferentes; los datos que se transferirá normalmente se conocen cuando se escribe la aplicación. Por lo tanto, las aplicaciones personalizadas también tienden a tener metadatos codificados de forma rígida.  
  
 Aplicaciones genéricas, especialmente las que admiten consultas ad hoc, casi nunca se sabe los metadatos de los conjuntos de resultados que se crean. Por lo tanto, deben detectar los metadatos en tiempo de ejecución mediante las funciones de **SQLNumResultCols**, **SQLDescribeCol**, y **SQLColAttribute**, que se describen en la la sección siguiente, [SQLDescribeCol y SQLColAttribute](../../../odbc/reference/develop-app/sqldescribecol-and-sqlcolattribute.md).  
  
 Todas las aplicaciones, independientemente de su tipo, pueden codificar metadatos para los conjuntos de resultados devueltos por las funciones de catálogo. Estos conjuntos de resultados se definen en la sección de referencia de este manual.

