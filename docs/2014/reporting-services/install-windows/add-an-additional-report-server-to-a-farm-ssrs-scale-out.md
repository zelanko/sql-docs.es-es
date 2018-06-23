---
title: Agregar un servidor de informes adicional a una granja de servidores (escalabilidad horizontal de SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: c1a6b683-15cf-44ae-ac60-ceee63a60aaf
caps.latest.revision: 9
author: markingmyname
ms.author: maghan
manager: jhubbard
ms.openlocfilehash: e3f59bd35ed4886c5c8ce35107120ab9a5eca87f
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36196400"
---
# <a name="add-an-additional-report-server-to-a-farm-ssrs-scale-out"></a>Agregar un servidor de informes adicional a una granja de servidores (escalado horizontal de SSRS)
  Agregar un segundo servidor de informes en modo de SharePoint o varios a una granja de servidores de SharePoint puede mejorar el rendimiento y el tiempo de respuesta de procesamiento del servidor de informes. Si ha detectado una disminución del rendimiento al agregar más usuarios, informes y otras aplicaciones al servidor de informes, agregar servidores adicionales puede mejorar el rendimiento. También se recomienda agregar un segundo servidor de informes para aumentar la disponibilidad de los servidores de informes cuando hay problemas de hardware o cuando se realiza el mantenimiento general en servidores individuales del entorno. A partir de la versión [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] , los pasos para escalar horizontalmente un entorno de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] en modo de SharePoint siguen la implementación estándar de la granja de servidores de SharePoint y aprovechan las características de equilibrio de carga de SharePoint.  
  
> [!IMPORTANT]  
>  El escalado horizontal de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] no se admite en ninguna de las ediciones de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Para obtener más información, consulte el [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] sección de [características compatibles con las ediciones de SQL Server 2014](../../../2014/getting-started/features-supported-by-the-editions-of-sql-server-2014.md).  
  
