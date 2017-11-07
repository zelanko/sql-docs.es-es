---
title: "Conceder permisos para una dimensión (Analysis Services) | Documentos de Microsoft"
ms.custom: 
ms.date: 03/04/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- analysis-services/multidimensional-tabular
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.asvs.roledesignerdialog.dimensions.f1
helpviewer_keywords:
- dimensions [Analysis Services], security
- read/write permissions
- user access rights [Analysis Services], dimensions
- permissions [Analysis Services], dimensions
ms.assetid: be5b2746-0336-4b12-827e-131462bdf605
caps.latest.revision: 39
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 72ea5d3842b0fbf2f568606004b2de7a7e66825f
ms.contentlocale: es-es
ms.lasthandoff: 09/01/2017

---
# <a name="grant-permissions-on-a-dimension-analysis-services"></a>Otorgar permisos para una dimensión (Analysis Services)
  La seguridad de dimensión se usa para establecer permisos en un objeto de dimensión, no en sus datos. Por lo general, el principal objetivo a la hora de establecer permisos en una dimensión es permitir o denegar el acceso a las operaciones de procesamiento.  
  
 Pero quizás su objetivo no sea controlar las operaciones de procesamiento, sino más bien el acceso a los datos para una dimensión o a los atributos y jerarquías que contiene. Por ejemplo, una empresa con divisiones comerciales regionales quiere que la información sobre rendimiento comercial esté disponible para aquellos que no pertenecen a la división. Para permitir o denegar el acceso a porciones de los datos de la dimensión para sus diferentes partes constituyentes, puede establecer permisos para los atributos de la dimensión y los miembros de la dimensión. Tenga en cuenta que no puede denegar el acceso a un objeto individual de una dimensión, solamente a sus datos. Si su objetivo inmediato es permitir o denegar el acceso a los miembros de una dimensión, incluidos los derechos de acceso a jerarquías de atributo individuales, vea [Conceder acceso personalizado a datos de dimensión &#40;Analysis Services&#41;](../../analysis-services/multidimensional-models/grant-custom-access-to-dimension-data-analysis-services.md) para obtener más información.  
  
 El resto de este tema se ocupa de los permisos que se pueden establecer en los propios objetos de la dimensión, lo cual incluye:  
  
-   permisos de Lectura o Lectura y escritura (se debe elegir Lectura o Lectura y escritura; no se puede indicar "ninguno"). Como se ha indicado, si su objetivo es restringir el acceso a los datos de dimensiones, vea [Conceder acceso personalizado a datos de dimensión &#40;Analysis Services&#41;](../../analysis-services/multidimensional-models/grant-custom-access-to-dimension-data-analysis-services.md) para obtener más información.  
  
-   Procesar permisos (haga esto cuando la situación requiera una estrategia de procesamiento que necesite permisos personalizados en objetos individuales).  
  
-   Leer permisos de definición (por lo general, esto se realizaría para admitir el procesamiento interactivo en una herramienta o para aportar visibilidad a un modelo. Leer definición permite ver la estructura de una dimensión, sin permisos para los datos o la capacidad para modificar su definición).  
  
 Cuando se definen roles para una dimensión, los permisos disponibles variarán en función de si el objeto es una dimensión de base de datos independiente (interno respecto a la base de datos, pero externo respecto al cubo) o una dimensión de cubo.  
  
> [!NOTE]  
>  De forma predeterminada, los permisos para una dimensión de base de datos los heredan las dimensiones de cubo. Por ejemplo, si habilita **Lectura y escritura** en una dimensión de base de datos Customer, la dimensión del cubo Customer heredará **Lectura y escritura** en el contexto del rol actual. Puede borrar los permisos heredados si desea invalidar un valor de configuración del permiso.  
  
## <a name="set-permissions-on-a-database-dimension"></a>Establecer permisos para una dimensión de base de datos  
 Las dimensiones de base de datos son objetos independientes en una base de datos, que permiten la reutilización de la dimensión en el mismo modelo. Tenga en cuenta una base de datos DATE que se usa varias veces en un modelo, como dimensiones de cubo Order Date, Ship Date y Due Date. Dado que las dimensiones de cubo y base de datos son objetos del mismo nivel en las bases de datos, puede establecer permisos de procesamiento independientes en cada objeto.  
  
1.  En [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], conéctese a la instancia de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)], expanda **Roles** para la base de datos correspondiente en Explorador de objetos y, después, haga clic en un rol de base de datos (o cree un rol de base de datos).  
  
