---
title: Listas de comprobación de configuración
description: Proporciona listas de comprobación para las tareas necesarias para configurar el sistema de plataforma de análisis para su propio entorno. Estas tareas de configuración son necesarias para poder usar el dispositivo.
author: mzaman1
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.custom: seo-dt-2019
ms.openlocfilehash: 80fc899400be167badaae9d617d43a61e0d346b5
ms.sourcegitcommit: ff1bd69a8335ad656b220e78acb37dbef86bc78a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 03/05/2020
ms.locfileid: "78340477"
---
# <a name="appliance-configuration-checklists-for-analytics-platform-system"></a>Listas de comprobación de la configuración del dispositivo para Analytics Platform System
Proporciona listas de comprobación para las tareas necesarias para configurar el sistema de plataforma de análisis para su propio entorno. Estas tareas de configuración son necesarias para poder usar el dispositivo.  
  
> [!WARNING]  
> El uso de Analytics Platform System**Configuration Manager** es la mejor manera y la única manera admitida para realizar las tareas disponibles en la herramienta.  
  
## <a name="BeforeTasks"></a>Antes de empezar  
  
### <a name="prerequisites"></a>Prerrequisitos  
  
1.  El dispositivo debe instalarse en el centro de datos y estar encendido.  
  
2.  Asegúrese de que dispone de la siguiente información, que es proporcionada por el IHV:  
  
    -   Dirección IP externa del nodo de control de PDW (*PDW_region*CTL01)  
  
    -   Nombre de dominio del dispositivo  
  
    -   Nombre de usuario y contraseña para el administrador del dominio del dispositivo  
  
3.  Obtener un certificado de confianza. Lo importará en un paso posterior para permitir que los clientes se conecten a la **consola de administración** con conexiones seguras. Guarde el certificado en el nodo de control en un archivo PFX protegido con contraseña.  
  
4.  Inicie el **Configuration Manager**mediante los pasos siguientes:  
  
    1.  Use **escritorio remoto** para conectarse al nodo de control de PDW (*PDW_region*-CTL01). (Puede que necesite conectarse con la dirección IP externa para CTL01).  
  
    2.  Inicie el **Configuration Manager** desde el menú **Inicio** del nodo control de PDW. En la primera pantalla del Configuration Manager se muestra la topología del dispositivo, creada por el IHV. Se trata de una lista de los nodos de hardware que reconoce el software PDW de SQL Server como parte del dispositivo. No es necesario cambiar la configuración de la pantalla de topología del dispositivo.  
  
## <a name="CMTasks"></a>Realización de tareas de Configuration Manager  
El**Configuration Manager** de PDW de SQL Server (PDWCM) es una herramienta de administración de aplicaciones que PDW de SQL Server los administradores del sistema usan para realizar operaciones de nivel de dispositivo y para cambiar la configuración de nivel de dispositivo. Por ejemplo, use PDWCM para restablecer contraseñas, establecer la zona horaria, cambiar las direcciones IP, configurar los certificados SSL, habilitar el acceso remoto a través del firewall, iniciar o detener el dispositivo y establecer la inicialización instantánea de archivos.  
  
Use **Configuration Manager** para realizar las siguientes tareas de configuración.  
  
