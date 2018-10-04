---
title: Solución de problemas de la utilidad de SQL Server | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
ms.assetid: f5f47c2a-38ea-40f8-9767-9bc138d14453
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 34d6c6eb60d48edad7d00a4baf890814dab8a016
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/02/2018
ms.locfileid: "48186205"
---
# <a name="troubleshoot-the-sql-server-utility"></a>Solucionar problemas de la Utilidad de SQL Server
  Se pueden citar como ejemplos de solución de problemas de la utilidad de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] la resolución de una operación que no ha podido inscribir una instancia de SQL Server con un UCP, la resolución de un error de recopilación de datos que crea iconos deshabilitados en la vista de lista de instancias administradas de un UCP, la mitigación de cuellos de botella de rendimiento o la resolución de problemas de mantenimiento de recursos. Para obtener más información sobre cómo mitigar problemas de mantenimiento de recursos identificados por un [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] UCP, vea [solucionar problemas de mantenimiento de recursos de SQL Server &#40;utilidad de SQL Server&#41;](../relational-databases/manage/troubleshoot-sql-server-resource-health-sql-server-utility.md).  
  
## <a name="failed-operation-to-enroll-an-instance-of-sql-server-into-a-sql-server-utility"></a>Error de una operación de inscripción de una instancia de SQL Server en una Utilidad de SQL Server  
 Si se conecta a la instancia de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] inscribirse mediante [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] autenticación y especificar una cuenta de proxy que pertenece a un dominio de Active Directory diferente que el dominio donde está el UCP, validación de instancia es correcta, pero el se produce un error en la operación de inscripción con el mensaje de error siguiente:  
  
 Se ha producido una excepción al ejecutar una instrucción o lote Transact-SQL. (Microsoft.SqlServer.ConnectionInfo)  
  
 Información adicional: no se ha podido obtener información sobre el grupo o usuario '\<nombreDeDominio\nombreDeCuenta>' de Windows NT, código de error 0x5. (Microsoft SQL Server, Error: 15404)  
  
 Este problema sucede en el siguiente escenario de ejemplo:  
  
1.  El UCP es miembro de "Domain_1."  
  
2.  Existe una relación de confianza de dominio unidireccional: es decir, "Domain_2" no confía en "Domain_1", pero "Domain_1" confía en "Domain_2."  
  
3.  La instancia de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] para inscribirse en la utilidad de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] también es miembro de "Domain_1."  
  
4.  Durante la operación de inscripción, conéctese a la instancia de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] para inscribirse usando "sa". Especifique una cuenta de proxy de "Domain_2."  
  
5.  La validación se realiza correctamente, pero se produce un error de inscripción.  
  
 La solución para este problema, usando el ejemplo anterior, es conectar a la instancia de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] para inscribirse en la utilidad de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] usando "sa" y proporcionar una cuenta de proxy de "Domain_1."  
  
## <a name="failed-wmi-validation"></a>Error de validación de WMI  
 Si WMI no se configura correctamente en una instancia de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)], las operaciones de creación de UCP y de inscripción de instancia administrada muestran una advertencia, pero no se bloquea la operación. Además, si cambia el [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] configuración de la cuenta de agente para que [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] agente no tiene permiso para las clases WMI necesarias, recopilación de datos en la instancia administrada afectada de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] no se puede cargar en el UCP. Esto genera iconos deshabilitados en el UCP.  
  
 Un error de recopilación de datos genera iconos de estado deshabilitados en la vista de lista del UCP para las instancias administradas de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] afectadas. El historial de trabajos en la instancia administrada de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] muestra que sysutility_mi_collect_and_upload produce un error en el paso 2 (almacenaje temporal de los datos recopilados del script de PowerShell).  
  
 Los mensajes de error simplificados son:  
  
 La ejecución del comando se detuvo porque la variable del shell "ErrorActionPreference" esa establecida en Stop: Access denied.  
  
 ERROR: \<fecha y hora (MM/DD/AAAA HH: mm:) >: excepción al recopilar propiedades de la cpu.  Se podría haber producido un error en una consulta WMI.  ADVERTENCIA.  
  
 Para resolver este problema, compruebe la configuración siguiente:  
  
-   En Windows Server 2003, el servicio Agente SQL Server debe formar parte del grupo de supervisión de rendimiento de Windows en la instancia administrada de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)].  
  
-   El servicio WMI/IP debe estar habilitado y configurado en la instancia administrada de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)].  
  
