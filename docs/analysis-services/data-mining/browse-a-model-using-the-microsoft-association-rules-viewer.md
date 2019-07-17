---
title: Examinar un modelo usando el Visor de reglas de asociación de Microsoft | Microsoft Docs
ms.date: 05/01/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: data-mining
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: bc244667df41f625084c9d436d30652491e4b3dc
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "68210185"
---
# <a name="browse-a-model-using-the-microsoft-association-rules-viewer"></a>Examinar un modelo usando el Visor de reglas de asociación de Microsoft
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  El Visor de reglas de asociación de [!INCLUDE[msCoName](../../includes/msconame-md.md)] en [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] muestra los modelos de minería de datos que se generan con el algoritmo de asociación de [!INCLUDE[msCoName](../../includes/msconame-md.md)] . Este algoritmo de [!INCLUDE[msCoName](../../includes/msconame-md.md)] es un algoritmo de asociación que se utiliza para crear modelos de minería de datos con el fin de realizar análisis de la cesta de la compra. Para obtener más información acerca de este algoritmo, vea [Microsoft Association Algorithm](../../analysis-services/data-mining/microsoft-association-algorithm.md).  
  
 A continuación se exponen las principales razones para utilizar el algoritmo de asociación de [!INCLUDE[msCoName](../../includes/msconame-md.md)] :  
  
-   Para buscar conjuntos de elementos que describen elementos que normalmente se encuentran juntos en una transacción.  
  
-   Para detectar reglas que predicen la presencia de otros elementos en una transacción en función de elementos existentes.  
  
