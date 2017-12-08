---
title: Configurar las cuentas de servicio de Power Pivot | Documentos de Microsoft
ms.custom: 
ms.date: 03/07/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: power-pivot-sharepoint
ms.reviewer: 
ms.suite: sql
ms.technology:
- analysis-services
- analysis-services/multidimensional-tabular
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 76a85cd0-af93-40c9-9adf-9eb0f80b30c1
caps.latest.revision: "15"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: aae3f818de4936974dd53f14c2b3fdbbea0b369f
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 11/17/2017
---
# <a name="configure-power-pivot-service-accounts"></a>Configurar las cuentas de servicio Power Pivot
  Una instalación de [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)]incluye dos servicios compatibles con operaciones de servidor. El servicio **SQL Server Analysis Services ([!INCLUDE[ssGemini](../../includes/ssgemini-md.md)])** es un servicio de Windows que proporciona compatibilidad con las consultas y el procesamiento de datos [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] en un servidor de aplicaciones. La cuenta de inicio de sesión para este servicio siempre se especifica durante la ejecución del programa de instalación de SQL Server al instalar Analysis Services en modo integrado de SharePoint.  
  
 Es necesario especificar una segunda cuenta para la aplicación de servicio [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] , un servicio web compartido que se ejecuta bajo una identidad del grupo de aplicaciones en una granja de SharePoint. Se especifica esta cuenta al configurar una instalación de [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)]mediante la herramienta de configuración de [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] o PowerShell.  
  
 Cada servicio se debe ejecutar con una cuenta dedicada para que pueda auditar las conexiones o habilitar el protocolo de autenticación Kerberos en la granja de servidores.  
  
 Una vez establecidas las cuentas de servicio, cualquier modificación de alguna de ellas se debe realizar a través de Administración central de SharePoint. Si utiliza las herramientas alternativas (como la aplicación de consola Servicios, el Administrador IIS o el Administrador de configuración de SQL Server), los permisos no se actualizarán para el acceso a bases de datos en la granja o para el acceso a archivos locales en el servidor físico.  
  
 Este tema contiene las siguientes secciones:  
  
 [Actualización de una contraseña expirada para la instancia de SQL Server Analysis Services (Power Pivot)](#bkmk_passwordssas)  
  
 [Actualización de una contraseña expirada para la Aplicación de servicio Power Pivot](../../analysis-services/power-pivot-sharepoint/configure-power-pivot-service-accounts.md#bkmk_passwordapp)  
  
 [Cambio de la cuenta con la que se ejecuta cada servicio](#bkmk_newacct)  
  
 [Creación o modificación del grupo de aplicaciones para una aplicación de servicio Power Pivot](#bkmk_appPool)  
  
 [Requisitos de cuentas y permisos](#requirements)  
  
 [Solucionar problemas: conceder los permisos administrativos manualmente](#updatemanually)  
  
 [Solución de problemas: resolver los errores HTTP 503 debidos a que las contraseñas han expirado para Administración central o para el servicio de aplicación web de SharePoint Foundation](#expired)  
  
##  <a name="bkmk_passwordssas"></a> Actualización de una contraseña expirada para la instancia de SQL Server Analysis Services (Power Pivot)  
  
1.  Haga clic en Inicio, seleccione **Herramientas administrativas**y, a continuación, **Servicios**. Haga doble clic en **SQL Server Analysis Services ([!INCLUDE[ssGemini](../../includes/ssgemini-md.md)])**. Haga clic en **Iniciar sesión**y escriba la nueva contraseña de la cuenta.  
  
2.  En Administración central, en la sección Seguridad, haga clic en **Configurar cuentas administradas**.  
  
3.  Haga clic en **Editar** para cambiar una cuenta concreta.  
  
4.  Seleccione **Cambiar la contraseña ahora**.  
  
5.  Seleccione **Establecer contraseña de cuenta con un nuevo valor**. Todos los servicios que se ejecutan en la cuenta administrada utilizarán las credenciales actualizadas.  
  
##  <a name="bkmk_passwordapp"></a> Actualización de una contraseña expirada para la Aplicación de servicio Power Pivot  
  
1.  En Administración central, en la sección Seguridad, haga clic en **Configurar cuentas administradas**.  
  
2.  Haga clic en **Editar** para cambiar una cuenta concreta.  
  
3.  Seleccione **Cambiar la contraseña ahora**.  
  
4.  Seleccione **Establecer contraseña de cuenta con un nuevo valor**. Todos los servicios que se ejecutan en la cuenta administrada utilizarán las credenciales actualizadas.  
  
##  <a name="bkmk_newacct"></a> Cambio de la cuenta con la que se ejecuta cada servicio  
  
1.  En Administración central, en la sección Seguridad, haga clic en **Configurar cuentas de servicio**.  
  
2.  Seleccione **Windows Service - SQL Server Analysis Services** para cambiar la cuenta de servicio de Analysis Services.  
  
3.  En **Seleccionar una cuenta para este servicio**, elija una cuenta administrada o cree una nueva. La cuenta debe ser una cuenta de usuario de dominio.  
  
4.  Seleccione **Grupo de aplicaciones de servicio - Sistema de SharePoint Web Services** para cambiar la identidad del grupo de aplicaciones de la aplicación de servicio [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] predeterminada. Según la forma en que esté configurada la instalación, el servicio puede ejecutarse con un grupo de aplicaciones de servicio existente, creado para los servicios de SharePoint. De forma predeterminada, la herramienta de configuración de [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] registra el servicio como **Aplicación de servicio [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] predeterminada (Aplicación de servicio [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)])**.  
  
     Si un administrador de SharePoint configuró manualmente el servicio, probablemente tendrá su propio grupo de aplicaciones de servicios.  
  
5.  En **Seleccionar una cuenta para este servicio**, elija una cuenta administrada o cree una nueva. La cuenta debe ser una cuenta de usuario de dominio.  
  
6.  Haga clic en **Aceptar**.  
  
##  <a name="bkmk_appPool"></a> Creación o modificación del grupo de aplicaciones para una aplicación de servicio Power Pivot  
  
1.  En Administración central, en Administración de aplicaciones, haga clic en **Administrar aplicaciones de servicio**.  
  
2.  Seleccione la aplicación de servicio [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] , pero no haga clic en ella. Al hacer clic en el nombre de aplicación, se abre el Panel de administración de [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] , que no proporciona un vínculo a la página de propiedades que especifica el grupo de aplicaciones.  Haga clic en el espacio en blanco vacío de la fila o en el nombre de tipo para seleccionar la aplicación de servicio [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] .  
  
3.  Haga clic en **Propiedades** en la cinta de opciones.  
  
4.  Seleccione **Crear un grupo de aplicaciones nuevo**. Proporcione un nombre para el grupo de aplicaciones y especifique una cuenta administrada para su identidad.  
  
##  <a name="requirements"></a> Requisitos de cuentas y permisos  
 Al planear una implementación de [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] para SharePoint, debe tener en cuenta las siguientes cuentas de servicio.  
  
-   Cuenta de servicio de Analysis Services. Analysis Services procesa las consultas de [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] y los trabajos de actualización de datos en la granja. Esta cuenta siempre se especifica en el programa de instalación de SQL Server al instalar [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] para SharePoint.  
  
-   [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] . Una aplicación de servicio [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] se asocia al Servicio de sistema de [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] que proporciona la integración y la infraestructura de SharePoint para el procesamiento de las consultas de [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] en una granja. El grupo de aplicaciones que especifique para una aplicación de servicio [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] es la identidad del Servicio de sistema de [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] . Puede tener varias aplicaciones de servicio [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] en una granja. Cada una que cree se debería ejecutar en su propio grupo de aplicaciones.  
  
#### <a name="analysis-services-service-account"></a>Cuenta de servicio de Analysis Services  
  
|Requisito|Description|  
|-----------------|-----------------|  
|Requisito del aprovisionamiento|Esta cuenta debe especificarse durante la instalación de SQL Server en la **página de configuración de Analysis Services** del Asistente para la instalación (o el parámetro de instalación **ASSVCACCOUNT** en una instalación mediante la línea de comandos).<br /><br /> Puede modificar el nombre de usuario o la contraseña usando Administración central, PowerShell o la herramienta de configuración de [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] . No se admite el uso de otras herramientas para cambiar las cuentas y las contraseñas.|  
|Requisito de la cuenta de usuario de dominio|Esta cuenta debe ser una cuenta de usuario de dominio de Windows. Las cuentas de equipo integradas (como Servicio de red o Servicio local) están prohibidas. El programa de instalación de SQL Server aplica el requisito de las cuentas de usuario de dominio bloqueando la instalación cada vez que se especifica una cuenta de equipo.|  
|Requisitos de permisos|Esta cuenta debe ser miembro de SQLServerMSASUser$\<servidor > $PowerPivot grupo de seguridad y los grupos de seguridad WSS_WPG en el equipo local. Estos permisos se deben conceder automáticamente. Para obtener más información sobre cómo comprobar o conceder los permisos, vea [Conceder los permisos administrativos manualmente](#updatemanually) en este tema y [Configuración inicial (PowerPivot para SharePoint)](http://msdn.microsoft.com/en-us/3a0ec2eb-017a-40db-b8d4-8aa8f4cdc146).|  
|Requisitos de escalamiento|Si instala varias instancias de servidor de [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] para SharePoint en una granja, todas las instancias de servidor de Analysis Services se deben ejecutar bajo la misma cuenta de usuario de dominio. Por ejemplo, si configura la primera instancia de [!INCLUDE[ssGeminiSrv](../../includes/ssgeminisrv-md.md)] para ejecutarse como Contoso\ssas-srv01, todas las instancias de [!INCLUDE[ssGeminiSrv](../../includes/ssgeminisrv-md.md)] adicionales que implemente después en la misma granja también se deben ejecutar como Contoso\ssas-srv01 (o la cuenta que sea).<br /><br /> Al configurar todas las instancias de los servicios para ejecutarse en la misma cuenta, se permite al servicio de sistema de [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] asignar los trabajos de actualización de datos o de procesamiento de consultas a cualquier instancia de servicio de Analysis Services de la granja. Además, habilita el uso de la característica de administración de cuentas de Administración central para las instancias de servidor de Analysis Services. Al usar la misma cuenta para todas las instancias de [!INCLUDE[ssGeminiSrv](../../includes/ssgeminisrv-md.md)] , puede cambiar la cuenta o la contraseña una vez, y todas las instancias de servicio que utilicen esas credenciales se actualizarán automáticamente.<br /><br /> El programa de instalación de SQL Server aplica el mismo requisito para la cuenta. En una implementación escalada en la que una granja de servidores de SharePoint ya tenga instalada una instancia de [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] para SharePoint, el programa de instalación bloqueará la nueva instalación si la cuenta de [!INCLUDE[ssGeminiSrv](../../includes/ssgeminisrv-md.md)] que haya especificado ya es diferente de la que se usa en la granja.|  
  
#### <a name="power-pivot-service-application-pool"></a>Grupo de aplicaciones de servicio Power Pivot  
  
|Requisito|Description|  
|-----------------|-----------------|  
|Requisito del aprovisionamiento|[!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] es un recurso compartido en la granja que pasa a estar disponible al crear una aplicación de servicio. Cuando se crea la aplicación de servicio se debe especificar el grupo de aplicaciones del servicio. Se puede especificar de dos maneras: mediante la herramienta de configuración de [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] o mediante comandos de PowerShell.<br /><br /> Puede haber configurado la identidad del grupo de aplicaciones para que se ejecute en una cuenta única. Pero si no lo ha hecho, considere la posibilidad de cambiarla para que se ejecute en una cuenta diferente.|  
|Requisito de la cuenta de usuario de dominio|La identidad del grupo de aplicaciones debe ser una cuenta de usuario de dominio de Windows. Las cuentas de equipo integradas (como Servicio de red o Servicio local) están prohibidas.|  
|Requisitos de permisos|Esta cuenta no necesita permisos de administrador del sistema local en el equipo. Sin embargo, debe tener los permisos de administrador del sistema de Analysis Services en el [!INCLUDE[ssGeminiSrv](../../includes/ssgeminisrv-md.md)] local que está instalado en el mismo equipo. El programa de instalación de SQL Server concede estos permisos automáticamente, o bien se conceden al establecer o cambiar la identidad del grupo de aplicaciones de servicio PowerPivot en Administración central.<br /><br /> Los permisos administrativos son necesarios para reenviar consultas a [!INCLUDE[ssGeminiSrv](../../includes/ssgeminisrv-md.md)]. También se requieren para supervisar el estado, cerrar las sesiones inactivas y escuchar los eventos de seguimiento.<br /><br /> La cuenta debe tener permisos de conexión, lectura y escritura para la base de datos de aplicaciones del servicio [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] . Estos permisos se conceden automáticamente cuando se crea la aplicación y se actualizan automáticamente al cambiar cuentas o contraseñas en Administración central.<br /><br /> La aplicación de servicio [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] comprobará que un usuario de SharePoint esté autorizado a ver los datos antes de recuperar el archivo, pero no suplantará al usuario. No hay ningún requisito de permiso para la suplantación.|  
|Requisitos de escalamiento|Ninguno.|  
  
##  <a name="updatemanually"></a> Solucionar problemas: conceder los permisos administrativos manualmente  
 Los permisos administrativos no podrán actualizarse si ella persona que actualiza las credenciales no es administrador local en el equipo. Si ocurre esto, puede conceder los permisos administrativos manualmente. La manera más fácil para ello es ejecutar el trabajo de temporizador de configuración de [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] en Administración central. Con esta solución, puede restablecer los permisos para todos los servidores de [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] en la granja. Observe que este enfoque solo funcionará si el trabajo de temporizador de SharePoint se ejecuta como administrador de la granja y como administrador local en el equipo.  
  
1.  Para Supervisión, haga clic en **Revisar definiciones de trabajo**.  
  
2.  Seleccione **Trabajo de temporizador de configuración de [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)]**.  
  
3.  Haga clic en **Ejecutar ahora**.  
  
 Como último recurso, puede garantizar los permisos correctos concediendo permisos de administración del sistema de Analysis Services a la [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] aplicación de servicio y, a continuación, agregando específicamente la identidad de aplicación de servicio al SQLServerMSASUser$\<servername > grupo de seguridad $PowerPivot Windows. Debe repetir estos pasos para cada instancia de Analysis Services que esté integrada con la granja de servidores de SharePoint.  
  
 Debe ser administrador local para actualizar los grupos de seguridad de Windows.  
  
1.  En SQL Server Management Studio, conéctese a la instancia de Analysis Services como \<nombre del servidor > \POWERPIVOT.  
  
2.  Haga clic con el botón derecho en el nombre del servidor y seleccione **Propiedades**.  
  
3.  Haga clic en **Seguridad**.  
  
4.  Haga clic en **Agregar**.  
  
5.  Escriba el nombre de la cuenta que se usa para el grupo de aplicaciones de servicio [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] y haga clic en **Aceptar**.  
  
6.  En Herramientas administrativas, haga clic en **Administración de equipos**.  
  
7.  Abra **Usuarios locales y grupos**.  
  
8.  Abra **Grupos**.  
  
9. Haga doble clic en SQLServerMSASUser$\<nombreDeServidor > $PowerPivot.  
  
10. Haga clic en **Agregar**.  
  
11. Escriba el nombre de la cuenta que se usa para el grupo de aplicaciones de servicio [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] y haga clic en **Aceptar**.  
  
##  <a name="expired"></a> Solución de problemas: resolver los errores HTTP 503 debidos a que las contraseñas han expirado para Administración central o para el servicio de aplicación web de SharePoint Foundation  
 Si el servicio Administración central o el servicio de aplicación web de SharePoint Foundation dejan de funcionar debido a que la cuenta se restablece o expira la contraseña, encontrará mensajes de error HTTP 503 "Servicio no disponible" al intentar abrir Administración central de SharePoint o un sitio de SharePoint. Siga estos pasos para volver a poner el servidor en línea. Cuando Administración central está disponible, puede continuar actualizando la información de la cuenta que ha expirado.  
  
1.  En Herramientas administrativas, haga clic en **Administrador de Internet Information Services**.  
  
2.  Si la identidad del sitio o el grupo de aplicaciones de Administración central es una cuenta de usuario de dominio que tiene una contraseña que ha expirado, haga lo siguiente:  
  
    1.  Haga clic con el botón derecho en el nombre del grupo de aplicaciones y seleccione **Configuración avanzada**.  
  
    2.  Seleccione **Identidad** y haga clic en el botón ... para abrir el cuadro de diálogo Identidad del grupo de aplicaciones.  
  
    3.  Haga clic en **Conjunto**.  
  
    4.  Escriba el nombre de usuario y la contraseña.  
  
3.  Ejecute IISRESET. Para ello, abra un símbolo del sistema de administrador y escriba **iisreset** en la línea de comandos.  
  
4.  En Administración central de SharePoint, en Seguridad, seleccione **Configurar cuentas administradas**.  
  
5.  Haga clic en **Editar** para actualizar la información de la cuenta administrada que tenga la contraseña que ha expirado.  
  
6.  Seleccione **Cambiar la contraseña ahora**.  
  
7.  Haga clic en **Usar la contraseña existente**.  
  
8.  Escriba la contraseña y, a continuación, haga clic en **Aceptar**.  
  
 Si Reporting Services está instalado, utilice el Administrador de configuración de Reporting Services para actualizar las contraseñas para el servidor de informes y la conexión a la base de datos del servidor de informes. Para obtener más información, vea [Configuración y administración de un servidor de informes &#40;modo de SharePoint de Reporting Services&#41;](../../reporting-services/report-server-sharepoint/configuration-and-administration-of-a-report-server.md).  
  
## <a name="see-also"></a>Vea también  
 [Iniciar o detener un servidor de Power Pivot para SharePoint](../../analysis-services/power-pivot-sharepoint/start-or-stop-a-power-pivot-for-sharepoint-server.md)   
 [Configurar la cuenta de actualización de datos desatendida de PowerPivot (PowerPivot para SharePoint)](http://msdn.microsoft.com/en-us/81401eac-c619-4fad-ad3e-599e7a6f8493)  
  
  
