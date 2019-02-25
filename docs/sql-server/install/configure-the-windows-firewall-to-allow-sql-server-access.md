---
title: Configurar el Firewall de Windows para permitir el acceso a SQL Server | Microsoft Docs
ms.custom: ''
ms.date: 05/17/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: install
ms.topic: conceptual
helpviewer_keywords:
- Windows Firewall ports
- WMI firewall ports
- Windows Firewall [Database Engine]
- firewall systems, configuring
- advfirewall
- firewall systems
- rules firewall
- firewall systems, overview and port list
- 1433 TCP port
- portopening using netsh
- ports [SQL Server], TCP
- netsh to open firewall ports
ms.assetid: f55c6a0e-b6bd-4803-b51a-f3a419803024
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 18808e95920384ec9b17e0514a286a675531322b
ms.sourcegitcommit: a13256f484eee2f52c812646cc989eb0ce6cf6aa
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 02/25/2019
ms.locfileid: "56803310"
---
# <a name="configure-the-windows-firewall-to-allow-sql-server-access"></a>Configure the Windows Firewall to Allow SQL Server Access
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

Los sistemas de firewall ayudan a evitar el acceso no autorizado a los recursos de los equipos. Si un firewall está activado pero no está configurado correctamente, es posible que se bloqueen los intentos de conexión a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
Para obtener acceso a una instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] a través de un firewall, debe configurar el firewall en el equipo en el que se ejecuta [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. El firewall es un componente de [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows. También puede instalar un firewall de otra compañía. En este artículo se explica cómo configurar el firewall de Windows, pero los principios básicos se aplican a otros programas de firewall.  
  
> [!NOTE]  
>  En este artículo se proporciona información general para configurar el firewall y se resume información de interés para administradores de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Para obtener más información acerca del firewall e información autorizada, vea la documentación sobre el firewall como [Windows Firewall con seguridad avanzada e IPsec](https://go.microsoft.com/fwlink/?LinkID=116904).  
  
 Los usuarios que conozcan el elemento **Firewall de Windows** del Panel de control y el complemento Microsoft Management Console (MMC) de Firewall de Windows con seguridad avanzada, y que sepan qué opciones del firewall quieren configurar, pueden ir directamente a los artículos de esta lista:  
  
-   [Configurar Firewall de Windows para el acceso al motor de base de datos](../../database-engine/configure-windows/configure-a-windows-firewall-for-database-engine-access.md)  
  
-   [Configurar Firewall de Windows para permitir el acceso a Analysis Services](../../analysis-services/instances/configure-the-windows-firewall-to-allow-analysis-services-access.md)  
  
-   [Configurar un firewall para el acceso al servidor de informes](../../reporting-services/report-server/configure-a-firewall-for-report-server-access.md)  
  
##  <a name="BKMK_basic"></a> Información básica del firewall  
 Los firewalls funcionan inspeccionando los paquetes entrantes y comparándolos con un conjunto de reglas. Si las reglas permiten el paquete, el firewall pasa el paquete al protocolo TCP/IP para su procesamiento adicional. Si las reglas no permiten el paquete, el firewall descarta el paquete y, si está habilitado el registro, crea una entrada en el archivo de registro del firewall.  
  
 La lista de tráfico permitido se rellena de una de las maneras siguientes:  
  
-   Cuando el equipo que tiene el firewall habilitado inicia la comunicación, el firewall crea una entrada en la lista para que se permita la respuesta. La respuesta de entrada se considera tráfico solicitado y no es necesario configurarla.  
  
-   Un administrador configura las excepciones para el firewall. Esto permite el acceso a programas específicos que se ejecutan en el equipo o el acceso a los puertos de conexión especificados en el equipo. En este caso, el equipo acepta el tráfico de entrada no solicitado cuando actúa como un servidor, un agente de escucha o un equipo del mismo nivel. Éste es el tipo de configuración que se debe completar para conectar a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 Elegir una estrategia del firewall es más complejo que decidir simplemente si un puerto determinado debe estar abierto o cerrado. Al diseñar una estrategia de firewall para la empresa, asegúrese considerar todas las reglas y opciones de configuración disponibles. En este artículo no se revisan todas las posibles opciones de firewall. Se recomienda que revise los siguientes documentos:  
  
 [Guía de introducción del Firewall de Windows con seguridad avanzada](https://go.microsoft.com/fwlink/?LinkId=116080)  
  
 [Guía de diseño del Firewall de Windows con seguridad avanzada](https://go.microsoft.com/fwlink/?LinkId=116904)  
  
 [Introducción al aislamiento de servidor y dominio](https://go.microsoft.com/fwlink/?LinkId=116081)  
  
##  <a name="BKMK_default"></a> Configuración predeterminada del firewall  
 El primer paso para planear la configuración del firewall es determinar el estado actual del firewall para el sistema operativo. Si el sistema operativo se actualizó desde una versión anterior, se puede haber conservado la configuración de firewall anterior. Además, otro administrador o una Directiva de grupo podría haber cambiado la configuración del firewall en el dominio.  
  
> [!NOTE]  
>  La activación del firewall afectará a otros programas que tengan acceso a este equipo, tales como el uso compartido de impresoras y archivos, y las conexiones remotas al escritorio. Los administradores deben considerar todas las aplicaciones que se están ejecutando en el equipo antes de ajustar la configuración de firewall.  
  
##  <a name="BKMK_programs"></a> Programas para configurar el firewall  
Configure el Firewall de Windows con **Microsoft Management Console** o **netsh**.  

-  **Microsoft Management Console (MMC)**  
  
     El complemento MMC del Firewall de Windows con seguridad avanzada permite establecer opciones de configuración de firewall más avanzadas. Este complemento presenta la mayoría de las opciones de firewall de una manera fácil de usar y presenta todos los perfiles de firewall. Para más información, vea [Utilizar el complemento Firewall de Windows con seguridad avanzada](#BKMK_WF_msc), más adelante en este artículo.  
  
-   **netsh**  
  
     Un administrador puede usar la herramienta **netsh.exe** para configurar y supervisar equipos basados en Windows en un símbolo del sistema o un archivo por lotes **.** Con la herramienta **netsh** , puede dirigir los comandos de contexto que escriba en el asistente adecuado y el asistente ejecutará el comando. Un asistente es un archivo de biblioteca de vínculos dinámicos (.dll) que extiende la funcionalidad de la herramienta **netsh** proporcionando funciones de configuración, supervisión y soporte técnico de uno o más servicios, utilidades o protocolos. Todos los sistemas operativos que admiten [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tienen un asistente de firewall. [!INCLUDE[firstref_longhorn](../../includes/firstref-longhorn-md.md)] también tiene un asistente avanzado denominado **advfirewall**. Los detalles del uso de **netsh** no se explican en este artículo. Sin embargo, muchas de las opciones de configuración descritas se pueden configurar con **netsh**. Por ejemplo, ejecute el script siguiente en un símbolo del sistema para abrir el puerto TCP 1433:  
  
    ```  
    netsh firewall set portopening protocol = TCP port = 1433 name = SQLPort mode = ENABLE scope = SUBNET profile = CURRENT  
    ```  
  
     Un ejemplo similar que usa Firewall de Windows para el asistente Seguridad avanzada:  
  
    ```  
    netsh advfirewall firewall add rule name = SQLPort dir = in protocol = tcp action = allow localport = 1433 remoteip = localsubnet profile = DOMAIN  
    ```  
  
     Para obtener más información acerca de **netsh**, consulte los siguientes vínculos:  
  
    -   [Cómo utilizar la herramienta Netsh.exe y los modificadores de la línea de comandos](https://support.microsoft.com/kb/242468)  
  
    -   [Cómo usar el contexto "netsh advfirewall firewall" en lugar del contexto "netsh firewall" para controlar el comportamiento del Firewall de Windows en Windows Server 2008 y en Windows Vista](https://support.microsoft.com/kb/947709)  
  
    -   [El comando "netsh firewall" junto con el parámetro "profile=all" no configura el perfil público en un equipo basado en Windows Vista](https://support.microsoft.com/kb/947213)  
    
- **Para Linux**: en Linux, también debe abrir los puertos asociados con los servicios a los que necesita acceso. Las distintas distribuciones de Linux y los distintos firewalls tienen sus propios procedimientos. Para ver dos ejemplos, consulte [SQL Server en Red Hat](https://review.docs.microsoft.com/sql/linux/quickstart-install-connect-red-hat?view=sqlallproducts-allversions) y [SQL Server en SUSE](https://review.docs.microsoft.com/sql/linux/quickstart-install-connect-suse?view=sqlallproducts-allversions). 
  
## <a name="ports-used-by-includessnoversionincludesssnoversion-mdmd"></a>Puertos utilizados por [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]  
 Las tablas siguientes pueden ayudarle a identificar los puertos que utiliza [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
###  <a name="BKMK_ssde"></a> Ports Used By the Database Engine  
 La tabla siguiente muestra los puertos de uso frecuente por parte de [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
|Escenario|Puerto|Comentarios|  
|--------------|----------|--------------|  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ejecutándose sobre TCP|Puerto TCP 1433|Éste es el puerto más común que permite el firewall. Se aplica a las conexiones rutinarias a la instalación predeterminada de [!INCLUDE[ssDE](../../includes/ssde-md.md)]o a una instancia con nombre que sea la única instancia que se ejecuta en el equipo. (Las instancias con nombre tienen consideraciones especiales. Vea [Puertos dinámicos](#BKMK_dynamic_ports) más adelante en este artículo).|  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] en la configuración predeterminada|El puerto TCP es un puerto dinámico determinado en el momento en el que se inicia [!INCLUDE[ssDE](../../includes/ssde-md.md)] .|Vea la explicación siguiente en la sección [Puertos dinámicos](#BKMK_dynamic_ports). El puerto UDP 1434 puede ser necesario para el servicio Explorador de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] cuando se utilizan instancias con nombre.|  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] cuando están configuradas para utilizar un puerto fijo|El número de puerto configurado por el administrador.|Vea la explicación siguiente en la sección [Puertos dinámicos](#BKMK_dynamic_ports).|  
|Conexión de administrador dedicada|Puerto TCP 1434 para la instancia predeterminada. Otros puertos se utilizan para las instancias con nombre. Compruebe en el registro de errores el número de puerto.|De forma predeterminada, las conexiones remotas a DAC (Conexión de administrador dedicada) no están habilitadas. Para habilitar la DAC remota, utilice la faceta Configuración de área expuesta. Para obtener más información, vea [Surface Area Configuration](../../relational-databases/security/surface-area-configuration.md).|  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Servicio Browser|Puerto UDP 1434|El servicio Explorador de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] escucha las conexiones entrantes a una instancia con nombre y proporciona al cliente el número de puerto TCP que corresponde a esa instancia con nombre. Normalmente, el servicio Explorador de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] se inicia siempre que se utilizan instancias con nombre de [!INCLUDE[ssDE](../../includes/ssde-md.md)] . El servicio [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Browser no tiene que iniciarse si el cliente está configurado para conectarse al puerto específico de la instancia con nombre.|  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ejecutándose sobre un extremo HTTP.|Se puede especificar cuando se crea un extremo HTTP. El valor predeterminado es el puerto TCP 80 para el tráfico de CLEAR_PORT y el puerto 443 para el tráfico de SSL_PORT.|Se utiliza para una conexión HTTP a través de una dirección URL.|  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ejecutándose en un extremo HTTPS.|Puerto TCP 443|Se utiliza para una conexión HTTPS a través de una dirección URL. HTTPS es una conexión HTTP que utiliza SSL (Capa de sockets seguros).|  
|[!INCLUDE[ssSB](../../includes/sssb-md.md)]|Puerto 4022 TCP. Para comprobar el puerto que se usa, ejecute la siguiente consulta:<br /><br /> `SELECT name, protocol_desc, port, state_desc`<br /><br /> `FROM sys.tcp_endpoints`<br /><br /> `WHERE type_desc = 'SERVICE_BROKER'`|No hay ningún puerto predeterminado para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)][!INCLUDE[ssSB](../../includes/sssb-md.md)], pero esta es la configuración convencional que se usa en los ejemplos de Libros en pantalla.|  
|Creación de reflejo de base de datos|Puerto elegido por el administrador. Para determinar el puerto, ejecute la siguiente consulta:<br /><br /> `SELECT name, protocol_desc, port, state_desc FROM sys.tcp_endpoints`<br /><br /> `WHERE type_desc = 'DATABASE_MIRRORING'`|No hay ningún puerto predeterminado para la creación de reflejo de la base de datos, pero en los ejemplos de los Libros en pantalla se usa el puerto TCP 5022 o 7022. Es muy importante evitar interrumpir un extremo de creación de reflejo que se esté usando, sobre todo en el modo de alta seguridad con conmutación automática por error. La configuración del firewall debe evitar el romper el quórum. Para obtener más información, vea [Especificar una dirección de red de servidor &#40;creación de reflejo de la base de datos&#41;](../../database-engine/database-mirroring/specify-a-server-network-address-database-mirroring.md).|  
|REPLICATION|Las conexiones de replicación a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] utilizan los puertos de [!INCLUDE[ssDE](../../includes/ssde-md.md)] normales (puerto TCP 1433, para la instancia predeterminada, etc.) habituales.<br /><br /> La sincronización web y el acceso de tipo FTP/UNC para la instantánea de replicación requieren que se abran puertos adicionales en el firewall. Para transferir los datos iniciales y los esquemas de una ubicación a otra, la replicación puede utilizar FTP (puerto TCP 21) o sincronizar sobre HTTP (puerto TCP 80) o Uso compartido de archivos. El uso compartido de archivos utiliza los puertos UDP 137 y 138, y el puerto TCP 139 si usa NetBIOS. El uso compartido de archivos usa el puerto TCP 445.|Para la sincronización sobre HTTP, la replicación utiliza el extremo IIS (para el que se pueden configurar los puertos, pero cuyo puerto predeterminado es el 80), pero el proceso IIS se conecta al servidor [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] a través de los puertos estándar (1433 para la instancia predeterminada).<br /><br /> Durante la sincronización web mediante FTP, la transferencia FTP tiene lugar entre IIS y el publicador de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , no entre el suscriptor e IIS.|  
|[!INCLUDE[tsql](../../includes/tsql-md.md)] depurador|Puerto TCP 135<br /><br /> Vea [Consideraciones especiales para el puerto 135](#BKMK_port_135)<br /><br /> Quizá sea necesaria también la excepción [IPsec](#BKMK_IPsec) .|Si utiliza [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)], en el equipo host [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] debe agregar también **Devenv.exe** a la lista Excepciones y abrir el puerto TCP 135.<br /><br /> Si utiliza [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)], en el equipo host [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] debe agregar también **ssms.exe** a la lista Excepciones y abrir el puerto TCP 135. Para obtener más información, vea [Configurar reglas de firewall antes de ejecutar al depurador de TSQL](../../relational-databases/scripting/configure-firewall-rules-before-running-the-tsql-debugger.md).|  
  
 Para obtener instrucciones detalladas sobre cómo configurar Firewall de Windows para el [!INCLUDE[ssDE](../../includes/ssde-md.md)], vea [Configurar Firewall de Windows para el acceso al motor de base de datos](../../database-engine/configure-windows/configure-a-windows-firewall-for-database-engine-access.md).  
  
####  <a name="BKMK_dynamic_ports"></a> Puertos dinámicos  
 De forma predeterminada, las instancias con nombre (incluido [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)]) utilizan puertos dinámicos. Eso significa que cada vez que se inicia [!INCLUDE[ssDE](../../includes/ssde-md.md)] , identifica un puerto disponible y utiliza ese número de puerto. Si la instancia con nombre es la única instancia de [!INCLUDE[ssDE](../../includes/ssde-md.md)] instalada, probablemente utilizará el puerto TCP 1433. Si se instalan otras instancias de [!INCLUDE[ssDE](../../includes/ssde-md.md)] , probablemente utilizará un puerto TCP diferente. Dado que el puerto seleccionado puede cambiar cada vez que se inicia [!INCLUDE[ssDE](../../includes/ssde-md.md)] , es difícil configurar el firewall para permitir el acceso al número de puerto correcto. Por consiguiente, si se usa un firewall, recomendamos reconfigurar el [!INCLUDE[ssDE](../../includes/ssde-md.md)] para que utilice siempre el mismo número de puerto. Esto se denomina un puerto fijo o un puerto estático. Para obtener más información, vea [Configurar un servidor para que escuche en un puerto TCP específico &#40;Administrador de configuración de SQL Server&#41;](../../database-engine/configure-windows/configure-a-server-to-listen-on-a-specific-tcp-port.md).  
  
 Una alternativa a configurar una instancia con nombre para escuchar en un puerto fijo es crear una excepción en el firewall para un programa de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] como **sqlservr.exe** (para el [!INCLUDE[ssDE](../../includes/ssde-md.md)]). Esto puede ser cómodo, pero el número de puerto no aparecerá en la columna **Puerto local** de la página **Reglas de entrada** cuando esté usando el complemento MMC de Firewall de Windows con seguridad avanzada. Esto puede hacer más difícil la tarea de auditar qué puertos están abiertos. Otra consideración es que un Service Pack o una actualización acumulativa puede cambiar la ruta de acceso a la aplicación ejecutable [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , lo que invalidará la regla de firewall.  
  
##### <a name="to-add-a-program-exception-to-the-firewall-using-windows-firewall-with-advanced-security"></a>Para agregar una excepción de programa al firewall mediante el Firewall de Windows con seguridad avanzada
  
1. En el menú Inicio, escriba *wf.msc*. Haga clic en **Firewall de Windows con seguridad avanzada**.

1. En el panel izquierdo, haga clic en **Reglas de entrada**.

1. En el panel derecho, en **Acciones**, haga clic en **Nueva regla…** Se abre el **Asistente para nueva regla de entrada**.

1. En **Tipo de regla**, escriba **Programa**. Haga clic en **Siguiente**.

1. En **Programa**, haga clic en **Esta ruta de acceso del programa**. Haga clic en **Examinar** para buscar la instancia de SQL Server. El programa se denomina sqlservr.exe. Suele encontrarse en:

   `C:\Program Files\Microsoft SQL Server\MSSQL13.<InstanceName>\MSSQL\Binn\sqlservr.exe`

   Haga clic en **Siguiente**.

1. En **Acción**, haga clic en **Permitir la conexión**.  

1. En Perfil, incluya los tres perfiles. Haga clic en **Siguiente**.

1. En **Nombre**, escriba un nombre para la regla. Haga clic en **Finalizar**.

Para obtener más información sobre los puntos de conexión, vea [Configurar el motor de base de datos para escuchar en varios puertos TCP](../../database-engine/configure-windows/configure-the-database-engine-to-listen-on-multiple-tcp-ports.md) y [Vistas de catálogo de puntos de conexión &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/endpoints-catalog-views-transact-sql.md). 
  
###  <a name="BKMK_ssas"></a> Puertos utilizados por Analysis Services  
 La tabla siguiente muestra los puertos de uso frecuente por parte de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)].  
  
|Característica|Puerto|Comentarios|  
|-------------|----------|--------------|  
|[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]|Puerto TCP 2383 para la instancia predeterminada|El puerto estándar para la instancia predeterminada de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)].|  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Servicio Browser|El puerto TCP 2382 solamente es necesario para una instancia con nombre de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]|Las solicitudes de conexión de cliente para una instancia con nombre de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] que no especifican un número de puerto se dirigen al puerto 2382, el puerto en el que escucha el Explorador de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] a continuación redirige la solicitud al puerto que utiliza la instancia con nombre.|  
|[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] configurado para el uso a través de IIS/HTTP<br /><br /> (El Servicio PivotTable® utiliza HTTP o HTTPS)|Puerto TCP 80|Se utiliza para una conexión HTTP a través de una dirección URL.|  
|[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] configurado para el uso a través de IIS/HTTPS<br /><br /> (El Servicio PivotTable® utiliza HTTP o HTTPS)|Puerto TCP 443|Se utiliza para una conexión HTTPS a través de una dirección URL. HTTPS es una conexión HTTP que utiliza SSL (Capa de sockets seguros).|  
  
 Si los usuarios tienen acceso a [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] a través de IIS e Internet, debe abrir el puerto en el que está escuchando IIS y especificar ese puerto en la cadena de conexión del cliente. En este caso, no se tiene que abrir ningún puerto para acceso directo a [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]. El puerto predeterminado, 2389 y el puerto 2382 deben restringirse junto con los demás puertos que no sean necesarios.  
  
 Para obtener instrucciones detalladas sobre cómo configurar Firewall de Windows para [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)], vea [Configurar Firewall de Windows para permitir el acceso a Analysis Services](../../analysis-services/instances/configure-the-windows-firewall-to-allow-analysis-services-access.md).  
  
###  <a name="BKMK_ssrs"></a> Puertos utilizados por Reporting Services  
La tabla siguiente muestra los puertos de uso frecuente por parte de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)].  
  
|Característica|Puerto|Comentarios|  
|-------------|----------|--------------|  
|[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] Servicios Web|Puerto TCP 80|Se utiliza para una conexión HTTP a [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] a través de una dirección URL. Recomendamos no usar la regla preconfigurada **World Wide Web Services (HTTP)**. Para obtener más información, vea la sección [Interacción con otras reglas de firewall](#BKMK_other_rules) más adelante|  
|[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] configurado para el uso a través de HTTPS|Puerto TCP 443|Se utiliza para una conexión HTTPS a través de una dirección URL. HTTPS es una conexión HTTP que utiliza SSL (Capa de sockets seguros). Recomendamos no usar la regla preconfigurada **Secure World Wide Web Services (HTTPS)**. Para obtener más información, vea la sección [Interacción con otras reglas de firewall](#BKMK_other_rules) más adelante|  
  
Cuando [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] se conecta a una instancia de [!INCLUDE[ssDE](../../includes/ssde-md.md)] o [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)], también debe abrir los puertos adecuados para esos servicios. Para obtener instrucciones detalladas sobre cómo configurar Firewall de Windows para [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)], vea [Configurar un firewall para el acceso al servidor de informes](../../reporting-services/report-server/configure-a-firewall-for-report-server-access.md).  
  
###  <a name="BKMK_ssis"></a> Puertos utilizados por Integration Services  
 La tabla siguiente muestra los puertos de uso frecuente por parte del servicio [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] .  
  
|Característica|Puerto|Comentarios|  
|-------------|----------|--------------|  
|[!INCLUDE[msCoName](../../includes/msconame-md.md)] llamadas a procedimiento remoto (MS RPC)<br /><br /> Utilizado por el motor de tiempo de ejecución [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] .|Puerto TCP 135<br /><br /> Vea [Consideraciones especiales para el puerto 135](#BKMK_port_135)|El servicio [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] utiliza DCOM en el puerto 135. El Administrador de control de servicios usa el puerto 135 para realizar tareas tales como iniciar y detener el servicio [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] , y transmitir solicitudes de control al servicio en funcionamiento. No se puede cambiar el número de puerto.<br /><br /> Solamente es necesario que este puerto esté abierto si se está conectando a una instancia remota del servicio [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] desde [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] o desde una aplicación personalizada.|  
  
Para ver instrucciones paso a paso para configurar el Firewall de Windows para [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)], vea [Integration Services Service &#40;SSIS Service&#41;](../../integration-services/service/integration-services-service-ssis-service.md) (Servicio de Integration Services &#40;Servicio SSIS&#41;).  
  
###  <a name="BKMK_additional_ports"></a> Puertos y servicios adicionales  
La tabla siguiente muestra los puertos y servicios de los que puede depender [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
|Escenario|Puerto|Comentarios|  
|--------------|----------|--------------|  
|Instrumental de administración de Windows<br /><br /> Para obtener más información acerca de WMI, vea [WMI Provider for Configuration Management Concepts](../../relational-databases/wmi-provider-configuration/wmi-provider-for-configuration-management.md).|WMI se ejecuta como parte de un host de servicio compartido con puertos asignados a través de DCOM. WMI podría estar utilizando el puerto TCP 135.<br /><br /> Vea [Consideraciones especiales para el puerto 135](#BKMK_port_135)|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] utiliza WMI para enumerar y administrar servicios. Recomendamos usar el grupo de reglas preconfigurado **Instrumental de administración de Windows (WMI)**. Para obtener más información, vea la sección [Interacción con otras reglas de firewall](#BKMK_other_rules) más adelante|  
|[!INCLUDE[msCoName](../../includes/msconame-md.md)] Coordinador de transacciones distribuidas de (MS DTC)|Puerto TCP 135<br /><br /> Vea [Consideraciones especiales para el puerto 135](#BKMK_port_135)|Si la aplicación utiliza transacciones distribuidas, quizá deba configurar el firewall para permitir que el tráfico del Coordinador de transacciones distribuidas de [!INCLUDE[msCoName](../../includes/msconame-md.md)] (MS DTC) fluya entre instancias independientes de MS DTC y entre MS DTC y administradores de recursos como [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Se recomienda usar el grupo de reglas preconfigurado **Coordinador de transacciones distribuidas** .<br /><br /> Cuando se configura un único MS DTC compartido para todo el clúster en un grupo de recursos independiente, se debería agregar sqlservr.exe como excepción al firewall.|  
|El botón Examinar en [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] utiliza UDP para establecer conexión con el servicio [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Browser. Para obtener más información, vea [Servicio SQL Server Browser &#40;motor de base de datos y SSAS&#41;](../../database-engine/configure-windows/sql-server-browser-service-database-engine-and-ssas.md).|Puerto UDP 1434|UDP es un protocolo sin conexión.<br /><br /> El firewall tiene una configuración, que se denomina [Propiedad UnicastResponsesToMulticastBroadcastDisabled de la interfaz INetFwProfile](https://go.microsoft.com/fwlink/?LinkId=118371) y controla el comportamiento del firewall respecto a las respuestas de unidifusión a una solicitud UDP de difusión (o multidifusión).  Tiene dos comportamientos.<br /><br /> Si el valor es TRUE, no se permite en absoluto ninguna respuesta de unidifusión a una difusión. La enumeración de servicios producirá un error.<br /><br /> Si la configuración es FALSE (valor predeterminado), las respuestas de unidifusión se permiten durante 3 segundos. La longitud de tiempo no es configurable. En una red congestionada o de latencia alta, o en servidores muy cargados, los intentos de enumerar instancias de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] pueden devolver una lista parcial, que puede desorientar a los usuarios.|  
|<a name="BKMK_IPsec"></a> Tráfico IPSec|Puerto UDP 500 y puerto UDP 4500|Si la directiva de dominio requiere que las comunicaciones se realicen a través de IPSec, también debe agregar los puertos UDP 4500 y 500 a la lista de excepciones. IPSec es una opción que usa el **Asistente para nueva regla de entrada** en el complemento de Firewall de Windows. Para obtener más información, vea [Utilizar el complemento Firewall de Windows con seguridad avanzada](#BKMK_WF_msc) más adelante.|  
|Utilizar la autenticación de Windows con dominios de confianza|Los firewalls se deben configurar para permitir solicitudes de autenticación.|Para obtener más información, vea [Cómo configurar un firewall para dominios y confianza](https://support.microsoft.com/kb/179442/).|  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] y Agrupación en clústeres de Windows|La agrupación en clústeres requiere puertos adicionales que no se relacionan directamente con [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|Para obtener más información, vea [Habilitar una red para el uso de clústeres](https://go.microsoft.com/fwlink/?LinkId=118372).|  
|Espacios de nombres URL reservados en la API del Servidor HTTP (HTTP.SYS)|Probablemente el puerto TCP 80, pero se puede configurar en otros puertos. Para obtener información general, vea [Configurar HTTP y HTTPS](https://go.microsoft.com/fwlink/?LinkId=118373).|Para obtener información específica de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] sobre cómo reservar un punto de conexión HTTP.SYS con HttpCfg.exe, vea [Acerca de las reservas y el registro de reservas de URL &#40;Administrador de configuración de SSRS&#41;](../../reporting-services/install-windows/about-url-reservations-and-registration-ssrs-configuration-manager.md).|  
  
##  <a name="BKMK_port_135"></a> Consideraciones especiales para el puerto 135  
 Cuando utilice RPC con TCP/IP o con UDP/IP como transporte, los puertos entrantes suelen asignarse dinámicamente a los servicios del sistema cuando es necesario; se utilizan los puertos TCP/IP y UDP/IP mayores que el puerto 1024. Se suelen conocer informalmente como "puertos RPC aleatorios". En estos casos, los clientes RPC se apoyan en el mapeador de extremos RPC para indicar qué puertos dinámicos se asignaron al servidor. Para algunos servicios basados en RPC, puede configurar un puerto concreto en lugar de permitir que RPC asigne dinámicamente uno. También puede restringir el intervalo de puertos que RPC asigna dinámicamente a un intervalo pequeño, con independencia del servicio. Dado que el puerto 135 se utiliza para muchos servicios, los usuarios malintencionados lo atacan con frecuencia. Al abrir el puerto 135, considere restringir el ámbito de la regla de firewall.  
  
 Para obtener más información sobre el puerto 135, vea las siguientes referencias:  
  
-   [Introducción al servicio y requisitos del puerto de red para el sistema Windows Server](https://support.microsoft.com/kb/832017)  
  
-   [Cómo solucionar errores del mapeador de extremos de RPC](https://support.microsoft.com/kb/839880)  
  
-   [Llamada a procedimiento remoto (RPC)](https://go.microsoft.com/fwlink/?LinkId=118375)  
  
-   [Configurar la asignación dinámica de puertos RPC para trabajar con firewalls](https://support.microsoft.com/kb/154596/)  
  
##  <a name="BKMK_other_rules"></a> Interacción con otras reglas de firewall  
 El Firewall de Windows utiliza reglas y grupos de reglas para establecer su configuración. Cada regla o grupo de reglas suele estar asociado con un programa o servicio determinado, y ese programa o servicio podría modificar o eliminar esa regla sin su conocimiento. Por ejemplo, los grupos de reglas **World Wide Web Services (HTTP)** y **World Wide Web Services (HTTPS)** están asociados a IIS. Al habilitar esas reglas, se abrirán los puertos 80 y 443, y las características de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que dependen de los puertos 80 y 443 funcionarán si esas reglas están habilitadas. Sin embargo, los administradores que configuran IIS podrían modificar o deshabilitar esas reglas. Por consiguiente, si está utilizando el puerto 80 o el puerto 443 para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], debe crear su propia regla o su propio grupo de reglas que mantenga la configuración de puerto que desee independientemente de las demás reglas IIS.  
  
 El complemento MMC del Firewall de Windows con seguridad avanzada permite cualquier tráfico que coincida con cualquier regla de permiso aplicable. Por lo tanto, si hay dos reglas que se apliquen al puerto 80 (con parámetros diferentes), se permitirá el tráfico que coincida con cualquiera de ellas. Así si una regla permite el tráfico sobre el puerto 80 de la subred local y otra permite el tráfico procedente de cualquier dirección, el efecto de la red será que se permita todo el tráfico dirigido al puerto 80, sin tener en cuenta su origen. Para administrar eficazmente el acceso a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], los administradores deben revisar periódicamente las reglas de firewall habilitadas en el servidor.  
  
##  <a name="BKMK_profiles"></a> Introducción a los perfiles de firewall  
 Los perfiles de firewall se explican en [Guía de introducción del Firewall de Windows con seguridad avanzada](https://go.microsoft.com/fwlink/?LinkId=116080) , en la sección **Firewall de host con reconocimiento de ubicación de red**. En resumen, los sistemas operativos identifican y recuerdan cada una de las redes a las que se conectan con respecto a la conectividad, las conexiones y la categoría.  
  
 Hay tres tipos de ubicación de red en Firewall de Windows con seguridad avanzada:  
  
-   Dominio. Windows puede autenticar el acceso al controlador de dominio para el dominio al que está unido el equipo.  
  
-   Públicas. Excepto las redes de dominio, todas las redes se categorizan inicialmente como públicas. Las redes que representan conexiones directas a Internet o que están en ubicaciones públicas, tales como aeropuertos o cafeterías, deben dejarse como públicas.  
  
-   Privadas. Una red identificada por un usuario o una aplicación como privada. Solo las redes confiables se deben identificar como redes privadas. Es probable que los usuarios deseen identificar las redes domésticas o de pequeña empresa como privadas.  
  
 El administrador puede crear un perfil para cada tipo de ubicación de red, cada perfil conteniendo diferentes directivas de firewall. En cada momento se aplica solamente un perfil. El orden de perfile se aplica de la manera siguiente:  
  
1.  Si todas las interfaces se autentican para el controlador de dominio para el dominio del que es miembro el equipo, se aplica el perfil del dominio.  
  
2.  Si todas las interfaces se autentican para el controlador de dominio o están conectadas a redes clasificadas como ubicaciones de la red privada, se aplica el perfil privado.  
  
3.  De lo contrario, se aplica el perfil público.  
  
 Utilice el complemento MMD de Firewall de Windows con seguridad avanzada para ver y configurar todos los perfiles del firewall. El elemento **Firewall de Windows** del Panel de control solo configura el perfil actual.  
  
##  <a name="BKMK_additional_settings"></a> Configuración adicional de Firewall de Windows con el elemento Firewall de Windows del Panel de control  
 Las excepciones que agregue al firewall pueden restringir la apertura del puerto a las conexiones entrantes de equipos concretos o de la subred local. Esta restricción del ámbito de la apertura del puerto puede reducir la exposición del equipo a usuarios malintencionados, y está recomendada.  
  
> [!NOTE]  
>  El uso del elemento **Firewall de Windows** del Panel de control solamente configura el perfil del firewall actual.  
  
### <a name="to-change-the-scope-of-a-firewall-exception-using-the-windows-firewall-item-in-control-panel"></a>Para cambiar el ámbito de una excepción de firewall utilizando el elemento Firewall de Windows del Panel de control  
  
1.  En el elemento **Firewall de Windows** de Panel de control, seleccione un programa o puerto en la pestaña **Excepciones** y, a continuación, haga clic en **Propiedades** o **Editar**.  
  
2.  En el cuadro de diálogo **Modificar un programa** o **Modificar un puerto** , haga clic en **Cambiar ámbito**.  
  
3.  Elija una de las opciones siguientes:  
  
    -   **Cualquier equipo (incluyendo los que están en Internet)**  
  
         No se recomienda. Esto permitirá que cualquier equipo que pueda direccionar su equipo se conecte al programa o al puerto especificados. Esta configuración puede ser necesaria para permitir que se presente información a usuarios anónimos de Internet, pero aumenta la exposición a los usuarios malintencionados. La exposición puede aumentarse aún más si habilita esta configuración y también permite la exploración transversal de la Traducción de direcciones de red (NAT), como la opción Permitir cruce seguro del perímetro.  
  
    -   **Mi red (subred) solamente**  
  
         Esta configuración de seguridad es más segura que **Cualquier equipo**. Solo los equipos de la subred local de la red pueden conectarse al programa o al puerto.  
  
    -   **Lista personalizada:**  
  
     Solo los equipos que tengan las direcciones IP de la lista se pueden conectar. Esta configuración puede ser más segura que **Sólo mi red (subred)**, pero los equipos cliente que usen DHCP pueden cambiar ocasionalmente su dirección IP. Entonces, el equipo deseado no podrá conectarse. Otro equipo, que no deseara autorizar, podría aceptar la dirección IP de la lista y, en consecuencia, podría conectarse La opción **Lista personalizada** puede ser adecuada para hacer una lista de otros servidores configurados para utilizar una dirección IP fija; no obstante, un intruso podría suplantar las direcciones IP. Las reglas restrictivas de firewall son tan fuertes como sea la infraestructura de red.  
  
##  <a name="BKMK_WF_msc"></a> Utilizar el complemento Firewall de Windows con seguridad avanzada  
 Se pueden configurar opciones de firewall avanzadas adicionales utilizando el complemento MMC del Firewall de Windows con seguridad avanzada. El complemento incluye un asistente de reglas y expone más valores de configuración que no están disponibles en el elemento **Firewall de Windows** en el Panel de control. Entre estas opciones de configuración, se incluyen las siguientes:  
  
-   Configuración de cifrado  
  
-   Restricciones de servicios  
  
-   Restringir conexiones para equipos por nombre  
  
-   Restringir conexiones para usuarios o perfiles específicos  
  
-   Cruce de perímetro que permite que el tráfico evite los enrutadores de Traducción de direcciones de red (NAT)  
  
-   Configurar reglas salientes  
  
-   Configurar reglas de seguridad  
  
-   Requerir IPSec para conexiones entrantes  
  
### <a name="to-create-a-new-firewall-rule-using-the-new-rule-wizard"></a>Para crear una nueva regla de firewall mediante el asistente de Nueva regla  
  
1.  En el menú Inicio, haga clic en **Ejecutar**, escriba **WF.msc**y, a continuación, haga clic en **Aceptar**.  
  
2.  En **Firewall de Windows con seguridad avanzada**, en el panel izquierdo, haga clic con el botón derecho en **Reglas de entrada**y, después, haga clic en **Nueva regla**.  
  
3.  Complete el **Asistente para nueva regla de entrada** usando la configuración que desee.  
  
##  <a name="BKMK_troubleshooting"></a> Solucionar problemas de configuración del firewall  
 Las herramientas y técnicas siguientes pueden ser útiles para solucionar problemas del firewall:  
  
-   El estado efectivo del puerto es la unión de todas las reglas relacionadas con el puerto. Cuando intente bloquear el acceso a través de un puerto, puede ser útil para revisar todas las reglas que citan el número de puerto. Para ello, utilice el complemento MMC del Firewall de Windows con seguridad avanzada y ordene las reglas entrantes y salientes por número de puerto.  
  
-   Revise los puertos activos en el equipo en el que se esté ejecutando [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Este proceso de revisión incluye la comprobación de qué puertos TCP/IP están escuchando y también la comprobación del estado de los puertos.  
  
     Para comprobar qué puertos están escuchando, use la utilidad de línea de comandos **netstat** . Además de mostrar las conexiones TCP activas, la utilidad **netstat** también muestra diversa información y estadísticas de IP.  
  
    #### <a name="to-list-which-tcpip-ports-are-listening"></a>Para mostrar qué puertos TCP/IP están escuchando  
  
    1.  Abra la ventana de símbolo del sistema.  
  
    2.  En el símbolo del sistema, escriba **netstat -n -a**.  
  
         El modificador **-n** indica a **netstat** que muestre numéricamente la dirección y el número de puerto de las conexiones TCP activas. El modificador **-a** indica a **netstat** que muestre los puertos TCP y UDP en los que está escuchando el equipo.  
  
-   La utilidad **PortQry** se puede usar para notificar el estado de los puertos TCP/IP para indicar que están escuchando, no escuchando o filtrados. (Con un estado de filtrado, el puerto puede o no estar escuchando; este estado indica que la utilidad no ha recibido una respuesta del puerto.) La utilidad **PortQry** se puede descargar desde el [Centro de descargas de Microsoft](https://go.microsoft.com/fwlink/?LinkId=28590).  
  
## <a name="see-also"></a>Consulte también  
 [Introducción al servicio y requisitos del puerto de red para el sistema Windows Server](https://support.microsoft.com/kb/832017)   
 [Cómo: Configurar los valores del firewall (Azure SQL Database)](https://azure.microsoft.com/documentation/articles/sql-database-configure-firewall-settings/)  
  
  
