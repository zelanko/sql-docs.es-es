---
title: Conectarse desde aplicaciones cliente (Analysis Services) | Documentos de Microsoft
ms.custom: 
ms.date: 03/07/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: instances
ms.reviewer: 
ms.suite: sql
ms.technology:
- analysis-services
- analysis-services/multidimensional-tabular
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.swb.connection.login.analysisserver.f1
- sql13.swb.connecttoas.connectionproperties.f1
- sql13.swb.connecttoas.login.f1
ms.assetid: b1e0f1d4-0b87-4ad3-8172-f746fe2f16a2
caps.latest.revision: "9"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: On Demand
ms.openlocfilehash: 0310a1012153fae8ecb364e63a270ce0846af277
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 11/17/2017
---
# <a name="connect-from-client-applications-analysis-services"></a>Conectarse desde aplicaciones cliente (Analysis Services)
  Si no está familiarizado con Analysis Services, use la información de este tema para conectarse a una instancia existente de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] mediante herramientas y aplicaciones comunes. En este tema también explica cómo conectarse bajo distintas identidades de usuario para realizar pruebas.  
  
-   [Conectarse con SQL Server Management Studio (SSMS)](#bkmk_SSMS)  
  
-   [Conectarse con Excel](#bkmk_excel)  
  
-   [Conectarse con SQL Server Data Tools](#bkmk_SSDT)  
  
-   [Probar conexiones](#bkmk_tshoot)  
  
 La documentación de referencia de la cadena de conexión se proporciona por separado. Para obtener más información, vea [Propiedades de cadena de conexión &#40;Analysis Services&#41;](../../analysis-services/instances/connection-string-properties-analysis-services.md).  
  
 Las conexiones correctas dependen de si la configuración de los puertos es válida y los permisos de usuario apropiados. Haga clic en los vínculos siguientes para obtener más información acerca de cada requisito.  
  
-   [Configurar Firewall de Windows para permitir el acceso a Analysis Services](../../analysis-services/instances/configure-the-windows-firewall-to-allow-analysis-services-access.md)  
  
-   [Cómo autorizar el acceso a objetos y operaciones &#40;Analysis Services&#41;](../../analysis-services/multidimensional-models/authorizing-access-to-objects-and-operations-analysis-services.md)  
  
##  <a name="bkmk_SSMS"></a> Conectarse con SQL Server Management Studio (SSMS)  
 Conéctese a Analysis Services en SSMS para administrar las instancias de servidor y las bases de datos de forma interactiva. También puede ejecutar consultas XMLA o MDX para realizar tareas administrativas o recuperar datos. A diferencia de otras herramientas y aplicaciones que solo cargan bases de datos cuando se envía una consulta, SSMS carga todas las bases de datos cuando se conecta al servidor, siempre y cuando tenga permiso para ver la base de datos. Esto significa que si tiene numerosas bases de datos tabulares en el servidor, todas ellas se cargan en la memoria del sistema cuando se conecta mediante SSMS.  
  
 Para probar los permisos, ejecute SSMS bajo una identidad de usuario específica y conéctese después a Analysis Services como ese usuario.  
  
 Mantenga pulsada la tecla MAYÚS y haga clic con el botón derecho en el acceso directo **SQL Server Management Studio** para tener acceso a la opción **Ejecutar como otro usuario** .  
  
1.  Inicie [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]. En el cuadro de diálogo **Conectar al servidor** , seleccione el tipo de servidor [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] .  
  
2.  En la pestaña Inicio de sesión, especifique el nombre del servidor escribiendo el nombre del equipo en el que se ejecuta el servidor. Puede especificar el servidor mediante su nombre de red o un nombre de dominio completo.  
  
     En el caso de una instancia con nombre, el nombre del servidor se debe especificar en este formato: nombreDeServidor\nombreDeInstancia. Un ejemplo de esta convención de nomenclatura puede ser ADV-SRV062\Finanzas para un servidor que tenga el nombre de red ADV-SRV062, donde Analysis Services se instala como una instancia con nombre denominada Finanzas.  
  
     Para los servidores implementados en un clúster de conmutación por error, conéctese usando el nombre de red del clúster de SSAS. Este nombre se especifica durante la instalación de SQL Server, como **Nombre de red de SQL Server**. Tenga en cuenta que si instaló SSAS como una instancia con nombre en un clúster de conmutación por error de Windows Server (WSFC), nunca agregue el nombre de instancia en la conexión. Esta práctica es única en SSAS; en cambio, una instancia con nombre de un motor de base de datos relacional en clúster incluye el nombre de instancia. Por ejemplo, si instaló SSAS y el motor de base de datos como una instancia con nombre (Contoso-Contabilidad) con un Nombre de red de SQL Server de SQL-CLU, se conectaría a SSAS con “SQL-CLU” y al motor de base de datos como "SQL-CLU\Contoso-Contabilidad". Vea [Organizar en clúster SQL Server Analysis Services](http://go.microsoft.com/fwlink/p/?LinkId=396548) para obtener más información y ejemplos.  
  
     En los servidores implementados en un clúster con equilibrio de carga de red, conéctese mediante el nombre de servidor virtual del NLB.  
  
3.  La autenticación siempre es la de Windows y la identidad de usuario siempre es el usuario de Windows que se está conectando a través de Management Studio.  
  
     Para que la conexión se realice correctamente, debe tener permiso para acceder al servidor o a la base de datos del servidor. La mayoría de las tareas que desea realizar en Management Studio necesitan permisos administrativos. Asegúrese de que la cuenta con la que se está conectando es miembro del rol de administrador del servidor. Para obtener más información, vea [Conceder permisos de administrador de servidor (Analysis Services)](../../analysis-services/instances/grant-server-admin-rights-to-an-analysis-services-instance.md).  
  
4.  Haga clic en **Propiedades de conexión** para especificar una base de datos determinada, establecer valores de tiempo de espera o configurar opciones de cifrado. La información de conexión opcional incluye las propiedades de conexión que se usan para la conexión actual únicamente.  
  
5.  Haga clic en la pestaña **Parámetros de conexión adicionales** para establecer las propiedades de conexión que no están disponibles en el cuadro de diálogo Conectar al servidor. Por ejemplo, puede escribir `Roles=Reader` en el cuadro de texto.  
  
     La conexión mediante un rol con menos permisos permite probar comportamientos de la base de datos cuando ese rol está activo.  
  
    ```  
    Provider=MSOLAP; Data Source=SERVERNAME; Initial Catalog=AdventureWorks2012; Roles=READER  
    ```  
  
##  <a name="bkmk_excel"></a> Conectarse con Excel  
 Se suele usar Microsoft Excel para analizar datos empresariales. Como parte de una instalación de Excel, Office instala el proveedor OLE DB de Analysis Services (MSOLAP DLL), ADOMD.NET y otros proveedores de datos para que pueda usar más fácilmente los datos de los servidores de red. Si usa una versión más reciente de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] con una versión anterior de Excel, lo más probable es que necesite instalar proveedores de datos más recientes en todas las estaciones de trabajo que se conecten a [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]. Vea [Proveedores de datos usados para conexiones de Analysis Services](../../analysis-services/instances/data-providers-used-for-analysis-services-connections.md) para obtener más información.  
  
 Al configurar una conexión a un cubo de Analysis Services o una base de datos modelo tabular, Excel guarda la información de conexión en un archivo .odc para su uso futuro. La conexión se realiza en el contexto de seguridad del usuario actual de Windows. La cuenta de usuario debe tener permisos de lectura en la base de datos para que la conexión se establezca correctamente.  
  
 Cuando se usan datos de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] en un libro de Excel, las conexiones se mantienen mientras dura una solicitud de consulta. Esta es la razón por la que probablemente vea muchas conexiones para cada sesión, que se mantienen durante períodos de tiempo muy cortos, al supervisar una carga de trabajo de consultas de Excel.  
  
 Puede probar los permisos si inicia Excel con una identidad de usuario específica.  
  
 Mantenga pulsada la tecla MAYÚS y haga clic con el botón derecho en el acceso directo **Excel** para tener acceso a la opción **Ejecutar como otro usuario** .  
  
1.  En la pestaña Datos de Excel, haga clic en **Desde otros orígenes**y, a continuación, haga clic en **Desde Analysis Services**. Escriba el nombre del servidor y seleccione un cubo o una perspectiva para consultar.  
  
     Para los servidores implementados en un clúster con equilibrio de carga, utilice el nombre de servidor virtual asignado al clúster.  
  
2.  Al configurar una conexión en Excel, en la última página del Asistente para la conexión de datos, puede especificar los valores de autenticación para Excel Services. Esta configuración se utiliza para establecer las propiedades del libro si lo carga en un servidor de SharePoint que tenga Excel Services. La configuración se utiliza en las operaciones de actualización de datos. Entre las opciones se incluyen **Autenticación de Windows**, **Servicio de almacenamiento seguro (SSS)** y **Ninguna**.  
  
     Evite usar **Ninguna**. Analysis Services no permite especificar un nombre de usuario y una contraseña en la cadena de conexión a menos que vaya a conectarse a un servidor que esté configurado para el acceso HTTP. Asimismo, no utilice SSS a menos que ya sepa que el identificador de la aplicación de destino SSS está asignado a un conjunto de credenciales de usuario de Windows que tiene acceso a las bases de datos de Analysis Services. En la mayoría de los escenarios, la opción de autenticación de Windows predeterminada es la mejor opción para una conexión de Analysis Services desde Excel.  
  
 Para obtener más información, vea [Conectarse a datos o importarlos desde SQL Server Analysis Services](http://go.microsoft.com/fwlink/?linkID=215150).  
  
##  <a name="bkmk_SSDT"></a> Conectarse con SQL Server Data Tools  
 SQL Server Data Tools se usa para compilar soluciones de BI, incluidos modelos de Analysis Services, informes de Reporting Services y paquetes SSIS. Al compilar informes o paquetes, puede que necesite especificar una conexión con Analysis Services.  
  
 Los vínculos siguientes explican cómo conectarse a Analysis Services desde un proyecto de servidor de informes o un proyecto de Integration Services:  
  
-   [Tipo de conexión de Analysis Services para MDX &#40;SSRS&#41;](../../reporting-services/report-data/analysis-services-connection-type-for-mdx-ssrs.md)  
  
-   [Administrador de conexiones de Analysis Services](../../integration-services/connection-manager/analysis-services-connection-manager.md)  
  
> [!NOTE]  
>  Cuando use SQL Server Data Tools para trabajar en un proyecto de Analysis Services existente, recuerde que puede conectarse sin conexión mediante un proyecto local o un proyecto con control de versiones, o puede conectarse en modo en línea para actualizar objetos de Analysis Services mientras la base de datos está en ejecución. Para obtener más información, vea [Connect in Online Mode to an Analysis Services Database](../../analysis-services/multidimensional-models/connect-in-online-mode-to-an-analysis-services-database.md). Normalmente, las conexiones desde [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)] están en modo de proyecto, en el que los cambios se implementan en la base de datos solo cuando el proyecto se implementa de modo explícito.  
  
##  <a name="bkmk_tshoot"></a> Probar conexiones  
 Puede usar SQL Server Profiler para supervisar las conexiones con Analysis Services. Los eventos Audit Login y Audit Logout proporcionan la prueba de una conexión. La columna de identidad indica el contexto de seguridad bajo el que se realiza la conexión.  
  
1.  Inicie **SQL Server Profiler** en la instancia de Analysis Services e inicie después un nuevo seguimiento.  
  
2.  En Selección de eventos, compruebe que **Audit Login** y **Audit Logout** están activadas en la sección Auditoría de seguridad.  
  
3.  Conéctese a Analysis Services a través de un servicio de aplicación (como SharePoint o Reporting Services) desde un equipo cliente remoto. El evento Audit Login mostrará la identidad del usuario que se conecta a Analysis Services.  
  
 Se suele hacer un seguimiento de los errores de conexión hasta llegar a una configuración de servidor incompleta o no válida. Compruebe siempre la configuración del servidor primero:  
  
-   Haga ping al servidor desde un equipo remoto para asegurarse de que permite conexiones remotas.  
  
-   **Las reglas de firewall del servidor permiten conexiones entrantes de clientes del mismo dominio**  
  
     A excepción de [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] para SharePoint, todas las conexiones a un servidor remoto requieren que haya configurado el firewall para permitir el acceso al puerto en el que Analysis Services escucha. Si está obteniendo errores de conexión, compruebe que el puerto es accesible y que se han concedido los permisos de usuario a las bases de datos correspondientes.  
  
     Para probar, use Excel o SSMS en un equipo remoto, especificando la dirección IP y el puerto empleados por la instancia de Analysis Services. Si puede conectarse, las reglas de firewall son válidas para la instancia y la instancia permite conexiones remotas.  
  
     Además, cuando se usa TCP/IP para el protocolo de conexión, recuerde que Analysis Services necesita que las conexiones de cliente se originen desde el mismo dominio o desde un dominio de confianza. Si las conexiones fluyen a través de los límites de seguridad, probablemente tendrá que configurar el acceso HTTP. Para obtener más información, vea [Configurar el acceso HTTP a Analysis Services en Internet Information Services &#40;IIS&#41; 8.0](../../analysis-services/instances/configure-http-access-to-analysis-services-on-iis-8-0.md).  
  
-   ¿Puede conectarse con algunas herramientas pero no con otras? El problema podría ser la versión errónea de una biblioteca de cliente. Puede obtener bibliotecas de cliente en la página de descarga de SQL Server Feature Pack.  
  
 He aquí algunos recursos que pueden ayudarle a resolver errores de conexión:  
  
 [Resolver problemas comunes de conectividad en escenarios de conectividad de SQL Server 2005 Analysis Services](http://technet.microsoft.com/library/cc917670.aspx) Este documento tiene algunos años de antigüedad, pero la información y las metodologías que contiene siguen siendo aplicables.  
  
## <a name="see-also"></a>Vea también  
 [Conectar a Analysis Services](../../analysis-services/instances/connect-to-analysis-services.md)   
 [Metodologías de autenticación admitidas por Analysis Services](../../analysis-services/instances/authentication-methodologies-supported-by-analysis-services.md)   
 [Suplantación &#40; SSAS Tabular &#41;](../../analysis-services/tabular-models/impersonation-ssas-tabular.md)   
 [Crear un origen de datos &#40;SSAS multidimensional&#41;](../../analysis-services/multidimensional-models/create-a-data-source-ssas-multidimensional.md)  
  
  
