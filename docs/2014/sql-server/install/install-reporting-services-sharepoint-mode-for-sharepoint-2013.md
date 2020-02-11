---
title: Instalar Reporting Services modo de SharePoint para SharePoint 2013 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
ms.assetid: b29d0f45-0068-4c84-bd7e-5b8a9cd1b538
author: maggiesMSFT
ms.author: maggies
manager: craigg
ms.openlocfilehash: 8874d4c57e2fb7b94e4efac44c90e93865d2b40f
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "72798338"
---
# <a name="install-reporting-services-sharepoint-mode-for-sharepoint-2013"></a>Instalar el modo de SharePoint de Reporting Services para SharePoint 2013
  Los procedimientos de este tema le guían por la instalación en un solo servidor de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] en modo de SharePoint. Los pasos incluyen la ejecución del Asistente para la instalación de SQL Server, así como tareas de configuración que usan Administración central de SharePoint. El tema también se puede usar para ver procedimientos individuales para actualizar una instalación existente, como crear una aplicación de servicio de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)].  
  
||  
|-|  
|**[!INCLUDE[applies](../../includes/applies-md.md)]** SharePoint 2013 &#124; **Nota:** [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] el modo de **SharePoint no admite la funcionalidad de** varios inquilinos de SharePoint Server.|  
  
 Para obtener información acerca de cómo agregar más servidores de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] a una granja existente, vea lo siguiente:  
  