> [!TIP]  
>  A partir de [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] , no se usa el Administrador de configuración de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] para agregar servidores y escalar horizontalmente los servidores de informes. Los productos de SharePoint administran el escalado horizontal de servicios de informes a medida que los servidores SharePoint con el servicio [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] se agregan a la granja.  
  
 Para obtener más información sobre cómo escalar horizontalmente los servidores de informes en modo nativo, vea [Configurar una implementación escalada horizontalmente del servidor de informes en modo nativo &#40;Administrador de configuración de SSRS&#41;](../../reporting-services/install-windows/configure-a-native-mode-report-server-scale-out-deployment.md).  
  
-   [Equilibrio de carga](#bkmk_loadbalancing)  
  
-   [Requisitos previos](#bkmk_prerequisites)  
  
-   [Pasos](#bkmk_steps)  
  
-   [Configuración adicional](#bkmk_additional)  
  
##  <a name="bkmk_loadbalancing"></a> Equilibrio de carga  
 SharePoint administra automáticamente el equilibrio de carga de las aplicaciones de servicios de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] a menos que el entorno tenga una solución personalizada o de terceros para el equilibrio de carga. El comportamiento predeterminado de equilibrio de carga de SharePoint consiste en que cada aplicación de servicios de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] se equilibrará en todos los servidores de aplicaciones que ha iniciado el servicio [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] . Para comprobar si el servicio [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] está instalado y se ha iniciado, haga clic en **Administrar servicios en el servidor** en Administración central de SharePoint.  
  
##  <a name="bkmk_prerequisites"></a> Requisitos previos  
  
-   Debe ser administrador local para ejecutar el programa de instalación de SQL Server.  
  
-   El equipo debe estar unido a un dominio.  
  
-   Debe saber el nombre del servidor de bases de datos existente que hospeda la configuración de SharePoint y las bases de datos de contenido.  
  
-   El servidor de bases de datos debe estar configurado para permitir las conexiones de base de datos remota.  Si no lo está, no podrá combinar el nuevo servidor con la granja de servidores porque el nuevo servidor no podrá establecer una conexión a las bases de datos de configuración de SharePoint.  
  
-   El nuevo servidor deberá tener instalada la misma versión de SharePoint que están ejecutando los servidores actuales de la granja. Por ejemplo, si la granja de servidores ya tiene instalado SharePoint 2010 Service Pack 1 (SP1), deberá instalar también SP1 en el nuevo servidor para poder combinar la granja de servidores.  
  
-   Revise los siguientes temas adicionales para conocer los requisitos del sistema y de las versiones:  
  
     [Instrucciones para usar características de BI de SQL Server en una granja de servidores de SharePoint 2010](../../../2014/sql-server/install/guidance-for-using-sql-server-bi-features-in-a-sharepoint-2010-farm.md)  
  
##  <a name="bkmk_steps"></a> Pasos  
 En los pasos de este tema se supone que el administrador de una granja de servidores de SharePoint va a instalar y configurar el servidor. En el diagrama se muestra un entorno típico de tres niveles. Los elementos numerados en el diagrama se describen en la siguiente lista:  
  
-   (1) Varios servidores front-end web (WFE). Los servidores WFE requieren el complemento [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] para SharePoint 2010.  
  
-   (2) Un único servidor de aplicaciones que ejecuta [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] y los sitios web, por ejemplo, Administración central. Los pasos siguientes agregan un segundo servidor de aplicaciones en este nivel.  
  
-   (3) Dos servidores de base de datos de SQL Server.  
  
-   (4) Representa una solución de equilibrio de carga de red (NLB) de software o hardware  
  
 ![Adición de un servidor de aplicaciones de Reporting Services](../../../2014/sql-server/install/media/rs-sharepointscale.gif "Adición de un servidor de aplicaciones de Reporting Services")  
  
 En los siguientes pasos se supone que un administrador va a instalar y configurar el servidor. El servidor se configurará como un nuevo servidor de aplicaciones de la granja de servidores y no se usa como front-end web (WFE).  
  
|Paso|Descripción y vínculo|  
|----------|--------------------------|  
|Ejecutar la herramienta de preparación de Productos de SharePoint 2010|Debe tener el disco de instalación para SharePoint 2010. La herramienta de preparación es **PrerequisiteInstaller.exe** en los discos de instalación.|  
|Instalar un producto de SharePoint 2010.|1) seleccione el **granja de servidores** tipo de instalación.<br /><br /> (2) seleccione **completar** para el tipo de servidor.<br /><br /> 3) Una vez completada la instalación, no ejecute el Asistente para configuración de Productos de SharePoint si la granja de servidores de SharePoint existente tiene instalado SharePoint 2010 SP1. Debe instalar SharePoint SP1 antes de ejecutar el Asistente para configuración de Productos de SharePoint.|  
|Instalar SharePoint Server 2010 SP1.|Si la granja de servidores de SharePoint existente tiene instalado SharePoint 2010 SP1 Descargue e instale SharePoint 2010 SP1 desde:[http://support.microsoft.com/kb/2460045](http://go.microsoft.com/fwlink/p/?linkID=219697).<br /><br /> Para obtener más información acerca de SharePoint 2010 SP1, vea [Problemas conocidos al instalar Office 2010 SP1 y SharePoint 2010 SP1](http://support.microsoft.com/kb/2532126):|  
|Ejecutar el Asistente para configuración de Productos de SharePoint para agregar el servidor a la granja.|(1) en el **productos de Microsoft SharePoint 2010** grupo de programas, haga clic en **Asistente para configuración de productos de Microsoft SharePoint 2010**.<br /><br /> 2) en el **conectar a una granja de servidores** página, seleccione **conectar a una granja existente** y haga clic en **siguiente**.<br /><br /> (3) en el **especificar opciones de base de datos de configuración** página, escriba el nombre del servidor de base de datos utilizado para la granja de servidores existente y el nombre de la base de datos de configuración. Haga clic en **Siguiente**.<br />**\*\* Importante \* \***  si aparece un mensaje de error similar al siguiente y se ha comprobado que tiene permisos, a continuación, compruebe qué protocolos están habilitados para la configuración de red de SQL Server en **Sql Server Administrador de configuración de**: "no se pudo conectar al servidor de base de datos. Asegúrese de la base de datos existe, es un servidor Sql Server, y que tiene los permisos adecuados para tener acceso al servidor. "<br />**\*\* Importante \* \***  si ve la página **de los productos y estado de la revisión**, debe revisar la información de la página y actualizar el servidor con los archivos necesarios para poder continuar y unir el servidor a la granja de servidores.<br /><br /> (4) en el **especifique la configuración de seguridad de granja** página, escriba la frase de contraseña de la granja de servidores y haga clic en **siguiente**. Haga clic en **Siguiente** en la página de confirmación para ejecutar el asistente.<br /><br /> 5) haga clic en **siguiente** para ejecutar el **Asistente de configuración de granja de servidores**.|  
|Comprobar que el servidor se ha agregado a la granja de servidores de SharePoint.|1) En Administración central de SharePoint, haga clic en **Administrar servidores en esta granja de servidores** en el grupo **Configuración del sistema** .<br /><br /> 2) Compruebe que el nuevo servidor se agrega y que el estado es correcto.<br /><br /> (3) Observe que no muestra el servicio **servicio de SQL Server Reporting Services** ejecutando. El servicio se instalará en el paso siguiente.<br /><br /> (4) para quitar este servidor del rol de WFE, haga clic en **administrar servicios en el servidor** y detener el servicio **aplicación Web de Microsoft SharePoint Foundation**.|  
|Instalar y configurar el modo de SharePoint de Reporting Services.|Ejecute la instalación de [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] . Para obtener más información sobre la instalación de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] modo de SharePoint, vea [instalar Reporting Services SharePoint Mode for SharePoint 2010](../../../2014/sql-server/install/install-reporting-services-sharepoint-mode-for-sharepoint-2010.md) si el servidor solo se usará como un servidor de aplicaciones y el servidor no se utilizará como WFE, no es necesario seleccionar **complemento de Reporting Services para productos de SharePoint** en:<br /><br /> el **rol de instalación** página, seleccione **instalación de características de SQL Server**<br /><br /> el **selección de características** página, seleccione **Reporting Services - SharePoint**<br /><br /> -O bien-<br /><br /> el **configuración de Reporting Services** de comprobación de páginas la **solo instalar** opción está seleccionada para **Reporting Services SharePoint Mode**.|  
|Comprobar que Reporting Services está operativo.|1) En Administración central de SharePoint, haga clic en **Administrar servidores en esta granja de servidores** en el grupo **Configuración del sistema** .<br /><br /> 2) Compruebe el servicio **SQL Server Reporting Services**.<br /><br /> Para obtener más información, vea [Verify a Reporting Services Installation](../../reporting-services/install-windows/verify-a-reporting-services-installation.md).|  
  
