---
title: Conectarse a una base de datos de modelo Tabular (SSAS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: 983d0c8a-77da-4c6e-8638-283bcb14f143
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 6f73a8e9e79a08c3f4a1f1e2b40ff5f83a0e39b7
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/23/2019
ms.locfileid: "66067656"
---
# <a name="connect-to-a-tabular-model-database-ssas"></a>Conectar a una base de datos de modelo tabular (SSAS)
  Después de generar un modelo tabular e implementarlo en un servidor de modo tabular de Analysis Services, debe establecer los permisos que permiten que esté disponible para las aplicaciones cliente. Este tema explica cómo establecer permisos y cómo conectarse a una base de datos de aplicaciones cliente.  
  
> [!NOTE]  
>  De forma predeterminada, las conexiones remotas a Analysis Services no están disponibles hasta que se configura el firewall. Asegúrese de que ha abierto el puerto adecuado si configura una instancia con nombre o predeterminada para las conexiones de cliente. Para obtener más información, consulte [Configure the Windows Firewall to Allow Analysis Services Access](../instances/configure-the-windows-firewall-to-allow-analysis-services-access.md).  
  
 Este tema contiene las siguientes secciones:  
  
 [Permisos de usuario en la base de datos](#bkmk_userpermissions)  
  
 [Permisos administrativos en el servidor](#bkmk_admin)  
  
 [Conexión de Excel o de SharePoint](#bkmk_excelconn)  
  
 [Solucionar problemas de conexión](#bkmk_Tshoot)  
  
##  <a name="bkmk_userpermissions"></a> Permisos de usuario en la base de datos  
 Los usuarios que se conecten a bases de datos tabulares deben pertenecer a un rol de base de datos que especifique el acceso de lectura.  
  
 Los roles, y a veces la pertenencia a los roles, se definen al crear un modelo en [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)], o en el caso de los modelos implementados, mediante [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]. Para obtener más información sobre cómo crear roles mediante el Administrador de roles en [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)], vea [Crear y administrar roles &#40;SSAS tabular&#41;](roles-ssas-tabular.md). Para obtener más información sobre cómo crear y administrar roles para un modelo implementado, vea [Roles de modelos tabulares &#40;SSAS tabular&#41;](tabular-model-roles-ssas-tabular.md).  
  
> [!CAUTION]  
>  El nuevo despliegue de un proyecto de modelos tabular con roles definidos mediante el Administrador de roles de [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)] sobrescribirá los roles definidos en un modelo tabular implementado.  
  
##  <a name="bkmk_admin"></a> Permisos administrativos en el servidor  
 En el caso de organizaciones que utilicen SharePoint para hospedar libros de Excel o informes de Reporting Services, se requiere una configuración adicional para hacer que los datos del modelo semántico de Business Intelligence estén a disposición de los usuarios de SharePoint. Si no va a utilizar SharePoint, omita esta sección.  
  
 Para ver libros de Excel o informes de [!INCLUDE[ssCrescent](../../includes/sscrescent-md.md)] que contengan datos tabulares, se requiere que la cuenta utilizada para ejecutar Excel Services o Reporting Services tenga permisos de administrador en la instancia de Analysis Services. Se requieren permisos administrativos para que estos servicios sean de confianza para la instancia de Analysis Services.  
  
#### <a name="grant-administrative-access-on-the-server"></a>Conceder acceso administrativo en el servidor  
  
1.  En Administración central, abra la página Configurar cuentas de servicio.  
  
2.  Seleccione el grupo de aplicaciones de servicio que utiliza Excel Services. Es posible que **grupo de aplicaciones de servicio - sistema de SharePoint Web Services** o un grupo de aplicaciones personalizadas. La cuenta administrada que utiliza Excel Services aparecerá en la página.  
  
     Para las granjas de servidores de SharePoint que incluyen Reporting Services en modo de SharePoint, obtenga también la información de cuenta para la aplicación de servicio de Reporting Services.  
  
     En los pasos siguientes, agregará estas cuentas al rol de servidor de la instancia de Analysis Services.  
  
3.  En [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], conéctese a la instancia de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)], haga clic con el botón derecho en la instancia del servidor y seleccione **Propiedades**. En el Explorador de objetos, haga clic con el botón derecho en **Roles** y seleccione **Nuevo rol**.  
  
4.  En la página Propiedades de Analysis Services, haga clic en **Seguridad**.  
  
5.  Haga clic en **Agregar**y escriba la cuenta utilizada por Excel Services, seguida de la cuenta utilizada por Reporting Services.  
  
##  <a name="bkmk_excelconn"></a> Conexión de Excel o de SharePoint  
 Las bibliotecas cliente que proporcionan acceso a las bases de datos de Analysis Services se pueden utilizar para conectarse a bases de datos de modelo que se ejecutan en un servidor de modo tabular. Las bibliotecas incluyen el proveedor OLE DB de Analysis Services, ADOMD.NET y AMO.  
  
 Excel usa el proveedor OLE DB. Si tiene MSOLAP.4 de SQL Server 2008 R2 (nombre de archivo msolap100.dll, versión 10.50.1600.1) o MSOLAP.5 (nombre de archivo msolap110.dll) que se instala con la versión para [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] de PowerPivot para Excel, tiene una versión que se conectará a las bases de datos tabulares.  
  
 Elija uno de los métodos siguientes para conectarse a las bases de datos de modelo desde Excel:  
  
-   Cree una conexión de datos desde Excel, utilizando las instrucciones proporcionadas en la sección siguiente.  
  
-   Cree un archivo de conexión de modelo semántico de BI (.bism) en SharePoint que proporcione redirección a una base de datos que se ejecute en un servidor de modo tabular de Analysis Services. Un archivo de conexión de modelo semántico de BI proporciona un comando para hacer clic con el botón secundario que inicia Excel con la base de datos de modelo especificada en la conexión. También se iniciará [!INCLUDE[ssCrescent](../../includes/sscrescent-md.md)] si se ha instalado Reporting Services. Para obtener más información sobre cómo crear y usar archivos de conexión de modelo semántico de BI, vea [Crear una conexión de modelo semántico de BI a una base de datos de modelo tabular](../power-pivot-sharepoint/create-a-bi-semantic-model-connection-to-a-tabular-model-database.md).  
  
-   Crear un origen de datos compartido de Reporting Services que haga referencia a una base de datos tabular como origen de datos. Puede crear el origen de datos compartido en SharePoint y usarlo para iniciar [!INCLUDE[ssCrescent](../../includes/sscrescent-md.md)].  
  
#### <a name="connect-from-excel"></a>Conexión de Excel  
  
1.  En Excel 2010, en la pestaña **Datos** , en **Obtener datos externos**, haga clic en **De otros orígenes**.  
  
2.  Seleccione **Desde Analysis Services**.  
  
3.  En **Nombre del servidor**, especifique la instancia de Analysis Services que hospeda la base de datos. El nombre de servidor suele ser el del equipo que ejecuta el software del servidor. Si el servidor se instaló como una instancia con nombre, debe especificar el nombre en este formato: \<servername >\\< nombreDeInstancia\>.  
  
     La instancia de servidor debe configurarse para la implementación tabular independiente y la instancia de servidor debe tener una regla de entrada que permita el acceso a ella. Para obtener más información, vea [Determinar el modo de servidor de una instancia de Analysis Services](../instances/determine-the-server-mode-of-an-analysis-services-instance.md) y [Configurar Firewall de Windows para permitir el acceso a Analysis Services](../instances/configure-the-windows-firewall-to-allow-analysis-services-access.md).  
  
4.  Para las credenciales de inicio de sesión, elija **Utilizar autenticación de Windows** si tiene permisos de lectura para la base de datos. De lo contrario, elija **Usar el nombre de usuario y la contraseña siguientes**y escriba el nombre de usuario y la contraseña de una cuenta de Windows que tenga permisos de base de datos. Haga clic en **Siguiente**.  
  
5.  Seleccione la base de datos. Una selección válida mostrará un solo cubo de **Modelo** para la base de datos. Haga clic en **Siguiente** y, a continuación, en **Finalizar**.  
  
 Una vez establecida la conexión, puede utilizar los datos para crear una tabla dinámica o un gráfico dinámico. Para obtener más información, vea [Analizar en Excel &#40;SSAS tabular&#41;](analyze-in-excel-ssas-tabular.md).  
  
##  <a name="bkmk_sharepoint"></a> Conexión desde SharePoint  
 Si va a utilizar PowerPivot para SharePoint, puede crear un archivo de conexión de modelo semántico de BI en SharePoint que proporcione redirección a una base de datos que se ejecuta en un servidor de modo tabular de Analysis Services. Una conexión de modelo semántico de BI proporciona un extremo HTTP a una base de datos. También simplifica el acceso al modelo tabular para los trabajadores del conocimiento que utilizan habitualmente documentos en un sitio de SharePoint. Los trabajadores del conocimiento solo necesitan conocer la ubicación del archivo de conexión de modelo semántico de BI o su dirección URL para tener acceso a las bases de datos de modelos tabulares. Los detalles sobre el nombre de la base de datos o la ubicación del servidor se encapsulan en la conexión de modelo semántico de BI. Para obtener más información sobre cómo crear y usar archivos de conexión de modelo semántico de BI, consulte [PowerPivot BI Semantic Model Connection &#40;.bism&#41; ](../power-pivot-sharepoint/power-pivot-bi-semantic-model-connection-bism.md) y [crear una conexión de modelo semántico de BI a un modelo Tabular Base de datos](../power-pivot-sharepoint/create-a-bi-semantic-model-connection-to-a-tabular-model-database.md).  
  
##  <a name="bkmk_Tshoot"></a> Solucionar problemas de conexión  
 En esta sección se proporcionan las causas y los pasos de resolución de los problemas que se producen al conectarse a una base de datos de modelo tabular.  
  
 **El Asistente para la conexión de datos no puede obtener una lista de bases de datos del origen de datos especificado.**  
  
 Al importar datos, este error de Microsoft Excel tiene lugar cuando intenta utilizar el asistente para conectarse a una base de datos de modelo tabular en un servidor de Analysis Services remoto y no tiene suficientes permisos. Para resolver este error, debe tener derechos de acceso de usuario en la base de datos. Consulte las instrucciones proporcionadas anteriormente en este tema para conceder al usuario acceso a los datos.  
  
 **Se produjo un error durante un intento para establecer una conexión al origen de datos externo. No se pudieron actualizar las siguientes conexiones: \<nombre de modelo > espacio aislado**  
  
 En SharePoint, este error de Microsoft Excel tiene lugar cuando se intenta llevar a cabo una interacción con los datos, por ejemplo filtrar los datos, en una tabla dinámica que utilice datos del modelo. El error se produce porque no tiene los permisos necesarios en el servidor de Analysis Services remoto. Para resolver este error, debe tener derechos de acceso de usuario en la base de datos. Consulte las instrucciones proporcionadas anteriormente en este tema para conceder al usuario acceso a los datos.  
  
 **Se produjo un error al intentar realizar esta operación. Volver a cargar el libro y, a continuación, intente realizar de nuevo la operación.**  
  
 En SharePoint, este error de Microsoft Excel tiene lugar cuando se intenta llevar a cabo una interacción con los datos, por ejemplo filtrar los datos, en una tabla dinámica que utilice datos del modelo. El error se produce porque Excel Services no es de confianza para la instancia de Analysis Services en la que se implementan los datos del modelo. Para resolver este error, conceda a Excel Services permisos administrativos en la instancia de Analysis Services. Consulte las instrucciones proporcionadas anteriormente en este tema para conceder permisos de administrador. Si el error persiste, recicle el grupo de aplicaciones de Excel Services.  
  
 **Error al intentar establecer una conexión con el origen de datos externo que se usa en el libro**  
  
 En SharePoint, este error de Microsoft Excel tiene lugar cuando se intenta llevar a cabo una interacción con los datos, por ejemplo filtrar los datos, en una tabla dinámica que utilice datos del modelo. El error se produce porque el usuario no tiene suficientes permisos de SharePoint en el libro. El usuario debe tener permisos de **Lectura** o superiores. Los permisos**Solo ver** no son suficientes para el acceso a los datos.  
  
## <a name="see-also"></a>Vea también  
 [Implementación de soluciones de modelos tabulares &#40;SSAS tabular&#41;](tabular-model-solution-deployment-ssas-tabular.md)  
  
  