-   [Agregar un servidor de informes adicional a una granja de servidores &#40;la escalabilidad horizontal de SSRS&#41;](../../reporting-services/install-windows/add-an-additional-report-server-to-a-farm-ssrs-scale-out.md)  
  
-   [Agregar un front-end web adicional de Reporting Services a una granja de servidores](../../reporting-services/install-windows/add-an-additional-reporting-services-web-front-end-to-a-farm.md)  
  
 Una instalación en un solo servidor es útil para escenarios de desarrollo y pruebas, pero no se recomienda en entornos de producción.  
  
 **En este tema:**  
  
-   [Ejemplo de implementación de un solo servidor](#bkmk_singleserver)  
  
-   [Cuentas de instalación](#bkmk_setupaccounts)  
  
-   [Paso 1: instalar Reporting Services servidor de informes en modo de SharePoint](#bkmk_install_SSRS)  
  
-   [Paso 2: registrar e iniciar el servicio de SharePoint de Reporting Services](#bkmk_install_SSRS_sharedservice)  
  
-   [Paso 3: crear una aplicación de servicio de Reporting Services](#bkmk_create_serrviceapplication)  
  
-   [Paso 4: activar la característica de colección de sitios de Power View.](#bkmk_powerview)  
  
-   [Script de Windows PowerShell para los pasos 1-4](#bkmk_full_script)  
  
-   [Configuración adicional](#bkmk_additional_config) , incluido el aprovisionamiento de suscripciones y alertas, [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] tipos de contenido y configuración de Excel Services para usar un servidor de Analysis Services.  
  
-   [Comprobación de la instalación](#bkmk_verify_installation)  
  
##  <a name="bkmk_singleserver"></a>Ejemplo de implementación de un solo servidor  
 Una instalación en un solo servidor es útil para escenarios de desarrollo y pruebas, pero no se recomienda usar un solo servidor en un entorno de producción. El entorno de un solo servidor hace referencia a un solo equipo que tiene SharePoint y los componentes de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] instalados en el mismo equipo. El tema no trata el escalado horizontal con varios servidores de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] .  
  
 En el diagrama siguiente se muestran los componentes que forman parte de una implementación de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] de un solo servidor.  
  
|||  
|-|-|  
|**dimensional**|Servicio de SharePoint instalado desde la instalación de SQL Server. Puede crear una o varias aplicaciones de servicio [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] .|  
|**dos**|
  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] complemento para productos de SharePoint proporciona los componentes de la interfaz de usuario en los servidores de SharePoint.|  
|**3**|La aplicación de servicio de Excel usada por Power View y PowerPivot.|  
|**4**|Aplicación de servicio PowerPivot.|  
  
 ![Implementación de un solo servidor en el modo SSRS de SharePoint](../../../2014/sql-server/install/media/rs-sharepoint-1server-deployment.gif "Implementación de un solo servidor en el modo SSRS de SharePoint")  
  
> [!TIP]  
>  Para obtener ejemplos de implementación más complejos, vea [Topologías de implementación para las características BI de SQL Server](deployment-topologies-for-sql-server-bi-features-in-sharepoint.md).  
  
##  <a name="bkmk_setupaccounts"></a>Cuentas de instalación  
 En esta sección se describen las cuentas y los permisos usados para los principales pasos de implementación de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] en modo de SharePoint.  
  
 **Instalación y registro del [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] servicio:**  
  
-   La cuenta actual durante la instalación (denominada cuenta de ' instalación ') de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] en modo de SharePoint debe tener derechos administrativos en el equipo local. Si va a instalar [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] después de instalar SharePoint y la cuenta de ' instalación ' también es miembro del grupo administradores de la granja de servidores de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] SharePoint, la instalación [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] registrará el servicio. Si instala [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] antes de instalar SharePoint o la cuenta de ' instalación ' no es miembro del grupo administradores de la granja, registre el servicio manualmente. Vea la sección [Paso 2: registrar e iniciar el servicio SharePoint de Reporting Services](#bkmk_install_SSRS_sharedservice).  
  
 **Crear [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] aplicaciones de servicio**  
  
-   Después de instalar y registrar el servicio [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] , cree una o más aplicaciones de servicio de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] . La "cuenta del servicio de la granja de servidores de SharePoint" debe ser temporalmente miembro del grupo local de administradores para que la aplicación de servicio de Reporting Services se pueda crear. Para obtener más información sobre los permisos de cuenta de SharePoint 2013, vea [configuración de seguridad y permisos de cuenta en sharepoint 2013](https://technet.microsoft.com/library/cc678863.aspx) (https://technet.microsoft.com/library/cc678863.aspx).  
  
     Es una práctica recomendada de seguridad que las cuentas de administrador de la granja de servidores de SharePoint no sean también cuentas locales de administrador del sistema operativo. Si agrega una cuenta de administrador de la granja de servidores al grupo local de administradores como parte del proceso de instalación, se recomienda que quite la cuenta del grupo local de administradores una vez completada la instalación.  
  
##  <a name="bkmk_install_SSRS"></a>Paso 1: instalar Reporting Services servidor de informes en modo de SharePoint  
 Este paso instala un servidor de informes de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] en modo de SharePoint y el complemento [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] para productos de SharePoint. Según lo que ya esté instalado en el equipo, quizás no vea algunas de las páginas de instalación que se describen en los pasos siguientes.  
  
1.  Ejecute el Asistente para la instalación de SQL Server (Setup.exe).  
  
2.  Haga clic en **Instalación** en el lado izquierdo del asistente y, a continuación, haga clic en **Nueva instalación independiente de SQL Server o agregar características a una instalación existente**.  
  
3.  Haga clic en **Aceptar** en la página **Reglas auxiliares del programa de instalación** , suponiendo que se han pasado todas las reglas.  
  
4.  Haga clic en **Instalar** en la página **Archivos auxiliares del programa de instalación** . Según lo que ya esté instalado en el equipo, podría ver el mensaje siguiente:  
  
    -   "Uno o varios archivos afectados tienen operaciones pendientes. Debe reiniciar el equipo una vez completado el proceso de actualización".  
  
    -   Haga clic en **Aceptar**.  
  
5.  Haga clic en **Siguiente** después de completarse la instalación de los archivos auxiliares y de que las páginas **Reglas auxiliares** muestren el estado **Superada**. Revise posibles advertencias o problemas de bloqueo.  
  
6.  En la página **Tipo de instalación** , haga clic en **Agregar características a una instancia existente de SQL Server 2014**. Seleccione la instancia correcta en la lista desplegable y haga clic en **Siguiente**.  
  
7.  Si ve la página **Clave del producto**, escriba la clave o acepte el valor predeterminado de la edición "Enterprise Evaluation".  
  
     Haga clic en **Next**.  
  
8.  Si ve la página Términos de licencia, examine y acepte los términos de licencia. Microsoft aprecia que haga clic para indicar que está conforme con enviar datos de uso de las características para ayudarle a mejorar las características y el soporte técnico de los productos.  
  
     Haga clic en **Next**.  
  
9. Si ve la página **Rol de instalación** , seleccione **Instalación de características de SQL Server**.  
  
     Haga clic en **Siguiente**.  
  
     ![Instalación de la característica de SQL Server para el rol de instalación](../../../2014/sql-server/install/media/rs-setuprole.gif "Instalación de la característica de SQL Server para el rol de instalación")  
  
10. Seleccione lo siguiente en la página **Selección de características** :  
  
    -   **Reporting Services-SharePoint**  
  
    -   **Reporting Services complemento para productos de SharePoint**.  
  
         ![Nota:](../../../2014/reporting-services/media/rs-fyinote.png "note") La opción del Asistente para la instalación de para instalar el complemento es nueva [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] en la versión.  
  
    -   Si aún no tiene una instancia del [!INCLUDE[ssDE](../../includes/ssde-md.md)]de SQL Server, también podría seleccionar **Servicios de Motor de base de datos** y **Herramientas de administración - Completa** para un entorno completo.  
  
     Haga clic en **Next**.  
  
     ![Selección de características de SSRS para el modo SharePoint](../../../2014/sql-server/install/media/rs-setupfeatureselection-sharepoint-with-circles.gif "Selección de características de SSRS para el modo SharePoint")  
  
11. Si ve la página **Reglas de instalación** . Revise posibles advertencias o problemas de bloqueo. A continuación, haga clic en **siguiente**  
  
12. Si seleccionó los servicios del Motor de base de datos, acepte la instancia predeterminada de **MSSQLSERVER** en la página **Configuración de instancia** y haga clic en **Siguiente**.  
  
     ![Nota:](../../../2014/reporting-services/media/rs-fyinote.png "note") La arquitectura de servicio de SharePoint de Reporting Services no se basa en una SQL Server "instancia" como era la arquitectura de Reporting Services anterior.  
  
13. Examine la página **Requisitos de espacio en disco** y haga clic en **Siguiente**.  
  
14. Si ve la página **Configuración del servidor** , escriba las credenciales adecuadas. Si desea usar las características de suscripción o alerta de datos de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] , necesita cambiar el **Tipo de inicio** para el Agente SQL Server a **Automático**. Quizás no vea la página **Configuración del servidor** , en función de lo que ya esté instalado en el equipo.  
  
     Haga clic en **Next**.  
  
15. Si seleccionó los servicios del Motor de base de datos, verá la página **Configuración del Motor de base de datos** ; agregue las cuentas adecuadas a la lista de administradores de SQL y haga clic en **Siguiente**.  
  
16. En la página **Configuración de Reporting Services** debe ver que la opción **Solo instalar** está seleccionada. Esta opción instala los archivos del servidor de informes y no configura el entorno de SharePoint para [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)].  
  
    > [!NOTE]  
    >  Una vez completada la instalación de SQL Server, vea las demás secciones de este tema para configurar el entorno de SharePoint. Esto incluye instalar el servicio compartido de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] y la creación de las aplicaciones de servicio de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] .  
  
     ![Página de configuración de SSRS del Asistente para la instalación de SQL Server](../../../2014/sql-server/install/media/rs-2012sp1-setup-ssrs-configpage-with-circles.gif "Página de configuración de SSRS del Asistente para la instalación de SQL Server")  
  
