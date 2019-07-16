---
title: Listas de comprobación de configuración - Analytics Platform System | Microsoft Docs
description: Proporciona listas de comprobación para las tareas necesarias para configurar Analytics Platform System para su propio entorno. Estas tareas de configuración son necesarias para poder usar el dispositivo.
author: mzaman1
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.openlocfilehash: 9977ac8ea73e37afef85a46d6794ea5136357b44
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "67961596"
---
# <a name="appliance-configuration-checklists-for-analytics-platform-system"></a>Listas de comprobación de configuración de dispositivo para Analytics Platform System
Proporciona listas de comprobación para las tareas necesarias para configurar Analytics Platform System para su propio entorno. Estas tareas de configuración son necesarias para poder usar el dispositivo.  
  
> [!WARNING]  
> Uso de Analytics Platform System**Configuration Manager** es la mejor manera y la única forma para realizar las tareas disponibles en la herramienta admite.  
  
## <a name="BeforeTasks"></a>Antes de empezar  
  
### <a name="prerequisites"></a>Requisitos previos  
  
1.  El dispositivo debe estar instalado en el centro de datos y encendido.  
  
2.  Asegúrese de que tiene la información siguiente, que proporciona el IHV:  
  
    -   Dirección IP externa para el nodo de Control de PDW (*PDW_region -* CTL01)  
  
    -   Nombre de dominio de aplicación  
  
    -   Nombre de usuario y contraseña para el Administrador de dominio de aplicación  
  
3.  Obtener un certificado de confianza. Se importará en un paso posterior para permitir que los clientes se conecten a la **Admin Console** con conexiones seguras. Guarde el certificado en el nodo de Control en un archivo PFX protegido con contraseña.  
  
4.  Iniciar el **Configuration Manager**, mediante los siguientes pasos:  
  
    1.  Use **escritorio remoto** para conectarse al nodo de Control de PDW (*PDW_region*-CTL01). (Es posible que deba conectarse con la dirección IP externa para CTL01.)  
  
    2.  Iniciar el **Configuration Manager** desde el **iniciar** menú del nodo de Control de PDW. La primera pantalla del Administrador de configuración muestra la topología del dispositivo, que se creó con el IHV. Es una lista de los nodos de hardware reconocidos por el software de PDW de SQL Server como parte de su dispositivo. No es necesario cambiar la configuración en la pantalla de la topología del dispositivo.  
  
## <a name="CMTasks"></a>Realizar tareas de Configuration Manager  
SQL Server PDW**Configuration Manager** (PDWCM) es una herramienta de administración de dispositivo que los administradores del sistema de PDW de SQL Server usar para realizar operaciones de nivel de dispositivo y para cambiar la configuración de nivel de dispositivo. Por ejemplo, utilice PDWCM para restablecer las contraseñas, establezca la zona horaria, cambian las direcciones IP, configurar certificados SSL, habilitar el acceso remoto a través del firewall, iniciar o detener el dispositivo y establecer la inicialización instantánea de archivos.  
  
Use **Configuration Manager** para realizar las siguientes tareas de configuración.  
  
