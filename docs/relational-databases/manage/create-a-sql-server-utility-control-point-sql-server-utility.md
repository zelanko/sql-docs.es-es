---
title: Crear un punto de control de la utilidad de SQL Server (utilidad de SQL Server)
description: Obtenga ayuda para identificar cuellos de botella de uso de recursos y oportunidades de consolidación mediante la creación de un punto de control (UCP) de la utilidad de SQL Server.
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
f1_keywords:
- sql13.SWB.create.ucp.validation.F1
- sql13.SWB.create.ucp.Summary.F1
- sql13.SWB.create.ucp.progress.F1
- sql13.SWB.create.ucp.agentconfiguration.F1
- sql13.SWB.create.ucp.welcome.F1
- sql13.SWB.create.ucp.instancename.F1
helpviewer_keywords:
- Create UCP
- UCP
ms.assetid: d5335124-1625-47ce-b4ac-36078967158c
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: d29ab79c75adb436b45faab5e8161c8d01e6c533
ms.sourcegitcommit: 01297f2487fe017760adcc6db5d1df2c1234abb4
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/09/2020
ms.locfileid: "86196899"
---
# <a name="create-a-sql-server-utility-control-point-sql-server-utility"></a>Crear un punto de control de la utilidad de SQL Server (utilidad de SQL Server)
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  Una empresa puede tener varias utilidades de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] y cada una de esas utilidades de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] puede administrar muchas instancias de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] y aplicaciones de capa de datos. Cada utilidad de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] dispone de un único punto de control de la utilidad (UCP). Debe crear un UCP nuevo para cada utilidad de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Cada instancia administrada de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] y todos los componentes de la aplicación de capa de datos pertenecen únicamente a una utilidad de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] y los administra un solo UCP.  
  
 El UCP recopila información de configuración y rendimiento de las instancias administradas de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] cada 15 minutos. Esta información se almacena en el almacén de administración de datos de la utilidad (UMDW) en el UCP; el nombre del archivo UMDW es sysutility_mdw. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] se comparan con directivas para ayudar a identificar cuellos de botella en el uso de recursos y oportunidades de consolidación.  
  
## <a name="before-you-begin"></a>Antes de empezar  
 Antes de crear un UCP, revise los siguientes requisitos y recomendaciones.  
  
 En esta versión, el UCP y todas las instancias administradas de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] deben satisfacer los requisitos siguientes:  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] debe ser de la versión 10.50 o posterior.  
  
-   El tipo de instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] debe ser [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
-   La utilidad de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] debe funcionar en un dominio de Windows único, o bien en dominios con relaciones bidireccionales de confianza.  
  
-   Las cuentas de servicio de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] en el UCP y todas las instancias administradas de SQL Server deben disponer de permisos de lectura para los usuarios de Active Directory.  
  
 En esta versión, el UCP debe satisfacer los siguientes requisitos:  
  
-   La instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] debe ser una edición admitida. Para obtener una lista de las características admitidas por las ediciones de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], vea [Características compatibles con las ediciones de SQL Server 2016](~/sql-server/editions-and-supported-features-for-sql-server-2016.md).  
  
-   Recomendamos que el UCP se hospede en una instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]que distinga entre mayúsculas y minúsculas.  
  
 Considere las siguientes recomendaciones para programar la capacidad en el equipo del UCP:  
  
-   En un escenario típico, el espacio en disco que utiliza la base de datos UMDW (sysutility_mdw) en el UCP es de aproximadamente 2 GB por cada instancia administrada de SQL Server y por año. Este cálculo puede variar en función del número de bases de datos y objetos de sistema que haya recopilado la instancia administrada. La frecuencia de crecimiento del espacio en disco de UMDW (sysutility_mdw) alcanza su índice máximo en los dos primeros días.  
  
