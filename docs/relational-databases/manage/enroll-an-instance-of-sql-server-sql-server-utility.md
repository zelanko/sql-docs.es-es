---
title: Inscribir una instancia de SQL Server (Utilidad de SQL Server) | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.SWB.makemanaged.agentaccount.F1
- sql13.SWB.makemanaged.welcome.F1
- sql13.SWB.makemanaged.enrolling.F1
- sql13.SWB.makemanaged.instancename.F1
- sql13.SWB.makemanaged.Summary.F1
- sql13.SWB.makemanaged.progress.F1
- sql13.SWB.makemanaged.validation.F1
helpviewer_keywords:
- Enroll instance
ms.assetid: a801c619-611b-4e82-a8d8-d1e01691b7a1
caps.latest.revision: 13
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.translationtype: HT
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: c5bb6279f7fd96f30aa3f19628e2edc5edb5cc53
ms.contentlocale: es-es
ms.lasthandoff: 08/03/2017

---
# <a name="enroll-an-instance-of-sql-server-sql-server-utility"></a>Inscribir una instancia de SQL Server (Utilidad de SQL Server)
  Inscriba una instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] en una Utilidad [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] existente para supervisar su rendimiento y configuración como una instancia administrada de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. El punto de control de la utilidad (UCP) recopila información de configuración y rendimiento de las instancias administradas de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] cada 15 minutos. Esta información se almacena en el almacén de administración de datos de la utilidad (UMDW) en el UCP; el nombre del archivo UMDW es sysutility_mdw. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] se comparan con directivas para ayudar a identificar cuellos de botella en el uso de recursos y oportunidades de consolidación.  
  
 En esta versión, el UCP y todas las instancias administradas de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] deben satisfacer los requisitos siguientes:  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] debe ser de la versión 10.50 o posterior.  
  
-   El tipo de instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] debe ser [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
-   La utilidad de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] debe funcionar en un dominio de Windows único, o bien en dominios con relaciones bidireccionales de confianza.  
  
-   Las cuentas de servicio de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] en el UCP y todas las instancias administradas de SQL Server deben disponer de permisos de lectura para los usuarios de Active Directory.  
  
-   La instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para inscribir no puede ser SQL Azure.  
  
 En esta versión, el UCP debe satisfacer los siguientes requisitos:  
  
-   La instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] debe ser una edición admitida. Para obtener una lista de las características admitidas por las ediciones de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], vea [Características compatibles con las ediciones de SQL Server 2016](~/sql-server/editions-and-supported-features-for-sql-server-2016.md).  
  
-   Recomendamos que el UCP esté hospedado en una instancia con distinción entre mayúsculas y minúsculas de SQL Server.  
  
-   Considere las siguientes recomendaciones para programar la capacidad en el equipo del UCP:  
  
    -   En un escenario típico, el espacio en disco que utiliza la base de datos UMDW (sysutility_mdw) en el UCP es de aproximadamente 2 GB por cada instancia administrada de SQL Server y por año. Este cálculo puede variar en función del número de bases de datos y objetos de sistema que haya recopilado la instancia administrada. La frecuencia de crecimiento del espacio en disco de UMDW (sysutility_mdw) alcanza su índice máximo en los dos primeros días.  
  
    -   En una situación de ejemplo típica, el espacio en disco que utiliza msdb en el UCP es de aproximadamente 20 MB por instancia administrada de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Observe que esta estimación puede variar, dependiendo de las directivas de utilización de recursos y del número de bases de datos y objetos de sistema que recopile la instancia administrada. En general, el uso del espacio en disco aumenta según va aumentando la cantidad de infracciones de directivas y la duración de la ventana de tiempo móvil para los recursos volátiles.  
  
    -   Observe que al quitar una instancia administrada del UCP, no se reducirá el espacio en disco que utilizan las bases de datos del UCP hasta que expiren los periodos de retención correspondientes a la instancia administrada.  
  
 En esta versión, todas las instancias administradas de SQL Server deben satisfacer los siguientes requisitos:  
  