17. Ayude a Microsoft a mejorar las características y los servicios de SQL Server activando la casilla para enviar informes de error de la página **Informes de errores** .  
  
     Haga clic en **Next**.  
  
18. Revise posibles advertencias y, a continuación, haga clic en **Siguiente** en la página **Reglas de configuración de instalación** .  
  
19. En la página **Listo para instalar** , examine el resumen de la instalación y, a continuación, haga clic en **Siguiente**. El resumen incluirá un nodo secundario **Modo de SharePoint de Reporting Services** que muestra un valor **SharePointFilesOnlyMode**. Haga clic en **Instalar**.  
  
20. La instalación tardará varios minutos. Verá la página **Operación completada** en la que se enumeran las características y el estado de cada una de ellas. Puede ver un cuadro de diálogo de información que indica que el equipo debe reiniciarse.  
  
##  <a name="bkmk_install_SSRS_sharedservice"></a>Paso 2: registrar e iniciar el servicio de SharePoint de Reporting Services  
 ![Contenido relacionado con PowerShell](../../../2014/reporting-services/media/rs-powershellicon.jpg "Contenido relacionado con PowerShell")  
  
> [!NOTE]  
>  Si va a realizar la instalación en una granja de SharePoint existente, no necesita completar los pasos de esta sección. El servicio SharePoint de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] se instaló e inició cuando ejecutó el Asistente para la instalación de SQL Server como parte de la sección anterior de este documento.  
  
 A continuación se exponen los motivos habituales por los que debe registrar manualmente el servicio [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] .  
  