|Tarea de configuración|Descripción|  
|----------------------|---------------|  
|Familiarícese con los nombres de los componentes físicos|[Componentes físicos de PDW y Appliance fabric &#40;Analytics Platform System&#41;](pdw-and-appliance-fabric-physical-components.md)|  
|Inicio PDW de SQL Server Configuration Manager|[Inicie el sistema de Configuration Manager &#40;Analytics Platform&#41;](launch-the-configuration-manager.md)|  
|Cambiar la contraseña de administrador de dominio|El dispositivo tiene una Active Directory Domain Services de Windows privada que se usa para autenticar los nodos dentro del dispositivo.<br /><br />El IHV configura el dispositivo con una contraseña predeterminada de administrador de dominio. Esto debe cambiarse a una contraseña segura.<br /><br />La **Configuration Manager** es la única manera admitida para cambiar la contraseña del administrador de dominio.<br /><br />Para obtener más información, consulte [restablecimiento de contraseña &#40;Analytics Platform System&#41;](password-reset.md).|  
|Cambiar la contraseña para el inicio de sesión de **SA**|PDW de SQL Server tiene un inicio de sesión de administrador del sistema denominado **SA**. El inicio de sesión **SA** tiene todos los privilegios. Puede conceder, denegar o revocar cualquier permiso. También puede ver todas las vistas del sistema.<br /><br />Para obtener más información, consulte [restablecimiento de contraseña &#40;Analytics Platform System&#41;](password-reset.md).|  
|Establecimiento de la zona horaria del dispositivo|Establezca la hora (local u otra hora deseada) para todos los nodos del dispositivo.<br /><br />Para obtener más información, consulte [configuración de zona horaria del dispositivo &#40;Analytics Platform System&#41;](appliance-time-zone-configuration.md).|  
|Especificar la configuración de red orientada externamente para el dispositivo PDW de SQL Server|[Configuración de red de dispositivo &#40;Analytics Platform System&#41;](appliance-network-configuration.md)|  
|Importar un certificado de seguridad para la consola de administración|Un certificado puede proporcionar conexiones Capa de sockets seguros (SSL) a través de HTTPS para [supervisar el dispositivo mediante la consola de administración &#40;Analytics Platform System&#41;](monitor-the-appliance-by-using-the-admin-console.md). De forma predeterminada, la **consola de administración** incluye un certificado autofirmado que proporciona privacidad, pero no la autenticación de servidor. Este certificado también devuelve un error en Internet Explorer que indica: "hay un problema con el certificado de seguridad de este sitio web" cuando el usuario se conecta. Aunque esta conexión cifra los datos en vuelo entre el cliente y el servidor, la conexión sigue en riesgo de los atacantes.<br /><br />PDW de SQL Server los administradores deben adquirir inmediatamente un certificado que se encadene a una entidad de certificación de confianza que reconozcan los clientes, con el fin de tener una conexión segura y quitar el error que informa de Internet Explorer. Esto requiere un nombre de dominio completo que asigne la dirección IP virtual del nodo de control (recomendado) o un nombre de certificado que coincida con el valor que los usuarios escriben en sus barras de direcciones del explorador para tener acceso a la consola de administración.<br /><br />Use el **Configuration Manager** para agregar o quitar certificados de confianza. No se admite directamente el uso de la herramienta de configuración`winHttpCertCfg.exe`de certificados de Microsoft Windows http Services () para administrar certificados.<br /><br />Para obtener más información, consulte el [aprovisionamiento de certificados PDW &#40;Analytics Platform System&#41;](pdw-certificate-provisioning.md).|
|Modificador de características|Muestra información sobre los modificadores de características que se introdujeron en Analytics Platform System AU7. Use esta página para actualizar o habilitar o deshabilitar características y configuraciones en Analytics Platform System. Cambiar los valores del modificador de características requiere un reinicio del servicio.<br /><br />Para más información, consulte [conmutador de características de PDW &#40;Analytics Platform System&#41;](appliance-feature-switch.md).|
|Habilitar o deshabilitar las reglas de Firewall de Windows que permiten o impiden el acceso a puertos específicos en el dispositivo PDW de SQL Server.|El IHV configurará y habilitará las reglas de Firewall necesarias para que el dispositivo funcione correctamente. En la mayoría de los casos, no se habilitarán o deshabilitarán las reglas de Firewall.<br /><br />Para obtener más información, consulte [PDW Firewall Configuration &#40;Analytics Platform System&#41;](pdw-firewall-configuration.md).|  
|Iniciar y detener el dispositivo PDW de SQL Server|Detiene o inicia la aplicación PDW de SQL Server. Para obtener más información, consulte el estado de los [servicios de PDW &#40;Analytics Platform System&#41;](pdw-services-status.md).|  
|Revisar las opciones de inicialización instantánea de archivos mediante el cuadro de diálogo **privilegios**|La inicialización instantánea de archivos es una característica SQL Server que permite que las operaciones de archivo de datos se ejecuten más rápidamente. Solo se habilita en PDW de SQL Server si se ha concedido el privilegio SE_MANAGE_VOLUME_NAME a la cuenta servicio de red. Está desactivada de forma predeterminada.<br /><br />Para obtener más información, vea configuración de la [inicialización instantánea de archivos &#40;Analytics Platform System&#41;](instant-file-initialization-configuration.md).|  
|Restaurar la base de datos maestra a partir de una copia de seguridad|Elimina la base de datos **maestra** actual y la reemplaza por una copia de seguridad. Para obtener más información, vea [restaurar la base de datos maestra &#40;Analytics Platform System&#41;](restore-the-master-database.md).|  
  
## <a name="AddTasks"></a>Realizar tareas de configuración adicionales  
Después de realizar las tareas de **Configuration Manager** , realice la siguiente lista de tareas de configuración adicionales. Algunas de estas tareas son opcionales.  
  
|Tarea de configuración|Descripción|  
|----------------------|---------------|  
|El software antivirus de terceros puede instalarse y configurarse en el dispositivo PDW de SQL Server para los nodos orientados externamente.<br /><br />(Opcional)|Para obtener más información, consulte [antivirus Software &#40;Analytics Platform System&#41;](antivirus-software.md).|  
|Se puede cambiar la contraseña de DSRM.<br /><br />(Opcional)|Para obtener más información, vea [establecer la contraseña de administrador para iniciar sesión en los nodos de AD en Modo de restauración de servicios de directorio &#40;DSRM&#41; &#40;Analytics Platform System&#41;](set-admin-password-for-logging-on-to-ad-nodes-in-directory-services-restore-mode.md).|  
|Configurar el dispositivo para recibir actualizaciones de software<br /><br />(Se recomienda)|El dispositivo debe configurarse para recibir actualizaciones del PDW de SQL Server y el software subyacente.<br /><br />Para obtener más información, consulte [configuración de Windows Server Update Services &#40;WSUS&#41; &#40;Analytics Platform System&#41;](configure-windows-server-update-services-wsus.md). Para obtener información sobre WSUS, consulte [servicio de Software &#40;Analytics Platform System&#41;](software-servicing.md).|  
|Configure la conectividad a datos externos, como Hadoop o Azure BLOB Storage.<br /><br />(Opcional)|Para obtener más información, consulte Configuración de la [conectividad de polybase con datos externos &#40;análisis de plataforma del sistema&#41;](configure-polybase-connectivity-to-external-data.md).|  
|Configurar el software antivirus<br /><br />(Opcional)|Las soluciones antivirus de terceros se pueden usar para proteger los nodos orientados externamente, pero no es necesario. Siga las instrucciones de.|  
|Configuración de adaptadores de red InfiniBand en servidores de copia de seguridad y carga<br /><br />(Opcional)|Para configurar los servidores de copia de seguridad y carga para que se conecten a PDW de SQL Server mediante la red InfiniBand, debe configurar los adaptadores de red para permitir que el DNS del dispositivo resuelva la conexión de InfiniBand con la red InfiniBand activa actualmente.|  
|Configurar para enviar datos de telemetría a Microsoft<br /><br />(Opcional)|Para configurar Analytics Platform System para que envíe datos de telemetría a Microsoft, debe ejecutar un script de PowerShell en el nodo de control. Para obtener instrucciones específicas, consulte [envío de comentarios de telemetría a Microsoft &#40;PDW de SQL Server&#41;](send-telemetry-feedback-to-microsoft-sql-server-pdw.md).|  
  
## <a name="see-also"></a>Consulte también  
[Software antivirus &#40;Analytics Platform System&#41;](antivirus-software.md)  
[Configuración de adaptadores de red InfiniBand &#40;PDW de SQL Server&#41;](configure-infiniband-network-adapters.md)  
  
