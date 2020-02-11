---
title: Configurar Analysis Services para la delegación restringida de Kerberos | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: 6d751477-6bf1-48b4-8833-5a631bbe7650
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: cfceb6b2314f9e57d6d383312d9f9373f7df1621
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "67832922"
---
# <a name="configure-analysis-services-for-kerberos-constrained-delegation"></a>Configurar Analysis Services para la delegación restringida de Kerberos
  Al configurar Analysis Services para la autenticación Kerberos, lo más probable es que le interese conseguir uno de los resultados siguientes o ambos: hacer que Analysis Services suplante una identidad de usuario al consultar datos o hacer que Analysis Services delegue una identidad de usuario a un servicio de nivel inferior. Cada escenario necesita requisitos de configuración ligeramente diferentes. En ambos escenarios es necesario asegurarse de que la configuración se ha realizado correctamente.  
  
> [!TIP]  
>  **[!INCLUDE[msCoName](../../includes/msconame-md.md)] Administrador de configuración de Kerberos para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]** es una herramienta de diagnóstico que sirve para solucionar problemas de conectividad de Kerberos relacionados con [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Para obtener más información, vea [Administrador de configuración de Microsoft Kerberos para SQL Server](https://www.microsoft.com/download/details.aspx?id=39046).  
  
 Este tema contiene las siguientes secciones:  
  
-   [Permitir que Analysis Services suplante una identidad de usuario](#bkmk_impersonate)  
  
-   [Configurar Analysis Services para la delegación de confianza](#bkmk_delegate)  
  
-   [Prueba de la identidad suplantada o delegada](#bkmk_test)  
  
> [!NOTE]  
>  La delegación no es necesaria si la conexión con Analysis Services es un solo salto, o si la solución usa credenciales almacenadas proporcionadas por el Servicio de almacenamiento seguro de SharePoint o por Reporting Services. Si todas las conexiones son conexiones directas desde Excel a una base de datos de Analysis Services, o se basan en credenciales almacenadas, puede utilizar Kerberos (o NTLM) sin tener que configurar la delegación restringida.  
>   
>  La delegación restringida de Kerberos es necesaria si la identidad del usuario tiene que fluir en varias conexiones de equipo (lo que se conoce como "salto doble"). Cuando el acceso de datos de Analysis Services depende de la identidad de usuario y la solicitud de conexión procede de un servicio de delegación, use la lista de comprobación de la sección siguiente para asegurarse de que Analysis Services puede suplantar al autor de la llamada original. Para obtener más información sobre los flujos de autenticación de Analysis Services, vea [Autenticación y delegación de identidad de Microsoft BI](https://go.microsoft.com/fwlink/?LinkID=286576).  
>   
>  Por seguridad, Microsoft siempre recomienda la delegación restringida más que la no restringida. La delegación no restringida supone un riesgo de seguridad mayor, porque permite que la identidad del servicio suplante a otros usuarios en *cualquier* equipo, servicio o aplicación de nivel inferior (en oposición a los servicios explícitamente definidos mediante delegación restringida).  
  
##  <a name="bkmk_impersonate"></a>Permitir que Analysis Services suplante una identidad de usuario  
 Para permitir que los servicios de nivel superior como Reporting Services, IIS o SharePoint suplanten una identidad de usuario en Analysis Services, debe configurar la delegación restringida de Kerberos para dichos servicios. En este escenario, Analysis Services suplanta al usuario actual usando la identidad que proporciona el servicio de delegación, devolviendo resultados según la pertenencia a roles de esa identidad de usuario.  
  
|Tarea|Descripción|  
|----------|-----------------|  
|Paso 1: Comprobación de que las cuentas son adecuadas para la delegación|Asegúrese de que las cuentas empleadas para ejecutar los servicios tienen las propiedades correctas en Active Directory. Las cuentas de servicio de Active Directory no se deben marcar como cuentas confidenciales ni excluir específicamente de los escenarios de delegación. Para obtener más información, vea [Información acerca de las cuentas de usuario](https://go.microsoft.com/fwlink/?LinkId=235818).<br /><br /> ** \* Importante \* \* ** Por lo general, todas las cuentas y servidores deben pertenecer al mismo Active Directory dominio o a dominios de confianza del mismo bosque. Sin embargo, dado que Windows Server 2012 admite la delegación entre límites de dominio, podrá configurar la delegación limitada de Kerberos en un límite de dominio si el nivel funcional de este dominio es Windows Server 2012. O bien, puede configurar Analysis Services para tener acceso HTTP y usar métodos de autenticación de IIS en la conexión de cliente. Para obtener más información, vea [Configurar el acceso HTTP a Analysis Services en Internet Information Services &#40;IIS&#41; 8.0](configure-http-access-to-analysis-services-on-iis-8-0.md).|  
|Paso 2: Registro del SPN|Antes de configurar una delegación, es preciso que registre un nombre principal de servicio (SPN) para la instancia de Analysis Services. Necesitará configurar el SPN de Analysis Services en el momento que configure la delegación restringida de Kerberos para servicios de nivel intermedio. Para obtener instrucciones, vea [SPN registration for an Analysis Services instance](spn-registration-for-an-analysis-services-instance.md) .<br /><br /> Un nombre principal del servicio (SPN) especifica la identidad única de un servicio en un dominio configurado para la autenticación Kerberos. Las conexiones de cliente que usan seguridad integrada suelen solicitar un SPN como parte de la autenticación SSPI. La solicitud se reenvía a un controlador de dominio (DC) de Active Directory y el KDC concede un vale si el SPN presentado por el cliente tiene un registro SPN coincidente en Active Directory.|  
|Paso 3: Configuración de la delegación restringida|Tras validar las cuentas que desea usar y registrar los SPN para esas cuentas, el siguiente paso es configurar los servicios de nivel superior, como IIS, Reporting Services o servicios Web de SharePoint para la delegación restringida, para lo cual, hay que especificar el SPN de Analysis Services como el servicio específico para el que se permite la delegación.<br /><br /> Los servicios que se ejecutan en SharePoint, como Excel Services o Reporting Services en modo de SharePoint, suelen hospedar libros e informes que usan datos multidimensionales o tabulares de Analysis Services. La configuración de la delegación restringida para estos servicios es una tarea de configuración frecuente y es necesaria para admitir la actualización de datos desde Excel Services. Los vínculos siguientes proporcionan instrucciones para los servicios de SharePoint así como otros que es probable que presenten una conexión de flujo de datos de nivel inferior para los datos de Analysis Services:<br /><br /> [Delegación de identidad para servicios de Excel (SharePoint server 2010)](https://go.microsoft.com/fwlink/?LinkId=299826) o [Cómo configurar Excel Services en SharePoint Server 2010 para la autenticación Kerberos](https://support.microsoft.com/kb/2466519)<br /><br /> [Delegación de identidad para PerformancePoint Services (SharePoint Server 2010)](https://go.microsoft.com/fwlink/?LinkId=299827)<br /><br /> [Delegación de identidad para SQL Server Reporting Services (SharePoint Server 2010)](https://go.microsoft.com/fwlink/?LinkId=299828)<br /><br /> Para IIS 7.0, vea [Configurar la autenticación de Windows (IIS 7.0)](https://technet.microsoft.com/library/cc754628\(v=ws.10\).aspx) o [Cómo configurar SQL Server 2008 Analysis Services y SQL Server 2005 Analysis Services para utilizar autenticación Kerberos](https://support.microsoft.com/kb/917409).|  
|Paso 4: Prueba de conexiones|Cuando lo pruebe, conéctese desde equipos remotos, con distintas identidades y haga consultas a Analysis Services con las mismas aplicaciones como usuario empresarial. Puede servirse de SQL Server Profiler para supervisar la conexión. En la solicitud, se debe ver la identidad del usuario. Para obtener más información, vea [Probar la identidad suplantada o delegada](#bkmk_test) en esta sección.|  
  
##  <a name="bkmk_delegate"></a>Configurar Analysis Services para la delegación de confianza  
 La configuración de Analysis Services para delegación restringida de Kerberos permite al servicio suplantar una identidad de cliente en un servicio de nivel inferior, como el motor de base de datos relacional, para poder consultar datos como si el cliente se conectara directamente.  
  
 Los escenarios de delegación para Analysis Services están limitados a los modelos tabulares configurados para el modo `DirectQuery`. Este es el único escenario en el que Analysis Services puede pasar credenciales delegadas a otro servicio. En el resto de situaciones, como en las situaciones de SharePoint mencionadas en la sección anterior, Analysis Services está en el lado receptor de la cadena de delegación. Para obtener más información sobre DirectQuery, vea [Modo DirectQuery &#40;SSAS tabular&#41;](../tabular-models/directquery-mode-ssas-tabular.md).  
  
> [!NOTE]  
>  Una idea equivocada habitual es que el almacenamiento ROLAP, las operaciones de procesamiento o el acceso a particiones remotas de alguna manera añaden requisitos para la delegación restringida. Esto no es así. Todas estas operaciones las ejecuta directamente la cuenta de servicio (también llamada cuenta de procesamiento) en su propio nombre. No se requiere delegación para estas operaciones en Analysis Services, ya que los permisos para estas operaciones se otorgan directamente a la cuenta de servicio (por ejemplo, otorgar permisos db_datareader en la base de datos relacional para que el servicio pueda procesar los datos). Para obtener más información sobre las operaciones del servidor y los permisos, vea [Configurar las cuentas de servicio &#40;Analysis Services&#41;](configure-service-accounts-analysis-services.md).  
  
 En esta sección se explica cómo configurar Analysis Services para la delegación de confianza. Después de completar esta tarea, Analysis Services podrá pasar credenciales delegadas a SQL Server, en apoyo al modo DirectQuery usado en las soluciones tabulares.  
  
 Antes de comenzar:  
  
-   Compruebe que Analysis Services se ha iniciado.  
  
-   Compruebe que el SPN para Analysis Services es válido. Para obtener instrucciones, vea [SPN registration for an Analysis Services instance](spn-registration-for-an-analysis-services-instance.md).  
  
 Cuando se cumplan ambos requisitos previos, continúe con los pasos siguientes. Tenga en cuenta que debe ser administrador de dominio para poder configurar la delegación restringida.  
  
1.  En Usuarios y equipos de Active Directory, busque la cuenta de servicio bajo la que se ejecuta Analysis Services. Haga clic con el botón derecho en la cuenta de servicio y elija **Propiedades**.  
  
     Con fines ilustrativos, las capturas de pantalla siguientes usan OlapSvc y SQLSvc para representar Analysis Services y SQL Server, respectivamente.  
  
     OlapSvc es la cuenta que se configurará para la delegación restringida en SQLSvc. Al completar esta tarea, OlapSvc tendrá permiso para pasar credenciales delegadas en un vale de servicio a SQLSvc, suplantando al autor de la llamada original cuando se soliciten datos.  
  
2.  En la pestaña Delegación, seleccione **Confiar en este usuario para la delegación solo a los servicios especificados**y, después, seleccione **Usar solamente Kerberos**. Haga clic en **Agregar** para especificar el servicio para el que Analysis Services tiene permiso para delegar credenciales.  
  
     La pestaña Delegación solo aparece cuando la cuenta de usuario (OlapSvc) está asignada a un servicio (Analysis Services) y el servicio tiene un SPN registrado para él. El registro de SPN necesita que el servicio esté en ejecución.  
  
     ![SSAS_Kerberos_1_AccountProperties](../media/ssas-kerberos-1-accountproperties.gif "SSAS_Kerberos_1_AccountProperties")  
  
3.  En la página Agregar servicios, haga clic en **Usuarios o equipos**.  
  
     ![SSAS_Kerberos_2_](../media/ssas-kerberos-2.gif "SSAS_Kerberos_2_")  
  
4.  En la página Seleccionar usuarios o equipos, escriba la cuenta usada para ejecutar la instancia de SQL Server que proporciona datos a bases de datos de modelos tabulares de Analysis Services. Haga clic en **Aceptar** para aceptar la cuenta de servicio.  
  
     Si no puede seleccionar la cuenta que desea, compruebe que SQL Server está en ejecución y tiene un SPN registrado para esta cuenta. Para obtener más información acerca de los SPN para el motor de base de datos, vea [Registrar un nombre principal de servicio para las conexiones con Kerberos](../../database-engine/configure-windows/register-a-service-principal-name-for-kerberos-connections.md).  
  
     ![SSAS_Kerberos_3_SelectUsers](../media/ssas-kerberos-3-selectusers.gif "SSAS_Kerberos_3_SelectUsers")  
  
5.  La instancia de SQL Server debe aparecer ahora en Agregar servicios. En la lista también aparecerán todos los servicios que usan también esa cuenta. Elija la instancia de SQL Server que desee usar. Haga clic en **Aceptar** para aceptar la instancia.  
  
     ![SSAS_Kerberos_4_](../media/ssas-kerberos-4.gif "SSAS_Kerberos_4_")  
  
6.  La página de propiedades del servicio Analysis Services debe ser similar ahora a la captura de pantalla siguiente. Haga clic en **Aceptar** para guardar los cambios.  
  
     ![SSAS_Kerberos_5_Finished](../media/ssas-kerberos-5-finished.gif "SSAS_Kerberos_5_Finished")  
  
7.  Pruebe si la delegación se ha realizado correctamente conectándose desde un equipo cliente remoto, con una identidad diferente, y consulte el modelo tabular. Debe ver la identidad de usuario de la solicitud en SQL Server Profiler.  
  
##  <a name="bkmk_test"></a>Prueba de la identidad suplantada o delegada  
 Use SQL Server Profiler para supervisar la identidad del usuario que está consultando datos.  
  
1.  Inicie **SQL Server Profiler** en la instancia de Analysis Services e inicie después un nuevo seguimiento.  
  
2.  En Selección de eventos, compruebe que `Audit Login` y `Audit Logout` están activadas en la sección Auditoría de seguridad.  
  
3.  Conéctese a Analysis Services a través de un servicio de aplicación (como SharePoint o Reporting Services) desde un equipo cliente remoto. El evento Audit Login mostrará la identidad del usuario que se conecta a Analysis Services.  
  
 Para realizar una prueba completa será necesario usar herramientas de supervisión de red que puedan capturar las solicitudes y respuestas de Kerberos en la red. Para esta tarea se puede emplear la utilidad Monitor de red (netmon.exe), filtrada para Kerberos. Para obtener más información sobre cómo usar Netmon 3.4 y otras herramientas para probar la autenticación de Kerberos, vea [Configuración de la autenticación Kerberos: Configuración principal (SharePoint Server 2010)](https://technet.microsoft.com/library/gg502602\(v=office.14\).aspx).  
  
 Vea también [El cuadro de diálogo más confuso de Active Directory](https://www.itprotoday.com/active-directory/most-confusing-dialog-box-active-directory) para obtener una descripción detallada de cada opción de la pestaña Delegación del cuadro de diálogo de la propiedad del objeto Active Directory. Este artículo también explica cómo utilizar el LDP para comprobar e interpretar los resultados de la prueba.  
  
## <a name="see-also"></a>Consulte también  
 [Autenticación y delegación de identidad de Microsoft BI](https://go.microsoft.com/fwlink/?LinkID=286576)   
 [Autenticación mutua con Kerberos](https://go.microsoft.com/fwlink/?LinkId=299283)   
 [Conectarse a Analysis Services](connect-to-analysis-services.md)   
 [Registro de SPN para una instancia de Analysis Services](spn-registration-for-an-analysis-services-instance.md)   
 [Propiedades de la cadena de conexión &#40;Analysis Services&#41;](connection-string-properties-analysis-services.md)  
  
  
