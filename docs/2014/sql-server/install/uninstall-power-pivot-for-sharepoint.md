---
title: Desinstalar PowerPivot para SharePoint | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: install
ms.topic: conceptual
ms.assetid: 3941a2f0-0d0c-4d1a-8618-7a6a7751beac
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: 9397dd268d767fd8c4bad9056455c21b9be65398
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/03/2018
ms.locfileid: "52769777"
---
# <a name="uninstall-powerpivot-for-sharepoint"></a>Desinstalar PowerPivot para SharePoint
  Desinstalar una instalación de [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] es una operación de varios pasos que incluye la preparación para desinstalar, quitar características y soluciones de la granja de servidores, y quitar archivos de programa y valores del Registro.  
  
 **[!INCLUDE[applies](../../includes/applies-md.md)]**  SharePoint 2013 | SharePoint 2010  
  
 **En este tema:**  
  
-   [Requisitos previos](#prereq)  
  
-   [Paso 1: Lista de comprobación previa a la desinstalación](#bkmk_before)  
  
-   [Paso 2: Quitar características y soluciones de SharePoint](#bkmk_remove)  
  
-   [Paso 3: Ejecute el programa de instalación SQL Server para quitar programas del equipo Local](#bkmk_uninstall)  
  
-   [Paso 4: Desinstalar PowerPivot para SharePoint complemento](#bkmk_addin)  
  
-   [Paso 5: Comprobar la desinstalación](#verify)  
  
-   [Paso 6: Lista de comprobación posteriores a la desinstalación](#bkmk_post)  
  
##  <a name="prereq"></a> Requisitos previos  
  
-   Debe ser administrador de la granja de servidores de SharePoint o administrador de aplicaciones de servicio para desinstalar características y soluciones de la granja de servidores.  
  
-   Debe ser administrador de sistema de SQL Server y miembro del grupo local Administradores si va a desinstalar también el Motor de base de datos.  
  
-   Debe ser administrador del sistema de Analysis Services y miembro del grupo local Administradores para desinstalar Analysis Services y [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)].  
  
##  <a name="bkmk_before"></a> Paso 1: Lista de comprobación previa a la desinstalación  
 El acceso a datos de PowerPivot se deshabilitará una vez que se quite de la granja de servidores el software que admite las consultas y el procesamiento de datos. Como un primer paso, debe eliminar de forma preferente los archivos y bibliotecas que dejarán de funcionar. Esto permite resolver cualquier duda o preocupación sobre la "ausencia de datos" antes de desinstalar el software.  
  
1.  Elimine todos los libros PowerPivot, documentos y bibliotecas que estén asociados con PowerPivot para SharePoint. Ni las bibliotecas ni los documentos funcionarán una vez se desinstale el software.  
  
    -   [Eliminar la Galería de PowerPivot](../../analysis-services/power-pivot-sharepoint/delete-power-pivot-gallery.md)  
  
    -   [Eliminar una biblioteca de fuente de distribución de datos PowerPivot](../../analysis-services/power-pivot-sharepoint/delete-a-power-pivot-data-feed-library.md)  
  
2.  Elimine los libros de Excel o los informes de Reporting Services de otras bibliotecas que contengan o hagan referencia a datos PowerPivot.  
  
3.  Elimine cualquier elemento web de un panel de PerformancePoint que haga referencia a datos PowerPivot.  
  
4.  Revise los permisos de SharePoint de los sitios y bibliotecas existentes para determinar si necesita cambiarlos. Algunos escenarios de acceso a datos PowerPivot, particularmente el acceso a datos secundarios a través de una cadena de conexión URL a los datos de PowerPivot de otro libro, requieren permisos de lectura, que son superiores a los permisos de vista que se asignan normalmente a los usuarios de SharePoint que solo visitan un sitio. Si ya no necesita permisos de lectura, puede reducirlos del modo correspondiente.  
  
5.  Si lo desea, puede detener los servicios y esperar varios días antes de desinstalar el software. Este paso no es necesario para la desinstalación, pero le ofrece la posibilidad de reanudar el servicio temporalmente mientras resuelve los problemas de migración de datos o sustituciones tecnológicas que podría haber pasado por alto.  
  
##  <a name="bkmk_remove"></a> Paso 2: Quitar características y soluciones de SharePoint  
 Use la Herramienta de configuración de PowerPivot para quitar servicios y aplicaciones PowerPivot de SharePoint.  
  
-   Debe ser administrador de granja, administrador de servidor de la instancia de Analysis Services y **db_owner** en la base de datos de configuración de la granja.  
  
-   Utilice la versión adecuada de la herramienta de configuración de la versión de SharePoint. No use la herramienta con instalaciones de [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] .  
  
-   Compruebe que se ejecuta el servicio de administración de SharePoint.  
  
1.  **Ejecute la herramienta de configuración:** Tenga en cuenta las herramientas de configuración se muestran solo cuando [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] está instalado en el servidor local. En el **iniciar** menú, elija **todos los programas**, haga clic en [!INCLUDE[ssCurrentUI](../../includes/sscurrentui-md.md)], haga clic en **herramientas de configuración**y, a continuación, haga clic en uno de los siguientes:  
  
    -   **PowerPivot para SharePoint 2013**  
  
    -   **Herramienta de configuración de PowerPivot**  
  
2.  Seleccione **Quitar características, servicios, aplicaciones y soluciones** y haga clic en **Aceptar**.  
  
3.  También puede ampliar la ventana al tamaño máximo. Aparecerá una barra de botones en la parte inferior de la ventana con los comandos **Validar** **Ejecutar**y **Salir** .  
  
4.  Revise cada acción de la lista de tareas para entender lo que realiza cada una.  
  
     En **Quitar aplicaciones de servicio PowerPivot**, se le ofrece la opción de eliminar los datos de aplicación asociados a la aplicación de servicio. Los datos de aplicación son una base de datos de SQL Server que se creó con la aplicación de servicio con el fin de almacenar programaciones de actualización de datos, información de la base de datos, datos de uso y otros datos utilizados por PowerPivot para SharePoint. No almacenan los archivos de usuario, como libros PowerPivot. A menos que tenga una razón concreta para mantener los datos de aplicación (por ejemplo, si tiene directivas de retención de datos relacionadas con la actualización de datos o el acceso a datos) puede eliminar la base de datos de aplicación sin quitar los archivos creados o guardados por los usuarios de SharePoint.  
  
     Para eliminar la base de datos, seleccione **Quitar aplicaciones de servicio PowerPivot** y seleccione **Eliminar los datos de aplicación asociados con esta aplicación de servicio**.  
  
5.  También puede revisar información detallada en la pestaña **Salida** o en la pestaña **Script** .  
  
     La pestaña Salida es un resumen de las acciones que realizará la herramienta. Esta información se guarda en archivos de registro en:  
  
     `C:\Program Files\Microsoft SQL Server\120\Tools\PowerPivotTools\SPAddinConfiguration\Log`  
  
     La pestaña Script muestra los cmdlets de PowerShell o hace referencia a los archivos de script de PowerShell que la herramienta ejecutará.  
  
6.  Haga clic en **Validar** para comprobar si cada acción es válida. Si la opción **Validar** no está disponible, significa que todas las acciones son válidas para el sistema.  
  
7.  Haga clic en **Ejecutar** para realizar todas las acciones válidas para esta tarea. La opción**Ejecutar** solo está disponible si se supera la comprobación de validación. Al hacer clic en **ejecutar**, aparece la advertencia siguiente recordándole que las acciones se procesan en modo por lotes: "Todos los valores de configuración que se indican como válidos en la herramienta se aplicarán a la granja de SharePoint. ¿Quiere continuar?".  
  
8.  Haga clic en **Sí** para continuar.  
  
 **Solucionar errores:**  
  
 En la herramienta de configuración, se muestra información de error en el panel Parámetros de cada acción. En el caso de problemas relacionados con la implementación o la retracción de soluciones, compruebe que se ha iniciado el servicio Administración de SharePoint. Este servicio ejecuta los trabajos de temporizador que desencadenan cambios de configuración en una granja. Si el servicio no se está ejecutando, la implementación o la retracción de soluciones producirá un error. Los errores persistentes indican que un trabajo existente de implementación o de retracción ya está en la cola y está bloqueando la acción posterior de la herramienta de configuración. Puede usar el comando de PowerShell siguiente para comprobar que el servicio está en ejecución.  
  
```  
Get-Service | where {$_.displayname -like "*sharepoint* administration*"}  
```  
  
 Para buscar y quitar un trabajo de implementación o de retracción que ya está en la cola, realice lo siguiente:  
  
1.  Para todos los demás errores, compruebe los registros ULS. Para obtener más información, consulte [configurar y ver archivos de registro de SharePoint y el registro de diagnóstico &#40;PowerPivot para SharePoint&#41;](../../analysis-services/power-pivot-sharepoint/configure-and-view-sharepoint-and-diagnostic-logging.md).  
  
2.  Inicie el Shell de administración de SharePoint como administrador y ejecute el siguiente comando para ver los trabajos de la cola:  
  
    ```  
    Stsadm -o enumdeployments  
    ```  
  
3.  Revise las implementaciones existentes para la siguiente información: **Tipo** es retracción o implementación, **archivo** es powerpivotwebapp.wsp o powerpivotfarm.wsp.  
  
4.  Las implementaciones o las retracciones relacionadas con soluciones de PowerPivot, copie el valor GUID para **JobId** y, a continuación, péguelo en el siguiente comando (use los comandos marcar, copiar y pegar en el menú de edición del Shell para copiar el GUID):  
  
    ```  
    Stsadm -o canceldeployment -id "<GUID>"  
    ```  
  
5.  Intente de nuevo la tarea en la herramienta de configuración haciendo clic en **Validar** seguido de **Ejecutar**.  
  
 Alternativamente, puede usar PowerShell para quitar características y soluciones de la granja de servidores. Para obtener más información, consulte [referencia de PowerShell para PowerPivot para SharePoint](/sql/analysis-services/powershell/powershell-reference-for-power-pivot-for-sharepoint).  
  
##  <a name="bkmk_uninstall"></a> Paso 3: Ejecute el programa de instalación SQL Server para quitar programas del equipo Local  
 Para eliminar los archivos de programa es necesario ejecutar el programa de instalación de SQL Server a fin de desinstalar el software. La desinstalación quita los archivos y las entradas del Registro creados por el programa de instalación. Puede utilizar la página Programas y características paginan para desinstalar el software. Una instalación de [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] forma parte de una instalación de SQL Server.  
  
 Puede desinstalar parte de una instalación sin afectar a otras instancias de SQL Server (o características en la misma instancia) que ya estén instaladas. Por ejemplo, puede desinstalar PowerPivot para SharePoint mientras deja instalados otros componentes, como [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] o el motor de base de datos.  
  
1.  Seleccione **Microsoft SQL Server 2014 (64 bits)** en la lista de programas.  
  
2.  Haga clic en **Desinstalar o cambiar**.  
  
3.  Haga clic en **Quitar**. De este modo inicia el programa de instalación de SQL Server.  
  
     Desde el programa de instalación, puede seleccionar la instancia de **PowerPivot** y, a continuación, seleccionar **Analysis Services** e **Integración con SharePoint de Analysis Services** para quitar solo esa característica, dejando todo lo demás en su lugar.  
  
##  <a name="bkmk_addin"></a> Paso 4: Desinstalar PowerPivot para SharePoint complemento  
 Si la implementación de [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] tiene dos o más servidores y ha instalado el complemento [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] , desinstale el complemento [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] de cada servidor donde se instaló para desinstalar completamente todos los archivos de [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] . Para obtener más información, consulte [instalar o desinstalar PowerPivot para SharePoint Add-in &#40;SharePoint 2013&#41;](../../analysis-services/instances/install-windows/install-or-uninstall-the-power-pivot-for-sharepoint-add-in-sharepoint-2013.md).  
  
##  <a name="verify"></a> Paso 5: Comprobar la desinstalación  
  
1.  En Administración central, en **Administrar servicios en el servidor**, conéctese al servidor del que desinstaló PowerPivot para SharePoint.  
  
2.  -   Si desinstaló [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] 2013, compruebe que **Servicio de sistema de SQL Server PowerPivot** ya no aparece en la lista.  
  
    -   Si desinstaló [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] 2010, compruebe que **SQL Server Analysis Services** y **Servicio de sistema de SQL Server PowerPivot** ya no aparecen en la lista.  
  
3.  Después de desinstalar el último servidor PowerPivot para SharePoint de la granja, haga lo siguiente:  
  
    1.  En Administración de aplicaciones, en **Administrar aplicaciones de servicio**, compruebe que Aplicación de servicio PowerPivot ya no aparece en la lista.  
  
    2.  En Configuración del sistema, en **Administrar características de la granja**, compruebe que la integración de características de PowerPivot ya no aparece en la página. En **Administrar soluciones del conjunto de servidores**, compruebe que las soluciones de PowerPivot ya no aparecen en la página.  
  
    3.  En Supervisión, en **Configurar registro de diagnósticos** y en **Configurar la recopilación de datos de uso y estado**, compruebe que los eventos y las categorías de eventos de PowerPivot ya no aparecen.  
  
    4.  En Configuración de aplicación general, compruebe que **Panel de administración de PowerPivot** ya no aparece en la página.  
  
##  <a name="bkmk_post"></a> Paso 6: Lista de comprobación posteriores a la desinstalación  
 Utilice la siguiente lista para quitar el software y los archivos que no se eliminaron durante la desinstalación.  
  
1.  Elimine todos los archivos de datos y subcarpetas de `C:\Program Files\Microsoft SQL Server\MSAS12.PowerPivot`y, a continuación, elimine la carpeta. Este paso también elimina los archivos almacenados previamente en memoria caché en el directorio DATA.  
  
2.  Elimine todos los libros PowerPivot, documentos y bibliotecas si no lo ha hecho con anterioridad.  
  
    -   [Eliminar la Galería de PowerPivot](../../analysis-services/power-pivot-sharepoint/delete-power-pivot-gallery.md)  
  
    -   [Eliminar una biblioteca de fuente de distribución de datos PowerPivot](../../analysis-services/power-pivot-sharepoint/delete-a-power-pivot-data-feed-library.md)  
  
3.  En Servicio de almacenamiento seguro, elimine cualquier aplicación de destino que contenga las credenciales almacenadas utilizadas por PowerPivot para SharePoint. Algunas de las entradas del Servicio de almacenamiento seguro se eliminan al desinstalar PowerPivot para SharePoint, pero no todas. Las aplicaciones de destino creadas para la cuenta de actualización de datos desatendida de PowerPivot además de todas las aplicaciones de destino que haya creado para la actualización de datos seguirán existiendo y se deben eliminar manualmente.  
  
     Por el contrario, las aplicaciones de destino individuales que generó automáticamente el Servicio de sistema de PowerPivot se eliminan automáticamente cuando se desinstala PowerPivot.  
  
4.  En el Panel de control, haga clic en **Programas**y, a continuación, haga clic en **Desinstalar un programa** . Desinstale cualquier biblioteca de cliente de Analysis Services que ya no se use. Analysis Services ADOMD.NET y Objetos de administración de análisis de Microsoft SQL Server no se quitan al desinstalar PowerPivot para SharePoint. El programa de instalación de SQL Server no desinstala automáticamente las bibliotecas porque podrían usarlas otros programas que utilizan datos de Analysis Services. Debe desinstalar estas bibliotecas cliente individualmente si ya no las necesita.  
  
     No desinstale el complemento SharePoint de SQL Server Reporting Services 2010 a menos que esté siguiendo instrucciones de solución de problemas o de instalación que le indiquen de manera concreta que debe hacerlo. Servicios de Access utiliza el complemento Reporting Services. Lo instala la herramienta de preparación de productos de SharePoint y debe permanecer en el sistema para admitir la funcionalidad que necesita SharePoint.  
  
     No desinstale el proveedor OLE DB de Analysis Services. SharePoint instala el proveedor OLE DB como un requisito previo de los libros de Excel que se conectan a las bases de datos de Analysis Services. [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] instala una versión más reciente, pero esta versión es compatible con las versiones anteriores, por lo que debe conservarse en el sistema para evitar problemas de conexión de datos más adelante.  
  
## <a name="see-also"></a>Vea también  
 [Instalar o desinstalar PowerPivot para SharePoint complemento &#40;SharePoint 2013&#41;](../../analysis-services/instances/install-windows/install-or-uninstall-the-power-pivot-for-sharepoint-add-in-sharepoint-2013.md)   
 [Herramientas de configuración de PowerPivot](../../analysis-services/power-pivot-sharepoint/power-pivot-configuration-tools.md)  
  
  
