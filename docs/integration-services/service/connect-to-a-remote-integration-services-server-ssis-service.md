---
title: "Conectarse a un servidor remoto de Integration Services (servicio SSIS) | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "integration-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "servicio [Integration Services], instancia remota"
  - "servicio Integration Services, conectarse"
  - "servicio Integration Services, instancia remota"
  - "servicio [Integration Services], conectarse"
ms.assetid: 9487aff1-44d8-42c1-8176-bb9891d4632d
caps.latest.revision: 42
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 40
---
# Conectarse a un servidor remoto de Integration Services (servicio SSIS)
    
> [!IMPORTANT] En este tema se describe el servicio de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] , un servicio Windows para administrar paquetes de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] . [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] admite el servicio para mantener la compatibilidad con versiones anteriores de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]. A partir de [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)], puede administrar objetos como paquetes en el servidor de Integration Services.  
  
 Para conectarse a una instancia de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] en un servidor remoto, desde [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] u otra aplicación de administración, los usuarios de la aplicación deben tener un conjunto específico de derechos para el servidor.  
  
> [!IMPORTANT] Para conectar directamente con una instancia del servicio Integration Services heredado, tendrá que usar la versión de SQL Server Management Studio (SSMS) alineada con la versión de SQL Server en la que se ejecuta el servicio Integration Services. Por ejemplo, para conectar con el servicio Integration Services heredado que se ejecuta en una instancia de SQL Server 2016, debe usar la versión de SSMS publicada para SQL Server 2016. [Descargue SQL Server Management Studio (SSMS)](https://msdn.microsoft.com/library/mt238290.aspx).
>
>  Para administrar paquetes almacenados en un servidor remoto, no tiene que conectarse a la instancia del servicio de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] en ese servidor remoto. En su lugar, modifique el archivo de configuración para el servicio de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] de manera que [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] muestre los paquetes almacenados en el servidor remoto. Para obtener más información, vea [Configurar el servicio Integration Services &#40;servicio SSIS&#41;](../../integration-services/service/configuring-the-integration-services-service-ssis-service.md).  
  
## Conectarse a Integration Services en un servidor remoto  
  
#### Para conectarse a Integration Services en un servidor remoto  
  
1.  Abra [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)].  
  
2.  Seleccione **Archivo**, **Conectar Explorador de objetos** para mostrar el cuadro de diálogo **Conectar al servidor** .  
  
3.  Seleccione **Integration Services** en la lista **Tipo de servidor** .  
  
4.  Escriba el nombre de un servidor [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] en el cuadro de texto **Nombre del servidor** .  
  
    > [!NOTE]  
    >  El servicio [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] no es específico de la instancia. La conexión al servicio se realiza utilizando el nombre del equipo en el que el servicio de Integration Services se está ejecutando.  
  
5.  Haga clic en **Conectar**.  
  
> [!NOTE]  
>  En el cuadro de diálogo **Buscar servidores** no se muestran las instancias remotas de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]. Además, las opciones disponibles en la pestaña **Opciones de conexión** del cuadro de diálogo **Conectar al servidor** , que se muestra al hacer clic en el botón **Opciones** , no se aplican a las conexiones de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] .  
  
## Eliminación del error de acceso denegado  
 Cuando un usuario que no tiene los derechos necesarios intenta conectarse a una instancia de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] en un servidor remoto, el servidor responde con el mensaje de error "Acceso denegado". Se puede evitar ese mensaje de error asegurándose de que los usuarios tengan los permisos DCOM necesarios.  
  
#### Para configurar derechos para usuarios remotos en Windows Server 2003 o Windows XP  
  
1.  Si el usuario no es miembro del grupo de administradores local, agregue el usuario al grupo de usuarios de COM distribuido. Puede hacerlo en el complemento Administración de equipos de MMC, en el menú **Herramientas administrativas**.  
  
2.  Abra el Panel de control, haga doble clic en **Herramientas administrativas** y en **Servicios de componente** para iniciar el complemento Servicios de componentes de MMC.  
  
3.  Expanda el nodo **Servicios de componente** en el panel izquierdo de la consola. Expanda los nodos **Equipos** y **Mi PC**y, a continuación, haga clic en el nodo **Configuración DCOM** .  
  
