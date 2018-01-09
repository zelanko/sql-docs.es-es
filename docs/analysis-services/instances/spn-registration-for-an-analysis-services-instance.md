---
title: Registro de SPN para una instancia de Analysis Services | Documentos de Microsoft
ms.custom: 
ms.date: 03/14/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: data-mining
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 9e78dc37-a3f0-415d-847c-32fec69efa8c
caps.latest.revision: "16"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: On Demand
ms.openlocfilehash: ecb1a5b33ede8c99150fd8b3ce1cf9babdb1f519
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 01/08/2018
---
# <a name="spn-registration-for-an-analysis-services-instance"></a>Registro de SPN para una instancia de Analysis Services
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]Un nombre principal de servicio (SPN) identifica de forma única una instancia de servicio en un dominio de Active Directory cuando se usa Kerberos para autenticar mutuamente las identidades de cliente y el servicio. Un SPN está asociado a la cuenta de inicio de sesión bajo la que se ejecuta la instancia del servicio.  
  
 Para las aplicaciones cliente que se conectan a Analysis Services a través de la autenticación Kerberos, las bibliotecas de cliente de Analysis Services crean un SPN con el nombre de host de la cadena de conexión y otras variables conocidas, como la clase de servicio, que son fijas en cualquier versión determinada de Analysis Services.  
  
 Para que se realice la autenticación mutua, los SPN generados por el cliente deben coincidir con un objeto de SPN correspondiente de un controlador de dominio (DC) de Active Directory. Esto significa que puede ser necesario registrar varios SPN para que una sola instancia de Analysis Services abarque todas las formas en las que un usuario puede especificar el nombre de host en una cadena de conexión. Por ejemplo, probablemente necesite dos SPN para controlar tanto el nombre de dominio completo (FQDN) de un servidor como el nombre corto de equipo. Es fundamental registrar correctamente el SPN de Analysis Services para que una conexión se realice correctamente. Si el SPN no existe, es incorrecto o está duplicado, se producirá un error en la conexión.  
  
 El registro de SPN suele ser una tarea manual que realiza el administrador de Analysis Services. A diferencia del motor de base de datos de SQL Server, Analysis Services nunca registra automáticamente su SPN durante el inicio del servicio. Es necesario realizar el registro manual cuando Analysis Services se ejecuta en una cuenta virtual predeterminada, una cuenta de usuario de dominio o una cuenta integrada, lo cual incluye un SID por servicio.  
  
 El registro de SPN no es necesario si el servicio se ejecuta con una cuenta de servicio administrada predefinida que un administrador de dominio ha creado. Tenga en cuenta que según el nivel funcional del dominio, para registrar un SPN puede ser necesario tener permisos de administrador de dominio.  
  
