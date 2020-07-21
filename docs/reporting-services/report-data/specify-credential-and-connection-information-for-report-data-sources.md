---
title: Especificación de información de credenciales y conexión para los orígenes de datos de informes | Microsoft Docs
description: Un servidor de informes utiliza credenciales para conectarse a orígenes de datos externos que proporcionan contenido a informes o información de destinatarios a una suscripción controlada por datos.
ms.date: 12/09/2019
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: report-data
ms.topic: conceptual
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
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: ab7f9d0717cac0dae86eb2b5202fd02de254c5e0
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 03/29/2020
ms.locfileid: "75244561"
---
# <a name="specify-credential-and-connection-information-for-report-data-sources"></a>Especificar información de credenciales y conexión para los orígenes de datos de informes
  Un servidor de informes utiliza credenciales para conectarse a orígenes de datos externos que proporcionan contenido a informes o información de destinatarios a una suscripción controlada por datos. Puede especificar credenciales que utilicen la autenticación de Windows, la autenticación de la base de datos, la autenticación personalizada o que no utilicen autenticación. Al enviar una solicitud de conexión a través de la red, el servidor de informes suplantará una cuenta de usuario o una cuenta de ejecución desatendida. Para obtener más información acerca del contexto de seguridad en el que se realiza una solicitud de conexión, vea [Configuración de orígenes de datos y conexiones de red](#DataSourceConfigurationConnections) más adelante en este tema.  
  
> [!NOTE]  
>  Las credenciales también sirven para autenticar a usuarios que tengan acceso a un servidor de informes. La información acerca de la autenticación de usuarios en un servidor de informes se proporciona en otro tema.  
  
 La conexión a un origen de datos externo se define cuando se crea el informe. Una vez publicado éste, se puede administrar por separado. Puede especificar una cadena de conexión estática o una expresión que permita a los usuarios seleccionar un origen de datos de una lista dinámica. Para más información sobre cómo especificar un tipo de origen de datos y una cadena de conexión, vea [Creación de cadenas de conexión de datos - Generador de informes y SSRS](../../reporting-services/report-data/data-connections-data-sources-and-connection-strings-report-builder-and-ssrs.md).  
  
## <a name="when-credentials-are-used-in-report-builder"></a>Cuando se usan las credenciales en el Generador de informes  
 En el Generador de informes, se suelen usar credenciales al conectarse a un servidor de informes o para las tareas relacionadas con datos, como crear un origen de datos incrustado, ejecutar una consulta del conjunto de datos u ofrecer una vista previa de un informe. Las credenciales no se guardan en el informe. Se administran separadamente en el servidor de informes o en el cliente local. La siguiente lista describe los tipos de credenciales que podría necesitar proporcionar, donde están almacenadas y cómo se utilizan:  
  
-   Las credenciales del servidor de informes que se escriben en el cuadro de diálogo Inicio de sesión de Reporting Services.  
  
     La primera vez que guarda en, publica en o va a un servidor de informes o un sitio de SharePoint, es posible que necesite escribir sus credenciales. Las credenciales que escribe se utilizan hasta el final de la sesión en el Generador de informes. Si decide guardar las credenciales, se almacenan con seguridad en el equipo junto con su configuración de usuario. En las siguientes sesiones del Generador de informes, se usan las credenciales guardadas para conectar con el mismo servidor de informes o con el sitio de SharePoint. El administrador del servidor de informes o el administrador de SharePoint especifica qué tipo de credenciales hay que utilizar.  
  
-   Las credenciales del origen de datos que escriba en la página [Propiedades del origen de datos (cuadro de diálogo), Credenciales &#40;Generador de informes&#41;](https://msdn.microsoft.com/library/4531f09f-d653-4c05-a120-d7788838bc99) de un origen de datos incrustados.  
  
     El servidor de informes utiliza estas credenciales para realizar una conexión de datos al origen de datos externo. Para algunos tipos de orígenes de datos, las credenciales pueden estar almacenadas con seguridad en el servidor de informes. Estas credenciales permiten a otros usuarios ejecutar el informe sin proporcionar las credenciales para la conexión de datos subyacente.  
  
-   Las credenciales del origen de datos que se escriben en el cuadro de diálogo **Escribir credenciales de origen de datos** al ejecutar una consulta de conjunto de datos, actualizar campos del conjunto de datos o generar una vista previa del informe.  
  
     Estas credenciales se utilizan para realizar una conexión de datos desde el Generador de informes al origen de datos externo o para ofrecer una vista previa de un informe que se configura para que pida las credenciales. Las credenciales que escribe en este cuadro de diálogo no están almacenadas en el servidor de informes y no están disponible para su uso por otros usuarios. El Generador de informes almacena en memoria caché las credenciales durante la sesión de edición del informe, para que no necesite escribirlas cada vez ejecuta la consulta u ofrece una vista previa del informe.  
  
     Para los orígenes de datos compartidos, utilice la opción **Guardar mi contraseña** para guardar localmente las credenciales con sus valores de usuario en su equipo. El Generador de informes utiliza las credenciales guardadas cada vez que se realiza una conexión al origen de datos externo correspondiente.  
  
 Para más información, vea [Propiedades del origen de datos (cuadro de diálogo), General &#40;Generador de informes&#41;](https://msdn.microsoft.com/library/b956f43a-8426-4679-acc1-00f405d5ff5b) y [Mostrar la vista previa de informes en el Generador de informes](../../reporting-services/report-builder/previewing-reports-in-report-builder.md).  
  
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
 También puede utilizar las credenciales para suplantar la identidad de otro usuario. En el caso de las bases de datos de SQL Server, al usar las opciones de suplantación, se establece la función [SETUSER](../../t-sql/statements/setuser-transact-sql.md) .  
  
> [!IMPORTANT]  
>  No utilice la suplantación para informes que admitan suscripciones o que utilicen programaciones para generar el historial del informe o para actualizar una instantánea de ejecución de informes.  
  
### <a name="no-credentials"></a>Sin credenciales  
 Puede configurar una conexión a un origen de datos de forma que no utilice credenciales. Microsoft recomienda que siempre utilice credenciales para tener acceso a orígenes de datos; no se aconseja prescindir de las credenciales. No obstante, puede elegir ejecutar un informe sin credenciales en los siguientes casos:  
  
-   El origen de datos remoto no requiere credenciales.  
  
-   Las credenciales se envían en la cadena de conexión (solo se recomienda para conexiones seguras).  
  
-   El informe es un subinforme que utiliza las credenciales del informe primario.  
  
 En estas condiciones, el servidor de informes se conecta a un origen de datos remoto utilizando una cuenta de ejecución desatendida que debe definirse de antemano. Dado que el servidor de informes no se conecta a un servidor remoto mediante sus credenciales de servicio, debe especificar una cuenta para que el servidor pueda realizar la conexión. Para más información sobre cómo crear esta cuenta, vea [Configurar la cuenta de ejecución desatendida &#40;Administrador de configuración de SSRS&#41;](../../reporting-services/install-windows/configure-the-unattended-execution-account-ssrs-configuration-manager.md).  
  
## <a name="user-name-and-password-login"></a>Inicio de sesión con nombre de usuario y contraseña  
 Cuando se selecciona la opción **Usar este nombre de usuario y esta contraseña**, debe especificarse un nombre de usuario y una contraseña para obtener acceso al origen de datos. En el caso de una base de datos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , las credenciales podrían servir para iniciar sesión en la base de datos. Las credenciales se pasan al origen de datos externo para su autenticación.  
  
##  <a name="data-source-configuration-and-network-connections"></a><a name="DataSourceConfigurationConnections"></a> Configuración de orígenes de datos y conexiones de red  
 La tabla siguiente muestra cómo se realizan las conexiones para combinaciones específicas de tipos de credenciales y extensiones de procesamiento de datos. Si usa una extensión de procesamiento de datos personalizada, vea [Especificar conexiones para extensiones de procesamiento de datos personalizadas](../../reporting-services/report-data/specify-connections-for-custom-data-processing-extensions.md).  
  
|**Tipo**|**Contexto para la conexión de red**|**Tipos de orígenes de datos**<br /><br /> **(SQL Server, Oracle, ODBC, OLE DB, Analysis Services, XML, SAP NetWeaver BI, Hyperion Essbase)**|  
|--------------|----------------------------------------|------------------------------------------------------------------------------------------------------------------------------------|  
|Seguridad integrada|Suplantar al usuario actual|Para todos los tipos de orígenes de datos, conectar mediante la cuenta de usuario actual.|  
|Credenciales de Windows|Suplantar al usuario especificado|Para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], Oracle, ODBC y OLE DB: conectar mediante la cuenta de usuario suplantado.|  
|Credenciales de base de datos|Suplantar la cuenta de ejecución desatendida o la cuenta de servicio.<br /><br /> Reporting Services quita los permisos de administrador cuando la solicitud de conexión se envía utilizando la identidad de servicio.|Para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], Oracle, ODBC y OLE DB:<br /><br /> Anexe el nombre de usuario y la contraseña a la cadena de conexión.<br /><br /> Para [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]:<br /><br /> La conexión será satisfactoria si está utilizando el protocolo TCP/IP; de lo contrario, la conexión generará error.<br /><br /> Para XML:<br /><br /> La conexión dará error en el servidor de informes si se utilizan las credenciales de la base de datos.|  
|None|Suplantar la cuenta de ejecución desatendida.|Para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], Oracle, ODBC y OLE DB:<br /><br /> Use las credenciales definidas en la cadena de conexión. La conexión generará error en el servidor de informes si la cuenta de ejecución desatendida está sin definir.<br /><br /> Para [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]:<br /><br /> La conexión siempre generará error si no se han especificado credenciales, aunque se haya definido la cuenta de ejecución desatendida.<br /><br /> Para XML:<br /><br /> Conéctese como usuario anónimo si la cuenta de ejecución desatendida se ha definido; de lo contrario, la conexión generará error.|  
  
## <a name="setting-credentials-programmatically"></a>Establecer credenciales mediante programación  
 Puede establecer credenciales en el código para controlar el acceso a informes y al servidor de informes. Para más información, consulte [Data Sources and Connection Methods](../../reporting-services/report-server-web-service/methods/data-sources-and-connection-methods.md).  
  
## <a name="see-also"></a>Consulte también  
 [Orígenes de datos admitidos por Reporting Services &#40;SSRS&#41;](../../reporting-services/report-data/data-sources-supported-by-reporting-services-ssrs.md)   
 [Creación de cadenas de conexión de datos - Generador de informes y SSRS](../../reporting-services/report-data/data-connections-data-sources-and-connection-strings-report-builder-and-ssrs.md)   
 [Administrar orígenes de datos de informe](../../reporting-services/report-data/manage-report-data-sources.md)   
 [Configuración de propiedades de origen de datos para un informe](../../reporting-services/report-data/configure-data-source-properties-for-a-report-report-manager.md)  
  
  
