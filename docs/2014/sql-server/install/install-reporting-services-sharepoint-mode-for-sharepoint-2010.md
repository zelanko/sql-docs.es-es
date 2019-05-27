---
title: Instalar Reporting Services SharePoint Mode for SharePoint 2010 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
ms.assetid: 47efa72e-1735-4387-8485-f8994fb08c8c
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: 524ad97d02192a19198891c79c07f875a738fc30
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/23/2019
ms.locfileid: "66094528"
---
# <a name="install-reporting-services-sharepoint-mode-for-sharepoint-2010"></a>Instalar el modo de SharePoint de Reporting Services para SharePoint 2010
  Los procedimientos de este tema le guían en la instalación de un único servidor del servidor de informes de Reporting Services en modo de SharePoint. Los pasos incluyen la ejecución del Asistente de instalación de SQL Server así como tareas de configuración adicionales que usan Administración central de SharePoint 2010. El tema también se puede usar para procedimientos individuales para una instalación existente, como crear una nueva aplicación de servicio de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]. Para obtener información sobre cómo agregar adicionales [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] servidores a una granja existente, consulte [agregar un servidor de informes adicional a una granja &#40;escalada SSRS&#41; ](../../reporting-services/install-windows/add-an-additional-report-server-to-a-farm-ssrs-scale-out.md) y [agregar una Web adicional de Reporting Services Front-end para una granja de servidores](../../reporting-services/install-windows/add-an-additional-reporting-services-web-front-end-to-a-farm.md).  
  
||  
|-|  
|**[!INCLUDE[applies](../../includes/applies-md.md)]**  SharePoint 2010|  
  
 Una instalación de servidor único resulta de utilidad en los escenarios de desarrollo y pruebas pero no se recomienda en entornos de producción.  
  
> [!NOTE]  
>  Para obtener información sobre la actualización y existente [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] instalación en modo SharePoint a [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], consulte [actualizar y migrar Reporting Services](../../reporting-services/install-windows/upgrade-and-migrate-reporting-services.md).  
  

  
##  <a name="bkmk_prereq"></a> Requisitos previos  
  
-   > [!IMPORTANT]  
    >  El Administrador de configuración de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] ya no es necesario ni se admite para configurar y administrar [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] en modo de SharePoint. Usar la Administración central de SharePoint para configurar un servidor de informes en modo de SharePoint. Para obtener más información, consulte [administrar una aplicación de servicio de Reporting Services SharePoint](../../../2014/reporting-services/manage-a-reporting-services-sharepoint-service-application.md).  
  
-   Revise los temas siguientes sobre los requisitos, incluidos los Productos de SharePoint 2010:  
  
    -   [Notas de la versión en línea](https://msdn.microsoft.com/library/dn169381.aspx)
  
    -   [Instrucciones para usar las características de SQL Server BI en una granja de servidores de SharePoint 2010](../../../2014/sql-server/install/guidance-for-using-sql-server-bi-features-in-a-sharepoint-2010-farm.md)  
  
-   Este tema no abarca la instalación de Productos de SharePoint 2010. Para obtener más información, consulte [instrucciones para usar características de BI de SQL Server en una granja de SharePoint 2010](../../../2014/sql-server/install/guidance-for-using-sql-server-bi-features-in-a-sharepoint-2010-farm.md).  
  
-   Estos procedimientos se han diseñado para configurar un servidor de informes de [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] y no funcionan con versiones anteriores del servidor de informes. Las versiones anteriores del servidor de informes no usaba la arquitectura de servicio compartido de SharePoint. Por ejemplo, los servidores de informes de SQL Server 2008 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] y los servidores de informes SQL Server 2008 R2 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)].  
  
-   Compruebe el **administración de SharePoint 2010** servicio se inicia en el administrador del servidor de Windows.  
  
 ![Componentes de SSRS en una instalación de 1 servidor](../../../2014/sql-server/install/media/rs-deployment-1-server.gif "componentes SSRS en una instalación de 1 servidor")  
  
### <a name="database-considerations-for-a-single-server-configuration"></a>Consideraciones acerca de las bases de datos en una configuración de un solo servidor  
  
-   Tanto Reporting Services como Productos y tecnologías de SharePoint utilizan bases de datos relacionales de SQL Server para almacenar los datos de aplicación.  
  
-   [!INCLUDE[ssRSCurrent](../../includes/ssrscurrent-md.md)] necesita una instancia de la edición de evaluación de SQL Server del Motor SQL.  
  
