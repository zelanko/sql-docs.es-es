---
title: "Crear un origen de datos (SSAS multidimensional) | Microsoft Docs"
ms.custom: ""
ms.date: "03/16/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "analysis-services"
  - "analysis-services/multidimensional-tabular"
  - "analysis-services/data-mining"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "sql13.asvs.sqlserverstudio.impersonationinfo.f1"
  - "sql13.asvs.connectionmanager.f1"
  - "sql13.asvs.datasourcedesigner.f1"
helpviewer_keywords: 
  - "suplantación [Analysis Services]"
  - "orígenes de datos [Analysis Services], crear"
  - "seguridad [Analysis Services], conexiones de orígenes de datos"
ms.assetid: 9fab8298-10dc-45a9-9a91-0c8e6d947468
caps.latest.revision: 61
author: "Minewiskan"
ms.author: "owend"
manager: "erikre"
caps.handback.revision: 61
---
# Crear un origen de datos (SSAS multidimensional)
  En un modelo multidimensional de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)], un objeto de origen de datos representa una conexión al origen de datos del que va a procesar o importar los datos. Un modelo multidimensional debe contener al menos un objeto de origen de datos, pero puede agregar más para combinar datos de varios almacenamientos de datos. Siga las instrucciones de este tema para crear un objeto de origen de datos para el modelo. Para obtener más información sobre cómo establecer propiedades en este objeto, vea [Establecer propiedades de origen de datos &#40;SSAS multidimensional&#41;](../../analysis-services/multidimensional-models/set-data-source-properties-ssas-multidimensional.md).  
  
 En este tema se incluyen las secciones siguientes:  
  
 [Elegir un proveedor de datos](#bkmk_provider)  
  
 [Establecer las opciones de suplantación y las credenciales](#bkmk_impersonation)  
  
 [Ver o modificar propiedades de conexión](#bkmk_ConnectionString)  
  
 [Crear un origen de datos con el Asistente para orígenes de datos](#bkmk_steps)  
  
 [Crear un origen de datos con una conexión existente](#bkmk_connection)  
  
 [Agregar varios orígenes de datos a un modelo](#bkmk_multipleDS)  
  
##  <a name="bkmk_provider"></a> Elegir un proveedor de datos  
 Puede conectarse con un proveedor OLE DB nativo o [!INCLUDE[msCoName](../../includes/msconame-md.md)] .NET Framework administrado. El proveedor de datos recomendado para los orígenes de datos de SQL Server es SQL Server Native Client porque proporciona un mejor rendimiento.  
  
 Para Oracle y otros orígenes de datos de terceros, compruebe si el de otros fabricantes proporciona un proveedor OLE DB y pruebe con ese primero. Si surgen errores, pruebe alguno de los otros proveedores .NET o de los proveedores de OLE DB nativos enumerados en el Administrador de conexiones. Asegúrese de que cualquier proveedor de datos que utilice está instalado en todos los equipos utilizados para desarrollar y ejecutar la solución de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] .  
  
##  <a name="bkmk_impersonation"></a> Establecer las opciones de suplantación y las credenciales  
 Una conexión a un origen de datos puede utilizar a veces la autenticación de Windows o un servicio de autenticación proporcionado por el Sistema de administración de bases de datos, como la autenticación de SQL Server al conectarse a bases de datos de SQL Azure. La cuenta que especifique debe tener un inicio de sesión en el servidor de base de datos remota y permisos de lectura en la base de datos externa.  
  
### Autenticación de Windows  
 Las conexiones que utilizan la autenticación de Windows se especifican en la pestaña **Información de suplantación** del Diseñador de origen de datos. Utilice esta pestaña para elegir la opción de suplantación que especifica la cuenta en la que se ejecuta [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] al conectarse al origen de datos externo. No todas las opciones se pueden usar en todos los escenarios. Para obtener más información sobre estas opciones y cuándo usarlas, vea [Establezca las opciones de suplantación &#40;SSAS - multidimensional&#41;](../../analysis-services/multidimensional-models/set-impersonation-options-ssas-multidimensional.md).  
  
### Autenticación de base de datos  
 Como alternativa a la autenticación de Windows, puede especificar una conexión que use un servicio de autenticación proporcionado por el sistema de administración de bases de datos. En algunos casos, se requiere usar la autenticación de base de datos. Algunos escenarios que requieren el uso de la autenticación de base de datos incluyen el uso de la autenticación de SQL Server para conectarse a una base de datos de Windows Azure SQL o el acceso a un origen de datos relacional que se ejecuta en otro sistema operativo o en un dominio que no sea de confianza.  
  
 En el caso de un origen de datos que use la autenticación de base de datos, el nombre de usuario y la contraseña de un inicio de sesión de base de datos se especifica en la cadena de conexión. Las credenciales se agregan a la cadena de conexión cuando se especifica un nombre de usuario y una contraseña en el Administrador de conexión la conexión a un origen de datos se configura en el modelo de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] . No olvide especificar una identidad que tenga permisos de lectura para los datos.  
  
 Al recuperar datos, la biblioteca cliente que realiza la conexión formula una solicitud de conexión que incluye las credenciales en la cadena de conexión. Las opciones de las credenciales de autenticación de Windows en la pestaña información de suplantación no se utilizan en la conexión, pero se pueden utilizar para otras operaciones, como recursos de acceso en el equipo local. Para obtener más información, vea [Establezca las opciones de suplantación &#40;SSAS - multidimensional&#41;](../../analysis-services/multidimensional-models/set-impersonation-options-ssas-multidimensional.md).  
  
 Después de guardar el objeto de origen de datos en el modelo, se cifran la cadena de conexión y la contraseña.  Por razones de seguridad, todos los seguimientos visibles de la contraseña se quitan de la cadena de conexión cuando la ve después en las herramientas, el script o el código.  
  
> [!NOTE]  
>  De manera predeterminada, [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] no guarda contraseñas con la cadena de conexión. Si no se guarda la contraseña, [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] le solicita que la escriba cuando es necesario. Si decide guardar la contraseña, esta se guarda en formato cifrado en la cadena de conexión de datos. [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] cifra la información de contraseña para los orígenes de datos mediante la clave de cifrado de la base de datos que contiene el origen de datos. Con la información de conexión cifrada, debe usar el Administrador de configuración de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para cambiar la cuenta de servicio de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] o la contraseña, ya que de lo contrario no se puede recuperar la información cifrada. Para más información, consulte [SQL Server Configuration Manager](../../relational-databases/sql-server-configuration-manager.md).  
  
### Definir la información de suplantación para los objetos de minería de datos  
 Las consultas de minería de datos se pueden ejecutar en el contexto de la cuenta de servicio de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] , pero también se pueden ejecutar en el contexto del usuario que envía la consulta o en el de un usuario especificado. El contexto en que se ejecute una consulta podría afectar a sus resultados. En las operaciones del tipo **OPENQUERY** de minería de datos, podría interesarle que la consulta de minería de datos se ejecutara en el contexto del usuario actual o de un usuario especificado (independientemente del usuario que ejecute la consulta) y no en el contexto de la cuenta de servicio. Así, la consulta se puede ejecutar con credenciales de seguridad limitadas. Si desea que [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] suplante al usuario actual o a un usuario especificado, seleccione las opciones **Utilizar un nombre de usuario y una contraseña específicos** o **Utilizar las credenciales del usuario actual** .  
  
##  <a name="bkmk_steps"></a> Crear un origen de datos con el Asistente para orígenes de datos  
  
1.  En [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)], abra el proyecto de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] o conéctese a la base de datos de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] en la que desea definir el origen de datos.  
  
2.  En el **Explorador de soluciones**, haga clic con el botón derecho en la carpeta **Orígenes de datos** y, después, haga clic en **Nuevo origen de datos** para iniciar el **Asistente para orígenes de datos**.  
  
3.  En la página **Seleccione cómo definir la conexión** , elija **Crear un origen de datos basado en una conexión nueva o existente** y, a continuación, haga clic en **Nueva** para abrir el **Administrador de conexiones**.  
  
     Las nuevas conexiones se crean en el Administrador de conexiones. En el Administrador de conexiones, se selecciona un proveedor y luego se especifican las propiedades de las cadenas de conexión que usa el proveedor para conectarse a los datos subyacentes. La información exacta necesaria depende del proveedor seleccionado, pero generalmente incluye un servidor o una instancia de servicio, la información para iniciar la sesión en el servidor o la instancia de servicio, un nombre de archivo o de base de datos y otras configuraciones específicas del proveedor. En el resto de este procedimiento, supondremos una conexión de base de datos de SQL Server.  
  
4.  Seleccione el proveedor [!INCLUDE[msCoName](../../includes/msconame-md.md)] .NET Framework o el proveedor OLE DB nativo que se va a usar para la conexión.  
  
     El proveedor predeterminado para una conexión nueva es el proveedor OLE DB nativo\\[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client. Este proveedor se usa para conectarse a una instancia del Motor de base de datos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] mediante OLE DB. Normalmente, para las conexiones con una base de datos relacional de SQL Server, el uso de OLE DB nativo\SQL Server Native Client 11.0 ofrece más velocidad que el uso de proveedores alternativos.  
  
     También puede elegir un proveedor diferente para acceder a otros orígenes de datos. Para obtener una lista de los proveedores y bases de datos relacionales compatibles con [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)], vea [Orígenes de datos admitidos &#40;SSAS - Multidimensionales&#41;](../../analysis-services/multidimensional-models/supported-data-sources-ssas-multidimensional.md).  
  
5.  Especifique la información solicitada por el proveedor seleccionado para conectar con el origen de datos subyacente. Si selecciona el proveedor **OLE DB nativo\SQL Server Native Client**, especifique la siguiente información:  
  
    1.  **Nombre del servidor** es el nombre de red de la instancia del motor de base de datos. Se puede especificar como la dirección IP, el nombre NETBIOS del equipo o un nombre de dominio completo. Si se ha instalado el servidor como una instancia con nombre, se debe incluir el nombre de la instancia (por ejemplo, \<nombreDeEquipo>\\<nombreDeInstancia\>).  
  
    2.  **Iniciar sesión en el servidor** especifica cómo se autenticará la conexión. **Usar la autenticación de Windows** usa la autenticación de Windows. **Usar autenticación de SQL Server** especifica un inicio de sesión de usuario de base de datos para una instancia de SQL Server o bases de datos de Windows Azure SQL que admiten la autenticación de modo mixto.  
  
        > [!IMPORTANT]  
        >  El Administrador de conexiones incluye una casilla **Guardar mi contraseña** para las conexiones que utilizan la autenticación de SQL Server. Aunque la casilla está siempre visible, no se utiliza siempre.  
        >   
        >  Entre las condiciones en las que Analysis Services no usa esta casilla se incluyen la actualización o el procesamiento de los datos relacionales de SQL Server que se usa en una base de datos de Analysis Services activa. Independientemente de si se activa o desactiva **Guardar mi contraseña**, Analysis Services siempre cifrará y guardará la contraseña. La contraseña se cifra y almacena en archivos de datos y archivos .abf. Este comportamiento se produce porque Analysis Services no admite el almacenamiento de contraseñas basado en sesiones en el servidor.  
        >   
        >  Este comportamiento solo se aplica a las bases de datos que a) se guardan en una instancia de servidor de Analysis Services, y b) utilizan la autenticación de SQL Server para actualizar o procesar los datos relacionales. No se aplica a las conexiones de origen de datos configuradas en [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] que se utilizan solo durante una sesión. Aunque no es posible quitar una contraseña que ya está almacenada, se pueden utilizar credenciales diferentes, o la autenticación de Windows, para sobrescribir la información de usuario almacenada actualmente en la base de datos.  
  
    3.  **Seleccione o escriba un nombre de base de datos** o **Adjunte un archivo de base de datos** se usan para especificar la base de datos.  
  
    4.  En el lado izquierdo del cuadro de diálogo, haga clic en **Todo** para ver las opciones adicionales de esta conexión, incluidas las predeterminadas para este proveedor.  
  
    5.  Cambie las opciones según lo adecuado para el entorno y haga clic en **Aceptar**.  
  
         La nueva conexión se muestra en el panel **Conexión de datos** de la página **Seleccione cómo definir la conexión** del Asistente para orígenes de datos.  
  
