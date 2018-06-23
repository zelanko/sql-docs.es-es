---
title: Filtrar el cubo de origen para una estructura de minería de datos | Documentos de Microsoft
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- slice cubes [Analysis Services]
- mining structures [Analysis Services], filtering source cube
- cubes [Analysis Services], slicing
- filtering data [Analysis Services]
ms.assetid: 05dce7e1-2fe5-4500-bacf-c1a8a76e1424
caps.latest.revision: 15
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: ed1ff70d4bb0f0ebd20da468c91f2603318ec217
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36197497"
---
# <a name="filter-the-source-cube-for-a-mining-structure"></a>Filtrar el cubo de origen para una estructura de minería de datos
  Cuando se crea una estructura de minería de datos que se basa en datos en un modelo multidimensional (un cubo OLAP), también puede *segmento* el cubo que se basa la estructura de minería de datos. La segmentación permite crear subconjuntos de datos, como un tipo de filtro en los datos que se utilizan para entrenar el modelo de minería de datos.  
  
### <a name="to-slice-a-cube"></a>Para segmentar un cubo  
  
1.  En el Diseñador de minería de datos en [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)], seleccione la **estructura de minería de datos** ficha o el **modelos de minería de datos** ficha.  
  
2.  En el **Mining Model** menú, seleccione **definir segmento de cubo de estructura de minería de datos**.  
  
     El **segmentar el cubo** abre el cuadro de diálogo.  
  
3.  En el **dimensión** columna de la **segmentar el cubo** cuadro de diálogo, seleccione la dimensión que desea filtrar.  
  
4.  Seleccione un nivel de una jerarquía, con la lista en la **jerarquía** columna.  
  
5.  Seleccione un operador en la lista en la **operador** columna, desea utilizar para generar la condición de filtro.  
  
6.  Haga clic en el cuadro en el **filtro** columna.  
  
     Se abre un cuadro de diálogo que contiene todos los miembros del nivel especificado de la jerarquía.  
  
7.  Seleccione el miembro o los miembros en los que desee filtrar.  
  
8.  Haga clic en **Aceptar** en el cuadro de diálogo de miembro.  
  
9. Haga clic en **Aceptar** en el **segmentar el cubo** cuadro de diálogo.  
  
     El cubo de origen se filtrará tal y como define el segmento del cubo.  
  
## <a name="see-also"></a>Vea también  
 [Tareas de estructura de minería de datos y procedimientos](data-mining/mining-structure-tasks-and-how-tos.md)   
 [Crear una estructura de minería de datos OLAP](data-mining/create-a-new-olap-mining-structure.md)  
  
  