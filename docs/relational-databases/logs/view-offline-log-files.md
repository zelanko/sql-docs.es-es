---
title: "Ver archivos de registro sin conexión | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- Log File Viewer, viewing offline logs
- offline log files
ms.assetid: 9223e474-f224-4907-a4f2-081e11db58f5
caps.latest.revision: 18
author: BYHAM
ms.author: rickbyh
manager: jhubbard
translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 339787b7252b5604a08770d417fe39d5b63aca70
ms.lasthandoff: 04/11/2017

---
# <a name="view-offline-log-files"></a>Ver archivos del registro sin conexión
  A partir de [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)], los archivos de registro de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] se pueden ver desde una instancia local o remota de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] cuando la instancia de destino está sin conexión o no se puede iniciar.  
  
 Puede tener acceso a los archivos de registro sin conexión de servidores registrados o mediante programación a través de consultas WMI y WQL (Lenguaje de la consulta de WMI).  
  
> [!NOTE]  
>  También puede utilizar estos métodos para conectar a una instancia que está en línea, pero por el motivo que sea no puede conectarse a través de una conexión de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
## <a name="before-you-begin"></a>Antes de empezar  
 Para conectarse a los archivos de registro sin conexión, debe haber una instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] instalada en el equipo que está utilizando para ver los archivos de registro sin conexión y en el equipo donde se encuentran los archivos de registro que desea ver. Si hay una instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] instalada en los dos equipos, puede ver los archivos sin conexión para las instancias de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]y para las instancias que ejecutan versiones anteriores de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] en cualquiera de los dos equipos.  
  
 Si utiliza servidores registrados, la instancia a la que desea conectarse debe estar registrada en **Grupos de servidores locales** o en **Servidores de administración central**. La instancia se puede registrar sola o pertenecer a un grupo de servidores. Para obtener más información acerca de cómo agregar una instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] a servidores registrados, vea los temas siguientes:  
  
-   [Crear o editar un grupo de servidores &#40;SQL Server Management Studio&#41;](../../tools/sql-server-management-studio/create-or-edit-a-server-group-sql-server-management-studio.md)  
  
-   [Registrar un servidor conectado &#40;SQL Server Management Studio&#41;](../../tools/sql-server-management-studio/register-a-connected-server-sql-server-management-studio.md)  
  
-   [Crear un servidor de administración central y un grupo de servidores &#40;SQL Server Management Studio&#41;](../../tools/sql-server-management-studio/create-a-central-management-server-and-server-group.md)  
  
 Para obtener más información sobre cómo ver archivos de registro sin conexión mediante programación con consultas WMI y WQL, vea los temas siguientes:  
  
-   [SqlErrorLogEvent Class](../../relational-databases/wmi-provider-configuration-classes/sqlerrorlogevent-class.md) (en este tema se muestra cómo recuperar los valores de los eventos registrados en un archivo de registro especificado).  
  
-   [SqlErrorLogFile Class](../../relational-databases/wmi-provider-configuration-classes/sqlerrorlogfile-class.md) (en este tema se muestra cómo recuperar información sobre todos los archivos de registro de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] de una instancia especificada de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]).  
  
##  <a name="BeforeYouBegin"></a> Permisos  
 Para conectarse a un archivo de registro sin conexión, debe tener los siguientes permisos en los equipos local y remoto:  
  
-   Acceso de lectura al espacio de nombres de WMI **raíz\Microsoft\SqlServer\ComputerManagement12** . De forma predeterminada, todos tienen acceso de lectura mediante el permiso Habilitar cuenta. Para obtener más información, vea el procedimiento sobre comprobación de permisos de WMI más adelante en esta sección.  
  
-   Permiso de lectura a la carpeta que contiene los archivos de registro de errores. Los archivos de registro de errores se encuentran de forma predeterminada en la siguiente ruta de acceso (donde \<*unidad>* representa la unidad donde se instaló [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] y \<*nombreInstancia*> es el nombre de la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]):  
  
     **\<unidad>:\Microsoft SQL Server\MSSQL13.\<nombreInstancia>\MSSQL\Log**  
  
 Para comprobar la configuración de seguridad del espacio de nombres WMI, puede utilizar el complemento Control WMI.  
  
#### <a name="to-verify-wmi-permissions"></a>Comprobar los permisos de WMI  
  