6.  Haga clic en **Siguiente**.  
  
7.  En la página **Información de suplantación**, especifique las credenciales de Windows o la identidad de usuario que Analysis Services usará al conectarse al origen de datos externo. Si usa la autenticación de base de datos, estas opciones no se tienen en cuenta para la conexión.  
  
     Las instrucciones para elegir una opción de suplantación varían en función del modo en que se use el origen de datos. Para las tareas de procesamiento, el servicio [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] se debe ejecutar en el contexto de seguridad de su cuenta de servicio o una cuenta de usuario especificada al conectar con el origen de datos.  
  
    -   **Utilizar un nombre de usuario y una contraseña de Windows específicos** para especificar un único conjunto de credenciales con los mínimos privilegios.  
  
    -   **Usar la cuenta de servicio** para procesar los datos con la identidad de servicio.  
  
     La cuenta que especifique debe tener permisos de lectura en el origen de datos.  
  
8.  Haga clic en **Siguiente**.  En **Finalización del asistente**, escriba un nombre del origen de datos o use el nombre predeterminado. El nombre predeterminado es el nombre de la base de datos especificada en la conexión. En el panel **Vista previa** se muestra la cadena de conexión de este nuevo origen de datos.  
  
9. Haga clic en **Finalizar**.  El nuevo origen de datos aparece en la carpeta **Orígenes de datos** del Explorador de soluciones.  
  
