---
title: Tareas de instalación de Master Data Services | Microsoft Docs
ms.custom: ''
ms.date: 03/24/2017
ms.prod: sql-non-specified
ms.prod_service: mds
ms.service: ''
ms.component: install-windows
ms.reviewer: ''
ms.suite: sql
ms.technology:
- setup-install
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: bb7aa3e7-8807-42c8-884f-0e41d7a20837
caps.latest.revision: 32
author: leolimsft
ms.author: lle
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 30435254dd2f8124098a484dd7c28d2755b11d4b
ms.sourcegitcommit: bb044a48a6af9b9d8edb178dc8c8bd5658b9ff68
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/18/2018
---
# <a name="installation-tasks-for-master-data-services"></a>Tareas de instalación de Master Data Services

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

  En este artículo se proporciona información general de las tareas de instalación, con vínculos a las instrucciones. Para ver un tutorial de instalación y configuración de Master Data Services, vea [Instalación y configuración de Master Data Services](../../master-data-services/master-data-services-installation-and-configuration.md). 
  
-   [Tareas de preinstalación:](#preinstall)compruebe los requisitos del sistema antes de instalar [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)].  
  
-   [Operaciones de instalación](#install): instale [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] utilizando en programa de instalación de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o el símbolo del sistema.  
  
-   [Tareas posteriores a la instalación:](#postinstall)abra [!INCLUDE[ssMDScfgmgr](../../includes/ssmdscfgmgr-md.md)] para completar las operaciones posteriores a la instalación. Cree y configure la base de datos de [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] , la aplicación web de [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] y los servicios web, e implemente un modelo de ejemplo.  
  
##  <a name="preinstall"></a> Tareas de preinstalación:  
  
|Acción|Detalles|Temas relacionados|  
|------------|-------------|--------------------|  
|Comprobar los requisitos de instalación|El equipo donde se ejecuta el programa de instalación de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] debe cumplir los requisitos mínimos para:<br /><br /> [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .<br /><br /> Los servicios web y la aplicación web de [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] .<br /><br /> La base de datos de [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] , si hospeda la base de datos en el mismo equipo que la aplicación web.<br /><br /> <br /><br /> Puede separar el equipo servidor web y el equipo servidor de bases de datos ejecutando el programa de instalación solo en el equipo servidor web y creando la base de datos de [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] en un equipo remoto que ejecute una versión y edición compatibles de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|[Características compatibles con las ediciones de SQL Server 2016](~/sql-server/editions-and-supported-features-for-sql-server-2016.md)<br /><br /> [Requisitos de hardware y software para instalar SQL Server 2016](../../sql-server/install/hardware-and-software-requirements-for-installing-sql-server.md)<br /><br /> [Requisitos de la aplicación web &#40;Master Data Services&#41;](../../master-data-services/install-windows/web-application-requirements-master-data-services.md)<br /><br /> [Requisitos de base de datos &#40;Master Data Services&#41;](../../master-data-services/install-windows/database-requirements-master-data-services.md)|  
|Configurar los roles necesarios, servicios del rol y características|Antes de ejecutar el programa de instalación, configure el equipo con los roles de Windows, los servicios de rol y las características necesarios.<br /><br /> Nota: Aunque puede seguir este paso posteriormente en el flujo de trabajo, es útil configurar esto antes de ejecutar el programa de instalación para poder realizar tareas de configuración de web inmediatamente después de la instalación.|[Requisitos de la aplicación web &#40;Master Data Services&#41;](../../master-data-services/install-windows/web-application-requirements-master-data-services.md)|  
|Revisar las consideraciones de la compatibilidad con idiomas|Determine el idioma con el que desea instalar y ejecutar [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] .|[Implementaciones plurilingües y globales &#40;Master Data Services&#41;](../../master-data-services/install-windows/multi-lingual-and-global-deployments-master-data-services.md)|  
  
##  <a name="install"></a> Operaciones de instalación  
  
|Acción|Detalles|Temas relacionados|  
|------------|-------------|--------------------|  
|Ejecutar el programa de instalación de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|En el equipo que hospedará la aplicación web de [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] y los servicios web de [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] , utilice el programa de instalación de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o un símbolo del sistema para instalar [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)]. Cuando se usa el programa de instalación de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] está disponible en la página **Selección de características** en **Características compartidas**. Si se usa un símbolo del sistema, [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] está disponible como parámetro de característica. Tenga en cuenta que el proceso de instalación desde la línea de comandos instala [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)], pero no lo configura. Debe configurarlo mediante el Administrador de configuración de Master Data Services.<br /><br /> Proceso de instalación:<br /><br /> Instala las carpetas y los archivos de [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] en la ubicación que especifique para las características compartidas y asigna permisos a estos objetos.<br /><br /> Registra los ensamblados de [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] en la memoria caché global de ensamblados (GAC).<br /><br /> Instala [!INCLUDE[ssMDScfgmgr](../../includes/ssmdscfgmgr-md.md)].|[Instalación de SQL Server 2016 desde el Asistente para la instalación &#40;programa de instalación&#41;](../../database-engine/install-windows/install-sql-server-from-the-installation-wizard-setup.md)<br /><br /> [Permisos de carpetas y archivos &#40;Master Data Services&#41;](../../master-data-services/folder-and-file-permissions-master-data-services.md)|  
  
##  <a name="postinstall"></a> Tareas posteriores a la instalación:  
  
|Acción|Detalles|Temas relacionados|  
|------------|-------------|--------------------|  
|Abrir [!INCLUDE[ssMDScfgmgr](../../includes/ssmdscfgmgr-md.md)] para completar las operaciones posteriores a la instalación|Una vez completada la instalación, abra [!INCLUDE[ssMDScfgmgr](../../includes/ssmdscfgmgr-md.md)]. [!INCLUDE[ssMDScfgmgr](../../includes/ssmdscfgmgr-md.md)] realiza las siguientes operaciones posteriores a la instalación en el equipo local:<br /><br /> Crea un grupo de Windows, **MDS_ServiceAccounts**, para contener las cuentas de servicio de [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] para los grupos de aplicaciones.<br /><br /> En la ruta de instalación de [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] , crea la carpeta MDSTempDir y asigna permisos para **MDS_ServiceAccounts**. Esta carpeta es donde los archivos de compilación temporales se compilan para la aplicación web de [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] .<br /><br /> En el archivo Web.config de [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)], configura el atributo **tempDirectory** del elemento **\<compilation>** con la ruta de acceso a la carpeta MDSTempDir.|[Permisos de carpetas y archivos &#40;Master Data Services&#41;](../../master-data-services/folder-and-file-permissions-master-data-services.md)<br /><br /> [Referencia de la configuración web &#40;Master Data Services&#41;](../../master-data-services/web-configuration-reference-master-data-services.md)|  
|Crear una base de datos de [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)]|Use [!INCLUDE[ssMDScfgmgr](../../includes/ssmdscfgmgr-md.md)] para crear una base de datos de [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] para los datos maestros.|[Crea una base de datos de Master Data Services](../../master-data-services/install-windows/create-a-master-data-services-database.md)|  
|Crear una aplicación web [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)]|Use [!INCLUDE[ssMDScfgmgr](../../includes/ssmdscfgmgr-md.md)] para crear y configurar una aplicación web para hospedar [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)].|[Crear una aplicación web de Master Data Manager &#40;Master Data Services&#41;](../../master-data-services/install-windows/create-a-master-data-manager-web-application-master-data-services.md)|  
|Asociar una base de datos de [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] a una aplicación web|Use [!INCLUDE[ssMDScfgmgr](../../includes/ssmdscfgmgr-md.md)] para asociar la aplicación web [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] a su base de datos de [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] .|[Asociar una base de datos y una aplicación web de Master Data Services](../../master-data-services/install-windows/associate-a-master-data-services-database-and-web-application.md)|  
|Configurar la seguridad mejorada de Internet Explorer|Al instalar [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] en un equipo de Windows Server 2012, podría tener que configurar la seguridad mejorada de Internet Explorer para permitir el scripting para el sitio de la aplicación [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] . De lo contrario, la exploración al sitio de la aplicación de [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] en el equipo servidor producirá errores.|[Internet Explorer: configuración de seguridad mejorada](http://go.microsoft.com/fwlink/p/?LinkId=223869)|  
|Instalar [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)][!INCLUDE[ssMDSXLS](../../includes/ssmdsxls-md.md)]|Los usuarios que vayan a trabajar con datos maestros pueden instalar [!INCLUDE[ssMDSXLS](../../includes/ssmdsxls-md.md)].|[http://go.microsoft.com/fwlink/?LinkID=398159](http://go.microsoft.com/fwlink/?LinkID=398159)|  
|Habilitar la integración con Data Quality Services (DQS)|Para los usuarios de [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)][!INCLUDE[ssMDSXLS](../../includes/ssmdsxls-md.md)], habilite la integración con la característica de DQS, que se puede usar para hacer corresponder datos similares.|[Habilitar la integración de Data Quality Services con Master Data Services](../../master-data-services/install-windows/enable-data-quality-services-integration-with-master-data-services.md)|  
|Implementar un modelo de ejemplo|Los paquetes del modelo de ejemplo se instalan con Master Data Services y pueden implementarse mediante MDSModelDeploy.exe.|[Implementar ejemplos de MDS en SQL Server](~/master-data-services/sql-server-samples-model-deployment-packages-mds.md)|
  
 Si encuentra problemas durante el proceso de instalación o la configuración inicial, vea [Solucionar problemas de instalación y configuración](http://social.technet.microsoft.com/wiki/contents/articles/troubleshooting-installation-and-configuration-issues-master-data-services.aspx) en TechNet Wiki.  
  
 Si ya no necesita [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] en un equipo, puede desinstalar [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] y determinar si se han de quitar los elementos que no estén afectados por el proceso de desinstalación. Para obtener más información, vea [Desinstalar y quitar Master Data Services](../../sql-server/install/uninstall-and-remove-master-data-services.md).  
  
## <a name="see-also"></a>Ver también  
 [Instalar SQL Server 2016](../../database-engine/install-windows/install-sql-server.md)  
  
  
