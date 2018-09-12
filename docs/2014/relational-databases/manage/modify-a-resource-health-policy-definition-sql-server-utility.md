---
title: Modificación de una definición de la directiva de mantenimiento de recursos (utilidad de SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: conceptual
f1_keywords:
- SQL12.SWB.UE.UTILITY.ADMINISTRATION.F1
ms.assetid: 27bec0b6-92e9-448e-8c70-fe36802cf128
caps.latest.revision: 8
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: e2ba0470599798a7a00972395a567db706332b8d
ms.sourcegitcommit: 8ae6e6618a7e9186aab3c6a37ea43776aa9a382b
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 09/06/2018
ms.locfileid: "43810651"
---
# <a name="modify-a-resource-health-policy-definition-sql-server-utility"></a>Modificar una definición de la directiva de mantenimiento de recursos (utilidad de SQL Server)
  En este tema se describe cómo modificar una definición de directiva de mantenimiento de recursos en [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] mediante [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]. Antes de modificar una directiva de uso de recursos en la Utilidad de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , debe crear un punto de control de la utilidad (UCP). Para obtener más información, vea [Características y tareas de la utilidad de SQL Server](sql-server-utility-features-and-tasks.md).  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Las directivas de uso de recursos de la utilidad se pueden configurar para las aplicaciones de capa de datos y las instancias administradas de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Las directivas de uso de recursos se pueden definir globalmente para todas las aplicaciones de capa de datos y las instancias administradas de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] en la Utilidad de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , o se pueden definir individualmente para cada aplicación de capa de datos y para cada instancia administrada de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] en la Utilidad de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . También es posible implementar directivas globales y configurar aplicaciones de capa de datos e instancias administradas individuales de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] con sus propias definiciones de la directiva.  
  
##  <a name="SSMSProcedure"></a> Usar SQL Server Management Studio  
  
#### <a name="modify-global-resource-utilization-policies-in-a-sql-server-utility"></a>Modifique las directivas de uso de recursos globales en una Utilidad SQL Server.  
  
1.  Conéctese al UCP en [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)].  
  
2.  En el panel de navegación del explorador de la utilidad, haga clic en **Administración de la utilidad** para ver o modificar las directivas de supervisión globales y, a continuación, haga clic en la pestaña **Directiva** en el panel de contenido del explorador de la utilidad.  
  
3.  En el panel de contenido del explorador de la utilidad, seleccione **Establecer directivas de supervisión globales de capas de datos** o **Establecer directivas de supervisión globales de instancias administradas** haciendo clic en la flecha o la descripción de la directiva.  
  
4.  Utilice los controles en el lado derecho de las descripciones de la directiva para establecer los umbrales de infrautilización o sobreutilización.  
  
5.  Utilice los botones **Aplicar**, **Descartar**o **Restaurar valores predeterminados** según sea necesario. El cambio de la directiva puede tardar hasta 15 minutos en propagarse en el panel de la Utilidad de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] y en los detalles de la vista de lista.  
  
6.  Para actualizar los datos, haga clic con el botón derecho en el nodo **Administración de la utilidad** en el panel de navegación del explorador de la utilidad y seleccione **Actualizar**.  
  
#### <a name="modify-resource-health-policy-definitions-for-an-individual-data-tier-application-or-an-individual-managed-instance-of-sql-server-in-a-sql-server-utility"></a>Modifique las definiciones de la directiva de mantenimiento de recursos para una aplicación de nivel de datos o instancia administrada individual en una Utilidad de SQL Server  
  
1.  Conéctese al UCP en [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)].  
  
2.  En el panel de navegación del explorador de la utilidad, haga clic en **Aplicaciones de capa de datos implementadas**o haga clic en **Instancias administradas**para ver o modificar las directivas de supervisión para una aplicación de capa de datos o instancia administrada individual.  
  
3.  En la vista de lista de panel de contenido del explorador de la utilidad, haga clic en la aplicación de capa de datos o nombre de instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] cuyas directivas le gustaría modificar y después haga clic en la pestaña **Detalles de la directiva** .  
  
4.  Seleccione la directiva para ver o modificar haciendo clic en la flecha o la descripción de la directiva. Las directivas globales están seleccionadas de forma predeterminada.  
  
5.  Seleccione el botón de radio **Invalidar la directiva global** para invalidar las directivas globales e implementar una definición de directiva individual para la aplicación de capa de datos especificada.  
  
6.  Use los controles en el lado derecho de la descripción de la directiva para establecer los umbrales de infrautilización o sobreutilización.  
  
7.  Utilice los botones **Aplicar**, **Descartar**o **Restaurar valores predeterminados** según sea necesario. El cambio de la directiva puede tardar hasta 15 minutos en propagarse en el panel de la Utilidad de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] y en los detalles de la vista de lista.  
  
8.  Para actualizar los datos, haga clic con el botón derecho en el nodo **Aplicaciones de capa de datos implementadas** en el panel de navegación del explorador de la utilidad y seleccione **Actualizar**.  
  
## <a name="see-also"></a>Vea también  
 [Características y tareas de la utilidad de SQL Server](sql-server-utility-features-and-tasks.md)   
 [Ver los resultados de la directiva de mantenimiento de recursos &#40;Utilidad de SQL Server&#41;](view-resource-health-policy-results-sql-server-utility.md)  
  
  
