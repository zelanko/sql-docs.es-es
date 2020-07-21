---
title: Pestaña conjuntos (visor de modelos de minería de datos) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.dm.miningmodeleditor.associationrules.itemsets.f1
ms.assetid: 95b2b805-b142-4064-9c80-4b1b3fe2fe63
author: minewiskan
ms.author: owend
ms.openlocfilehash: 800e14fb360feef3f03804f5d57ed36c57142744
ms.sourcegitcommit: f0772f614482e0b3cde3609e178689ce62ca3a19
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/09/2020
ms.locfileid: "84543697"
---
# <a name="itemsets-tab-mining-model-viewer"></a>Pestaña Conjuntos de elementos (Visor de modelos de minería de datos)
  Puede utilizar el panel **Conjuntos de elementos** para ver los conjuntos de elementos frecuentes que contiene un modelo de minería de datos de reglas de asociación. Dado que un modelo de asociación puede contener muchos conjuntos de elementos, el visor dispone de controles para ayudarle a filtrar los conjuntos de elementos que se muestran en el visor.  
  
 **Para obtener más información:** [Algoritmo de asociación de Microsoft](data-mining/microsoft-association-algorithm.md), [Examinar un modelo usando el Visor de reglas de asociación de Microsoft](data-mining/browse-a-model-using-the-microsoft-association-rules-viewer.md)  
  
## <a name="options"></a>Opciones  
 **Actualizar el contenido del visor**  
 Vuelva a cargar el modelo de minería de datos en el visor.  
  
 **Modelo de minería de datos**  
 Elija esta opción para ver un modelo de minería de datos que se encuentra en la estructura de minería de datos actual. El modelo de minería de datos se abrirá en el visor asociado.  
  
 **Visor**  
 Elija un visor para ver el modelo de minería de datos seleccionado. Puede utilizar el visor personalizado de los modelos de asociación o el visor de árbol de contenido genérico de [!INCLUDE[msCoName](../includes/msconame-md.md)] . También puede utilizar visores de complemento si están disponibles.  
  
 **Soporte mínimo**  
 Cambie este valor para establecer el soporte mínimo que un conjunto de elementos debe contener para aparecer en el visor. El valor predeterminado que se muestra al abrir el modelo por primera vez es calculado por el modelo, pero puede cambiarlo para ver más o menos conjuntos de elementos.  
  
 **Tamaño mínimo del conjunto de elementos**  
 Cambie este valor para establecer el número mínimo de elementos que se debe incluir en un conjunto de elementos para que dicho el conjunto de elementos se pueda mostrar en el visor.  
  
 **Filtrar conjunto de elementos**  
 Especifique un valor de cadena para filtrar el número de conjuntos de elementos que aparece en el visor.  
  
 También puede escribir expresiones regulares .NET como criterios de filtro. Por ejemplo, la siguiente expresión devuelve todos los conjuntos de elementos que contienen 'Road Bottle Cage':  
  
 `\bRoad\b.\bBottle\b.\bCage\b.*`  
  
 Observe que podría tener que actualizar la vista para ver los criterios de filtro aplicados. También puede activar y desactivar la opción **Mostrar nombre largo** para actualizar la lista.  
  
 De forma predeterminada, los criterios de filtro se aplican a todo el nombre de la combinación de atributo-valor; por consiguiente, si solo está viendo el nombre del atributo, podría no ser obvio que los criterios de filtro se han aplicado correctamente. Utilice la lista desplegable **Mostrar** para seleccionar **Mostrar el valor y el nombre del atributo**, y compruebe que la lista de conjuntos de elementos se filtra correctamente.  
  
 **Mostrar**  
 Ajuste el modo en que desea que se muestre el conjunto de elementos en el visor. Puede seleccionar una de las tres opciones siguientes:  
  
-   Mostrar el valor y el nombre del atributo  
  
-   Mostrar solo el valor del atributo  
  
-   Mostrar solo el nombre del atributo  
  
 Observe que esta opción no consulta de nuevo el modelo; solo filtra los atributos o valores que se muestran.  
  
 **Mostrar nombre largo**  
 Seleccione esta opción para mostrar el nombre completo del conjunto de elementos tal como aparece en el contenido del modelo de minería de datos.  
  
 **Número máximo de filas**  
 Limite el número de conjuntos de elementos que se muestran en el visor. De forma predeterminada, los conjuntos de elementos se clasifican por soporte en orden descendente, de modo que si se baja este valor, la lista se restringe a los conjuntos de elementos más comunes.  
  
 **Soporte técnico**  
 Muestra el soporte de cada conjunto de elementos.  
  
 **Tamaño**  
 Muestra el número de elementos que existe en cada conjunto de elementos.  
  
 **Conjunto de elementos**  
 Muestra la descripción de cada conjunto de elementos. De forma predeterminada, los conjuntos de elementos se presentan en una lista de atributos y sus valores delimitada por comas. Puede cambiar la manera en que se muestran utilizando la opción **Mostrar** .  
  
## <a name="see-also"></a>Consulte también  
 [Algoritmos de minería de datos &#40;Analysis Services:&#41;de minería de datos](data-mining/data-mining-algorithms-analysis-services-data-mining.md)   
 [Visores de modelos de minería de datos &#40;diseñador de modelos de minería de datos&#41;](mining-model-viewers-data-mining-model-designer.md)   
 [Visores de modelos de minería de datos](data-mining/data-mining-model-viewers.md)  
  
  
