---
title: Configurar un firewall de Windows para el acceso al servicio SSIS | Microsoft Docs
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- security [Integration Services], firewalls
- Windows Firewall [Integration Services]
- unauthorized access [Integration Services]
- Integration Services service, firewalls
- firewall systems [Integration Services]
- SQL Server Integration Services, firewalls
- SSIS, firewalls
ms.assetid: 39975cf2-c351-4205-8c39-27a0fadfb010
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: b2c6a19eb44b1d53fe87bef0183bdafbb3ec105b
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "66060850"
---
# <a name="configure-a-windows-firewall-for-access-to-the-ssis-service"></a>Configurar Firewall de Windows para el acceso al servicio SSIS
    
> [!IMPORTANT]  
>  En este tema se describe el servicio de [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] , un servicio Windows para administrar paquetes de [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] . [!INCLUDE[ssSQL11](../includes/sssql11-md.md)]admite el servicio para mantener la compatibilidad con versiones anteriores [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)]de. A partir de [!INCLUDE[ssSQL11](../includes/sssql11-md.md)], puede administrar objetos como paquetes en el servidor de Integration Services.  
  
 El sistema Firewall de Windows impide el acceso no autorizado a los recursos de los equipos de una conexión de red. Para obtener acceso a [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] mediante este firewall, debe configurarlo para permitir el acceso.  
  