-   En una situación de ejemplo típica, el espacio en disco que utiliza msdb en el UCP es de aproximadamente 20 MB por instancia administrada de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Observe que esta estimación puede variar, dependiendo de las directivas de utilización de recursos y del número de bases de datos y objetos de sistema que recopile la instancia administrada. En general, el uso del espacio en disco aumenta según va aumentando la cantidad de infracciones de directivas y la duración de la ventana de tiempo móvil para los recursos volátiles.  
  
-   Observe que al quitar una instancia administrada del UCP, no se reducirá el espacio en disco que utilizan las bases de datos del UCP hasta que expiren los periodos de retención correspondientes a la instancia administrada.  
  
 En esta versión, todas las instancias administradas de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] deben satisfacer los siguientes requisitos:  
  
-   Recomendamos que en caso de que el UCP se encuentre hospedado en una instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]que no distinga entre mayúsculas y minúsculas, las instancias administradas de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tampoco distingan entre mayúsculas y minúsculas.  
  
-   Los datos FILESTREAM no se admiten para la supervisión de la utilidad de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
 Para obtener más información, vea [Especificaciones de capacidad máxima para SQL Server](../../sql-server/maximum-capacity-specifications-for-sql-server.md) y [Características compatibles con las ediciones de SQL Server 2016](~/sql-server/editions-and-supported-features-for-sql-server-2016.md).  
  
### <a name="remove-previous-utility-control-points-before-installing-a-new-one"></a>Quitar los puntos de control anteriores de la utilidad antes de instalar uno nuevo  
 Si trata de instalar un punto de control de utilidad (UCP) en una instancia de SQL Server que se configuró en algún momento como UCP, debe quitar todas las instancias administradas de SQL Server y el UCP antes de proceder a la instalación. Para ello, debe ejecutar el procedimiento almacenado **sp_sysutility_ucp_remove** .  
  
 Antes de ejecutar el procedimiento, tenga en cuenta los siguientes requisitos:  
  
-   Este procedimiento se tiene que ejecutar en un equipo que sea un UCP.  
  
-   Para ejecutar este procedimiento, el usuario debe tener los permisos sysadmin, los mismos que se necesitan para crear un UCP.  
  
-   Todas las instancias administradas de SQL Server se deben quitar del UCP. Tenga en cuenta que el UCP es una instancia administrada de SQL Server. Para más información, vea: [Cómo: quitar una instancia de SQL Server de la utilidad de SQL Server](https://go.microsoft.com/fwlink/?LinkId=169392).  
  
 Use este procedimiento para quitar una UCP de SQL Server de la utilidad de SQL Server. Cuando haya terminado la operación, se puede volver a crear un UCP en la instancia de SQL Server.  
  
 Use SQL Server Management Studio para conectarse al UCP y, a continuación, ejecute este script:  
  
```  
EXEC msdb.dbo.sp_sysutility_ucp_remove;  
```  
  
> [!NOTE]  
>  Si la instancia de SQL Server de la que se quitó el UCP tiene un conjunto de recopilación de datos que no es de utilidad, el procedimiento no quita la base de datos sysutility_mdw. En tal caso, la base de datos sysutility_mdw se debe quitar manualmente para poder volver a crear el UCP.  
  
 Cada instancia administrada de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] y todos los componentes de la aplicación de capa de datos pertenecen únicamente a una utilidad de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] y los administra un solo UCP. Para obtener más información sobre conceptos de la utilidad de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , vea [Características y tareas de la utilidad de SQL Server](../../relational-databases/manage/sql-server-utility-features-and-tasks.md).  
  
 Un UCP es el punto de razonamiento central de la utilidad de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Con el UCP, puede ver la información de configuración y rendimiento que se ha recopilado en las instancias administradas de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] y en las aplicaciones de capa de datos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , además de realizar actividades generales de diseño de la capacidad. El UCP es el punto de inicio para inscribirse y quitar instancias de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] de la utilidad de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
 Después de inscribir instancias de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] en la utilidad [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , puede supervisar el estado de recursos para las instancias administradas de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] y aplicaciones de nivel de datos para identificar las oportunidades de consolidación y aislar los cuellos de botella de recursos. Para obtener más información, vea [Supervisar instancias de SQL Server en la utilidad de SQL Server](../../relational-databases/manage/monitor-instances-of-sql-server-in-the-sql-server-utility.md).  
  
