---
title: Configurar el Firewall de Windows para permitir el acceso a Analysis Services | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- ports [Analysis Services]
- Windows Firewall [Analysis Services]
- firewall systems [Analysis Services]
ms.assetid: 7673acc5-75f0-4703-9ce2-87425ea39d49
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: ac7570550cd256a5c65c82c9585b2baf7713c878
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "66080273"
---
# <a name="configure-the-windows-firewall-to-allow-analysis-services-access"></a>Configurar Firewall de Windows para permitir el acceso a Analysis Services
  Un primer paso esencial para hacer que [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] o [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] esté disponible en la red consiste en determinar si es necesario desbloquear puertos en un firewall. La mayoría de las instalaciones necesitarán que cree al menos una regla de firewall de entrada que permita las conexiones a [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)].  
  
 Los requisitos de configuración del firewall varían según cómo instalara [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)].  
  
-   Abra el puerto TCP 2383 al instalar una instancia predeterminada o crear un clúster de conmutación por error de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] .  
  
-   Abra el puerto TCP 2382 al instalar una instancia con nombre. Las instancias con nombre usan asignaciones de puerto dinámicas. Igual que el servicio de detección de Analysis Services, el servicio SQL Server Browser escucha en el puerto TCP 2382 y redirige la solicitud de conexión al puerto utilizado actualmente por [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)].  
  
-   Abra el puerto TCP 2382 al instalar [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] en modo de SharePoint para admitir [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] 2013. En [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] 2013, la instancia de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] es externa para SharePoint. Las solicitudes de entrada a la instancia con nombre 'PowerPivot' se originan en aplicaciones web de SharePoint a través de una conexión de red, lo que requiere un puerto abierto. Como ocurre con otras instancias con nombre de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] , cree una regla de entrada para el servicio SQL Server Browser en el puerto TCP 2382 para permitir el acceso a [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)].  
  
-   En [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] 2010, no abra puertos en Firewall de Windows. Como complemento de SharePoint, el servicio usa los puertos configurados para SharePoint y solo realiza conexiones locales a la instancia de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] que carga y consulta modelos de datos de [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] .  
  