-   Los productos de SharePoint pueden utilizar una instancia de base de datos existente. Si una instancia del motor de base de datos no está instalada, el programa de instalación de productos de SharePoint instala SQL Server Express Edition para las bases de datos de aplicación de SharePoint.  
  
-   La instancia del servidor de informes no puede utilizar SQL Server Express Edition para su base de datos. Sin embargo, la instancia de SQL Server Express Edition instalada por el producto de SharePoint puede coexistir con otras ediciones del Motor de base de datos.  
  

  
##  <a name="bkmk_install_SSRS"></a> Instalar a servidor de informes de Reporting Services en modo de SharePoint  
  
1.  Ejecute el Asistente para la instalación de SQL Server.  
  
2.  Haga clic en **Instalación** en el lado izquierdo del asistente y, a continuación, haga clic en **Nueva instalación independiente de SQL Server o agregar características a una instalación existente**.  
  
3.  Haga clic en **Aceptar** en la página **Reglas auxiliares del programa de instalación** , suponiendo que se han pasado todas las reglas.  
  
4.  Haga clic en **Instalar** en la página **Archivos auxiliares del programa de instalación** .  
  
5.  Haga clic en **siguiente** después de finalizar la instalación de los archivos de compatibilidad y las reglas auxiliares muestren el estado **pasa**. Revise posibles advertencias o problemas de bloqueo.  
  
6.  En el **clave de producto** página, escriba la clave o acepte el valor predeterminado de la edición 'Enterprise Evaluation'.  
  
     Haga clic en **Siguiente**.  
  
7.  Revise y acepte los términos de la licencia. Microsoft aprecia que haga clic para indicar que está conforme con enviar datos de uso de las características para ayudarle a mejorar las características y el soporte técnico de los productos.  
  
     Haga clic en **Siguiente**.  
  
8.  Seleccione **instalación de características de SQL Server** en el **rol de instalación** página.  
  
     Haga clic en **Siguiente**.  
  
     ![Instalación de la característica de SQL Server para el rol de instalación](../../../2014/sql-server/install/media/rs-setuprole.gif "Instalación de la característica de SQL Server para el rol de instalación")  
  
9. Seleccione lo siguiente en la página **Selección de características** :  
  
    -   **Reporting Services - SharePoint**  
  
    -   **Reporting Services complemento para productos de SharePoint 2010**. ![Tenga en cuenta](../../../2014/reporting-services/media/rs-fyinote.png "Nota")la opción del Asistente de instalación para instalar el complemento es nueva con el [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] de versión.  
  
    -   Si aún no tiene una instancia del [!INCLUDE[ssDE](../../includes/ssde-md.md)]de SQL Server, también podría seleccionar **Servicios de Motor de base de datos** y **Herramientas de administración - Completa** para un entorno completo.  
  
     Haga clic en **Siguiente**.  
  
     ![Selección de características de SSRS para el modo de SharePoint](../../../2014/sql-server/install/media/rs-setupfeatureselection-sharepoint-with-circles.gif "selección de características de SSRS para el modo de SharePoint")  
  
10. Haga clic en **siguiente** en el **reglas de instalación** página. Revise posibles advertencias o problemas de bloqueo.  
  
11. Si seleccionó los servicios del Motor de base de datos, acepte la instancia predeterminada de **MSSQLSERVER** en la página **Configuración de instancia** y haga clic en **Siguiente**. La arquitectura de servicio compartido de Reporting Services no se basa en una "instancia" de SQL Server como la arquitectura de Reporting Services anterior.  
  
12. Examine la página **Requisitos de espacio en disco** y haga clic en **Siguiente**.  
  
13. En el **configuración del servidor** página escriba las credenciales adecuadas. Si desea usar las características de suscripción o alerta de datos de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] , necesita cambiar el **Tipo de inicio** para el Agente SQL Server a **Automático**.  
  
     Haga clic en **Siguiente**.  
  
14. Si seleccionó los servicios del Motor de base de datos, verá la página **Configuración del Motor de base de datos** ; agregue las cuentas adecuadas a la lista de administradores de SQL y haga clic en **Siguiente**.  
  
