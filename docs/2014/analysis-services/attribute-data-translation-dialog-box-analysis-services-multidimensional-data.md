---
title: Cuadro de diálogo traducción de datos de atributos (Analysis Services-datos multidimensionales) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.dimensiondesigner.dimensionstoragesettings.f1
helpviewer_keywords:
- Attribute Data Translation dialog box
ms.assetid: bed286de-1e9b-49de-b09e-3cd076aba152
author: minewiskan
ms.author: owend
ms.openlocfilehash: 76af68a7f9668b46a55a3bf28f9cf07dd64766aa
ms.sourcegitcommit: 2f166e139f637d6edfb5731510d632a13205eb25
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/08/2020
ms.locfileid: "84527931"
---
# <a name="attribute-data-translation-dialog-box-analysis-services---multidimensional-data"></a>Cuadro de diálogo Traducción de datos de atributos (Analysis Services - Datos multidimensionales)
  Use el cuadro de diálogo **Traducción de datos de atributos** para establecer la columna que contiene los datos del título de la traducción, así como la intercalación y el orden que desea utilizar en los datos traducidos. Para mostrar el cuadro de diálogo **Traducción de datos de atributos** :  
  
-   Haga clic en **Nueva columna de títulos** o **Editar columna de títulos** en el panel **Barra de herramientas** en la pestaña **Traducciones** del **Diseñador de dimensiones**.  
  
-   Haga clic con el botón derecho en el panel **Detalles de traducción** de la pestaña **Traducciones** del **Diseñador de dimensiones** y seleccione **Nueva columna de títulos** o **Editar columna de títulos**.  
  
## <a name="options"></a>Opciones  
 **Attribute**  
 Muestra el atributo seleccionado.  
  
 **Idioma**  
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
  
 **Distinguir mayúsculas de minúsculas**  
 Seleccione esta opción para ordenar y comparar datos según las reglas de los diccionarios del idioma o alfabeto asociado y distinguir letras mayúsculas de minúsculas.  
  
 Si no selecciona esta opción, [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] considera que las mayúsculas y las minúsculas son versiones de letras iguales. [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]no define si el orden de las letras minúsculas es inferior o superior al de las letras mayúsculas cuando no se selecciona distinguir mayúsculas de **minúsculas** .  
  
 **Distinguir acentos**  
 Seleccione esta opción para ordenar y comparar datos según las reglas de los diccionarios del idioma o alfabeto asociado y distinguir los caracteres acentuados de los no acentuados. Por ejemplo, 'a' no es igual a 'á'.  
  
 Si no está seleccionada, [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] considera que las letras con y sin acentos son iguales.  
  
 **Distinguir kana**  
 Seleccione esta opción para ordenar y comparar datos según las reglas de los diccionarios del idioma o alfabeto asociado y distinguir los dos tipos de caracteres kana japoneses: hiragana y katakana.  
  
 Si no está seleccionada, [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] considera que los caracteres hiragana y katakana son iguales.  
  
 **Distinguir ancho**  
 Seleccione esta opción para ordenar y comparar datos según las reglas de los diccionarios del idioma o alfabeto asociado y distinguir un carácter de un byte del mismo carácter representado con un carácter de dos bytes.  
  
 Si no está seleccionada, [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] considera que la representación de un byte y la de dos bytes del mismo carácter son iguales.  
  
## <a name="see-also"></a>Consulte también  
 [Analysis Services diseñadores y cuadros de diálogo &#40;datos multidimensionales&#41;](analysis-services-designers-and-dialog-boxes-multidimensional-data.md)   
 [Detalles de traducción &#40;pestaña traducciones, diseñador de dimensiones&#41; &#40;Analysis Services-datos multidimensionales&#41;](translation-details-dimension-designer-analysis-services-multidimensional-data.md)  
  
  
