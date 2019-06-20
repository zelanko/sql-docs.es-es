---
title: Administración de la instancia de Analysis Services | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: 0455fa4f-b92d-4a8b-a8f0-f2a268a5c84e
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: ac0c6637dd08dc2ea8927853b7a6bf8dccca454d
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "66080350"
---
# <a name="analysis-services-instance-management"></a>Administración de una instancia de Analysis Services
  Una instancia de Analysis Services es una copia del ejecutable `msmdsrv.exe` que se ejecuta como un servicio de sistema operativo. Cada instancia es totalmente independiente de otras instancias en el mismo servidor y tiene su propia configuración, permisos, puertos, cuentas de inicio, almacenamiento de archivos, y propiedades del modo de servidor.  
  
 Cada instancia de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] ejecuta un servicio de Windows, Msmdsrv.exe, en el contexto de seguridad de una cuenta de inicio de sesión definida.  
  
-   El nombre de servicio de la instancia predeterminada de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] es MSSQLServerOLAPService.  
  
-   El nombre de servicio de cada instancia con nombre de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] es MSOLAP$InstanceName.  
  
> [!NOTE]  
>  Si hay instaladas varias instancias de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] , el programa de instalación también instala un servicio redirector que está integrado en el servicio [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Browser. El servicio redirector es responsable de dirigir clientes a la instancia con nombre correspondiente de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]. El servicio [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Browser siempre se ejecuta en el contexto de seguridad de la cuenta del sistema local, una cuenta de administrador local utilizada por Windows para los servicios del sistema que no tengan acceso a recursos de fuera del equipo local.  
  
 Varias instancias significa que podrá realizar escalamientos verticalmente si instala varias instancias del servidor en el mismo hardware. En Analysis Services en concreto, también significa que podrá admitir diferentes modos de servidor si tiene varias instancias en el mismo servidor, cada una de ellas configurada para ejecutarse en un modo determinado.  
  
 El modo de servidor es una propiedad de servidor que determina el almacenamiento y la arquitectura de memoria que se usarán con esa instancia. Un servidor que se ejecuta en modo multidimensional utiliza el nivel de administración de recursos compilado para las bases de datos multidimensionales de cubo y los modelos de minería de datos. En cambio, el modo de servidor tabular utiliza el motor analítico en memoria xVelocity (VertiPaq) y la compresión de datos para agregar datos según se solicite.  
  
 Las diferencias entre el almacenamiento y la arquitectura de memoria significan que una única instancia de Analysis Services ejecutará las bases de datos tabulares o las bases de datos multidimensionales, pero no ambas. La propiedad del modo de servidor determina el tipo de base de datos que se ejecuta en la instancia.  
  
 El modo de servidor se establece durante la instalación al especificar el tipo de base de datos que ejecutará en el servidor. Para admitir todos los modos disponibles, instale varias instancias de Analysis Services, cada una de ellas implementada en un modo de servidor que se corresponda con los proyectos que está generando.  
  
 Por lo general, la mayoría de las tareas administrativas que debe realizar no variarán según el modo. Como administrador del sistema de Analysis Services, puede usar los mismos procedimientos y scripts para administrar cualquier instancia de Analysis Services en su red, independientemente de cómo se haya instalado.  
  
> [!NOTE]  
>  La excepción es PowerPivot para SharePoint. La administración de servidores de una implementación de PowerPivot siempre está en el contexto de una granja de SharePoint. PowerPivot se diferencia de otros modos de servidor en que es siempre de instancia única y se administra siempre a través de Administración central de SharePoint o la Herramienta de configuración de PowerPivot. Aunque es posible conectarse a PowerPivot para SharePoint de SQL Server Management Studio o [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)], no es deseable. Una granja de servidores de SharePoint incluye la infraestructura que sincroniza el estado del servidor y supervisa la disponibilidad del servidor. El uso de otras herramientas puede interferir con estas operaciones. Para obtener más información sobre la administración de servidor de PowerPivot, vea [PowerPivot para SharePoint &#40;SSAS&#41;](../power-pivot-sharepoint/power-pivot-for-sharepoint-ssas.md).  
  
## <a name="in-this-section"></a>En esta sección  
  
|Vínculo|Descripción de la tarea|  
|----------|----------------------|  
|[Configuración posterior a la instalación &#40;Analysis Services&#41;](post-install-configuration-analysis-services.md)|Describe las tareas necesarias y opcionales que completan o modifican una instalación de Analysis.|  
|[Conectar a Analysis Services](connect-to-analysis-services.md)|Describe las propiedades de cadena de conexión, las bibliotecas de cliente, las metodologías de autenticación y los pasos para establecer o borrar conexiones.|  
|[Supervisar una instancia de Analysis Services](monitor-an-analysis-services-instance.md)|Describe las herramientas y técnicas de supervisión de instancias de servidor, incluida una explicación sobre el uso del monitor de rendimiento y SQL Server Profiler.|  
|[Crear scripts para tareas administrativas en Analysis Services](../script-administrative-tasks-in-analysis-services.md)|Explica cómo automatizar muchas tareas administrativas, incluido el procesamiento.|  
|[Escenarios de globalización para Analysis Services multidimensional](../globalization-scenarios-for-analysis-services-multiidimensional.md)|Explica la compatibilidad de intercalación e idioma, los pasos que se deben seguir para cambiar ambas propiedades y sugerencias para configurar y probar el comportamiento de estas.|  
|[Operaciones de registro en Analysis Services](log-operations-in-analysis-services.md)|Describe los registros y explica cómo configurarlos.|  
  
## <a name="see-also"></a>Vea también  
 [Comparar soluciones tabulares y multidimensionales &#40;SSAS&#41;](../comparing-tabular-and-multidimensional-solutions-ssas.md)   
 [Herramientas de configuración de PowerPivot](../power-pivot-sharepoint/power-pivot-configuration-tools.md)   
 [Administración de servidor de PowerPivot y la configuración en Administración Central](../power-pivot-sharepoint/power-pivot-server-administration-and-configuration-in-central-administration.md)   
 [Determinar el modo de servidor de una instancia de Analysis Services](determine-the-server-mode-of-an-analysis-services-instance.md)  
  
  
