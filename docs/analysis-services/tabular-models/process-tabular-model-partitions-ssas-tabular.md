---
title: Procesar particiones de modelos tabulares (SSAS Tabular) | Documentos de Microsoft
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: tabular-models
ms.reviewer: 
ms.suite: sql
ms.technology:
- analysis-services
- analysis-services/multidimensional-tabular
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 6c498d2b-22d6-4661-bc21-2ee708336c8b
caps.latest.revision: 6
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 46fe768f2176501fc6b15a0f14f0d6bff808b065
ms.contentlocale: es-es
ms.lasthandoff: 09/01/2017

---
# <a name="process-tabular-model-partitions-ssas-tabular"></a>Procesar particiones de modelos tabulares (SSAS tabular)
  Las particiones dividen una tabla en partes lógicas. A continuación, cada partición se puede procesar (actualizar) de forma independiente de las demás particiones. Las tareas de este tema describen cómo procesar particiones en una base de datos del modelo mediante el cuadro de diálogo **Procesar particiones** de [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)].  
  
###  <a name="bkmk_create_new"></a> Para procesar una partición  
  
1.  En [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], haga clic con el botón derecho en la tabla que tiene las particiones que quiere procesar y, después, haga clic en **Particiones**.  
  
2.  En el cuadro de diálogo **Particiones** , en **Particiones**, haga clic en el botón Procesar.  
  
3.  En el cuadro de diálogo **Procesar particiones** , en el cuadro de lista **Modo** , seleccione uno de los modos de procesamiento siguientes:  
  
    |Modo|Description|  
    |----------|-----------------|  
    |**Proceso predeterminado**|Detecta el estado de proceso de un objeto de partición y realiza el procesamiento necesario para devolver objetos de partición sin procesar o procesados parcialmente a un estado de procesamiento completo. Se cargan los datos de las tablas vacías y las particiones; se generan o se vuelven a generar las jerarquías, las columnas calculadas y las relaciones.|  
    |**Proceso completo**|Procesa un objeto de partición y todos los objetos que contiene. Cuando se ejecuta Proceso completo en un objeto que ya se ha procesado, [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] quita todos los datos del objeto y, a continuación, lo procesa. Este tipo de procesamiento es necesario cuando se ha realizado un cambio estructural en un objeto.|  
    |**Procesar datos**|Carga datos en una partición o en una tabla sin volver a generar las jerarquías o las relaciones, ni volver a calcular las columnas calculadas y las medidas.|  
    |**Procesar borrado**|Quita todos los datos de una partición.|  
    |**Procesar adición**|Actualiza la partición con nuevos datos de forma incremental.|  
  
4.  En la columna de casilla **Procesar** , seleccione las particiones que desea procesar con el modo seleccionado y haga clic en **Aceptar**.  
  
## <a name="see-also"></a>Vea también  
 [Particiones de modelos tabulares &#40;SSAS tabular&#41;](../../analysis-services/tabular-models/tabular-model-partitions-ssas-tabular.md)   
 [Crear y administrar particiones de modelos tabulares &#40;SSAS tabular&#41;](../../analysis-services/tabular-models/create-and-manage-tabular-model-partitions-ssas-tabular.md)  
  
  