2.  En el panel **Dimensiones** , el conjunto de dimensiones debe establecerse en **Todas las dimensiones de la base de datos**.  
  
     De forma predeterminada, los permisos se establecen en **Lectura**.  
  
     Aunque **Lectura y escritura** está disponible, se recomienda no usar este permiso. **Lectura y escritura** se usa en escenarios de reescritura de dimensiones, que están en desuso. Vea [Características en desuso de Analysis Services en SQL Server 2016](../../analysis-services/deprecated-analysis-services-features-in-sql-server-2016.md).  
  
     Si lo prefiere, puede establecer permisos de **Leer definición** y **Procesar** en objetos de dimensión individuales, siempre que esos permisos no se hayan establecido al nivel de la base de datos. Vea [Otorgar permisos de procesamiento &#40;Analysis Services&#41;](../../analysis-services/multidimensional-models/grant-process-permissions-analysis-services.md) y [Otorgar permisos Leer definición en metadatos de objetos &#40;Analysis Services&#41;](../../analysis-services/multidimensional-models/grant-read-definition-permissions-on-object-metadata-analysis-services.md) para obtener más información.  
  
## <a name="set-permissions-on-a-cube-dimension"></a>Establecer permisos para una dimensión de cubo  
 Las dimensiones de cubo son dimensiones de base de datos que se han agregado a un cubo. Como tales, dependen estructuralmente de grupos de medida asociados. Pese a que puede procesar estos objetos de forma atómica, en términos de autorización, conviene tratar al cubo y las dimensiones de cubo como una entidad única.  
  
1.  En [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], conéctese a la instancia de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)], expanda **Roles** para la base de datos correspondiente en el Explorador de objetos y, después, haga clic en un rol de base de datos (o cree un rol de base de datos).  
  
2.  En el **dimensiones** panel, el cambio de la dimensión se establece en \<nombre del cubo > **dimensiones de cubo**.  
  
     De forma predeterminada, los permisos se heredan de la dimensión de base de datos que corresponda. Desactive la casilla **Heredar** para modificar los permisos de **Lectura** a **Lectura y escritura**. Antes de usar **Lectura y escritura**, asegúrese de leer la nota de la sección anterior.  
  
> [!IMPORTANT]  
>  Si configura permisos de rol de base de datos con Objetos de administración de análisis (AMO), cualquier referencia a una dimensión de cubo en el atributo DimensionPermission de un cubo interrumpe la herencia de permisos del atributo DimensionPermission de la base de datos. Para más información, vea [Desarrollar con Objetos de administración de análisis &#40;AMO&#41;](../../analysis-services/multidimensional-models/analysis-management-objects/developing-with-analysis-management-objects-amo.md).  
  
## <a name="see-also"></a>Vea también  
 [Roles y permisos &#40;Analysis Services&#41;](../../analysis-services/multidimensional-models/roles-and-permissions-analysis-services.md)   
 [Otorgar permisos para cubos o modelos &#40;Analysis Services&#41;](../../analysis-services/multidimensional-models/grant-cube-or-model-permissions-analysis-services.md)   
 [Conceder permisos en las estructuras de minería de datos y modelos de &#40; Analysis Services &#41;](../../analysis-services/multidimensional-models/grant-permissions-on-data-mining-structures-and-models-analysis-services.md)   
 [Conceder acceso personalizado a la dimensión de datos &#40; Analysis Services &#41;](../../analysis-services/multidimensional-models/grant-custom-access-to-dimension-data-analysis-services.md)   
 [Otorgar acceso personalizado a los datos de las celdas &#40;Analysis Services&#41;](../../analysis-services/multidimensional-models/grant-custom-access-to-cell-data-analysis-services.md)  
  
  

