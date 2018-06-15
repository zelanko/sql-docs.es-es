---
title: Listas de comprobación de configuración - Analytics Platform System | Documentos de Microsoft
description: Proporciona listas de comprobación para las tareas necesarias para configurar el sistema de la plataforma de análisis para su propio entorno. Estas tareas de configuración son necesarias para poder usar el dispositivo.
author: mzaman1
manager: craigg
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.openlocfilehash: 17099af36994f24d182c7465bcbdc3f82e670328
ms.sourcegitcommit: fc3cd23685c6b9b6972d6a7bab2cc2fc5ebab5f2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/25/2018
ms.locfileid: "34550726"
---
# <a name="appliance-configuration-checklists-for-analytics-platform-system"></a>Listas de comprobación de configuración de dispositivo de sistema de la plataforma de análisis
Proporciona listas de comprobación para las tareas necesarias para configurar el sistema de la plataforma de análisis para su propio entorno. Estas tareas de configuración son necesarias para poder usar el dispositivo.  
  
> [!WARNING]  
> Usar Analytics Platform System**Configuration Manager** es la mejor manera y la única manera, para realizar las tareas disponibles en la herramienta admite.  
  
## <a name="BeforeTasks"></a>Antes de empezar  
  
### <a name="prerequisites"></a>Requisitos previos  
  
1.  El dispositivo debe estar instalado en el centro de datos y con Bing Maps en.  
  
2.  Asegúrese de que dispone de la información siguiente, que se proporciona mediante el IHV:  
  
    -   Dirección IP externa para el nodo de Control de PDW (*PDW_region -* CTL01)  
  
    -   Nombre de dominio de aplicación  
  
    -   Nombre de usuario y contraseña del Administrador de dominio de aplicación  
  
3.  Obtener un certificado de confianza. Se importarán en un paso posterior para permitir a los clientes para conectarse a la **consola de administración** con conexiones seguras. Guarde el certificado en el nodo de Control en un archivo PFX protegido por contraseña.  
  
4.  Iniciar el **Configuration Manager**, mediante los siguientes pasos:  
  
    1.  Use **escritorio remoto** para conectarse al nodo de Control de PDW (*PDW_region*-CTL01). (Puede que tenga conexión con la dirección IP externa para CTL01).  
  
    2.  Iniciar el **Configuration Manager** desde el **iniciar** menú del nodo de Control de PDW. La primera pantalla del Administrador de configuración muestra la topología de dispositivos, que se creó con el IHV. Es una lista de los nodos de hardware reconocidos por el software de SQL Server PDW como parte de su dispositivo. No es necesario cambiar la configuración en la pantalla de topología de dispositivos.  
  
## <a name="CMTasks"></a>Realizar tareas de Configuration Manager  
SQL Server PDW**Configuration Manager** (PDWCM) es una herramienta de administración de dispositivo que los administradores del sistema de SQL Server PDW usar para realizar operaciones de nivel de dispositivo y para cambiar la configuración de la aplicación. Por ejemplo, utilice PDWCM para restablecer las contraseñas, establezca la zona horaria, cambiar las direcciones IP, configurar certificados de SSL, habilitar el acceso remoto a través del firewall, iniciar o detener el dispositivo y establecer la inicialización instantánea de archivos.  
  
Use **Configuration Manager** para realizar las siguientes tareas de configuración.  
  
