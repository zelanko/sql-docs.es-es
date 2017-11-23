---
title: "Cambiar las propiedades de una estructura de minería de datos | Documentos de Microsoft"
ms.custom: 
ms.date: 03/13/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: data-mining
ms.reviewer: 
ms.suite: sql
ms.technology:
- analysis-services
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords: mining structures [Analysis Services], properties
ms.assetid: 03b16897-2e36-42b8-9f7d-db1b9b898401
caps.latest.revision: "28"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 1bd35f96e4748f2e453930e74621edfbcb3aaee4
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/17/2017
---
# <a name="change-the-properties-of-a-mining-structure"></a>Cambiar las propiedades de una estructura de minería de datos
  Hay dos tipos de propiedades en una estructura de minería de datos que pueden modificarse:  
  
-   Propiedades de la estructura de minería de datos que afectan a la estructura entera  
  
-   Propiedades de columnas individuales en la estructura  
  
 Tenga en cuenta que algunas de estas propiedades dependen de la configuración de otras propiedades. Por ejemplo, no se pueden establecer las propiedades que controlan el comportamiento de discretización (como <xref:Microsoft.AnalysisServices.ScalarMiningStructureColumn.DiscretizationMethod%2A> o <xref:Microsoft.AnalysisServices.ScalarMiningStructureColumn.DiscretizationBucketCount%2A>) hasta que se haya configurado el tipo de datos de la columna en **Discretizado**.  
  
 Para más información sobre las propiedades de la estructura de minería, vea [Columnas de la estructura de minería de datos](../../analysis-services/data-mining/mining-structure-columns.md).  
  
### <a name="to-change-the-properties-of-a-mining-structure"></a>Para cambiar las propiedades de una estructura de minería de datos  
  
1.  En la pestaña **Estructura de minería de datos** del Diseñador de minería de datos, haga clic con el botón derecho en la estructura de minería de datos o en una columna de la estructura de minería de datos y, después, seleccione **Propiedades**.  
  
     La ventana **Propiedades** se abre en la parte derecha de la pantalla, si es que aún no estaba visible.  
  
2.  En la ventana **Propiedades** , seleccione el valor correspondiente a la propiedad que desee cambiar y, a continuación, escriba el nuevo valor.  
  
     El nuevo valor tendrá efecto cuando se seleccione otro elemento diferente en el diseñador.  
  
## <a name="see-also"></a>Vea también  
 [Tareas y procedimientos de las estructuras de minería de datos](../../analysis-services/data-mining/mining-structure-tasks-and-how-tos.md)  
  
  
