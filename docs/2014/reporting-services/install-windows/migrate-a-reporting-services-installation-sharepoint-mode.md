---
title: Migrar una instalación de Reporting Services (modo de SharePoint) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 61290949-690a-4e19-b078-57c99b6b30fa
caps.latest.revision: 21
author: markingmyname
ms.author: maghan
manager: jhubbard
ms.openlocfilehash: 655064d54334aa58d8e997c06c08e04a525f350b
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36113100"
---
# <a name="migrate-a-reporting-services-installation-sharepoint-mode"></a>Migrar una instalación de Reporting Services (modo de SharePoint)
  Este tema contiene información general de los pasos necesarios para migrar una implementación del modo de SharePoint de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] desde un entorno de SharePoint a otro. Los pasos concretos pueden ser distintos dependiendo de la versión desde la que esté migrando. Para obtener más información sobre los escenarios de actualización y migración para el modo de SharePoint, vea [Upgrade and Migrate Reporting Services](../../reporting-services/install-windows/upgrade-and-migrate-reporting-services.md). Si solo desea copiar los elementos de informe de un servidor a otro, consulte [Sample Reporting Services rs.exe Script to Migrate Content between Report Servers](../tools/sample-reporting-services-rs-exe-script-to-copy-content-between-report-servers.md).  
  
 Para obtener información sobre cómo migrar una implementación en modo nativo de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] , vea [Migrar una instalación de Reporting Services &#40;modo nativo&#41;](../../reporting-services/install-windows/migrate-a-reporting-services-installation-native-mode.md).  
  
||  
|-|  
|**[!INCLUDE[applies](../../includes/applies-md.md)]**  SharePoint 2010 y SharePoint 2013|  
  
 Un motivo frecuente para completar una migración es cuando se desea actualizar la implementación de SharePoint 2010 a SharePoint 2013. SharePoint 2013 no admite la actualización en contexto desde SharePoint 2010 y se debe completar el procedimiento de **actualizar y adjuntar la base de datos** o realizar una migración solo de contenido.  
  
 Para obtener más información acerca de la actualización de SharePoint 2013, vea lo siguiente:  
  
-   [Información general del proceso de actualización a SharePoint 2013](http://go.microsoft.com/fwlink/p/?LinkId=256688).  
  
-   [Actualizar bases de datos de SharePoint 2010 a SharePoint 2013](http://go.microsoft.com/fwlink/p/?LinkId=256690).  
  
-   [Mover bases de datos de contenido en SharePoint 2013](http://technet.microsoft.com/library/cc262792.aspx).  
  
 
  
##  <a name="bkmk_prior_versions"></a> Migrar desde versiones anteriores a SQL Server 2012 del modo de SharePoint de Reporting Services  
 La arquitectura del modo de SharePoint de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] cambió en [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)], incluido el esquema de la base de datos de aplicación de servicio. Si desea migrar al modo de SharePoint de [!INCLUDE[ssRSCurrent](../../includes/ssrscurrent-md.md)] desde una versión anterior a [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)], cree primero el nuevo entorno de SharePoint instalando SharePoint y el modo de SharePoint de [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] . Para obtener más información, consulte [instalación de modo de SharePoint de Reporting Services &#40;SharePoint 2010 y SharePoint 2013&#41;](../../reporting-services/install-windows/install-reporting-services-sharepoint-mode.md).  
  
 Una vez que el nuevo entorno de SharePoint está en ejecución, puede elegir entre realizar una migración solo de contenido o una migración completa en el nivel de base de datos que incluya las bases de datos de contenido.  
  
###  <a name="bkmk_content_only_migration"></a> Migrar solo contenido  
 **Migración solo de contenido de Reporting Services** : si desea copiar el contenido de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] a una nueva granja, necesita usar herramientas como **rs.exe** para copiar el contenido a la nueva instalación de SharePoint. Para obtener más información acerca de las migraciones solo de contenido, vea lo siguiente:  
  
-   **[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] :** los scripts pueden migrar contenido y recursos entre servidores de informes en modo nativo y en modo de SharePoint. Para obtener más información, consulte [Sample Reporting Services rs.exe Script para migrar contenido entre servidores de informes](../tools/sample-reporting-services-rs-exe-script-to-copy-content-between-report-servers.md) y [script de Reporting Services RS.exe que migra contenido de un servidor de informes a otro](http://azuresql.codeplex.com/releases/view/115207).  
  
-   **Herramienta de migración de Reporting Services:** La herramienta puede copiar los elementos de informe de un servidor en modo nativo en un servidor en modo de SharePoint. Para más información, consulte la página de la [herramienta de migración de Reporting Services](http://www.microsoft.com/download/details.aspx?id=29560).  
  
###  <a name="bkmk_full_migration"></a> Migración completa  
 **Migración completa** : si va a migrar bases de datos de contenido de SharePoint junto con las bases de datos del catálogo de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] a una nueva granja, puede seguir una serie de opciones de copia de seguridad y restauración que se resumen en este tema. En algunos casos necesitará emplear otra herramienta diferente para la fase de restauración que la que usó para la fase de copia de seguridad. Por ejemplo, puede usar el Administrador de configuración de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] para hacer copia de seguridad de las claves de cifrado de una versión anterior de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] , pero necesita usar Administración central de SharePoint o PowerShell para restaurar las claves de cifrado a una instalación en modo de SharePoint de [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] .  
  