|Tarea de configuración|Descripción|  
|----------------------|---------------|  
|Familiarizarse con los nombres de componentes físicos|[Los componentes físicos PDW y el tejido de dispositivo &#40;sistema de la plataforma de análisis&#41;](pdw-and-appliance-fabric-physical-components.md)|  
|Inicie el Administrador de configuración de SQL Server PDW|[Inicie el Administrador de configuración &#40;sistema de la plataforma de análisis&#41;](launch-the-configuration-manager.md)|  
|Cambiar la contraseña de administrador de dominio|El dispositivo tiene una privada Windows Active Directory Domain Services que se utiliza para autenticar los nodos dentro de la aplicación.<br /><br />El IHV configurar el dispositivo con una contraseña de administrador de dominio predeterminada. Esto debe cambiarse a una contraseña segura.<br /><br />El **Configuration Manager** se admite la única forma para cambiar la contraseña de administrador de dominio.<br /><br />Para obtener más información, consulte [de restablecimiento de contraseña &#40;Analytics Platform System&#41;](password-reset.md).|  
|Cambiar la contraseña de la **sa** inicio de sesión|PDW de SQL Server tiene un inicio de sesión de administrador de sistema denominada **sa**. El **sa** inicio de sesión tiene todos los privilegios. Puede conceder, denegar o revocar los permisos. También pueden ver todas las vistas del sistema.<br /><br />Para obtener más información, consulte [de restablecimiento de contraseña &#40;Analytics Platform System&#41;](password-reset.md).|  
|Establecer la zona horaria del dispositivo|Establezca la hora (local o de otros deseado) para todos los nodos de dispositivo.<br /><br />Para obtener más información, consulte [configuración de zona horaria del dispositivo &#40;Analytics Platform System&#41;](appliance-time-zone-configuration.md).|  
|Especificar la configuración de red con orientación externa para la aplicación de SQL Server PDW|[Configuración de red de dispositivo &#40;sistema de la plataforma de análisis&#41;](appliance-network-configuration.md)|  
|Importar un certificado de seguridad para la consola de administración|Un certificado puede proporcionar conexiones de capa de Sockets seguros (SSL) a través de HTTPS el [supervisar el dispositivo mediante la consola de administración &#40;Analytics Platform System&#41;](monitor-the-appliance-by-using-the-admin-console.md). De forma predeterminada, el **consola de administración de** incluye un certificado autofirmado que proporciona privacidad, pero no la autenticación de servidor. Este certificado también devuelve un error en Internet Explorer que indica: "Hay un problema con el certificado de seguridad del sitio Web" cuando el usuario se conecta. Aunque esta conexión cifra los datos sobre la marcha entre el cliente y el servidor, la conexión todavía está expuesto a los atacantes.<br /><br />Los administradores de SQL Server PDW inmediatamente deben adquirir un certificado que se encadena a una entidad de certificación de confianza reconocido por los clientes, con el fin de tener una conexión segura y quitar el error que informa de Internet Explorer. Esto requiere un nombre de dominio completo que se asigna la dirección IP virtual del nodo de Control (recomendado) o barras de un nombre de certificado que coincide con el valor que los usuarios escriban sus direcciones del explorador para tener acceso a la consola de administración.<br /><br />Use la **Configuration Manager** para agregar o quitar certificados de confianza. Directamente mediante la herramienta de configuración de certificado de servicios de Microsoft Windows HTTP (`winHttpCertCfg.exe`) administrar los certificados no se admite.<br /><br />Para obtener más información, consulte [suministro de certificados de PDW &#40;Analytics Platform System&#41;](pdw-certificate-provisioning.md).|
|Modificador de características|Muestra información acerca de los modificadores de función que se introducen en AU7 de sistema de plataforma de análisis. Utilice esta página para actualizar o habilitar o deshabilitar características y configuración de sistema de la plataforma de análisis. Cambiar valores de modificador de características, requiere un reinicio del servicio.<br /><br />Para obtener más información, consulte [modificador de características de PDW &#40;Analytics Platform System&#41;](appliance-feature-switch.md).|
|Habilitar o deshabilitar las reglas de Firewall de Windows que permiten o impedir el acceso a puertos específicos de la aplicación de SQL Server PDW.|El IHV configurará y habilitar las reglas de firewall que son necesarias para la aplicación para que funcione correctamente. En la mayoría de los casos no se habilitar o deshabilitar las reglas de firewall.<br /><br />Para obtener más información, consulte [configuración del Firewall PDW &#40;Analytics Platform System&#41;](pdw-firewall-configuration.md).|  
|Iniciar y detener la aplicación de SQL Server PDW|Detiene o inicia la aplicación de SQL Server PDW. Para obtener más información, consulte [estado de los servicios PDW &#40;Analytics Platform System&#41;](pdw-services-status.md).|  
|Opciones de inicialización instantánea de archivos de revisión mediante la **privilegios** cuadro de diálogo|Inicialización instantánea de archivos es una característica de SQL Server que permite que las operaciones de archivo de datos se ejecute más rápidamente. Está habilitada en SQL Server PDW solo si se ha concedido el privilegio SE_MANAGE_VOLUME_NAME a la cuenta de servicio de red. Se ha desactivado de forma predeterminada.<br /><br />Para obtener más información, consulte [configuración de la inicialización instantánea de archivos &#40;Analytics Platform System&#41;](instant-file-initialization-configuration.md).|  
|Restaurar la base de datos maestra desde una copia de seguridad|Elimina la actual **principal** la base de datos y lo reemplaza con una copia de seguridad. Para obtener más información, consulte [restaurar la base de datos Master &#40;Analytics Platform System&#41;](restore-the-master-database.md).|  
  
## <a name="AddTasks"></a>Realizar tareas de configuración adicionales  
Después de realizar la **Configuration Manager** tareas, realizar la siguiente lista de tareas de configuración adicionales. Algunas de estas tareas son opcionales.  
  
|Tarea de configuración|Descripción|  
|----------------------|---------------|  
|Software antivirus de terceros puede ser instalado y configurado en el dispositivo PDW de SQL Server para la orientación externa nodos.<br /><br />(Opcional)|Para obtener más información, consulte [Software Antivirus &#40;Analytics Platform System&#41;](antivirus-software.md).|  
|Puede cambiarse la contraseña de DSRM.<br /><br />(Opcional)|Para obtener más información, consulte [establecer contraseña de administrador para iniciar sesión en nodos de AD en modo de restauración de servicios de directorio &#40;DSRM&#41; &#40;Analytics Platform System&#41;](set-admin-password-for-logging-on-to-ad-nodes-in-directory-services-restore-mode.md).|  
|Configurar el dispositivo para recibir actualizaciones de software<br /><br />(Se recomienda)|El dispositivo debe configurarse para recibir las actualizaciones de software subyacente y PDW de SQL Server.<br /><br />Para obtener más información, consulte [configurar Windows Server Update Services &#40;WSUS&#41; &#40;Analytics Platform System&#41;](configure-windows-server-update-services-wsus.md). Para obtener información acerca de WSUS, consulte [mantenimiento de Software &#40;Analytics Platform System&#41;](software-servicing.md).|  
|Configurar la conectividad a datos externos, como el almacenamiento de blobs de Azure o Hadoop.<br /><br />(Opcional)|Para obtener más información, consulte [configurar PolyBase conectividad a datos externos &#40;Analytics Platform System&#41;](configure-polybase-connectivity-to-external-data.md).|  
|Configure el Software Antivirus<br /><br />(Opcional)|Soluciones antivirus de terceros pueden usarse para proteger los nodos con orientación externa, pero no es necesarias. Siga las instrucciones de.|  
|Configurar adaptadores de red InfiniBand en copia de seguridad y los servidores de carga<br /><br />(Opcional)|Para configurar copias de seguridad y cargar los servidores para conectarse a SQL Server PDW mediante el uso de la red InfiniBand, debe configurar los adaptadores de red para permitir que el dispositivo DNS para resolver la conexión de InfiniBand a la red InfiniBand actualmente activa.|  
|Configurar para enviar los datos de telemetría a Microsoft<br /><br />(Opcional)|Para configurar el sistema de la plataforma de análisis para enviar los datos de telemetría a Microsoft, debe ejecutar un script de PowerShell en el nodo de Control. Para obtener instrucciones específicas, consulte [enviar comentarios de telemetría a Microsoft &#40;PDW de SQL Server&#41;](send-telemetry-feedback-to-microsoft-sql-server-pdw.md).|  
  
## <a name="see-also"></a>Vea también  
[El Software antivirus &#40;sistema de la plataforma de análisis&#41;](antivirus-software.md)  
[Configurar adaptadores de red InfiniBand &#40;SQL Server PDW&#41;](configure-infiniband-network-adapters.md)  
  