> [!IMPORTANT]  
>  Para administrar paquetes almacenados en un servidor remoto, no tiene que conectarse a la instancia del servicio de [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] en ese servidor remoto. En su lugar, modifique el archivo de configuración para el servicio de [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] de manera que [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] muestre los paquetes almacenados en el servidor remoto. Para obtener más información, vea [Configurar el servicio Integration Services &#40;servicio SSIS&#41;](configuring-the-integration-services-service-ssis-service.md).  
  
 El servicio [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] utiliza el protocolo DCOM. Para obtener más información acerca de cómo funciona el protocolo DCOM a través de firewalls, consulte el artículo sobre el[uso de com distribuido con firewalls](https://manualzz.com/doc/19762578/using-distributed-com-with-firewalls-by-michael-nelson-in...).  
  
 Existen varios sistemas de firewall. Si ejecuta un firewall distinto de Firewall de Windows, vea la documentación del firewall para obtener información específica del sistema que utiliza.  
  
 Si el firewall admite el filtrado de aplicaciones, puede utilizar la interfaz de usuario de Windows para especificar las excepciones permitidas en el firewall, como programas y servicios. Si no es el caso, debe configurar DCOM para utilizar un conjunto limitado de puertos TCP. El vínculo al sitio web de Microsoft mencionado anteriormente incluye información acerca de cómo especificar los puertos TCP que debe utilizar.  
  
 El servicio Integration Services utiliza el puerto 135 y no es posible cambiarlo. Debe abrir el puerto TCP 135 para obtener acceso al Administrador de control de servicios (SCM). Entre las tareas que realiza el SCM se encuentra el inicio y detención de servicios de [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] y la transmisión de solicitudes de control al servicio en ejecución.  
  
 La información que se incluye en la siguiente sección es específica de Firewall de Windows. Para configurar el sistema Firewall de Windows, debe ejecutar un comando desde el símbolo del sistema o establecer las propiedades en el cuadro de diálogo de Firewall de Windows.  
  
 Para obtener más información sobre la configuración predeterminada de Firewall de Windows y una descripción de los puertos TCP que afectan al motor de base de datos, Analysis Services, Reporting Services e Integration Services, vea [Configurar Firewall de Windows para permitir el acceso a SQL Server](../../2014/sql-server/install/configure-the-windows-firewall-to-allow-sql-server-access.md).  
  
## <a name="configuring-a-windowsfirewall"></a>Configurar Firewall de Windows  
 Puede utilizar los siguientes comandos para abrir el puerto TCP 135, agregar MsDtsSrvr.exe a la lista de excepciones y especificar el ámbito de desbloqueo del firewall.  
  
#### <a name="to-configure-a-windowsfirewall-using-the-command-prompt-window"></a>Para configurar un firewall de Windows en la ventana del símbolo del sistema  
  
1.  Ejecute el comando: `netsh firewall add portopening protocol=TCP port=135 name="RPC (TCP/135)" mode=ENABLE scope=SUBNET`  
  
2.  Ejecute el comando: `netsh firewall add allowedprogram program="%ProgramFiles%\Microsoft SQL Server\100\DTS\Binn\MsDtsSrvr.exe" name="SSIS Service" scope=SUBNET`  
  
    > [!NOTE]  
    >  Para abrir el firewall en todos los equipos, además de los que se encuentran en Internet, reemplace el ámbito=SUBNET por el ámbito=ALL.  
  
 En el siguiente procedimiento se describe cómo utilizar la interfaz de usuario de Windows para abrir el puerto TCP 135, agregar MsDtsSrvr.exe a la lista de excepciones y especificar el ámbito de desbloqueo del firewall.  
  
#### <a name="to-configure-a-firewall-using-the-windowsfirewall-dialog-box"></a>Para configurar un firewall mediante el cuadro de diálogo Firewall de Windows  
  
1.  En el Panel de control, haga doble clic en **Firewall de Windows**.  
  
2.  En el cuadro de diálogo **Firewall de Windows** , haga clic en la pestaña **Excepciones** y, a continuación, haga clic en **Agregar programa**.  
  
3.  En el cuadro de diálogo **Agregar un programa** , haga clic en **Examinar**, navegue a la carpeta Archivos de programa\Microsoft SQL Server\100\DTS\Binn, haga clic en MsDtsSrvr.exe y, después, en **Abrir**. Haga clic en **Aceptar** para cerrar el cuadro de diálogo **Agregar un programa** .  
  
4.  En la pestaña **Excepciones** , haga clic en **Agregar puerto**.  
  
5.  En el cuadro de diálogo **Agregar un puerto** , escriba **RPC(TCP/135)** u otro nombre descriptivo en el cuadro **Nombre**, escriba **135** en el cuadro **Número de puerto** y seleccione **TCP**.  
  
    > [!IMPORTANT]  
    >  
  [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] utiliza siempre el puerto 135. No se puede especificar un puerto diferente.  
  
6.  En el cuadro de diálogo **Agregar un puerto** , puede hacer clic en **Cambiar ámbito** para modificar el ámbito predeterminado.  
  
7.  En el cuadro de diálogo **Cambiar ámbito** , seleccione **Mi red (solo subred)** o escriba una lista personalizada y haga clic en **Aceptar**.  
  
8.  Para cerrar el cuadro de diálogo **Agregar un puerto** , haga clic en **Aceptar**.  
  
9. Para cerrar el cuadro de diálogo **Firewall de Windows** , haga clic en **Aceptar**.  
  
    > [!NOTE]  
    >  Para configurar el Firewall de Windows, este procedimiento utiliza el elemento **Firewall de Windows** del Panel de control. El elemento **Firewall de Windows** solo configura el firewall para el perfil de la ubicación de red actual. En cambio, también puede configurar el Firewall de Windows mediante la herramienta de línea de comandos **netsh** o el complemento [!INCLUDE[msCoName](../includes/msconame-md.md)] Management Console (MMC) denominado Firewall de Windows con Seguridad avanzada. Para obtener más información sobre estas herramientas, vea [Configurar Firewall de Windows para permitir el acceso a SQL Server](../../2014/sql-server/install/configure-the-windows-firewall-to-allow-sql-server-access.md).  
  
## <a name="see-also"></a>Consulte también  
 [Configuración del servicio Integration Services &#40;servicio SSIS&#41;](service/integration-services-service-ssis-service.md)   
 [Servicio Integration Services &#40;servicio SSIS&#41;](service/integration-services-service-ssis-service.md)  
  
  
