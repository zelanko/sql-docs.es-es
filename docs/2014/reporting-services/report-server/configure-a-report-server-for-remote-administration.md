---
title: Configurar un servidor de informes para la administración remota | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- reporting-services-native
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- Reporting Services Configuration tool
- WMI provider [Reporting Services], remote configuration
- configuration management [WMI]
- report servers [Reporting Services], configuring
- remote server administration [Reporting Services]
ms.assetid: 8c7f145f-3ac2-4203-8cd6-2a4694395d09
caps.latest.revision: 9
author: markingmyname
ms.author: maghan
manager: mblythe
ms.openlocfilehash: 0f7a3ee16a9085639e03abe268c4c72dc0f488de
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36111284"
---
# <a name="configure-a-report-server-for-remote-administration"></a>Configurar un servidor de informes para la administración remota
  En [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)], puede configurar las instancias del servidor de informes local o remotamente. Para configurar una instancia del servidor de informes remota, se puede utilizar la herramienta Configuración de Reporting Services o escribir código personalizado que utilice el proveedor de Instrumental de administración de Windows (WMI) de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] . La herramienta de configuración de Reporting Services proporciona una interfaz gráfica para el proveedor WMI, de modo que se puede configurar un servidor de informes sin tener que escribir código. Al iniciar la herramienta, se puede especificar el servidor remoto con el que se desea establecer la conexión.  
  
 Para poder utilizar la herramienta con el fin de configurar un servidor de informes remoto, debe seguir las instrucciones de este tema para habilitar los puertos en Firewall de Windows, habilitar las conexiones remotas y habilitar las solicitudes de WMI remotas.  
  
 La configuración apropiada le ayuda a evitar el error siguiente:  
  
 `The machine could not be found.`  
  
 `"The RPC server is unavailable. (Exception from HRESULT: 0x800706BA)".`  
  