-   Instaló el modo de SharePoint de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] antes de instalar SharePoint.  
  
-   La cuenta usada para instalar el modo de SharePoint de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] no era miembro del grupo de administradores de la granja de servidores de SharePoint. Para obtener más información, vea la sección [Setup accounts](#bkmk_setupaccounts).  
  
 Los archivos necesarios se instalaron como parte de la instalación del Asistente para la instalación de SQL Server, pero los servicios tienen que ser registrados en la granja de servidores de SharePoint. La versión [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] incluye la compatibilidad con PowerShell para [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] en modo de SharePoint.  
  
 Los pasos siguientes le guían a través de la apertura del Shell de administración de SharePoint y de la ejecución de cmdlets:  
  
1.  Haga clic en el botón **Inicio**  
  
2.  Haga clic en el grupo **Productos de Microsoft SharePoint 2013** .  
  
3.  Haga clic con el botón secundario en **Shell de administración de SharePoint 2013** y, a continuación, haga clic en **Ejecutar como administrador**. NOTA: los comandos de SharePoint no se reconocen en la ventana estándar de Windows PowerShell. Use el **Shell de administración de SharePoint 2013**.  
  
4.  Ejecute el siguiente comando de PowerShell para instalar el servicio de SharePoint. Si el comando se completa correctamente, muestra una nueva línea en el shell de administración. **No se devuelve ningún mensaje** al shell de administración cuando el comando se completa correctamente:  
  
    ```powershell
    Install-SPRSService  
    ```  
  
    > [!IMPORTANT]  
    >  Si ve un mensaje de error similar al siguiente:  
    >   
    >  Install-SPRSService: el término ' Install-SPRSService ' **no se reconoce** como  
    > nombre de un cmdlet, función, archivo de script o programa ejecutable. Active la  
    > escribió correctamente el nombre, o si incluyó una ruta de acceso, compruebe que dicha ruta  
    > es correcta e inténtelo de nuevo.  
  
5.  Ejecute el siguiente comando de PowerShell para instalar el proxy del servicio. Si el comando se completa correctamente, muestra una nueva línea en el shell de administración. **No se devuelve ningún mensaje** al shell de administración cuando el comando se completa correctamente:  
  
    ```powershell
    Install-SPRSServiceProxy  
    ```  
  
6.  Ejecute el siguiente comando de PowerShell para iniciar el servicio o vea en las notas siguientes las instrucciones para iniciar el servicio desde Administración central de SharePoint:  
  
    ```powershell
    Get-SPServiceInstance -all |where {$_.TypeName -like "SQL Server Reporting*"} | Start-SPServiceInstance  
    ```  
  
 Está en Windows Powershell en lugar del Shell de administración de SharePoint o el modo de SharePoint de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] no está instalado. Para obtener más información sobre [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] y PowerShell, vea [Cmdlets de PowerShell para el modo de SharePoint de Reporting Services](../../../2014/reporting-services/powershell-cmdlets-for-reporting-services-sharepoint-mode.md).  
  
 También puede iniciar el servicio de Administración central de SharePoint en lugar de ejecutar el tercer comando de PowerShell. Los siguientes pasos también son útiles para comprobar que el servicio se está ejecutando.  
  
1.  En Administración central de SharePoint, haga clic en **Administrar servicios en el servidor** en el grupo **Configuración del sistema** .  
  
2.  Busque **Servicio SQL Server Reporting Services** y haga clic en **Iniciar** en la columna Acción.  
  
3.  El estado del servicio Reporting Services cambiará de **Detenido** a **Iniciado**. Si el servicio Reporting Services no está en la lista, use PowerShell para instalar el servicio.  
  
    > [!NOTE]  
    >  Si el servicio de Reporting Services se queda en estado **Iniciando** y no cambia a **Iniciado**, compruebe que el servicio "Administración de SharePoint 2013" se ha iniciado en el Administrador de Windows Server.  
  
##  <a name="bkmk_create_serrviceapplication"></a>Paso 3: crear una aplicación de servicio de Reporting Services  
 En esta sección se proporcionan los pasos para crear una aplicación de servicio y una descripción de las propiedades, si está revisando una aplicación de servicio existente.  
  
1.  En administración central de SharePoint, en el grupo **Administración de aplicaciones** , haga clic en **Administrar aplicaciones de servicio**.  
  
