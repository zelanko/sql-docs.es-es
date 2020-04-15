---
title: Argumentos de valor de patrón ? Microsoft Docs
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 0b8e7b7de64d8051118089a54cf14eb45dc96f74
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/14/2020
ms.locfileid: "81282385"
---
# <a name="pattern-value-arguments"></a>Argumentos de valor de patrón
Algunos argumentos de las funciones de catálogo, como el argumento *TableName* en **SQLTables**, aceptan patrones de búsqueda. Estos argumentos aceptan patrones de búsqueda si el atributo de instrucción SQL_ATTR_METADATA_ID se establece en SQL_FALSE; son argumentos identificador que no aceptan un patrón de búsqueda si este atributo se establece en SQL_TRUE.  
  
 Los caracteres del patrón de búsqueda son:  
  
-   Un carácter de subrayado (_), que representa cualquier carácter individual.  
  
-   Un signo de porcentaje (%), que representa cualquier secuencia de cero o más caracteres.  
  
-   Un carácter de escape, que es específico del controlador y se utiliza para incluir guiones bajos, signos de porcentaje y el carácter de escape como literales. Si el carácter de escape precede a un carácter no especial, el carácter de escape no tiene ningún significado especial. Si el carácter de escape precede a un carácter especial, escapa al carácter especial. Por ejemplo, "a" se trataría como\\dos caracteres, "\\" y "a", pero " %" se trataría como el carácter único no especial "%".  
  
 El carácter de escape se recupera con la opción SQL_SEARCH_PATTERN_ESCAPE en **SQLGetInfo**. Debe preceder a cualquier carácter de subrayado, signo de porcentaje o de escape en un argumento que acepte patrones de búsqueda para incluir ese carácter como literal. En la tabla siguiente se muestran ejemplos.  
  
|Patrón de búsqueda|Descripción|  
|--------------------|-----------------|  
|%A%|Todos los identificadores que contienen la letra A|  
|ABC_|Los cuatro identificadores de caracteres que comienzan con ABC|  
|ABC\\_|El identificador ABC_, suponiendo que el\\carácter de escape es una barra diagonal inversa ( )|  
|\\\\%|Todos los identificadores que\\comienzan con una barra diagonal inversa ( ), suponiendo que el carácter de escape sea una barra diagonal inversa|  
  
 Se debe tener especial cuidado para escapar de los caracteres de patrón de búsqueda en argumentos que acepten patrones de búsqueda. Esto es particularmente cierto para el carácter de subrayado, que se utiliza comúnmente en identificadores. Un error común en las aplicaciones es recuperar un valor de una función de catálogo y pasar ese valor a un argumento de patrón de búsqueda en otra función de catálogo. Por ejemplo, supongamos que una aplicación recupera el nombre de tabla MY_TABLE del conjunto de resultados para **SQLTables** y lo pasa a **SQLColumns** para recuperar una lista de columnas en MY_TABLE. En lugar de obtener las columnas para MY_TABLE, la aplicación obtendrá las columnas de todas las tablas que coinciden con el patrón de búsqueda MY_TABLE, como MY_TABLE, MY1TABLE, MY2TABLE, etc.  
  
> [!NOTE]
>  ODBC 2. *x* los controladores no admiten patrones de búsqueda en el argumento *CatalogName* de **SQLTables**. Los controladores *.x* de ODBC 3 aceptan patrones de búsqueda en este argumento si el atributo de entorno SQL_ATTR_ ODBC_VERSION se establece en SQL_OV_ODBC3; no aceptan patrones de búsqueda en este argumento si se establece en SQL_OV_ODBC2.  
  
 Pasar un puntero nulo a un argumento de patrón de búsqueda no restringe la búsqueda de ese argumento; es decir, un puntero nulo y el patrón de búsqueda % (cualquier carácter) son equivalentes. Sin embargo, un patrón de búsqueda de longitud cero , es decir, un puntero válido a una cadena de longitud cero, coincide solo con la cadena vacía ("").
