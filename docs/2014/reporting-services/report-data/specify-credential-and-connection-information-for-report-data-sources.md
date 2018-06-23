---
title: Especificar información de credenciales y conexión para los orígenes de datos de informes | Microsoft Docs
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- reporting-services-native
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- no credentials option [Reporting Services]
- impersonation [Reporting Services]
- user impersonation [Reporting Services]
- Windows authentication [Reporting Services]
- data sources [Reporting Services], security
- connection strings [Reporting Services]
- unattended report processing [Reporting Services]
- reports [Reporting Services], security
- remote data sources [Reporting Services]
- credentials [Reporting Services]
- authentication [Reporting Services]
- external data sources [Reporting Services]
- prompted credentials [Reporting Services]
- multiple connections
- stored credentials [Reporting Services]
- security [Reporting Services], data sources
- Windows integrated security [Reporting Services]
ms.assetid: fee1a663-a313-424a-aed2-5082bfd114b3
caps.latest.revision: 59
author: douglaslM
ms.author: douglasl
manager: mblythe
ms.openlocfilehash: 3e3dc577cf7b0db69fbcc8140996ce33a4802040
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36197894"
---
# <a name="specify-credential-and-connection-information-for-report-data-sources"></a>Especificar información de credenciales y conexión para los orígenes de datos de informes
  Un servidor de informes utiliza credenciales para conectarse a orígenes de datos externos que proporcionan contenido a informes o información de destinatarios a una suscripción controlada por datos. Puede especificar credenciales que utilicen la autenticación de Windows, la autenticación de la base de datos, la autenticación personalizada o que no utilicen autenticación. Al enviar una solicitud de conexión a través de la red, el servidor de informes suplantará una cuenta de usuario o una cuenta de ejecución desatendida. Para obtener más información acerca del contexto de seguridad en el que se realiza una solicitud de conexión, vea [Configuración de orígenes de datos y conexiones de red](#DataSourceConfigurationConnections) más adelante en este tema.  
  
> [!NOTE]  
>  Las credenciales también sirven para autenticar a usuarios que tengan acceso a un servidor de informes. La información acerca de la autenticación de usuarios en un servidor de informes se proporciona en otro tema.  
  
 La conexión a un origen de datos externo se define cuando se crea el informe. Una vez publicado éste, se puede administrar por separado. Puede especificar una cadena de conexión estática o una expresión que permita a los usuarios seleccionar un origen de datos de una lista dinámica. Para obtener más información sobre cómo especificar una cadena de conexión y tipo de origen de datos, vea [las conexiones de datos, orígenes de datos y cadenas de conexión en Reporting Services](../data-connections-data-sources-and-connection-strings-in-reporting-services.md).  
  
## <a name="using-remote-data-sources"></a>Usar orígenes de datos remotos  
 Si el informe recupera datos de un servidor de bases de datos remoto, compruebe lo siguiente:  
  
-   Las credenciales proporcionadas al servidor de bases de datos son válidas. Si está usando credenciales de usuario de Windows, asegúrese de que el usuario tiene permiso para el servidor y la base de datos.  
  
-   Los puertos usados por el servidor de bases de datos están abiertos. Si está teniendo acceso a las bases de datos relacionales de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] en equipos externos, o si la base de datos del servidor de informes se encuentra en una instancia [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] externa, debe abrir el puerto 1433 y 1434 del equipo externo. Asegúrese de reiniciar el servidor después de abrir los puertos. Para más información, vea [Configurar Firewall de Windows para el acceso al motor de base de datos](../../database-engine/configure-windows/configure-a-windows-firewall-for-database-engine-access.md).  
  
-   Las conexiones remotas deben estar habilitadas. Si está teniendo acceso a las bases de datos relacionales de SQL Server en equipos externos, puede usar la herramienta Administrador de configuración de SQL Server para comprobar que las conexiones remotas sobre TCP están habilitadas.  
  
