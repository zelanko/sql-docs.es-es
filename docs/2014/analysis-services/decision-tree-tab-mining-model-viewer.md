---
title: Ficha (Visor de modelos de minería de datos) del árbol de decisión | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.dm.miningmodeleditor.decisiontree.f1
ms.assetid: dc88606f-ba7c-4f8d-af65-bfa17ec16e2b
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: cee721aca66f5266a29d3bf61babf9060e9aef32
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/23/2019
ms.locfileid: "66082298"
---
# <a name="decision-tree-tab-mining-model-viewer"></a>Pestaña Árbol de decisión (Visor de modelos de minería de datos)
  El panel **Árbol de decisión** muestra una representación visual de las reglas de decisión que se crean en un modelo de árbol de decisión. Las reglas de decisión describen las rutas hacia un determinado resultado.  
  
 **Para obtener más información:** [Algoritmo de árboles de decisión de Microsoft](data-mining/microsoft-decision-trees-algorithm.md), [examinar un modelo usando el Visor de árboles de Microsoft](data-mining/browse-a-model-using-the-microsoft-tree-viewer.md)  
  
## <a name="options"></a>Opciones  
 **Actualizar el contenido del Visor**  
 Vuelva a cargar el modelo de minería de datos en el visor.  
  
 **Modelo de minería de datos**  
 Elija un modelo de minería de datos de los de la estructura de minería de datos actual. El modelo de minería de datos se abrirá en el visor asociado.  
  
 **Viewer**  
 Elija un visor para explorar el modelo de minería de datos seleccionado. Puede utilizar el visor personalizado o el Visor de contenido de minería de datos de [!INCLUDE[msCoName](../includes/msconame-md.md)] . También puede utilizar visores de complemento si están disponibles.  
  
 **Acercar**  
 Acerque para obtener una vista más detallada de los nodos y bifurcaciones del árbol de decisión. En un modelo complejo, los árboles de decisión pueden tener muchos niveles de bifurcación.  
  
 **Alejar**  
 Aleje para obtener una vista global de la estructura de árbol.  
  
 **Copiar vista del gráfico**  
 Copie la sección visible del diagrama en el portapapeles.  
  
 **Copiar todo el gráfico**  
 Copie el diagrama completo en el portapapeles.  
  
 **Ajustar diagrama a la ventana**  
 Aleje el diagrama hasta que toda la estructura de árbol se ajuste a la pantalla.  
  
 **Histogramas**  
 Seleccione el número de estados que pueden aparecer en el histograma para cada nodo. Si el número de estados del modelo es menor que el valor seleccionado, no se muestra ninguna barra adicional.  
  
 **Árbol**  
 Elija un árbol para mostrarlo en el visor. Si crea un modelo que tiene varios atributos de predicción, el algoritmo creará un árbol independiente para cada atributo de predicción.  
  
 **Información previa**  
 Elija un valor del atributo de predicción para utilizarlo a la hora de representar el color de fondo de cada nodo. Así, en los modelos de ejemplo de AdventureWorks, si establece **Background** en 1 ([Bike Buyer] = Yes), los nodos se sombrean más si tienen una proporción mayor de compradores de bicicletas. Esta opción proporciona una indicación visual adicional sobre el significado de las bifurcaciones y nodos del árbol.  
  
 **Expansión predeterminada**  
 Elija un valor de la lista para establecer el valor predeterminado del número de niveles que se muestra en el gráfico de árbol.  
  
 **Mostrar nivel**  
 Mueva la barra deslizante a la derecha o izquierda para ajustar el número de niveles que se muestran en el gráfico de árbol. Para ver todos los nodos del modelo, deslice la barra hasta el extremo derecho.  
  
## <a name="see-also"></a>Vea también  
 [Algoritmos de minería de datos &#40;Analysis Services: Minería de datos&#41;](data-mining/data-mining-algorithms-analysis-services-data-mining.md)   
 [Visores de modelos de minería de datos &#40;Diseñador de modelos de minería de datos&#41;](mining-model-viewers-data-mining-model-designer.md)   
 [Visores de modelos de minería de datos](data-mining/data-mining-model-viewers.md)  
  
  
