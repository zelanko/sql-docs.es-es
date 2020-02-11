---
title: Agregar un servidor de informes adicional a una granja de servidores (escalabilidad horizontal de SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
ms.assetid: c1a6b683-15cf-44ae-ac60-ceee63a60aaf
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: b90bb5624e5b5cdbf3f1542ad0bef0d2765da248
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "66108965"
---
# <a name="add-an-additional-report-server-to-a-farm-ssrs-scale-out"></a>Agregar un servidor de informes adicional a una granja de servidores (escalado horizontal de SSRS)
  Agregar un segundo servidor de informes en modo de SharePoint o varios a una granja de servidores de SharePoint puede mejorar el rendimiento y el tiempo de respuesta de procesamiento del servidor de informes. Si ha detectado una disminución del rendimiento al agregar más usuarios, informes y otras aplicaciones al servidor de informes, agregar servidores adicionales puede mejorar el rendimiento. También se recomienda agregar un segundo servidor de informes para aumentar la disponibilidad de los servidores de informes cuando hay problemas de hardware o cuando se realiza el mantenimiento general en servidores individuales del entorno. A partir de la versión [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] , los pasos para escalar horizontalmente un entorno de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] en modo de SharePoint siguen la implementación estándar de la granja de servidores de SharePoint y aprovechan las características de equilibrio de carga de SharePoint.  
  
> [!IMPORTANT]  
>  El escalado horizontal de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] no se admite en ninguna de las ediciones de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Para obtener más información, vea [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] la sección de [características admitidas por las ediciones de SQL Server 2014](../../../2014/getting-started/features-supported-by-the-editions-of-sql-server-2014.md).  
  
