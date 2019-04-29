---
title: 'Lista de comprobación de implementación: Escalabilidad horizontal mediante la adición de servidores de PowerPivot a una granja de SharePoint 2010 | Microsoft Docs'
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: conceptual
ms.assetid: 2dbddcc7-427a-4537-a8e2-56d99b9d967d
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: 7bef5104038dad251927c6afff613f248f4a6a47
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "63025702"
---
# <a name="deployment-checklist-scale-out-by-adding-powerpivot-servers-to-a-sharepoint-2010-farm"></a>Lista de comprobación de implementación: Escalar horizontalmente mediante la adición de servidores de PowerPivot a una granja de SharePoint 2010
  Si se prevé un volumen alto de solicitudes para el procesamiento de consultas PowerPivot en una granja de servidores de SharePoint, puede agregar una instancia PowerPivot adicional para SharePoint para agregar una mayor compatibilidad con el procesamiento de datos y nuevas consultas.  
  
 Después de instalar una nueva instancia, tendrá más capacidad para consultar datos PowerPivot o procesar los trabajos de actualización de datos PowerPivot. Si lo desea, tendrá la opción de configurar cada servidor para administrar un tipo de solicitud: consulta o actualización de datos.  
  
## <a name="prerequisites"></a>Requisitos previos  
 SharePoint Server 2010 se instala y configura.  
  
 Se aplica SharePoint Server 2010 SP1 y se actualiza la granja.  
  
 La instancia existente de PowerPivot para SharePoint en la granja de servidores es [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] (una instalación nueva o actualizada desde SQL Server 2008 R2).  
  
 El equipo en el que se instala el nuevo servidor de [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] PowerPivot para SharePoint se une a la granja. El equipo y los demás servidores de la granja deben estar en el mismo dominio.  
  
 Revise los siguientes temas adicionales para conocer los requisitos del sistema y de las versiones:  
  
-   [Instrucciones para usar las características de SQL Server BI en una granja de servidores de SharePoint 2010](../../../2014/sql-server/install/guidance-for-using-sql-server-bi-features-in-a-sharepoint-2010-farm.md)  
  
> [!NOTE]  
>  En una granja con varios servidores, todas las instancias de PowerPivot para SharePoint deben ser de la misma versión. Si ha aplicado algún Service Pack o actualización en otros servidores PowerPivot que ya están en la granja, la nueva instancia que va a agregar debe actualizarse a la misma versión que la instancia existente que ya esté en la granja. La nueva instancia no estará disponible hasta que se hayan aplicado las actualizaciones.  
  
## <a name="steps"></a>Pasos  
 Utilice esta lista de comprobación para agregar servidores de PowerPivot adicionales a una granja de SharePoint. En estas instrucciones se supone que ya tiene un servidor de PowerPivot para SharePoint en la granja y que va a agregar un segundo servidor para administrar la carga de procesamiento adicional. Salvo por las diferencias de los requisitos de instalación, la configuración posterior a la instalación y la comprobación, los pasos para implementar una solución escalada son idénticos a los de agregar un único servidor de PowerPivot a una granja existente.  
  
