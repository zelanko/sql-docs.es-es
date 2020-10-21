---
title: Base de datos del servidor de informes (modo nativo) | Microsoft Docs
description: Obtenga información sobre cómo una instalación en modo nativo de Reporting Services separa el almacenamiento de datos persistentes y el almacenamiento de datos temporal en dos bases de datos.
ms.date: 06/06/2019
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: report-server
ms.topic: conceptual
helpviewer_keywords:
- databases [Reporting Services]
- report servers [Reporting Services], databases
- temporary databases [Reporting Services]
- report server database
- reportservertempdb
- reportserver database
ms.assetid: 0fc5c033-3fe1-4cea-86c7-66ea5e424d65
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 9b5f4230aacedcff2ecdffedb943ae39097fc1d4
ms.sourcegitcommit: fe59f8dc27fd633f5dfce54519d6f5dcea577f56
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 10/09/2020
ms.locfileid: "91934991"
---
# <a name="report-server-database-ssrs-native-mode"></a>Base de datos del servidor de informes (Modo nativo de SSRS)
  Un servidor de informes es un servidor sin estado que usa el [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssDE](../../includes/ssde-md.md)] para almacenar metadatos y definiciones de objeto. Una instalación en modo nativo de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] emplea dos bases de datos para separar los requisitos de almacenamiento persistente de datos de los de almacenamiento temporal. Las bases de datos se crean juntas y se enlazan mediante el nombre. De forma predeterminada, los nombres de base de datos son **ReportServer** y **ReportServerTempDB**, respectivamente.  
  
 Una instalación en modo SharePoint de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] también creará una base de datos para la característica de alerta de datos. Las tres bases de datos en modo de SharePoint están asociadas a las aplicaciones de servicio de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] . Para obtener más información, vea [Administrar una aplicación de servicio de SharePoint para Reporting Services](../../reporting-services/report-server-sharepoint/manage-a-reporting-services-sharepoint-service-application.md).  
  
 Las bases de datos se pueden ejecutar en una instancia local o remota del [!INCLUDE[ssDE](../../includes/ssde-md.md)] . La elección de una instancia local es útil si tiene recursos suficientes del sistema o si desea conservar licencias de software, pero la ejecución de las bases de datos en un equipo remoto puede mejorar el rendimiento.  
  
 Puede trasladar o reutilizar una base de datos de servidor de informes existente de una instalación anterior u otra instancia con otra instancia del servidor de informes. El esquema de la base de datos del servidor de informes debe ser compatible con la instancia del servidor de informes. Si la base de datos está en un formato anterior, se le solicitarán que la actualice al formato actual. Las versiones más recientes no se pueden pasar a una versión anterior. Si tiene una base de datos de servidor de informes más reciente, no puede usarla con una versión anterior de una instancia del servidor de informes. Para más información sobre cómo se actualizan las bases de datos del servidor de informes a formatos más recientes, vea [Actualizar una base de datos del servidor de informes](../../reporting-services/install-windows/upgrade-a-report-server-database.md).  
  
> [!IMPORTANT]  
> La estructura de tabla para las bases de datos se optimiza para las operaciones de servidor y no se debe modificar ni ajustar. [!INCLUDE[msCoName](../../includes/msconame-md.md)] podría cambiar la estructura de tabla en una versión posterior. Si modifica o amplía la base de datos, es posible que esté limitando o anulando la capacidad de ejecutar futuras actualizaciones o aplicar Service Pack. También podría realizar cambios que dificultaran las operaciones del servidor de informes. Por ejemplo, si activa READ_COMMITTED_SNAPSHOT en la base de datos ReportServer, interrumpirá la característica de ordenación interactiva.  
  
 Todos los accesos a una base de datos del servidor de informes deben controlarse a través del servidor de informes. Para acceder al contenido de una base de datos del servidor de informes se pueden usar herramientas de administración del servidor de informes (como el portal web y [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]) o interfaces de programación, como el acceso URL, el servicio web del servidor de informes o el proveedor de Instrumental de administración de Windows (WMI).  
  
 La conexión a la base de datos del servidor de informes se define generalmente a través del Administrador de configuración de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] . No obstante, se puede definir durante la instalación si decide instalar la configuración predeterminada. Para más información sobre la conexión del servidor de informes a la base de datos, vea [Configurar una conexión a la base de datos del servidor de informes &#40;Administrador de configuración del servidor de informes&#41;](../../reporting-services/install-windows/configure-a-report-server-database-connection-ssrs-configuration-manager.md).  
  
## <a name="report-server-database"></a>Base de datos del servidor de informes  
 La base de datos del servidor de informes es una base de datos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] donde se almacena el siguiente contenido:  
  