-   El repositorio WMI podría estar dañado en la instancia administrada de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)].  
  
-   La biblioteca de rendimiento podría ser ausentes o dañados en la instancia administrada de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)].  
  
 Para comprobar que la instancia especificada de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] está configurada correctamente para notificar datos al UCP, compruebe que las siguientes clases están disponibles en la instancia especificada de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] y que son accesibles para la cuenta del servicio Agente SQL Server:  
  
-   Win32_MountPoint  
  
-   Win32_PerfRawData_PerfProc_Process  
  
-   Win32_PerfRawData_PerfOS_Processor  
  
-   Win32_Processor  
  
-   Win32_Volume  
  
-   Win32_LogicalDisk  
  
 Puede usar el cmdlet Get-WmiObject de PowerShell en cada una de las clases para comprobar que todas son accesibles. Ejecute los siguientes cmdlets en la instancia administrada de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]:  
  
```  
Get-WmiObject Win32_MountPoint -ErrorAction Stop | Out-Null  
Get-WmiObject Win32_PerfRawData_PerfProc_Process -ErrorAction Stop| Out-Null  
Get-WmiObject Win32_PerfRawData_PerfOS_Processor -ErrorAction Stop | Out-Null  
Get-WmiObject Win32_Processor -ErrorAction Stop | Out-Null  
Get-WmiObject Win32_Volume -ErrorAction Stop | Out-Null  
Get-WmiObject Win32_LogicalDisk -ErrorAction Stop | Out-Null  
```  
  
 Para obtener más información sobre la solución de problemas de WMI, vea [Solucionar problemas de WMI](http://go.microsoft.com/fwlink/?LinkId=178250). Observe que las consultas de estas operaciones de la Utilidad de SQL Server se ejecutan localmente, de modo que el DCOM y el contenido de la solución de problemas remota no se deben tener en cuenta.  
  
## <a name="failed-data-collection"></a>Error en la recopilación de datos  
 Si [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] eventos de recopilación de datos de utilidad producirá un error, tenga en cuenta las siguientes posibilidades:  
  
-   No cambie las propiedades del conjunto de recopilación "Información de la utilidad" en una instancia administrada de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]y no active ni desactive manualmente la recopilación de datos, ya que la recopilación de datos la controla un trabajo del agente de la Utilidad.  
  
-   Error de validación de WMI o validación de WMI no compatible. Para obtener más información, vea la sección sobre error de validación de WMI de este tema.  
  
-   Actualizar datos en la vista de lista de instancias administradas, como datos en [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] utilidad no se actualizan automáticamente. Para actualizar los datos, haga clic en el **instancias administradas** nodo en el **navegación del explorador de utilidad** panel, a continuación, seleccione **actualizar**, o haga doble clic en el [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] nombre de la vista de lista de la instancia y, después, seleccione **actualizar**. Tenga en cuenta que una vez se haya inscrito una instancia de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] con un UCP, pueden transcurrir hasta 30 minutos hasta que los datos aparezcan por vez primera en el panel y puntos de vista en el panel de contenido del explorador de la utilidad.  
  
-   Use el Administrador de configuración de SQL Server para comprobar que la instancia de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] se está ejecutando.  
  
-   Si se produjo un error de recopilación de datos o de carga de datos debido a problemas de tiempo de espera, actualice la función dbo.fn_sysutility_mi_get_collect_script() de la base de datos MSDB. Especialmente, en la función "Invoke-BulkCopyCommand()" agregue una línea:  
  
    ```  
    $bulkCopy.BulkCopyTimeout=180  
    ```  
  
     El valor predeterminado del tiempo de espera es de 30 segundos.  
  
-   Si la instancia de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] no se agrupa, compruebe que el servicio del Agente [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] se está ejecutando y que el servicio se establece para que se inicie de forma automática en el UCP y en la instancia administrada de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)].  
  
-   Compruebe que se usa para ejecutar la recopilación de datos en la instancia administrada de una cuenta válida de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]. Por ejemplo, la contraseña puede haber expirado. Si la contraseña del proxy ha expirado, actualice las credenciales de la contraseña en SSMS, tal como sigue:  
  
    1.  En el **Explorador de objetos**de SSMS, expanda el nodo **Seguridad** y el nodo **Credenciales** .  
  
    2.  Haga doble clic en **UtilityAgentProxyCredential_\<GUID >** y seleccione **propiedades**.  
  
    3.  En el cuadro de diálogo Propiedades de credencial, actualice las credenciales según sea necesario para la **UtilityAgentProxyCredential_\<GUID >** credencial.  
  
    4.  Haga clic en **Aceptar** para confirmar el cambio.  
  