15. En la página **Configuración de Reporting Services** debe ver que la opción **Solo instalar** está seleccionada. Esta opción instala los archivos del servidor de informes y no configura el entorno de SharePoint para [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]. Cuando la instalación de SQL Server se complete, tendrá que seguir las otras secciones de este tema para configurar el entorno de SharePoint. Esto incluye instalar el servicio compartido de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] y la creación de las aplicaciones de servicio de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] .  
  
     ![rs_SQL11_SETUP_SSRS_configpage_withcircles](../../../2014/sql-server/install/media/rs-kj-setup-ssrs-configpage-withcircles.gif "rs_SQL11_SETUP_SSRS_configpage_withcircles")  
  
16. Ayude a Microsoft a mejorar las características y los servicios de SQL Server activando la casilla para enviar informes de error de la página **Informes de errores** .  
  
     Haga clic en **Siguiente**.  
  
17. Revise posibles advertencias y, a continuación, haga clic en **Siguiente** en la página **Reglas de configuración de instalación** .  
  
18. En la página **Listo para instalar** , examine el resumen de la instalación y, a continuación, haga clic en **Siguiente**. El resumen incluirá un **Reporting Services** nodo que incluirá el valor del modo de instalación de **SharePointFilesOnlyMode** , así como la información de cuenta.  
  

  
##  <a name="bkmk_install_SSRS_sharedservice"></a> Instale e inicie el servicio de SharePoint de Reporting Services  
 ![Contenido relacionado con PowerShell](../../../2014/reporting-services/media/rs-powershellicon.jpg "Contenido relacionado con PowerShell")  
  
> [!NOTE]  
>  Si va a instalar en una granja de SharePoint existente, **no es necesario** completar los pasos descritos en esta sección. El servicio SharePoint de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] se instaló e inició cuando ejecutó el Asistente para la instalación de SQL Server en la sección anterior.  
  
 Los archivos necesarios se instalaron como parte de la instalación del Asistente para la instalación de SQL Server, pero los servicios tienen que ser registrados en la granja de servidores de SharePoint. La versión [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] incluye la compatibilidad con PowerShell para [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] en modo de SharePoint. Los pasos siguientes le guían a través de la apertura del Shell de administración de SharePoint y de la ejecución de cmdlets:  
  
1.  Haga clic en el botón **Inicio** .  
  
2.  Haga clic en el **productos de Microsoft SharePoint 2010** grupo.  
  
3.  Haga clic en **SharePoint 2010 Management Shell** haga clic en **ejecutar como administrador**.  
  
4.  Ejecute el siguiente comando de PowerShell para instalar el servicio de SharePoint. Si el comando se completa correctamente, muestra una nueva línea en el shell de administración. No se devuelve ningún mensaje al shell de administración cuando el comando se completa correctamente:  
  
    ```  
    Install-SPRSService  
    ```  
  
5.  Ejecute el siguiente comando de PowerShell para instalar el proxy del servicio:  
  
    ```  
    Install-SPRSServiceProxy  
    ```  
  
6.  Ejecute el siguiente comando de PowerShell para iniciar el servicio o vea en las notas siguientes las indicaciones para iniciar el servicio de Administración Central de SharePoint:  
  
    ```  
    get-spserviceinstance -all |where {$_.TypeName -like "SQL Server Reporting*"} | Start-SPServiceInstance  
    ```  
  
 También puede iniciar el servicio de Administración central de SharePoint en lugar de ejecutar el tercer comando de PowerShell. Los siguientes pasos también son útiles para comprobar que el servicio se está ejecutando.  
  
1.  En Administración central de SharePoint, haga clic en **Administrar servicios en el servidor** en el grupo **Configuración del sistema** .  
  
2.  Busque **Servicio SQL Server Reporting Services** y haga clic en **Iniciar** en la columna Acción.  
  
3.  El estado del servicio Reporting Services cambiará de **Detenido** a **Iniciado**. Si el servicio Reporting Services no está en la lista, use PowerShell para instalar el servicio.  
  
    > [!NOTE]  
    >  Si el servicio de Reporting Services se queda en el **iniciando** estado y no cambia a **iniciado**, compruebe el servicio 'Administración de SharePoint 2010' se ha iniciado en el administrador del servidor de Windows.  
  

  
##  <a name="bkmk_create_serrviceapplication"></a> Crear una aplicación de servicio de Reporting Services  
 En esta sección se proporcionan los pasos para crear una aplicación de servicio y una descripción de las propiedades, si está revisando una aplicación de servicio existente.  
  
1.  En Administración central de SharePoint, en el grupo **Administración de aplicaciones** , haga clic en **Administrar aplicaciones de servicio**.  
  
2.  En la cinta de SharePoint, haga clic en el botón **Nuevo** .  
  
