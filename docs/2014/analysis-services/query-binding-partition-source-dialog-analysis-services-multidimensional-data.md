---
title: Consulta (cuadro de diálogo origen de partición) de detalle del enlace (Analysis Services - datos multidimensionales) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
f1_keywords:
- sql12.asvs.cubeeditor.partitions.partitionfilterexpression.f1
ms.assetid: 697874d4-3f7a-4126-96f5-37cc8e2ee306
caps.latest.revision: 20
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 7789e99c47f2219d8155eb929a081c5f734a75d9
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/02/2018
ms.locfileid: "37194345"
---
# <a name="query-binding-detail-partition-source-dialog-box-analysis-services---multidimensional-data"></a>Detalle del enlace de consultas (cuadro de diálogo Origen de la partición) (Analysis Services - Datos multidimensionales)
  Use la opción **Enlace de consultas** del cuadro de diálogo **Origen de la partición** para especificar la consulta que proporciona los datos para la partición. Puede mostrar este panel seleccionando **Enlace de consultas** en la opción **Tipo de enlace** del cuadro de diálogo **Origen de la partición** .  
  
## <a name="options"></a>Opciones  
 **Origen de datos**  
 Seleccione el origen de datos en el que se ejecuta la consulta para proporcionar datos de hechos para la partición.  
  
 **Consulta**  
 Escriba o modifique la instrucción SQL que se utiliza al recuperar datos de hechos cuando se procesa la partición.  
  
> [!IMPORTANT]  
>  Si se especifica una cláusula WHERE, puede utilizarse un subconjunto de registros para esta partición. Esto es muy importante para evitar la duplicación de datos cuando varias particiones se basan en una única tabla de hechos. Para más información, vea [Partition Source Dialog Box &#40;Analysis Services - Multidimensional Data&#41;](partition-source-dialog-box-analysis-services-multidimensional-data.md).  
  
 **Comprobación**  
 Haga clic para comprobar que la instrucción en **Consultar** sea una instrucción SQL válida.  
  
## <a name="see-also"></a>Vea también  
 [Cuadro de diálogo origen de la partición &#40;Analysis Services - datos multidimensionales&#41;](partition-source-dialog-box-analysis-services-multidimensional-data.md)  
  
  