-   Recomendamos que en caso de que el UCP se encuentre hospedado en una instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]que no distinga entre mayúsculas y minúsculas, las instancias administradas de SQL Server tampoco distingan entre mayúsculas y minúsculas.  
  
-   Los datos FILESTREAM no se admiten para la supervisión de la utilidad de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
 Para obtener más información, vea [Especificaciones de capacidad máxima para SQL Server](../../sql-server/maximum-capacity-specifications-for-sql-server.md) y [Características compatibles con las ediciones de SQL Server 2016](~/sql-server/editions-and-supported-features-for-sql-server-2016.md).  
  
 Para obtener más información sobre conceptos de la utilidad de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , vea [Características y tareas de la utilidad de SQL Server](../../relational-databases/manage/sql-server-utility-features-and-tasks.md).  
  
> [!IMPORTANT]  
>  El conjunto de recopilación de la utilidad de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] se admite en paralelo con conjuntos de recopilación que no sean de la utilidad de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Es decir, otros conjuntos de recopilación pueden supervisar una instancia administrada de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] mientras pertenezca a una utilidad de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Sin embargo, debe tener en cuenta que todos los conjuntos de recopilación de la instancia administrada cargarán sus datos en el almacén de administración de datos de la utilidad. Para obtener más información, vea [Consideraciones para ejecutar conjuntos de recopilación de la utilidad y que no sean de la utilidad en la misma instancia de SQL Server](../../relational-databases/manage/run-utility-and-non-utility-collection-sets-on-same-sql-instance.md) y [Configurar el almacenamiento de datos del punto de control de la utilidad &#40;Utilidad de SQL Server&#41;](../../relational-databases/manage/configure-your-utility-control-point-data-warehouse-sql-server-utility.md).  
  
## <a name="wizard-steps"></a>Pasos del asistente  
 En las siguientes secciones se proporciona información detallada sobre cada página del flujo de trabajo del asistente. Haga clic en un vínculo para navegar a los detalles de una página del asistente. Para obtener más información sobre un script de PowerShell de esta operación, vea el [ejemplo](#PowerShell_enroll)de PowerShell.  
  
-   [Introducción al Asistente Inscribir instancia](#Welcome)  
  
-   [Especificar la instancia de SQL Server](#Instance_name)  
  
-   [Cuadro de diálogo de conexión](#Connection_dialog)  
  
-   [Conjunto de recopilación de datos Información de la utilidad](#Proxy_configuration)  
  
-   [Validación de instancia de SQL Server](#Validation_rules)  
  
-   [Resumen de la inscripción de instancia](#Summary)  
  
-   [Inscripción de la instancia de SQL Server](#Enrolling)  
  
##  <a name="Welcome"></a> Introducción al Asistente Inscribir instancia  
 Para iniciar el asistente, expanda el árbol explorador de la utilidad en un punto de control de la utilidad, haga clic con el botón derecho en **Instancias administradas**y seleccione **Agregar instancia administrada…**.  
  
 Para continuar, haga clic en **Siguiente**.  
  
##  <a name="Instance_name"></a> Especificar la instancia de SQL Server  
 Para seleccionar una instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] en el diálogo de conexión, haga clic en **Conectar…**. Proporcione el nombre del equipo y el nombre de la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] con el formato nombreDeEquipo\nombreDeInstancia. Para obtener más información, vea [Conectar al servidor &#40;motor de base de datos&#41;](http://msdn.microsoft.com/library/ee9017b4-8a19-4360-9003-9e6484082d41).  
  
 Para continuar, haga clic en **Siguiente**.  
  
##  <a name="Connection_dialog"></a> Cuadro de diálogo de conexión  
 En el cuadro de diálogo Conectar al servidor, compruebe la información sobre el tipo de servidor, el nombre del equipo y el nombre de instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Para obtener más información, vea [Conectar al servidor &#40;motor de base de datos&#41;](http://msdn.microsoft.com/library/ee9017b4-8a19-4360-9003-9e6484082d41).  
  
> [!NOTE]  
>  Si la conexión está cifrada, se usará la conexión cifrada. Si la conexión no está cifrada, la Utilidad [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] volverá a conectarse mediante una conexión cifrada.  
  
 Para continuar, haga clic en **Conectar...**.  
  
##  <a name="Proxy_configuration"></a> Conjunto de recopilación de datos Información de la utilidad  
 Especifique una cuenta de dominio de Windows para ejecutar el conjunto de recopilación de la utilidad de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Esta cuenta se utiliza como la cuenta de proxy del Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para el conjunto de recopilación de la utilidad de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . De forma alternativa, puede utilizar la cuenta del servicio del Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] existente. Para pasar los requisitos de validación, utilice las siguientes instrucciones con el fin de especificar la cuenta.  
  
 Si especifica la opción de cuenta del servicio del Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] :  
  
-   La cuenta del servicio del Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] debe ser una cuenta de dominio de Windows que no sea una cuenta integrada como LocalSystem, NetworkService o LocalService.  
  
 Para continuar, haga clic en **Siguiente**.  
  
##  <a name="Validation_rules"></a> Validación de instancia de SQL Server  
 En esta versión, deben cumplirse las siguientes condiciones en la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que se va a inscribir en la Utilidad [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] :  
  
|Condición|Acción correctora|  
|---------------|-----------------------|  
|Debe tener privilegios de administrador en la instancia especificada de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] y en el UCP.|Inicie sesión con una cuenta que tenga privilegios de administrador en la instancia especificada de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] y en el UCP.|  
|La edición [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] debe admitir la inscripción de la instancia.|Para obtener una lista de las características admitidas por las ediciones de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], vea [Características compatibles con las ediciones de SQL Server 2016](~/sql-server/editions-and-supported-features-for-sql-server-2016.md).|  
|El UCP de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] debe tener habilitado TCP/IP.|Habilite TCP/IP en el UCP de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .|  
|La instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ya no se puede inscribir con ningún otro UCP [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .|Si la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que especifica ya se administra como parte de una Utilidad [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] existente, no puede inscribirla con un UCP diferente.|  
|La instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] aún no puede ser un UCP.|Si la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que especifica ya es un UCP que es diferente del UCP que está conectado; no puede inscribirla en este UCP.|  
|La instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] debe tener conjuntos de recopilación de la Utilidad [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] instalados.|Reinstale la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
|Los conjuntos de recopilación de la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] especificada deben detenerse.|Detenga los conjuntos de recopilación ya existentes sobre la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]especificada. Si se deshabilita el recopilador de datos, habilítelo, detenga cualquier conjunto de recopilación en ejecución y, a continuación, vuelva a ejecutar las reglas de validación para la operación Crear UCP.<br /><br /> Para habilitar el recopilador de datos:<br /><br /> En el Explorador de objetos, expanda el nodo **Administración** .<br /><br /> Haga clic con el botón derecho en **Recopilación de datos**y, luego, haga clic en **Habilitar recopilación de datos**.<br /><br /> Para detener un conjunto de recopilación:<br /><br /> En el Explorador de objetos, expanda el nodo Administración, expanda **Recopilación de datos**y, después, **Conjuntos de recopilación de datos del sistema**.<br /><br /> Haga clic con el botón derecho en el conjunto de recopilación que quiere detener y, luego, haga clic en **Detener conjunto de recopilación de datos**.<br /><br /> Un cuadro de mensaje muestra los resultados de esta acción y un círculo rojo en el icono para el conjunto de recopilación indica que el conjunto de recopilación se ha detenido.|  
|Se debe iniciar el servicio Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] en la instancia especificada de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .|Inicie el servicio Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] en la instancia especificada de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Si la instancia especificada de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] es una instancia en clúster de conmutación por error de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , configure el servicio Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] de forma que se tenga que iniciar manualmente. En caso contrario, configure el servicio Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para que se inicie automáticamente.|  
|Se debe iniciar el servicio Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] en el UCP.|Inicie el servicio Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] en el UCP. Si el UCP de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] es una instancia de clúster de conmutación por error de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , configure el servicio Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] de forma que se tenga que iniciar manualmente. En caso contrario, configure el servicio Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para que se inicie automáticamente.|  
|WMI debe estar configurado correctamente.|Para solucionar problemas de configuración de WMI, vea [Solucionar problemas de la Utilidad de SQL Server](http://msdn.microsoft.com/library/f5f47c2a-38ea-40f8-9767-9bc138d14453).|  
|La cuenta de proxy del Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] debe ser una cuenta de dominio de Windows válida en el UCP.|Especifique una cuenta de dominio de Windows válida. Para asegurarse de que la cuenta es válida, inicie sesión en el UCP mediante la cuenta de dominio de Windows.|  
|Si selecciona la opción de cuenta de proxy, la cuenta de proxy del Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] debe ser una cuenta de dominio de Windows válida en la instancia especificada de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|Especifique una cuenta de dominio de Windows válida. Para asegurarse de que la cuenta es válida, inicie sesión en la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] especificada mediante la cuenta de dominio de Windows.|  
|La cuenta de servicio del Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] no puede ser ninguna cuenta integrada, como Servicio de red.|Reasigne la cuenta a una cuenta de dominio de Windows. Para asegurarse de que la cuenta es válida, inicie sesión en la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] especificada mediante la cuenta de dominio de Windows.|  
|La cuenta de servicio del Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] debe ser una cuenta de dominio de Windows válida en el UCP.|Especifique una cuenta de dominio de Windows válida. Para asegurarse de que la cuenta es válida, inicie sesión en el UCP mediante la cuenta de dominio de Windows.|  
|Si selecciona la opción de cuenta de servicio, la cuenta de servicio del Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] debe ser una cuenta de dominio de Windows válida en la instancia especificada de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|Especifique una cuenta de dominio de Windows válida. Para asegurarse de que la cuenta es válida, inicie sesión en la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] especificada mediante la cuenta de dominio de Windows.|  
  
 Si en los resultados de validación se producen errores respecto a las condiciones, corrija los problemas de bloqueo y, a continuación, haga clic en **Volver a ejecutar validación** para comprobar la configuración del equipo.  
  
 Para guardar el informe de la validación, haga clic en **Guardar informe** y después especifique una ubicación para el archivo.  
  
 Para continuar, haga clic en **Siguiente**.  
  
