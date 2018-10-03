---
title: Examinar un modelo usando el Visor de reglas de asociación de Microsoft | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
helpviewer_keywords:
- itemsets [Analysis Services]
- mining models [Analysis Services], associations
- mining model content, viewing
- rules [Data Mining]
- Association Rules Viewer [Analysis Services]
- market basket analysis [Analysis Services]
- associations [Analysis Services]
- Microsoft Association Rules Viewer
- dependencies [Analysis Services]
ms.assetid: 538fc01b-8eb1-467a-9b66-3cd57cf7489f
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: bc86d962a978990d9b4e29323d10c53dd9b805a8
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/02/2018
ms.locfileid: "48206845"
---
# <a name="browse-a-model-using-the-microsoft-association-rules-viewer"></a>Examinar un modelo usando el Visor de reglas de asociación de Microsoft
  El Visor de reglas de asociación de [!INCLUDE[msCoName](../../includes/msconame-md.md)] en [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] muestra los modelos de minería de datos que se generan con el algoritmo de asociación de [!INCLUDE[msCoName](../../includes/msconame-md.md)] . Este algoritmo de [!INCLUDE[msCoName](../../includes/msconame-md.md)] es un algoritmo de asociación que se utiliza para crear modelos de minería de datos con el fin de realizar análisis de la cesta de la compra. Para obtener más información acerca de este algoritmo, vea [Microsoft Association Algorithm](microsoft-association-algorithm.md).  
  
 A continuación se exponen las principales razones para utilizar el algoritmo de asociación de [!INCLUDE[msCoName](../../includes/msconame-md.md)] :  
  
-   Para buscar conjuntos de elementos que describen elementos que normalmente se encuentran juntos en una transacción.  
  
-   Para detectar reglas que predicen la presencia de otros elementos en una transacción en función de elementos existentes.  
  