> [!IMPORTANT]  
>  El conjunto de recopilación de la utilidad de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] se admite en paralelo con conjuntos de recopilación que no sean de la utilidad de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Es decir, otros conjuntos de recopilación pueden supervisar una instancia administrada de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] mientras pertenezca a una utilidad de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Sin embargo, debe tener en cuenta que todos los conjuntos de recopilación en la instancia administrada cargarán sus datos en el almacén de administración de datos de la utilidad de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Para obtener más información, vea [Consideraciones para ejecutar conjuntos de recopilación de la utilidad y que no sean de la utilidad en la misma instancia de SQL Server](../../relational-databases/manage/run-utility-and-non-utility-collection-sets-on-same-sql-instance.md) y [Configurar el almacenamiento de datos del punto de control de la utilidad &#40;Utilidad de SQL Server&#41;](../../relational-databases/manage/configure-your-utility-control-point-data-warehouse-sql-server-utility.md).  
  
## <a name="wizard-steps"></a>Pasos del asistente  
 ![Crear UCP](../../relational-databases/manage/media/create-ucp.gif "Create_UCP")  
  
 En las siguientes secciones se proporciona información sobre cada página del flujo de trabajo del asistente para crear un UCP nuevo de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Para iniciar el asistente para crear un nuevo UCP, abra el panel Explorador de la utilidad en el menú Vista de SSMS, luego haga clic en el botón ![Crear UCP](../../relational-databases/manage/media/create-ucp.gif "Create_UCP") **Crear UCP** en la parte superior del panel Explorador de la utilidad.  
  
 Haga clic en un vínculo en la lista siguiente para navegar a los detalles de una página del asistente:  
  
 Para obtener más información sobre un script de PowerShell de esta operación, vea el [ejemplo](#PowerShell_create_UCP).  
  
-   [Introducción al Asistente para crear UCP](#Welcome)  
  
-   [Especificar la instancia](#Instance_name)  
  
-   [Cuadro de diálogo de conexión](#Connection_dialog)  
  
-   [Conjunto de recopilación de datos Información de la utilidad](#Agent_configuration)  
  
-   [Reglas de validación](#Validation_rules)  
  
-   [Resumen](#Summary)  
  
-   [Crear el punto de control de utilidad](#Creating_UCP)  
  
##  <a name="introduction-to-create-ucp-wizard"></a><a name="Welcome"></a> Introducción al Asistente para crear UCP  
 Si abre el explorador de la utilidad y no existe ningún punto de control de utilidad, es preciso que se conecte a uno o que cree uno nuevo.  
  
 **Conectarse a UCP existente**: si ya existe un punto de control de la utilidad en la implementación, puede conectarse a él si hace clic en el botón ![Conectar con la utilidad](../../relational-databases/manage/media/connect-to-utility.gif "Connect_to_Utility")**Conectar con la utilidad** en la parte superior del panel Explorador de la utilidad. Para conectarse a un UCP existente, es preciso disponer de credenciales de administrador o ser un miembro del rol Lector de utilidad. Observe que puede haber solo un UCP por utilidad [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] y solo se puede estar conectado a un UCP de una instancia de SSMS.  
  
 **Crear nuevo UCP**: para crear un punto de control de la utilidad nuevo, haga clic en el botón ![Crear UCP](../../relational-databases/manage/media/create-ucp.gif "Create_UCP")**Crear UCP** en la parte superior del panel Explorador de la utilidad. Para crear un UCP nuevo, debe especificar el nombre de instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] y facilitar las credenciales de administrador en el cuadro de diálogo de conexión. Observe que solo puede haber un UCP por utilidad de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
##  <a name="specify-instance"></a><a name="Instance_name"></a> Especificar la instancia  
 Especifique la siguiente información sobre el UCP que está creando:  
  
-   **Nombre de la instancia**: para seleccionar una instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] en el cuadro de diálogo de conexión, haga clic en **Conectar...** . Proporcione el nombre del equipo y el nombre de la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] con el formato nombreDeEquipo\nombreDeInstancia.  
  
-   **Nombre de la utilidad** - Especifique un nombre que se utilizará para identificar la utilidad de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] en la red.  
  
 Para continuar, haga clic en **Siguiente**.  
  
##  <a name="connection-dialog"></a><a name="Connection_dialog"></a> Cuadro de diálogo de conexión  
 En el cuadro de diálogo Conectar al servidor, compruebe la información sobre el tipo de servidor, el nombre del equipo y el nombre de instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Para obtener más información, vea [Conectar al servidor &#40;motor de base de datos&#41;](https://msdn.microsoft.com/library/ee9017b4-8a19-4360-9003-9e6484082d41).  
  
> [!NOTE]  
>  Si la conexión está cifrada, se utilizará la conexión cifrada. Si la conexión no está cifrada, la utilidad de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] volverá a conectarse mediante una conexión cifrada.  
  
 Para continuar, haga clic en **Conectar...** .  
  
##  <a name="utility-collection-set-account"></a><a name="Agent_configuration"></a> Conjunto de recopilación de datos Información de la utilidad  
 Especifique una cuenta de dominio de Windows para ejecutar el conjunto de recopilación de la utilidad de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Esta cuenta se utiliza como la cuenta de proxy del Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para el conjunto de recopilación de la utilidad de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . De forma alternativa, puede utilizar la cuenta del servicio del Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] existente. Para pasar los requisitos de validación, utilice las siguientes instrucciones con el fin de especificar la cuenta.  
  
 Si especifica la opción de cuenta del servicio del Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] :  
  
-   La cuenta del servicio del Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] debe ser una cuenta de dominio de Windows que no sea una cuenta integrada como LocalSystem, NetworkService o LocalService.  
  
 Para continuar, haga clic en **Siguiente**.  
  
##  <a name="validation-rules"></a><a name="Validation_rules"></a> Reglas de validación  
 En esta versión de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], se deben dar las siguientes condiciones en la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] donde se creará el UCP:  
  
