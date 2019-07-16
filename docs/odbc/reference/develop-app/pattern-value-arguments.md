---
title: Argumentos de valor de patrón | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- catalog functions [ODBC], arguments
- arguments in catalog functions [ODBC], pattern value
- pattern value arguments [ODBC]
ms.assetid: 1d3f0ea6-87af-4836-807f-955e7df2b5df
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 53c091fd0b7a6cfdf390997fb5163fbc9d98e18c
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "68023337"
---
# <a name="pattern-value-arguments"></a>Argumentos de valor de patrón
Funciones de algunos argumentos en el catálogo, como el *TableName* argumento en **SQLTables**, acepte los patrones de búsqueda. Estos argumentos aceptan modelos de búsqueda si se establece el atributo de instrucción SQL_ATTR_METADATA_ID en SQL_FALSE; son los argumentos de identificador que no aceptan un patrón de búsqueda si este atributo está establecido en SQL_TRUE.  
  
 Los caracteres del patrón de búsqueda son:  
  
-   Un carácter de subrayado (_), que representa cualquier carácter individual.  
  
-   Un signo de porcentaje (%), que representa cualquier secuencia de cero o más caracteres.  
  
-   Un carácter de escape, que es específico del controlador y se usa para incluir caracteres de subrayado, signos de porcentaje, y el carácter de escape como literales. Si el carácter de escape precede a un carácter que no es especial, el carácter de escape tiene ningún significado especial. Si el carácter de escape precede a un carácter especial, convierte el carácter especial. Por ejemplo, "\a" se trataría como dos caracteres "\\" y "a", pero "\\%" se tratará como el único carácter especial que no es "%".  
  
 El carácter de escape se recupera con la opción SQL_SEARCH_PATTERN_ESCAPE en **SQLGetInfo**. Debe preceder a cualquier carácter de subrayado, el signo de porcentaje o el carácter de escape en un argumento que acepta patrones de búsqueda para que incluya ese carácter como un literal. En la tabla siguiente se muestran ejemplos.  
  
|Patrón de búsqueda|Descripción|  
|--------------------|-----------------|  
|%A %|Todos los identificadores que contiene la letra A|  
|ABC_|Todos los identificadores de cuatro caracteres, empezando por ABC|  
|ABC\\_|El identificador ABC_, suponiendo que el carácter de escape es una barra diagonal inversa (\\)|  
|\\\\%|Todos los identificadores a partir de una barra diagonal inversa (\\), suponiendo que el carácter de escape es una barra diagonal inversa|  
  
 Debe tener especial cuidado para escapar caracteres del patrón de búsqueda en los argumentos que aceptan los patrones de búsqueda. Esto es especialmente cierto para el carácter de subrayado, que se utiliza habitualmente en los identificadores. Es un error común en las aplicaciones recuperar un valor de una función de catálogo y pasar ese valor a un argumento de patrón de búsqueda en otra función de catálogo. Por ejemplo, suponga que una aplicación recupera el nombre de tabla MY_TABLE desde el resultado establecido para **SQLTables** y la pasa a **SQLColumns** para recuperar una lista de columnas de MY_TABLE. En lugar de obtener las columnas para MY_TABLE, la aplicación obtendrá las columnas para todas las tablas que coinciden con el patrón de búsqueda MY_TABLE como MY_TABLE, MY1TABLE, MY2TABLE y así sucesivamente.  
  
> [!NOTE]
>  ODBC 2. *x* controladores no admiten patrones de búsqueda en el *CatalogName* argumento en **SQLTables**. ODBC 3 *.x* los controladores aceptan modelos de búsqueda en este argumento si el atributo de entorno SQL_ATTR_ ODBC_VERSION está establecido en SQL_OV_ODBC3; no acepta patrones de búsqueda en este argumento si se establece en SQL_OV_ODBC2.  
  
 Pasar un puntero nulo a un argumento de patrón de búsqueda no restringe la búsqueda para ese argumento; es decir, un puntero nulo y el % de patrón de búsqueda (caracteres) son equivalentes. Sin embargo, un patrón de búsqueda de longitud cero: es decir, un puntero válido a una cadena de longitud cero - coincide con la cadena vacía ("").