|Tarea de configuración|Descripción|  
|----------------------|---------------|  
|Familiarizarse con los nombres de componentes físicos|[Componentes físicos PDW y el tejido de dispositivo &#40;Analytics Platform System&#41;](pdw-and-appliance-fabric-physical-components.md)|  
|Inicie el Administrador de configuración de SQL Server PDW|[Inicie el Administrador de configuración &#40;Analytics Platform System&#41;](launch-the-configuration-manager.md)|  
|Cambiar la contraseña de administrador de dominio|El dispositivo tiene una privada Windows Active Directory Domain Services que se usa para autenticar nodos en el dispositivo.<br /><br />El IHV de configurar el dispositivo con una contraseña de administrador de dominio predeterminada. Esto se debe cambiarse a una contraseña segura.<br /><br />El **Configuration Manager** es la única manera admitida para cambiar la contraseña de administrador de dominio.<br /><br />Para obtener más información, consulte [de restablecimiento de contraseña &#40;Analytics Platform System&#41;](password-reset.md).|  
|Cambiar la contraseña de la **sa** inicio de sesión|PDW de SQL Server tiene un inicio de sesión del administrador del sistema denominada **sa**. El **sa** inicio de sesión tiene todos los privilegios. Puede conceder, denegar o revocar los permisos. También pueden ver todas las vistas del sistema.<br /><br />Para obtener más información, consulte [de restablecimiento de contraseña &#40;Analytics Platform System&#41;](password-reset.md).|  
|Establecer la zona horaria del dispositivo|Establecer el tiempo (tiempo deseado local u otro) para todos los nodos del dispositivo.<br /><br />Para obtener más información, consulte [configuración de zona horaria del dispositivo &#40;Analytics Platform System&#41;](appliance-time-zone-configuration.md).|  
|Especificar la configuración de red con orientación externa para el dispositivo PDW de SQL Server|[Configuración de red del dispositivo &#40;Analytics Platform System&#41;](appliance-network-configuration.md)|  
|Importar un certificado de seguridad para la consola de administración|Un certificado puede proporcionar conexiones de capa de Sockets seguros (SSL) a través de HTTPS a la [supervisar el dispositivo mediante la consola de administración &#40;Analytics Platform System&#41;](monitor-the-appliance-by-using-the-admin-console.md). De forma predeterminada, el **Admin Console** incluye un certificado autofirmado que proporciona privacidad, pero no la autenticación de servidor. Este certificado también devuelve un error en Internet Explorer que indica: "Hay un problema con el certificado de seguridad del sitio Web" cuando el usuario se conecta. Aunque esta conexión cifra los datos sobre la marcha entre el cliente y el servidor, la conexión todavía está expuesto a los atacantes.<br /><br />Los administradores de SQL Server PDW inmediatamente deben adquirir un certificado que se encadena a una entidad de certificación de confianza reconocida por los clientes, con el fin de tener una conexión segura y quitar el error que informa de Internet Explorer. Esto requiere un nombre de dominio completo que se asigna la dirección IP virtual del nodo de Control (recomendado) o las barras de un nombre de certificado que coincida con el valor de que los usuarios escriben en sus direcciones del explorador para tener acceso a la consola de administración.<br /><br />Use la **Configuration Manager** para agregar o quitar certificados de confianza. Directamente mediante la herramienta de configuración de certificado de Microsoft Windows HTTP Services (`winHttpCertCfg.exe`) administrar los certificados no se admite.<br /><br />Para obtener más información, consulte [suministro de certificados de PDW &#40;Analytics Platform System&#41;](pdw-certificate-provisioning.md).|
|Modificador de característica|Muestra información sobre los modificadores de características que se introducen en Analytics Platform System AU7. Utilice esta página para habilitar o deshabilitar características y la configuración de Analytics Platform System o actualizar. Cambiar los valores de conmutador de característica requiere un reinicio del servicio.<br /><br />Para obtener más información, consulte [el modificador de característica PDW &#40;Analytics Platform System&#41;](appliance-feature-switch.md).|
|Habilitar o deshabilitar las reglas de Firewall de Windows que permiten o impiden el acceso a puertos específicos en el dispositivo PDW de SQL Server.|Configurará el IHV y habilitar las reglas de firewall que son necesarias para el dispositivo para que funcione correctamente. En la mayoría de los casos se habilita ni deshabilita las reglas de firewall.<br /><br />Para obtener más información, consulte [configuración del Firewall PDW &#40;Analytics Platform System&#41;](pdw-firewall-configuration.md).|  
|Iniciar y detener el dispositivo PDW de SQL Server|Detiene o inicia la aplicación de PDW de SQL Server. Para obtener más información, consulte [estado de servicios de PDW &#40;Analytics Platform System&#41;](pdw-services-status.md).|  
|Revisar opciones de inicialización instantánea de archivos mediante el **privilegios** cuadro de diálogo|Inicialización instantánea de archivos es una característica de SQL Server que permite que las operaciones de archivo de datos se ejecute más rápidamente. Está habilitado en PDW de SQL Server solo si se ha concedido el privilegio SE_MANAGE_VOLUME_NAME a la cuenta de servicio de red. Se ha desactivado de forma predeterminada.<br /><br />Para obtener más información, consulte [configuración de inicialización instantánea de archivos &#40;Analytics Platform System&#41;](instant-file-initialization-configuration.md).|  
|Restaurar la base de datos maestra desde una copia de seguridad|Elimina la actual **maestro** de base de datos y lo reemplaza con una copia de seguridad. Para obtener más información, consulte [restaurar la base de datos Master &#40;Analytics Platform System&#41;](restore-the-master-database.md).|  
  
## <a name="AddTasks"></a>Realizar tareas de configuración adicionales  
Después de realizar la **Configuration Manager** tareas, realice la siguiente lista de tareas de configuración adicionales. Algunas de estas tareas son opcionales.  
  
|Tarea de configuración|Descripción|  
|----------------------|---------------|  
|Software antivirus de terceros puede ser instalado y configurado en el dispositivo PDW de SQL Server para la orientación externa nodos.<br /><br />(Opcional)|Para obtener más información, consulte [Software Antivirus &#40;Analytics Platform System&#41;](antivirus-software.md).|  
|Se puede cambiar la contraseña de DSRM.<br /><br />(Opcional)|Para obtener más información, consulte [establecer contraseña de administrador para iniciar sesión en los nodos de AD en el modo de restauración de servicios de directorio &#40;DSRM&#41; &#40;Analytics Platform System&#41;](set-admin-password-for-logging-on-to-ad-nodes-in-directory-services-restore-mode.md).|  
|Configurar el dispositivo para recibir actualizaciones de software<br /><br />(Se recomienda)|La aplicación debe configurarse para recibir las actualizaciones de software subyacente y PDW de SQL Server.<br /><br />Para obtener más información, consulte [configurar Windows Server Update Services &#40;WSUS&#41; &#40;Analytics Platform System&#41;](configure-windows-server-update-services-wsus.md). Para obtener información acerca de WSUS, consulte [Software Mantenimiento &#40;Analytics Platform System&#41;](software-servicing.md).|  
|Configurar la conectividad a datos externos, como Hadoop o Azure blob storage.<br /><br />(Opcional)|Para obtener más información, consulte [configurar la conectividad de PolyBase a datos externos &#40;Analytics Platform System&#41;](configure-polybase-connectivity-to-external-data.md).|  
|Configurar el Software Antivirus<br /><br />(Opcional)|Las soluciones de antivirus de terceros puede usarse para proteger los nodos con orientación externa, pero no es necesarias. Siga las instrucciones de.|  
|Configurar adaptadores de red InfiniBand en la copia de seguridad y los servidores de carga<br /><br />(Opcional)|Para configurar la copia de seguridad y carga de los servidores para conectarse a SQL Server PDW mediante el uso de la red InfiniBand, deberá configurar los adaptadores de red para permitir que el dispositivo de DNS para resolver la conexión de InfiniBand a la red InfiniBand actualmente activa.|  
|Configurar para enviar datos de telemetría a Microsoft<br /><br />(Opcional)|Para configurar Analytics Platform System para enviar datos de telemetría a Microsoft, deberá ejecutar un script de PowerShell en el nodo de Control. Para obtener instrucciones específicas, consulte [enviar comentarios de telemetría a Microsoft &#40;PDW de SQL Server&#41;](send-telemetry-feedback-to-microsoft-sql-server-pdw.md).|  
  
## <a name="see-also"></a>Vea también  
[Software antivirus &#40;Analytics Platform System&#41;](antivirus-software.md)  
[Configurar adaptadores de red de InfiniBand &#40;SQL Server PDW&#41;](configure-infiniband-network-adapters.md)  
  