## <a name="prerequisites"></a>Requisitos previos  
 Para modificar la configuración del firewall, es necesario iniciar sesión de manera local y ser miembro del grupo local Administradores. No se puede modificar la configuración del firewall de Windows de un equipo remoto a través de una conexión remota.  
  
 Si se desea habilitar la administración remota para un usuario que no es administrador, es necesario conceder a la cuenta permisos para la activación remota del Modelo de objetos componentes distribuido (DCOM). En este tema se ofrecen instrucciones para configurar el servidor para el acceso de usuarios que no son administradores.  
  
 Algunas organizaciones tienen directivas de grupo que impiden la administración remota de servidores para algunos sistemas operativos o usuarios. Antes de modificar la configuración del firewall, pregunte al administrador de la red si existen restricciones en cuanto a la administración remota.  
  
 Para obtener más información, vea [Connecting Through Windows Firewall](http://go.microsoft.com/fwlink/?LinkId=63615) en la documentación de Plataform SDK en MSDN.  
  
## <a name="tasks"></a>Tareas  
 Entre las tareas que habilitan la configuración del servidor de informes remoto figuran las siguientes:  
  
-   Habilitar los puertos en Firewall de Windows para permitir solicitudes en los puertos que usa el servidor de informes y la instancia del Motor de base de datos de SQL Server.  
  
-   Habilitar las conexiones remotas a la instancia del Motor de base de datos que hospeda la base de datos del servidor de informes. La conexión remota es necesaria para configurar la conexión de la base de datos del servidor de informes y administrar las claves de cifrado.  
  
-   Habilitar las solicitudes de WMI remotas para atravesar el Firewall de [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows.  
  
-   Si está configurando un servidor de informes remoto para que lo administre un usuario sin derechos administrativos, debe establecer los permisos DCOM para habilitar el acceso WMI remoto a una cuenta de usuario de Windows estándar. Debido a que WMI utiliza DCOM como transporte para las llamadas remotas, es necesario establecer los permisos de DCOM de manera que los usuarios que no inicien sesión como administrador local puedan configurar el servidor.  
  
-   Si está configurando un servidor de informes remoto para que lo administre un usuario sin derechos administrativos, también debe establecer los permisos WMI en el espacio de nombres WMI del servidor de informes. De manera predeterminada, todos los miembros del grupo local Administradores tienen acceso al espacio de nombres de WMI del servidor de informes. Si se desea conceder acceso a usuarios que no sean administradores, deben establecerse permisos.  
  
 Las instrucciones para realizar estas tareas se proporcionan en este tema.  
  
### <a name="to-open-ports-in-windows-firewall"></a>Abrir puertos en Firewall de Windows  
  
1.  [Configurar Firewall de Windows para obtener acceso al motor de base de datos](../../database-engine/configure-windows/configure-a-windows-firewall-for-database-engine-access.md).  
  
2.  [Configurar un Firewall para el acceso del servidor de informes](configure-a-firewall-for-report-server-access.md).  
  
### <a name="to-configure-remote-connections-to-the-report-server-database"></a>Configurar las conexiones remotas a la base de datos del servidor de informes  
  
1.  Haga clic en **Inicio**, elija **Todos los programas**, [!INCLUDE[ssCurrentUI](../../includes/sscurrentui-md.md)], **Herramientas de configuración**y, finalmente, haga clic en **Administrador de configuración de SQL Server**.  
  
2.  En el panel izquierdo, expanda **Configuración de red de SQL Server**y, a continuación, haga clic en **Protocolos** para la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
3.  En el panel de detalles, habilite los protocolos TCP/IP y Canalizaciones con nombre y, después, reinicie el servicio [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
### <a name="to-enable-remote-administration-in-windows-firewall"></a>Para habilitar la administración remota en Firewall de Windows  
  
1.  Inicie sesión como administrador local en el equipo para el que desea habilitar la administración remota.  
  
2.  Si el servidor de informes se ejecuta en Windows Vista, haga clic en **símbolo** y seleccione **ejecutar como administrador**. En otros sistemas operativos, abra una ventana del símbolo del sistema.  
  
3.  Ejecute el siguiente comando:  
  
    ```  
    netsh.exe firewall set service type=REMOTEADMIN mode=ENABLE scope=ALL  
    ```  
  
     Puede especificar varias opciones para Scope. Para obtener más información, vea la documentación del producto Firewall de Windows.  
  
4.  Compruebe que se ha habilitado la administración remota. Puede ejecutar el comando siguiente para mostrar el estado:  
  
    ```  
    netsh.exe firewall show state  
    ```  
  
5.  Reinicie el equipo.  
  
### <a name="to-set-dcom-permissions-to-enable-remote-wmi-access-for-non-administrators"></a>Para establecer permisos DCOM que habiliten el acceso remoto a WMI para usuarios que no son administradores  
  
1.  En el menú Inicio, seleccione **Herramientas administrativas**y haga clic en **Servicios de componente**.  
  
     En Windows Vista, en el menú Inicio, haga clic en **todos los programas**, haga clic en **ejecutar**y, a continuación, escriba `mmc comexp.msc`.  
  
2.  Abra la carpeta Servicios de componente.  
  
3.  Abra la carpeta Equipos.  
  
4.  Seleccione Mi PC.  
  
5.  En el menú **Acción** , seleccione **Propiedades**.  
  
6.  Haga clic en **Seguridad COM**.  
  
7.  En **Permisos de inicio y activación**, haga clic en **Editar límites**.  
  
8.  Si no aparece su nombre en **Permisos de inicio**, haga clic en **Agregar**.  
  
9. Escriba el nombre de su cuenta de usuario y, a continuación, haga clic en **Aceptar**.  
  
10. En **Permisos de \<usuario o grupo**, en la columna **Permitir**, seleccione **Ejecución remota** y **Activación remota** y luego haga clic en **Aceptar**.  
  
### <a name="to-set-permissions-on-the-report-server-wmi-namespace-for-non-administrators"></a>Para establecer permisos para el espacio de nombres de WMI del servidor de informes para usuarios que no son administradores  
  
1.  En el menú Inicio, seleccione **Herramientas administrativas**y haga clic en **Administración de equipos**.  
  
2.  Abra la carpeta Servicios y Aplicaciones.  
  
3.  Haga clic con el botón derecho en **Control WMI**y seleccione **Propiedades**.  
  
4.  Haga clic en **Seguridad**.  
  
5.  Abra la carpeta raíz.  
  
6.  Abra la carpeta Microsoft.  
  
7.  Abra la carpeta SQLServer.  
  
8.  Abra la carpeta ReportServer.  
  
9. Abra la carpeta de la instancia. Si instaló la instancia predeterminada, la carpeta es MSSQLSERVER.  
  
10. Abra la carpeta v10.  
  
11. Seleccione la carpeta Admin y, a continuación, haga clic en **Seguridad**.  
  
12. Haga clic en **Agregar**y, después, escriba la cuenta de usuario que se empleará para administrar el servidor.  
  
13. En la columna **Permitir** , seleccione **Habilitar cuenta**, **Llamada remota habilitada**y **Seguridad de lectura**y, a continuación, haga clic en **Aceptar**.  
  
## <a name="see-also"></a>Vea también  
 [Administrador de configuración de Reporting Services &#40;modo nativo&#41;](../../sql-server/install/reporting-services-configuration-manager-native-mode.md)  
  
  