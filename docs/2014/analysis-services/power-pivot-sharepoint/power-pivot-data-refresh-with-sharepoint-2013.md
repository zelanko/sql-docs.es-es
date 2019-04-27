---
title: Actualización de datos PowerPivot con SharePoint 2013 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
ms.assetid: 34f03407-2ec4-4554-b16b-bc9a6c161815
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 04c366bc668fe09d1ebf57d169587ec11476f707
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "62749713"
---
# <a name="powerpivot-data-refresh-with-sharepoint-2013"></a>Actualización de datos PowerPivot con SharePoint 2013
  El diseño de la actualización de modelos de datos de [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] de SharePoint 2013 emplea Excel Services como componente principal para cargar y actualizar modelos de datos en una instancia de [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] que se ejecuta en modo de SharePoint. El servidor de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] ejecuta fuera de la granja de servidores de SharePoint.  
  
 La arquitectura usada anteriormente para la actualización de datos se basaba exclusivamente en el servicio de sistema de PowerPivot para cargar y actualizar modelos de datos en una instancia de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] en modo de SharePoint. La instancia de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] se ejecutaba localmente en el servidor de aplicaciones de PowerPivot. La nueva arquitectura presenta también un nuevo método para mantener la información de programación como metadatos datos del elemento de libro en la biblioteca de documentos. La arquitectura de SharePoint 2013 Excel Services admite tanto la **actualización de datos interactiva** como la **actualización de datos programada**.  
  
 **[!INCLUDE[applies](../../includes/applies-md.md)]**  SharePoint 2013  
  
 **En este tema:**  
  
