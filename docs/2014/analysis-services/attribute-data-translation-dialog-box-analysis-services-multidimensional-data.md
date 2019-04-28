---
title: Atributo de cuadro de diálogo traducción de datos (Analysis Services - datos multidimensionales) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.dimensiondesigner.dimensionstoragesettings.f1
helpviewer_keywords:
- Attribute Data Translation dialog box
ms.assetid: bed286de-1e9b-49de-b09e-3cd076aba152
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 32832a354342b822ac0e6b2853c18c11ed3eb004
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "62650666"
---
# <a name="attribute-data-translation-dialog-box-analysis-services---multidimensional-data"></a>Cuadro de diálogo Traducción de datos de atributos (Analysis Services - Datos multidimensionales)
  Use el cuadro de diálogo **Traducción de datos de atributos** para establecer la columna que contiene los datos del título de la traducción, así como la intercalación y el orden que desea utilizar en los datos traducidos. Para mostrar el cuadro de diálogo **Traducción de datos de atributos** :  
  
-   Haga clic en **Nueva columna de títulos** o **Editar columna de títulos** en el panel **Barra de herramientas** en la pestaña **Traducciones** del **Diseñador de dimensiones**.  
  
-   Haga clic con el botón derecho en el panel **Detalles de traducción** de la pestaña **Traducciones** del **Diseñador de dimensiones** y seleccione **Nueva columna de títulos** o **Editar columna de títulos**.  
  
## <a name="options"></a>Opciones  
 **Atributo**  
 Muestra el atributo seleccionado.  
  
 **Lenguaje**  
 Muestra el idioma seleccionado.  
  
 **Título traducido**  
 Establece el título traducido para el atributo seleccionado.  
  
 **Columnas de traducción**  
 Establece la columna en la que se almacenarán los datos del título de traducción. Solo se puede seleccionar una columna. Se mostrarán todas las tablas relacionadas a las que hace referencia la tabla de dimensión principal.  
  
 **Designador de intercalación**  
 Establece el designador de intercalación para el atributo seleccionado. De manera predeterminada, se selecciona la intercalación actual de Windows. Haga clic en la flecha abajo para seleccionar una de las intercalaciones disponibles.  
  
 **Binario**  
 Seleccione esta opción para ordenar y comparar datos según los patrones de bits definidos para cada carácter. El orden binario distingue mayúsculas de minúsculas, es decir, las minúsculas siempre preceden a las mayúsculas, y distingue acentos. Éste es el orden más rápido.  
  
 Si no selecciona esta opción, [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] sigue el orden y las reglas de comparación definidas en los diccionarios del idioma o alfabeto asociado.  
  
> [!NOTE]  
>  Si selecciona esta opción, se deshabilitarán las opciones **Distinguir mayúsculas de minúsculas**, **Distinguir acentos**, **Distinguir kana**y **Distinguir ancho** .  
  
 **Distingue mayúsculas de minúsculas**  
 Seleccione esta opción para ordenar y comparar datos según las reglas de los diccionarios del idioma o alfabeto asociado y distinguir letras mayúsculas de minúsculas.  
  
 Si no selecciona esta opción, [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] considera que las mayúsculas y las minúsculas son versiones de letras iguales. [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] no define si el orden de las letras minúsculas es inferior o superior en relación con mayúscula las letras si **distingue mayúsculas de minúsculas** no está seleccionada.  
  
 **Distinguir acentos**  
 Seleccione esta opción para ordenar y comparar datos según las reglas de los diccionarios del idioma o alfabeto asociado y distinguir los caracteres acentuados de los no acentuados. Por ejemplo, 'a' no es igual a 'á'.  
  
 Si no está seleccionada, [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] considera que las letras con y sin acentos son iguales.  
  
 **Distinguir Kana**  
 Seleccione esta opción para ordenar y comparar datos según las reglas de diccionario proporcionadas para el idioma o alfabeto asociado y distinguir entre los dos tipos de caracteres kana japoneses: Hiragana y Katakana.  
  
 Si no está seleccionada, [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] considera que los caracteres hiragana y katakana son iguales.  
  
 **Distinguir ancho**  
 Seleccione esta opción para ordenar y comparar datos según las reglas de los diccionarios del idioma o alfabeto asociado y distinguir un carácter de un byte del mismo carácter representado con un carácter de dos bytes.  
  
 Si no está seleccionada, [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] considera que la representación de un byte y la de dos bytes del mismo carácter son iguales.  
  
## <a name="see-also"></a>Vea también  
 [Diseñadores y cuadros de diálogo de Analysis Services &#40;datos multidimensionales&#41;](analysis-services-designers-and-dialog-boxes-multidimensional-data.md)   
 [Detalles de traducción &#40;pestaña traducciones, Diseñador de dimensiones&#41; &#40;Analysis Services - datos multidimensionales&#41;](translation-details-dimension-designer-analysis-services-multidimensional-data.md)  
  
  