> [!TIP]  
>  A partir de [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] , no se usa el Administrador de configuración de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] para agregar servidores y escalar horizontalmente los servidores de informes. Los productos de SharePoint administran el escalado horizontal de servicios de informes a medida que los servidores SharePoint con el servicio [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] se agregan a la granja.  
  
 Para obtener más información sobre cómo escalar horizontalmente los servidores de informes en modo nativo, vea [Configurar una implementación escalada horizontalmente del servidor de informes en modo nativo &#40;Administrador de configuración de SSRS&#41;](../../reporting-services/install-windows/configure-a-native-mode-report-server-scale-out-deployment.md).  
  
-   [Equilibrio de carga](#bkmk_loadbalancing)  
  
-   [Requisitos previos](#bkmk_prerequisites)  
  
-   [Pasos](#bkmk_steps)  
  
-   [Configuración adicional](#bkmk_additional)  
  
##  <a name="bkmk_loadbalancing"></a>Equilibrio de carga  
 SharePoint administra automáticamente el equilibrio de carga de las aplicaciones de servicios de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] a menos que el entorno tenga una solución personalizada o de terceros para el equilibrio de carga. El comportamiento predeterminado de equilibrio de carga de SharePoint consiste en que cada aplicación de servicios de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] se equilibrará en todos los servidores de aplicaciones que ha iniciado el servicio [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] . Para comprobar si el servicio [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] está instalado y se ha iniciado, haga clic en **Administrar servicios en el servidor** en Administración central de SharePoint.  
  
##  <a name="bkmk_prerequisites"></a> Requisitos previos  
  
-   Debe ser administrador local para ejecutar el programa de instalación de SQL Server.  
  
-   El equipo debe estar unido a un dominio.  
  
-   Debe saber el nombre del servidor de bases de datos existente que hospeda la configuración de SharePoint y las bases de datos de contenido.  
  
-   El servidor de bases de datos debe estar configurado para permitir las conexiones de base de datos remota.  Si no lo está, no podrá combinar el nuevo servidor con la granja de servidores porque el nuevo servidor no podrá establecer una conexión a las bases de datos de configuración de SharePoint.  
  
-   El nuevo servidor deberá tener instalada la misma versión de SharePoint que están ejecutando los servidores actuales de la granja. Por ejemplo, si la granja de servidores ya tiene instalado SharePoint 2010 Service Pack 1 (SP1), deberá instalar también SP1 en el nuevo servidor para poder combinar la granja de servidores.  
  
-   Revise los siguientes temas adicionales para conocer los requisitos del sistema y de las versiones:  
  
     [Instrucciones para usar las características de SQL Server BI en una granja de servidores de SharePoint 2010](../../../2014/sql-server/install/guidance-for-using-sql-server-bi-features-in-a-sharepoint-2010-farm.md)  
  
##  <a name="bkmk_steps"></a>Pasos  
 En los pasos de este tema se supone que el administrador de una granja de servidores de SharePoint va a instalar y configurar el servidor. En el diagrama se muestra un entorno típico de tres niveles. Los elementos numerados en el diagrama se describen en la siguiente lista:  
  
-   (1) Varios servidores front-end web (WFE). Los servidores WFE requieren el complemento [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] para SharePoint 2010.  
  
-   (2) Un único servidor de aplicaciones que ejecuta [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] y los sitios web, por ejemplo, Administración central. Los pasos siguientes agregan un segundo servidor de aplicaciones en este nivel.  
  
-   (3) Dos servidores de base de datos de SQL Server.  
  
-   (4) Representa una solución de equilibrio de carga de red (NLB) de software o hardware  
  
 ![Agregar un servidor de aplicaciones de Reporting Services](../../../2014/sql-server/install/media/rs-sharepointscale.gif "Agregar un servidor de aplicaciones de Reporting Services")  
  
 En los siguientes pasos se supone que un administrador va a instalar y configurar el servidor. El servidor se configurará como un nuevo servidor de aplicaciones de la granja de servidores y no se usa como front-end web (WFE).  
  
|Paso|Descripción y vínculo|  
|----------|--------------------------|  
|Ejecutar la herramienta de preparación de Productos de SharePoint 2010|Debe tener el disco de instalación para SharePoint 2010. La herramienta de preparación es **PrerequisiteInstaller. exe** en los medios de instalación de.|  
|Instalar un producto de SharePoint 2010.|1) Seleccione el tipo de instalación **granja de servidores** .<br /><br /> 2) Seleccione **completo** para el tipo de servidor.<br /><br /> 3) Una vez completada la instalación, no ejecute el Asistente para configuración de Productos de SharePoint si la granja de servidores de SharePoint existente tiene instalado SharePoint 2010 SP1. Debe instalar SharePoint SP1 antes de ejecutar el Asistente para configuración de Productos de SharePoint.|  
|Instalar SharePoint Server 2010 SP1.|Si su granja de servidores de SharePoint existente tiene instalado SharePoint 2010 SP1, descargue e instale SharePoint[https://support.microsoft.com/kb/2460045](https://go.microsoft.com/fwlink/p/?linkID=219697)2010 SP1 desde:.<br /><br /> Para obtener más información acerca de SharePoint 2010 SP1, vea [Problemas conocidos al instalar Office 2010 SP1 y SharePoint 2010 SP1](https://support.microsoft.com/kb/2532126):|  
|Ejecutar el Asistente para configuración de Productos de SharePoint para agregar el servidor a la granja.|1) en el grupo de programas **productos de Microsoft sharepoint 2010** , haga clic en el **Asistente para configuración de productos de Microsoft SharePoint 2010**.<br /><br /> 2) en la página **conectar a una granja de servidores** , seleccione **conectar a una granja** de servidores existente y haga clic en **siguiente**.<br /><br /> 3) en la página **especificar las opciones** de la base de datos de configuración, escriba el nombre del servidor de bases de datos usado para la granja existente y el nombre de la base de datos de configuración. Haga clic en **Next**.<br />** \* Importante \* \* ** Si ve un mensaje de error similar al siguiente y ha comprobado que tiene permisos, compruebe qué protocolos están habilitados para la SQL Server configuración de red en **SQL Server Configuration Manager**: "no se pudo conectar al servidor de base de datos. Asegúrese de que la base de datos existe, es un servidor SQL Server y de que tiene los permisos adecuados para obtener acceso al servidor ".<br />** \* Importante \* \* ** Si ve la página estado de la **granja de servidores y el estado**de la revisión, tendrá que revisar la información de la página y actualizar el servidor con los archivos necesarios antes de continuar con la Unión del servidor a la granja.<br /><br /> 4) en la página **especificar la configuración de seguridad del conjunto de servidores** , escriba la frase de contraseña de la granja y haga clic en **siguiente**. Haga clic en **Siguiente** en la página de confirmación para ejecutar el asistente.<br /><br /> 5) haga clic en **siguiente** para ejecutar el **Asistente para configuración de granja de servidores**.|  
|Comprobar que el servidor se ha agregado a la granja de servidores de SharePoint.|1) En Administración central de SharePoint, haga clic en **Administrar servidores en esta granja de servidores** en el grupo **Configuración del sistema** .<br /><br /> 2) Compruebe que el nuevo servidor se agrega y que el estado es correcto.<br /><br /> 3) tenga en cuenta que no ve el servicio **SQL Server Reporting Services** servicio en ejecución. El servicio se instalará en el paso siguiente.<br /><br /> 4) para quitar este servidor del rol de WFE, haga clic en **administrar servicios en el servidor** y detenga el servicio **aplicación Web de Microsoft SharePoint Foundation**.|  
|Instalar y configurar el modo de SharePoint de Reporting Services.|Ejecute la instalación de [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] . Para obtener más información acerca de la [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] instalación del modo de SharePoint de, vea [instalar el modo de SharePoint de Reporting Services para SharePoint 2010](../../../2014/sql-server/install/install-reporting-services-sharepoint-mode-for-sharepoint-2010.md) si el servidor solo se va a usar como servidor de aplicaciones y el servidor no se utilizará como WFE, no es necesario seleccionar **Reporting Services complemento para productos de SharePoint** en:<br /><br /> en la página **rol de instalación** , seleccione **SQL Server instalación de características** .<br /><br /> la página **selección de características** , seleccione **Reporting Services-SharePoint**<br /><br /> O<br /><br /> en la página **configuración de Reporting Services** , compruebe que la opción **solo instalar** está seleccionada para **Reporting Services modo de SharePoint**.|  
|Comprobar que Reporting Services está operativo.|1) En Administración central de SharePoint, haga clic en **Administrar servidores en esta granja de servidores** en el grupo **Configuración del sistema** .<br /><br /> 2) Compruebe el servicio **SQL Server Reporting Services**.<br /><br /> Para obtener más información, vea [comprobar una instalación de Reporting Services](../../reporting-services/install-windows/verify-a-reporting-services-installation.md) .|  
  