4.  Seleccione el nodo **Configuración DCOM** y, a continuación, seleccione SQL Server Integration Services 11.0 en la lista de aplicaciones que pueden configurarse.  
  
5.  Haga clic con el botón derecho en SQL Server Integration Services 11.0 y seleccione **Propiedades**.  
  
6.  En el cuadro de diálogo **Propiedades de SQL Server Integration Services 11.0** , seleccione la pestaña **Seguridad** .  
  
7.  En **Permisos de inicio y activación**, active **Personalizar**y haga clic en **Editar** para abrir el cuadro de diálogo **Permisos de inicio** .  
  
8.  En el cuadro de diálogo **Permisos de inicio** , agregue o elimine usuarios y asigne los permisos adecuados a los usuarios y grupos correspondientes. Los permisos disponibles son Ejecución local, Ejecución remota, Activación local y Activación remota. Los derechos de ejecución conceden o deniegan el permiso para iniciar y detener el servicio; los derechos de activación conceden o deniegan el permiso para conectarse al servicio.  
  
9. Haga clic en Aceptar para cerrar el cuadro de diálogo.  
  
10. En **Permisos de acceso**, repita los pasos 7 y 8 con el fin de asignar los permisos pertinentes a los correspondientes usuarios y grupos.  
  
11. Cierre el complemento MMC.  
  
12. Reinicie el servicio [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] .  
  
#### Para configurar derechos para usuarios remotos en Windows 2000 con los Service Pack más recientes  
  
1.  Ejecute **dcomcnfg.exe** en el símbolo del sistema.  
  
2.  En la página **Aplicaciones** del cuadro de diálogo **Propiedades de Configuración de COM distribuido** , seleccione SQL Server Integration Services 11.0 y haga clic en **Propiedades**.  
  
3.  Seleccione la página **Seguridad** .  
  
4.  Utilice los dos cuadros de diálogo independientes para configurar **Permisos de acceso** y **Permisos de inicio**. No se puede distinguir entre el acceso remoto y el acceso local; los permisos de acceso incluyen el acceso local y el remoto, y los permisos de inicio incluyen la ejecución local y la remota.  
  
5.  Cierre los cuadros de diálogo y **dcomcnfg.exe**.  
  
6.  Reinicie el servicio [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] .  
  
## Conectarse con una cuenta local  
 Si se trabaja en una cuenta local de Windows en un equipo cliente, solo es posible conectarse al servicio [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] en un equipo remoto si en el equipo remoto existe una cuenta local con el mismo nombre y contraseña, y con los derechos adecuados.  
  
## De forma predeterminada, el servicio SSIS no admite la delegación  
De forma predeterminada, el servicio [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] no admite la delegación de credenciales, a veces denominada salto doble. En este escenario, se trabaja con un equipo cliente, el servicio [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] se ejecuta en un segundo equipo y [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] se ejecuta en un tercer equipo. Primero, [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] pasa correctamente las credenciales del equipo cliente al segundo equipo en el que se ejecuta el servicio [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]. Pero, después, el servicio [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] no puede delegar las credenciales del segundo equipo al tercero, en el que se ejecuta [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].

Puede habilitar la delegación de credenciales si concede el derecho **Confiar en este usuario para la delegación a cualquier servicio (solo Kerberos)** a la cuenta de servicio de SQL Server, que inicia el servicio Integration Services (ISServerExec.exe) como un proceso secundario. Antes de conceder este derecho, considere si cumple los requisitos de seguridad de su organización.

Para obtener más información, vea [Getting Cross Domain Kerberos and Delegation working with SSIS Package](https://blogs.msdn.microsoft.com/psssql/2014/06/26/getting-cross-domain-kerberos-and-delegation-working-with-ssis-package/) (Conseguir que la delegación y Kerberos entre dominios funcionen con el paquete SSIS).
  
## Vea también  
 [Configurar Firewall de Windows para el acceso al servicio SSIS](../../integration-services/service/configure-a-windows-firewall-for-access-to-the-ssis-service.md)  
  
  