2.  En la cinta de SharePoint, haga clic en el botón **Nuevo** .  
  
3.  En el menú Nuevo, haga clic en **Aplicación de servicio de SQL Server Reporting Services**.  
  
    > [!IMPORTANT]  
    >  Si la opción [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] no aparece en la lista, es **indicativo de que el servicio compartido de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] no está instalado**. Revise la sección anterior sobre cómo utilizar cmdlts de PowerShell para instalar el servicio [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)].  
  
4.  En la página **Crear aplicación de servicio de SQL Server Reporting Services** , escriba un nombre para la aplicación. Si va a crear varias aplicaciones de servicio de Reporting Services, un nombre descriptivo o una convención de nomenclatura le ayudará a organizar las operaciones de administración.  
  
5.  En la sección **Grupo de aplicaciones** , cree un grupo de aplicaciones para la aplicación (recomendado). Si usa el mismo nombre para el grupo de aplicaciones y para la aplicación de servicio, puede simplificar la administración continuada. Esto también puede verse afectado por el número de aplicaciones de servicio que creará y si necesita usar varias aplicaciones de un solo grupo. Consulte la documentación de SharePoint Server para ver recomendaciones y prácticas recomendadas para la administración de grupos de aplicaciones.  
  
     Seleccione o cree una cuenta de seguridad para el grupo de aplicaciones. No olvide especificar una cuenta de usuario de dominio. Una cuenta de usuario de dominio habilita el uso de la característica de cuentas administradas de SharePoint, que permite actualizar la información de cuentas y contraseñas en un solo lugar. Las cuentas de dominio también se necesitan si planea escalar horizontalmente la implementación para incluir instancias de servicio adicionales que se ejecutan bajo la misma identidad.  
  
6.  En **Servidor de bases de datos**, puede usar el servidor actual o elegir otro servidor SQL Server diferente.  
  
7.  En **Nombre de la base de datos** , el valor predeterminado es `ReportingService_<guid>`, que es un nombre de base de datos único. Si escribe un nuevo valor, escriba un valor único. Es la nueva base de datos que se crea específicamente para la aplicación de servicio.  
  
8.  En **Autenticación de bases de datos**, el valor predeterminado es Autenticación de Windows. Si elige **Autenticación de SQL**, consulte la documentación de SharePoint para conocer las prácticas recomendadas sobre cómo usar este tipo de autenticación en una implementación de SharePoint.  
  
9. En la sección **Asociación de aplicación web** , seleccione la aplicación web que se va a aprovisionar para el acceso de la aplicación de servicio de Reporting Services. Puede asociar una aplicación de servicio de Reporting Services a una aplicación web. Si todas las aplicaciones web actuales ya están asociadas a una aplicación de servicio de Reporting Services, ve un mensaje de advertencia.  
  
10. Haga clic en **OK**.  
  
11. El proceso de creación de la aplicación de servicio podría tardar varios minutos en completarse. Cuando se complete, verá un mensaje de confirmación y un vínculo a una página **Aprovisionar suscripciones y alertas** . Complete el paso de aprovisionamiento si desea usar las características de suscripciones o de alertas de datos de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] . Para más información, vea [Aprovisionar suscripciones y alertas para aplicaciones de servicio SSRS](../../reporting-services/install-windows/provision-subscriptions-and-alerts-for-ssrs-service-applications.md).  
  
 ![Contenido relacionado con PowerShell](../../../2014/reporting-services/media/rs-powershellicon.jpg "Contenido relacionado con PowerShell") Para obtener información sobre el uso de PowerShell [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] para crear una aplicación de servicio, consulte:  
  
-   Vea la siguiente sección [Script de Windows PowerShell para los pasos 1 a 4](#bkmk_full_script).  
  
-   Tema [Para crear una aplicación de servicio de Reporting Services mediante PowerShell](../../../2014/reporting-services/reporting-services-sharepoint-service-and-service-applications.md#bkmk_powershell_create_ssrs_serviceapp).  
  
##  <a name="bkmk_powerview"></a>Paso 4: activar la característica de colección de sitios de Power View.  
 
  [!INCLUDE[ssCrescent](../../includes/sscrescent-md.md)], una característica del [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)][!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] complemento para [!INCLUDE[msCoName](../../includes/msconame-md.md)] productos SharePoint, es una característica de colección de sitios. La característica se activa automáticamente para colecciones de sitios raíz y se crean las colecciones de sitios tras instalar el complemento de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] . Si tiene previsto utilizar [!INCLUDE[ssCrescent](../../includes/sscrescent-md.md)], compruebe que la característica está activada.  
  
 Si instala el complemento [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] para productos de SharePoint después de instalar SharePoint Server, la característica de integración del servidor de informes y la característica de Power View solo se activarán para las colecciones de sitios raíz. Para las demás colecciones de sitios, active manualmente las características.  
  
