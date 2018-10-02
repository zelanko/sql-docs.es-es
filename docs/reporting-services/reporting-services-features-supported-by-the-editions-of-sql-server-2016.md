---
title: Características de Reporting Services compatibles con las ediciones de SQL Server 2016 | Microsoft Docs
ms.date: 05/30/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.technology: reporting-services
ms.topic: conceptual
ms.assetid: 39f03d2d-6e48-4b34-a9d3-07f86313b937
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 757e8652993e4bed8df1095eaec7252be9df13b7
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 10/01/2018
ms.locfileid: "47779653"
---
# <a name="reporting-services-features-supported-by-the-editions-of-sql-server-2016"></a>Características de Reporting Services compatibles con las ediciones de SQL Server 2016

En este tema se indica información detallada de las características admitidas por las diversas ediciones de SQL Server 2016.  
  
 La edición de evaluación de SQL Server está disponible durante un período de prueba de 180 días.  
  
 Para consultar las notas de la última versión, vea [SQL Server 2016 Release Notes](../sql-server/sql-server-2016-release-notes.md). Para obtener la información más reciente sobre novedades, consulte [Novedades de Reporting Services (SSRS)](~/reporting-services/what-s-new-in-sql-server-reporting-services-ssrs.md).
    
 **Pruebe SQL Server 2016.**    
    
 > [![Descargar desde el Centro de evaluación](../analysis-services/media/download.png)](https://www.microsoft.com/en-us/evalcenter/evaluate-sql-server-2016) **[Descargar SQL Server 2016 desde el Centro de evaluación](https://www.microsoft.com/en-us/evalcenter/evaluate-sql-server-2016)**    
    
> ![Máquina virtual de Azure pequeña](../analysis-services/media/azure-virtual-machine-small.png) **[Poner en marcha una máquina virtual con SQL Server 2016 ya instalado](https://azure.microsoft.com/marketplace/partners/microsoft/sqlserver2016rtmenterprisewindowsserver2012r2/?wt.mc_id=sqL16_vm)**    

Para conocer las características admitidas por las ediciones Evaluation y Developer, consulte SQL Server Enterprise Edition.

Para navegar por la tabla para buscar una tecnología de SQL Server, haga clic en su vínculo:  

-   [Reporting Services](#SSRS)  
  
-   [Clientes de Business Intelligence](#BIC)  

##  <a name="SSRS"></a> Reporting Services  
  
|Nombre de la característica|Enterprise|Estándar|Web|Express con Advanced Services|Express con herramientas|Express|Desarrollador|  
|------------------|----------------|--------------|---------|------------------------------------|------------------------|-------------|---------------|  
|Informes móviles y KPI|Sí||||||Sí|  
|Catálogo compatible con la edición DB [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]|Estándar o superior|Estándar o superior|Web|Express|||Estándar o superior|  
|Origen de datos compatibles con la edición [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]|Todas las ediciones de   [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]|Todas las ediciones de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]|Web|Express|||Todas las ediciones de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]|  
|Servidor de informes|Sí|Sí|Sí|Sí|||Sí|  
|Diseñador de informes|Sí|Sí|Sí|Sí|||Sí|  
|Portal web de diseñador de informes|Sí|Sí|Sí|Sí|||Sí|  
|Seguridad basada en roles|Sí|Sí|Sí|Sí|||Sí|  
|Exportar a Excel, PowerPoint, Word, PDF e imágenes|Sí|Sí|Sí|Sí|||Sí|  
|Medidores y gráficos mejorados|Sí|Sí|Sí|Sí|||Sí|  
|Anclar elementos de informe a paneles de [!INCLUDE[sspowerbi](../includes/sspowerbi-md.md)]|Sí|Sí|Sí|Sí|||Sí|  
|Autenticación personalizada|Sí|Sí|Sí|Sí|||Sí|  
|Informe como fuentes de distribución de datos|Sí|Sí|Sí|Sí|||Sí|  
|Compatibilidad con los modelos|Sí|Sí|Sí||||Sí|  
|Crear roles personalizados para la seguridad basada en roles|Sí|Sí|||||Sí|  
|Seguridad de elementos del modelo|Sí|Sí|||||Sí|  
|Clic sobre aviso (click-through) infinito|Sí|Sí|||||Sí|  
|Biblioteca de componentes compartidos|Sí|Sí|||||Sí|  
|Suscripciones y programación de recursos compartidos de archivo y correo electrónico|Sí|Sí|||||Sí|  
|Historial de informes, instantáneas de ejecución y almacenamiento en memoria caché|Sí|Sí|||||Sí|  
|Integración de SharePoint|Sí|Sí|||||Sí|  
|Compatibilidad con orígenes de datos remotos y ajenos a SQL<sup>1</sup>|Sí|Sí|||||Sí|  
|Extensibilidad de orígenes de datos, entrega y representación, RDCE|Sí|Sí|||||Sí|  
|Marca personalizada|Sí||||||Sí|  
|Suscripción a informes controlada por datos|Sí||||||Sí|  
|Implementación escalada (grupo de servidores web)|Sí||||||Sí|  
|Alertas<sup>2</sup>|Sí||||||Sí|  
|[!INCLUDE[ssCrescent](../includes/sscrescent-md.md)] <sup>2</sup>|Sí||||||Sí|  
  
 <sup>1</sup> Para obtener más información sobre los orígenes de datos compatibles con SQL Server 2016 Reporting Services (SSRS), consulte [Orígenes de datos admitidos por Reporting Services &#40;SSRS&#41;](../reporting-services/report-data/data-sources-supported-by-reporting-services-ssrs.md).  
  
 <sup>2</sup> Requiere Reporting Services en el modo de SharePoint. Para obtener más información, vea [Instalar el modo de SharePoint de Reporting Services](../reporting-services/install-windows/install-reporting-services-sharepoint-mode.md).  
  
## <a name="report-server-database-server-edition-requirements"></a>Requisitos de edición de servidor de la base de datos del servidor de informes  
 Al crear una base de datos del servidor de informes, no se pueden usar todas las ediciones de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] para hospedarla. En la tabla siguiente se muestra qué ediciones del [!INCLUDE[ssDE](../includes/ssde-md.md)] se pueden usar para ediciones concretas de [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)].  
  
|Para esta edición de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Reporting Services|Utilice esta edición de la instancia del motor de base de datos para hospedar la base de datos|  
|----------------------------------------------------------------------|---------------------------------------------------------------------------|  
|Enterprise|Edición Enterprise o Standard (local o remota)|  
|Estándar|Edición Enterprise o Standard (local o remota)|  
|Web|Web Edition (solo local)|  
|Express con Advanced Services|Express con Advanced Services (solo local).|  
|Evaluation|Evaluation|  
  
##  <a name="BIC"></a> Clientes de Business Intelligence  
 Las siguientes aplicaciones cliente de software están disponibles en el Centro de descarga de Microsoft y le ayudan a crear documentos de Business Intelligence que se ejecutan en una instancia de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] . Si hospeda estos documentos en un entorno de servidor, use una edición de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] compatible con ese tipo de documento. En la siguiente tabla se indica qué edición de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] tiene las características de servidor necesarias para hospedar los documentos creados en estas aplicaciones cliente.  
  
