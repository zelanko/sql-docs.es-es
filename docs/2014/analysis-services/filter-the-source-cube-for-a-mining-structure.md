---
title: Filtrar el cubo de origen para una estructura de minería de datos | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- slice cubes [Analysis Services]
- mining structures [Analysis Services], filtering source cube
- cubes [Analysis Services], slicing
- filtering data [Analysis Services]
ms.assetid: 05dce7e1-2fe5-4500-bacf-c1a8a76e1424
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 74220f2385e27484c5cc511c84be5625290a28db
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/26/2020
ms.locfileid: "66081149"
---
# <a name="filter-the-source-cube-for-a-mining-structure"></a>Filtrar el cubo de origen para una estructura de minería de datos
  Al crear una estructura de minería de datos que se basa en los datos de un modelo multidimensional (un cubo OLAP), puede *segmentar* el cubo en el que se basa la estructura de minería de datos. La segmentación permite crear subconjuntos de datos, como un tipo de filtro en los datos que se utilizan para entrenar el modelo de minería de datos.  
  
### <a name="to-slice-a-cube"></a>Para segmentar un cubo  
  
1.  En el diseñador de minería [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)]de datos de, seleccione la pestaña **estructura de minería** de datos o la pestaña **modelos de minería** de datos.  
  
2.  En el menú **modelo de minería de datos** , seleccione **definir segmento de cubo de estructura de minería de datos**.  
  
     Se abre el cuadro de diálogo **segmentar cubo** .  
  
3.  En la columna **dimensión** del cuadro de diálogo **segmentar el cubo** , seleccione la dimensión que desea filtrar.  
  
4.  Seleccione un nivel de una jerarquía mediante la lista de la columna **jerarquía** .  
  
5.  Seleccione un operador en la lista de la columna **operador** para usarlo en la creación de la condición de filtro.  
  
6.  Haga clic en el cuadro de la columna **filtro** .  
  
     Se abre un cuadro de diálogo que contiene todos los miembros del nivel especificado de la jerarquía.  
  
7.  Seleccione el miembro o los miembros en los que desee filtrar.  
  
8.  Haga clic en **Aceptar** en el cuadro de diálogo miembro.  
  
9. Haga clic en **Aceptar** en el cuadro de diálogo **segmentar cubo** .  
  
     El cubo de origen se filtrará tal y como define el segmento del cubo.  
  
## <a name="see-also"></a>Consulte también  
 [Tareas y procedimientos de la estructura de minería de datos](data-mining/mining-structure-tasks-and-how-tos.md)   
 [Crear una estructura de minería de datos OLAP](data-mining/create-a-new-olap-mining-structure.md)  
  
  
