---
title: Base de datos del servidor de informes (modo nativo de SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 08/10/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- databases [Reporting Services]
- report servers [Reporting Services], databases
- temporary databases [Reporting Services]
- report server database
- reportservertempdb
- reportserver database
ms.assetid: 0fc5c033-3fe1-4cea-86c7-66ea5e424d65
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: b1ee55e0ec602ee2723b9e31b5dc80c611071b8e
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/02/2018
ms.locfileid: "48073885"
---
# <a name="report-server-database-ssrs-native-mode"></a>Base de datos del servidor de informes (Modo nativo de SSRS)
  Un servidor de informes es un servidor sin estado que usa el [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssDE](../../includes/ssde-md.md)] para almacenar metadatos y definiciones de objeto. Una instalación en modo nativo de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] emplea dos bases de datos para separar los requisitos de almacenamiento persistente de datos de los de almacenamiento temporal. Las bases de datos se crean juntas y se enlazan mediante el nombre. De forma predeterminada, los nombres de base de datos son **reportserver** y **reportservertempdb**, respectivamente.  
  
 Una instalación en modo SharePoint de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] también creará una base de datos para la característica de alerta de datos. Las tres bases de datos en modo de SharePoint están asociadas a las aplicaciones de servicio de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] . Para obtener más información, vea [Administrar una aplicación de servicio de SharePoint para Reporting Services](../manage-a-reporting-services-sharepoint-service-application.md).  
  
 Las bases de datos se pueden ejecutar en una instancia local o remota del [!INCLUDE[ssDE](../../includes/ssde-md.md)] . La elección de una instancia local es útil si tiene recursos suficientes del sistema o si desea conservar licencias de software, pero la ejecución de las bases de datos en un equipo remoto puede mejorar el rendimiento.  
  
 Puede trasladar o reutilizar una base de datos de servidor de informes existente de una instalación anterior u otra instancia con otra instancia del servidor de informes. El esquema de la base de datos del servidor de informes debe ser compatible con la instancia del servidor de informes. Si la base de datos está en un formato anterior, se le solicitarán que la actualice al formato actual. Las versiones más recientes no se pueden pasar a una versión anterior. Si tiene una base de datos de servidor de informes más reciente, no puede utilizarla con una versión anterior de una instancia del servidor de informes. Para obtener más información sobre cómo se actualizan las bases de datos del servidor de informes a formatos más recientes, consulte [actualizar una base de datos del servidor de informes](../install-windows/upgrade-a-report-server-database.md).  
  
> [!IMPORTANT]  
>  La estructura de tabla para las bases de datos se optimiza para las operaciones de servidor y no se debe modificar ni ajustar. [!INCLUDE[msCoName](../../includes/msconame-md.md)] podría cambiar la estructura de tabla en una versión posterior. Si modifica o amplía la base de datos, es posible que esté limitando o anulando la capacidad de ejecutar futuras actualizaciones o aplicar Service Pack. También podría realizar cambios que dificultaran las operaciones del servidor de informes. Por ejemplo, si activa READ_COMMITTED_SNAPSHOT en la base de datos ReportServer, interrumpirá la característica de ordenación interactiva.  
  
 Todos los accesos a una base de datos del servidor de informes deben controlarse a través del servidor de informes. Para acceder al contenido de una base de datos del servidor de informes se pueden usar herramientas de administración del servidor de informes (como el Administrador de informes y [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]) o interfaces de programación como el acceso URL, el servicio web del servidor de informes o el proveedor de Instrumental de administración de Windows (WMI).  
  
 La conexión a la base de datos del servidor de informes se define generalmente a través del Administrador de configuración de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] . No obstante, se puede definir durante la instalación si decide instalar la configuración predeterminada. Para más información sobre la conexión del servidor de informes a la base de datos, vea [Configurar una conexión a la base de datos del servidor de informes &#40;Administrador de configuración de SSRS&#41;](../../sql-server/install/configure-a-report-server-database-connection-ssrs-configuration-manager.md).  
  
## <a name="report-server-database"></a>base de datos del servidor de informes  
 La base de datos del servidor de informes es una base de datos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] donde se almacena el siguiente contenido:  
  
-   Los elementos administrados por un servidor de informes (.. / informan de informes e informes vinculados, orígenes de datos compartidos, modelos, carpetas, recursos) y todas las propiedades y configuración de seguridad que está asociadas con esos elementos.  
  
-   Definiciones de suscripciones y programaciones.  
  
-   Instantáneas de informes (que incluyen resultados de consultas) e historial de informes.  
  
-   Propiedades del sistema y configuración de seguridad en el nivel del sistema.  
  
-   Datos de registro de ejecución de informes.  
  
-   Claves simétricas y credenciales y conexión cifrada para orígenes de datos de informe.  
  
 Debido a que la base de datos del servidor de informes almacena el estado de la aplicación y los datos persistentes, debería crear una programación de copia de seguridad para esta base de datos y así evitaría la pérdida de datos. Para obtener recomendaciones e instrucciones sobre cómo hacer una copia de seguridad de la base de datos, vea [Mover las bases de datos del servidor de informes a otro equipo &#40;Modo nativo de SSRS&#41;](moving-the-report-server-databases-to-another-computer-ssrs-native-mode.md).  
  
## <a name="report-server-temporary-database"></a>Base de datos temporal del servidor de informes  
 Cada base de datos del servidor de informes utiliza una base de datos temporal relacionada para almacenar datos de sesiones y de ejecución, informes almacenados en caché y tablas de trabajo que genera el servidor de informes. Los procesos de servidor en segundo plano quitarán periódicamente los elementos que no se usen y los más antiguos de las tablas de la base de datos temporal.  
  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] no vuelve a crear la base de datos temporal si no está presente, ni repara las tablas que falten o se hayan modificado. Aunque la base de datos temporal no contiene datos persistentes, conviene crear una copia de seguridad para evitar tener que crearla de nuevo como parte de una operación de recuperación en caso de error.  
  
 Si realiza una copia de seguridad de la base de datos temporal y posteriormente la restaura, debería eliminar el contenido. Generalmente, se puede eliminar el contenido de la base de datos temporal en cualquier momento. No obstante, deberá reiniciar el servicio Servidor de informes de Windows una vez realizada esa operación.  
  
## <a name="see-also"></a>Vea también  
 [Hospedar una base de datos del servidor de informes en un clúster de conmutación por error SQL Server](../install-windows/host-a-report-server-database-in-a-sql-server-failover-cluster.md)   
 [Almacenar datos cifrados del servidor de informes &#40;Administrador de configuración de SSRS&#41;](../install-windows/ssrs-encryption-keys-store-encrypted-report-server-data.md)   
 [Servidor de informes de Reporting Services](../reporting-services-report-server.md)   
 [Administrar una base de datos del servidor de informes &#40;Modo nativo de SSRS&#41;](report-server-database-ssrs-native-mode.md)   
 [Crear una base de datos del servidor de informes &#40;Administrador de configuración de SSRS&#41;](../../sql-server/install/create-a-report-server-database-ssrs-configuration-manager.md)   
 [Operaciones de copia de seguridad y restauración de Reporting Services](../install-windows/backup-and-restore-operations-for-reporting-services.md)  
  
  