##  <a name="bkmk_connection"></a> Crear un origen de datos con una conexión existente  
 Al trabajar en un proyecto de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] , el origen de datos se puede basar en un origen de datos existente de la solución o en un proyecto de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] . El Asistente para orígenes de datos ofrece varias opciones para crear el objeto de origen de datos, como es usar una conexión existente en el mismo proyecto.  
  
-   Si crea un origen de datos basado en un origen de datos existente en la solución, puede definir un origen de datos que se sincronice con el existente. Al crear el proyecto con el nuevo origen de datos, se usa la configuración de origen de datos del origen de datos subyacente.  
  
-   Si crea un origen de datos basado en un proyecto de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] , puede hacer referencia a otro proyecto de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] de la solución en el proyecto actual. El nuevo origen de datos usa el proveedor MSOLAP con sus propiedades **Data Source** y **Initial Catalog** tomadas de las propiedades **TargetServer** y **TargetDatabase** del proyecto seleccionado. Esta característica resulta útil en soluciones donde se utilizan varios proyectos de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] para administrar las particiones remotas, ya que las bases de datos de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] de origen y de destino requieren orígenes de datos recíprocos para admitir el almacenamiento y el procesamiento de particiones remotas.  
  
 Si hace referencia a un objeto de origen de datos, puede editar el objeto únicamente en el objeto o proyecto al que se hace referencia. No es posible editar la información de conexión del objeto de origen de datos que contiene la referencia. Los cambios en la información de conexión del objeto o proyecto al que se hace referencia aparecen en el nuevo origen de datos cuando se crea. La información de la cadena de conexión que aparece en el archivo de origen de datos (.ds) del proyecto se sincroniza cuando se genera el proyecto o cuando se borra la referencia en el Diseñador de origen de datos.  
  
