---
title: Actualizar PowerPivot para SharePoint | Documentos de Microsoft
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 80ba9e43-f3f0-4730-9fb1-2afd2dd3e6fc
caps.latest.revision: 13
author: markingmyname
ms.author: maghan
manager: jhubbard
ms.openlocfilehash: 8c052ff9ba3c1c568beb580f92ca15c94fcd55d5
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36199229"
---
# <a name="upgrade-powerpivot-for-sharepoint"></a>Actualizar PowerPivot para SharePoint
  En este tema se resumen los pasos necesarios para actualizar una implementación de [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] a [!INCLUDE[ssGeminiLong](../../includes/ssgeminilong-md.md)]. Los pasos específicos dependen de la versión de SharePoint que está ejecutando el entorno e incluyen el complemento PowerPivot para SharePoint (**spPowerPivot.msi**).  
  
 **[!INCLUDE[applies](../../includes/applies-md.md)]**  SharePoint 2010 | SharePoint 2013  
  
 Para obtener las notas de la versión, vea [Notas de la versión de SQL Server 2014](http://go.microsoft.com/fwlink/?LinkID=296445).  
  

  
## <a name="background"></a>Información previa  
  
-   Si va a actualizar una granja multiservidor de SharePoint 2010 que tiene dos o más instancias de [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] , debe actualizar totalmente cada servidor **antes** de continuar con el servidor siguiente. Una actualización completa incluye ejecutar el programa de instalación de SQL Server para actualizar los archivos de programa de [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] , seguido de acciones de actualización de SharePoint que configuran los servicios actualizados. Se limitará la disponibilidad del servidor hasta que ejecute las acciones de actualización en la Herramienta de configuración de PowerPivot o el comando de Windows PowerShell adecuado.  
  
-   Todas las instancias del Servicio de sistema de PowerPivot y Analysis Services de una granja de SharePoint 2010 tienen que ser de la misma versión. Para obtener información sobre cómo comprobar la versión, consulte la sección [Comprobar las versiones de los componentes y servicios de PowerPivot](#bkmk_verify_versions) en este tema.  
  
-   Las herramientas de configuración de PowerPivot son una de las características compartidas de SQL Server y todas las características compartidas se actualizan al mismo tiempo. Si durante un proceso de actualización selecciona otras instancias o características de SQL Server que necesitan la actualización de una característica compartida, la herramienta de configuración de PowerPivot también se actualizará. Puede tener problemas si se actualiza la herramienta de configuración de PowerPivot pero no la instancia de PowerPivot. Para obtener más información acerca de las características compartidas de SQL Server, vea [actualizar a SQL Server 2014 mediante el Asistente para la instalación &#40;el programa de instalación&#41;](../../database-engine/install-windows/upgrade-sql-server-using-the-installation-wizard-setup.md).  
  
-   El complemento PowerPivot para SharePoint (**spPowerPivot.msi**) se instala en paralelo con versiones anteriores. Por ejemplo, el complemento [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] se instala en la carpeta `c:\Program Files\Microsoft SQL Server\120\Tools\PowerPivotTools`.  
  

  
##  <a name="bkmk_prereq"></a> Requisitos previos  
 **Permisos**  
  
-   Debe ser administrador de granja para actualizar una instalación de PowerPivot para SharePoint. Debe ser administrador local para ejecutar el programa de instalación de SQL Server.  
  
-   Debe tener permisos **db_owner** en la base de datos de configuración de la granja.  
  
 **SQL Server:**  
  
-   Si la instalación existente de PowerPivot es [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)], [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] Service Pack 2 (SP2) es necesario para realizar una actualización a [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)].  
  
-   Si la instalación existente de PowerPivot es [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)], [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] Service Pack 1 (SP1) se requiere una actualización a [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)].  
  
 **SharePoint 2010:**  
  
