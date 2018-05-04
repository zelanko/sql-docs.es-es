---
title: Procesar particiones en la base de datos del área de trabajo | Documentos de Microsoft
ms.custom: ''
ms.date: 03/01/2017
ms.prod: analysis-services
ms.prod_service: analysis-services, azure-analysis-services
ms.component: data-mining
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 3a369705-43fa-4961-9045-32e06fbdde33
caps.latest.revision: 12
author: Minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: 814214b3ffeca29df465eaa55a3d89e29914452c
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="process-partitions-in-the-workspace-databse"></a>Procesar particiones en la base de datos del área de trabajo 
[!INCLUDE[ssas-appliesto-sqlas-aas](../../includes/ssas-appliesto-sqlas-aas.md)]
  Las particiones dividen una tabla en partes lógicas. A continuación, cada partición se puede procesar (actualizar) de forma independiente de las demás particiones. Las tareas de este tema describen cómo procesar particiones en la base de datos del área de trabajo del modelo mediante el cuadro de diálogo **Procesar particiones** de [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)].  
  
 Una vez implementado un modelo en otra instancia de Analysis Services, los administradores de bases de datos pueden crear y administrar las particiones del modelo (implementado) mediante [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], mediante un script o usando un paquete IS. Para obtener más información, consulte [crear y administrar particiones de modelos tabulares](../../analysis-services/tabular-models/create-and-manage-tabular-model-partitions-ssas-tabular.md).  
  
###  <a name="bkmk_create_new"></a> Para procesar una partición  
  
1.  En [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)], haga clic en el menú **Modelo** , en **Procesar** (Actualizar) y, por último, en **Procesar particiones**.  
  
2.  En el cuadro de lista **Modo** , seleccione uno de los modos de procesamiento siguientes:  
  
    |Modo|Description|  
    |----------|-----------------|  
    |**Proceso predeterminado**|Detecta el estado de proceso de un objeto de partición y realiza el procesamiento necesario para devolver objetos de partición sin procesar o procesados parcialmente a un estado de procesamiento completo. Se cargan los datos de las tablas vacías y las particiones; se generan o se vuelven a generar las jerarquías, las columnas calculadas y las relaciones.|  
    |**Proceso completo**|Procesa un objeto de partición y todos los objetos que contiene. Cuando se ejecuta Proceso completo en un objeto que ya se ha procesado, [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] quita todos los datos del objeto y, a continuación, lo procesa. Este tipo de procesamiento es necesario cuando se ha realizado un cambio estructural en un objeto.|  
    |**Procesar datos**|Carga datos en una partición o en una tabla sin volver a generar las jerarquías o las relaciones, ni volver a calcular las columnas calculadas y las medidas.|  
    |**Procesar borrado**|Quita todos los datos de una partición.|  
    |**Procesar adición**|Actualiza la partición con nuevos datos de forma incremental.|  
  
3.  En la columna de casilla **Procesar** , seleccione las particiones que desea procesar con el modo seleccionado y haga clic en **Aceptar**.  
  
## <a name="see-also"></a>Vea también  
 [Particiones](../../analysis-services/tabular-models/partitions-ssas-tabular.md)   
 [Crear y administrar particiones en la base de datos del área de trabajo](../../analysis-services/tabular-models/create-and-manage-partitions-in-the-workspace-database-ssas-tabular.md)  
  
  