#### <a name="to-activate-or-verify-the-power-view-site-collection-feature"></a>Para activar o comprobar la característica de colección de sitios de Power View  
  
1.  En los pasos siguientes se da por supuesto que el sitio de SharePoint está configurado para la **versión de la experiencia**2013.  
  
     Abra el explorador en el sitio de SharePoint que desee. Por ejemplo, http://\<nombreServidor>/sites/bi  
  
2.  Haga clic en **configuración**![configuración de SharePoint](https://docs.microsoft.com/analysis-services/analysis-services/media/as-sharepoint2013-settings-gear.gif "Configuración de SharePoint").  
  
3.  Haga clic en **configuración del sitio**.  
  
4.  En el grupo **Administración de la colección de sitios** , haga clic en **Características de la colección de sitios**.  
  
5.  Busque **Característica Power View Integration** en la lista.  
  
6.  Haga clic en **Activar**. El estado de la característica cambiará a **Activo**.  
  
 Este procedimiento se completa en cada colección de sitios. Para más información, consulte [Activate the Report Server and Power View Integration Features in SharePoint](../../../2014/reporting-services/activate-the-report-server-and-power-view-integration-features-in-sharepoint.md).  
  
##  <a name="bkmk_full_script"></a>Script de Windows PowerShell para los pasos 1-4  
 El script de PowerShell de esta sección es el equivalente a completar los pasos 1 a 4 de las secciones anteriores. El script hace lo siguiente:  
  
-   Instala el servicio [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] y el proxy del servicio, e inicia el servicio.  
  
-   Crea un proxy del servicio denominado "Reporting Services".  
  
-   Crea una [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] aplicación de servicio denominada "Reporting Services aplicación".  
  
-   Habilita la característica [!INCLUDE[ssCrescent](../../includes/sscrescent-md.md)] para una colección de sitios.  
  
 Parámetros  
  
-   Actualice el parámetro **-Account** del proxy del servicio. La cuenta debe ser una cuenta de servicio administrada en la granja de servidores de SharePoint. Para obtener más información, vea el tema de SharePoint [Planeación de cuentas administrativas y de servicio en SharePoint 2013](https://technet.microsoft.com/library/cc263445.aspx).  
  
-   Actualice el parámetro **-DatabaseServer** para la aplicación de servicio. Este parámetro es la instancia del motor de base de datos  
  
-   Actualice el parámetro **-url** del sitio en el que quiera habilitar la característica [!INCLUDE[ssCrescent](../../includes/sscrescent-md.md)].  
  
 **Para usar el script:**  
  
1.  Abra Windows PowerShell con privilegios de administrador.  
  
2.  Copie el código siguiente en la ventana de script.  
  
3.  Actualice los tres parámetros descritos en la sección anterior y ejecute el script.  
  
```powershell
#This script Configures SQL Server Reporting Services SharePoint mode  
  
$starttime = Get-Date  
Write-Host -foregroundcolor DarkGray StartTime>> $starttime   
  
Write-Host -ForegroundColor Green "Import the SharePoint PowerShell snappin"  
Add-PSSnapin Microsoft.Sharepoint.Powershell -EA 0  
  
Write-Host -ForegroundColor Green "Install SSRS Service and Service Proxy, and start the service"  
Write-Host -ForegroundColor Green ">>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>"  
  
    Write-Host -ForegroundColor Green "Install the Reporting Services Shared Service"  
    Install-SPRSService  
  
    Write-Host -ForegroundColor Green " Install the Reporting Services Service Proxy"  
    Install-SPRSServiceProxy  
  
    # Get the ID of the RS Service Instance and start the service   
    Write-Host -ForegroundColor Green "Start the Reporting Services Service"  
    $RS = Get-SPServiceInstance | Where {$_.TypeName -eq "SQL Server Reporting Services Service"}  
    Start-SPServiceInstance -Identity $RS.Id.ToString()  
  
    # Wait for the Reporting Services Service to start...  
    $Status = Get-SPServiceInstance $RS.Id.ToString()  
    While ($Status.Status -ne "Online")  
    {  
        Write-Host -ForegroundColor Green "SSRS Service Not Online...Current Status = " $Status.Status  
        Start-Sleep -Seconds 2  
        $Status = Get-SPServiceInstance $RS.Id.ToString()  
    }  
  
$time = Get-Date  
Write-Host -foregroundcolor DarkGray StartTime>> $starttime   
Write-Host -foregroundcolor DarkGray $time  
  
Write-Host -ForegroundColor Green "Create a new application pool and Reporting Services service application"  
Write-Host -ForegroundColor Green ">>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>"  
Write-Host -ForegroundColor Green "Create a new application pool"  
#!!!! update "-Account" with an existing Managed Service Account  
New-SPServiceApplicationPool -Name "Reporting Services" -Account "<domain>\User name>"  
$appPool = Get-SPServiceApplicationPool "Reporting Services"  
  
Write-Host -ForegroundColor Green " Create the Reporting Services Service Application"  
#!!!! Update "-DatabaseServer", an instance of the SQL Server database engine   
$rsService = New-SPRSServiceApplication -Name "Reporting Services Application" -ApplicationPool $appPool -DatabaseName "Reporting_Services_Application" -DatabaseServer "<server name>"  
  
Write-Host -ForegroundColor Green "Create the Reporting Services Service Application Proxy"  
$rsServiceProxy = New-SPRSServiceApplicationProxy -Name "Reporting Services Application Proxy" -ServiceApplication $rsService  
  
Write-Host -ForegroundColor Green "Associate service application proxy to default web site and grant web applications rights to SSRS application pool"  
Write-Host -ForegroundColor Green ">>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>"     
# Associate the Reporting Services Service Applicatoin Proxy to the default web site...  
Get-SPServiceApplicationProxyGroup -default | Add-SPServiceApplicationProxyGroupMember -Member $rsServiceProxy  
  
$time=Get-Date  
Write-Host -foregroundcolor DarkGray StartTime>> $starttime   
Write-Host -foregroundcolor DarkGray $time  
  
Write-Host -ForegroundColor Green "Enable the PowerView and reportserver site features"  
Write-Host -ForegroundColor Green ">>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>"  
#!!!! update "-url"  of the site where you want the features enabled  
Enable-SPfeature -identity "powerview" -Url http://server/sites/bi  
Enable-SPfeature -identity "reportserver" -Url http://server/sites/bi  
  
####To Verify, you can run the following:  
#Get-SPRSServiceApplication  
#Get-SPServiceApplicationPool | where {$_.name -like "reporting*"}  
#Get-SPRSServiceApplicationProxy
```  
  
##  <a name="bkmk_additional_config"></a>Configuración adicional  
 En esta sección se describen los pasos de configuración que son importantes para la mayoría de las implementaciones de SharePoint.  
  
###  <a name="bkmk_configure_ECS"></a>Configurar Excel Services y PowerPivot  
 Si desea ver informes de [!INCLUDE[ssCrescent](../../includes/sscrescent-md.md)] de un libro de Excel 2013 en SharePoint, es necesario configurar una aplicación de servicio de Excel en la granja para que use un servidor de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] en modo de SharePoint. Además, la cuenta de seguridad del grupo de aplicaciones usada por la aplicación de servicio de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] debe ser administrador del servidor de Analysis Services. Para obtener más información, vea lo siguiente:  
  