##  <a name="Summary"></a> Resumen de la inscripción de instancia  
 La página de resumen muestra información sobre la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que se va a agregar a la Utilidad [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
 Configuración de la instancia administrada:  
  
-   Nombre de instancia de SQL Server: NombreEquipo\NombreInstancia  
  
-   Cuenta del conjunto de recopilación de la utilidad: NombreDominio\NombreUsuario  
  
 Para continuar, haga clic en **Siguiente**.  
  
##  <a name="Enrolling"></a> Inscripción de la instancia de SQL Server  
 La página de inscripción proporciona el estado de la operación:  
  
-   Preparar la instancia para la inscripción.  
  
-   Crear el directorio de memoria caché para los datos recopilados.  
  
-   Configurar el conjunto de recopilación de la utilidad.  
  
 Para guardar un informe sobre la operación de inscripción, haga clic en **Guardar informe** y especifique una ubicación para el archivo.  
  
 Para completar el asistente, haga clic en **Finalizar**.  
  
> [!NOTE]  
>  Si utiliza Autenticación de SQL Server para conectar con la instancia de SQL Server para inscribirse, y especifica una cuenta de proxy que pertenece a un dominio de Active Directory que no es el dominio en el que está el UCP, la validación de la instancia será correcta, pero se produce un error en la operación de inscripción con un mensaje de error parecido a este:  
>   
>  Se ha producido una excepción al ejecutar una instrucción o lote Transact-SQL. (Microsoft.SqlServer.ConnectionInfo)  
>   
>  Información adicional: no se ha podido obtener información sobre el grupo o usuario '\<nombreDeDominio\nombreDeCuenta>' de Windows NT, código de error 0x5. (Microsoft SQL Server, Error: 15404)  
>   
>  Para obtener más información sobre cómo solucionar este error, vea [Solucionar problemas de la Utilidad de SQL Server](http://msdn.microsoft.com/library/f5f47c2a-38ea-40f8-9767-9bc138d14453).  
  
> [!IMPORTANT]  
>  No cambie las propiedades del conjunto de recopilación "Información de la utilidad" en una instancia administrada de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]y no active ni desactive manualmente la recopilación de datos, ya que la recopilación de datos la controla un trabajo del agente de la Utilidad.  
  
 Después de completar el asistente para inscribir instancia, haga clic en el nodo **Instancias administradas** en el panel **Navegación del Explorador de Utilidad** en SSMS. Las instancias inscritas de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] se muestran en la vista de lista en panel **Contenido del explorador de la utilidad** .  
  
 El proceso de recopilación de datos comienza inmediatamente, pero puede que sea necesario que transcurran hasta 30 minutos para que aparezcan por primera vez en el panel y puntos de vista del panel de contenido del explorador de la utilidad. La recopilación de datos se inicia una vez cada 15 minutos. Para actualizar los datos, haga clic con el botón derecho en el nodo **Instancias administradas** del panel **Navegación del explorador de la utilidad** ; después, seleccione **Actualizar**o haga clic con el botón derecho en el nombre de instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] en la vista de lista y seleccione **Actualizar**.  
  
 Para eliminar instancias administradas de la Utilidad [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , seleccione **Instancias administradas** en el panel **Navegación del Explorador de la utilidad** con el fin de rellenar la vista de lista de instancias administradas, haga clic con el botón derecho en el nombre de instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] en la vista de lista **Contenido del explorador de la utilidad** y, después, seleccione **Convertir instancia en no administrada**.  
  
