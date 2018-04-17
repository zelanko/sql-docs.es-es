---
title: Los argumentos de valor de patrón | Documentos de Microsoft
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: odbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- catalog functions [ODBC], arguments
- arguments in catalog functions [ODBC], pattern value
- pattern value arguments [ODBC]
ms.assetid: 1d3f0ea6-87af-4836-807f-955e7df2b5df
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 39e6bf4734a63c79b09a78178e567900ff636bd3
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/16/2018
---
# <a name="pattern-value-arguments"></a>Argumentos de valor de patrón
Algunos argumentos en el catálogo de funciones, como la *TableName* argumento en **SQLTables**, acepta patrones de búsqueda. Estos argumentos aceptan patrones de búsqueda si se establece el atributo de instrucción de SQL_ATTR_METADATA_ID en SQL_FALSE; son los argumentos de identificador que no aceptan un patrón de búsqueda si este atributo está establecido en SQL_TRUE.  
  
 Los caracteres del patrón de búsqueda son:  
  
-   Un carácter de subrayado (_), que representa cualquier carácter individual.  
  
-   Un signo de porcentaje (%), que representa cualquier secuencia de cero o más caracteres.  
  
-   Un carácter de escape, que es específico del controlador y se usa para incluir caracteres de subrayado, inicia sesión por ciento, y el carácter de escape como literales. Si el carácter de escape precede a un carácter no especial, el carácter de escape no tiene ningún significado especial. Si el carácter de escape precede a un carácter especial, convierte el carácter especial. Por ejemplo, "\a" se trataría como dos caracteres "\\" y "a", pero "\\%" se tratará como no especial único carácter "%".  
  
 El carácter de escape se recupera con la opción SQL_SEARCH_PATTERN_ESCAPE en **SQLGetInfo**. Debe preceder a cualquier carácter de subrayado, el signo de porcentaje o el carácter de escape dentro de un argumento que acepta patrones de búsqueda para que incluya ese carácter como un literal. En la tabla siguiente se muestran ejemplos.  
  
|Patrón de búsqueda|Description|  
|--------------------|-----------------|  
|% DE %A|Todos los identificadores que contiene la letra A|  
|ABC_|Todos los identificadores de cuatro caracteres a partir de ABC|  
|ABC\\_|El identificador ABC_, suponiendo que el carácter de escape es una barra diagonal inversa (\\)|  
|\\\\%|Todos los identificadores a partir de una barra diagonal inversa (\\), suponiendo que el carácter de escape es una barra diagonal inversa|  
  
 Debe tener un cuidado especial para anteponer caracteres de patrón de búsqueda en los argumentos que aceptan los patrones de búsqueda. Esto es especialmente cierto para el carácter de subrayado, que se utiliza habitualmente en los identificadores. Es un error común en las aplicaciones recuperar un valor de una función de catálogo y pasar ese valor a un argumento de patrón de búsqueda en otra función de catálogo. Por ejemplo, suponga que una aplicación recupera el nombre de tabla MY_TABLE del resultado establecido para **SQLTables** y pasa esta opción para **SQLColumns** para recuperar una lista de columnas de MY_TABLE. En lugar de ver las columnas para MY_TABLE, la aplicación obtendrá las columnas para todas las tablas que coinciden con el patrón de búsqueda MY_TABLE, por ejemplo, MY_TABLE, MY1TABLE, MY2TABLE y así sucesivamente.  
  
> [!NOTE]  
>  ODBC 2. *x* controladores no son compatibles con los patrones de búsqueda en el *CatalogName* argumento en **SQLTables**. ODBC 3*.x* controladores aceptan patrones de búsqueda en este argumento si el atributo de entorno SQL_ATTR_ ODBC_VERSION está establecido en SQL_OV_ODBC3; no acepta patrones de búsqueda en este argumento si se establece en SQL_OV_ODBC2.  
  
 Se pasa un puntero null a un argumento de patrón de búsqueda no limite la búsqueda para dicho argumento; es decir, un puntero nulo y el porcentaje de patrón de búsqueda (en caracteres) son equivalentes. Sin embargo, una longitud de cero Buscar patrón, es decir, un puntero válido a una cadena de longitud cero, coincide con la cadena vacía ("").