|Paso|Vínculo|  
|----------|----------|  
|Determinar la cuenta de servicio de la instancia de Analysis Services que ya está en la granja|Cada instancia adicional que instale se debe ejecutar en la misma cuenta que la primera instancia. Puede determinar cuál es la cuenta de servicio de varias maneras:<br /><br /> En Administración Central, en la sección seguridad, haga clic en **configurar cuentas de servicio**. Seleccione **servicio de Windows: SQL Server Analysis Services**. Después de seleccionar el servicio, el nombre de la cuenta de servicio se mostrará en la página.<br /><br /> En un servidor que ya tiene una instalación de servicio PowerPivot, abra el **servicios** aplicación en Herramientas administrativas de consola. Haga doble clic en **Analysis Services de SQL Server**. Haga clic en el **iniciar sesión** pestaña para ver la cuenta de servicio.<br />**\*\* Importante \* \***  sólo use Administración Central para cambiar las cuentas de servicio. Si utiliza otra herramienta o método, los permisos no se actualizarán correctamente en la granja.|  
|Ejecutar el programa de instalación para instalar una segunda instancia de PowerPivot para SharePoint|[Instalar PowerPivot para SharePoint 2010](../../../2014/sql-server/install/install-powerpivot-for-sharepoint-2010.md)<br /><br /> Elija un servidor de aplicaciones que se una a la granja, pero que no tenga una instancia de PowerPivot existente en el servidor.<br /><br /> Durante la instalación, cuando se le pida confirmación para especificar una cuenta de servicio, escriba la cuenta del paso anterior. Todas las instancias del servicio de Analysis Services se deben ejecutar en la misma cuenta de dominio. Este requisito habilita el uso de la característica de cuentas administradas en SharePoint que le permite actualizar la contraseña en un lugar para todas las instancias de servicio del mismo tipo.|  
|Configurar la segunda instancia|Puede utilizar cualquier enfoque para configurar la instancia: [Herramientas de configuración de PowerPivot](../../analysis-services/power-pivot-sharepoint/power-pivot-configuration-tools.md) o [configuración de PowerPivot mediante Windows PowerShell](../../analysis-services/power-pivot-sharepoint/power-pivot-configuration-using-windows-powershell.md)<br /><br /> Al configurar una segunda instancia, solo necesita proporcionar los servicios locales. Todas las demás tareas de configuración se realizan durante la configuración inicial (como la creación de aplicaciones de servicio o la configuración de la actualización de datos) y son usadas por la siguientes instancias que instale.|  
|Tareas posteriores a la instalación|Específicamente no se requiere ningún paso más. No tiene que crear aplicaciones de servicio, activar características, implementar soluciones ni cambiar la identidad de aplicación de servicios. Las aplicaciones web y las aplicaciones de servicio existentes detectarán y usarán automáticamente el nuevo software de servidor.<br /><br /> Opcionalmente, si instaló un segundo servidor con el propósito de utilizar uno para las consultas y otro para la actualización de datos, puede configurar ahora las propiedades de instancia del servidor para especificar el tipo de solicitud administrado por cada servidor. Para obtener más información, consulte [Configurar actualización de datos dedicada o procesamiento Query-Only &#40;PowerPivot para SharePoint&#41;](../../analysis-services/configure-dedicated-data-refresh-query-only-processing-powerpivot-sharepoint.md).|  
|Comprobar la instalación de la segunda instancia|Puede usar los pasos siguientes para comprobar el procesamiento de consultas de PowerPivot en el servidor instalado.<br /><br /> (1) en Administración Central, abra los servicios de administración en la página del servidor para confirmar que aparecen el servidor y sus servicios.<br />-En el servidor, haga clic en la flecha hacia abajo, haga clic en Cambiar servidor y, a continuación, seleccione el servidor que tiene la nueva instalación de PowerPivot para SharePoint.<br />-Compruebe que se han iniciado SQL Server Analysis Services y el servicio de sistema de PowerPivot de SQL Server.<br /><br /> (2) en Administración Central, detenga otro servidores PowerPivot para SharePoint para que el servidor que acaba de instalar es el único disponible. Para obtener más información, consulte [iniciar o detener un PowerPivot para SharePoint Server](../../analysis-services/power-pivot-sharepoint/start-or-stop-a-power-pivot-for-sharepoint-server.md).<br /><br /> (3) haga clic en un libro de PowerPivot para abrirlo desde la biblioteca.<br /><br /> (4) haga clic en una segmentación o dinamice los datos para iniciar una consulta. El servidor cargará los datos PowerPivot en segundo plano. En el paso siguiente, se conectará al servidor para comprobar que los datos se cargan y se almacenan en caché.<br /><br /> (5) inicie SQL Server Management Studio desde el grupo de programas de Microsoft SQL Server en el menú Inicio. Si esta herramienta no está instalada en el servidor, puede pasar al último paso para confirmar la presencia de archivos almacenados en caché.<br /><br /> (6) en el tipo de servidor, seleccione **Analysis Services**.<br /><br /> (7) en el nombre del servidor, escriba  **\<nombre del servidor > \powerpivot**, donde  **\<server-name >** es el nombre del equipo que tiene la nueva instalación de PowerPivot para SharePoint.<br /><br /> 8) haga clic en **conectar**.<br /><br /> 9) en el Explorador de objetos, haga clic en **bases de datos** para ver la lista de archivos de datos de PowerPivot que se cargan.<br /><br /> 10) en el sistema de archivos del equipo, compruebe la siguiente carpeta para determinar si los archivos se almacenan en caché en el disco. La presencia de archivos almacenados en caché es una prueba más de que la implementación está operativa. Para ver la memoria caché de archivos, vaya a la carpeta \Archivos de programa\Microsoft SQL Server\MSAS11.POWERPIVOT\OLAP\Backup.<br /><br /> 11) reiniciar los servicios que detuvo anteriormente.|  
  
## <a name="see-also"></a>Vea también  
 [Configuración inicial &#40;PowerPivot para SharePoint&#41;](../../../2014/sql-server/install/initial-configuration-powerpivot-for-sharepoint.md)   
 [PowerPivot para SharePoint 2010](../../../2014/sql-server/install/powerpivot-for-sharepoint-2010-installation.md)   
 [Administración y configuración del servidor PowerPivot en Administración central](../../analysis-services/power-pivot-sharepoint/power-pivot-server-administration-and-configuration-in-central-administration.md)  
  
  