3.  En el menú Nuevo, haga clic en **Aplicación de servicio de SQL Server Reporting Services**.  
  
    > [!WARNING]  
    >  Si la opción [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] no aparece en la lista, es **indicativo de que el servicio compartido de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] no está instalado**. Revise la sección anterior sobre cómo utilizar cmdlts de PowerShell para instalar el servicio [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)].  
  
4.  En la página **Crear aplicación de servicio de SQL Server Reporting Services** , escriba un nombre para la aplicación. Si va a crear varias aplicaciones de servicio de Reporting Services, un nombre descriptivo o una convención de nomenclatura le ayudan a organizar las operaciones y la administración.  
  
5.  En la sección **Grupo de aplicaciones** , cree un grupo de aplicaciones para la aplicación (recomendado). Utilizar el mismo nombre para el nuevo grupo de aplicaciones que la aplicación de servicio facilita su administración continuada.  
  
     Seleccione o cree una cuenta administrada para el grupo de aplicaciones. No olvide especificar una cuenta de usuario de dominio. Una cuenta de usuario de dominio habilita el uso de la característica de cuentas administradas de SharePoint, que permite actualizar la información de cuentas y contraseñas en un solo lugar. Las cuentas de dominio también se necesitan si planea escalar horizontalmente la implementación para incluir instancias de servicio adicionales que se ejecutan bajo la misma identidad.  
  
6.  En **Servidor de bases de datos**, puede usar el servidor actual o elegir otro servidor SQL Server diferente.  
  
7.  En **Nombre de la base de datos** , el valor predeterminado es `ReportingService_<guid>`, que es un nombre de base de datos único. Si escribe un nuevo valor, escriba un valor único.  
  
8.  En **Autenticación de bases de datos**, el valor predeterminado es Autenticación de Windows. Si elige **Autenticación de SQL**, consulte la guía del administrador de SharePoint para obtener información sobre cómo usar este tipo de autenticación en una implementación de SharePoint.  
  
9. En la sección **Asociación de aplicación web** , seleccione la aplicación web que se va a aprovisionar para el acceso de la aplicación de servicio de Reporting Services. Puede asociar una aplicación de servicio de Reporting Services a una aplicación web. Si todas las aplicaciones web actuales ya están asociadas a una aplicación de servicio de Reporting Services, ve un mensaje de advertencia.  
  
10. Haga clic en **Aceptar**.  
  
11. El proceso de creación de la aplicación de servicio podría tardar varios minutos en completarse. Cuando se complete, verá un mensaje de confirmación y un vínculo a una página **Aprovisionar suscripciones y alertas** . Complete el paso de aprovisionamiento si desea utilizar las características de alertas y las suscripciones de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]. Para más información, vea [Aprovisionar suscripciones y alertas para aplicaciones de servicio SSRS](../../reporting-services/install-windows/provision-subscriptions-and-alerts-for-ssrs-service-applications.md).  
  
 ![Contenido relacionado con PowerShell](../../../2014/reporting-services/media/rs-powershellicon.jpg "contenido relacionado con PowerShell") para obtener información sobre el uso de PowerShell para crear un [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] aplicación de servicio, consulte [para crear una aplicación de servicio de Reporting Services uso de PowerShell](../../../2014/reporting-services/reporting-services-sharepoint-service-and-service-applications.md#bkmk_powershell_create_ssrs_serviceapp).  
  

  
##  <a name="bkmk_powerview"></a> Activar la característica de colección de sitios de Power View.  
 [!INCLUDE[ssCrescent](../../includes/sscrescent-md.md)], una característica de [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] complemento para [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[SPS2010](../../includes/sps2010-md.md)] Enterprise Edition, es una característica de colección de sitios. La característica se activa automáticamente para colecciones de sitios raíz y se crean las colecciones de sitios tras instalar el complemento de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] . Si tiene previsto utilizar [!INCLUDE[ssCrescent](../../includes/sscrescent-md.md)], compruebe que la característica está activada.  
  
 Si instala el complemento de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] para productos de SharePoint 2010 después de instalar el producto de SharePoint 2010, la característica de integración del servidor de informes y la característica de integración de la vista avanzada se activarán únicamente para colecciones de sitios raíz. Para las demás colecciones de sitios, active manualmente las características.  
  
#### <a name="to-activate-the-power-view-feature"></a>Para activar la característica de la vista avanzada  
  
1.  Abra el explorador en el sitio de SharePoint que desee.  
  