##  <a name="bkmk_additional"></a>Configuración adicional  
 Puede optimizar servidores individuales de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] en una implementación escalada horizontalmente para realizar el procesamiento en segundo plano únicamente ya que no compiten por los recursos con la ejecución de informes interactiva. El procesamiento en segundo plano incluye programaciones, suscripciones y alertas de datos.  
  
 Para cambiar el comportamiento de servidores de informes individuales, establezca ** \<IsWebServiceEnable>** en false en el archivo de configuración **RSreportServer. config** .  
  
 De forma predeterminada, los servidores están configurados con \<IsWebServiceEnable> establecido en TRUE. Cuando todos los servidores están configurados en TRUE, los interactivos y los de reserva tendrán equilibrio de carga en todos los nodos de la granja.  
  
 Si configura todos los servidores de informes con \<IsWebServiceEnable> establecido en False, verá un mensaje de error similar al siguiente al intentar usar las características de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]:  
  
 El servicio web de Reporting Services no está habilitado. Configure al menos una instancia del servicio Reporting Services SharePoint para tener \<IsWebServiceEnable> establecido en true. Para obtener más información, vea [modificar un archivo de configuración de Reporting Services &#40;RSreportserver. config&#41;](../report-server/modify-a-reporting-services-configuration-file-rsreportserver-config.md)  
  
## <a name="see-also"></a>Consulte también  
 [Agregar servidores web o de aplicaciones a las granjas de SharePoint 2013](https://technet.microsoft.com/library/cc261752.aspx)   
 [Configurar los servicios (SharePoint Server 2010)](https://technet.microsoft.com/library/ee794878.aspx)  
  
  
