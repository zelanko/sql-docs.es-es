---
title: Instalación y configuración del dispositivo
description: Recorra a los administradores de dispositivos de Analytics Platform System (APS) a través de los pasos iniciales para configurar y empezar a usar el nuevo dispositivo.
author: mzaman1
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.custom: seo-dt-2019
ms.openlocfilehash: 9f96d953dbd427bfb6cf94470c0ee80ade3aed48
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "74401444"
---
# <a name="appliance-installation-and-configuration-for-analytics-platform-system"></a>Instalación y configuración del dispositivo de Analytics Platform System
Recorra a los administradores de dispositivos de Analytics Platform System (APS) a través de los pasos iniciales para configurar y empezar a usar el nuevo dispositivo.  
  
<!-- MISSING LINKS ## <a name="BeforeYouBegin"></a>Before You Begin  
Before you begin to install, configure, and use your new appliance, we recommend reviewing information about the appliance components. Review the following to familiarize yourself with the appliance:  
  
-   Review [Understanding the Appliance Nodes and Hardware (SQL Server PDW)](assetId:///f60f419f-d1e1-403d-8cf9-07e7ef6d6627) to be sure you understand the components included in your new appliance.  
  
-   Review [Connecting to SQL Server PDW (SQL Server PDW)](assetId:///721851d5-e521-4d5b-ba6d-8e2e9d3c7808) to understand how and when appliance administrators will connect to each appliance node.  
-->

## <a name="InstallHardware"></a>1. instalar el hardware  
El nuevo dispositivo se entregará en los palets en el Dock del centro de datos.  
  
> [!IMPORTANT]  
> En algunos casos, el IHV desempaquetará, bastidor y conectará el dispositivo en su centro de datos. Si es así, estas instrucciones no son necesarias y puede ir a la [3. Configure la sección del dispositivo](#ConfigureAppliance) a continuación.  
  
Si el IHV no está realizando la instalación de hardware, siga estos pasos para instalar el hardware.  
  
|||  
|-|-|  
|**Task**|**Descripción**|  
|Confirmar documentación|Confirme que ha recibido todos los documentos e información necesarios de su proveedor de hardware independiente (IHV). Consulte [la información que se obtiene de la&#41;del sistema IHV &#40;Analytics Platform System ](information-to-obtain-from-your-ihv.md).|  
|Instalar hardware|Compruebe que el centro de datos puede alojar el dispositivo. Mueva los componentes del dispositivo al centro de datos. Bastidor de conmutadores de red, PDU y cableado. Consulte [instalación de Hardware &#40;Analytics Platform System&#41;](hardware-installation.md).|  
  
## <a name="PowerOnAppliance"></a>2. encender el dispositivo  
  
|||  
|-|-|  
|**Task**|**Descripción**|  
|Encender el dispositivo|Encienda cada nodo del componente del dispositivo en el orden requerido, en espera según sea necesario para confirmar que no se producen errores.|  
  
## <a name="ConfigureAppliance"></a>3. configurar el dispositivo  
  
|||  
|-|-|  
|**Task**|**Descripción**|  
|||  
|Configure el dispositivo mediante el PDW de SQL Server**Configuration Manager**|Use el Configuration Manager para establecer contraseñas de aplicación, zonas horarias, configuración de red y firewall, certificados de seguridad y rendimiento y otras opciones de configuración en el dispositivo. Consulte [configuración del dispositivo &#40;Analytics Platform System&#41;](appliance-configuration.md).|  
  
> [!WARNING]  
> Los cambios de configuración solo deben realizarse mediante el**Configuration Manager**de PDW de SQL Server. No se admiten los cambios que no se exponen mediante **Configuration Manager** . Por ejemplo, el dispositivo PDW de SQL Server solo es compatible con la configuración del idioma Inglés de EE. UU.  
  
## <a name="SoftwareServicing"></a>4. configurar el servicio de software  
  
|||  
|-|-|  
|**Task**|**Descripción**|  
|Aplicar actualizaciones de PDW de SQL Server|Opta Es posible que tenga que aplicar una o varias actualizaciones de PDW de SQL Server para actualizar el software de PDW de SQL Server a la versión más reciente. Consulte [Apply Analytics Platform System revisations &#40;Analytics Platform system&#41;](apply-analytics-platform-system-hotfixes.md).|  
|Configuración de Windows Server Update Services|Configure el dispositivo para recibir actualizaciones de Windows Server Update Services para el software auxiliar. Consulte [Descargar y aplicar actualizaciones de Microsoft &#40;Analytics Platform System&#41;](download-and-apply-microsoft-updates.md).|  
  
## <a name="NextSteps"></a>Pasos siguientes  
Una vez completados todos los pasos anteriores, el dispositivo está listo para su uso. Usted u otro personal de su ubicación puede continuar con las siguientes tareas.  
  
|||  
|-|-|  
|**Task**|**Descripción**|  
|Instalación de controladores de PDW de SQL Server y configuración de la conectividad|Configure los equipos locales para que se conecten a PDW de SQL Server mediante SQL Server Data Tools, SQLCMD, software de Business Intelligence u otras herramientas. <!-- MISSING LINKS See [Client Tools (SQL Server PDW)](assetId:///721851d5-e521-4d5b-ba6d-8e2e9d3c7808).-->|  
|Crear inicios de sesión y roles de servidor y asignar permisos|Planee y cree inicios de sesión y roles de servidor que permitirán a los usuarios iniciar sesión en PDW de SQL Server con los permisos adecuados. <!-- MISSING LINKS See [PDW Permissions &#40;SQL Server PDW&#41;](../sqlpdw/pdw-permissions-sql-server-pdw.md).-->|  
|Configuración de Azure Data Management Gateway|La puerta de enlace permite a los usuarios de Azure acceder a datos de APS locales mediante la exposición de datos de APS como fuentes de OData seguras. La puerta de enlace ya está instalada en el nodo de control. Pida ayuda a Microsoft para la configuración.|  
|Supervisión de consultas y usuarios de dispositivos|Use la consola de administración de y otros recursos para supervisar las consultas y los usuarios del dispositivo. Consulte [supervisión del dispositivo mediante la consola de administración &#40;Analytics Platform System&#41;](monitor-the-appliance-by-using-the-admin-console.md)<!-- MISSING LINKS and [User Sessions &#40;SQL Server PDW&#41;](../sqlpdw/user-sessions-sql-server-pdw.md)-->.|  
|Cargar datos en PDW de SQL Server|Cargar datos en el dispositivo. <!-- MISSING LINKS See [Load &#40;SQL Server PDW&#41;](../sqlpdw/load-sql-server-pdw.md).-->|  
|Creación de un plan de recuperación ante desastres|Planee cómo va a proteger los datos de errores de hardware o sobrescrituras de datos. Cree un plan con copias de seguridad periódicas y planes de restauración en caso de daños o pérdida de datos. <!-- MISSING LINKS See [Create a Disaster Recovery Plan &#40;SQL Server PDW&#41;](../sqlpdw/create-a-disaster-recovery-plan-sql-server-pdw.md).-->|  
|Supervisar el dispositivo|Supervise el estado del dispositivo, el estado y el rendimiento mediante las vistas del sistema, los registros y la consola de administración. Corrija o notifique cualquier problema. Consulte [supervisión del estado de mantenimiento del dispositivo &#40;Analytics Platform System&#41;](../relational-databases/system-dynamic-management-views/sys-dm-pdw-component-health-status-transact-sql.md).|  
