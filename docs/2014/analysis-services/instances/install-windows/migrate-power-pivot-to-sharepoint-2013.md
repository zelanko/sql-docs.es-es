---
title: Migrar PowerPivot a SharePoint 2013 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
ms.assetid: f698ceb1-d53e-4717-a3a0-225b346760d0
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: db1cdc1f10d53f11e06e37196d938667fb96327a
ms.sourcegitcommit: a1adc6906ccc0a57d187e1ce35ab7a7a951ebff8
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/09/2019
ms.locfileid: "68888517"
---
# <a name="migrate-powerpivot-to-sharepoint-2013"></a>Migrar PowerPivot a SharePoint 2013
  
  
 SharePoint 2013 no admite la actualización en contexto. Pero se admite el procedimiento de **actualizar y adjuntar la base de datos**. El comportamiento es diferente de la actualización a SharePoint 2010, donde un cliente puede elegir entre los dos métodos básicos de actualización: actualización en contexto y actualizar y adjuntar la base de datos.  
  
 Si tiene una instalación de [!INCLUDE[ssGeminiShort](../../../includes/ssgeminishort-md.md)] integrada con SharePoint 2010, no puede realizar una actualización en contexto del servidor de SharePoint. Sin embargo, puede migrar las bases de datos de contenido y las bases de datos de aplicación de servicio de la granja de SharePoint 2010 a una granja de SharePoint 2013. Este tema ofrece información general de los pasos necesarios para completar el procedimiento de actualizar y adjuntar la base de datos y para completar una migración relacionada con PowerPivot:  
  
 **[!INCLUDE[applies](../../../includes/applies-md.md)]**  SharePoint 2013  
  
### <a name="migration-overview"></a>Información general sobre la migración  
  
|1|2|3|4|  
|-------|-------|-------|-------|  
|Preparar la granja de SharePoint 2013|Hacer copia de seguridad, copiar y restaurar bases de datos.|Montar bases de datos de contenido|Migrar programaciones de [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)]|  
||[!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)]|Administración central de SharePoint<br /><br /> Windows PowerShell|Páginas de aplicación de SharePoint<br /><br /> Windows PowerShell|  
  
 **En este tema:**  
  