##  <a name="bkmk_ConnectionString"></a> Ver o modificar propiedades de conexión  
 La cadena de conexión se formula según las propiedades que seleccione en el Diseñador de orígenes de datos o en el Asistente para nuevos orígenes de datos. Puede ver la cadena de conexión y otras propiedades en [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)].  
  
 **Para modificar la cadena de conexión**  
  
1.  En [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)], haga doble clic en el objeto de origen de datos en el Explorador de soluciones.  
  
2.  Haga clic en **Editar**y en **Todo** , en el panel de navegación de la izquierda.  
  
3.  Aparece la cuadrícula de propiedades que muestra las propiedades disponibles del proveedor de datos que usa. Para obtener más información sobre estas propiedades, vea la documentación del producto del proveedor.  Para el cliente nativo de SQL Server, vea [Using Connection String Keywords with SQL Server Native Client](../../relational-databases/native-client/applications/using-connection-string-keywords-with-sql-server-native-client.md).  
  
 Si tiene varios objetos de origen de datos en la solución y prefiere mantener la cadena de conexión en un único lugar, puede configurar el origen de datos actual para que haga referencia a otro objeto de origen de datos.  
  
 Una *referencia de origen de datos* es una asociación con otro proyecto u origen de datos de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] de la misma solución. Las referencias proporcionan un medio de sincronizar los orígenes de datos entre los objetos de una solución. La información de la cadena de conexión se sincroniza siempre que se genera el proyecto. Para cambiar la cadena de conexión de un origen de datos que hace referencia a otro objeto, debe cambiar la cadena de conexión del objeto al que se hace referencia.  
  
 Puede quitar la referencia desactivando la casilla. Esto finalizará la sincronización entre los objetos y le permitirá cambiar la cadena de conexión en el origen de datos.  
  