-   Si la instalación existente ejecuta SharePoint 2010, instale SharePoint 2010 Service Pack 2 antes de realizar la actualización a [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)][!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)]. Para obtener más información, vea [Service Pack 2 para Microsoft SharePoint 2010](http://www.microsoft.com/download/details.aspx?id=39672). Use el comando `(Get-SPfarm).BuildVersion.ToString()` de PowerShell para comprobar la versión. Para saber la versión de compilación en la fecha de lanzamiento, vea [Números de compilación de SharePoint 2010](http://www.toddklindt.com/blog/Lists/Posts/Post.aspx?ID=224).  
  
 
  
##  <a name="bkmk_uprgade_sharepoint2013"></a> Actualizar una granja existente de SharePoint 2013  
 Para actualizar [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] implementado en SharePoint 2013, haga lo siguiente:  
  
 ![actualizar powerpivot para sharepoint 2013](../../../2014/sql-server/install/media/as-powepivot-upgrade-flow-sharepoint2013.png "actualizar powerpivot para sharepoint 2013")  
  
1.  Ejecute el programa de instalación de [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] en los servidores back-end que ejecutan [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] en modo de SharePoint. Si el servidor hospeda varias instancias de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)], actualice al menos la instancia de **POWERPIVOT** . La lista siguiente es un resumen de pasos del Asistente para la instalación relacionados con una actualización de [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] :  
  
    1.  En el Asistente para la instalación de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , haga clic en **Instalación**.  
  
    2.  Haga clic en **Actualizar desde SQL Server…..**.  
  
    3.  En la página **Seleccionar instancia** , seleccione el nombre de instancia **POWERPIVOT** y, a continuación, haga clic en **Siguiente**.  
  
    4.  Para obtener más información, consulte [actualizar a SQL Server 2014 mediante el Asistente para la instalación &#40;el programa de instalación&#41;](../../database-engine/install-windows/upgrade-sql-server-using-the-installation-wizard-setup.md)  
  
2.  Reinicie el servidor.  
  
3.  Ejecute el complemento [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] para SharePoint (**spPowerPivot.msi**) en todos los servidores de la granja de SharePoint 2013 para instalar los proveedores de datos. La excepción está en los servidores donde se ejecutó el Asistente para la instalación de SQL Server, que también actualiza los proveedores de datos. Para obtener más información, consulte [descargar Microsoft SQL Server 2014 PowerPivot para Microsoft SharePoint 2013,](http://www.microsoft.com/download/details.aspx?id=40737) y [instalar o desinstalar PowerPivot para SharePoint Add- &#40;SharePoint 2013&#41; ](../../analysis-services/instances/install-windows/install-or-uninstall-the-power-pivot-for-sharepoint-add-in-sharepoint-2013.md).  
  
4.  **Ejecute la herramienta de configuración de PowerPivot para SharePoint 2013** en uno de los servidores de aplicaciones de SharePoint para configurar la granja de servidores de SharePoint con los archivos de solución actualizados que el complemento instaló. No puede usar Administración central de SharePoint para este paso. Para obtener más información, vea:  
  
    1.  En la página Inicio de Windows, escriba **PowerPivot** y después, en los resultados de la búsqueda, haga clic en **Configuración de PowerPivot para SharePoint 2013**. Tenga en cuenta la búsqueda puede devolver ambas versiones de la herramienta de configuración.  
  
         ![dos herramientas de configuración de PowerPivot](../../../2014/analysis-services/media/as-powerpivot-configtools-bothicons.gif "dos herramientas de configuración de PowerPivot")  
  
         o bien  
  
         En el **iniciar** menú, elija **todos los programas**, haga clic en [!INCLUDE[ssCurrentUI](../../includes/sscurrentui-md.md)], haga clic en **herramientas de configuración**y, a continuación, haga clic en **PowerPivot para SharePoint 2013 Configuración demasiado**. Observe que esta herramienta solo se enumera cuando [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] está instalado en el servidor local.  
  
    2.  Al iniciarse, la herramienta de configuración comprueba el estado de actualización de la solución de granja de PowerPivot y las soluciones de aplicación web de PowerPivot. Si se detectan versiones anteriores de estas soluciones, verá el mensaje "**Se han detectado versiones más recientes de los archivos de solución de PowerPivot. Seleccione la opción de actualización para actualizar la granja**". Haga clic en **Aceptar** para cerrar el mensaje de validación del sistema.  
  
    3.  Haga clic en **Actualizar características, servicios, aplicaciones y soluciones**y, a continuación, haga clic en **Aceptar**.  
  
    4.  Revise las acciones de la lista de tareas del panel izquierdo y excluya las que no desea que realice la herramienta. Todas las acciones se incluyen de forma predeterminada. Para quitar una acción, selecciónela en la lista de tareas de la izquierda y, a continuación, en la página **Parámetros** , desactive la casilla **Incluir esta acción en la lista de tareas** .  
  
    5.  También puede revisar información detallada en la pestaña **Script** o en la pestaña **Salida** .  
  
         La pestaña Salida es un resumen de las acciones que realizará la herramienta. Esta información se guarda en archivos de registro en `C:\Program Files\Microsoft SQL Server\120\Tools\PowerPivotTools\SPAddinConfiguration\Log`.  
  
         La pestaña Script muestra los cmdlets de PowerShell o hace referencia a los archivos de script de PowerShell que la herramienta ejecutará.  
  
    6.  Haga clic en **Validar** para comprobar si cada acción es válida. Si la opción **Validar** no está disponible, significa que todas las acciones son válidas para el sistema. Si la opción **Validar** está disponible, puede que haya modificado un valor de entrada (por ejemplo, el nombre de aplicación de servicios de Excel), o que la herramienta haya determinado que una acción determinada no se puede realizar. Si una acción no se puede realizar, debe excluirla o corregir las condiciones subyacentes que hacen que la acción se indique como no válida.  
  
        > [!IMPORTANT]  
        >  La primera acción, **Actualizar solución de granja**, siempre se debe procesar primero. Registra los cmdlets de PowerShell que se utilizan para configurar el servidor. Si obtiene un error en esta acción, no debe continuar. En su lugar, utilice la información proporcionada por el error para diagnosticar y resolver el problema antes de procesar acciones adicionales en la lista de tareas.  
  
    7.  Haga clic en **Ejecutar** para realizar todas las acciones válidas para esta tarea. La opción**Ejecutar** solo está disponible si se supera la comprobación de validación. Cuando se hace clic en **Ejecutar**, aparece la advertencia siguiente recordándole que las acciones se procesan en modo por lotes: "**Todos los parámetros de configuración que se indican como válidos en la herramienta se aplicarán a la granja de SharePoint. ¿Quiere continuar?**".  
  
    8.  Haga clic en **Sí** para continuar.  
  
    9. La actualización de soluciones y características de la granja puede tardar varios minutos en completarse. Durante este tiempo, las solicitudes de conexión para los datos PowerPivot **se producirá un error** con errores similares a "**no se pueden actualizar datos**"o"**un error al intentar realizar la acción solicitada. Inténtelo de nuevo**". Una vez finalizada la actualización, el servidor estará disponible y estos errores ya no se producirán.  
  
     Para obtener más información, vea:  
  
    -   [Herramientas de configuración de PowerPivot](../../analysis-services/power-pivot-sharepoint/power-pivot-configuration-tools.md)  
  
    -   [Configurar o reparar PowerPivot para SharePoint 2013 &#40;herramienta de configuración de PowerPivot&#41;](../../analysis-services/power-pivot-sharepoint/configure-or-repair-power-pivot-for-sharepoint-2013.md)  
  
    -   [Configuración de PowerPivot mediante Windows PowerShell](../../analysis-services/power-pivot-sharepoint/power-pivot-configuration-using-windows-powershell.md)  
  
    -   [Referencia de PowerShell para PowerPivot para SharePoint](/sql/analysis-services/powershell/powershell-reference-for-power-pivot-for-sharepoint)  
  
5.  Para comprobar que la actualización se efectuó correctamente, ejecute los pasos posteriores a la actualización y compruebe la versión de los servidores de PowerPivot en la granja de servidores. Para obtener más información, vea [Post-upgrade verification tasks](#verify) en este tema y la siguiente sección:  
  
 
  
##  <a name="bkmk_uprgade_sharepoint2010"></a> Actualizar una granja existente de SharePoint 2010  
 Para actualizar [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] implementado en SharePoint 2010, haga lo siguiente:  
  
 ![actualizar powerpivot para sharepoint 2010](../../../2014/sql-server/install/media/as-powepivot-upgrade-flow-sharepoint2010.png "actualizar powerpivot para sharepoint 2010")  
  
1.  Descargue [Service Pack 2 para Microsoft SharePoint 2010](http://www.microsoft.com/download/details.aspx?id=39672) y aplíquelo en todos los servidores de la granja. Compruebe que la instalación de SharePoint SP2 se ha realizado correctamente. En Administración central, en la página Actualización y migración, abra la página Verificar el estado de la instalación de productos y revisiones para ver el estado de los mensajes relacionados con SP2.  
  
2.  Compruebe que el servicio de Windows Administración de SharePoint 2010 está en ejecución.  
  
    ```  
    Get-Service | where {$_.displayname -like "*SharePoint*"}  
    ```  
  
3.  Compruebe que los servicios de **SharePoint** **SQL Server Analysis Services** y **Servicio de sistema de SQL Server PowerPivot** se han iniciado en Administración central de SharePoint o use el siguiente comando de PowerShell:.  
  
    ```  
    get-SPserviceinstance | where {$_.typename -like "*sql*"}  
    ```  
  
4.  Compruebe que el servicio de **Windows** **SQL Server Analysis Services (PowerPivot)** se está ejecutando.  
  
    ```  
    Get-Service | where {$_.displayname -like "*powerpivot*"}  
    ```  
  
5.  **Ejecutar [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] el programa de instalación** en el primer servidor de aplicaciones de SharePoint que se ejecuta el **SQL Server Analysis Services (PowerPivot)** servicio de Windows para actualizar la instancia POWERPIVOT. En la página Instalación del Asistente para la instalación de SQL Server, elija la opción de actualización. Para obtener más información, consulte [actualizar a SQL Server 2014 mediante el Asistente para la instalación &#40;el programa de instalación&#41;](../../database-engine/install-windows/upgrade-sql-server-using-the-installation-wizard-setup.md).  
  
6.  **Reinicie el servidor** antes de ejecutar la herramienta de configuración. Este paso garantizará que las actualizaciones o requisitos previos instalados con el programa de instalación de SQL Server se configuren totalmente en el sistema.  
  
7.  **Ejecute la herramienta de configuración de PowerPivot** en el primer servidor de aplicaciones de SharePoint que ejecuta el servicio de SQL Server Analysis Services (PowerPivot) para actualizar las soluciones y servicios Web de SharePoint. No puede utilizar Administración Central para este paso.  
  
    1.  En el **iniciar** menú, elija **todos los programas**, haga clic en [!INCLUDE[ssCurrentUI](../../includes/sscurrentui-md.md)], haga clic en **herramientas de configuración**y, a continuación, haga clic en **herramienta de configuración de PowerPivot** . Observe que esta herramienta solo se enumera cuando [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] está instalado en el servidor local.  
  
    2.  Al iniciarse, la herramienta de configuración comprueba el estado de actualización de la solución de granja de PowerPivot y las soluciones de aplicación web de PowerPivot. Si se detectan versiones anteriores de estas soluciones, verá el mensaje "Se han detectada versiones más recientes de los archivos de solución de PowerPivot. Seleccione la opción de actualización para actualizar la granja". Haga clic en **Aceptar** para cerrar el mensaje.  
  
    3.  Haga clic en **Actualizar características, servicios, aplicaciones y soluciones**y, a continuación, haga clic en **Aceptar** para continuar.  
  
    4.  Aparece la advertencia siguiente: "Los libros del Panel de administración de PowerPivot van a actualizarse a la última versión. Se perderán las personalizaciones realizadas en los libros existentes. ¿Desea continuar?"  
  
         Esta advertencia se refiere a los libros del Panel de administración de PowerPivot que informan sobre la actividad de actualización de datos. Si ha personalizado estos libros, los cambios realizados en ellos se perderán cuando los archivos existentes se reemplacen con versiones más recientes.  
  
         Haga clic en **Sí** para sobrescribir los libros con versiones más recientes. De lo contrario, haga clic en **No** para volver a la página principal. Guarde los libros en una ubicación diferente para tener una copia y vuelva a este paso cuando esté listo para continuar.  
  
         Para obtener más información acerca de cómo personalizar los libros utilizados en el panel, vea el tema que explica [cómo personalizar el Panel de administración de PowerPivot](http://go.microsoft.com/fwlink/?linkID=229639).  
  
    5.  Revise las acciones de la lista de tareas y excluya las que no desea que la herramienta realice. Todas las acciones se incluyen de forma predeterminada. Para quitar una acción, selecciónela en la lista de tareas y, a continuación, desactive la casilla **Incluir esta acción en la lista de tareas** en la página Parámetros.  
  
    6.  También puede revisar información detallada en la pestaña **Salida** o en la pestaña **Script** .  
  
         La pestaña Salida es un resumen de las acciones que realizará la herramienta. Esta información se guarda en archivos de registro en `c:\Program Files\Microsoft SQL Server\120\Tools\PowerPivotTools\ConfigurationTool\Log`.  
  
         La pestaña Script muestra los cmdlets de PowerShell o hace referencia a los archivos de script de PowerShell que la herramienta ejecutará.  
  
    7.  Haga clic en **Validar** para comprobar si cada acción es válida. Si la opción **Validar** no está disponible, significa que todas las acciones son válidas para el sistema. Si la opción **Validar** está disponible, puede que haya modificado un valor de entrada (por ejemplo, el nombre de aplicación de servicios de Excel), o que la herramienta haya determinado que una acción determinada no se puede realizar. Si una acción no se puede realizar, debe excluirla o corregir las condiciones subyacentes que hacen que la acción se indique como no válida.  
  
        > [!IMPORTANT]  
        >  La primera acción, **Actualizar solución de granja**, siempre se debe procesar primero. Registra los cmdlets de PowerShell que se utilizan para configurar el servidor. Si obtiene un error en esta acción, no debe continuar. En su lugar, utilice la información proporcionada por el error para diagnosticar y resolver el problema antes de procesar acciones adicionales en la lista de tareas.  
  
    8.  Haga clic en **Ejecutar** para realizar todas las acciones válidas para esta tarea. La opción**Ejecutar** solo está disponible si se supera la comprobación de validación. Cuando se hace clic en **Ejecutar**, aparece la advertencia siguiente recordándole que las acciones se procesan en modo por lotes: “Todos los parámetros de configuración que se indican como válidos en la herramienta se aplicarán a la granja de SharePoint. ¿Desea continuar?"  
  
    9. Haga clic en **Sí** para continuar.  
  
    10. La actualización de soluciones y características de la granja puede tardar varios minutos en completarse. Durante este período de tiempo, las solicitudes de conexión para los datos PowerPivot darán error con errores tales como “No se pueden actualizar datos” o “Se ha producido un error al intentar realizar la acción solicitada. Inténtelo de nuevo". Una vez finalizada la actualización, el servidor estará disponible y estos errores ya no se producirán.  
  
8.  **Repita el proceso** para cada servicio de SQL Server Analysis Services (PowerPivot) en la granja de servidores: el programa de instalación de 1) ejecute SQL Server 2) ejecute la herramienta de configuración de PowerPivot.  
  
9. Para comprobar que la actualización se efectuó correctamente, ejecute los pasos posteriores a la actualización y compruebe la versión de los servidores de PowerPivot en la granja de servidores. Para obtener más información, vea [Post-upgrade verification tasks](#verify) en este tema y la siguiente sección:  
  
10. **Solucionar errores**  
  
     Puede ver la información de error en el panel Parámetros para cada acción.  
  
     Para los problemas relacionados con la implementación o la retracción de soluciones, compruebe que se ha iniciado el servicio Administrador de SharePoint 2010 . Este servicio ejecuta los trabajos de temporizador que desencadenan cambios de configuración en una granja. Si el servicio no se está ejecutando, la implementación o la retracción de soluciones producirá un error. Los errores persistentes indican que un trabajo existente de implementación o de retracción ya está en la cola y está bloqueando la acción posterior de la herramienta de configuración.  
  
    1.  Inicie el Shell de administración de SharePoint 2010 como administrador y ejecute el siguiente comando para ver los trabajos de la cola:  
  
        ```  
        Stsadm –o enumdeployments  
        ```  
  
    2.  Revise las implementaciones existentes para la siguiente información: **Tipo** es Retracción o Implementación, **Archivo** es powerpivotwebapp.wsp o powerpivotfarm.wsp.  
  
    3.  En las implementaciones o las retracciones relacionadas con soluciones de PowerPivot, copie el valor GUID para **JobId** y péguelo en el siguiente comando (utilice los comandos Marcar, Copiar y Pegar del menú Edición del shell para copiar el GUID):  
  
        ```  
        Stsadm –o canceldeployment –id “<GUID>”  
        ```  
  
    4.  Intente de nuevo la tarea en la herramienta de configuración haciendo clic en **Validar** seguido de **Ejecutar**.  
  
     Para todos los demás errores, compruebe los registros ULS. Para obtener más información, consulte [configurar y ver archivos de registro de SharePoint y el registro de diagnósticos &#40;PowerPivot para SharePoint&#41;](../../analysis-services/power-pivot-sharepoint/configure-and-view-sharepoint-and-diagnostic-logging.md).  
  

  
##  <a name="bkmk_workbooks"></a> Libros  
 Al actualizar un servidor, no se actualizan necesariamente los libros PowerPivot que se ejecutan en él, pero los libros anteriores creados en la versión anterior de PowerPivot para Excel continuarán funcionando como antes y utilizando las características disponibles en esa versión. Los libros permanecen funcionales porque un servidor actualizado tiene la versión del proveedor OLE DB de Analysis Services que formaba parte de la instalación anterior.  
  
  
  
##  <a name="bkmk_datarefresh"></a> Actualización de datos  
 La actualización afectará a las operaciones de actualización de datos. La actualización de datos programada en el servidor solo está disponible para los libros que coincidan con la versión del servidor. Si hospeda libros de la versión anterior, puede que la actualización de datos ya no funcione para dichos libros. Para volver a habilitar la actualización de datos, debe actualizar los libros. Puede actualizar cada libro manualmente en PowerPivot para Excel o bien puede habilitar la actualización automática para la característica de actualización de datos en SharePoint 2010. Con la actualización automática, se actualizará un libro a la versión anterior a la ejecución de la actualización de datos, lo que permite que se continúe la programación de las operaciones de actualización de datos.  
  

  
##  <a name="bkmk_verify_versions"></a> Comprobar las versiones de servicios y componentes de PowerPivot  
 Todas las instancias del Servicio de sistema de [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] y Analysis Services tienen que ser de la misma versión. Para comprobar que todos los componentes del servidor tienen la misma versión después, compruebe lo siguiente en la información de la versión:  
  
### <a name="verify-the-version-of-powerpivot-solutions-and-the-powerpivot-system-service"></a>Comprobar la versión de las soluciones de PowerPivot y del Servicio de sistema de PowerPivot  
 Ejecute el siguiente comando de PowerShell:  
  
```  
Get-PowerPivotSystemService  
```  
  
 Compruebe **CurrentSolutionVersion**. [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] es la versión 12.0. \<compilación principal >. \<compilación secundaria >  
  
### <a name="verify-the-version-of-the-analysis-services-windows-service"></a>Comprobar la versión del servicio de Windows Analysis Services  
 Si solo actualizó alguno de los servidores [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] de una granja de SharePoint 2010, la instancia de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] en los servidores sin actualizar será anterior a la de la versión esperada en la granja. Necesitará actualizar todos los servidores a la misma versión para que puedan utilizarse. Utilice uno de los métodos siguientes para comprobar la versión del servicio de Windows de SQL Server Analysis Services (PowerPivot) en cada equipo.  
  
 **Explorador de archivos de Windows**:  
  
1.  Navegue hasta la carpeta **Bin** para la instancia de [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] . Por ejemplo, `C:\Program Files\Microsoft SQL Server\MSAS12.POWERPIVOT\OLAP\bin`.  
  
2.  Haga clic con el botón derecho en `msmdsrv.exe`y seleccione **Propiedades**.  
  
3.  Haga clic en **Detalles**.  
  
4.  [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] versión del archivo debe ser 12.00. \<compilación principal >. \<compilación secundaria >.  
  
5.  Compruebe que este número es idéntico a la versión de la solución y del servicio de sistema de PowerPivot.  
  
 **Información de inicio del servicio:**  
  
 Cuando el servicio PowerPivot se inicia, escribe la información de versión en el registro de eventos de Windows.  
  
1.  Ejecute Windows `eventvwr`  
  
2.  Cree un filtro para el origen `MSOLAP$POWERPIVOT`.  
  
3.  Busque un evento de nivel de información similar al siguiente  
  
     Se ha iniciado el servicio  de . Microsoft SQL Server Analysis Services de 64 bits evaluación (x64) RTM **12.0.2000.8**.  
  
 **Use PowerShell para comprobar la versión del archivo.**  
  
 Puede usar PowerShell para comprobar la versión del producto. PowerShell es una buena opción si desea incluir en un script o automatizar la comprobación de la versión.  
  
```  
(get-childitem "C:\Program Files\Microsoft SQL Server\MSAS12.POWERPIVOT2000\OLAP\bin\msmdsrv.exe").VersionInfo  
```  
  
 El comando PowerShell anterior devuelve información similar a la siguiente:  
  
 ProductVersion   FileVersion           FileName  
  
 **12.0.2000.8** 2014.0120.200    C:\Archivos de programa\Microsoft SQL Server\MSAS12.POWERPIVOT2000\OLAP\bin\msmdsrv.exe  
  
### <a name="verify-the-msolap-data-provider-version-on-sharepoint"></a>Comprobar la versión del proveedor de datos MSOLAP en SharePoint  
 Utilice las siguientes instrucciones para comprobar qué versiones de los proveedores OLE DB de Analysis Services son de confianza en Excel Services. Debe ser administrador de las aplicaciones de servicio o de una granja para comprobar la configuración del proveedor de datos de confianza de Excel Services.  
  
1.  En Administración central, en Administración de aplicaciones, haga clic en **Administrar aplicaciones de servicio**.  
  
2.  Haga clic en el nombre de la aplicación de servicio Excel Services; por ejemplo, **ExcelServiceApp1**.  
  
3.  Haga clic en **Proveedores de datos de confianza**. Debe ver MSOLAP.5 (Proveedor OLE DB de Microsoft para OLAP Services 11.0). Si actualizó la instalación de [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] , también verá MSOLAP.4 de la versión anterior.  
  
4.  Para obtener más información, vea [Add MSOLAP.5 as a Trusted Data Provider in Excel Services](../../analysis-services/power-pivot-sharepoint/add-msolap-5-as-a-trusted-data-provider-in-excel-services.md).  
  
 MSOLAP.4 se describe como el proveedor Microsoft OLE DB para OLAP Services 10.0. Esta versión podría ser la predeterminada de [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] que se instala con Excel Services o podría ser la versión de [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] . La versión predeterminada que SharePoint instala no admite el acceso a datos PowerPivot. Debe tener la versión de [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] o posterior para conectarse a los libros PowerPivot en SharePoint. Para comprobar que tiene la versión de [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] , utilice las instrucciones de la sección anterior que explican cómo comprobar la versión viendo las propiedades del archivo.  
  
### <a name="verify-the-adomdnet-data-provider-version"></a>Comprobar la versión del proveedor de datos ADOMD.NET  
 Use las instrucciones siguientes para comprobar la versión de ADOMD.NET instalada. Debe ser administrador de las aplicaciones de servicio o de una granja para comprobar la configuración del proveedor de datos de confianza de Excel Services.  
  
1.  En el servidor de aplicaciones de SharePoint, vaya a `c:\Windows\Assembly`.  
  
2.  Ordene por nombre del ensamblado y busque **Microsoft.Analysis Services.Adomd.Client**.  
  
3.  Compruebe que tiene la versión 12.0. \<número de compilación >.  
  
  
  
##  <a name="geminifarm"></a> Actualizar varios PowerPivot para servidores de SharePoint en una granja de SharePoint  
 En una topología multiservidor que incluya más de un servidor [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] , todas las instancias y componentes del servidor deben ser de la misma versión. El servidor que ejecuta la versión más reciente del software establece el nivel para todos los servidores de la granja. Si simplemente actualiza algunos de los servidores, los que ejecuten versiones anteriores del software dejarán de estar disponibles hasta que también se actualicen.  
  
 Después de actualizar el primer servidor, los servidores adicionales que aún no se hayan actualizado **dejarán de estar disponibles**. La disponibilidad se restaura una vez que todos los servidores se ejecutan en el mismo nivel.  
  
 El programa de instalación de SQL Server actualiza los archivos de solución de PowerPivot en el equipo físico, pero para actualizar las soluciones que se usan en la granja debe usar la Herramienta de configuración de PowerPivot que de describe en una sección anterior de este tema.  
  
 
  
##  <a name="qfe"></a> Aplicar un QFE a una instancia de PowerPivot en la granja de servidores  
 Al aplicar una revisión a un servidor PowerPivot para SharePoint, se actualizan los archivos de programa existentes con una versión más reciente que incluye la corrección de un problema concreto. Al aplicar un QFE a una topología multi-servidor, no hay ningún servidor principal con el que deba comenzar. Puede empezar con cualquier servidor, siempre que aplique el mismo QFE a los demás servidores PowerPivot de la granja.  
  
 Al aplicar el QFE, también debe realizar un paso de configuración que actualiza la información de versión del servidor en la base de datos de configuración de la granja. La versión del servidor al que se aplicó la revisión pasa a ser la nueva versión que se espera para la granja. Hasta que el QFE se aplique y configure en todos los equipos, las instancias de PowerPivot para SharePoint que no tienen el QFE no podrán atender solicitudes de datos de PowerPivot.  
  
 Para asegurarse de que el QFE se aplica y configura correctamente, siga estas instrucciones:  
  
1.  Instale la revisión usando las instrucciones que se proporcionan con el QFE.  
  
2.  Inicie la Herramienta de Configuración de PowerPivot.  
  
3.  Haga clic en **Actualizar características, servicios, aplicaciones y soluciones**y, a continuación, haga clic en **Aceptar**.  
  
4.  Revise las acciones que se incluyen en la tarea de actualización y haga clic en **Validar**.  
  
5.  Haga clic en **Ejecutar** para aplicar las acciones.  
  
6.  Repita esos pasos para las instancias adicionales de PowerPivot para SharePoint de la granja.  
  
    > [!IMPORTANT]  
    >  En una implementación multiservidor, asegúrese de aplicar la revisión y configurar cada instancia antes de continuar con el equipo siguiente. La Herramienta de configuración de PowerPivot debe completar la tarea de actualización de la instancia actual antes de pasar a la instancia siguiente.  
  
 Para comprobar la información de versión de los servicios de la granja de servidores, use la página **Verificar el estado de la instalación de productos y revisiones** en la sección Administración de actualizaciones y revisiones de Administración central.  
  
##  <a name="verify"></a> Tareas de comprobación posteriores a la actualización  
 Una vez completada la actualización, use los siguientes pasos para comprobar si el servidor está operativo.  
  
|Tarea|Vínculo|  
|----------|----------|  
|Compruebe que el servicio se está ejecutando en todos los equipos que ejecutan PowerPivot para SharePoint.|[Iniciar o detener un PowerPivot para SharePoint Server](../../analysis-services/power-pivot-sharepoint/start-or-stop-a-power-pivot-for-sharepoint-server.md)|  
|Comprobar la activación de las características en el nivel de colección de sitios.|[Activar la integración de características de PowerPivot para colecciones de sitios en Administración Central](../../analysis-services/power-pivot-sharepoint/activate-power-pivot-integration-for-site-collections-in-ca.md)|  
|Compruebe que los libros PowerPivot individuales están cargados correctamente abriendo un libro y haciendo clic en los filtros y segmentaciones para iniciar una consulta.|Compruebe si hay archivos almacenados en la memoria caché del disco duro. Si hay un archivo almacenado en memoria caché, se confirma que el archivo de datos se cargó en ese servidor físico. Busque los archivos almacenados en caché en la carpeta c:\Archivos de programa\Microsoft SQL Server\MSAS12.POWERPIVOT\OLAP\Backup.|  
|Pruebe la actualización de datos en los libros seleccionados que estén configurados para la actualización de datos.|La manera más fácil de probar la actualización de datos consiste en modificar una programación de actualización de datos y activar la casilla **También actualizar lo más rápido posible** de modo que la actualización de datos se ejecute inmediatamente. Este paso determinará si la actualización de datos es correcta para el libro actual. Repita estos pasos en otros libros de uso frecuente para asegurarse de que la actualización de datos funciona. Para obtener más información sobre la programación de datos de una actualización, vea [programar una actualización de datos &#40;PowerPivot para SharePoint&#41;](../../../2014/analysis-services/schedule-a-data-refresh-powerpivot-for-sharepoint.md).|  
|A lo largo del tiempo, supervise los informes de actualización de datos en el Panel de administración de PowerPivot para confirmar que no se produjo ningún error en la actualización de datos.|[Panel de administración de PowerPivot y datos de uso](../../analysis-services/power-pivot-sharepoint/power-pivot-management-dashboard-and-usage-data.md)|  
  
 Para obtener más información acerca de cómo configurar opciones de PowerPivot y características, vea [administración del servidor de PowerPivot y configuración en Administración Central](../../analysis-services/power-pivot-sharepoint/power-pivot-server-administration-and-configuration-in-central-administration.md).  
  
 Para obtener instrucciones paso a paso que le guían a través de todas las tareas de configuración posteriores a la instalación, consulte [configuración inicial &#40;PowerPivot para SharePoint&#41;](../../../2014/sql-server/install/initial-configuration-powerpivot-for-sharepoint.md).  
  

  
## <a name="see-also"></a>Vea también  
 [Características compatibles con las ediciones de SQL Server 2014](../../../2014/getting-started/features-supported-by-the-editions-of-sql-server-2014.md)   
 [PowerPivot para SharePoint 2010](../../../2014/sql-server/install/powerpivot-for-sharepoint-2010-installation.md)  
  
  