####  <a name="bkmk_databases"></a> Bases de datos que verá cuando se complete la migración  
 En la tabla siguiente se describen las bases de datos de SQL Server relacionadas con [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] que tendrá una vez que haya migrado correctamente la instalación en modo de SharePoint de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] :  
  
|Base de datos|Nombre del ejemplo||  
|--------------|------------------|-|  
|Base de datos del catálogo|ReportingService_[GUID de la aplicación de servicio] **(\*)**|Migraciones de usuario.|  
|Base de datos temp|ReportingService_[GUID de la aplicación de servicio]TempDB **(\*)**|Migraciones de usuario.|  
|Base de datos de alertas|ReportingService_[GUID de la aplicación de servicio]_Alerting|Se crea cuando se crea una aplicación de servicio de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] .|  
  
 **(\*)** Los nombres de ejemplo que se muestran en la tabla siguen la convención de nomenclatura que SSRS emplea al crear una nueva aplicación de servicio de SSRS. Si está migrando desde un servidor diferente, el catálogo y las bases de datos tempDB tendrán los nombres de la instalación original.  
  
####  <a name="bkmk_backup_operations"></a> Operaciones de copia de seguridad  
 En esta sección se describen los tipos de información que necesita migrar y las herramientas o los procesos que se usan para completar la copia de seguridad.  
  
 ![Diagrama básico de SSRS SharePoint Migration](../../../2014/sql-server/install/media/rs-sharepoint-migration.gif "Diagrama básico de SSRS SharePoint Migration")  
  
||Objetos|Método|Notas|  
|-|-------------|------------|-----------|  
|**1**|[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] .|**Rskeymgmt.exe** o Administrador de configuración de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] . Vea [Hacer copia de seguridad y restaurar claves de cifrado de Reporting Services](../../reporting-services/install-windows/ssrs-encryption-keys-back-up-and-restore-encryption-keys.md).|Las herramientas indicadas se pueden usar para la copia de seguridad, pero para la operación de restauración usará las páginas de administración de la aplicación de servicio de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] o PowerShell.|  
|**2**|Bases de datos de contenido de SharePoint.||Haga una copia de seguridad de la base de datos y sepárela.<br /><br /> Consulte la sección "Actualización de base de datos adjunta" en [Determinación del enfoque de actualización (SharePoint Server 2010) (http://technet.microsoft.com/library/cc263447.aspx)](http://technet.microsoft.com/library/cc263447.aspx).|  
|**3**|La base de datos de SQL Server que es la base de datos del catálogo de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)].|Hacer copia de seguridad y restaurar bases de datos de SQL Server<br /><br /> o Administrador de configuración de<br /><br /> Adjuntar y separar bases de datos de SQL Server.||  
|**4**|[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] .|Copia de archivos simple.|Solo necesita copiar rsreportserver.config si ha realizado personalizaciones en el archivo. Ejemplo de la ubicación predeterminada de los archivos: C:\Archivos de programa\Archivos comunes\Microsoft Shared\Web Server Extensions\15\WebServices\Reporting<br /><br /> Rsreportserver.config<br /><br /> Rssvrpolicy.config<br /><br /> Web.config para la aplicación ASP.NET del servidor de informes.<br /><br /> Machine.config para ASP.NET.|  
  