1.  Abra el complemento Control WMI. Para hacerlo, realice una de las operaciones siguientes, en función del sistema operativo:  
  
    -   Haga clic en **Inicio**, escriba **wmimgmt.msc** en el cuadro **Iniciar búsqueda** y presione ENTRAR.  
  
    -   Haga clic en **Inicio**, haga clic en **Ejecutar**, escriba **wmimgmt.msc**y, a continuación, presione ENTRAR.  
  
2.  De forma predeterminada, el complemento Control WMI administra el equipo local.  
  
     Si desea conectarse a un equipo remoto, siga estos pasos:  
  
    1.  Haga clic con el botón derecho en **Control WMI (local)**y, luego, haga clic en **Conectarse a otro equipo**.  
  
    2.  En el cuadro de diálogo **Cambiar equipo administrado** , haga clic en **Otro equipo**.  
  
    3.  Escriba el nombre del equipo remoto y haga clic en **Aceptar**.  
  
3.  Haga clic con el botón derecho en **Control WMI (local)** o **Control WMI (***nombreEquipoRemoto***)**y, después, haga clic en **Propiedades**.  
  
4.  En el cuadro de diálogo **Propiedades de Control WMIP** , haga clic en la pestaña **Seguridad** .  
  
5.  En el árbol de espacio de nombres, busque el siguiente espacio de nombres y haga clic en él:  
  
     **Raíz\Microsoft\SqlServer\ComputerManagement10**  
  
6.  Haga clic en **Seguridad**.  
  
7.  Asegúrese de que la cuenta que se va a utilizar tiene el permiso **Habilitar cuenta** . Este permiso permite el acceso de lectura a los objetos WMI.  
  
### <a name="view-log-files"></a>Ver archivos de registro  
 El siguiente procedimiento indica cómo ver los archivos de registro sin conexión a través de servidores registrados. En el procedimiento se supone que:  
  
 La instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] a la que desea conectarse ya está registrada en servidores registrados.  
  
##### <a name="to-view-log-files-for-instances-that-are-offline"></a>Ver los archivos de registro de las instancias que están sin conexión  
  
1.  Si desea ver los archivos de registro sin conexión en una instancia local, asegúrese de que inicia [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] con permisos elevados. Para ello, al iniciar [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)], haga clic con el botón derecho en **SQL Server Management Studio**y, después, haga clic en **Ejecutar como administrador**.  
  
2.  En [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], en el menú **Ver** , haga clic en **Servidores registrados**.  
  
3.  En el árbol de consola, busque la instancia en la que desea ver los archivos sin conexión.  
  
4.  Realice una de las siguientes operaciones:  
  
    -   Si la instancia está en **Grupos de servidor locales**, expanda **Grupos de servidor locales**, expanda el grupo de servidores (si la instancia pertenece a un grupo), haga clic con el botón derecho en la instancia y, después, haga clic en **Ver registro de SQL Server**.  
  
    -   Si la instancia es el propio servidor de administración Central, expanda **Servidores de administración central**, haga clic con el botón derecho en la instancia, seleccione **Acciones del servidor de administración central**y, después, haga clic en **Ver registro de SQL Server**.  
  
    -   Si la instancia está en **Servidores de administración central**, expanda **Servidores de administración central**, expanda el servidor de administración central, haga clic con el botón derecho en la instancia (o expanda un grupo de servidores y haga clic con el botón derecho en la instancia) y, después, haga clic en **Ver registro de SQL Server**.  
  
5.  Si se va a conectar a una instancia local, la conexión se realiza utilizando las credenciales de usuario actuales.  
  
     Si se va a conectar a una instancia remota, en el cuadro de diálogo **Visor de archivos de registro - Conectar como** , realice una de las operaciones siguientes:  
  
    -   Para conectarse como usuario actual, asegúrese de que la casilla **Conectar como otro usuario** está desactivada y, a continuación, haga clic en **Aceptar**.  
  
    -   Para conectarse como otro usuario, active la casilla **Conectar como otro usuario** y, a continuación, haga clic en **Establecer usuario**. Cuando se le pida, especifique las credenciales de usuario (con el nombre de usuario en el formato *nombre_dominio*\\*nombre_usuario*), haga clic en **Aceptar**y, después, de nuevo en **Aceptar** para conectarse.  
  
    > [!NOTE]  
    >  Si los archivos de registro tardan demasiado en cargarse, puede hacer clic en **Detener** en la barra de herramientas del Visor del archivo de registros.  
  
## <a name="see-also"></a>Vea también  
 [Visor de archivos de registro](../../relational-databases/logs/log-file-viewer.md)  
  
  