-   TCP/IP debe estar habilitado en el UCP y en la instancia administrada de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]. Habilite TCP/IP a través de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Configuration Manager.  
  
-   Se debería iniciar el servicio SQL Server Browser en el UCP y se debería configurar para que se iniciara automáticamente. Si su organización impide el uso del servicio SQL Server Browser, siga los siguientes pasos para permitir que a una instancia administrada de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] se conecte al UCP:  
  
    1.  En la barra de tareas de Windows en la instancia administrada de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)], haga clic en **iniciar**, a continuación, haga clic en **ejecutar...** .  
  
    2.  Escriba "cliconfg.exe" en el espacio proporcionado y, a continuación, haga clic en **Aceptar**.  
  
    3.  Si se le solicita que permita el inicio del ejecutable de la utilidad de configuración del cliente SQL ("SQL Client Configuration Utility EXE"), haga clic en "**Continuar**".  
  
    4.  En el cuadro de diálogo **Herramienta de cliente de red de SQL Server** , seleccione la pestaña **Alias** y, a continuación, haga clic en **Agregar...**.  
  
    5.  En el cuadro de diálogo **Agregar configuración de biblioteca de red** :  
  
    6.  Especifique TCP/IP de la lista de bibliotecas de red.  
  
    7.  Especifique el nombreDeEquipo\nombreDeInstancia del UCP en el cuadro de texto **Alias del servidor** .  
  
    8.  Especifique el nombreDeEquipo del UCP en el cuadro de texto **Alias del servidor** .  
  
    9. Desactive la casilla **Determinar el puerto dinámicamente** .  
  
    10. Especifique el número de puerto que el UCP enumera en el cuadro de texto **Número de puerto** .  
  
    11. Haga clic en **Aceptar** para guardar los cambios.  
  
    12. Repita estos pasos para cada instancia administrada de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] que se conecta a un UCP donde no está habilitado el servicio SQL Server Browser.  
  
-   Asegúrese de que las instancias administradas de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] están conectados a la red.  
  
-   Si hay bases de datos con el mismo nombre pero con una configuración de distinción entre mayúsculas y minúsculas diferente en una instancia administrada de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)], puede que la identificación entre la base de datos y sus puntos de vista sea incorrecta, y se produzca un error de recopilación de datos. Por ejemplo, es posible que una base de datos denominada "MYDATABASE" muestre estados de mantenimiento para una base de datos con el nombre "MyDatabase". En esta situación no se producirán errores. Un error de recopilación de datos también puede ser consecuencia de la disparidad entre mayúsculas y minúsculas en otros objetos mostrados en el UCP, como el archivo de base de datos y los nombres de grupos de archivos.  
  
-   Si una instancia administrada de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] se hospeda en un equipo con Windows Server 2003, es preciso que la cuenta del servicio del Agente [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] pertenezca al grupo Usuarios del monitor del sistema o al grupo local Administradores. De lo contrario, se producirá un error en la recopilación de datos con un error de denegación del acceso. Para agregar un [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] cuenta de servicio del agente al grupo de seguridad usuarios del Monitor de rendimiento, siga estos pasos:  
  
    1.  Abra **Administración de equipos**, expanda **Usuarios y grupos locales**y haga clic en **Grupos**.  
  
    2.  Haga clic con el botón secundario en **Usuarios del monitor del sistema** y seleccione **Agregar a grupo**.  
  
    3.  Haga clic en **Agregar**.  
  
    4.  Escriba la cuenta que está ejecutando el servicio del Agente SQL Server y haga clic en **Aceptar**.  
  
    5.  Si la instancia de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] ya se ha inscrito con el UCP antes de agregar al usuario a este grupo, reinicie el servicio del Agente [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)].  
  
## <a name="see-also"></a>Vea también  
 [Características y tareas de la utilidad de SQL Server](../relational-databases/manage/sql-server-utility-features-and-tasks.md)   
 [Solucionar problemas de estado de recursos de SQL Server &#40;Utilidad de SQL Server&#41;](../relational-databases/manage/troubleshoot-sql-server-resource-health-sql-server-utility.md)  
  
  
