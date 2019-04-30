---
title: Dispositivo, instalar y configurar - Analytics Platform System | Microsoft Docs
description: Le guía a los administradores del equipo a través de los pasos iniciales para configurar y empezar a usar la nueva aplicación Analytics Platform System (APS).
author: mzaman1
manager: craigg
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.openlocfilehash: 5b6aa75cdab85fce9ef308d3e853ddb0107c28ee
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "63276351"
---
# <a name="appliance-installation-and-configuration-for-analytics-platform-system"></a>Instalación de dispositivo y la configuración de Analytics Platform System
Le guía a los administradores del equipo a través de los pasos iniciales para configurar y empezar a usar la nueva aplicación Analytics Platform System (APS).  
  
<!-- MISSING LINKS ## <a name="BeforeYouBegin"></a>Before You Begin  
Before you begin to install, configure, and use your new appliance, we recommend reviewing information about the appliance components. Review the following to familiarize yourself with the appliance:  
  
-   Review [Understanding the Appliance Nodes and Hardware (SQL Server PDW)](assetId:///f60f419f-d1e1-403d-8cf9-07e7ef6d6627) to be sure you understand the components included in your new appliance.  
  
-   Review [Connecting to SQL Server PDW (SQL Server PDW)](assetId:///721851d5-e521-4d5b-ba6d-8e2e9d3c7808) to understand how and when appliance administrators will connect to each appliance node.  
-->

## <a name="InstallHardware"></a>1. Instale el Hardware  
El nuevo dispositivo se entregará en paletas a la base en su centro de datos.  
  
> [!IMPORTANT]  
> En algunos casos, los IHV desempaquetar, bastidor y conectar el dispositivo para usted en su centro de datos. Si es así, estas instrucciones no son necesarias y puede ir a la [3. Configurar el dispositivo](#ConfigureAppliance) sección más adelante.  
  
Si el IHV no está realizando la instalación de hardware, siga estos pasos para instalar el hardware.  
  
|||  
|-|-|  
|**Tarea**|**Descripción**|  
|Confirme la documentación|Confirme que ha recibido todos los documentos necesarios e información de su proveedor de hardware independientes (IHV). Consulte [información para obtener de IHV &#40;Analytics Platform System&#41;](information-to-obtain-from-your-ihv.md).|  
|Instale el hardware|Compruebe que el centro de datos puede dar cabida a la aplicación. Mover los componentes del dispositivo al centro de datos. Los conmutadores de red, PDU, en bastidor y cableado. Consulte [Hardware instalación &#40;Analytics Platform System&#41;](hardware-installation.md).|  
  
## <a name="PowerOnAppliance"></a>2. Encienda el dispositivo  
  
|||  
|-|-|  
|**Tarea**|**Descripción**|  
|Encienda el dispositivo|Encienda cada nodo del componente de dispositivo en el orden adecuado, según sea necesario para confirmar que no se encuentran errores en espera.|  
  
## <a name="ConfigureAppliance"></a>3. Configurar el dispositivo  
  
|||  
|-|-|  
|**Tarea**|**Descripción**|  
|||  
|Configurar el dispositivo mediante el uso de SQL Server PDW**Configuration Manager**|Use el Administrador de configuración para establecer las contraseñas de aplicación, zonas horarias, configuración de red y del firewall, certificados de seguridad y rendimiento y otras opciones en el dispositivo. Consulte [la configuración del equipo &#40;Analytics Platform System&#41;](appliance-configuration.md).|  
  
> [!WARNING]  
> Solo se deben realizar los cambios de configuración con SQL Server PDW**Configuration Manager**. Los cambios no se exponen a través de **Configuration Manager** no se admiten. Por ejemplo, el dispositivo PDW de SQL Server solo admite la configuración de idioma inglés de Estados Unidos.  
  
## <a name="SoftwareServicing"></a>4. Configuración de mantenimiento de Software  
  
|||  
|-|-|  
|**Tarea**|**Descripción**|  
|Aplicar actualizaciones de SQL Server PDW|(Opcional) Es posible que deba aplicar una o varias actualizaciones de PDW de SQL Server para actualizar el software de PDW de SQL Server a la versión más reciente. Consulte [aplicar las revisiones de Analytics Platform System &#40;Analytics Platform System&#41;](apply-analytics-platform-system-hotfixes.md).|  
|Configuración de Windows Server Update Services|Configurar el dispositivo para recibir actualizaciones de Windows Server Update Services para admitir el software. Consulte [descargue y aplique las actualizaciones de Microsoft &#40;Analytics Platform System&#41;](download-and-apply-microsoft-updates.md).|  
  
## <a name="NextSteps"></a>Pasos siguientes  
Después de haber completado todos los pasos anteriores, el dispositivo está listo para su uso. Usted o a otros miembros del personal en su ubicación pueden continuar con las siguientes tareas.  
  
|||  
|-|-|  
|**Tarea**|**Descripción**|  
|Instalar a controladores de PDW de SQL Server y configurar la conectividad|Configurar los equipos locales para conectarse a SQL Server PDW mediante el uso de SQL Server Data Tools, sqlcmd, software de inteligencia de negocio u otras herramientas. <!-- MISSING LINKS See [Client Tools (SQL Server PDW)](assetId:///721851d5-e521-4d5b-ba6d-8e2e9d3c7808).-->|  
|Crear roles de servidor e inicios de sesión y asignar permisos|Planear y crear roles de servidor e inicios de sesión que permiten a los usuarios iniciar sesión en PDW de SQL Server con los permisos adecuados. <!-- MISSING LINKS See [PDW Permissions &#40;SQL Server PDW&#41;](../sqlpdw/pdw-permissions-sql-server-pdw.md).-->|  
|Configurar la puerta de enlace de administración de datos de Azure|La puerta de enlace permite a los usuarios de Azure tener acceso a datos de puntos de acceso local mediante la exposición de datos de puntos de acceso como segura fuentes de OData. La puerta de enlace ya está instalado en el nodo de Control. Pedir a Microsoft para obtener ayuda con la configuración.|  
|Monitor realiza consultas y los usuarios del dispositivo|Use la consola de administración y otros recursos para supervisar las consultas y los usuarios del dispositivo. Consulte [supervisar el dispositivo mediante la consola de administración &#40;Analytics Platform System&#41;](monitor-the-appliance-by-using-the-admin-console.md)<!-- MISSING LINKS and [User Sessions &#40;SQL Server PDW&#41;](../sqlpdw/user-sessions-sql-server-pdw.md)-->.|  
|Cargar datos en PDW de SQL Server|Cargue datos en su dispositivo. <!-- MISSING LINKS See [Load &#40;SQL Server PDW&#41;](../sqlpdw/load-sql-server-pdw.md).-->|  
|Crear un plan de recuperación ante desastres|Planear cómo sus datos estarán protegidos frente a errores de hardware o datos sobrescriben. Crear un plan de copias de seguridad periódicas y restauración de los planes en el caso de daños en los datos o la pérdida. <!-- MISSING LINKS See [Create a Disaster Recovery Plan &#40;SQL Server PDW&#41;](../sqlpdw/create-a-disaster-recovery-plan-sql-server-pdw.md).-->|  
|Supervisión del dispositivo|Supervisar el estado del dispositivo, el estado y el rendimiento mediante el uso de vistas del sistema, registros y la consola de administración. Corrija o informe de cualquier problema. Consulte [Monitor de estado de dispositivo &#40;Analytics Platform System&#41;](../relational-databases/system-dynamic-management-views/sys-dm-pdw-component-health-status-transact-sql.md).|  
