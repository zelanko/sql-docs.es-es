---
title: Pestaña reglas (visor de modelos de minería de datos) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.dm.miningmodeleditor.associationrules.rules.f1
ms.assetid: 705d5492-b58f-45d9-94d7-ed57b7025823
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: fca78578046122a1598df096e45965367b7880ad
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/26/2020
ms.locfileid: "66070102"
---
# <a name="rules-tab-mining-model-viewer"></a>Pestaña Reglas (Visor de modelos de minería de datos)
  Utilice el panel **Reglas** en un modelo de asociación para ver las reglas que el algoritmo extrajo de los datos. Las reglas describen cómo se relacionan los elementos entre sí, y se pueden utilizar para crear recomendaciones.  
  
 Puede utilizar las opciones del visor para filtrar el número de reglas que se muestra en el visor.  
  
> [!WARNING]  
>  De forma predeterminada, solo las reglas que están por encima del umbral de probabilidad definidas en **Probabilidad mínima** se muestran en el visor. No puede reducir más este valor utilizando el visor, porque el umbral de probabilidad del resultado de la regla se determina cuando se crea el modelo. Para más información, vea [Referencia técnica del algoritmo de asociación de Microsoft](data-mining/microsoft-association-algorithm-technical-reference.md).  
  
 **Para obtener más información:** [Algoritmo de asociación de Microsoft](data-mining/microsoft-association-algorithm.md), [Examinar un modelo usando el Visor de reglas de asociación de Microsoft](data-mining/browse-a-model-using-the-microsoft-association-rules-viewer.md)  
  
## <a name="options"></a>Opciones  
 **Actualizar el contenido del visor**  
 Vuelva a cargar el modelo de minería de datos en el visor.  
  
 **Modelo de minería de datos**  
 Elija esta opción para ver un modelo de minería de datos que se encuentra en la estructura de minería de datos actual. El modelo de minería de datos se abrirá en el visor asociado.  
  
 **Visor**  
 Elija un visor para ver el modelo de minería de datos seleccionado. Puede utilizar el visor personalizado de cada modelo de minería de datos o el **Visor de árbol de contenido genérico de Microsoft**. También puede utilizar visores de complemento si están disponibles.  
  
 **Probabilidad mínima**  
 Cambie este valor para establecer la probabilidad mínima necesaria para que se muestre una regla en el visor. Si se aumenta el valor de probabilidad, se reducirá el número de reglas que se muestran.  
  
 **Importancia mínima**  
 Cambie este valor para establecer la importancia mínima necesaria para que se muestre una regla en el visor. Si se aumenta el valor de importancia, se reducirá el número de reglas que se muestran.  
  
 **Regla del filtro**  
 Especifique un valor de cadena para filtrar el número de reglas que aparece en el visor.  
  
 También puede escribir expresiones regulares .NET como criterios de filtro. Por ejemplo, la siguiente expresión devuelve todas las reglas que contienen 'Road Bottle Cage' en el lado izquierdo de la regla:  
  
 `\bRoad\b.\bBottle\b.\bCage\b.*->.*`  
  
 Observe que podría tener que actualizar la vista para ver los criterios de filtro aplicados. También puede activar y desactivar la opción **Mostrar nombre largo** para actualizar la lista.  
  
 De forma predeterminada, los criterios de filtro se aplican a todo el nombre de la combinación de atributo-valor; por consiguiente, si solo está viendo el nombre del atributo, podría no ser obvio que los criterios de filtro se han aplicado correctamente. Utilice la lista desplegable **Mostrar** para seleccionar **Mostrar el valor y el nombre del atributo**, y compruebe que la lista de conjuntos de elementos se filtra correctamente.  
  
 **Mostrar**  
 Ajuste el modo en que desea que se muestre la regla en el visor. Puede seleccionar una de las tres opciones siguientes:  
  
-   Mostrar el valor y el nombre del atributo  
  
-   Mostrar solo el valor del atributo  
  
-   Mostrar solo el nombre del atributo  
  
 **Mostrar nombre largo**  
 Se muestra el nombre completo de la regla tal como aparece en el contenido del modelo de minería de datos.  
  
 **Número máximo de filas**  
 Limite el número de reglas que se muestra en el visor.  
  
 **Probabilidad**  
 Esta columna del gráfico muestra la probabilidad de cada regla.  
  
 Puede hacer clic en el encabezado de columna para ordenar por probabilidad.  
  
 **Importance**  
 Esta columna del gráfico muestra la importancia de cada regla.  
  
 Puede hacer clic en el encabezado de columna para ordenar por importancia.  
  
 **Regla**  
 Esta columna del gráfico muestra la descripción de texto de cada regla, según el formato especificado mediante las opciones **Mostrar** y **Mostrar nombre largo**.  
  
 Puede hacer clic en el encabezado de columna para ordenar por el texto de la regla.  
  
## <a name="see-also"></a>Consulte también  
 [Algoritmos de minería de datos &#40;Analysis Services:&#41;de minería de datos](data-mining/data-mining-algorithms-analysis-services-data-mining.md)   
 [Visores de modelos de minería de datos &#40;diseñador de modelos de minería de datos&#41;](mining-model-viewers-data-mining-model-designer.md)   
 [Visores de modelos de minería de datos](data-mining/data-mining-model-viewers.md)  
  
  