> [!NOTE]  
>  Para ver información detallada sobre las ecuaciones utilizadas en el modelo y los modelos que se detectaron, utilice el Visor de árbol de contenido genérico de [!INCLUDE[msCoName](../../includes/msconame-md.md)] . Para obtener más información, vea [Examinar un modelo usando el Visor de árbol de contenido genérico de Microsoft](../../analysis-services/data-mining/browse-a-model-using-the-microsoft-generic-content-tree-viewer.md) o [Visor de árbol de contenido genérico de Microsoft &#40;Minería de datos&#41;](http://msdn.microsoft.com/library/751b4393-f6fd-48c1-bcef-bdca589ce34c).  
  
 Para ver un tutorial sobre cómo crear, explorar y usar un modelo de minería de datos de asociación, vea [lección 3: Generar un escenario de cesta &#40;intermedio de Tutorial de minería de datos&#41;](http://msdn.microsoft.com/library/651eef38-772e-4d97-af51-075b1b27fc5a).  
  
##  <a name="BKMK_ViewerTabs"></a> Fichas del visor  
 Cuando se explora un modelo de minería de datos en [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)], el modelo aparece en la pestaña **Visor de modelos de minería de datos** del visor del diseñador de minería de datos apropiado para el modelo. El Visor de reglas de asociación de [!INCLUDE[msCoName](../../includes/msconame-md.md)] incluye las siguientes pestañas:  
  
-   [Conjuntos de elementos](#BKMK_Itemsets)  
  
-   [Reglas](#BKMK_Rules)  
  
-   [Red de dependencias](#BKMK_Dependency)  
  
 Cada pestaña contiene la casilla **Mostrar nombre largo** , que puede utilizar para ocultar o mostrar la tabla desde la que se origina el conjunto de elementos en la regla o el conjunto de elementos.  
  
###  <a name="BKMK_Itemsets"></a> Conjuntos de elementos  
 La pestaña **Conjuntos de elementos** muestra una lista de los conjuntos de elementos que el modelo identifica como encontrados juntos con frecuencia. La pestaña muestra una cuadrícula con las siguientes columnas: **Compatibilidad con**, **tamaño**, y **conjunto de elementos**. Para obtener más información sobre el soporte, vea [Microsoft Association Algorithm](../../analysis-services/data-mining/microsoft-association-algorithm.md). La columna **Tamaño** muestra el número de elementos del conjunto de elementos. La columna **Conjunto de elementos** muestra el conjunto de elementos real que ha descubierto el modelo. Puede controlar el formato del conjunto de elementos mediante la lista **Mostrar** , en la que puede establecer las siguientes opciones:  
  
-   **Mostrar el valor y el nombre del atributo**  
  
-   **Mostrar solo el valor del atributo**  
  
-   **Mostrar solo el nombre del atributo**  
  
 Puede filtrar el número de conjuntos de elementos que se muestran en la pestaña utilizando **Soporte mínimo** y **Tamaño mínimo del conjunto de elementos**. Puede limitar aún más el número de conjuntos de elementos que se muestran utilizando **Filtrar conjunto de elementos** y especificando una característica que debe tener el conjunto de elementos. Por ejemplo, si escribe "Water Bottle = existing", puede limitar los conjuntos de elementos a los que contengan una botella de agua. La opción **Filtrar conjunto de elementos** también muestra una lista de los filtros que ha usado anteriormente.  
  
 Puede ordenar las filas de la cuadrícula haciendo clic en un encabezado de columna.  
  
 [Volver al principio](#BKMK_ViewerTabs)  
  
###  <a name="BKMK_Rules"></a> Reglas  
 La ficha **Reglas** muestra las reglas que ha descubierto el algoritmo de asociación. El **reglas** ficha incluye una cuadrícula que contiene las siguientes columnas: **Probabilidad**, **importancia**, y **regla**. La primera columna describe la probabilidad de que se produzca el resultado de una regla. La importancia está diseñada para medir la utilidad de una regla. Aunque la probabilidad de que una regla se cumpla puede ser alta, puede que la utilidad de la propia regla no sea muy importante. Ésta es la finalidad de la columna de importancia. Por ejemplo, si cada conjunto de elementos contiene un estado específico de un atributo, una regla que predice el estado no será muy significativa, aunque la probabilidad sea muy alta. Cuando mayor sea la importancia, más importante será la regla.  
  
 Puede utilizar las opciones **Probabilidad mínima** e **Importancia mínima** para filtrar las reglas. Es un proceso similar al filtro que se puede aplicar en la pestaña **Conjuntos de elementos** . También puede utilizar **Regla del filtro** para filtrar una regla en función de los estados de los atributos que contiene.  
  
 Puede ordenar las filas de la cuadrícula haciendo clic en un encabezado de columna.  
  
 [Volver al principio](#BKMK_ViewerTabs)  
  
###  <a name="BKMK_Dependency"></a> Red de dependencias  
 La pestaña **Red de dependencias** incluye un visor de redes de dependencias. Cada nodo del visor representa un elemento, por ejemplo, "state = WA". La flecha entre los nodos representa la asociación entre los elementos. La dirección de la flecha indica la asociación entre los elementos según las reglas que haya descubierto el algoritmo. Por ejemplo, si el Visor contiene tres elementos, A, B y C y C lo predicen A y B, si selecciona el nodo C, dos flechas señalarán hacia el nodo C - A C y B a C.  
  
 El control deslizante de la izquierda del visor actúa como un filtro vinculado a la probabilidad de las reglas. Si desplaza el control deslizante hacia abajo, sólo se verán los vínculos más similares.  
  
 [Volver al principio](#BKMK_ViewerTabs)  
  
## <a name="see-also"></a>Vea también  
 [Microsoft Association Algorithm](../../analysis-services/data-mining/microsoft-association-algorithm.md)   
 [Tareas y procedimientos del Visor de modelos de minería de datos](../../analysis-services/data-mining/mining-model-viewer-tasks-and-how-tos.md)   
 [Tareas y procedimientos del Visor de modelos de minería de datos](../../analysis-services/data-mining/mining-model-viewer-tasks-and-how-tos.md)   
 [Herramientas de minería de datos](../../analysis-services/data-mining/data-mining-tools.md)   
 [Visores de modelos de minería de datos](../../analysis-services/data-mining/data-mining-model-viewers.md)  
  
  
