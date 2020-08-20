---
description: Argumentos de valor de patrón
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: a014c63c7fff6b82bbdd26d9fd5b4391c29d0ce2
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/17/2020
ms.locfileid: "88465757"
---
# <a name="pattern-value-arguments"></a>Argumentos de valor de patrón
Algunos argumentos de las funciones de catálogo, como el argumento *TableName* en **SQLTables**, aceptan patrones de búsqueda. Estos argumentos aceptan patrones de búsqueda si el atributo de instrucción SQL_ATTR_METADATA_ID está establecido en SQL_FALSE; son argumentos de identificador que no aceptan un modelo de búsqueda si este atributo se establece en SQL_TRUE.  
  
 Los caracteres de patrón de búsqueda son:  
  
-   Un carácter de subrayado (_), que representa cualquier carácter individual.  
  
-   Un signo de porcentaje (%), que representa cualquier secuencia de cero o más caracteres.  
  
-   Un carácter de escape, que es específico del controlador y se usa para incluir caracteres de subrayado, signos de porcentaje y el carácter de escape como literales. Si el carácter de escape precede a un carácter no especial, el carácter de escape no tiene ningún significado especial. Si el carácter de escape precede a un carácter especial, escapa al carácter especial. Por ejemplo, "\a" se trataría como dos caracteres, " \\ " y "a", pero " \\ %" se trataría como el carácter individual no especial "%".  
  
 El carácter de escape se recupera con la opción SQL_SEARCH_PATTERN_ESCAPE de **SQLGetInfo**. Debe preceder a cualquier carácter de subrayado, signo de porcentaje o carácter de escape de un argumento que acepte patrones de búsqueda para incluir ese carácter como un literal. En la tabla siguiente se muestran ejemplos.  
  
|Patrón de búsqueda|Descripción|  
|--------------------|-----------------|  
|Un|Todos los identificadores que contienen la letra A|  
|ABC_|Los cuatro identificadores de carácter a partir de ABC|  
|ABC \\ _|El identificador ABC_, suponiendo que el carácter de escape es una barra diagonal inversa ( \\ )|  
|\\\\%|Todos los identificadores que comienzan con una barra diagonal inversa ( \\ ), suponiendo que el carácter de escape es una barra diagonal inversa|  
  
 Se debe tener especial cuidado para escapar caracteres de patrón de búsqueda en argumentos que acepten patrones de búsqueda. Esto es especialmente cierto para el carácter de subrayado, que se usa normalmente en los identificadores. Un error común en las aplicaciones es recuperar un valor de una función de catálogo y pasar ese valor a un argumento de patrón de búsqueda en otra función de catálogo. Por ejemplo, supongamos que una aplicación recupera el nombre de tabla MY_TABLE del conjunto de resultados para **SQLTables** y lo pasa a **SQLColumns** para recuperar una lista de columnas en MY_TABLE. En lugar de obtener las columnas de MY_TABLE, la aplicación obtendrá las columnas de todas las tablas que coinciden con el patrón de búsqueda MY_TABLE, como MY_TABLE, MY1TABLE, MY2TABLE, etc.  
  
> [!NOTE]
>  ODBC 2. los controladores *x* no admiten patrones de búsqueda en el argumento *nombrecatálogo* en **SQLTables**. Los controladores ODBC 3 *. x* aceptan patrones de búsqueda en este argumento si el atributo de entorno de SQL_ATTR_ ODBC_VERSION se establece en SQL_OV_ODBC3; no aceptan patrones de búsqueda en este argumento si se establece en SQL_OV_ODBC2.  
  
 Si se pasa un puntero nulo a un argumento de patrón de búsqueda, no se limita la búsqueda de ese argumento; es decir, un puntero nulo y el patrón de búsqueda% (cualquier carácter) son equivalentes. Sin embargo, un patrón de búsqueda de longitud cero, es decir, un puntero válido a una cadena de longitud cero coincide con la cadena vacía ("").