## <a name="ways-to-specify-credentials-for-connecting-to-remote-data-sources"></a>Maneras de especificar las credenciales para conectarse a orígenes de datos remotos  
 Los orígenes de datos que proporcionan contenido para informes normalmente se hospedan en servidores remotos. Para recuperar datos para un informe, un servidor de informes debe conectarse a un servidor utilizando un conjunto de credenciales proporcionadas por adelantado u obtenidas en tiempo de ejecución. Cuando configure un origen de datos, puede especificar credenciales de las formas que se indican a continuación:  
  
-   Pedir las credenciales al usuario.  
  
-   Almacenar las credenciales.  
  
-   Usar la seguridad integrada de Windows.  
  
-   No usar credenciales.  
  
 El entorno de red determina los tipos de conexiones compatibles. Por ejemplo, si la versión 5 del protocolo Kerberos está habilitada, puede que sea capaz de usar las características de delegación y suplantación disponibles en la autenticación de Windows para permitir conexiones en varios servidores. Si la red no admite estas características de seguridad, deberá intentar resolver las restricciones de conexión. Si la delegación y suplantación no están habilitadas, las credenciales de Windows se pueden pasar por una conexión de equipo antes de expirar. La conexión de un usuario desde un equipo cliente al equipo de servidor de informes cuenta como la primera conexión. Si el usuario abre un informe que recupera datos de un servidor remoto, ese inicio de sesión cuenta como segunda conexión y generará un error si ha especificado que la conexión use seguridad integrada cuando la delegación no está habilitada.  
  
 Si necesita varias conexiones para completar un ciclo de ida y vuelta desde el equipo cliente a un origen de datos de informe externo, elija alguna de las estrategias siguientes para realizar las conexiones.  
  
-   Habilite las características de suplantación y delegación en el dominio de manera que las credenciales se puedan delegar a otros equipos sin límite.  
  
-   Utilice credenciales almacenadas o solicitadas para realizar consultas en los orígenes de datos externos a fin de obtener datos para los informes. Las credenciales pueden ser una cuenta de dominio de Windows o un inicio de sesión de base de datos.  
  
### <a name="prompted-credentials"></a>Credenciales solicitadas  
 Al configurar una conexión de origen de datos del informe para usar las credenciales solicitadas, cada usuario que tiene acceso al informe debe escribir un nombre de usuario y una contraseña para recuperar los datos. Esta opción es recomendable para informes que contengan información confidencial. Las credenciales solicitadas solo se pueden usar en los informes que se ejecutan a petición. Las credenciales solicitadas pueden ser una cuenta de dominio de Windows o un inicio de sesión de base de datos. Para utilizar la Autenticación de Windows, debe seleccionar **Usar como credenciales de Windows para la conexión al origen de datos**. De lo contrario, el servidor de informes pasa credenciales al servidor de bases de datos para la autenticación de usuario. Si el servidor de bases de datos no puede autenticar las credenciales que proporciona, se producirá un error en la conexión.  
  
### <a name="windows-integrated-security"></a>Seguridad integrada de Windows  
 Cuando utilice la opción **Seguridad integrada de Windows** , el servidor de informes pasa el token de seguridad del usuario que tiene acceso al informe al servidor que hospeda el origen de datos externo. En este caso, no se solicita al usuario que escriba un nombre de usuario ni una contraseña. Se recomienda este enfoque si las características de suplantación y delegación están habilitadas. Si estas características no están habilitadas, solo debería usar este enfoque si todos los servidores a los que desea tener acceso se encuentran en el mismo equipo.  
  
