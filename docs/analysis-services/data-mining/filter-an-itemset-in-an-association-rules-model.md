---
title: Filtro de modelo de reglas de un conjunto de elementos en una asociación | Microsoft Docs
ms.date: 05/08/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: data-mining
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 8cb507be05ae8f8ad3b25b386d55785c966f14f7
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "68183234"
---
# <a name="filter-an-itemset-in-an-association-rules-model"></a>Filtrar un conjunto de elementos en un modelo de reglas de asociación
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  En [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)], puede filtrar los conjuntos de elementos que se muestran en la pestaña **Conjuntos de elementos** del Visor de reglas de asociación de [!INCLUDE[msCoName](../../includes/msconame-md.md)] .  
  
### <a name="to-filter-an-itemset"></a>Para filtrar un conjunto de elementos  
  
1.  En la pestaña **Visor de modelos de minería de datos** del Diseñador de minería de datos de [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)], haga clic en la pestaña **Conjuntos de elementos** del **Visor de reglas de asociación**.  
  
2.  Escriba una condición de regla en el cuadro **Filtrar conjunto de elementos** . Por ejemplo, una condición de regla podría ser "Touring-1000 = existing"  
  
3.  Haga clic en **Entrar**.  
  
 Los conjuntos de elementos se filtrarán para mostrar únicamente los conjuntos de elementos que contienen los elementos seleccionados. El cuadro no distingue entre mayúsculas y minúsculas. Los filtros se almacenan en memoria para permitir la selección de un filtro antiguo de la lista.  
  
## <a name="see-also"></a>Vea también  
 [Tareas y procedimientos del Visor de modelos de minería de datos](../../analysis-services/data-mining/mining-model-viewer-tasks-and-how-tos.md)  
  
  