2.  Haga clic en **Acciones del sitio**.  
  
3.  Haga clic en **Configuración del sitio**.  
  
4.  Haga clic en **Características de la colección de sitios** en el grupo Administración de la colección de sitios.  
  
5.  Busque **Característica Power View Integration** en la lista.  
  
6.  Haga clic en **Activar**.  
  
 Este procedimiento se completa en cada colección de sitios. Para obtener más información, consulte [activar el servidor de informes y Power View Integration Features in SharePoint](../../reporting-services/activate-the-report-server-and-power-view-integration-features-in-sharepoint.md) .  
  
##  <a name="bkmk_additional_config"></a> Configuración adicional  
 En esta sección se describen los pasos de configuración que son importantes para la mayoría de las implementaciones de SharePoint.  
  
###  <a name="bkmk_provision_agent"></a> Aprovisionar suscripciones y alertas  
 Las características de alerta de datos y suscripción de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] pueden requerir la configuración de permisos del Agente SQL Server. Si obtiene un mensaje de error que indica que se requiere el Agente SQL Server y ha comprobado que se está ejecutando, tiene que actualizar los permisos. Puede hacer clic en el vínculo **Aprovisionar suscripciones y alertas** en la página que indica que la aplicación de servicio se creó correctamente para ir a otra página y aprovisionar el Agente SQL Server. El paso de aprovisionamiento es necesario si la implementación cruza los límites del equipo, por ejemplo, cuando la instancia de la base de datos de SQL Server está en un equipo diferente. Para obtener más información, vea [Aprovisionar Subscripciones y alertas para aplicaciones de servicio SSRS](../../reporting-services/install-windows/provision-subscriptions-and-alerts-for-ssrs-service-applications.md).  
  

  
### <a name="configure-e-mail-for-a-service-application"></a>Configurar el correo electrónico para una aplicación de servicio  
 La característica de alertas de datos de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] envía alertas en los mensajes de correo electrónico. Para enviar correo electrónico, quizás tenga que configurar la aplicación de servicio de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] y modificar la extensión de entrega de correo electrónico para ella. Si piensa usar la extensión de entrega por correo electrónico para la característica de suscripción de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] , hay que configurar el correo electrónico. Para obtener más información, vea [Configurar el correo electrónico para una aplicación de servicio de Reporting Services &#40;SharePoint 2010 y SharePoint 2013&#41;](../../reporting-services/install-windows/configure-e-mail-for-a-reporting-services-service-application.md).  
  

  
### <a name="add-reporting-services-content-types"></a>Agregar tipos de contenido de Reporting Services  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] proporciona tipos de contenido predefinidos que se usan para administrar archivos de orígenes de datos compartidos (.rsds), modelos de informe (.smdl) y archivos de definición de informe (.rdl) del Generador de informes. Al agregar un tipo de contenido **Informe del Generador de informes**, **Modelo de informe**y **Origen de datos de informe** a una biblioteca se habilita el comando **Nuevo** para que pueda crear nuevos documentos de ese tipo. Para obtener más información, consulte [Agregar informe Server tipos de contenido en una biblioteca &#40;Reporting Services en modo integrado de SharePoint&#41;](../../../2014/reporting-services/add-reporting-services-content-types-to-a-sharepoint-library.md).  
  

  
### <a name="activate-the-file-sync-feature"></a>Activar la característica de sincronización de archivos  
 Si los usuarios cargan directamente y con frecuencia los elementos de informe publicados en las bibliotecas de documentos de SharePoint, la característica de sincronización de archivos del servidor de informes será beneficiosa. La característica de sincronización de archivos sincronizará el catálogo del servidor de informes con los elementos de las bibliotecas de documentos con más frecuencia. Para más información, consulte [Activar la característica de sincronización de archivos del servidor de informes en Administración central de SharePoint](../../../2014/reporting-services/activate-report-server-file-sync-feature-sharepoint-central-administration.md).  
  
## <a name="see-also"></a>Vea también  
 [Cmdlets de PowerShell para el modo de SharePoint de Reporting Services](../../../2014/reporting-services/powershell-cmdlets-for-reporting-services-sharepoint-mode.md)   
 [Características compatibles con las ediciones de SQL Server 2012](https://go.microsoft.com/fwlink/?linkid=232473)   
 [Aplicaciones de servicio y servicio de SharePoint de Reporting Services](../../../2014/reporting-services/reporting-services-sharepoint-service-and-service-applications.md)  
  
  
