---
title: Características y tareas de la utilidad de SQL Server | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
helpviewer_keywords:
- SQL Server utility [SQL Server]
- utility control point
- Utility growth rate
- Multiserver management
- UCP
- Multi-server management [SQL Server]
ms.assetid: 6e6cbd25-6b1c-4e21-9ade-4584e243fd8f
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 1d3f61904a1a820df58583212dcbd2e998dbabbd
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/03/2018
ms.locfileid: "52767127"
---
# <a name="sql-server-utility-features-and-tasks"></a>Características y tareas de la utilidad de SQL Server
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] necesitan administrar su entorno de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] en conjunto, requisito cubierto en esta versión por medio del concepto de administración de aplicaciones y de varios servidores de la Utilidad de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
## <a name="benefits-of-the-sql-server-utility"></a>Ventajas de la Utilidad de SQL Server  
 La Utilidad de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] modela las entidades relacionadas con [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]de una organización en una vista unificada. Los puntos de vista del Explorador de Utilidad y de la Utilidad de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] en [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] (SSMS) proporcionan a los administradores una vista global del estado de los recursos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] a través de una instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que actúa como punto de control de la utilidad (UCP). La combinación del resumen y los datos detallados presentados por el UCP sobre directivas de infrautilización o sobreutilización, y sobre diversidad de parámetros clave, habilita posibilidades de consolidación de recursos y de fácil identificación de sobreutilización. Las directivas de mantenimiento se pueden configurar y ajustarse para modificar umbrales de uso mayor o menor de los recursos. Es posible cambiar las directivas de supervisión globales o configurar directivas de supervisión individuales para cada entidad administrada en la Utilidad [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
##  <a name="typical_scenarios"></a> Introducción a la Utilidad de SQL Server  
 El escenario de usuario típico comienza con la creación de un punto de control de la utilidad  que establece el punto de razonamiento central para la Utilidad [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . El UCP proporciona una vista global del estado de los recursos, tomada de las instancias administradas de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] en la Utilidad [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Una vez creado el UCP, inscriba instancias de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] en la Utilidad de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para que el UCP las pueda administrar.  
  
 Cada instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] y aplicación de capa de datos administrada por la Utilidad [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] se pueden supervisar dependiendo de definiciones de directiva globales o basándose definiciones de directiva individuales.  
  
## <a name="related-tasks"></a>Related Tasks  
 Use los temas siguientes para empezar a trabajar con la utilidad de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
|||  
|-|-|  
|**Descripción**|**Tema**|  
|Describe las consideraciones para configurar un servidor que ejecute los conjuntos de recopilación de la utilidad y que no sean de la utilidad en la misma instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|[Consideraciones para ejecutar conjuntos de recopilación de la utilidad y que no sean de la utilidad en la misma instancia de SQL Server](run-utility-and-non-utility-collection-sets-on-same-sql-instance.md)|  
|Describe cómo crear un punto de control de la Utilidad de SQL Server.|[Crear un punto de control de la Utilidad de SQL Server &#40;Utilidad de SQL Server&#41;](create-a-sql-server-utility-control-point-sql-server-utility.md)|  
|Describe cómo conectarse a una Utilidad de SQL Server.|[Conectarse a una utilidad de SQL Server](connect-to-a-sql-server-utility.md)|  
|Describe cómo inscribir una instancia de SQL Server con un punto de control de la utilidad.|[Inscribir una instancia de SQL Server &#40;Utilidad de SQL Server&#41;](enroll-an-instance-of-sql-server-sql-server-utility.md)|  
|Describe cómo usar el Explorador de la utilidad para administrar la Utilidad de SQL Server.|[Utilizar el explorador de Utilidad para administrar la utilidad de SQL Server](use-utility-explorer-to-manage-the-sql-server-utility.md)|  
|Describe cómo supervisar las instancias de SQL Server de la Utilidad de SQL Server.|[Supervisar instancias de SQL Server en la utilidad de SQL Server](monitor-instances-of-sql-server-in-the-sql-server-utility.md)|  
|Describe cómo ver los resultados de la directiva de mantenimiento de recursos.|[Ver los resultados de la directiva de mantenimiento de recursos &#40;Utilidad de SQL Server&#41;](view-resource-health-policy-results-sql-server-utility.md)|  
|Describe cómo modificar una definición de la directiva de mantenimiento de recursos.|[Modificar una definición de la directiva de mantenimiento de recursos &#40;Utilidad de SQL Server&#41;](modify-a-resource-health-policy-definition-sql-server-utility.md)|  
|Describe cómo configurar el almacenamiento de datos del UCP.|[Configurar el almacenamiento de datos del punto de control de la utilidad &#40;Utilidad de SQL Server&#41;](configure-your-utility-control-point-data-warehouse-sql-server-utility.md)|  
|Describe cómo configurar las directivas de mantenimiento de la utilidad.|[Configurar las directivas de mantenimiento &#40;Utilidad de SQL Server&#41;](configure-health-policies-sql-server-utility.md)|  
|Describe cómo ajustar la atenuación en las directivas de uso de la CPU.|[Reducir el ruido en las directivas de uso de la CPU &#40;Utilidad de SQL Server&#41;](reduce-noise-in-cpu-utilization-policies-sql-server-utility.md)|  
|Describe cómo quitar una instancia de SQL Server de un UCP.|[Quitar una instancia de SQL Server de la utilidad de SQL Server](remove-an-instance-of-sql-server-from-the-sql-server-utility.md)|  
|Describe cómo cambiar la cuenta de proxy para el conjunto de recopilación de la utilidad en una instancia administrada de SQL Server.|[Cambiar la cuenta de proxy para el conjunto de recopilación de la utilidad en una instancia administrada de SQL Server &#40;Utilidad de SQL Server&#41;](change-proxy-account-for-utility-collection-on-managed-sql-server.md)|  
|Describe cómo mover un UCP desde una instancia de SQL Server a otra.|[Mover un UCP desde una instancia de SQL Server a otra &#40;Utilidad de SQL Server&#41;](move-a-ucp-from-one-instance-of-sql-server-to-another-sql-server-utility.md)|  
|Describe cómo quitar una instancia de UCP.|[Quitar un punto de control de la utilidad de SQL Server &#40;Utilidad de SQL Server&#41;](remove-a-utility-control-point-sql-server-utility.md)|  
|Describe cómo solucionar problemas de la Utilidad de SQL Server.|[Solucionar problemas de la Utilidad de SQL Server](../../database-engine/troubleshoot-the-sql-server-utility.md)|  
|Describe cómo solucionar problemas de mantenimiento de recursos de SQL Server.|[Solucionar problemas de estado de recursos de SQL Server &#40;Utilidad de SQL Server&#41;](troubleshoot-sql-server-resource-health-sql-server-utility.md)|  
|Vínculos a temas de la Ayuda F1 del Explorador de la utilidad.|[Explorador de Utilidad (Ayuda F1)](utility-explorer-f1-help.md)|  
  
  
