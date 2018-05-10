---
title: Procesar particiones de modelos tabulares | Documentos de Microsoft
ms.date: 05/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: tabular-models
ms.topic: article
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 4722bd1c6aecb32f448b3c8d1628205d728f318f
ms.sourcegitcommit: 1aedef909f91dc88dc741748f36eabce3a04b2b1
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/08/2018
---
# <a name="process-tabular-model-partitions"></a>Procesar particiones de modelos tabulares 
[!INCLUDE[ssas-appliesto-sqlas-aas](../../includes/ssas-appliesto-sqlas-aas.md)]
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
 [Particiones de modelos tabulares](../../analysis-services/tabular-models/tabular-model-partitions-ssas-tabular.md)   
 [Crear y administrar particiones de modelos tabulares](../../analysis-services/tabular-models/create-and-manage-tabular-model-partitions-ssas-tabular.md)  
  
  