##  <a name="bkmk_additional"></a> Configuración adicional  
 Puede optimizar servidores individuales de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] en una implementación escalada horizontalmente para realizar el procesamiento en segundo plano únicamente ya que no compiten por los recursos con la ejecución de informes interactiva. El procesamiento en segundo plano incluye programaciones, suscripciones y alertas de datos.  
  
 Para cambiar el comportamiento de servidores de informes individuales, establezca **\<IsWebServiceEnable>** en el archivo de configuración **RSreportServer.config**.  
  
 De forma predeterminada, los servidores están configurados con \<IsWebServiceEnable> establecido en TRUE. Cuando todos los servidores están configurados en TRUE, los interactivos y los de reserva tendrán equilibrio de carga en todos los nodos de la granja.  
  
 Si configura todos los servidores de informes con \<IsWebServiceEnable> establecido en False, verá un mensaje de error similar al siguiente al intentar usar las características de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]:  
  
 El servicio web de Reporting Services no está habilitado. Configurar al menos una instancia de que el servicio de SharePoint de Reporting Services que \<IsWebServiceEnable > establecido en true. Para obtener más información, vea [Modificar un archivo de configuración de Reporting Services &#40;RSreportserver.config&#41;](../report-server/modify-a-reporting-services-configuration-file-rsreportserver-config.md).  
  
## <a name="see-also"></a>Vea también  
 [Agregar servidores web o aplicación a las granjas de SharePoint 2013](http://technet.microsoft.com/library/cc261752.aspx)   
 [Configurar los servicios (SharePoint Server 2010)](http://technet.microsoft.com/library/ee794878.aspx)  
  
  