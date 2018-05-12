---
title: Administración del servidor de Analysis Services | Documentos de Microsoft
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: ''
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 62c350b13db727b747fc4573b3bb634ac59256f9
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/10/2018
---
# <a name="analysis-services-server-management"></a>Administración de servidor de Analysis Services

  Una instancia del servidor de Analysis Services es una copia de la **msmdsrv.exe** archivo ejecutable que se ejecuta como un servicio de sistema operativo. Cada instancia es totalmente independiente de otras instancias en el mismo servidor y tiene su propia configuración, permisos, puertos, cuentas de inicio, almacenamiento de archivos, y propiedades del modo de servidor.  
  
 Cada instancia se ejecuta como servicio de Windows, Msmdsrv.exe, en el contexto de seguridad de una cuenta de inicio de sesión definida.  
  
-   El nombre del servicio de instancia predeterminada es MSSQLServerOLAPService.  
  
-   El nombre de cada instancia con nombre de servicio es MSOLAP$ InstanceName.  
  
> [!NOTE]  
>  Si se instalan varias instancias, el programa de instalación también instala un servicio redirector que está integrado en el [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] servicio Browser. El servicio redirector es responsable de dirigir clientes a la instancia con nombre correspondiente de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]. El servicio [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Browser siempre se ejecuta en el contexto de seguridad de la cuenta del sistema local, una cuenta de administrador local utilizada por Windows para los servicios del sistema que no tengan acceso a recursos de fuera del equipo local.  
  
 Varias instancias significa que podrá realizar escalamientos verticalmente si instala varias instancias del servidor en el mismo hardware. En Analysis Services en concreto, también significa que podrá admitir diferentes modos de servidor si tiene varias instancias en el mismo servidor, cada una de ellas configurada para ejecutarse en un modo determinado.  
  
 El modo de servidor es una propiedad de servidor que determina el almacenamiento y la arquitectura de memoria que se usarán con esa instancia. Un servidor que se ejecuta en modo multidimensional utiliza el nivel de administración de recursos compilado para las bases de datos multidimensionales de cubo y los modelos de minería de datos. En cambio, el modo de servidor tabular utiliza el motor analítico en memoria VertiPaq y la compresión de datos para agregar datos según se solicite.  
  
 Las diferencias entre el almacenamiento y la arquitectura de memoria significan que una única instancia de Analysis Services ejecutará las bases de datos tabulares o las bases de datos multidimensionales, pero no ambas. La propiedad del modo de servidor determina el tipo de base de datos que se ejecuta en la instancia.  
  
 El modo de servidor se establece durante la instalación al especificar el tipo de base de datos que ejecutará en el servidor. Para admitir todos los modos disponibles, instale varias instancias de Analysis Services, cada una de ellas implementada en un modo de servidor que se corresponda con los proyectos que está generando.  
  
 Por lo general, la mayoría de las tareas administrativas que debe realizar no variarán según el modo. Como administrador del sistema de Analysis Services, puede usar los mismos procedimientos y scripts para administrar cualquier instancia de Analysis Services en su red, independientemente de cómo se haya instalado.  
  
> [!NOTE]  
>  La excepción es [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] para SharePoint. La administración de servidores de una implementación de [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] siempre está en el contexto de una granja de SharePoint. [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] se diferencia de otros modos de servidor en que es siempre de instancia única y se administra siempre a través de Administración central de SharePoint o la Herramienta de configuración de [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] . Aunque es posible conectarse a [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] para SharePoint de SQL Server Management Studio o [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)], no es deseable. Una granja de servidores de SharePoint incluye la infraestructura que sincroniza el estado del servidor y supervisa la disponibilidad del servidor. El uso de otras herramientas puede interferir con estas operaciones. Para obtener más información acerca de [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] administración del servidor, consulte [PowerPivot para SharePoint ](../../analysis-services/power-pivot-sharepoint/power-pivot-for-sharepoint-ssas.md).  
  
## <a name="in-this-section"></a>En esta sección  
  
|Vínculo|Descripción de la tarea|  
|----------|----------------------|  
|[Configuración posterior a la instalación](../../analysis-services/instances/post-install-configuration-analysis-services.md)|Describe las tareas necesarias y opcionales que completan o modifican una instalación de Analysis.|  
|[Conectar a Analysis Services](../../analysis-services/instances/connect-to-analysis-services.md)|Describe las propiedades de cadena de conexión, las bibliotecas de cliente, las metodologías de autenticación y los pasos para establecer o borrar conexiones.|  
|[Supervisar una instancia de Analysis Services](../../analysis-services/instances/monitor-an-analysis-services-instance.md)|Describe las herramientas y técnicas de supervisión de instancias de servidor, incluida una explicación sobre el uso del monitor de rendimiento y SQL Server Profiler.|  
|[Alta disponibilidad y escalabilidad](../../analysis-services/instances/high-availability-and-scalability-in-analysis-services.md)|Describe las técnicas empleadas con más frecuencia para lograr una alta disponibilidad y escalabilidad de las bases de datos de Analysis Services. |  
|[Escenarios de globalización para Analysis Services](../../analysis-services/globalization-scenarios-for-analysis-services.md)|Explica la compatibilidad de intercalación e idioma, los pasos que se deben seguir para cambiar ambas propiedades y sugerencias para configurar y probar el comportamiento de estas.|  
|[Operaciones de registro en Analysis Services](../../analysis-services/instances/log-operations-in-analysis-services.md)|Describe los registros y explica cómo configurarlos.|  
  
  
## <a name="see-also"></a>Vea también  
 [Comparar soluciones tabulares y multidimensionales ](../../analysis-services/comparing-tabular-and-multidimensional-solutions-ssas.md)   
 [Determinar el modo de servidor de una instancia de Analysis Services](../../analysis-services/instances/determine-the-server-mode-of-an-analysis-services-instance.md)  
  
  