##  <a name="PowerShell_enroll"></a> Inscribir una instancia de SQL Server usando PowerShell  
 Use el siguiente ejemplo para inscribir una instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] en una utilidad de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] existente:  
  
```  
> $UtilityInstance = new-object -Type Microsoft.SqlServer.Management.Smo.Server "ComputerName\UCP-Name";  
> $SqlStoreConnection = new-object -Type Microsoft.SqlServer.Management.Sdk.Sfc.SqlStoreConnection $UtilityInstance.ConnectionContext.SqlConnectionObject;  
> $Utility = [Microsoft.SqlServer.Management.Utility.Utility]::Connect($SqlStoreConnection);  
> $Instance = new-object -Type Microsoft.SqlServer.Management.Smo.Server "ComputerName\ManagedInstanceName";  
> $InstanceConnection = new-object -Type Microsoft.SqlServer.Management.Sdk.Sfc.SqlStoreConnection $Instance.ConnectionContext.SqlConnectionObject;  
> $ManagedInstance = $Utility.EnrollInstance($InstanceConnection, "ProxyAccount", "ProxyPassword");  
```  
  
## <a name="see-also"></a>Vea también  
 [Características y tareas de la utilidad de SQL Server](../../relational-databases/manage/sql-server-utility-features-and-tasks.md)   
 [Supervisar instancias de SQL Server en la utilidad de SQL Server](../../relational-databases/manage/monitor-instances-of-sql-server-in-the-sql-server-utility.md)   
 [Solucionar problemas de la Utilidad de SQL Server](http://msdn.microsoft.com/library/f5f47c2a-38ea-40f8-9767-9bc138d14453)  
  
  