####  <a name="bkmk_restore_operations"></a> Operaciones de restauración  
 En esta sección se describen los tipos de información que necesita migrar y las herramientas o los procesos que se usan para completar la restauración. Las herramientas que use para la restauración pueden ser diferentes de las empleadas para la copia de seguridad.  
  
 Antes de completar los pasos de restauración, debe instalar y configurar la nueva granja de SharePoint y el modo de SharePoint de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] . Para obtener más información sobre la instalación básica de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] modo de SharePoint, vea [instalación de modo de SharePoint de Reporting Services &#40;SharePoint 2010 y SharePoint 2013&#41;](../../reporting-services/install-windows/install-reporting-services-sharepoint-mode.md).  
  
||Objetos|Método|Notas|  
|-|-------------|------------|-----------|  
|**1**|Restaurar bases de datos de contenido de SharePoint en la nueva granja.|Método "Actualización de base de datos adjunta“ de SharePoint.|Pasos básicos:<br /><br /> 1) Restaure la base de datos en el nuevo servidor.<br /><br /> 2) Adjunte la base de datos de contenido a una aplicación Web indicando la dirección URL.<br /><br /> 3) Get-SPWebapplication muestra todas las aplicaciones web y las direcciones URL.<br /><br /> Consulte la sección "Actualización de base de datos adjunta" en [Determinación del enfoque de actualización (SharePoint Server 2010) (http://technet.microsoft.com/library/cc263447.aspx)](http://technet.microsoft.com/library/cc263447.aspx) y [Bases de datos adjuntas y actualización a SharePoint Server 2010 (http://technet.microsoft.com/library/cc263299.aspx)](http://technet.microsoft.com/library/cc263299.aspx).|  
|**2**|Restaurar la base de datos SQL es el [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] base de datos de catálogo (servidor de informes).|Copia de seguridad y restauración de bases de datos de SQL.<br /><br /> **o Administrador de configuración de**<br /><br /> Adjuntar y separar bases de datos de SQL Server.|La primera vez que se use la base de datos, [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] actualizará el esquema de la base de datos según sea necesario para que funcione con el entorno de [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] .|  
|**3**|Cree una nueva aplicación de servicio de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] .|Administración central de SharePoint.|Al crear la nueva aplicación de servicio, configúrela para usar la base de datos del servidor de informes que copió.<br /><br /> Para obtener más información sobre el uso de Administración Central de SharePoint, vea la sección "Paso 3: crear una aplicación Reporting Services Service" en [instalar Reporting Services SharePoint Mode for SharePoint 2013](../../../2014/sql-server/install/install-reporting-services-sharepoint-mode-for-sharepoint-2013.md).<br /><br /> Para ver ejemplos sobre el uso de PowerShell, vea la sección "Para crear una aplicación de servicio de Reporting Services mediante PowerShell" en [Reporting Services SharePoint Service and Service Applications](../../../2014/reporting-services/reporting-services-sharepoint-service-and-service-applications.md).|  
|**4**|Restaure los archivos de configuración de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] .|Copia de archivos simple.|Ejemplo de la ubicación predeterminada de los archivos: C:\Archivos de programa\Archivos comunes\Microsoft Shared\Web Server Extensions\15\WebServices\Reporting.|  
|**5**|Restaurar la [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] las claves de cifrado.|Restaure el archivo de copia de seguridad de claves usando la página “Configuración del sistema” de la aplicación de servicio de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] .<br /><br /> **o Administrador de configuración de**<br /><br /> PowerShell.|Vea la sección "Key Management" (Administración de claves) del tema [Manage a Reporting Services SharePoint Service Application](../../../2014/reporting-services/manage-a-reporting-services-sharepoint-service-application.md) (Administrar una aplicación de servicio de SharePoint de Reporting Services).|  
  