> [!NOTE]  
>  Para ver información detallada sobre las ecuaciones utilizadas en el modelo y los modelos que se detectaron, utilice el Visor de árbol de contenido genérico de [!INCLUDE[msCoName](../../includes/msconame-md.md)] . Para obtener más información, vea [Examinar un modelo usando el Visor de árbol de contenido genérico de Microsoft](browse-a-model-using-the-microsoft-generic-content-tree-viewer.md) o [Visor de árbol de contenido genérico de Microsoft &#40;Minería de datos&#41;](../microsoft-generic-content-tree-viewer-data-mining.md).  
  
 Para consultar un tutorial que muestre cómo crear, explorar y usar un modelo de minería de datos de asociación, vea [Lección 3: Generar un escenario de cesta de la compra &#40;Tutorial intermedio de minería de datos&#41;](../../tutorials/lesson-3-building-a-market-basket-scenario-intermediate-data-mining-tutorial.md).  
  
##  <a name="BKMK_ViewerTabs"></a> Fichas del visor  
 Cuando se explora un modelo de minería de datos en [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)], el modelo aparece en la pestaña **Visor de modelos de minería de datos** del visor del diseñador de minería de datos apropiado para el modelo. El Visor de reglas de asociación de [!INCLUDE[msCoName](../../includes/msconame-md.md)] incluye las siguientes pestañas:  
  
-   [Conjuntos de elementos](#BKMK_Itemsets)  
  
-   [Reglas](#BKMK_Rules)  
  
-   [Red de dependencias](#BKMK_Dependency)  
  
 Cada pestaña contiene la casilla **Mostrar nombre largo** , que puede utilizar para ocultar o mostrar la tabla desde la que se origina el conjunto de elementos en la regla o el conjunto de elementos.  
  
###  <a name="BKMK_Itemsets"></a> Conjuntos de elementos  
 La pestaña **Conjuntos de elementos** muestra una lista de los conjuntos de elementos que el modelo identifica como encontrados juntos con frecuencia. La pestaña muestra una cuadrícula con las columnas siguientes: **Soporte**, **Tamaño**y **Conjunto de elementos**. Para obtener más información sobre el soporte, vea [Microsoft Association Algorithm](microsoft-association-algorithm.md). La columna **Tamaño** muestra el número de elementos del conjunto de elementos. La columna **Conjunto de elementos** muestra el conjunto de elementos real que ha descubierto el modelo. Puede controlar el formato del conjunto de elementos mediante la lista **Mostrar** , en la que puede establecer las siguientes opciones:  
  
-   **Mostrar el valor y el nombre del atributo**  
  
-   **Mostrar solo el valor del atributo**  
  
-   **Mostrar solo el nombre del atributo**  
  
 Puede filtrar el número de conjuntos de elementos que se muestran en la pestaña utilizando **Soporte mínimo** y **Tamaño mínimo del conjunto de elementos**. Puede limitar aún más el número de conjuntos de elementos que se muestran utilizando **Filtrar conjunto de elementos** y especificando una característica que debe tener el conjunto de elementos. Por ejemplo, si escribe "Water Bottle = existing", puede limitar los conjuntos de elementos a los que contengan una botella de agua. La opción **Filtrar conjunto de elementos** también muestra una lista de los filtros que ha usado anteriormente.  
  
 Puede ordenar las filas de la cuadrícula haciendo clic en un encabezado de columna.  
  
 [Volver al principio](#BKMK_ViewerTabs)  
  
###  <a name="BKMK_Rules"></a> Reglas  
 La ficha **Reglas** muestra las reglas que ha descubierto el algoritmo de asociación. La ficha **Reglas** incluye una cuadrícula que contiene las siguientes columnas: **Probabilidad**, **Importancia**y **Regla**. La primera columna describe la probabilidad de que se produzca el resultado de una regla. La importancia está diseñada para medir la utilidad de una regla. Aunque la probabilidad de que una regla se cumpla puede ser alta, puede que la utilidad de la propia regla no sea muy importante. Ésta es la finalidad de la columna de importancia. Por ejemplo, si cada conjunto de elementos contiene un estado específico de un atributo, una regla que predice el estado no será muy significativa, aunque la probabilidad sea muy alta. Cuando mayor sea la importancia, más importante será la regla.  
  
 Puede utilizar las opciones **Probabilidad mínima** e **Importancia mínima** para filtrar las reglas. Es un proceso similar al filtro que se puede aplicar en la pestaña **Conjuntos de elementos** . También puede utilizar **Regla del filtro** para filtrar una regla en función de los estados de los atributos que contiene.  
  
 Puede ordenar las filas de la cuadrícula haciendo clic en un encabezado de columna.  
  
 [Volver al principio](#BKMK_ViewerTabs)  
  
###  <a name="BKMK_Dependency"></a> Red de dependencias  
 La pestaña **Red de dependencias** incluye un visor de redes de dependencias. Cada nodo del visor representa un elemento, por ejemplo, "state = WA". La flecha entre los nodos representa la asociación entre los elementos. La dirección de la flecha indica la asociación entre los elementos según las reglas que haya descubierto el algoritmo. Por ejemplo, si el visor contiene tres elementos, A, B y C, y C lo predicen A y B, si selecciona el nodo C, dos flechas señalarán hacia el nodo C: de A a C y de B a C.  
  
 El control deslizante de la izquierda del visor actúa como un filtro vinculado a la probabilidad de las reglas. Si desplaza el control deslizante hacia abajo, sólo se verán los vínculos más similares.  
  
 [Volver al principio](#BKMK_ViewerTabs)  
  
## <a name="see-also"></a>Vea también  
 [Algoritmo de asociación de Microsoft](microsoft-association-algorithm.md)   
 [Tareas del Visor de modelo de minería de datos y procedimientos](mining-model-viewer-tasks-and-how-tos.md)   
 [Tareas del Visor de modelo de minería de datos y procedimientos](mining-model-viewer-tasks-and-how-tos.md)   
 [Herramientas de minería de datos](data-mining-tools.md)   
 [Visores de modelos de minería de datos](data-mining-model-viewers.md)  
  
  
