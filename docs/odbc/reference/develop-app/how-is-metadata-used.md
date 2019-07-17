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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: ab2efd47ca5b5492c67b88261795cf524c440bda
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "68139009"
---
# <a name="how-is-metadata-used"></a>¿Forma de metadatos utiliza?
Las aplicaciones requieren metadatos para la mayoría de las operaciones de conjunto de resultados. Por ejemplo, la aplicación utiliza el tipo de datos de una columna para determinar qué tipo de variable se ha de enlazar a esa columna. La longitud de bytes de una columna de caracteres utiliza para determinar la cantidad de espacio que necesita para mostrar los datos de esa columna. El modo en que una aplicación determina los metadatos de una columna depende del tipo de la aplicación.  
  
 Aplicaciones verticales trabajar con tablas predefinidas y realizan operaciones predefinidas en esas tablas. Dado que los metadatos del conjunto de resultados para dichas aplicaciones se definen antes de la aplicación aún se escribe y se controla mediante el programador de aplicaciones, puede ser codificada de forma rígida en la aplicación. Por ejemplo, si una columna Id. de pedido se define como un entero de 4 bytes en el origen de datos, la aplicación siempre puede enlazar un entero de 4 bytes a esa columna. Cuando los metadatos están codificados de forma rígida en la aplicación, un cambio en las tablas utilizadas por la aplicación suele implicar un cambio en el código de la aplicación. Rara vez es un problema, ya que estos cambios se realizan normalmente como parte de una nueva versión de la aplicación.  
  
 Al igual que aplicaciones verticales, aplicaciones personalizadas suele trabajar con tablas predefinidas y realizan operaciones predefinidas en esas tablas. Por ejemplo, una aplicación podría escribirse para transferir datos entre los tres orígenes de datos diferentes; los datos que se transfieren normalmente se conocen cuando se escribe la aplicación. Por lo tanto, aplicaciones personalizadas también tienden a tener metadatos codificados de forma rígida.  
  
 Aplicaciones genéricas, especialmente aquellos que admiten consultas ad hoc, casi nunca se sabe los metadatos de los conjuntos de resultados que se crean. Por lo tanto, deben detectar los metadatos en tiempo de ejecución mediante las funciones de **SQLNumResultCols**, **SQLDescribeCol**, y **SQLColAttribute**, que se describen en la la sección siguiente, [SQLDescribeCol y SQLColAttribute](../../../odbc/reference/develop-app/sqldescribecol-and-sqlcolattribute.md).  
  
 Todas las aplicaciones, independientemente de su tipo, pueden codificar de forma rígida metadatos para los conjuntos de resultados devueltos por las funciones de catálogo. Estos conjuntos de resultados se definen en la sección de referencia de este manual.