### <a name="stored-credentials"></a>Credenciales almacenadas  
 Puede almacenar las credenciales utilizadas para tener acceso a un origen de datos externo. Las credenciales se almacenan con cifrado reversible en la base de datos del servidor de informes, Puede especificar un conjunto de credenciales almacenadas para cada origen de datos utilizado en un informe. Las credenciales que proporcione recuperan los mismos datos para cada usuario que ejecute el informe.  
  
 Se recomienda utilizar credenciales almacenadas como parte de una estrategia de acceso a servidores de bases de datos remotos. Las credenciales almacenadas son necesarias si desea admitir suscripciones, o bien programar la generación del historial del informe o actualizaciones de instantáneas de informe. Cuando un informe se ejecuta como un proceso en segundo plano, el servidor de informes es el agente que ejecuta el informe. Puesto que no existe un contexto de usuario, el servidor de informes debe obtener información de credenciales de la base de datos del servidor de informes para conectarse a un origen de datos.  
  
 El nombre de usuario y la contraseña que especifique pueden ser credenciales de Windows o un inicio de sesión de base de datos. Si especifica credenciales de Windows, el servidor de informes las envía a Windows para la autenticación consiguiente. De lo contrario, las credenciales se envían al servidor de bases de datos para realizar la autenticación.  
  
#### <a name="how-to-grant-allow-log-on-locally-permissions-to-domain-user-accounts"></a>Cómo conceder permisos "Permitir el inicio de sesión local" a cuentas de dominio de usuario  
 Si usa credenciales almacenadas para conectarse a un origen de datos externo, la cuenta de usuario de dominio de Windows debe tener permiso para iniciar sesión localmente. Este permiso permite al servidor de informes suplantar al usuario en el servidor de informes y enviar la solicitud al origen de datos externo como dicho usuario suplantado.  
  
 Para conceder este permiso, haga lo siguiente:  
  
1.  En el equipo del servidor de informes, en **Herramientas administrativas**, abra **Directiva de seguridad local**.  
  
2.  En **Configuración de seguridad**, expanda **Directivas locales**y, a continuación, haga clic en **Asignación de derechos de usuario**.  
  
3.  En el panel de detalles, haga clic con el botón derecho en **Permitir el inicio de sesión local** y, después, haga clic con el botón derecho en **Propiedades**.  
  
4.  Haga clic en **Agregar grupo o usuario**.  
  
5.  Haga clic en **Ubicaciones**, especifique un dominio u otra ubicación en la que desee buscar y, a continuación, haga clic en **Aceptar**.  
  
6.  Escriba la cuenta de Windows para la que desea permitir el inicio de sesión interactivo y, a continuación, haga clic en **Aceptar**.  
  
7.  En el cuadro de diálogo **Propiedades de Permitir el inicio de sesión local** , haga clic en **Aceptar**.  
  
8.  Compruebe que la cuenta que ha seleccionado no tiene permisos de denegación:  
  
    1.  Haga clic con el botón derecho en **Denegar el inicio de sesión localmente** y, después, haga clic con el botón derecho en **Propiedades**.  
  
    2.  Si aparece la cuenta en la lista, selecciónela y, a continuación, haga clic en **Quitar**.  
  
#### <a name="using-impersonation-with-stored-credentials"></a>Usar la suplantación con credenciales almacenadas  
 También puede utilizar las credenciales para suplantar la identidad de otro usuario. Las bases de datos de SQL Server, debe usar la suplantación opciones establece la [SETUSER](/sql/t-sql/statements/setuser-transact-sql) función.  
  
> [!IMPORTANT]  
>  No utilice la suplantación para informes que admitan suscripciones o que utilicen programaciones para generar el historial del informe o para actualizar una instantánea de ejecución de informes.  
  
### <a name="no-credentials"></a>Sin credenciales  
 Puede configurar una conexión a un origen de datos de forma que no utilice credenciales. Microsoft recomienda que siempre utilice credenciales para tener acceso a orígenes de datos; no se aconseja prescindir de las credenciales. No obstante, puede elegir ejecutar un informe sin credenciales en los siguientes casos:  
  
-   El origen de datos remoto no requiere credenciales.  
  
-   Las credenciales se envían en la cadena de conexión (solo se recomienda para conexiones seguras).  
  
