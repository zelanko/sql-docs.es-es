---
title: Instalar Master Data Services | Microsoft Docs
ms.custom: ''
ms.date: 05/24/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: install
ms.topic: conceptual
ms.assetid: bb7aa3e7-8807-42c8-884f-0e41d7a20837
author: lrtoyou1223
ms.author: lle
ms.openlocfilehash: 3fe5382fae26d01478b33c7b54c3d6f5170d34eb
ms.sourcegitcommit: f71e523da72019de81a8bd5a0394a62f7f76ea20
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/17/2020
ms.locfileid: "84971339"
---
# <a name="install-master-data-services"></a>Instalar Master Data Services
  El siguiente flujo de trabajo proporciona información general acerca de cómo instalar y configurar [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)]. [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] La instalación es un proceso que consta de tres partes:  
  
-   [Tareas de preinstalación:](#preinstall)compruebe los requisitos del sistema antes de instalar [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)].  
  
-   [Operaciones de instalación](#install): instale [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] utilizando en programa de instalación de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o el símbolo del sistema.  
  
-   [Tareas posteriores a la instalación:](#postinstall)abra [!INCLUDE[ssMDScfgmgr](../../includes/ssmdscfgmgr-md.md)] para completar las operaciones posteriores a la instalación. Cree y configure la base de datos de [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] , la aplicación web de [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] y los servicios web, e implemente un modelo de ejemplo.  
  
##  <a name="pre-installation-tasks"></a><a name="preinstall"></a>Tareas previas a la instalación  
  
|Acción|Detalles|Temas relacionados|  
|------------|-------------|--------------------|  
|Comprobar los requisitos de instalación|El equipo donde se ejecuta el programa de instalación de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] debe cumplir los requisitos mínimos para:<br /><br /> [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .<br /><br /> Los servicios web y la aplicación web de [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] .<br /><br /> La base de datos de [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] , si hospeda la base de datos en el mismo equipo que la aplicación web.<br /><br /> Tenga en cuenta que puede separar el equipo servidor Web y el equipo servidor de base de datos ejecutando el programa de instalación solo en el equipo servidor Web y creando la [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] base de datos en un equipo remoto que ejecute una versión y edición compatibles de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .|[Características admitidas por las ediciones de SQL Server 2014](../../getting-started/features-supported-by-the-editions-of-sql-server-2014.md)<br /><br /> [Requisitos de hardware y software para instalar SQL Server 2014](../../sql-server/install/hardware-and-software-requirements-for-installing-sql-server.md)<br /><br /> [Requisitos de la aplicación web &#40;Master Data Services&#41;](web-application-requirements-master-data-services.md)<br /><br /> [Requisitos de base de datos &#40;Master Data Services&#41;](database-requirements-master-data-services.md)|  
|Configurar los roles necesarios, servicios del rol y características|Antes de ejecutar el programa de instalación, configure el equipo con los roles de Windows, los servicios de rol y las características necesarios.<br /><br /> Nota: Aunque puede seguir este paso posteriormente en el flujo de trabajo, es útil configurar esto antes de ejecutar el programa de instalación para poder realizar tareas de configuración de web inmediatamente después de la instalación.|[Requisitos de la aplicación web &#40;Master Data Services&#41;](web-application-requirements-master-data-services.md)|  
|Revisar las consideraciones de la compatibilidad con idiomas|Determine el idioma con el que desea instalar y ejecutar [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] .|[Implementaciones plurilingües y globales &#40;Master Data Services&#41;](multi-lingual-and-global-deployments-master-data-services.md)|  
  
##  <a name="installation-operations"></a><a name="install"></a> Operaciones de instalación  
  
|Acción|Detalles|Temas relacionados|  
|------------|-------------|--------------------|  
|Ejecutar el programa de instalación de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|En el equipo que hospedará la aplicación web de [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] y los servicios web de [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] , utilice el programa de instalación de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o un símbolo del sistema para instalar [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)]. Cuando se usa el programa de instalación de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] está disponible en la página **Selección de características** en **Características compartidas**. Si se usa un símbolo del sistema, [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] está disponible como parámetro de característica. Tenga en cuenta que el proceso de instalación desde la línea de comandos instala [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)], pero no lo configura. Debe configurarlo mediante el Administrador de configuración de Master Data Services. Proceso de instalación:<br /><br /> Instala las carpetas y los archivos de [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] en la ubicación que especifique para las características compartidas y asigna permisos a estos objetos.<br /><br /> Registra los ensamblados de [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] en la memoria caché global de ensamblados (GAC).<br /><br /> Instala [!INCLUDE[ssMDScfgmgr](../../includes/ssmdscfgmgr-md.md)].|[Instale SQL Server 2014 desde el Asistente para la instalación &#40;el programa de instalación&#41;](../../database-engine/install-windows/install-sql-server-from-the-installation-wizard-setup.md)<br /><br /> [Permisos de carpetas y archivos &#40;Master Data Services&#41;](../folder-and-file-permissions-master-data-services.md)|  
  
##  <a name="post-installation-tasks"></a><a name="postinstall"></a>Tareas posteriores a la instalación  
  
|Acción|Detalles|Temas relacionados|  
|------------|-------------|--------------------|  
|Abrir [!INCLUDE[ssMDScfgmgr](../../includes/ssmdscfgmgr-md.md)] para completar las operaciones posteriores a la instalación|Una vez completada la instalación, abra [!INCLUDE[ssMDScfgmgr](../../includes/ssmdscfgmgr-md.md)]. [!INCLUDE[ssMDScfgmgr](../../includes/ssmdscfgmgr-md.md)] realiza las siguientes operaciones posteriores a la instalación en el equipo local:<br /><br /> Crea un grupo de Windows, **MDS_ServiceAccounts**, para contener las cuentas de servicio de [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] para los grupos de aplicaciones.<br /><br /> En la ruta de instalación de [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] , crea la carpeta MDSTempDir y asigna permisos para **MDS_ServiceAccounts**. Esta carpeta es donde los archivos de compilación temporales se compilan para la aplicación web de [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] .<br /><br /> En el [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] archivo de Web.config, configura el `tempDirectory` atributo del **\<compilation>** elemento con la ruta de acceso a la carpeta MDSTempDir.<br /><br /> <br /><br /> Si incluye en un script el proceso de instalación, puede abrir [!INCLUDE[ssMDScfgmgr](../../includes/ssmdscfgmgr-md.md)] para registrar el complemento [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)], pero debe realizar manualmente los demás pasos para completar la configuración. [!INCLUDE[ssMDScfgmgr](../../includes/ssmdscfgmgr-md.md)] proporciona un proceso de configuración controlado por un asistente. No hay ningún proceso desde la línea de comandos para configurar [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)].|[Permisos de carpetas y archivos &#40;Master Data Services&#41;](../folder-and-file-permissions-master-data-services.md)<br /><br /> [Referencia de la configuración web &#40;Master Data Services&#41;](../web-configuration-reference-master-data-services.md)|  
|Crear una base de datos de [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)]|Use [!INCLUDE[ssMDScfgmgr](../../includes/ssmdscfgmgr-md.md)] para crear una base de datos de [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] para los datos maestros.|[Crea una base de datos de Master Data Services](create-a-master-data-services-database.md)|  
|Crear una aplicación web [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)]|Use [!INCLUDE[ssMDScfgmgr](../../includes/ssmdscfgmgr-md.md)] para crear y configurar una aplicación web para hospedar [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)].|[Crear una aplicación web de Master Data Manager &#40;Master Data Services&#41;](create-a-master-data-manager-web-application-master-data-services.md)|  
|Asociar una base de datos de [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] a una aplicación web|Use [!INCLUDE[ssMDScfgmgr](../../includes/ssmdscfgmgr-md.md)] para asociar la aplicación web [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] a su base de datos de [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] .|[Asociar una base de datos y una aplicación web de Master Data Services](associate-a-master-data-services-database-and-web-application.md)|  
|Configurar la seguridad mejorada de Internet Explorer|Al instalar [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] en un equipo de Windows Server 2008 o Windows Server 2008 R2, podría tener que configurar la seguridad mejorada de Internet Explorer para permitir el scripting para el sitio de la aplicación [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] . De lo contrario, la exploración al sitio de la aplicación de [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] en el equipo servidor producirá errores.|[Internet Explorer: configuración de seguridad mejorada](https://go.microsoft.com/fwlink/p/?LinkId=223869)|  
|Instalar [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)][!INCLUDE[ssMDSXLS](../../includes/ssmdsxls-md.md)]|Los usuarios que vayan a trabajar con datos maestros pueden instalar [!INCLUDE[ssMDSXLS](../../includes/ssmdsxls-md.md)].|[https://go.microsoft.com/fwlink/?LinkId=219530](https://go.microsoft.com/fwlink/?LinkId=219530)|  
|Habilitar la integración con Data Quality Services (DQS)|Para los usuarios de [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)][!INCLUDE[ssMDSXLS](../../includes/ssmdsxls-md.md)], habilite la integración con la característica de DQS, que se puede usar para hacer corresponder datos similares.|[Habilitar la integración de Data Quality Services con Master Data Services](enable-data-quality-services-integration-with-master-data-services.md)|  
|Implementar un modelo de ejemplo|Los paquetes del modelo de ejemplo se instalan con Master Data Services y pueden implementarse mediante MDSModelDeploy.exe.|[Implementar ejemplos de MDS en SQL Server](https://go.microsoft.com/fwlink/?LinkId=251486&clcid=0x409)|  
  
 Si encuentra problemas durante el proceso de instalación o la configuración inicial, vea [Solucionar problemas de instalación y configuración](https://social.technet.microsoft.com/wiki/contents/articles/troubleshooting-installation-and-configuration-issues-master-data-services.aspx) en TechNet Wiki.  
  
 Si ya no necesita [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] en un equipo, puede desinstalar [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] y determinar si se han de quitar los elementos que no estén afectados por el proceso de desinstalación. Para obtener más información, vea [Desinstalar y quitar Master Data Services](../../sql-server/install/uninstall-and-remove-master-data-services.md).  
  
## <a name="see-also"></a>Consulte también  
 [Instalar SQL Server 2014](../../database-engine/install-windows/install-sql-server.md)  
  
  