|Regla de validación|Acción correctiva|  
|---------------------|-----------------------|  
|Debe contar con privilegios de administrador en la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] donde se creará el punto de control de utilidad.|Inicie sesión con una cuenta que disponga de privilegios de administrador en la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
|La versión de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] debe ser 10.50 o posterior.|Especifique una instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] diferente para hospedar el UCP.|  
|La instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] debe ser una edición admitida. Para obtener una lista de las características admitidas por las ediciones de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], vea [Características compatibles con las ediciones de SQL Server 2016](~/sql-server/editions-and-supported-features-for-sql-server-2016.md).|Especifique una instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] diferente para hospedar el UCP.|  
|La instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] no debe ser una instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] inscrita con cualquier otro UCP de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .|Especifique otra instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para hospedar el UCP o anule la inscripción de la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] del UCP en el que es actualmente una instancia administrada de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
|La instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] no puede estar ya hospeda en un punto de control de utilidad.|Especifique una instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] diferente para hospedar el UCP.|  
|La instancia especificada de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] debe tener TCP/IP habilitado.|Habilite TCP/IP para la instancia especificada de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
|La instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] no puede tener una base de datos denominada "sysutility_mdw".|La operación para crear un UCP generará un almacén de administración de datos de la utilidad (UMDW) denominado "sysutility_mdw". En esta operación es preciso que el nombre no exista en el equipo en el momento de ejecutar las reglas de validación. Para continuar, debe quitar o cambiar el nombre de cualquier base de datos denominada "sysutility_mdw." Para obtener más información sobre estas operaciones para cambiar el nombre, vea [ALTER DATABASE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql.md).|  
|Los conjuntos de recopilación de la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] especificada deben detenerse.|Detenga los conjuntos de recopilación que ya existen mientras el UCP se crea en la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]especificada. Si se deshabilita el recopilador de datos, habilítelo, detenga cualquier conjunto de recopilación en ejecución y, a continuación, vuelva a ejecutar las reglas de validación para la operación Crear UCP.<br /><br /> Para habilitar el recopilador de datos:<br /><br /> En el Explorador de objetos, expanda el nodo **Administración** .<br /><br /> Haga clic con el botón derecho en **Recopilación de datos**y, luego, haga clic en **Habilitar recopilación de datos**.<br /><br /> Para detener un conjunto de recopilación:<br /><br /> En el Explorador de objetos, expanda el nodo Administración, expanda **Recopilación de datos**y, después, **Conjuntos de recopilación de datos del sistema**.<br /><br /> Haga clic con el botón derecho en el conjunto de recopilación que quiere detener y, luego, haga clic en **Detener conjunto de recopilación de datos**.<br /><br /> Un cuadro de mensaje muestra los resultados de esta acción y un círculo rojo en el icono para el conjunto de recopilación indica que el conjunto de recopilación se ha detenido.|  
|Se debe iniciar el servicio Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] en la instancia especificada. Si la instancia especificada de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] es una instancia en clúster de conmutación por error de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , el servicio Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] debe estar configurado de forma que se inicie manualmente. En caso contrario, el servicio Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] debe estar configurado para iniciarse automáticamente.|Inicie el servicio Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Si la instancia especificada de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] es una instancia en clúster de conmutación por error de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , configure el servicio Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] de forma que se tenga que iniciar manualmente. En caso contrario, configure el servicio Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para que se inicie automáticamente.|  
|WMI debe estar configurado correctamente.|Para solucionar problemas de configuración de WMI, vea [Solucionar problemas de la Utilidad de SQL Server](https://msdn.microsoft.com/library/f5f47c2a-38ea-40f8-9767-9bc138d14453).|  
|La cuenta de proxy del Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] no puede ser ninguna cuenta integrada, como Servicio de red.|Si la cuenta de proxy del Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] es una cuenta integrada, como Servicio de red, vuelva a asignar la cuenta a una cuenta de dominio de Windows que sea sysadmin.|  
|Si selecciona la opción de cuenta de proxy, la cuenta de proxy del Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] debe ser una cuenta de dominio de Windows válida.|Especifique una cuenta de dominio de Windows válida. Para asegurarse de que la cuenta es válida, inicie sesión en la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] especificada mediante la cuenta de dominio de Windows.|  
|Si selecciona la opción de cuenta del servicio, la cuenta del servicio del Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] no podrá ser una cuenta integrada.|Si la cuenta del servicio del Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] es una cuenta integrada, como Servicio de red, vuelva a asignar la cuenta a una cuenta de dominio de Windows.|  
|Si selecciona la opción de cuenta del servicio, la cuenta del servicio del Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] debe ser una cuenta de dominio de Windows válida.|Especifique una cuenta de dominio de Windows válida. Para asegurarse de que la cuenta es válida, inicie sesión en la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] especificada mediante la cuenta de dominio de Windows.|  
  
 Si en los resultados de validación se producen errores respecto a las condiciones, corrija los problemas de bloqueo y, a continuación, haga clic en **Volver a ejecutar validación** para comprobar la configuración del equipo.  
  
 Para guardar el informe de la validación, haga clic en **Guardar informe** y después especifique una ubicación para el archivo.  
  
 Para continuar, haga clic en **Siguiente**.  
  
