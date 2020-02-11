---
title: Examinar un modelo mediante el visor de red neuronal de Microsoft | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- mining model content, viewing
- classification mining model [Analysis Services]
- Microsoft Neural Network Viewer
- regression algorithms [Analysis Services]
- Neural Network Viewer [Analysis Services]
- neural network model [Analysis Services]
ms.assetid: 2343d746-c4f4-499b-9d3c-17d63310a9a3
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 1628eff6e5c440071126ce3508b977f9f7508ba5
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "66086056"
---
# <a name="browse-a-model-using-the-microsoft-neural-network-viewer"></a>Examinar un modelo usando el Visor de redes neuronales de Microsoft
  El [!INCLUDE[msCoName](../../includes/msconame-md.md)] visor de red neuronal [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] de muestra los modelos de minería de datos [!INCLUDE[msCoName](../../includes/msconame-md.md)] que se generan con el algoritmo de red neuronal de. El algoritmo de red neuronal de [!INCLUDE[msCoName](../../includes/msconame-md.md)] crea modelos de minería de datos de regresión y de clasificación que pueden analizar entradas y salidas múltiples, y es muy útil para los análisis de final abierto y la exploración. Para obtener más información acerca de este algoritmo, vea [Microsoft Neural Network Algorithm](microsoft-neural-network-algorithm.md).  
  
 Cuando se explora un modelo usando el Visor de redes neuronales de [!INCLUDE[msCoName](../../includes/msconame-md.md)] , se suele elegir un determinado atributo y estado de destino, y después se usa el visor para ver cómo afectan al resultado los atributos de entrada.  
  
 Por ejemplo, suponga que conoce estos hechos sobre una clase de clientes potenciales:  
  
-   Mediana edad (40 a 50 años).  
  
-   Tiene casa en propiedad.  
  
-   Tiene dos hijos que todavía viven en casa.  
  
 ¿Cómo puede correlacionar estos atributos con la probabilidad de que el cliente haga una compra?  
  
 Mediante la construcción de un modelo de red neuronal que use los hábitos de compra como resultado de destino, puede explorar diversas combinaciones de atributos del cliente, tales como ingresos altos, y descubrir qué combinación de atributos es más probable que influya en los hábitos de compra. Por ejemplo, puede que descubra que el factor determinante es la distancia entre su domicilio y el trabajo.  
  
 Si necesita información más detallada, como las ecuaciones que representan cada patrón descubierto, puede cambiar de vista y usar el Visor de árbol de contenido genérico de [!INCLUDE[msCoName](../../includes/msconame-md.md)] . Para obtener más información, vea [Examinar un modelo usando el Visor de árbol de contenido genérico de Microsoft](browse-a-model-using-the-microsoft-generic-content-tree-viewer.md) o [Visor de árbol de contenido genérico de Microsoft &#40;Minería de datos&#41;](../microsoft-generic-content-tree-viewer-data-mining.md).  
  
##  <a name="BKMK_ViewerTabs"></a>Pestañas del visor  
 Cuando se explora un modelo de minería de datos en [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)], el modelo aparece en la pestaña **Visor de modelos de minería de datos** del visor del diseñador de minería de datos apropiado para el modelo. El Visor de redes neuronales de [!INCLUDE[msCoName](../../includes/msconame-md.md)] ofrece las siguientes pestañas para usarlas con el fin de explorar modelos de minería de datos de redes neuronales:  
  
-   [Entradas](#BKMK_Inputs)  
  
-   [Salidas](#BKMK_Outputs)  
  
-   [Variables](#BKMK_Characteristics)  
  
###  <a name="BKMK_Inputs"></a>Comentarios  
 Use la pestaña **Entradas** para elegir los atributos y los valores que usará el modelo como entradas. De forma predeterminada, el visor se abre con todos los atributos incluidos. En esta vista predeterminada, el modelo elige qué valores de los atributos son los más importantes que se van a mostrar.  
  
 Para seleccionar un atributo de entrada, haga clic en la columna **Atributo** de la cuadrícula **Entrada** y, después, seleccione un atributo de la lista desplegable. (En la lista solo están incluidos los atributos presentes en el modelo).  
  
 El primer valor distinto aparece en la columna **Valor** . Si hace clic en el valor predeterminado aparece una lista que contiene los posibles estados del atributo asociado. Puede seleccionar el estado que desea investigar. Puede seleccionar tantos atributos como desee.  
  
 [Volver al principio](#BKMK_ViewerTabs)  
  
###  <a name="BKMK_Outputs"></a>Salidas  
 Use la pestaña **Salidas** para elegir el atributo de resultados que se debe investigar. Puede elegir dos estados resultantes cualesquiera para compararlos, suponiendo que las columnas se definieron como atributos de predicción cuando se creó el modelo.  
  
 Use la lista **Atributo de salida** para seleccionar un atributo. Después puede seleccionar dos estados asociados con el atributo en las listas **Valor 1** y **Valor 2** . Estos dos estados del atributo de salida se compararán en el panel **Variables** .  
  
 [Volver al principio](#BKMK_ViewerTabs)  
  
###  <a name="BKMK_Characteristics"></a>Variable  
 La cuadrícula de la pestaña **Variables** contiene las columnas siguientes: **Atributo**, **Valor**, **Favorece [valor 1]** y **Favorece [valor 2]**. De forma predeterminada, las columnas se ordenan por la intensidad de **Favorece [valor 1]**. Si hace clic en un encabezado de columna, cambia el orden de la columna seleccionada.  
  
 Una barra a la derecha del atributo muestra el estado del atributo de entrada que el estado del atributo de salida favorece. El tamaño de la barra muestra la intensidad con la que el estado de salida favorece al estado de entrada.  
  
 [Volver al principio](#BKMK_ViewerTabs)  
  
## <a name="see-also"></a>Consulte también  
 [Algoritmo de red neuronal de Microsoft](microsoft-neural-network-algorithm.md)   
 [Tareas y procedimientos del visor de modelos de minería de datos](mining-model-viewer-tasks-and-how-tos.md)   
 [Tareas y procedimientos del visor de modelos de minería de datos](mining-model-viewer-tasks-and-how-tos.md)   
 [Herramientas de minería de datos](data-mining-tools.md)   
 [Visores de modelos de minería de datos](data-mining-model-viewers.md)  
  
  
