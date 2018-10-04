---
title: Filtrar el cubo de origen para una estructura de minería de datos | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
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
ms.openlocfilehash: 5c7d3208729ec225c25d1616e7a2052245e6ed25
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/02/2018
ms.locfileid: "48123535"
---
# <a name="filter-the-source-cube-for-a-mining-structure"></a>Filtrar el cubo de origen para una estructura de minería de datos
  Cuando se crea una estructura de minería de datos que se basa en datos en un modelo multidimensional (un cubo OLAP), puede *segmento* el cubo que se basa la estructura de minería de datos. La segmentación permite crear subconjuntos de datos, como un tipo de filtro en los datos que se utilizan para entrenar el modelo de minería de datos.  
  
### <a name="to-slice-a-cube"></a>Para segmentar un cubo  
  
1.  En el Diseñador de minería de datos en [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)], seleccione el **Mining Structure** ficha o el **modelos de minería de datos** ficha.  
  
2.  En el **Mining Model** menú, seleccione **definir segmento de cubo de estructura de minería de datos**.  
  
     El **segmentar el cubo** abre el cuadro de diálogo.  
  
3.  En el **dimensión** columna de la **segmentar el cubo** cuadro de diálogo, seleccione la dimensión que desea filtrar.  
  
4.  Seleccione un nivel de una jerarquía, con la lista en el **jerarquía** columna.  
  
5.  Seleccione un operador en la lista en el **operador** columna desea utilizar para generar la condición de filtro.  
  
6.  Haga clic en el cuadro el **filtro** columna.  
  
     Se abre un cuadro de diálogo que contiene todos los miembros del nivel especificado de la jerarquía.  
  
7.  Seleccione el miembro o los miembros en los que desee filtrar.  
  
8.  Haga clic en **Aceptar** en el cuadro de diálogo de miembro.  
  
9. Haga clic en **Aceptar** en el **segmentar el cubo** cuadro de diálogo.  
  
     El cubo de origen se filtrará tal y como define el segmento del cubo.  
  
## <a name="see-also"></a>Vea también  
 [Tareas de estructura de minería de datos y procedimientos](data-mining/mining-structure-tasks-and-how-tos.md)   
 [Crear una estructura de minería de datos OLAP](data-mining/create-a-new-olap-mining-structure.md)  
  
  