> [!TIP]  
>  **[!INCLUDE[msCoName](../../includes/msconame-md.md)] Administrador de configuración de Kerberos para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]** es una herramienta de diagnóstico que sirve para solucionar problemas de conectividad de Kerberos relacionados con [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Para obtener más información, vea [Administrador de configuración de Microsoft Kerberos para SQL Server](http://www.microsoft.com/download/details.aspx?id=39046).  
  
 Este tema contiene las siguientes secciones:  
  
 [Cuándo se necesita un registro de SPN](#bkmk_scnearios)  
  
 [Formato de SPN para Analysis Services](#bkmk_SPNSyntax)  
  
 [Registro de SPN para una cuenta virtual](#bkmk_virtual)  
  
 [Registro de SPN para una cuenta de dominio](#bkmk_domain)  
  
 [Registro de SPN para una cuenta integrada](#bkmk_builtin)  
  
 [Registro de SPN para una instancia con nombre](#bkmk_spnNamed)  
  
 [Registro de SPN para un clúster de SSAS](#bkmk_spnCluster)  
  
 [Registro de SPN para instancias de SSAS configuradas para acceso HTTP](#bkmk_spnHTTP)  
  
 [Registro de SPN para instancias de SSAS que escuchan en varios puertos fijos](#bkmk_spnFixedPorts)  
  
##  <a name="bkmk_scnearios"></a> Cuándo se necesita un registro de SPN  
 Las conexiones de cliente que especifican "SSPI=Kerberos" en la cadena de conexión necesitarán el registro de SPN para una instancia de Analysis Services.  
  
 El registro de SPN es necesario en las siguientes circunstancias. Para obtener información más detallada, vea [Configure Analysis Services for Kerberos constrained delegation](../../analysis-services/instances/configure-analysis-services-for-kerberos-constrained-delegation.md).  
  
-   La delegación de identidad es necesaria para que la identidad del usuario fluya de la aplicación cliente o del servicio de nivel intermedio a Analysis Services. La delegación de identidad se usa normalmente cuando se han definido permisos o filtros por usuario en objetos concretos.  
  
     Un escenario común que implica la delegación de identidad es la configuración de los servicios de nivel intermedio, como Servicios de Excel o Reporting Services, para la delegación restringida con el fin de representar la identidad de un usuario cuando se recuperan datos en Analysis Services. Para admitir este comportamiento, debe proporcionar un SPN de Analysis Services como servicio de destino al configurar los Servicios de Excel o Reporting Services para la delegación restringida.  
  
-   Analysis Services delega una identidad de usuario al recuperar datos de una base de datos relacional de SQL Server en el caso de bases de datos tabulares que usan el modo DirectQuery. Este es el único escenario en el que Analysis Services suplantará la identidad del usuario para otro servicio.  
  
##  <a name="bkmk_SPNSyntax"></a> Formato de SPN para Analysis Services  
 Use **setspn** para registrar un SPN. En los sistemas operativos más recientes, **setspn** se instala como una utilidad del sistema. Para obtener más información, vea [SetSPN](http://technet.microsoft.com/library/cc731241\(WS.10\).aspx).  
  
 En la tabla siguiente se describen la distintas partes de un SPN de Analysis Services.  
  
|Elemento|Description|  
|-------------|-----------------|  
|Clase de servicio|MSOLAPSvc.3 identifica el servicio como una instancia de Analysis Services. .3 es una referencia a la versión del protocolo XMLA sobre TCP/IP usado en las transmisiones de Analysis Services. No está relacionado con la versión del producto. Por tanto, MSOLAPSvc.3 es la clase de servicio correcta para SQL Server 2005, 2008, 2008 R2, 2012 y cualquier versión futura de Analysis Services hasta que se revise el propio protocolo.|  
|Nombre de host|Identifica el equipo en el que se está ejecutando el servicio. Puede ser un nombre de dominio completo o un nombre NetBIOS. Se debe registrar un SPN para ambos.<br /><br /> Al registrar un SPN para el nombre NetBIOS de un servidor, asegúrese de usar `SetupSPN –S` para comprobar si se produce un registro duplicado. No se garantiza que los nombres NetBIOS sean únicos en un bosque y la existencia de un registro de SPN duplicado producirá errores de conexión.<br /><br /> Para los clústeres de carga equilibrada de Analysis Services, el nombre de host debe ser el nombre virtual asignado al clúster.<br /><br /> No cree nunca un SPN con la dirección IP. Kerberos emplea las capacidades de resolución de DNS del dominio. Al especificar una dirección IP se elude esa capacidad.|  
|Número de puerto|Aunque el número de puerto forma parte de la sintaxis de SPN, no especifique nunca un número de puerto al registrar un SPN de Analysis Services. Analysis Services suele usar el carácter de dos puntos (:) para proporcionar un número de puerto en la sintaxis estándar de SPN, con el fin de especificar el nombre de instancia. En el caso de una instancia de Analysis Services, se supone que el puerto será el puerto predeterminado (TCP 2383) o un puerto asignado por el servicio SQL Server Browser (TCP 2382).|  
|Nombre de instancia|Analysis Services es un servicio replicable que se puede instalar varias veces en el mismo equipo. Cada instancia se identifica mediante su nombre de instancia.<br /><br /> El nombre de instancia tiene como prefijo un carácter de dos puntos (:). Por ejemplo, dado un equipo host con el nombre SRV01 y una instancia con el nombre SSAS-Tabular, el SPN debe ser SRV01:SSAS-Tabular.<br /><br /> Observe que la sintaxis para especificar una instancia con nombre de Analysis Services es distinta de la que usan otras instancias de SQL Server. Otros servicios usan una barra diagonal inversa (\) para anexar el nombre de instancia en un SPN.|  
|Cuenta de servicio|Es la cuenta de inicio del servicio **MSSQLServerOLAPService** de Windows. Puede ser una cuenta de usuario de dominio de Windows, una cuenta virtual, una cuenta de servicio administrada o una cuenta integrada, como un SID por servicio, NetworkService o LocalSystem. Una cuenta de usuario de dominio de Windows puede tener el formato dominio ombre de usuario o user@domain.|  
  
##  <a name="bkmk_virtual"></a> Registro de SPN para una cuenta virtual  
 Las cuentas virtuales son el tipo de cuenta predeterminado de los servicios de SQL Server. La cuenta virtual es **nt\msolapservice** para una instancia predeterminada y **servicio nt\msolap $**\<nombre de instancia > para una instancia con nombre.  
  
 Como implica el nombre, estas cuentas no existen en Active Directory. Una cuenta virtual solo existe en el equipo local. Cuando se conecta a servicios, aplicaciones o dispositivos externos, la conexión se realiza mediante la cuenta de equipo local. Por esta razón, un registro de SPN para Analysis Services en ejecución en una cuenta virtual es realmente un registro de SPN para la cuenta de equipo.  
  
 **Sintaxis de ejemplo para una instancia predeterminada que se ejecuta como Servicio NT\MSOLAPService**  
  
 En este ejemplo se muestra la sintaxis de **setspn** para la instancia predeterminada de Analysis Services en ejecución en la cuenta virtual predeterminada. En este ejemplo, el nombre de host del equipo es **AW-SRV01**. Tal y como se indicó, el registro de SPN debe especificar la *cuenta de equipo* en lugar de la cuenta virtual, **NT Service\MSOLAPService**.  
  
```  
Setspn -s MSOLAPSvc.3/AW-SRV01.AdventureWorks.com AW-SRV01  
```  
  
> [!NOTE]  
>  Recuerde crear dos registros de SPN, uno para el nombre de host de NetBIOS y otro para el nombre de dominio completo del host. Las diferentes aplicaciones cliente utilizan distintas convenciones de nombre de host cuando se conectan a Analysis Services. El uso de dos registros de SPN asegura que se tienen en cuenta ambas versiones del nombre de host.  
  
 **Sintaxis de ejemplo para una instancia con nombre que se ejecuta como servicio nt\msolap$\<nombre de instancia >**  
  
 En este ejemplo se muestra la sintaxis de **setspn** para una instancia con nombre en ejecución en la cuenta virtual predeterminada. En este ejemplo, el nombre de host del equipo es **AW-SRV02** y el nombre de instancia es **AW-FINANCE**. De nuevo, es la cuenta de equipo que se especifica para el SPN, en lugar de la cuenta virtual **servicio nt\msolap $**\<nombre de instancia >.  
  
```  
Setspn -s MSOLAPSvc.3/AW-SRV02.AdventureWorks.com:AW-FINANCE AW-SRV02  
```  
  
##  <a name="bkmk_domain"></a> Registro de SPN para una cuenta de dominio  
 Una práctica común consiste en usar una cuenta de dominio para ejecutar una instancia de Analysis Services.  
  
 Para las instancias de Analysis Services que se ejecutan en un clúster de carga equilibrada de red o de hardware, se necesita una cuenta de dominio, con cada instancia del clúster en ejecución en la misma cuenta de dominio.  
  
 **Sintaxis de ejemplo para una instancia predeterminada que se ejecuta como usuario de dominio**  
  
 En este ejemplo se muestra la sintaxis de **setspn** para la instancia predeterminada de Analysis Services que se ejecuta en una cuenta de usuario de dominio, **SSAS-Service**, en el dominio AdventureWorks.  
  
```  
Setspn –s msolapsvc.3\AW-SRV01.Adventureworks.com AdventureWorks\SSAS-Service  
```  
  
> [!TIP]  
>  Compruebe si se ha creado el SPN para el servidor de Analysis Services ejecutando `Setspn -L <domain account>` o `Setspn -L <machinename>`, según la forma en que se haya registrado el SPN. Debería aparecer msolapsvc.3 /\<nombreHost > en la lista.  
  
##  <a name="bkmk_builtin"></a> Registro de SPN para una cuenta integrada  
 Aunque esta práctica no se recomienda, las instalaciones antiguas de Analysis Services están configuradas a veces para ejecutarse en cuentas integradas como Servicio de red, Servicio local o Sistema local.  
  
 **Sintaxis de ejemplo para una instancia predeterminada que se ejecuta en una cuenta integrada**  
  
 El registro de SPN para un servicio en ejecución en una cuenta integrada o un SID por servicio equivale a la sintaxis de SPN usada para la cuenta virtual. En lugar del nombre de cuenta, use la cuenta de equipo:  
  
```  
Setspn -s MSOLAPSvc.3/AW-SRV01.AdventureWorks.com AW-SRV01  
```  
  
##  <a name="bkmk_spnNamed"></a> Registro de SPN para una instancia con nombre  
 Las instancias con nombre de Analysis Services usan las asignaciones dinámicas de puerto que el servicio SQL Server Browser detecta. Cuando se usa una instancia con nombre, debe registrar un SPN tanto para el servicio SQL Server Browser como para la instancia con nombre de Analysis Services. Para obtener más información, vea [Se necesita un SPN para el servicio SQL Server Browser cuando se establece una conexión para una instancia con nombre de SQL Server Analysis Services o de SQL Server](http://support.microsoft.com/kb/950599).  
  
 **Ejemplo de sintaxis de SPN para el servicio SQL Browser en ejecución como LocalService**  
  
 La clase de servicio es **MSOLAPDisco.3**. De forma predeterminada, este servicio se ejecuta como NT AUTHORITY\LocalService, lo que significa que el registro de SPN está establecido para la cuenta de equipo. En este ejemplo, la cuenta de equipo es **AW-SRV01**, que corresponde al nombre de equipo.  
  
```  
Setspn -S MSOLAPDisco.3/AW-SRV01.AdventureWorks.com AW-SRV01  
```  
  
##  <a name="bkmk_spnCluster"></a> Registro de SPN para un clúster de SSAS  
 Para los clústeres de conmutación por error de Analysis Services, el nombre de host debe ser el nombre virtual asignado al clúster. Este es el nombre de red de SQL Server que se especificó durante la instalación de SQL Server en el momento de instalar Analysis Services sobre un WSFC existente. Puede encontrar este nombre en Active Directory. También puede encontrarlo en la pestaña **Administrador de clústeres de conmutación por error** | **Rol** | **Recursos** . El nombre del servidor en la pestaña Recursos es lo que debe usarse como "nombre virtual" en el comando SPN.  
  
 **Sintaxis de SPN para un clúster de Analysis Services**  
  
```  
Setspn –s msolapsvc.3/<virtualname.FQDN > <domain user account>  
```  
  
 Recuerde que los nodos de un clúster de Analysis Services deben usar el puerto predeterminado (TCP 2383) y ejecutarse bajo la misma cuenta de usuario de dominio para que cada nodo tenga el mismo SID. Vea el artículo sobre [cómo organizar en clúster SQL Server Analysis Services](http://msdn.microsoft.com/library/dn736073.aspx) para más información.  
  
##  <a name="bkmk_spnHTTP"></a> Registro de SPN para instancias de SSAS configuradas para acceso HTTP  
 En función de los requisitos de la solución, puede que haya configurado Analysis Services para acceso HTTP. Si la solución incluye IIS como componente de nivel intermedio, y la autenticación Kerberos es un requisito de la solución, puede que sea necesario registrar manualmente un SPN para IIS. Para obtener más información, vea "Configurar las opciones en el equipo que ejecuta IIS" en [Cómo configurar SQL Server 2008 Analysis Services y SQL Server 2005 Analysis Services para usar la autenticación de Kerberos](http://support.microsoft.com/kb/917409).  
  
 En cuanto al registro de SPN para la instancia de Analysis Services, no hay ninguna diferencia entre una instancia configurada para TCP o para HTTP. La conexión con Analysis Services desde IIS, mediante la extensión ISAPI de MSMDPUMP, siempre es TCP.  
  
 Esto significa que puede usar las instrucciones de las secciones anteriores relativas a la instancia con nombre o predeterminada para registrar el SPN. Al especificar el nombre de host, asegúrese de usar el nombre de host que especificó en el archivo msmdpump.ini al configurar el servicio para acceso HTTP.  
  
 Para más información, vea [Configurar el acceso HTTP a Analysis Services en Internet Information Services &#40;IIS&#41; 8.0](../../analysis-services/instances/configure-http-access-to-analysis-services-on-iis-8-0.md).  
  
##  <a name="bkmk_spnFixedPorts"></a> Registro de SPN para instancias de SSAS que escuchan en varios puertos fijos  
 No puede especificar un número de puerto en un registro de SPN de Analysis Services. Si instaló Analysis Services como instancia predeterminada y lo configuró para escuchar en un puerto fijo, ahora debe configurarlo para escuchar en el puerto predeterminado (TCP 2383). En el caso de instancias con nombre, debe usar el servicio SQL Server Browser y asignaciones dinámicas de puerto.  
  
 Una instancia de Analysis Services solo puede escuchar en un único puerto. No se admite usar varios puertos. Para obtener más información acerca de la configuración de puertos, vea [Configure the Windows Firewall to Allow Analysis Services Access](../../analysis-services/instances/configure-the-windows-firewall-to-allow-analysis-services-access.md).  
  
## <a name="see-also"></a>Vea también  
 [Autenticación y delegación de identidades de Microsoft BI](http://go.microsoft.com/fwlink/?LinkID=286576)   
 [Autenticación mutua con Kerberos](http://go.microsoft.com/fwlink/?LinkId=299283)   
 [Cómo configurar SQL Server 2008 Analysis Services y SQL Server 2005 Analysis Services para usar la autenticación de Kerberos](http://support.microsoft.com/kb/917409)   
 [Nombres de entidad de servicio (SPN) sintaxis de SetSPN (Setspn.exe)](http://social.technet.microsoft.com/wiki/contents/articles/717.service-principal-names-spns-setspn-syntax-setspn-exe.aspx)   
 [¿Qué SPN se debe usar y cómo llega allí?](http://social.technet.microsoft.com/wiki/contents/articles/717.service-principal-names-spns-setspn-syntax-setspn-exe.aspx)   
 [SetSPN](http://technet.microsoft.com/library/cc731241\(WS.10\).aspx)   
 [Guía paso a paso de las cuentas de servicio](http://technet.microsoft.com/library/dd548356\(WS.10\).aspx)   
 [Configurar los permisos y las cuentas de servicio de Windows](../../database-engine/configure-windows/configure-windows-service-accounts-and-permissions.md)   
 [Cómo usar SPN al configurar aplicaciones Web que se hospedan en Internet Information Services](http://support.microsoft.com/kb/929650)   
 [Novedades de las cuentas de servicio](http://technet.microsoft.com/library/dd367859\(WS.10\).aspx)   
 [Configurar la autenticación de Kerberos para productos de SharePoint 2010 (notas del producto)](http://technet.microsoft.com/library/ff829837.aspx)  
  
  