-   Para las instancias de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] que se ejecutan en Máquinas virtuales de Windows Azure, use otras instrucciones alternativas para configurar el acceso al servidor. Vea [Business Intelligence de SQL Server en Máquinas virtuales de Windows Azure](https://msdn.microsoft.com/library/windowsazure/jj992719.aspx).  
  
 Aunque la instancia predeterminada de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] escucha en el puerto TCP 2383, puede configurar el servidor para que escuche en otro puerto fijo, conectándose al servidor en este formato: \<nombreDeServidor >:\<portnumber >.  
  
 Una instancia de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] solo puede utilizar un puerto TCP. En los equipos que tienen varias tarjetas de red o varias direcciones IP, [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] escucha en un puerto TCP para todas las direcciones IP asignadas o con alias en el equipo. Si tiene requisitos específicos de varios puertos, considere la posibilidad de configurar [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] para el acceso HTTP. Después puede configurar varios extremos HTTP en los puertos que elija. Vea [Configurar el acceso HTTP a Analysis Services en Internet Information Services &#40;IIS&#41; 8.0](configure-http-access-to-analysis-services-on-iis-8-0.md).  
  
 Este tema contiene las siguientes secciones:  
  
-   [Comprobar la configuración de puertos y del firewall para Analysis Services](#bkmk_checkport)  
  
-   [Configurar Firewall de Windows para una instancia predeterminada de Analysis Services](#bkmk_default)  
  
-   [Configurar el acceso de Firewall de Windows para una instancia con nombre de Analysis Services](#bkmk_named)  
  
-   [Configuración de puertos para un clúster de Analysis Services](#bkmk_cluster)  
  
-   [Configuración de puerto de PowerPivot para SharePoint](#bkmk_powerpivot)  
  
-   [Utilizar un puerto fijo para una instancia predeterminada o con nombre de Analysis Services](#bkmk_fixed)  
  
 Para obtener más información sobre la configuración predeterminada de Firewall de Windows y una descripción de los puertos TCP que afectan al motor de base de datos, Analysis Services, Reporting Services e Integration Services, vea [Configurar Firewall de Windows para permitir el acceso a SQL Server](../../sql-server/install/configure-the-windows-firewall-to-allow-sql-server-access.md).  
  
##  <a name="bkmk_checkport"></a> Comprobar la configuración de puertos y del firewall para Analysis Services  
 En los sistemas operativos Microsoft Windows compatibles con [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], Firewall de Windows está activado de forma predeterminada y bloquea las conexiones remotas. Debe abrir manualmente un puerto en el firewall para permitir las solicitudes de entrada en Analysis Services. El programa de instalación de SQL Server no realiza este paso automáticamente.  
  
 La configuración de puertos se especifica en el archivo msmdsrv.ini y en la página Propiedades generales de una instancia de Analysis Services en SQL Server Management Studio. Si `Port` está establecido en un entero positivo, el servicio está escuchando en un puerto fijo. Si `Port` está establecido en 0, el servicio está escuchando en el puerto 2383 si es la instancia predeterminada o en un puerto asignado dinámicamente si es una instancia con nombre.  
  
 Las asignaciones dinámicas de puerto solo las usan las instancias con nombre. El servicio `MSOLAP$InstanceName` determina qué puerto utilizará cuando se inicie. Puede determinar el número de puerto real en uso por una instancia con nombre haciendo lo siguiente:  
  
-   Inicie el Administrador de tareas y, a continuación, haga clic en **servicios** para obtener el PID de la `MSOLAP$InstanceName`.  
  
-   Ejecute `netstat -ao -p TCP` desde la línea de comandos para ver la información del puerto TCP para ese PID.  
  
-   Compruebe el puerto con SQL Server Management Studio y conéctese a un servidor de Analysis Services en este formato: \<Dirección IP >:\<portnumber >.  
  
 Aunque una aplicación podría estar escuchando en un puerto concreto, las conexiones no tendrán éxito si un firewall está bloqueando el acceso. Para que las conexiones alcancen una instancia con nombre de Analysis Services, debe desbloquear el acceso a msmdsrv.exe o al puerto fijo en el que está escuchando en el firewall. En las secciones restantes de este tema se proporcionan instrucciones para hacerlo.  
  
 Para comprobar si la configuración del firewall ya está definida para Analysis Services, utilice Firewall de Windows con seguridad avanzada en el Panel de control. La página Firewall de la carpeta Supervisión muestra una lista completa de las reglas definidas para el servidor local.  
  
 Tenga en cuenta que para [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)], todas las reglas de firewall debe definirse manualmente. Aunque [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] y SQL Server Browser reservan los puertos 2382 y 2383, ni el programa de instalación de SQL Server ni ninguna de las herramientas de configuración definen reglas de firewall que permitan el acceso a los puertos o los archivos ejecutables del programa.  
  
##  <a name="bkmk_default"></a> Configurar Firewall de Windows para una instancia predeterminada de Analysis Services  
 La instancia predeterminada de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] escucha en el puerto TCP 2383. Si instaló la instancia predeterminada y desea usar este puerto, solo tiene que desbloquear el acceso de entrada al puerto TCP 2383 en Firewall de Windows para habilitar el acceso remoto a la instancia predeterminada de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]. Si instaló la instancia predeterminada pero desea configurar el servicio para que escuche en un puerto fijo, vea [Utilizar un puerto fijo para una instancia predeterminada o con nombre de Analysis Services](#bkmk_fixed) en este tema.  
  
 Para comprobar si el servicio se está ejecutando como la instancia predeterminada (MSSQLServerOLAPService), compruebe el nombre del servicio en el Administrador de configuración de SQL Server. Una instancia predeterminada de Analysis Services siempre se muestra como **SQL Server Analysis Services (MSSQLSERVER)** .  
  
> [!NOTE]  
>  Los distintos sistemas operativos Windows proporcionan herramientas alternativas para configurar Firewall de Windows. La mayoría de estas herramientas le permiten elegir entre abrir un puerto o un programa ejecutable concreto. A menos que tenga una razón para especificar el programa ejecutable, recomendamos que especifique el puerto.  
  
 Al especificar una regla de entrada, asegúrese de adoptar una convención de nomenclatura que le permita encontrar fácilmente las reglas más adelante, por ejemplo, **SQL Server Analysis Services (TCP-entrada) 2383**.  
  
#### <a name="windows-firewall-with-advanced-security"></a>Firewall de Windows con seguridad avanzada  
  
1.  En Windows 7 o Windows Vista, en el Panel de control, haga clic en **Sistema y seguridad**, seleccione **Firewall de Windows**y haga clic en **Configuración avanzada**. En Windows Server 2008 o 2008 R2, abra Herramientas administrativas y haga clic en **Firewall de Windows con seguridad avanzada**. En Windows Server 2012, abra la página Aplicaciones y escriba **Firewall de Windows**.  
  
2.  Haga clic con el botón derecho en **Reglas de entrada** y seleccione **Nueva regla**.  
  
3.  En el tipo de regla, haga clic en `Port` y, a continuación, haga clic en **siguiente**.  
  
4.  En protocolo y puertos, seleccione **TCP** y, a continuación, escriba `2383` en **puertos locales específicos**.  
  
5.  En Acción, haga clic en **Permitir la conexión** y, después, haga clic en **Siguiente**.  
  
6.  En Perfil, borre cualquier ubicación de red que no sea aplicable y haga clic en **Siguiente**.  
  
7.  En nombre, escriba un nombre descriptivo para esta regla (por ejemplo, `SQL Server Analysis Services (tcp-in) 2383`) y, a continuación, haga clic en **finalizar**.  
  
8.  Para comprobar que las conexiones remotas están habilitadas, abra SQL Server Management Studio o Excel en un equipo diferente y conéctese a [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] especificando el nombre de red del servidor en **Nombre de servidor**.  
  
    > [!NOTE]  
    >  Otros usuarios no tendrán acceso a este servidor hasta que les conceda permisos. Para obtener más información, vea [Cómo autorizar el acceso a objetos y operaciones &#40;Analysis Services&#41;](../multidimensional-models/authorizing-access-to-objects-and-operations-analysis-services.md).  
  
#### <a name="netsh-advfirewall-syntax"></a>Sintaxis de Netsh AdvFirewall  
  
-   El siguiente comando crea una regla de entrada que permite solicitudes entrantes en el puerto TCP 2383.  
  
    ```  
    netsh advfirewall firewall add rule name="SQL Server Analysis Services inbound on TCP 2383" dir=in action=allow protocol=TCP localport=2383 profile=domain  
    ```  
  
##  <a name="bkmk_named"></a> Configurar el acceso de Firewall de Windows para una instancia con nombre de Analysis Services  
 Las instancias con nombre de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] pueden escuchar en un puerto fijo o en un puerto asignado dinámicamente, donde el servicio SQL Server Browser proporciona información de la conexión actual para el servicio en el momento de la conexión.  
  
 El servicio SQL Server Browser escucha en el puerto TCP 2382. No se usa UDP. TCP es el único protocolo de transmisión que usa [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)].  
  
 Elija uno de los siguientes métodos para habilitar el acceso remoto a una instancia con nombre de Analysis Services:  
  
-   Use asignaciones dinámicas de puertos y el servicio SQL Server Browser. Desbloquee el puerto utilizado por el servicio SQL Server Browser en Firewall de Windows. Conectarse al servidor en este formato: \<servername >\\< nombreDeInstancia\>.  
  
-   Use un puerto fijo y el servicio SQL Server Browser conjuntamente. Este enfoque le permite conectarse con este formato: \<servername >\\< instancename\>, idéntico al enfoque de asignación de puertos dinámicos, excepto que en este caso, el servidor escucha en un puerto fijo. En este escenario, el Servicio SQL Server Browser proporciona la resolución de nombres a la instancia de Analysis Services que escucha en el puerto fijo. Para usar este método, configure el servidor para que escuche en un puerto fijo y desbloquee el acceso a dicho puerto y al puerto utilizado por el servicio SQL Server Browser.  
  
 El servicio SQL Server Browser solo se usa con instancias con nombre, nunca con la instancia predeterminada. El servicio se instala y habilita de modo automático siempre que se instala una característica de SQL Server como una instancia con nombre. Si elige un método que requiera el servicio SQL Server Browser, asegúrese de que permanece habilitado e iniciado en el servidor.  
  
 Si no puede utilizar el servicio SQL Server Browser, debe asignar un puerto fijo en la cadena de conexión, omitiendo la resolución de nombres de dominio. Sin el servicio SQL Server Browser, todas las conexiones de cliente deben incluir el número de puerto en la cadena de conexión (por ejemplo, AW-SRV01:54321).  
  
 **Opción 1: Usar asignaciones dinámicas de puerto y desbloquear el acceso al servicio de SQL Server Browser**  
  
 `MSOLAP$InstanceName` establece las asignaciones dinámicas de puerto para las instancias con nombre de Analysis Services cuando se inicia el servicio. De forma predeterminada, el servicio reclama el primer número de puerto disponible que encuentra, utilizando un número de puerto diferente cada vez que se reinicia el servicio.  
  
 El servicio SQL Server Browser administra la resolución de nombres de instancia. Siempre es necesario desbloquear el puerto TCP 2382 para el servicio SQL Server Browser en el caso de que se usen asignaciones dinámicas de puerto con una instancia con nombre.  
  
> [!NOTE]  
>  El servicio SQL Server Browser escucha en el puerto UDP 1434 y en el puerto TCP 2382 para el Motor de base de datos y Analysis Services, respectivamente. Aunque ya desbloqueara el puerto UDP 1434 para el servicio SQL Server Browser, debe seguir desbloqueando el puerto TCP 2382 para Analysis Services.  
  
#### <a name="windows-firewall-with-advanced-security"></a>Firewall de Windows con seguridad avanzada  
  
1.  En Windows 7 o Windows Vista, en el Panel de control, haga clic en **Sistema y seguridad**, seleccione **Firewall de Windows**y haga clic en **Configuración avanzada**. En Windows Server 2008 o 2008 R2, abra Herramientas administrativas y haga clic en **Firewall de Windows con seguridad avanzada**. En Windows Server 2012, abra la página Aplicaciones y escriba **Firewall de Windows**.  
  
2.  Para desbloquear el acceso al servicio SQL Server Browser, haga clic con el botón derecho en **Reglas de entrada** y seleccione **Nueva regla**.  
  
3.  En el tipo de regla, haga clic en `Port` y, a continuación, haga clic en **siguiente**.  
  
4.  En protocolo y puertos, seleccione **TCP** y, a continuación, escriba `2382` en **puertos locales específicos**.  
  
5.  En Acción, haga clic en **Permitir la conexión** y, después, haga clic en **Siguiente**.  
  
6.  En Perfil, borre cualquier ubicación de red que no sea aplicable y haga clic en **Siguiente**.  
  
7.  En nombre, escriba un nombre descriptivo para esta regla (por ejemplo, `SQL Server Browser Service (tcp-in) 2382`) y, a continuación, haga clic en **finalizar**.  
  
8.  Para comprobar que las conexiones remotas están habilitadas, abra SQL Server Management Studio o Excel en un equipo diferente y conéctese a Analysis Services especificando el nombre de red del servidor y el nombre de instancia en este formato: \<servername > \\< nombreDeInstancia\>. Por ejemplo, en un servidor denominado **AW-SRV01** con una instancia con nombre denominada **Finanzas**, el nombre del servidor es **AW-SRV01\Finanzas**.  
  
 **Opción 2: Configurar un puerto fijo para una instancia con nombre**  
  
 O bien, puede asignar un puerto fijo y, a continuación, desbloquear el acceso a dicho puerto. Este método proporciona una capacidad de auditoría mejor que si se permite el acceso al programa ejecutable. Por eso, se recomienda utilizar un puerto fijo para acceder a una instancia de Analysis Services.  
  
 Para asignar un puerto fijo, siga las instrucciones de [Utilizar un puerto fijo para una instancia predeterminada o con nombre de Analysis Services](#bkmk_fixed) en este tema y vuelva a esta sección para desbloquear el puerto.  
  
#### <a name="windows-firewall-with-advanced-security"></a>Firewall de Windows con seguridad avanzada  
  
1.  En Windows 7 o Windows Vista, en el Panel de control, haga clic en **Sistema y seguridad**, seleccione **Firewall de Windows**y haga clic en **Configuración avanzada**. En Windows Server 2008 o 2008 R2, abra Herramientas administrativas y haga clic en **Firewall de Windows con seguridad avanzada**. En Windows Server 2012, abra la página Aplicaciones y escriba **Firewall de Windows**.  
  
2.  Para desbloquear el acceso a Analysis Services, haga clic con el botón derecho en **Reglas de entrada** y seleccione **Nueva regla**.  
  
3.  En el tipo de regla, haga clic en `Port` y, a continuación, haga clic en **siguiente**.  
  
4.  En Protocolo y puertos, seleccione **TCP** y escriba el puerto fijo en **Puertos locales específicos**.  
  
5.  En Acción, haga clic en **Permitir la conexión** y, después, haga clic en **Siguiente**.  
  
6.  En Perfil, borre cualquier ubicación de red que no sea aplicable y haga clic en **Siguiente**.  
  
7.  En nombre, escriba un nombre descriptivo para esta regla (por ejemplo, `SQL Server Analysis Services on port 54321`) y, a continuación, haga clic en **finalizar**.  
  
8.  Para comprobar que las conexiones remotas están habilitadas, abra SQL Server Management Studio o Excel en un equipo diferente y conéctese a Analysis Services especificando el nombre de red del servidor y el número de puerto en este formato: \<nombreDeServidor >: \<portnumber >.  
  
#### <a name="netsh-advfirewall-syntax"></a>Sintaxis de Netsh AdvFirewall  
  
-   Los siguientes comandos crean reglas de entrada que desbloquean el puerto TCP 2382 para el servicio SQL Server Browser y desbloquean el puerto fijo que especificó para la instancia de Analysis Services. Puede ejecutar cualquiera de los comandos siguientes para permitir el acceso a una instancia con nombre de Analysis Services.  
  
     En este comando de ejemplo, el puerto 54321 es el puerto fijo. Asegúrese de reemplazarlo con el puerto real en uso en el sistema.  
  
    ```  
    netsh advfirewall firewall add rule name="SQL Server Analysis Services (tcp-in) on 54321" dir=in action=allow protocol=TCP localport=54321 profile=domain  
    ```  
  
    ```  
    netsh advfirewall firewall add rule name="SQL Server Browser Services inbound on TCP 2382" dir=in action=allow protocol=TCP localport=2382 profile=domain  
    ```  
  
##  <a name="bkmk_fixed"></a> Utilizar un puerto fijo para una instancia predeterminada o con nombre de Analysis Services  
 En esta sección se explica cómo configurar Analysis Services para escuchar en un puerto fijo. El uso de un puerto fijo es habitual si se instala Analysis Services como una instancia con nombre, pero también puede usar este método si los requisitos de seguridad o de la empresa especifican que se usen asignaciones de puertos no predeterminadas.  
  
 Tenga en cuenta que el uso de un puerto fijo modificará la sintaxis de conexión para la instancia predeterminada exigiéndole anexar el número de puerto al nombre del servidor. Por ejemplo, la conexión a una instancia predeterminada local de Analysis Services que escucha en el puerto 54321 en SQL Server Management Studio requeriría escribir localhost:54321 como nombre del servidor en el cuadro de diálogo Conectar con el servidor en Management Studio.  
  
 Si usa una instancia con nombre, puede asignar un puerto fijo sin cambios cómo se especifica el nombre del servidor (en concreto, puede usar \<nombreDeServidor\nombreDeInstancia > para conectarse a una instancia con nombre escucha en un puerto fijo). Esto solo funciona si se está ejecutando el servicio SQL Server Browser y se desbloquea el puerto en el que escucha. Servicio SQL Server Browser proporcionará la redirección al puerto fijo según \<nombreDeServidor\nombreDeInstancia >. Siempre y cuando abra puertos para el servicio SQL Server Browser y para la instancia con nombre de Analysis Services que escucha en el puerto fijo, el servicio SQL Server Browser resolverá la conexión con una instancia con nombre.  
  
1.  Determine un puerto TCP/IP disponible para su uso.  
  
     Para ver una lista de los puertos reservados y registrados cuyo uso debe evitar, vea la página dedicada a los [números de puerto (IANA)](https://go.microsoft.com/fwlink/?LinkID=198469). Para ver una lista de los puertos que ya están en uso en el sistema, abra una ventana de símbolo del sistema y escriba `netstat -a -p TCP` para mostrar una lista de los puertos TCP que están abiertos en el sistema.  
  
2.  Después de determinar qué puerto va a usar, especifique el puerto modificando el valor de configuración de `Port` en el archivo msmdsrv.ini o en la página Propiedades generales de una instancia de Analysis Services en SQL Server Management Studio.  
  
3.  Reiniciar el servicio.  
  
4.  Configure Firewall de Windows para desbloquear el puerto TCP que especificó. O bien, si está utilizando un puerto fijo para una instancia con nombre, desbloquee el puerto TCP que especificó para esa instancia y también el puerto TCP 2382 para el servicio SQL Server Browser.  
  
5.  Haga la comprobación conectando localmente (en Management Studio) y después remotamente, desde una aplicación cliente de otro equipo. Para usar Management Studio, conectarse a una instancia predeterminada de Analysis Services especificando un nombre de servidor en este formato: \<nombreDeServidor >:\<portnumber >. Para una instancia con nombre, especifique el nombre del servidor como \<servername >\\< nombreDeInstancia\>.  
  
##  <a name="bkmk_cluster"></a> Configuración de puertos para un clúster de Analysis Services  
 Un clúster de conmutación por error de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] siempre escucha en el puerto TCP 2383, independientemente de si se ha instalado como una instancia predeterminada o como una instancia con nombre. [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] no usa asignaciones dinámicas de puerto cuando se instala en un clúster de conmutación por error de Windows. Asegúrese de abrir el puerto TCP 2383 en todos los nodos que ejecuten [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] en el clúster. Para obtener más información acerca de cómo organizar en clúster [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)], vea [Organizar en clúster SQL Server Analysis Services](https://go.microsoft.com/fwlink/p/?LinkId=396548).  
  
##  <a name="bkmk_powerpivot"></a> Configuración de puerto de PowerPivot para SharePoint  
 La arquitectura del servidor para [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] es diferente según la versión de SharePoint que se está utilizando.  
  
 **SharePoint 2013**  
  
 En SharePoint 2013, Excel Services redirige las solicitudes para los modelos de datos de Power Pivot, que se cargan en una instancia de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] fuera del entorno de SharePoint. Las conexiones siguen el patrón típico, donde una biblioteca de cliente de Analysis Services de un equipo local envía una solicitud de conexión a una instancia remota de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] de la misma red.  
  
 Puesto que [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] siempre instala [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] como una instancia con nombre, debe suponer que se usan el servicio SQL Server Browser y asignaciones de puerto dinámicas. Como se ha indicado anteriormente, el servicio SQL Server Browser escucha en el puerto TCP 2382 las solicitudes de conexión enviadas a instancias con nombre de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] , redirigiendo la solicitud al puerto actual.  
  
 Tenga en cuenta que Excel Services en SharePoint 2013 no admite la sintaxis fija de conexión de puerto, por lo que debe asegurarse de que el servicio SQL Server Browser es accesible.  
  
 **SharePoint 2010**  
  
 Si está usando SharePoint 2010, no necesita abrir puertos en Firewall de Windows. SharePoint abre los puertos que necesita, y los complementos como PowerPivot para SharePoint se ejecutan dentro del entorno de SharePoint. En una instalación de PowerPivot para SharePoint 2010, el Servicio de sistema de PowerPivot tiene uso exclusivo de la instancia de servicio local de SQL Server Analysis Services (PowerPivot) que se instala con él en el mismo equipo. Utiliza conexiones locales, no conexiones de red, para tener acceso al servicio de motor local de Analysis Services que carga, consulta y procesa datos PowerPivot en el servidor de SharePoint. Para solicitar datos PowerPivot desde aplicaciones cliente, las solicitudes se enrutan a través de puertos abiertos por el programa de instalación de SharePoint (en concreto, se definen las reglas de entrada para permitir el acceso a SharePoint - 80, Administración Central de SharePoint v4, SharePoint Web Services y SPUserCodeV4). Puesto que los servicios web PowerPivot se ejecutan dentro de una granja de servidores de SharePoint, las reglas de firewall de SharePoint son suficientes para el acceso remoto a datos PowerPivot en una granja de servidores de SharePoint.  
  
## <a name="see-also"></a>Vea también  
 [Servicio SQL Server Browser &#40;motor de base de datos y SSAS&#41;](../../database-engine/configure-windows/sql-server-browser-service-database-engine-and-ssas.md)   
 [Iniciar, detener, pausar, reanudar y reiniciar el motor de base de datos, Agente SQL Server o el Servicio SQL Server Browser](../../database-engine/configure-windows/start-stop-pause-resume-restart-sql-server-services.md)   
 [Configurar Firewall de Windows para el acceso al motor de base de datos](../../database-engine/configure-windows/configure-a-windows-firewall-for-database-engine-access.md)  
  
  
