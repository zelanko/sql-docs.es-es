---
title: Procesar particiones en la base de datos del área de trabajo (SSAS tabular) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: 3a369705-43fa-4961-9045-32e06fbdde33
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 15b9f9203075734dd84d7b601574f66bc401e700
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/26/2020
ms.locfileid: "66066799"
---
# <a name="process-partitions-in-the-workspace-database-ssas-tabular"></a>Procesar particiones en la base de datos del área de trabajo (SSAS tabular)
  Las particiones dividen una tabla en partes lógicas. A continuación, cada partición se puede procesar (actualizar) de forma independiente de las demás particiones. Las tareas de este tema describen cómo procesar particiones en la base de datos del área de trabajo del modelo mediante el cuadro de diálogo **Procesar particiones** de [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)].  
  
 Una vez implementado un modelo en otra instancia de Analysis Services, los administradores de bases de datos pueden crear y administrar las particiones del modelo (implementado) mediante [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], mediante un script o usando un paquete IS. Para obtener más información, vea [Crear y administrar particiones de modelos tabulares &#40;SSAS tabular&#41;](partitions-ssas-tabular.md).  
  
###  <a name="to-process-a-partition"></a><a name="bkmk_create_new"></a> Para procesar una partición  
  
1.  En [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)], haga clic en el menú **Modelo** , en **Procesar** (Actualizar) y, por último, en **Procesar particiones**.  
  
2.  En el cuadro de lista **Modo** , seleccione uno de los modos de procesamiento siguientes:  
  
    |Mode|Descripción|  
    |----------|-----------------|  
    |**Proceso predeterminado**|Detecta el estado de proceso de un objeto de partición y realiza el procesamiento necesario para devolver objetos de partición sin procesar o procesados parcialmente a un estado de procesamiento completo. Se cargan los datos de las tablas vacías y las particiones; se generan o se vuelven a generar las jerarquías, las columnas calculadas y las relaciones.|  
    |**Proceso completo**|Procesa un objeto de partición y todos los objetos que contiene. Cuando se ejecuta Proceso completo en un objeto que ya se ha procesado, [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] quita todos los datos del objeto y, a continuación, lo procesa. Este tipo de procesamiento es necesario cuando se ha realizado un cambio estructural en un objeto.|  
    |**Procesar datos**|Carga datos en una partición o en una tabla sin volver a generar las jerarquías o las relaciones, ni volver a calcular las columnas calculadas y las medidas.|  
    |**Procesar borrado**|Quita todos los datos de una partición.|  
    |**Procesar adición**|Actualiza la partición con nuevos datos de forma incremental.|  
  
3.  En la columna de casilla **Procesar** , seleccione las particiones que desea procesar con el modo seleccionado y haga clic en **Aceptar**.  
  
## <a name="see-also"></a>Consulte también  
 [Particiones &#40;&#41;tabular de SSAS](partitions-ssas-tabular.md)   
 [Crear y administrar particiones en la base de datos del área de trabajo &#40;SSAS tabular&#41;](workspace-database-ssas-tabular.md)  
  
  
