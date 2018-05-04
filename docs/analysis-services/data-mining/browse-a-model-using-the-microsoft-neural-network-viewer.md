---
title: Examinar un modelo usando el Visor de red neuronal de Microsoft | Documentos de Microsoft
ms.date: 05/01/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: data-mining
ms.topic: article
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: ba0f41f182eaa2d96ce771373b8abba4d863d619
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="browse-a-model-using-the-microsoft-neural-network-viewer"></a>Examinar un modelo usando el Visor de redes neuronales de Microsoft
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  El Visor de redes neuronales de [!INCLUDE[msCoName](../../includes/msconame-md.md)] en [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] muestra los modelos de minería de datos que se generan con el algoritmo de Red neuronal de [!INCLUDE[msCoName](../../includes/msconame-md.md)] . El algoritmo de red neuronal de [!INCLUDE[msCoName](../../includes/msconame-md.md)] crea modelos de minería de datos de regresión y de clasificación que pueden analizar entradas y salidas múltiples, y es muy útil para los análisis de final abierto y la exploración. Para obtener más información acerca de este algoritmo, vea [Microsoft Neural Network Algorithm](../../analysis-services/data-mining/microsoft-neural-network-algorithm.md).  
  
 Cuando se explora un modelo usando el Visor de redes neuronales de [!INCLUDE[msCoName](../../includes/msconame-md.md)] , se suele elegir un determinado atributo y estado de destino, y después se usa el visor para ver cómo afectan al resultado los atributos de entrada.  
  
 Por ejemplo, suponga que conoce estos hechos sobre una clase de clientes potenciales:  
  
-   Mediana edad (40 a 50 años).  
  
-   Tiene casa en propiedad.  
  
-   Tiene dos hijos que todavía viven en casa.  
  
 ¿Cómo puede correlacionar estos atributos con la probabilidad de que el cliente haga una compra?  
  
 Mediante la construcción de un modelo de red neuronal que use los hábitos de compra como resultado de destino, puede explorar diversas combinaciones de atributos del cliente, tales como ingresos altos, y descubrir qué combinación de atributos es más probable que influya en los hábitos de compra. Por ejemplo, puede que descubra que el factor determinante es la distancia entre su domicilio y el trabajo.  
  
 Si necesita información más detallada, como las ecuaciones que representan cada patrón descubierto, puede cambiar de vista y usar el Visor de árbol de contenido genérico de [!INCLUDE[msCoName](../../includes/msconame-md.md)] . Para más información, vea [Examinar un modelo usando el Visor de árbol de contenido genérico de Microsoft](../../analysis-services/data-mining/browse-a-model-using-the-microsoft-generic-content-tree-viewer.md) o [Visor de árbol de contenido genérico de Microsoft &#40;Minería de datos&#41;](http://msdn.microsoft.com/library/751b4393-f6fd-48c1-bcef-bdca589ce34c).  
  
##  <a name="BKMK_ViewerTabs"></a> Fichas del visor  
 Cuando se explora un modelo de minería de datos en [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)], el modelo aparece en la pestaña **Visor de modelos de minería de datos** del visor del diseñador de minería de datos apropiado para el modelo. El Visor de redes neuronales de [!INCLUDE[msCoName](../../includes/msconame-md.md)] ofrece las siguientes pestañas para usarlas con el fin de explorar modelos de minería de datos de redes neuronales:  
  
-   [Entradas](#BKMK_Inputs)  
  
-   [Salidas](#BKMK_Outputs)  
  
-   [Variables](#BKMK_Characteristics)  
  
###  <a name="BKMK_Inputs"></a> Entradas  
 Use la pestaña **Entradas** para elegir los atributos y los valores que usará el modelo como entradas. De forma predeterminada, el visor se abre con todos los atributos incluidos. En esta vista predeterminada, el modelo elige qué valores de los atributos son los más importantes que se van a mostrar.  
  
 Para seleccionar un atributo de entrada, haga clic en la columna **Atributo** de la cuadrícula **Entrada** y, después, seleccione un atributo de la lista desplegable. (En la lista solo están incluidos los atributos presentes en el modelo).  
  
 El primer valor distinto aparece en la columna **Valor** . Si hace clic en el valor predeterminado aparece una lista que contiene los posibles estados del atributo asociado. Puede seleccionar el estado que desea investigar. Puede seleccionar tantos atributos como desee.  
  
 [Volver al principio](#BKMK_ViewerTabs)  
  
###  <a name="BKMK_Outputs"></a> Salidas  
 Use la pestaña **Salidas** para elegir el atributo de resultados que se debe investigar. Puede elegir dos estados resultantes cualesquiera para compararlos, suponiendo que las columnas se definieron como atributos de predicción cuando se creó el modelo.  
  
 Use la lista **Atributo de salida** para seleccionar un atributo. Después puede seleccionar dos estados asociados con el atributo en las listas **Valor 1** y **Valor 2** . Estos dos estados del atributo de salida se compararán en el panel **Variables** .  
  
 [Volver al principio](#BKMK_ViewerTabs)  
  
###  <a name="BKMK_Characteristics"></a> Variables  
 La cuadrícula de la pestaña **Variables** contiene las columnas siguientes: **Atributo**, **Valor**, **Favorece [valor 1]** y **Favorece [valor 2]**. De forma predeterminada, las columnas se ordenan por la intensidad de **Favorece [valor 1]**. Si hace clic en un encabezado de columna, cambia el orden de la columna seleccionada.  
  
 Una barra a la derecha del atributo muestra el estado del atributo de entrada que el estado del atributo de salida favorece. El tamaño de la barra muestra la intensidad con la que el estado de salida favorece al estado de entrada.  
  
 [Volver al principio](#BKMK_ViewerTabs)  
  
## <a name="see-also"></a>Vea también  
 [Algoritmo de red neuronal de Microsoft](../../analysis-services/data-mining/microsoft-neural-network-algorithm.md)   
 [Tareas y tareas del Visor de modelo de minería de datos](../../analysis-services/data-mining/mining-model-viewer-tasks-and-how-tos.md)   
 [Tareas y tareas del Visor de modelo de minería de datos](../../analysis-services/data-mining/mining-model-viewer-tasks-and-how-tos.md)   
 [Herramientas de minería de datos](../../analysis-services/data-mining/data-mining-tools.md)   
 [Visores de modelos de minería de datos](../../analysis-services/data-mining/data-mining-model-viewers.md)  
  
  
