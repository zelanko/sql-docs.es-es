---
title: Implementación y compatibilidad de versiones en SQL Server Data Tools (SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
ms.assetid: 36f5686d-7e40-4f31-be81-bd197ca33a02
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: bfac4568659d03f62294bf6159604ce6230639d2
ms.sourcegitcommit: 8d6fb6bbe3491925909b83103c409effa006df88
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/22/2019
ms.locfileid: "59959081"
---
# <a name="deployment-and-version-support-in-sql-server-data-tools-ssrs"></a>Implementación y compatibilidad de versiones en las herramientas de datos de SQL Server (SSRS)
  [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)] admite los escenarios siguientes:  
  
-   Abrir definiciones de informe (*.rdl) y proyectos de servidor de informes (\*.rptproj).  
  
-   Generar definiciones de informes.  
  
-   Obtener una vista previa de informes en el Diseñador de informes.  
  
-   Implementar informes en servidores de informes.  
  
##  <a name="bkmk_ConfigurationandDeploymentProperties"></a> Propiedades de configuración e implementación  
 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] es compatible con las configuraciones de proyectos. La configuración de un proyecto consta de un conjunto de propiedades que especifican las ubicaciones y los comportamientos cuando un proyecto se integra como un paso, bien en una vista previa o bien en la implementación de informes. Para obtener más información acerca de las configuraciones de proyecto, vea la documentación de Visual Studio.  
  
 Use las configuraciones de proyecto para controlar la actualización de las definiciones de informe en las versiones de esquema compatibles con los servidores de informes de destino. Entre las propiedades que se controlan mediante configuraciones de proyecto se incluyen el servidor de informes de destino, la carpeta donde el proceso de compilación almacena temporalmente las definiciones de informe para la vista previa e implementación, y los niveles de error.  
  
 Los informes se compilan antes de representarse como vistas previas en el Diseñador de informes o antes de implementarse en el servidor de informes.  
  
 Las propiedades de configuración se establecen en el cuadro de diálogo [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] **de** .  
  
 Entre las propiedades de generación e implementación se incluyen:  
  
-   OutputPath es una propiedad de generación que identifica la ruta de acceso de las carpetas donde almacenar la definición de informe que se usa en la comprobación de la generación, la implementación y la vista previa de informes.  
  
-   ErrorLevel es una propiedad de generación que identifica la severidad de los problemas de la generación que se notifican como errores. Los problemas con un nivel de gravedad menor o igual que el valor de ErrorLevel se notifican como errores; de lo contrario, se notifican como advertencias. Para obtener más información, vea la sección "Validación de informes y niveles de Error" de [Diseño de informes con el Diseñador de informes &#40;SSRS&#41;](design-reporting-services-paginated-reports-with-report-designer-ssrs.md).  
  
-   TargetServerVersion es una propiedad de implementación que identifica la versión esperada de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] que está instalada en el servidor de informes de destino especificado en la propiedad TargetServerURL.  
  
 Al especificar la versión anterior de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] en el cuadro de diálogo **Propiedad del proyecto** , los informes no revierten automáticamente a la versión anterior. Por tanto, un proyecto del servidor de informes puede contener informes de dos versiones diferentes de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Cuando se implementa el proyecto del servidor de informes, todos los informes del proyecto se convierten a la versión especificada en TargetServerVersion.  
  
 Puede agregar a un proyecto más de una configuración de proyecto; cada una se usa para un escenario diferente, por ejemplo en la implementación en distintas versiones de los servidores de informes. Para obtener más información, vea [Establecer propiedades de implementación &#40;Reporting Services&#41;](set-deployment-properties-reporting-services.md) y [Páginas de propiedades del proyecto (cuadro de diálogo)](project-property-pages-dialog-box.md).  
  
##  <a name="bkmk_SupportedVersions"></a> Versiones admitidas  
  
> [!NOTE]  
>  [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)], el entorno de desarrollo de 32 bits para proyectos de servidor de informes, no está diseñado para ejecutarse en equipos basados en [!INCLUDE[vcpritanium](../../includes/vcpritanium-md.md)]y no se instala en servidores basados en [!INCLUDE[vcpritanium](../../includes/vcpritanium-md.md)]. En cambio, [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)] sí es compatible con los equipos basados en x64.  
  
 En la tabla siguiente se describen las versiones compatibles para crear y publicar los informes en [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)].  
  
> [!NOTE]  
>  El esquema no ha cambiado desde [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)].  
  
|Tipo de archivo o proyecto|Versión|Crear informes|Publicar informes|Notas|  
|--------------------------|-------------|--------------------|---------------------|-----------|  
|Proyecto de servidor de informes<br /><br /> o Administrador de configuración de<br /><br /> Proyecto de asistente de proyectos de servidor de informes|[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]|Esquema RDL 2014|[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]||  
|Proyecto de servidor de informes<br /><br /> o Administrador de configuración de<br /><br /> Proyecto de asistente de proyectos de servidor de informes|[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]|Esquema RDL 2012|[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]||  
|Proyecto de servidor de informes<br /><br /> o Administrador de configuración de<br /><br /> Proyecto de asistente de proyectos de servidor de informes|[!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]|Esquema RDL 2008 R2|[!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]||  
|Proyecto de servidor de informes<br /><br /> o Administrador de configuración de<br /><br /> Proyecto de asistente de proyectos de servidor de informes|[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]|Esquema RDL 2008|[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] Solo el servidor de informes|Actualiza localmente el esquema RDL 2003 y RDL 2005 al esquema RDL 2008.|  
|Proyecto de servidor de informes<br /><br /> o Administrador de configuración de<br /><br /> Proyecto de asistente de proyectos de servidor de informes|[!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]|Esquema RDL 2005|[!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] o [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] servidor de informes||  
|Proyecto de servidor de informes|[!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)]|Esquema RDL 2003|No compatible||  
|Diseñador de informes RDLC de [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)]|[!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] 2005<br /><br /> [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] 2008|Esquema RDL 2005|No compatible|No admite el esquema RDL 2008.|  
|Controles de visor de [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)]|[!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] 2005<br /><br /> [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] 2008|RDL 2008 no se admite en modo local|N/D|Pueden verse informes RDL 2008 en el servidor de informes de [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] en modo de servidor.|  
  
 Para obtener más información sobre la forma de abrir informes en una versión anterior del esquema de definición de informes, vea [Actualizar informes](../install-windows/upgrade-reports.md). Para obtener más información sobre esquemas de definición de informe concretos, vea la [SQL Server RDL Specification](https://go.microsoft.com/fwlink/?linkid=116865).  
  
## <a name="see-also"></a>Vea también  
 [Publicar orígenes de datos e informes](../reports/publishing-data-sources-and-reports.md)  
  
  