-   El informe es un subinforme que utiliza las credenciales del informe primario.  
  
 En estas condiciones, el servidor de informes se conecta a un origen de datos remoto utilizando una cuenta de ejecución desatendida que debe definirse de antemano. Dado que el servidor de informes no se conecta a un servidor remoto mediante sus credenciales de servicio, debe especificar una cuenta para que el servidor pueda realizar la conexión. Para más información sobre cómo crear esta cuenta, vea [Configurar la cuenta de ejecución desatendida &#40;Administrador de configuración de SSRS&#41;](../install-windows/configure-the-unattended-execution-account-ssrs-configuration-manager.md).  
  
##  <a name="DataSourceConfigurationConnections"></a> Configuración de orígenes de datos y conexiones de red  
 La tabla siguiente muestra cómo se realizan las conexiones para combinaciones específicas de tipos de credenciales y extensiones de procesamiento de datos. Si usa una extensión de procesamiento de datos personalizada, vea [Especificar conexiones para extensiones de procesamiento de datos personalizadas](specify-connections-for-custom-data-processing-extensions.md).  
  
|**Tipo**|**Contexto para la conexión de red**|**Tipos de orígenes de datos**<br /><br /> **(SQL Server, Oracle, ODBC, OLE DB, Analysis Services, XML, SAP NetWeaver BI, Hyperion Essbase)**|  
|--------------|----------------------------------------|------------------------------------------------------------------------------------------------------------------------------------|  
|Seguridad integrada|Suplantar al usuario actual|Para todos los tipos de orígenes de datos, conectar mediante la cuenta de usuario actual.|  
|Credenciales de Windows|Suplantar al usuario especificado|Para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], Oracle, ODBC y OLE DB: conectar mediante la cuenta de usuario suplantado.|  
|Credenciales de base de datos|Suplantar la cuenta de ejecución desatendida o la cuenta de servicio.<br /><br /> Reporting Services quita los permisos de administrador cuando la solicitud de conexión se envía utilizando la identidad de servicio.|Para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], Oracle, ODBC y OLE DB:<br /><br /> Anexe el nombre de usuario y la contraseña a la cadena de conexión.<br /><br /> Para [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]:<br /><br /> La conexión será satisfactoria si está utilizando el protocolo TCP/IP; de lo contrario, la conexión generará error.<br /><br /> Para XML:<br /><br /> La conexión dará error en el servidor de informes si se utilizan las credenciales de la base de datos.|  
|None|Suplantar la cuenta de ejecución desatendida.|Para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], Oracle, ODBC y OLE DB:<br /><br /> Use las credenciales definidas en la cadena de conexión. La conexión generará error en el servidor de informes si la cuenta de ejecución desatendida está sin definir.<br /><br /> Para [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]:<br /><br /> La conexión siempre generará error si no se han especificado credenciales, aunque se haya definido la cuenta de ejecución desatendida.<br /><br /> Para XML:<br /><br /> Conéctese como usuario anónimo si la cuenta de ejecución desatendida se ha definido; de lo contrario, la conexión generará error.|  
  
## <a name="setting-credentials-programmatically"></a>Establecer credenciales mediante programación  
 Puede establecer credenciales en el código para controlar el acceso a informes y al servidor de informes. Para obtener más información, consulte [orígenes de datos y métodos de conexión](../report-server-web-service/methods/data-sources-and-connection-methods.md).  
  
## <a name="see-also"></a>Vea también  
 [Orígenes de datos admitidos por Reporting Services &#40;SSRS&#41;](../create-deploy-and-manage-mobile-and-paginated-reports.md)   
 [Las conexiones de datos, orígenes de datos y cadenas de conexión en Reporting Services](../data-connections-data-sources-and-connection-strings-in-reporting-services.md)   
 [Administrar los orígenes de datos de informe](../../integration-services/connection-manager/data-sources.md)   
 [El Administrador de informes &#40;modo nativo de SSRS&#41;](../report-manager-ssrs-native-mode.md)   
 [Crear, eliminar o modificar un origen de datos compartido &#40;el Administrador de informes&#41;](../create-delete-or-modify-a-shared-data-source-report-manager.md)   
 [Configurar las propiedades del origen de datos para un informe &#40;el Administrador de informes&#41;](configure-data-source-properties-for-a-report-report-manager.md)  
  
  
