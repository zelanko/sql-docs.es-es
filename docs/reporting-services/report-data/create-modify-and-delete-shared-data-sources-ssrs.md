---
title: "Crear, modificar y eliminar orígenes de datos compartidos (SSRS) | Documentos de Microsoft"
ms.custom: 
ms.date: 03/17/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- modifying data source properties
- shared data sources [Reporting Services]
- removing shared data sources
- roles [Reporting Services], shared data sources
- data sources [Reporting Services], shared
- data sources [Reporting Services], modifying properties
- deleting shared data sources
ms.assetid: 1e58c1c2-5ecf-4ce6-9d04-0a8acfba17be
caps.latest.revision: 53
author: guyinacube
ms.author: asaxton
manager: erikre
ms.translationtype: Machine Translation
ms.sourcegitcommit: 0eb007a5207ceb0b023952d5d9ef6d95986092ac
ms.openlocfilehash: 3d4025539369dcc955e8675a92def39e356cb86d
ms.contentlocale: es-es
ms.lasthandoff: 06/13/2017

---
# <a name="create-modify-and-delete-shared-data-sources-ssrs"></a>Crear, modificar y eliminar orígenes de datos compartidos (SSRS)
  Un origen de datos compartido es un conjunto de propiedades de conexión de un origen de datos a las que pueden hacer referencia varios informes, modelos y suscripciones controladas por datos que se ejecutan en un servidor de informes de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] .  Los orígenes de datos compartidos proporcionan una manera fácil de administrar las propiedades del origen de datos que, a menudo, cambian con el tiempo. Si una cuenta de usuario o una contraseña cambia, o si mueve la base de datos a otro servidor, puede actualizar la información de conexión en un único lugar.  
  
 El siguiente icono indica que existe un origen de datos compartido en la jerarquía de carpetas del Administrador de informes:  
  
 ![Shared data source icon](../../reporting-services/report-data/media/hlp-16datasource.png "Shared data source icon")  
Icono de origen de datos compartido  
  
 Los orígenes de datos compartidos son opcionales para los informes y para las suscripciones controladas por datos, pero obligatorios para los modelos de informe. Si tiene previsto usar modelos de informe para la notificación ad hoc, deberá crear y mantener un elemento de origen de datos compartido que proporcione información de conexión al modelo.  
  
 Un origen de datos compartido se compone de las partes siguientes:  
  