-   La sección "configurar Excel Services para la integración de Analysis Services" en la [instalación de PowerPivot para SharePoint 2013](https://docs.microsoft.com/analysis-services/instances/install-windows/install-analysis-services-in-power-pivot-mode).  
  
-   [Administrar la configuración del modelo de datos de servicios de Excel (SharePoint Server 2013)](https://technet.microsoft.com/library/jj219780.aspx).  
  
###  <a name="bkmk_provision_agent"></a>Aprovisionar suscripciones y alertas  
 Las características de alerta de datos y suscripción de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] pueden requerir la configuración de permisos del Agente SQL Server. Si obtiene un mensaje de error que indica que se requiere el Agente SQL Server y ha comprobado que se está ejecutando, tiene que actualizar los permisos. Puede hacer clic en el vínculo **Aprovisionar suscripciones y alertas** en la página que indica que la aplicación de servicio se creó correctamente para ir a otra página y aprovisionar el Agente SQL Server. El paso de aprovisionamiento es necesario si la implementación cruza los límites del equipo, por ejemplo, cuando la instancia de la base de datos de SQL Server está en un equipo diferente. Para obtener más información, vea [aprovisionar suscripciones y alertas para aplicaciones de servicio de SSRS](../../reporting-services/install-windows/provision-subscriptions-and-alerts-for-ssrs-service-applications.md) .  
  
### <a name="configure-e-mail-for-ssrs-service-applications"></a>Configurar el correo electrónico para aplicaciones de servicio de SSRS  
 La característica de alertas de datos de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] envía alertas en los mensajes de correo electrónico. Para enviar correo electrónico, quizás tenga que configurar la aplicación de servicio de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] y modificar la extensión de entrega de correo electrónico para ella. Si piensa usar la extensión de entrega por correo electrónico para la característica de suscripción de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)], hay que configurar el correo electrónico. Para obtener más información, vea [Configurar el correo electrónico para una aplicación de servicio de Reporting Services &#40;SharePoint 2010 y SharePoint 2013&#41;](../../reporting-services/install-windows/configure-e-mail-for-a-reporting-services-service-application.md).  
  
### <a name="add-reporting-services-content-types-to-content-libraries"></a>Agregar tipos de contenido de Reporting Services a bibliotecas de contenido  
 
  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] proporciona tipos de contenido predefinidos que se usan para administrar archivos de orígenes de datos compartidos (.rsds), modelos de informe (.smdl) y archivos de definición de informe (.rdl) del Generador de informes. Al agregar un tipo de contenido **Informe del Generador de informes**, **Modelo de informe**y **Origen de datos de informe** a una biblioteca se habilita el comando **Nuevo** para que pueda crear nuevos documentos de ese tipo. Para obtener más información, vea [agregar tipos de contenido del servidor de informes a una biblioteca &#40;Reporting Services en el modo integrado de SharePoint&#41;](../../../2014/reporting-services/add-reporting-services-content-types-to-a-sharepoint-library.md).  
  
### <a name="activate-the-report-server-file-sync-feature"></a>Activar la característica de sincronización de archivos del servidor de informes  
 Si los usuarios van a cargar con frecuencia elementos de informe publicados directamente en bibliotecas de documentos de SharePoint, la característica de nivel de sitio **Sincronizar archivo del Servidor de informes** será beneficiosa. La característica de sincronización de archivos sincronizará el catálogo del servidor de informes con los elementos de las bibliotecas de documentos con más frecuencia. Para obtener más información, vea [activar la característica File Sync del servidor de informes en administración central de SharePoint](../../../2014/reporting-services/activate-report-server-file-sync-feature-sharepoint-central-administration.md).  
  
##  <a name="bkmk_verify_installation"></a>Comprobar la instalación  
 A continuación se muestran los pasos y procedimientos sugeridos para comprobar la implementación de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] en modo de SharePoint.  
  