##  <a name="summary"></a><a name="Summary"></a> Resumen  
 La página del resumen muestra la información que facilitó sobre el UCP:  
  
-   El nombre de instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que hospeda el UCP.  
  
-   El nombre de la utilidad de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
-   El nombre de la cuenta que se utilizará para ejecutar trabajos para la recopilación de datos de la utilidad de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
 Para cambiar la configuración del UCP, haga clic en **Anterior**. Para continuar, haga clic en **Siguiente**.  
  
##  <a name="creating-the-utility-control-point"></a><a name="Creating_UCP"></a> Crear el punto de control de utilidad  
 Durante la operación para crear el UCP, el asistente mostrará los pasos y facilitará el estado:  
  
-   Preparación de la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para la creación del UCP.  
  
-   Creación del almacén de administración de datos de la utilidad (UMDW).  
  
-   Inicialización del almacén de administración de datos de la utilidad de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ; el nombre del archivo de dicho almacén es sysutility_mdw.  
  
-   Configuración del UCP.  
  
-   Configuración del conjunto de recopilación de la utilidad de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
 Para guardar un informe sobre la operación de creación del UCP, haga clic en **Guardar informe** y después especifique una ubicación para el archivo.  
  
 Para finalizar el asistente, haga clic en **Finalizar**.  
  
 Tras completar el Asistente para crear UCP, el panel de navegación del explorador de la utilidad en SSMS muestra un nodo para el UCP con los nodos subordinados para las aplicaciones de capa de datos, instancias administradas y administración de utilidades. El UCP pasa a ser automáticamente una instancia administrada.  
  
 El proceso de recopilación de datos comienza inmediatamente, pero puede que sea necesario que transcurran hasta 30 minutos para que aparezcan por primera vez en el panel y puntos de vista del panel de contenido del explorador de la utilidad. La recopilación de datos se inicia cada 15 minutos. Los datos iniciales se obtendrán del propio UCP. Es decir, el UCP es la primera instancia administrada de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] en la utilidad de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
 Para mostrar el panel, haga clic en **Ver** y, a continuación, seleccione **Contenido del explorador de la utilidad** en el menú de SSMS. Para actualizar los datos, haga clic con el botón derecho en el nombre de la utilidad en el panel Explorador de la utilidad y luego seleccione **Actualizar**.  
  
 Para obtener más información sobre cómo inscribir instancias adicionales de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] a la Utilidad de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], vea [Inscribir una instancia de SQL Server &#40;Utilidad de SQL Server&#41;](../../relational-databases/manage/enroll-an-instance-of-sql-server-sql-server-utility.md). Para quitar el UCP como instancia administrada de la utilidad de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , seleccione **Instancias administradas** en el panel **Explorador de la utilidad** con el fin de rellenar la vista de lista de instancias administradas, haga clic con el botón derecho del mouse en el nombre de instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] en la vista de lista de **Contenido del explorador de la utilidad** y luego seleccione **Convertir instancia en no administrada**.  
  
##  <a name="create-a-new-utility-control-point-using-powershell"></a><a name="PowerShell_create_UCP"></a> Crear un punto de control de utilidad nuevo con PowerShell  
 Sírvase del siguiente ejemplo para crear un punto de control de utilidad nuevo:  
  
```  
> $UtilityInstance = new-object -Type Microsoft.SqlServer.Management.Smo.Server "ComputerName\UCP-Name";  
> $SqlStoreConnection = new-object -Type Microsoft.SqlServer.Management.Sdk.Sfc.SqlStoreConnection $UtilityInstance.ConnectionContext.SqlConnectionObject;  
> $Utility = [Microsoft.SqlServer.Management.Utility.Utility]::CreateUtility("Utility", $SqlStoreConnection, "ProxyAccount", "ProxyAccountPassword");  
```  
  
## <a name="see-also"></a>Consulte también  
 [Características y tareas de la utilidad de SQL Server](../../relational-databases/manage/sql-server-utility-features-and-tasks.md)   
 [Solucionar problemas de la Utilidad de SQL Server](https://msdn.microsoft.com/library/f5f47c2a-38ea-40f8-9767-9bc138d14453)  
  
  