|Parte|Description|  
|----------|-----------------|  
|Nombre|Un nombre que identifica el origen dentro de la jerarquía de carpetas del servidor de informes.|  
|Description|Una descripción que aparece con el elemento en el Administrador de informes cuando el usuario ve el contenido de la carpeta.|  
|Tipo de conexión|La extensión de procesamiento de datos usada con el origen de datos. Solo puede usar extensiones de procesamiento de datos implementadas en el servidor de informes. Para más información sobre las extensiones de procesamiento de datos que se incluyen con [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)], vea [Orígenes de datos admitidos por Reporting Services &#40;SSRS&#41;](../../reporting-services/report-data/data-sources-supported-by-reporting-services-ssrs.md).|  
|Cadena de conexión|La cadena de conexión para la base de datos. Para más información y para consultar los ejemplos más usados de cadenas de conexión a orígenes, vea [Conexiones de datos, orígenes de datos y cadenas de conexión &#40;Generador de informes y SSRS&#41;](../../reporting-services/report-data/data-connections-data-sources-and-connection-strings-report-builder-and-ssrs.md).|  
|Tipo de credencial|Especifica cómo se obtienen las credenciales para la conexión y si se van a usar una vez establecida la conexión. Para más información, consulte [Specify Credential and Connection Information for Report Data Sources](../../reporting-services/report-data/specify-credential-and-connection-information-for-report-data-sources.md).|  
  
 El origen de datos compartido no contiene información de consulta utilizada para recuperar datos. La consulta siempre se conserva en la definición de informe.  
  
## <a name="creating-and-modifying-shared-data-sources"></a>Creación y modificación de origen de datos compartidos  
 Para crear un origen de datos compartido o modificar sus propiedades, debe tener permisos de tipo **Administrar orígenes de datos** en el servidor de informes. Si el servidor de informes se ejecuta en modo nativo, puede usar el Administrador de informes para crear y configurar el origen de datos compartido. Si el servidor de informes se ejecuta en el modo integrado de SharePoint, puede usar las páginas de aplicación de un sitio de SharePoint. Para cualquier servidor de informes, sea cual sea su modo, puede crear un origen de datos compartido en el Diseñador de informes y, a continuación, publicarlo en un servidor de destino.  
  
 Después de crear un origen de datos compartido en el servidor de informes, puede crear asignaciones de roles para controlar el acceso a él, moverlo a otra ubicación, cambiar su nombre o ponerlo en modo sin conexión para evitar el procesamiento de informes mientras se realizan operaciones de mantenimiento en el origen de datos externos. Si cambia de nombre o mueve un origen de datos compartido a otra ubicación en la jerarquía de carpetas del servidor de informes, la información de ruta de acceso en todos los informes o suscripciones que hagan referencia a él se actualiza en consecuencia. Si pone el origen de datos en modo sin conexión, todos los informes, modelos y suscripciones dejarán de ejecutarse hasta que vuelva a habilitar el origen de datos.  
  
 Para más información sobre cómo controlar el acceso a orígenes de datos compartidos en la jerarquía de carpetas del servidor de informes, vea [Proteger elementos de orígenes de datos compartidos](../../reporting-services/security/secure-shared-data-source-items.md).  
  
 **Para crear un origen de datos compartido en el Diseñador de informes**  
  
1.  En la barra de herramientas del panel Datos de informe, haga clic en **Nuevo** y, a continuación, haga clic en **Origen de datos**. Se abre el cuadro de diálogo **Propiedades del origen de datos** .  
  
    > [!NOTE]  
    >  Si el panel Datos de informe no es visible, haga clic en **Datos de informe** en el menú **Ver** .  
  
2.  En el cuadro de texto **Nombre** , escriba un nombre para el origen de datos o acepte el valor predeterminado. El nombre del origen de datos se utiliza internamente en el informe. Para evitar confusiones, se recomienda que el nombre del origen de datos contenga el nombre de la base de datos especificada en la cadena de conexión.  
  
3.  Compruebe que **Usar referencia de origen de datos compartido** está seleccionada y luego haga lo siguiente.  
  
    1.  Haga clic en **Nueva**. En el cuadro de diálogo de propiedades **Origen de datos compartido** , siga los pasos 2 y 3 para crear un nuevo origen de datos.  
  
    2.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
         El nuevo origen de datos compartido aparece en la carpeta Orígenes de datos compartidos del Explorador de soluciones.  
  
4.  Haga clic en Credenciales.  
  
     Especifique las credenciales que se deben usar para este origen de datos. El propietario del origen de datos elige el tipo de credenciales que se admiten.  
  
 **Para crear un origen de datos compartido en el Administrador de informes**  
  
1.  Inicie el [Administrador de informes &#40;Modo nativo de SSRS&#41;](http://msdn.microsoft.com/library/80949f9d-58f5-48e3-9342-9e9bf4e57896).  
  
2.  En el Administrador de informes, navegue hasta la página **Contenido** .  
  
3.  Haga clic en **Nuevo origen de datos**. Se abre la página **Nuevo origen de datos** .  
  
4.  Escriba el nombre del elemento. El nombre debe incluir al menos un carácter y debe empezar con una letra. También puede incluir determinados símbolos, pero no espacios en blanco o los caracteres ; ? : @ & = + , $ / * < > | " /.  
  
5.  Si lo desea, escriba una descripción que ofrezca a los usuarios información sobre la conexión. Esta descripción aparecerá en la página **Contenido** del Administrador de informes.  
  
6.  En la lista **Tipo de origen de datos** , especifique la extensión de procesamiento de datos que se utiliza para procesar datos desde el origen de datos.  
  
7.  En **Cadena de conexión**, especifique la cadena de conexión que utiliza el servidor de informes para conectarse al origen de datos. Se recomienda que no especifique credenciales en la cadena de conexión.  
  
     En el ejemplo siguiente, se muestra una cadena de conexión para establecer conexión con la base de datos [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] local:  
  
    ```  
    data source=<localservername>; initial catalog=AdventureWorks2012  
    ```  
  
8.  En **Conectar utilizando**, especifique cómo se obtienen las credenciales cuando se ejecuta el informe:  
  
    -   Si desea solicitar al usuario un nombre de inicio de sesión y una contraseña, haga clic en **Credenciales suministradas por el usuario que ejecuta el informe**. Para utilizar las credenciales que el usuario especifica como credenciales de Windows, active la casilla **Utilizar como credenciales de Windows para la conexión al origen de datos**. Si el nombre de usuario y la contraseña son las credenciales de la base de datos, no active esta opción.  
  
    -   Si va a usar el origen de datos para que se comparta con credenciales guardadas administradas por el propietario del origen de datos, o con informes que admitan suscripciones u otras operaciones programadas (por ejemplo, la generación automatizada de historiales de informes), haga clic en **Credenciales almacenadas de forma segura en el servidor de informes**. Si el servidor de bases de datos admite la suplantación o la delegación, puede seleccionar **Suplantar al usuario autenticado después de realizar una conexión al origen de datos**.  
  
    -   Si desea que el servidor de informes envíe las credenciales del usuario que tiene acceso al informe al servidor que hospeda el origen de datos externo, haga clic en **Seguridad integrada de Windows NT**. En este caso, no se solicita al usuario que escriba un nombre de usuario ni una contraseña.  
  
    -   Si el origen de datos no usa credenciales (por ejemplo, si el origen de datos es un archivo XML al que se tiene acceso desde el sistema de archivos), haga clic en **No se necesitan credenciales**. Solo debería especificar este tipo de credencial si es válido para el origen de datos. Si selecciona esta opción para un origen de datos que requiere autenticación, se producirá un error en la conexión. Si selecciona esta opción, asegúrese de que configura la cuenta de ejecución desatendida que permite al servidor de informes conectar a otros equipos para recuperar datos o archivos cuando las credenciales del usuario no están disponibles.  
  
         Para más información sobre la configuración de credenciales, vea [Especificar información de credenciales y conexión para los orígenes de datos de informes](../../reporting-services/report-data/specify-credential-and-connection-information-for-report-data-sources.md). Para más información sobre la cuenta de ejecución desatendida, vea [Configurar la cuenta de ejecución desatendida &#40;Administrador de configuración de SSRS&#41;](../../reporting-services/install-windows/configure-the-unattended-execution-account-ssrs-configuration-manager.md).  
  
9. Haga clic en el botón **Probar conexión** para validar la configuración del origen de datos.  
  
    > [!NOTE]  
    >  El botón Probar conexión no se admite para el tipo de origen de datos XML.  
  
10. Haga clic en **Aceptar**.  
  
 **Para modificar un origen de datos compartido en el Administrador de informes**  
  
1.  En el Administrador de informes, navegue a la página Contenido.  
  
2.  Navegue al elemento de orígenes de datos compartidos, mantenga el mouse sobre el elemento, haga clic en la lista desplegable y seleccione **Administrar**en el menú contextual. Se abre la página **Propiedades** .  
  
3.  Modifique el origen de datos y, a continuación, haga clic en **Aplicar**.  
  
## <a name="deleting-shared-data-sources"></a>eliminar orígenes de datos compartidos  
 Puede eliminar un origen de datos compartido de la misma manera que eliminaría cualquier elemento del servidor de informes.  
  
 **Para eliminar un origen de datos compartido**  
  
1.  En el Administrador de informes, navegue a la página **Contenido** y realice una de las siguientes acciones:  
  
    -   Navegue al elemento de origen de datos compartido.  
  
         Haga clic en el elemento para abrirlo. Se abre la página de propiedades General.  
  
         Haga clic en **Eliminar**y, después, en **Aceptar**.  
  
    -   En la página **Contenido** , navegue a la carpeta que contiene el origen de datos que desea eliminar.  
  
         Mantenga el mouse sobre el elemento, haga clic en la lista desplegable y seleccione **Eliminar**en el menú contextual.  
  
         [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
 Si elimina un origen de datos compartido, se desactivarán todos los informes, modelos y suscripciones controladas por datos que lo usan. Sin la información de conexión de un origen de datos, los elementos dejan de ejecutarse. Para activar estos elementos, deberá abrir cada uno de ellos y hacer lo siguiente:  
  
-   Para los informes y las suscripciones controladas por datos que hacen referencia al origen de datos compartido, puede especificar información de conexión del origen de datos en las propiedades de informe o de suscripción, o puede seleccionar un nuevo origen de datos compartido que tenga los valores que desea usar.  
  
-   Para los modelos e informes del Generador de informes que usan ese modelo, debe especificar un nuevo origen de datos compartido. Los modelos solo obtienen información de conexión de un origen de datos a través de orígenes de datos compartidos.  
  
 No hay ninguna operación de deshacer para eliminar un origen de datos compartido. Sin embargo, si elimina accidentalmente un origen de datos compartido, puede crear uno nuevo usando las mismas propiedades que las del origen eliminado. Tendrá que abrir cada uno de los informes, modelos y suscripciones controladas por datos para volver a enlazar el origen de datos compartido al elemento que lo usa, pero siempre y cuando las propiedades del origen de datos sean las mismas, los informes, modelos y suscripciones continuarán funcionando como antes.  
  
## <a name="importing-shared-data-sources"></a>Importación de orígenes de datos compartidos  
 **Para importar un origen de datos existente en el Diseñador de informes**  
  
1.  En el Explorador de soluciones, haga clic con el botón derecho en la carpeta **Orígenes de datos compartidos** del proyecto de servidor de informes y, después, haga clic en **Agregar elemento existente**. Se abrirá el cuadro de diálogo **Agregar elemento existente** .  
  
2.  Navegue a un archivo existente de origen de datos compartido de definición de informe (rds) y, después, haga clic en **Abrir**.  
  
3.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
## <a name="shared-data-sources-in-sharepoint"></a>Orígenes de datos compartidos en SharePoint  
 Al ejecutar un informe desde una biblioteca de SharePoint, la información de conexión puede definirse dentro del informe o en un archivo externo que esté vinculado al informe. Si la información de conexión está incrustada en el informe, se denomina origen de datos personalizado. Si la información de conexión se define en un archivo externo, se denomina origen de datos compartido. El archivo externo puede ser un archivo de origen de datos del servidor de informes (.rsds) o un archivo de conexión de datos de Office (.odc).  
  
 Un archivo .rsds es similar a un archivo .rds, pero tiene un esquema distinto. Para crear un archivo .rsds, puede publicar un archivo .rds del Diseñador de informes o del Diseñador de modelos en una biblioteca de SharePoint (se creará un nuevo archivo .rsds a partir del archivo .rds original). O bien, puede crear un nuevo archivo en una biblioteca de un sitio de SharePoint.  
  
 Después de crear o publicar un origen de datos compartido, podrá editar las propiedades de conexión o eliminar el archivo si deja de usarse. Antes de eliminar un origen de datos compartido, debe determinar si lo usan los informes y modelos de informe. Para ello, vea los elementos dependientes que hacen referencia al origen de datos compartido.  
  
 Aunque la lista de elementos dependientes le indica si se hace referencia al origen de datos compartido, no indica si el elemento se utiliza de forma activa. Para determinar si el origen de datos compartido o el modelo se usa de manera activa, puede consultar los archivos de registro del equipo del servidor de informes. Si no tiene acceso a los archivos de registro o si éstos no contienen la información deseada, considere la posibilidad de mover el informe a una capeta inaccesible mientras determina su estado actual.  
  
 **Para crear un archivo de origen de datos compartido (.rsds) (SharePoint 2010)**  
  
1.  Haga clic en la pestaña **Documentos** de la cinta de bibliotecas.  
  
2.  En el menú **Nuevo documento** , haga clic en **Origen de datos de informe**.  
  
    > [!NOTE]  
    >  Si no ve el elemento **Origen de datos de informe** en el menú, significa que no se ha habilitado el tipo de contenido del origen de datos de informe. Para obtener más información, vea [Add Reporting Services Content Types to a SharePoint Library (Agregar los tipos de contenido de Reporting Services a una biblioteca de SharePoint)](../../reporting-services/report-server-sharepoint/add-reporting-services-content-types-to-a-sharepoint-library.md).  
  
3.  En **Nombre**, escriba un nombre descriptivo para el archivo .rsds.  
  
4.  En **Tipo de origen de datos**, seleccione en la lista el tipo de origen de datos. Para más información, vea [Orígenes de datos admitidos por Reporting Services &#40;SSRS&#41;](../../reporting-services/report-data/data-sources-supported-by-reporting-services-ssrs.md).  
  
5.  En **Cadena de conexión**, especifique un puntero al origen de datos y cualquier otra opción de configuración necesaria para establecer una conexión al origen de datos externo. El tipo de origen de datos que esté utilizando determinará la sintaxis de la cadena de conexión. Para más información y consultar algunos ejemplos, vea [Conexiones de datos, orígenes de datos y cadenas de conexión &#40;Generador de informes y SSRS&#41;](../../reporting-services/report-data/data-connections-data-sources-and-connection-strings-report-builder-and-ssrs.md).  
  
6.  En **Credenciales**, especifique el modo en que el servidor de informes debe obtener las credenciales para obtener acceso al origen de datos externo. Las credenciales pueden almacenarse, solicitarse, integrarse o configurarse para el procesamiento de informes en modo desatendido.  
  
    -   Seleccione **Autenticación de Windows (integrada)** si quiere acceder a los datos con las credenciales del usuario que ha abierto el informe. No seleccione esta opción si el sitio o la granja de servidores de SharePoint usa la autenticación de formularios o se conecta al servidor de informes a través de una cuenta de confianza. No seleccione esta opción si desea programar el procesamiento de suscripciones o datos para este informe. Esta opción funciona de manera óptima cuando la autenticación Kerberos está habilitada para el dominio o cuando el origen de datos se encuentra en el mismo equipo que el servidor de informes. Si la autenticación Kerberos no está habilitada, las credenciales de Windows solo se pueden pasar a otro equipo. Esto significa que si el origen de datos externo es otro equipo, que requiere una conexión adicional, obtendrá un error en lugar de los datos esperados.  
  
    -   Seleccione **Pedir credenciales** si desea que el usuario especifique sus credenciales cada vez que ejecute el informe. No seleccione esta opción si desea programar el procesamiento de suscripciones o datos para este informe.  
  
    -   Seleccione **Credenciales almacenadas** si desea obtener acceso a los datos mediante un único conjunto de credenciales. Las credenciales se cifran antes de guardarse. Puede seleccionar opciones que determinan el modo en que se autentican las credenciales almacenadas. Seleccione Usar como credenciales de Windows si las credenciales almacenadas pertenecen a una cuenta de usuario de Windows. Seleccione **Establecer contexto de ejecución en esta cuenta** si desea establecer el contexto de ejecución en el servidor de base de datos. En el caso de las bases de datos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , esta opción establece la función SETUSER. Para más información, vea [SETUSER &#40;Transact-SQL&#41;](../../t-sql/statements/setuser-transact-sql.md).  
  
    -   Seleccione **No se necesitan credenciales** si quiere especificar credenciales en la cadena de conexión o si quiere ejecutar el informe con una cuenta con privilegios mínimos configurada en el servidor de informes. Si esta cuenta no está configurada en el servidor de informes, se solicitarán las credenciales a los usuarios y no se ejecutará ninguna de las operaciones programadas que defina para el informe.  
  
7.  Seleccione **Habilitar este origen de datos** si desea que el origen de datos esté activo. Si el origen de datos está configurado pero no activo, los usuarios recibirán un mensaje de error si intentan utilizar un informe basado en él.  
  
8.  Haga clic en el botón **Probar conexión** para validar la configuración del origen de datos.  
  
    > [!NOTE]  
    >  El botón Probar conexión no se admite para el tipo de origen de datos XML.  
  
9. Haga clic en **Aceptar** para crear el origen de datos compartido.  
  
 **Para eliminar un archivo de origen de datos compartido (.rsds)**  
  
1.  Abra la biblioteca que contiene el archivo .rsds.  
  
2.  Seleccione el origen de datos compartido.  
  
3.  Haga clic para que se muestre una flecha hacia abajo y haga clic en **Eliminar**.  
  
 Si elimina por error un origen de datos compartido que tenía intención de conservar, puede crear uno nuevo que contenga la misma información de conexión. Después de volver a crear el origen de datos compartido, debe abrir cada uno de los informes y modelos que usaba el origen de datos y seleccionar el origen de datos compartido. El nuevo elemento de origen de datos compartido puede tener un nombre, unas credenciales o una sintaxis de la cadena de conexión distintos de los del eliminado. Mientras la conexión se resuelva en el mismo origen de datos, las propiedades del origen de datos pueden variar con respecto a los valores originales.  
  
 Tenga cuidado al eliminar un modelo de informe. Si elimina un modelo, no podrá abrir ni modificar ningún informe basado en ese modelo en el Generador de informes. Si elimina accidentalmente un modelo utilizado por los informes existentes, deberá volver a generar el modelo, deberá volver a crear y guardar todos los informes que utilicen dicho modelo y deberá volver a especificar la seguridad de elementos de modelo que desee utilizar. No basta con volver a generar el modelo y luego adjuntarlo a un informe existente.  
  
## <a name="dependent-items"></a>Elementos dependientes  
 Si desea ver una lista de informes y modelos que usan el origen de datos, abra la página Elementos dependientes para el origen de datos compartido. Puede tener acceso a esta página al abrir el origen de datos en el Administrador de informes o en una página de aplicación de SharePoint. Observe que la página Elementos dependientes no muestra las suscripciones controladas por datos. Si una suscripción usa un origen de datos compartido, la suscripción no aparecerá en la lista de elementos dependientes.  
  
 **Para ver elementos dependientes en SharePoint**  
  
1.  Abra la biblioteca que contiene el archivo .rsds.  
  
2.  Seleccione el origen de datos compartido.  
  
3.  Haga clic para que se muestre una flecha hacia abajo y seleccione **Ver elementos dependientes**.  
  
     En el caso de los modelos de informe, la lista de elementos dependientes muestra los informes creados en el Generador de informes. En el caso de los orígenes de datos compartidos, la lista de elementos dependientes puede incluir tanto informes como modelos de informe.  
  
## <a name="see-also"></a>Vea también  
 [Crear y administrar orígenes de datos compartidos &#40;Reporting Services en el modo integrado de SharePoint&#41;](http://msdn.microsoft.com/library/2d3428e4-a810-4e66-a287-ff18e57fad76)   
 [Conexiones de datos, orígenes de datos y cadenas de conexión &#40;Generador de informes y SSRS&#41;](../../reporting-services/report-data/data-connections-data-sources-and-connection-strings-report-builder-and-ssrs.md)   
 [Administrar orígenes de datos de informe](../../reporting-services/report-data/manage-report-data-sources.md)   
 [Administrador de informes &#40;Modo nativo de SSRS&#41;](http://msdn.microsoft.com/library/80949f9d-58f5-48e3-9342-9e9bf4e57896)   
 [Conexiones de datos u orígenes de datos compartidos e incrustados &#40;Generador de informes y SSRS&#41;](http://msdn.microsoft.com/library/f417782c-b85a-4c4d-8a40-839176daba56)   
 [Orígenes de datos &#40;página de propiedades del Administrador de informes&#41;](http://msdn.microsoft.com/library/f37edda0-19e6-489e-b544-8751fa6b6cfb)   
 [Crear, eliminar o modificar un origen de datos compartido &#40;Administrador de informes&#41;](http://msdn.microsoft.com/library/cd7bace3-f8ec-4ee3-8a9f-2f217cdca9f2)   
 [Configurar propiedades de origen de datos para un informe &#40;Administrador de informes&#41;](../../reporting-services/report-data/configure-data-source-properties-for-a-report-report-manager.md)  
  
  