-   Vea la sección de SharePoint en el tema de comprobación [Verify a Reporting Services Installation](../../reporting-services/install-windows/verify-a-reporting-services-installation.md).  
  
-   En una biblioteca de documentos de SharePoint, cree un informe básico de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] que solo contenga un cuadro de texto, por ejemplo un título. El informe no contiene ningún origen de datos o conjuntos de datos. El objetivo es comprobar que puede abrir el Generador de informes, crear un informe básico y obtener una vista previa del mismo.  
  
     Guarde el informe en la biblioteca de documentos y ejecútelo desde la biblioteca. Para obtener más información sobre cómo crear informes con el Generador de informes, vea [Iniciar el Generador de informes (Generador de informes)](https://technet.microsoft.com/library/ms159221.aspx).  
  
## <a name="see-also"></a>Consulte también  
 [Cmdlets de PowerShell para el modo de SharePoint de Reporting Services](../../../2014/reporting-services/powershell-cmdlets-for-reporting-services-sharepoint-mode.md)   
 [Actualización y migración de Reporting Services](../../reporting-services/install-windows/upgrade-and-migrate-reporting-services.md)   
 [Mapa de ruta de contenido: configuración y configuración de SharePoint Server y SQL Server BI](https://technet.microsoft.com/library/dn205112.aspx)   
 [Características admitidas por las ediciones de SQL Server 2012](https://go.microsoft.com/fwlink/?linkid=232473)   
 [Reporting Services las aplicaciones de servicio y servicio de SharePoint](../../../2014/reporting-services/reporting-services-sharepoint-service-and-service-applications.md)
