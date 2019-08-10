---
title: 'Lista de comprobación de implementación: Escalar horizontalmente agregando servidores de PowerPivot a una granja de servidores de SharePoint 2010 | Microsoft Docs'
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
ms.assetid: 2dbddcc7-427a-4537-a8e2-56d99b9d967d
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: 597ed445d9e8fb444b08c260e4ef2a4af9d04418
ms.sourcegitcommit: a1adc6906ccc0a57d187e1ce35ab7a7a951ebff8
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/09/2019
ms.locfileid: "68890580"
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
|Determinar la cuenta de servicio de la instancia de Analysis Services que ya está en la granja|Cada instancia adicional que instale se debe ejecutar en la misma cuenta que la primera instancia. Puede determinar cuál es la cuenta de servicio de varias maneras:<br /><br /> En administración central, en la sección seguridad, haga clic en **configurar cuentas de servicio**. Seleccione **servicio de Windows: SQL Server Analysis Services**. Después de seleccionar el servicio, el nombre de la cuenta de servicio se mostrará en la página.<br /><br /> En un servidor que ya tenga una instalación del servicio PowerPivot, abra la aplicación de consola **servicios** en herramientas administrativas. Haga doble clic en **SQL Server Analysis Services**. Haga clic en la pestaña **iniciar sesión** para ver la cuenta de servicio.<br />Solo es **importante\*usaradministración central para cambiar las cuentas de servicio. \* \* \*** Si utiliza otra herramienta o método, los permisos no se actualizarán correctamente en la granja.|  
|Ejecutar el programa de instalación para instalar una segunda instancia de PowerPivot para SharePoint|[Instalar PowerPivot para SharePoint 2010](../../../2014/sql-server/install/install-powerpivot-for-sharepoint-2010.md)<br /><br /> Elija un servidor de aplicaciones que se una a la granja, pero que no tenga una instancia de PowerPivot existente en el servidor.<br /><br /> Durante la instalación, cuando se le pida confirmación para especificar una cuenta de servicio, escriba la cuenta del paso anterior. Todas las instancias del servicio de Analysis Services se deben ejecutar en la misma cuenta de dominio. Este requisito habilita el uso de la característica de cuentas administradas en SharePoint que le permite actualizar la contraseña en un lugar para todas las instancias de servicio del mismo tipo.|  
|Configurar la segunda instancia|Puede utilizar cualquiera de estos métodos para configurar la instancia: Configuración de PowerPivot [herramientas de configuración](https://docs.microsoft.com/analysis-services/power-pivot-sharepoint/power-pivot-configuration-tools) o [PowerPivot mediante Windows PowerShell](https://docs.microsoft.com/analysis-services/power-pivot-sharepoint/power-pivot-configuration-using-windows-powershell)<br /><br /> Al configurar una segunda instancia, solo necesita proporcionar los servicios locales. Todas las demás tareas de configuración se realizan durante la configuración inicial (como la creación de aplicaciones de servicio o la configuración de la actualización de datos) y son usadas por la siguientes instancias que instale.|  
|Tareas posteriores a la instalación|Específicamente no se requiere ningún paso más. No tiene que crear aplicaciones de servicio, activar características, implementar soluciones ni cambiar la identidad de aplicación de servicios. Las aplicaciones web y las aplicaciones de servicio existentes detectarán y usarán automáticamente el nuevo software de servidor.<br /><br /> Opcionalmente, si instaló un segundo servidor con el propósito de utilizar uno para las consultas y otro para la actualización de datos, puede configurar ahora las propiedades de instancia del servidor para especificar el tipo de solicitud administrado por cada servidor. Para obtener más información, vea [configurar la actualización de datos dedicada o el &#40;procesamiento&#41;de solo consultas PowerPivot para SharePoint](https://docs.microsoft.com/analysis-services/configure-dedicated-data-refresh-query-only-processing-powerpivot-sharepoint).|  
|Comprobar la instalación de la segunda instancia|Puede usar los pasos siguientes para comprobar el procesamiento de consultas de PowerPivot en el servidor instalado.<br /><br /> 1) en administración central, abra la página Administrar servicios en el servidor para confirmar que aparecen el servidor y sus servicios.<br />-En servidor, haga clic en la flecha hacia abajo, haga clic en cambiar servidor y, a continuación, seleccione el servidor que tiene la nueva instalación de PowerPivot para SharePoint.<br />-Compruebe que se han iniciado SQL Server Analysis Services y SQL Server Servicio de sistema de PowerPivot.<br /><br /> 2) en administración central, detenga otros servidores de PowerPivot para SharePoint para que el servidor que acaba de instalar sea el único disponible. Para obtener más información, consulte [iniciar o detener un servidor de PowerPivot para SharePoint](https://docs.microsoft.com/analysis-services/power-pivot-sharepoint/start-or-stop-a-power-pivot-for-sharepoint-server).<br /><br /> 3) haga clic en un libro PowerPivot para abrirlo desde la biblioteca.<br /><br /> 4) haga clic en una segmentación o dinamizar los datos para iniciar una consulta. El servidor cargará los datos PowerPivot en segundo plano. En el paso siguiente, se conectará al servidor para comprobar que los datos se cargan y se almacenan en caché.<br /><br /> 5) inicie SQL Server Management Studio desde el Microsoft SQL Server grupo de programas en el menú Inicio. Si esta herramienta no está instalada en el servidor, puede pasar al último paso para confirmar la presencia de archivos almacenados en caché.<br /><br /> 6) en tipo de servidor, seleccione **Analysis Services**.<br /><br /> 7) en nombre del servidor, escriba  **\<el nombre del servidor > \powerpivot**, donde  **\<nombre** del servidor > es el nombre del equipo que tiene la nueva PowerPivot para SharePoint instalación.<br /><br /> 8) haga clic en **conectar**.<br /><br /> 9) en Explorador de objetos, haga clic en **bases** de datos para ver la lista de archivos de datos PowerPivot que se cargan.<br /><br /> 10) en el sistema de archivos del equipo, Compruebe la siguiente carpeta para determinar si los archivos se almacenan en caché en el disco. La presencia de archivos almacenados en caché es una prueba más de que la implementación está operativa. Para ver la memoria caché de archivos, vaya a la carpeta \Archivos de programa\Microsoft SQL Server\MSAS11.POWERPIVOT\OLAP\Backup.<br /><br /> 11) reinicie los servicios que detuvo antes.|  
  
## <a name="see-also"></a>Vea también  
 [PowerPivot para SharePoint de &#40;configuración inicial&#41;](../../../2014/sql-server/install/initial-configuration-powerpivot-for-sharepoint.md)   
 [Instalación de PowerPivot para SharePoint 2010](../../../2014/sql-server/install/powerpivot-for-sharepoint-2010-installation.md)   
 [Administración y configuración del servidor PowerPivot en Administración central](https://docs.microsoft.com/analysis-services/power-pivot-sharepoint/power-pivot-server-administration-and-configuration-in-central-administration)  
  
  
