---
title: Filtro de modelo de reglas de un conjunto de elementos en una asociación | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
helpviewer_keywords:
- itemsets [Analysis Services]
- filtering itemsets [Analysis Services]
- Mining Model Viewer [Analysis Services], itemsets
ms.assetid: 3ed919ea-8598-45d2-a4a0-b1b3357a4ab1
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 42f1ed629413bd68f01abd12679907f58d204a78
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "62722507"
---
# <a name="filter-an-itemset-in-an-association-rules-model"></a>Filtrar un conjunto de elementos en un modelo de reglas de asociación
  En [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)], puede filtrar los conjuntos de elementos que se muestran en la pestaña **Conjuntos de elementos** del Visor de reglas de asociación de [!INCLUDE[msCoName](../../includes/msconame-md.md)] .  
  
### <a name="to-filter-an-itemset"></a>Para filtrar un conjunto de elementos  
  
1.  En la pestaña **Visor de modelos de minería de datos** del Diseñador de minería de datos de [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)], haga clic en la pestaña **Conjuntos de elementos** del **Visor de reglas de asociación**.  
  
2.  Escriba una condición de regla en el cuadro **Filtrar conjunto de elementos** . Por ejemplo, una condición de regla podría ser "Touring-1000 = existing"  
  
3.  Haga clic en **Entrar**.  
  
 Los conjuntos de elementos se filtrarán para mostrar únicamente los conjuntos de elementos que contienen los elementos seleccionados. El cuadro no distingue entre mayúsculas y minúsculas. Los filtros se almacenan en memoria para permitir la selección de un filtro antiguo de la lista.  
  
## <a name="see-also"></a>Vea también  
 [Tareas y procedimientos del Visor de modelos de minería de datos](mining-model-viewer-tasks-and-how-tos.md)  
  
  