-   [Interactive Data Refresh](#bkmk_interactive_refresh)  
  
-   [Autenticación de Windows con conexiones de datos de libro y actualización de datos interactiva](#bkmk_windows_auth_interactive_data_refresh)  
  
-   [Scheduled Data Refresh](#bkmk_scheduled_refresh)  
  
-   [Arquitectura de actualización de datos programada de SharePoint 2013](#bkmk_refresh_architecture)  
  
-   [Otras consideraciones sobre la autenticación](#datarefresh_additional_authentication)  
  
-   [Más información](#bkmk_moreinformation)  
  
## <a name="background"></a>Información previa  
 SharePoint Server 2013 Excel Services administra la actualización de datos de los libros de Excel 2013 y desencadena el procesamiento del modelo de datos en un servidor [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] que se ejecuta en modo de SharePoint. Para los libros de Excel 2010, Excel Services también administra la carga y el almacenamiento de libros y modelos de datos. Sin embargo, Excel Services emplea el servicio de sistema de PowerPivot para enviar los comandos de procesamiento al modelo de datos. En la tabla siguiente se resumen los componentes que envían comandos de procesamiento para la actualización de datos según la versión del libro. Se supone que se usa un entorno de una granja de SharePoint 2013 configurada para usar un [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] Analysis Server en modo de SharePoint.  
  
||||  
|-|-|-|  
||Libros de Excel 2013|Libros de Excel 2010|  
|Desencadenar la actualización de datos|**Interactiva:** Usuario autenticado<br /><br /> **Programado:** Servicio de sistema de PowerPivot|Servicio de sistema de PowerPivot|  
|Cargar el libro desde las bases de datos de contenido|SharePoint 2013 Excel Services|SharePoint 2013 Excel Services|  
|Cargar modelo de datos en la instancia de Analysis Services|SharePoint 2013 Excel Services|SharePoint 2013 Excel Services|  
|Enviar comandos de procesamiento a la instancia de Analysis Services|SharePoint 2013 Excel Services|Servicio de sistema de PowerPivot|  
|Actualizar datos del libro|SharePoint 2013 Excel Services|SharePoint 2013 Excel Services|  
|Guardar el libro y el modelo de datos en la base de datos de contenido|**Interactiva:** N/D<br /><br /> **Programado:** SharePoint 2013 Excel Services|SharePoint 2013 Excel Services|  
  
 En la tabla siguiente se resumen las características de actualización admitidas en una granja de SharePoint 2013 configurada para usar un [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] Analysis Server en modo de SharePoint:  
  
|Libro creado en|actualización de datos programada|Actualización interactiva|  
|-------------------------|----------------------------|-------------------------|  
|2008 R2 PowerPivot para Excel|No compatible. Actualizar el libro **(\*)**|No compatible. Actualizar el libro **(\*)**|  
|2012 PowerPivot para Excel|Admitida|No compatible. Actualizar el libro **(\*)**|  
|Excel 2013|Admitida|Admitida|  
  
 **(\*)** Para obtener más información sobre actualizaciones de libros, vea [Actualizar libros y actualización de datos programada &#40;SharePoint 2013&#41;](../instances/install-windows/upgrade-workbooks-and-scheduled-data-refresh-sharepoint-2013.md).  
  
##  <a name="bkmk_interactive_refresh"></a> Interactive Data Refresh  
 La actualización de datos interactiva, o manual, de SharePoint Server 2013 Excel Services puede actualizar modelos de datos con datos del origen de datos original. La actualización de datos interactiva está disponible después de configurar una aplicación de Excel Services registrando un servidor de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] que se ejecuta en modo de SharePoint. Para obtener más información, vea [Administrar la configuración del modelo de datos de Servicios de Excel (SharePoint Server 2013)](https://technet.microsoft.com/library/jj219780.aspx).  
  
> [!NOTE]  
>  La actualización de datos interactiva solo está disponible para los libros creados en Excel 2013. Si se intenta actualizar un libro de Excel 2010, Excel Services mostrará un mensaje de error similar a "operación de PowerPivot con errores: El libro se creó con una versión anterior de Excel y PowerPivot no se puede actualizar hasta que se actualice el archivo". Para obtener más información sobre actualizaciones de libros, vea [Actualizar libros y actualización de datos programada &#40;SharePoint 2013&#41;](../instances/install-windows/upgrade-workbooks-and-scheduled-data-refresh-sharepoint-2013.md).  
  
 **Punto clave de interés de la actualización interactiva:**  
  
-   La actualización de datos interactiva solo actualiza los datos de la sesión de usuario actual. Los datos no se vuelven a guardar automáticamente en el elemento de libro en la base de datos de contenido de SharePoint.  
  
-   **Credenciales:** Actualización de datos interactiva puede usar la identidad del usuario que ha iniciado sesión como credenciales o credenciales almacenadas para conectarse al origen de datos. Las credenciales empleadas dependen de la configuración de autenticación de Excel Services definida para la conexión del libro al origen de datos externo.  
  
-   **Libros admitidos:**  Libros creados en Excel 2013.  
  
 **Para actualizar datos:**  
  
-   Vea la ilustración que hay a continuación de estos pasos.  
  
1.  En una biblioteca de documentos de SharePoint, abra un libro PowerPivot en el explorador.  
  
2.  En la ventana del explorador, haga clic en el menú **Datos** y, a continuación, haga clic en **Actualizar la conexión seleccionada** o en **Actualizar todas las conexiones**.  
  
3.  Excel Services carga la base de datos de PowerPivot, la procesa y después la consulta para actualizar la caché de libros de Excel.  
  
4.  **Nota:** El libro actualizado no se guarda automáticamente en la biblioteca de documentos.  
  
 ![actualización de datos interactiva](../media/as-interactive-datarefresh-sharepoint2013.gif "actualización de datos interactiva")  
  
###  <a name="bkmk_windows_auth_interactive_data_refresh"></a> Autenticación de Windows con conexiones de datos de libro y actualización de datos interactiva  
 Excel Services envía al servidor de Analysis Services un comando de proceso que indica al servidor que debe suplantar una cuenta de usuario. Para obtener derechos del sistema suficientes para realizar el proceso de suplantación-delegación de usuario, la cuenta de servicio de Analysis Services necesita el privilegio **Actuar como parte del sistema operativo** en el servidor local. El servidor de Analysis Services también debe poder delegar las credenciales del usuario a orígenes de datos. El resultado de la consulta se envía a Excel Services.  
  
 Experiencia de usuario típica: Cuando un cliente selecciona "Actualizar todas las conexiones" en un libro de Excel 2013 que contiene un modelo de PowerPivot, verán un mensaje de error similar al siguiente:  
  
-   **No se pudo actualizar los datos externos:** Se produjo un error mientras se trabajaba con el modelo de datos en el libro. Inténtelo de nuevo. No se pueden actualizar una o más conexiones de datos del libro.  
  
 Según el proveedor de datos que esté usando, verá mensajes similares a los siguientes en el registro de ULS.  
  
 **Con SQL Native Client:**  
  
-   No se pudo crear una conexión externa ni ejecutar una consulta. Mensaje del proveedor: Objeto fuera de línea 'DataSource', que hace referencia a los identificadores ' 20102481-39 8-4 d 21-bf63-68f583ad22bb', se ha especificado, pero no se ha usado.  Error de OLE DB u ODBC: Se produjo un error relacionado con la red o específico de la instancia al establecer una conexión a SQL Server. El servidor no se encuentra o no está accesible. Compruebe si el nombre de la instancia es correcto y si SQL Server está configurado para permitir conexiones remotas. Para obtener más información, consulte Libros en pantalla de SQL Server.; 08001; Proveedor de SSL: El paquete de seguridad solicitado no existe; 08001; Cliente no puede establecer conexión; 08001; Cifrado no admitido en el cliente.; 08001.  , ConnectionName: ThisWorkbookDataModel, libro: book1.xlsx.  
  
 **Con el proveedor Microsoft OLE DB para SQL Server:**  
  
-   No se pudo crear una conexión externa ni ejecutar una consulta. Mensaje del proveedor: Objeto fuera de línea 'DataSource', que hace referencia a los identificadores '6e711bfa-b62f-4879-a177-c5dd61d9c242', se ha especificado, pero no se ha usado. Error de OLE DB u ODBC. , ConnectionName: ThisWorkbookDataModel, libro: OLEDB Provider.xlsx.  
  
 **Con el proveedor de datos de .NET Framework para SQL Server:**  
  
-   No se pudo crear una conexión externa ni ejecutar una consulta. Mensaje del proveedor: Fuera de línea 'DataSource', que hace referencia a los identificadores 'f5fb916c-3eac - 4D 07-a542-531524c0d44a', del objeto se ha especificado, pero no se ha usado.  Errores del motor relacional de alto nivel. Se produjo la excepción siguiente mientras se estaba usando la interfaz administrada IDbConnection: No se pudo cargar el archivo o ensamblado ' System.Transactions, Version = 4.0.0.0, Culture = neutral, PublicKeyToken = b77a5c561934e089' o uno de sus dependencias. No se ha proporcionado el nivel de representación necesario o el nivel de representación no es válido. (Excepción de HRESULT: 0x80070542).  , ConnectionName: ThisWorkbookDataModel, libro: NETProvider.xlsx.  
  
 **Resumen de pasos de configuración** Para configurar el privilegio **Actuar como parte del sistema operativo** en el servidor local:  
  
1.  En el servidor de Analysis Services que se ejecuta en modo de SharePoint, agregue la cuenta de servicio de Analysis Services al privilegio "**Actuar como parte del sistema operativo**":  
  
    1.  Ejecute "`secpol.msc`"  
  
    2.  Haga clic sucesivamente en **Directiva de seguridad local**, **Directivas locales**y **Asignación de derechos de usuario**.  
  
    3.  Agregue la cuenta de servicio.  
  
2.  Reinicie Excel Services y rearranque el servidor de Analysis Services.  
  
3.  No es necesaria la delegación desde la cuenta de servicio de Excel Services o desde el servicio de notificaciones de token de Windows (C2WTS) a la instancia de Analysis Services. Por tanto, no se necesita ninguna configuración para KCD desde Excel Services o C2WTS en el servicio PowerPivot AS. Si el origen de datos backend está en el mismo servidor que la instancia [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] , no se necesita la delegación restringida de Kerberos. Sin embargo, la cuenta de servicio [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] requiere el derecho para actuar como parte del sistema operativo.  
  
 ![as_interactive_data_refresh2012SP1_windowsauth](../media/as-interactive-data-refresh2012sp1-windowsauth.gif "as_interactive_data_refresh2012SP1_windowsauth")  
  
 Para obtener más información, consulte [actuar como parte del sistema operativo](https://technet.microsoft.com/library/cc784323\(WS.10\).aspx).  
  
##  <a name="bkmk_scheduled_refresh"></a> Scheduled Data Refresh  
 **Puntos clave de interés de la actualización de datos programada:**  
  
-   Necesita la implementación del complemento PowerPivot para SharePoint. Para obtener más información, consulte [instalar o desinstalar PowerPivot para SharePoint Add-in &#40;SharePoint 2013&#41;](../instances/install-windows/install-or-uninstall-the-power-pivot-for-sharepoint-add-in-sharepoint-2013.md).  
  
-   Un usuario configura una programación de actualización para un libro. En el momento programado, el servicio de sistema de PowerPivot envía una solicitud a Excel Services para:  
  
    -   Cargar y procesar la base de datos de PowerPivot.  
  
    -   Actualizar el libro.  
  
    -   Volver a guardar el libro en la base de datos de contenido.  
  
-   **Credenciales:** Use las credenciales almacenadas. No usa la identidad del usuario actual.  
  
-   **Libros admitidos:** Libros creados mediante el [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] complemento PowerPivot para Excel 2010 o con Excel 2013. No se admiten los libros creados en Excel 2010 con el complemento [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] PowerPivot. Actualice el libro como mínimo al formato de [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] PowerPivot. Para obtener más información sobre actualizaciones de libros, vea [Actualizar libros y actualización de datos programada &#40;SharePoint 2013&#41;](../instances/install-windows/upgrade-workbooks-and-scheduled-data-refresh-sharepoint-2013.md).  
  
 Para mostrar la página **Administrar actualización de datos** :  
  
-   Vea la ilustración que hay a continuación de estos pasos.  
  
1.  En una biblioteca de documentos de SharePoint, haga clic en el **menú Abrir** (**...**) para un libro PowerPivot.  
  
2.  Haga clic en el segundo **menú Abrir** y, a continuación, haga clic en **Administrar actualización de datos de PowerPivot**.  
  
3.  En la página **Administrar actualización de datos** , haga clic en **Habilitar** y configure la programación de actualización.  
  
4.  En el momento especificado, el servicio de sistema de PowerPivot envía una solicitud a Excel Services para:  
  
    -   Cargar y procesar el modelo de datos de PowerPivot.  
  
    -   Actualizar el libro.  
  
    -   Volver a guardar el libro en la base de datos de contenido.  
  
 ![menú contextual de la actualización de datos administrar](../media/as-manage-datarefresh-sharepoint2013.gif "administrar menú contextual de la actualización de datos")  
  
> [!TIP]  
>  Para obtener información sobre actualizar libros desde SharePoint online, consulte [actualizar libros de Excel con modelos de PowerPivot incrustados desde SharePoint Online (notas)](https://technet.microsoft.com/library/jj992650.aspx) (https://technet.microsoft.com/library/jj992650.aspx).  
  
##  <a name="bkmk_refresh_architecture"></a> Arquitectura de actualización de datos programada de SharePoint 2013  
 En la ilustración siguiente se resume la arquitectura de actualización de datos de SharePoint 2013 y SQL Server 2012 SP1.  
  
 ![arquitectura de actualización de datos de SQL Server 2012 SP1](../media/as-scheduled-data-refresh2012sp1-architecture.gif "arquitectura de actualización de datos de SQL Server 2012 SP1")  
  
||Descripción||  
|-|-----------------|-|  
|**(1)**|Motor de Analysis Services|Un servidor de [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)][!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] que se ejecuta en modo de SharePoint. El servidor se ejecuta fuera de la granja de servidores de SharePoint.|  
|**(2)**|Interfaz de usuario|La interfaz de usuario consta de dos páginas: una para definir la programación y la segunda para ver el historial de actualización. Las páginas no obtienen acceso directamente a las bases de datos de aplicación de servicio PowerPivot pero usan el servicio de sistema de PowerPivot para obtener acceso a las bases de datos.|  
|**(3)**|Servicio de sistema de PowerPivot|El servicio se instala al implementar el complemento PowerPivot para SharePoint. El servicio se emplea para lo siguiente:<br /><br /> Este servicio hospeda el motor de programación de actualización, que llama a las API de Excel Services para la actualización de datos de libros de Excel 2013. Para los libros de Excel 2010, el servicio realiza directamente el procesamiento del modelo de datos pero continúa usando Excel Services para cargar el modelo de datos y actualizar el libro.<br /><br /> Este servicio proporciona métodos para componentes como las páginas de la interfaz de usuario, para comunicarse con el servicio de sistema.<br /><br /> Administra las solicitudes de acceso externo a libros como origen de datos que se reciben del servicio Web PowerPivot.<br /><br /> Administración de solicitudes de actualización de datos programada para los trabajos del temporizador y las páginas de configuración. El servicio administra las solicitudes para leer datos dentro y fuera de la base de datos de aplicaciones de servicio y desencadena la actualización de datos con Excel Services.<br /><br /> Procesamiento de uso y trabajo de temporizador relacionado.|  
|**(4)**|Excel Calculation Services|Responsable de cargar los modelos de datos.|  
|**(5)**|Servicio de almacenamiento seguro|Si la configuración de autenticación en el libro está configurada para **usar cuenta de usuario autenticada** o **ninguno**, se utilizan las credenciales almacenadas en el identificador de aplicación de destino Store seguro para datos actualización. Para obtener más información, vea la sección [Otras consideraciones sobre la autenticación](#datarefresh_additional_authentication) en este tema.|  
|**(6)**|Trabajo de temporizador de actualización de datos de PowerPivot|Indica al servicio de sistema de PowerPivot que se conecte a Excel Services para actualizar los modelos de datos.|  
  
 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] necesita los proveedores de datos y las bibliotecas de cliente adecuados para que el servidor de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] en modo de SharePoint pueda obtener acceso a los orígenes de datos.  
  
> [!NOTE]  
>  Como el servicio de sistema de PowerPivot ya no carga ni guarda modelos de PowerPivot, la mayoría de los valores para los modelos de almacenamiento en caché de un servidor de aplicaciones no se aplican a una granja de SharePoint 2013.  
  
## <a name="data-refresh-log-data"></a>Datos de registro de actualización de datos  
 **Datos de uso:** Puede ver los datos de uso en el panel de administración de PowerPivot. Para ver los datos de uso:  
  
1.  En Administración central de SharePoint, haga clic en **Panel de administración de PowerPivot** en el grupo **Configuración de aplicación general** .  
  
2.  En la parte inferior del panel, vea el **actualización de datos: actividad reciente** y **actualización de datos: errores recientes**.  
  
3.  Para obtener más información sobre los datos de uso y cómo habilitarlos, vea [PowerPivot Management Dashboard and Usage Data](power-pivot-management-dashboard-and-usage-data.md).  
  
 **Datos de registro de diagnóstico:** Puede ver los datos de registro de diagnóstico de SharePoint relacionados con la actualización de datos. En primer lugar, compruebe el registro de diagnósticos del **Servicio PowerPivot** en la página **Supervisión** de Administración central de SharePoint. Es posible que deba aumentar el nivel de registro para el "evento menos crítico" al registro. Por ejemplo, establezca temporalmente el valor en **Detallado** y vuelva a ejecutar las operaciones de actualización de datos.  
  
 Las entradas del registro contienen:  
  
-   El **Área** de **Servicio PowerPivot**.  
  
-   La categoría de **Actualización de datos**.  
  
 Examine **Configurar registro de diagnósticos**. Para obtener más información, consulte [configurar y ver archivos de registro de SharePoint y el registro de diagnóstico &#40;PowerPivot para SharePoint&#41;](configure-and-view-sharepoint-and-diagnostic-logging.md).  
  
##  <a name="datarefresh_additional_authentication"></a> Otras consideraciones sobre la autenticación  
 Los valores del cuadro de diálogo **Configuración de autenticación de los Servicios de Excel** en Excel 2013 determinan la identidad de Windows que Excel Services y [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] emplean para la actualización de datos.  
  
-   **Usar la cuenta de usuario autenticada**: Excel Services realiza la actualización de datos con la identidad del usuario que ha iniciado sesión actualmente.  
  
-   **Usar una cuenta almacenada**: Presupone un identificador de aplicación de servicio Store seguro de SharePoint, que Excel Services usa para recuperar el nombre de usuario y contraseña para autenticar la autenticación de actualización de datos.  
  
-   **Ninguno**: Los servicios de Excel **cuenta de servicio desatendida** se utiliza. La cuenta de servicio se asocia a un proxy de almacenamiento seguro. Configure los valores de la página **Configuración de la aplicación de Excel Services** , en la sección **Datos externos** .  
  
 Para abrir el cuadro de diálogo de configuración de autenticación:  
  
1.  Haga clic en la pestaña **Datos** en Excel 2013.  
  
2.  Haga clic en **Conexiones** en la cinta de opciones.  
  
3.  En el cuadro de diálogo **Conexiones del libro**, seleccione la conexión y haga clic en **Propiedades**.  
  
4.  En el **las propiedades de conexión** cuadro de diálogo, haga clic en **definición**y, a continuación, haga clic en el **configuración de autenticación...**  botón.  
  
 ![excel services authentication settings](../media/as-authentication-settings-4-ecs-in-excel2013.gif "excel services authentication settings")  
  
 Para obtener más información sobre la autenticación de actualización de datos y el uso de credenciales, vea la entrada de blog [Actualizar datos PowerPivot en SharePoint 2013](https://blogs.msdn.com/b/analysisservices/archive/2012/12/21/refreshing-powerpivot-data-in-sharepoint-2013.aspx).  
  
##  <a name="bkmk_moreinformation"></a> Más información  
 [Solución de problemas de actualización de datos PowerPivot](https://social.technet.microsoft.com/wiki/contents/articles/3870.troubleshooting-powerpivot-data-refresh.aspx).  
  
 [Servicios de Excel en SharePoint 2013](https://www.enjoysharepoint.com/configure-excel-service-application-in-sharepoint-2013/). 
  
## <a name="see-also"></a>Vea también  
 [Actualizar libros y actualización de datos programada &#40;SharePoint 2013&#41;](../instances/install-windows/upgrade-workbooks-and-scheduled-data-refresh-sharepoint-2013.md)   
 [Instalación de PowerPivot para SharePoint 2013](../instances/install-windows/install-analysis-services-in-power-pivot-mode.md)  
  
  