##  <a name="bkmk_multipleDS"></a> Agregar varios orígenes de datos a un modelo  
 Puede crear más de un objeto de origen de datos para admitir conexiones a orígenes de datos adicionales. Cada origen de datos debe tener columnas que se puedan usar para crear relaciones.  
  
> [!NOTE]  
>  Si se han definido varios orígenes de datos y se necesitan datos de varios de ellos en una sola consulta, como en una dimensión de copo de nieve, debe definir un origen de datos que admita consultas remotas mediante **OpenRowset**. Normalmente, será un origen de datos de Microsoft SQL Server.  
  
 Algunos requisitos para usar varios orígenes de datos son los siguientes:  
  
-   Designe un origen de datos como origen de datos principal. El origen de datos principal es el que se usa para crear una vista del origen de datos.  
  
-   Un origen de datos principal debe admitir la función **OpenRowset** .  Para obtener más información sobre esta función en SQL Server, vea <xref:Microsoft.SqlServer.TransactSql.ScriptDom.TSqlTokenType.OpenRowSet>.  
  
 Use la siguiente solución para combinar los datos de varios orígenes de datos:  
  
1.  Cree los orígenes de datos en su modelo.  
  
2.  Cree una vista del origen de datos usando una base de datos relacional de SQL Server como origen de datos. Este es su origen de datos principal.  
  
3.  En el Diseñador de vistas del origen de datos, usando la vista del origen de datos recién creada, haga clic con el botón derecho en cualquier lado del área de trabajo y seleccione **Agregar o quitar tablas**.  
  
4.  Elija el segundo origen de datos y después seleccione las tablas que desea agregar.  
  
5.  Busque la tabla que agregó y selecciónela. Haga clic con el botón derecho en la tabla y seleccione **Nueva relación**. Elija las columnas de origen y de destino que contienen los datos coincidentes.  
  
## Vea también  
 [Orígenes de datos admitidos &#40;SSAS - Multidimensionales&#41;](../../analysis-services/multidimensional-models/supported-data-sources-ssas-multidimensional.md)   
 [Vistas del origen de datos en modelos multidimensionales](../../analysis-services/multidimensional-models/data-source-views-in-multidimensional-models.md)  
  
  