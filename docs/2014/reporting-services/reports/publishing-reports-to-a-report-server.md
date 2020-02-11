---
title: Publicar informes en un servidor de informes | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- production environments [Reporting Services]
- report projects [Reporting Services]
- Debug configuration [Reporting Services]
- report publishing [Reporting Services]
- publishing reports [Reporting Services]
- report properties [Reporting Services]
- Report Designer [Reporting Services], deploying reports
- Production configuration [Reporting Services]
- publishing reports [Reporting Services], production environments
- DebugLocal configuration [Reporting Services]
- deploying [Reporting Services], reports
- Report Designer [Reporting Services], publishing reports
ms.assetid: bd7aa5e0-61ce-43fd-8f74-5d1aeed078bb
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 5c73e75bbdf458b27d0f879a91e72ececc832b88
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "66102493"
---
# <a name="publishing-reports-to-a-report-server"></a>Publicar informes en un servidor de informes
  Después de diseñar y probar un informe o un conjunto de informes, puede utilizar las características de implementación integradas en [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] para publicar los informes en un servidor de informes. Puede publicar informes individuales o un proyecto del servidor de informes. Publicar un proyecto del servidor de informes es la manera más fácil de publicar varios informes. [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]usa el término *implementación*, en lugar del término *publicar*. Las dos condiciones son intercambiables.  
  
 Para poder publicar un informe, debe tener permiso para hacerlo. El permiso se determina a través de la seguridad basada en roles que define el administrador del servidor de informes. Normalmente, las operaciones de publicación se conceden a través del rol Publicador.  
  
 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] proporciona las configuraciones de proyecto para administrar la publicación de informes. La configuración especifica la ubicación del servidor de informes, la versión de SQL Server Reporting Services instalada en el servidor de informes, si los orígenes de datos publicados en el servidor de informes se sobrescriben y otras opciones. Además de utilizar las configuraciones que [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] proporciona, puede crear otras adicionales.  
  
## <a name="project-configurations"></a>Configuraciones del proyecto  
 Los informes se generan antes de publicarse para asegurarse de que solo las definiciones de informe válidas se publiquen en el servidor de informes. Las configuraciones de proyecto incluyen propiedades para generar los informes, como la carpeta en la que almacenar temporalmente los informes integrados y cómo administrar los problemas de generación. Las configuraciones también tienen las propiedades que se utilizan para especificar la ubicación, la versión y las carpetas del servidor de informes.  
  
 De forma predeterminada, [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] proporciona tres configuraciones de proyecto: depuración local, depuración y lanzamiento. La configuración predeterminada es de depuración local. Normalmente, se utiliza la configuración de depuración local para ver informes en una ventana de vista previa local, la configuración de depuración para publicar informes en un servidor de pruebas y la configuración de lanzamiento para publicar los informes en un servidor de producción. En la lista desplegable de configuraciones de soluciones de la barra de herramientas estándar, se muestra la configuración activa. Para utilizar una configuración diferente, selecciónela en la lista.  
  
 El entorno de informes podría tener varios servidores de informes y versiones diferentes de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] instaladas. Puede crear varias configuraciones y, a continuación, utilizar una diferente según el escenario de implementación. Para obtener más información, vea [implementación y compatibilidad de versiones en SQL Server Data Tools &#40;SSRS&#41;](../tools/deployment-and-version-support-in-sql-server-data-tools-ssrs.md) y [establecer las propiedades de implementación &#40;Reporting Services ](../tools/set-deployment-properties-reporting-services.md)&#41;.  
  
## <a name="publishing-reports"></a>Publicar informes  
 Puede publicar un informe único o un proyecto del servidor de informes que contenga varios informes. Para obtener instrucciones sobre cómo publicar informes, vea [publicar informes](../publish-reports.md).  
  
### <a name="publishing-a-single-report"></a>Publicar un solo informe  
 Si no desea publicar todos los informes de un proyecto, puede optar por publicar uno solo. Para ello, seleccione una configuración que implemente el informe (por ejemplo, la configuración de lanzamiento), haga clic con el botón derecho en el informe y, después, haga clic en **Implementar**.  
  
 Si un informe utiliza un origen de datos compartido, también tiene que implementar el origen de datos compartido o el informe implementado no se ejecutará. Haga clic con el botón derecho en el origen de datos compartido y, después, haga clic en **Implementar**.  
  
 Se debe especificar la dirección URL del servidor de destino del servidor de informes y puede ser conveniente cambiar las carpetas predeterminadas en las que los informes y orígenes de datos compartidos se implementan.  
  
### <a name="publishing-multiple-reports"></a>Publicar varios informes  
 Cuando se publica un proyecto del servidor de informes, se publican todos los informes del proyecto. Todos los informes se implementan utilizando la misma configuración de proyecto: el mismo servidor de informes, la misma carpeta en el servidor, etc. Para publicar informes en servidores diferentes, publíquelos uno por uno o incluya solo los que desee en el proyecto del servidor de informes. Una solución puede incluir varios proyectos del servidor de informes. Utilizar varios proyectos podría facilitar la administración de la implementación de informes porque se puede usar una configuración diferente para implementar proyectos distintos.  
  
## <a name="see-also"></a>Consulte también  
 [Páginas de propiedades del proyecto (cuadro de diálogo)](../tools/project-property-pages-dialog-box.md)   
 [Administración de contenido del servidor de informes &#40;Modo nativo de SSRS&#41;](../report-server/report-server-content-management-ssrs-native-mode.md)   
 [Actualización de informes](../install-windows/upgrade-reports.md)  
  
  