|Nombre de la herramienta|Enterprise|Estándar|Web|Express con Advanced Services|Express con herramientas|Express|Desarrollador|  
|---------------|----------------|--------------|---------|------------------------------------|------------------------|-------------|---------------|  
|[!INCLUDE[ssRBnoversion](../includes/ssrbnoversion.md)] (.rdl y .rds)|Sí|Sí|||||Sí|  
|[!INCLUDE[SS_MobileReptPub_Long](../includes/ss-mobilereptpub-long.md)] (.rsmobile)|Sí||||||Sí|  
|Aplicaciones de Power BI para dispositivos móviles (iOS, Windows 10 y Android) (.rsmobile)|Sí||||||Sí|  
  
> [!NOTE]  
> 1.  En la tabla anterior se identifican las ediciones de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] necesarias para habilitar estas herramientas de cliente, aunque dichas herramientas pueden obtener acceso a los datos hospedados en cualquier edición de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)].  
> 2.  [!INCLUDE[SS_MobileReptPub_Long](../includes/ss-mobilereptpub-long.md)] es el único punto para crear informes móviles. Conéctese a un servidor de [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] para obtener acceso a orígenes de datos y para crear informes. Luego, publíquelos en el servidor de [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] para que otros usuarios de la organización puedan tener acceso a ellos, ya sea en el servidor o en dispositivos móviles. También puede usar [!INCLUDE[SS_MobileReptPub_Long](../includes/ss-mobilereptpub-long.md)] de modo independiente con orígenes de datos locales.  
> 3.  Tanto si usa  [!INCLUDE[ssRSCurrent](../includes/ssrscurrent-md.md)] de forma local, [!INCLUDE[sspowerbi](../includes/sspowerbi-md.md)] en la nube o ambos como solución de entrega de informes, solo necesita una aplicación móvil para obtener acceso a los paneles e informes móviles desde dispositivos móviles. Las aplicaciones de [!INCLUDE[sspowerbi](../includes/sspowerbi-md.md)] se pueden descargar en las tiendas de aplicaciones de Windows, iOS y Android.  

## <a name="next-steps"></a>Pasos siguientes

[Características compatibles con las ediciones de SQL Server 2016](~/sql-server/editions-and-supported-features-for-sql-server-2016.md)  
[Especificaciones de producto para SQL Server 2016](http://msdn.microsoft.com/library/6445fd53-6844-4170-a86b-7fe76a9f64cb)  
[Instalación de SQL Server 2016](../database-engine/install-windows/installation-for-sql-server-2016.md) 

¿Tiene alguna pregunta más? [Puede plantear sus dudas en el foro de Reporting Services](http://go.microsoft.com/fwlink/?LinkId=620231).