#####  <a name="bkmk_additional_configuration"></a> Configuración adicional  
 Dependiendo de cómo se configurara el entorno anterior de SharePoint, puede que necesite completar uno o más de los pasos siguientes:  
  
1.  Configure la autenticación NTLM para una aplicación de servicio de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]. Para obtener más información, consulte [configurar el correo electrónico para una aplicación de servicio de Reporting Services &#40;SharePoint 2010 y SharePoint 2013&#41;](../../reporting-services/install-windows/configure-e-mail-for-a-reporting-services-service-application.md)  
  
##  <a name="bkmk_migrate_from_ctp"></a> Migrar desde una implementación de SQL Server 2012  
 En una granja con varios servidores, los usuarios probablemente tendrán que las bases de datos de contenido y del catálogo en equipos diferentes, en cuyo caso solo se necesita agregar a la granja de SharePoint un nuevo servidor con el servicio [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] instalado y después quitar el servidor antiguo. No debe ser necesario copiar ninguna base de datos.  
  
### <a name="backup-operations"></a>Operaciones de copia de seguridad  
  
1.  Realice una copia de seguridad de las claves de cifrado de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] .  
  
2.  Haga una copia de seguridad de la aplicación de servicio de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] en Administración central de SharePoint (o use PowerShell). Esto también hará una copia de seguridad de las bases de datos de la aplicación de servicio de SharePoint. Vea el tema [copias de seguridad y restaurar Reporting Services SharePoint aplicaciones de servicio](../../../2014/reporting-services/backup-and-restore-reporting-services-sharepoint-service-applications.md)  
  
3.  Si tiene una cuenta de ejecución desatendida (UEA) y autenticación de Windows, anote las credenciales para poder usarlas en el proceso de restauración.  
  
4.  Para obtener más información, vea [Realizar copias de seguridad de aplicaciones de servicio en SharePoint 2013](http://technet.microsoft.com/library/ee428318.aspx).  
  
### <a name="restore-operations"></a>Operaciones de restauración  
  
1.  Restaure la aplicación de servicio de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] mediante Administración central de SharePoint. También podría emplear PowerShell.  
  
2.  Restaure las claves de cifrado de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] .  
  
     Vea la sección "Administración de claves" en el tema [administrar una aplicación de servicio de SharePoint de Reporting Services](../../../2014/reporting-services/manage-a-reporting-services-sharepoint-service-application.md)  
  
3.  Configure la UEA y las credenciales de Windows en la aplicación de servicio.  
  
4.  Para obtener más información, vea [Restaurar las aplicaciones de servicio en SharePoint 2013](http://technet.microsoft.com/library/ee428305.aspx).  
  
##  <a name="bkmk_additional_resources"></a> Recursos adicionales  
  
-   [Introducción a las actualizaciones para SharePoint 2013 (http://technet.microsoft.com/library/ee833948.aspx)](http://technet.microsoft.com/library/ee833948.aspx).  
  
-   [Información general del proceso de actualización a SharePoint 2013 (http://technet.microsoft.com/library/cc262483.aspx)](http://technet.microsoft.com/library/cc262483.aspx).  
  
## <a name="see-also"></a>Vea también  
 [Upgrade and Migrate Reporting Services](../../reporting-services/install-windows/upgrade-and-migrate-reporting-services.md)   
 [Migrar una instalación de Reporting Services &#40;modo nativo&#41;](../../reporting-services/install-windows/migrate-a-reporting-services-installation-native-mode.md)  
  
  