-   [1) Preparar la granja de SharePoint 2013](#bkmk_prepare_sharepoint2013)  
  
-   [2) Hacer copia de seguridad, copiar y restaurar las bases de datos](#bkmk_backup_restore)  
  
-   [3) Preparar las aplicaciones web y montar bases de datos de contenido](#bkmk_prepare_mount_databases)  
  
-   [4) actualizar programaciones de PowerPivot](#bkmk_upgrade_powerpivot_schedules)  
  
-   [Recursos adicionales](#bkmk_additional_resources)  
  
##  <a name="bkmk_prepare_sharepoint2013"></a> 1) Preparar la granja de SharePoint 2013  
  
1.  > [!TIP]  
    >  Revise el método de autenticación para el que están configuradas las aplicaciones web existentes. Las aplicaciones web de SharePoint 2013 usan de forma predeterminada la autenticación basada en notificaciones. Las aplicaciones web de SharePoint 2010 configuradas para la autenticación en modo clásico necesitan unos pasos adicionales para migrar bases de datos de SharePoint 2010 a SharePoint 2013. Si sus aplicaciones web están configuradas para la autenticación en modo clásico, consulte la documentación de SharePoint 2013.  
  
2.  Instale una nueva granja de servidores de SharePoint Server 2013.  
  
3.  Instale una instancia de un servidor de [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] en modo de SharePoint. Para obtener más información, vea [PowerPivot for SharePoint 2013 Installation](https://docs.microsoft.com/analysis-services/instances/install-windows/install-analysis-services-in-power-pivot-mode).  
  
4.  Ejecute el paquete de instalación de [!INCLUDE[ssGeminiShort](../../../includes/ssgeminishort-md.md)] 2013, **spPowerPivot.msi** , en todos los servidores de la granja de SharePoint. Para obtener más información, vea [instalar o desinstalar el complemento de PowerPivot para SharePoint &#40;SharePoint 2013&#41;](https://docs.microsoft.com/analysis-services/instances/install-windows/install-or-uninstall-the-power-pivot-for-sharepoint-add-in-sharepoint-2013).  
  
5.  En Administración central de SharePoint 2013, configure la aplicación de servicio Excel Services para que use el servidor en modo SharePoint de [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] creado en el paso anterior. Para obtener más información, vea la sección "configurar la integración de SharePoint básica Analysis Services SharePoint" de [PowerPivot para SharePoint instalación de 2013](https://docs.microsoft.com/analysis-services/instances/install-windows/install-analysis-services-in-power-pivot-mode).  
  
##  <a name="bkmk_backup_restore"></a> 2) Hacer copia de seguridad, copiar y restaurar las bases de datos  
 El proceso de "actualizar y adjuntar la base de datos de SharePoint" es una secuencia de pasos para realizar copias de seguridad, copiar y restaurar bases de datos de contenido y de aplicación de servicio relacionadas con PowerPivot en la granja de servidores de SharePoint 2013.  
  
1.  **Establecer base de datos en solo lectura:** En [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)], haga clic con el botón secundario en el nombre de la base de datos y haga clic en **propiedades**. En la página **Opciones** , establezca la propiedad **Base de datos de solo lectura** en **True**.  
  
2.  **Copia de seguridad:** Realice una copia de seguridad de cada base de datos de contenido y base de datos de aplicación de servicio que desee migrar a la granja de servidores de SharePoint 2013. En [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)], haga clic con el botón derecho en el nombre de la base de datos, haga clic en **Tareas**y, después, haga clic en **Copia de seguridad**.  
  
3.  Copia de los archivos de copia de seguridad de la base de datos (.bak) al servidor de destino deseado.  
  
4.  **Restaurar** Restaure las bases de datos en el [!INCLUDE[ssDEnoversion](../../../includes/ssdenoversion-md.md)]destino. Este paso se puede realizar con [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)].  
  
5.  **Establecer base de datos en lectura-escritura:** Establezca la **base de datos de solo lectura** en **false**.  
  
##  <a name="bkmk_prepare_mount_databases"></a> 3) Preparar las aplicaciones web y montar bases de datos de contenido  
 Para obtener una explicación más detallada de los procedimientos siguientes, vea [actualizar bases de datos de sharepoint 2010 a sharepoint 2013](https://go.microsoft.com/fwlink/p/?LinkId=256690) (https://go.microsoft.com/fwlink/p/?LinkId=256690).  
  
1.  **Poner bases de datos sin conexión:**  
  
     ponga sin conexión todas las bases de datos de contenido de SharePoint 2013 mediante Administración central de SharePoint. Las bases de datos de contenido se reemplazan con las bases de datos que copió. Considere cuál es la mejor secuencia para su entorno. Considere la posibilidad de poner sin conexión cada base de datos y montar su base de datos de reemplazo correspondiente antes de poner sin conexión la siguiente base de datos de contenido. Otra opción consiste en poner sin conexión todas las bases de datos de contenido como un grupo.  
  
    1.  En Administración central de SharePoint, haga clic en **Administración de aplicaciones**.  
  
    2.  Haga clic en **Administrar bases de datos de contenido**.  
  
    3.  Haga clic en el nombre de la base de datos.  
  
    4.  En **Administrar configuración de bases de datos de contenido**, establezca **Estado de la base de datos** en **Sin conexión**.  
  
    5.  Seleccione **Quitar base de datos de contenido**. Tenga en cuenta la advertencia de que ya no podrá obtener acceso a los sitios almacenados en la base de datos de contenido.  
  
-   **Montar bases de datos de contenido:**  
  
     Use cmdlets de PowerShell en el shell de administración de SharePoint 2013 para montar la base de datos de contenido migrada. No es necesario montar la base de datos de aplicación de servicio, solo las bases de datos de contenido: ![Contenido relacionado con PowerShell](../../../reporting-services/media/rs-powershellicon.jpg "Contenido relacionado con PowerShell")  
  
    ```  
    Mount-SPContentDatabase "SharePoint_Content_O14-KJSP1" -DatabaseServer "[server name]\powerpivot" -WebApplication [web application URL]  
    ```  
  
     Para obtener más información, vea adjuntar [o separar bases de datos de contenido (SharePoint Server 2010)](https://technet.microsoft.com/library/ff628582.aspx) (https://technet.microsoft.com/library/ff628582.aspx).  
  
     **Estado cuando se completa el paso:**  Una vez completada la operación de montaje, los usuarios pueden ver los archivos que estaban en la antigua base de datos de contenido. Por tanto, los usuarios pueden ver y abrir los libros en la biblioteca de documentos.  
  
    > [!TIP]  
    >  En este punto del proceso de migración, es posible crear nuevas programaciones para los libros migrados. Sin embargo, las programaciones se crean en la nueva base de datos de aplicación de servicio [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] , no en la base de datos que copió de la granja de servidores de SharePoint antigua. Por tanto, no contendrá ninguna de las programaciones anteriores. Después de completar los pasos siguientes para usar la antigua base de datos y migrar las programaciones anteriores, las nuevas programaciones no están disponibles.  
  
### <a name="troubleshoot-issues-when-you-attempt-to-mount-databases"></a>Solucionar problemas al intentar montar bases de datos  
 En esta sección se resumen los posibles problemas que pueden producirse al montar la base de datos.  
  
1.  **Errores de autenticación:** Si ve errores relacionados con la autenticación, revise el modo de autenticación que están usando las aplicaciones Web de origen. El error puede deberse a una incoherencia en la autenticación entre la aplicación web de SharePoint 2013 y la aplicación web de SharePoint 2010. Vea [1) Preparar la granja de SharePoint 2013](#bkmk_prepare_sharepoint2013) para obtener más información.  
  
2.  **Archivos de PowerPivot que faltan:** Si ve errores relacionados con los archivos dll de PowerPivot que faltan, no se ha instalado **spPowerPivot. msi** o la [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] herramienta de configuración de no se ha usado para configurar PowerPivot.  
  
##  <a name="bkmk_upgrade_powerpivot_schedules"></a>4) actualizar programaciones de PowerPivot  
 En esta sección se describen los detalles y las opciones para migrar programaciones de PowerPivot. La migración de programaciones es un proceso que consta de dos pasos. Primero debe configurar la aplicación de servicio PowerPivot para que use la base de datos de aplicación de servicio migrada. Después debe elegir una de las dos opciones para la migración de programaciones.  
  
 **Configure la aplicación de servicio para que use la base de datos de aplicación de servicio migrada.**  
  
 En Administración central de SharePoint, configure la aplicación de servicio PowerPivot para que use la antigua base de datos de aplicación de servicio que copió. El servicio PowerPivot actualiza la base de datos de aplicación de servicio al nuevo esquema.  
  
1.  En Administración central de SharePoint, haga clic en **Administrar aplicaciones de servicio**.  
  
2.  Busque la aplicación de servicio PowerPivot, por ejemplo "aplicación de servicio PowerPivot predeterminada", haga clic en el nombre de la aplicación de servicio y haga clic en **propiedades** en la cinta de opciones de SharePoint.  
  
3.  Actualice el nombre de instancia del servidor de bases de datos y el nombre de la base de datos. Corrija el nombre de la base de datos de la que hizo copia de seguridad, copió y restauró. Una vez que haga clic en **Aceptar**, se actualizará la base de datos de aplicación de servicio. Los errores se escribirán en el registro de ULS.  
  
 **Actualizar programaciones de PowerPivot**  
  
 Configure la aplicación de servicio PowerPivot para migrar las programaciones de actualización.  
  
-   **Se ha migrado la programación Opción1: Administrador de la granja de SharePoint**  
  
    1.  En la administración de SharePoint 2013, `Set-PowerPivotServiceApplication` ejecute el cmdlet `-StartMigratingRefreshSchedules` con el modificador para habilitar la migración automática a petición programación de ![PowerShell](../../../reporting-services/media/rs-powershellicon.jpg "contenido relacionado con")PowerShell. En el siguiente script de Windows PowerShell se da por supuesto que solo existe una aplicación de servicio PowerPivot.  
  
        ```  
        $app=Get-PowerPivotServiceApplication  
        Set-PowerPivotServiceApplication $app -StartMigratingRefreshSchedules  
        ```  
  
         Después de ejecutar el script de Windows PowerShell, las programaciones están activas y se ejecutarán en la siguiente hora apropiada. Sin embargo, no se habilita el estado de la página de actualización de programaciones. La primera vez que se ejecute la programación, se migrará y en la página de actualización de las programaciones, **Habilitada**  será true.  
  
    2.  Si desea comprobar el valor actual de la propiedad StartMigratingRefreshSchedules, ejecute el siguiente script de PowerShell. El script recorre en bucle todos los objetos de aplicación de servicio PowerPivot y muestra el nombre y los valores de propiedad:  
  
        ```  
        $apps = Get-PowerPivotServiceApplication  
        foreach ($app in $apps){}  
        Get-PowerPivotServiceApplication $appp | format-table -property displayname,id,StartMigratingRefreshSchedules  
        ```  
  
     **Migrar programaciones opción2: El usuario actualiza cada libro**  
  
    1.  Otra opción para migrar programaciones consiste en habilitar la programación de actualización para cada libro. Navegue a la biblioteca de documentos que contenga los libros.  
  
    2.  Abra el menú contextual libro y haga clic en **Administrar actualización de datos de PowerPivot**.  
  
    3.  En la sección **Programar actualización** , haga clic en **Habilitada**.  
  
    4.  Puede seleccionar **También actualizar lo más rápido posible**. Esta opción agregará una instancia de la actualización a la cola en cuanto haga clic en Aceptar. La programación de actualización periódica se sigue desencadenando en el momento adecuado.  
  
    5.  Haga clic en **Aceptar**. El historial de actualización es visible ahora en la página de actualización; la programación se desencadenará a la hora normal.  
  
 **Libros PowerPivot SQL Server 2008 R2**  
  
-   Los libros de SQL Server 2008 R2 PowerPivot no se actualizan automáticamente cuando se usan en SQL Server 2012 SP1 PowerPivot para SharePoint 2013. Después de migrar una base de datos de contenido que incluye los libros de 2008 R2, puede usar los libros pero las programaciones no se actualizan.  
  
-   Para obtener más información, vea [Actualizar libros y actualización de datos programada &#40;SharePoint 2013&#41;](https://docs.microsoft.com/analysis-services/instances/install-windows/upgrade-workbooks-and-scheduled-data-refresh-sharepoint-2013).  
  
##  <a name="bkmk_additional_resources"></a> Recursos adicionales  
  
> [!NOTE]  
>  Para obtener más información acerca de [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] y cómo actualizar y adjuntar la base de datos de SharePoint, vea lo siguiente:  
  
-   [Actualizar libros y actualización de datos programada &#40;SharePoint 2013&#41;](https://docs.microsoft.com/analysis-services/instances/install-windows/upgrade-workbooks-and-scheduled-data-refresh-sharepoint-2013).  
  
-   [Información general del proceso de actualización a SharePoint 2013](https://go.microsoft.com/fwlink/p/?LinkId=256688) (https://go.microsoft.com/fwlink/p/?LinkId=256688).  
  
-   [Limpiar preparativos antes de actualizar a SharePoint 2013](https://go.microsoft.com/fwlink/p/?LinkId=256689) (https://go.microsoft.com/fwlink/p/?LinkId=256689).  
  
-   [Actualizar bases de datos de sharepoint 2010 a sharepoint 2013](https://go.microsoft.com/fwlink/p/?LinkId=256690) (https://go.microsoft.com/fwlink/p/?LinkId=256690).  
  
  
