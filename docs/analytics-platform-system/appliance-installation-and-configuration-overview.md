---
title: "Instalación de dispositivo y la información general de configuración (Analytics Platform System)"
author: barbkess
ms.author: barbkess
manager: jhubbard
ms.prod: sql-non-specified
ms.prod_service: mpp-data-warehouse
ms.service: 
ms.component: analytics-platform-system
ms.technology: mpp-data-warehouse
ms.custom: 
ms.date: 01/05/2017
ms.reviewer: na
ms.suite: sql
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 10934f62-4acf-4ca5-b550-f426ba81fe11
caps.latest.revision: "23"
ms.openlocfilehash: 34d66302d0ed114c32e0c6294dfe7789e32a9253
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/17/2017
---
# <a name="appliance-installation-and-configuration-overview"></a>Introducción a la configuración e instalación de dispositivo
Le guía a los administradores del equipo PDW de SQL Server a través de los pasos iniciales para configurar y empezar a usar el nuevo dispositivo PDW de SQL Server.  
  
<!-- MISSING LINKS ## <a name="BeforeYouBegin"></a>Before You Begin  
Before you begin to install, configure, and use your new appliance, we recommend reviewing information about the appliance components. Review the following to familiarize yourself with the appliance:  
  
-   Review [Understanding the Appliance Nodes and Hardware (SQL Server PDW)](assetId:///f60f419f-d1e1-403d-8cf9-07e7ef6d6627) to be sure you understand the components included in your new appliance.  
  
-   Review [Connecting to SQL Server PDW (SQL Server PDW)](assetId:///721851d5-e521-4d5b-ba6d-8e2e9d3c7808) to understand how and when appliance administrators will connect to each appliance node.  
-->

## <a name="InstallHardware"></a>1. Instalar el Hardware  
El dispositivo de nuevo se entregarán en palés al dock en su centro de datos.  
  
> [!IMPORTANT]  
> En algunos casos, el IHV desempaquetar, bastidor y conecte el dispositivo para usted en su centro de datos. Si por lo tanto, estas instrucciones no son necesarias y puede ir a la [3. Configurar el dispositivo](#ConfigureAppliance) sección más adelante.  
  
Si el IHV no está realizando la instalación de hardware, siga estos pasos para instalar el hardware.  
  
|||  
|-|-|  
|**Tarea**|**Description**|  
|Confirmar la documentación|Confirme que ha recibido todos los documentos necesarios e información de su proveedor de hardware independientes (IHV). Vea [información para obtener de su IHV &#40; Sistema de la plataforma de análisis &#41; ](information-to-obtain-from-your-ihv.md).|  
|Instale el hardware|Compruebe el centro de datos puede dar cabida a la aplicación. Mover los componentes del dispositivo al centro de datos. Los conmutadores de red, PDU, rack y cableado. Consulte [la instalación de Hardware &#40; Sistema de la plataforma de análisis &#41; ](hardware-installation.md).|  
  
## <a name="PowerOnAppliance"></a>2. Encienda el dispositivo  
  
|||  
|-|-|  
|**Tarea**|**Description**|  
|Encienda el dispositivo|Potencia en cada nodo del componente de dispositivo en el orden requerido, esperando según sea necesario para confirmar que no se encuentran errores.|  
  
## <a name="ConfigureAppliance"></a>3. Configurar el dispositivo  
  
|||  
|-|-|  
|**Tarea**|**Description**|  
|||  
|Configurar el dispositivo mediante el uso de SQL Server PDW**Configuration Manager**|Utilice el Administrador de configuración para establecer las contraseñas de dispositivo, zonas horarias, configuración de red y del firewall, certificados de seguridad y rendimiento y otras opciones en el dispositivo. Consulte [la configuración del equipo &#40; Sistema de la plataforma de análisis &#41; ](appliance-configuration.md).|  
  
> [!WARNING]  
> Cambios de configuración deben realizarse solo mediante SQL Server PDW**Configuration Manager**. Cambios no se exponen a través de **Configuration Manager** no son compatibles. Por ejemplo, el dispositivo PDW de SQL Server sólo admite la configuración de idioma inglés de Estados Unidos.  
  
## <a name="SoftwareServicing"></a>4. Configurar el servicio de Software  
  
|||  
|-|-|  
|**Tarea**|**Description**|  
|Aplicar las actualizaciones de SQL Server PDW|(Opcional) Debe aplicar una o varias actualizaciones de PDW de SQL Server para actualizar el software de PDW de SQL Server a la versión más reciente. Vea [aplicar las revisiones del sistema de plataforma de análisis &#40; Sistema de la plataforma de análisis &#41; ](apply-analytics-platform-system-hotfixes.md).|  
|Configurar Windows Server Update Services|Configurar el dispositivo para recibir actualizaciones de Windows Server Update Services para admitir el software. Vea [descargar y aplicar las actualizaciones de Microsoft &#40; Sistema de la plataforma de análisis &#41; ](download-and-apply-microsoft-updates.md).|  
  
## <a name="NextSteps"></a>Pasos siguientes  
Después de haber completado todos los pasos anteriores, el dispositivo está listo para su uso. Usted o a otros miembros del personal en su ubicación pueden continuar con las siguientes tareas.  
  
|||  
|-|-|  
|**Tarea**|**Description**|  
|Instalar a controladores de PDW de SQL Server y configurar la conectividad|Configurar los equipos locales para conectarse a SQL Server PDW mediante el uso de SQL Server Data Tools, sqlcmd, software de inteligencia de negocio u otras herramientas. <!-- MISSING LINKS See [Client Tools (SQL Server PDW)](assetId:///721851d5-e521-4d5b-ba6d-8e2e9d3c7808).-->|  
|Crear roles de servidor e inicios de sesión y asignar permisos|Planear y crear roles de servidor e inicios de sesión que permitirán a los usuarios iniciar sesión en SQL Server PDW con los permisos adecuados. <!-- MISSING LINKS See [PDW Permissions &#40;SQL Server PDW&#41;](../sqlpdw/pdw-permissions-sql-server-pdw.md).-->|  
|Configurar la puerta de enlace de administración de datos de Azure|La puerta de enlace permite a los usuarios de Azure tener acceso a datos APS locales mediante la exposición de datos APS como proteger las fuentes de OData. La puerta de enlace ya está instalado en el nodo de Control. Solicitar a Microsoft para obtener ayuda con la configuración.|  
|Las consultas del monitor y los usuarios del dispositivo|Utilice la consola de administración y otros recursos para supervisar las consultas y los usuarios del dispositivo. Vea [supervisar el dispositivo mediante la consola de administración &#40; Sistema de la plataforma de análisis &#41; ](monitor-the-appliance-by-using-the-admin-console.md)<!-- MISSING LINKS and [User Sessions &#40;SQL Server PDW&#41;](../sqlpdw/user-sessions-sql-server-pdw.md)-->.|  
|Cargar datos en SQL Server PDW|Cargar datos en el dispositivo. <!-- MISSING LINKS See [Load &#40;SQL Server PDW&#41;](../sqlpdw/load-sql-server-pdw.md).-->|  
|Crear un plan de recuperación ante desastres|Planear cómo protegerá los datos de errores de hardware o la sobrescritura de datos. Crear un plan mediante copias de seguridad periódicas y planes en el caso de daños en los datos o la pérdida de restauración. <!-- MISSING LINKS See [Create a Disaster Recovery Plan &#40;SQL Server PDW&#41;](../sqlpdw/create-a-disaster-recovery-plan-sql-server-pdw.md).-->|  
|Supervisar el dispositivo|Supervisar el estado del dispositivo, el estado y el rendimiento mediante el uso de vistas del sistema, los registros y la consola de administración. Corrija o informar de los problemas. Vea [Monitor de estado de dispositivo &#40; Sistema de la plataforma de análisis &#41; ](../relational-databases/system-dynamic-management-views/sys-dm-pdw-component-health-status-transact-sql.md).|  