-   Elementos administrados por un servidor de informes (informes e informes vinculados, orígenes de datos compartidos, modelos de informe, carpetas, recursos) y todas las propiedades y la configuración de seguridad asociadas a dichos elementos.  
  
-   Definiciones de suscripciones y programaciones.  
  
-   Instantáneas de informes (que incluyen resultados de consultas) e historial de informes.  
  
-   Propiedades del sistema y configuración de seguridad en el nivel del sistema.  
  
-   Datos de registro de ejecución de informes.  
  
-   Claves simétricas y credenciales y conexión cifrada para orígenes de datos de informe.  
  
 Debido a que la base de datos del servidor de informes almacena el estado de la aplicación y los datos persistentes, debería crear una programación de copia de seguridad para esta base de datos y así evitaría la pérdida de datos. Para obtener recomendaciones e instrucciones sobre cómo hacer una copia de seguridad de la base de datos, vea [Mover las bases de datos del servidor de informes a otro equipo &#40;Modo nativo de SSRS&#41;](../../reporting-services/report-server/moving-the-report-server-databases-to-another-computer-ssrs-native-mode.md).  
  
## <a name="report-server-temporary-database"></a>Base de datos temporal del servidor de informes  
 Cada base de datos del servidor de informes utiliza una base de datos temporal relacionada para almacenar datos de sesiones y de ejecución, informes almacenados en caché y tablas de trabajo que genera el servidor de informes. Los procesos de servidor en segundo plano quitarán periódicamente los elementos que no se usen y los más antiguos de las tablas de la base de datos temporal.  
  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] no vuelve a crear la base de datos temporal si no está presente, ni repara las tablas que falten o se hayan modificado. Aunque la base de datos temporal no contiene datos persistentes, conviene crear una copia de seguridad para evitar tener que crearla de nuevo como parte de una operación de recuperación en caso de error.  
  
 Si realiza una copia de seguridad de la base de datos temporal y posteriormente la restaura, debería eliminar el contenido. Generalmente, se puede eliminar el contenido de la base de datos temporal en cualquier momento. No obstante, deberá reiniciar el servicio Servidor de informes de Windows una vez realizada esa operación.  
  
## <a name="see-also"></a>Consulte también  
 [Hospedar una base de datos del servidor de informes en un clúster de conmutación por error de SQL Server](../../reporting-services/install-windows/host-a-report-server-database-in-a-sql-server-failover-cluster.md)   
 [Almacenar datos cifrados del servidor de informes &#40;Administrador de configuración del servidor de informes&#41;](../../reporting-services/install-windows/ssrs-encryption-keys-store-encrypted-report-server-data.md)   
 [Servidor de informes de Reporting Services](../../reporting-services/report-server-sharepoint/reporting-services-report-server.md)   
 [Administrar una base de datos del servidor de informes &#40;Modo nativo de SSRS&#41;](../../reporting-services/report-server/administer-a-report-server-database-ssrs-native-mode.md)   
 [Crear una base de datos del servidor de informes &#40;Administrador de configuración del servidor de informes&#41;](../../reporting-services/install-windows/ssrs-report-server-create-a-report-server-database.md)   
 [Operaciones de copia de seguridad y restauración de Reporting Services](../../reporting-services/install-windows/backup-and-restore-operations-for-reporting-services.md)  
  