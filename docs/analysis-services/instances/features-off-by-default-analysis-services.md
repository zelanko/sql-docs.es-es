---
title: "Características desactivado de forma predeterminada (Analysis Services) | Documentos de Microsoft"
ms.custom: 
ms.date: 03/01/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology:
- analysis-services
- analysis-services/multidimensional-tabular
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: a9529edf-337e-4fdd-9a13-99cfe96b4fa1
caps.latest.revision: "5"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 644101b1010028ac88066f44f2b4427776ca983f
ms.sourcegitcommit: f1a6944f95dd015d3774a25c14a919421b09151b
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/08/2017
---
# <a name="features-off-by-default-analysis-services"></a>Características desactivadas de manera predeterminada (Analysis Services)
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]Una instancia de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] está diseñado para ser seguro de forma predeterminada. Por lo tanto, las características que comprometen la seguridad se deshabilitan de forma predeterminada. Las siguientes características están instaladas en estado deshabilitado y deben habilitarse específicamente si se desean utilizar.  
  
## <a name="feature-list"></a>Lista de características  
 Para habilitar las siguientes características, conéctese a [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] usando [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]. Haga clic con el botón derecho en el nombre de la instancia y seleccione **Facetas**. También puede habilitar estas características utilizando las propiedades del servidor, como se describe en la sección siguiente.  
  
-   Consultas ad hoc de minería de datos (OpenRowset)  
  
-   Objetos vinculados (a)  
  
-   Objetos vinculados (desde)  
  
-   Escuchar solo en conexiones locales  
  
-   Funciones definidas por el usuario  
  
## <a name="server-properties"></a>Propiedades del servidor  
 Otras características que están deshabilitadas de manera predeterminada se pueden habilitar mediante las propiedades del servidor. Conéctese a [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] usando [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]. Haga clic con el botón derecho en el nombre de la instancia y seleccione **Propiedades**. Haga clic en **General**y, a continuación, haga clic en **Mostrar avanzadas** para visualizar una lista de propiedades más extensa.  
  
-   Consultas ad hoc de minería de datos (OpenRowset)  
  
-   Permitir modelos de minería de datos de sesión (minería de datos)  
  
-   Objetos vinculados (a)  
  
-   Objetos vinculados (desde)  
  
-   Funciones definidas por el usuario basadas en COM  
  
-   Definición de seguimiento de la Caja negra (plantillas).  
  
-   Registro de consultas  
  
-   Escuchar solo en conexiones locales  
  
-   XML binario  
  
-   Compresión  
  
-   Afinidad del grupo. Para obtener información detallada, vea [Thread Pool Properties](../../analysis-services/server-properties/thread-pool-properties.md) .  
  
  
