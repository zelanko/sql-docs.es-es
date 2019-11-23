---
title: Configuración inicial (PowerPivot para SharePoint) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
ms.assetid: 3a0ec2eb-017a-40db-b8d4-8aa8f4cdc146
author: maggiesMSFT
ms.author: maggies
manager: craigg
ms.openlocfilehash: ba58e81cb802f3debe1c481443751de1947c595e
ms.sourcegitcommit: f912c101d2939084c4ea2e9881eb98e1afa29dad
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 10/23/2019
ms.locfileid: "72798119"
---
# <a name="initial-configuration-powerpivot-for-sharepoint"></a>Configuración inicial (PowerPivot para SharePoint)
  Siga los pasos de este tema para configurar una instalación inicial de PowerPivot para SharePoint. La manera más fácil de configurar una instalación inicial es utilizar la herramienta de configuración de PowerPivot. Automatiza todos los pasos de configuración que se describen a continuación.  
  
 Como alternativa, si desea obtener más control sobre cómo se configura el servidor, puede utilizar Administración central y la información de este tema para realizar cada paso individualmente.  
  
 
  
## <a name="prerequisites"></a>Prerequisites  
 El servidor de SharePoint debe haberse instalado utilizando la opción de instalación Granja de servidores del programa de instalación de SharePoint. No se admite ningún servidor de SharePoint independiente que utilice una base de datos integrada. Para obtener más información, vea [instrucciones para usar las características de SQL Server BI en una granja de servidores de SharePoint 2010](../../../2014/sql-server/install/guidance-for-using-sql-server-bi-features-in-a-sharepoint-2010-farm.md).  
  
> [!IMPORTANT]  
>  SharePoint 2010 SP1 debe instalarse antes de configurar PowerPivot para SharePoint o una granja de servidores de SharePoint que use un servidor de bases de datos de [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]. Si no ha instalado todavía el Service Pack, hágalo ahora antes de empezar la configuración del servidor.  
  
 Debe instalarse PowerPivot para SharePoint. Como mínimo, debe implementarse la solución de granja. Use la herramienta de configuración de PowerPivot o el script de PowerShell para implementar la solución de granja. En este tema se proporcionan las instrucciones para este paso.  
  
 El equipo debe estar unido a un dominio. Las cuentas que especifique para los servicios deben ser cuentas de usuario de dominio. Como mínimo, necesitará una cuenta de dominio para la aplicación de servicio PowerPivot. Si está configurando servicios adicionales (como Excel Services), debe tener cuentas independientes para cada servicio que aprovisione.  
  
 Debe ser administrador de granja para agregar PowerPivot para SharePoint a la granja. Debe conocer la frase de contraseña para agregar servidores y aplicaciones a la granja.  
  
##  <a name="deploywsp"></a>Paso 1: implementar soluciones de PowerPivot  
 Hay dos soluciones que deben instalarse e implementarse: una solución de granja y una solución de aplicación web.  
  
### <a name="install-and-deploy-the-farm-solution"></a>Instalar e implementar la solución de granja de servidores
  
 En la versión anterior, el programa de instalación de SQL Server instalaba e implementaba la solución de granja. En esta versión, debe utilizar la herramienta de configuración de PowerPivot o el script de PowerShell para implementar la solución de granja. No puede utilizar Administración central para implementar la solución de granja. Este es el único paso en la configuración de PowerPivot para SharePoint que no se puede realizar en Administración central. Una vez implementada la solución de granja, puede usar Administración central y los pasos de este tema para configurar una instalación de PowerPivot para SharePoint.  
  
 En este paso, ejecute PowerShell para instalar e implementar la solución de granja. Para obtener más información, vea [configuración de PowerPivot mediante Windows PowerShell](https://docs.microsoft.com/analysis-services/power-pivot-sharepoint/power-pivot-configuration-using-windows-powershell).  
  
1.  Abra un shell de administración de SharePoint 2010 utilizando la opción **Ejecutar como administrador** .  
  
2.  Ejecute el primer cmdlet:  
  
    ```powershell
    Add-SPSolution -LiteralPath "C:\Program Files\Microsoft SQL Server\120\Tools\PowerPivotTools\ConfigurationTool\Resources\PowerPivotFarm.wsp"  
    ```  
  
     El cmdlet devuelve el nombre de la solución, su identificador de solución y Deployed=False. En el paso siguiente, implementará la solución.  
  
3.  Ejecute el segundo cmdlet para implementar la solución:  
  
    ```powershell
    Install-SPSolution -Identity PowerPivotFarm.wsp -GACDeployment -Force  
    ```  
  
### <a name="deploy-the-web-application-solution"></a>Implementación de la solución de aplicación Web
  
1.  Haga clic en el botón Inicio, seleccione **todos los programas**, seleccione **productos de Microsoft SharePoint 2010**y, a continuación, seleccione **Administración central de SharePoint 2010**.  
  
2.  En Administración central de SharePoint 2010, en Configuración del sistema, haga clic en **Administrar las soluciones de la granja**.  
  
     Debe ver dos paquetes de solución independientes: powerpivotfarm.wsp y powerpivotwebapp.wsp. La primera solución (powerpivotfarm.wsp) debe estar implementada. Una vez implementada, no es necesario implementarla de nuevo. La segunda solución (powerpivotwebapp.wsp) se implementa para Administración central, pero debe implementar esta solución manualmente para cada aplicación web de SharePoint que vaya a admitir el acceso a datos PowerPivot.  
  
3.  Haga clic en **powerpivotwebapp.wsp**.  
  
4.  Haga clic en **implementar solución.**  
  
5.  En **¿cómo implementar en?** , seleccione la aplicación Web de SharePoint a la que desea agregar compatibilidad con las características de PowerPivot.  
  
6.  Haga clic en **Aceptar**.  
  
7.  Repita el mismo proceso con las demás aplicaciones web de SharePoint que también admitirán el acceso a datos PowerPivot.  
  
##  <a name="Geneva"></a>Paso 2: iniciar los servicios en el servidor  
 Una implementación de PowerPivot para SharePoint requiere que la granja incluya los siguientes servicios: Excel Calculation Services, Servicio de almacenamiento seguro y Notificaciones del servicio de token de Windows.  
  
 Notificaciones del servicio de token de Windows es necesario para Excel Services y PowerPivot para SharePoint. Se utiliza para establecer conexiones con orígenes de datos externos utilizando la identidad de Windows del usuario de SharePoint actual. Este servicio se debe ejecutar en todos los servidores de SharePoint que tienen Excel Services o PowerPivot para SharePoint habilitado. Si el servicio aún no está iniciado, debe iniciarlo ahora para permitir que Excel Services reenvíe las solicitudes autenticadas al Servicio de sistema de PowerPivot.  
  
1.  En Administración central, en Configuración del sistema, haga clic en **Administrar servicios en el servidor**.  
  
2.  Inicie Notificaciones del servicio de token de Windows.  
  
3.  Inicie Excel Calculation Services.  
  
4.  Inicie Servicio de almacenamiento seguro.  
  
5.  Compruebe que se han iniciado SQL Server Analysis Services y el Servicio de sistema de SQL Server PowerPivot.  
  
##  <a name="createapp"></a>Paso 3: crear una aplicación de servicio PowerPivot  
 El próximo paso es crear una aplicación de servicio PowerPivot.  
  
1.  En Administración central, en Administración de aplicaciones, haga clic en **Administrar aplicaciones de servicio**.  
  
2.  En la cinta **Aplicaciones de servicio** , haga clic en **Nuevo**.  
  
3.  Seleccione **SQL Server aplicación de servicio PowerPivot**. Si no aparece en la lista, PowerPivot para SharePoint no está instalado o la solución no se implementó.  
  
4.  En la página **crear nueva aplicación de servicio PowerPivot** , escriba un nombre para la aplicación. El valor predeterminado es PowerPivotServiceApplication\<número >. Si va a crear varias aplicaciones de servicio PowerPivot, un nombre descriptivo ayudará a otros administradores a saber cómo se utiliza la aplicación.  
  
5.  En Grupo de aplicaciones, cree un nuevo grupo de aplicaciones y seleccione una cuenta de seguridad para él. Se requiere una cuenta de usuario de dominio.  
  
6.  En **servidor de base de datos**, elija un servidor de base de datos en el que crear la base de datos de aplicación de servicio. El valor predeterminado es la instancia del motor de base de datos de SQL Server que hospeda las bases de datos de configuración de la granja.  
  
7.  En **nombre**de la base de datos, el valor predeterminado es PowerPivotServiceApplication1_\<GUID >. El nombre predeterminado de la base de datos corresponde al de la aplicación de servicio. Si escribió un nombre de aplicación del servicio único, siga una convención de nomenclatura similar para el nombre de la base de datos, de modo que pueda administrarlos juntos.  
  
8.  En **Autenticación de bases de datos**, el valor predeterminado es Autenticación de Windows. Si elige **Autenticación de SQL**, consulte la guía del administrador de SharePoint para obtener información sobre cómo usar este tipo de autenticación en una implementación de SharePoint.  
  
9. Active la casilla de **Agregar el proxy para esta aplicación de servicio PowerPivot al grupo de proxy predeterminado.** De esta forma se agrega la conexión de la aplicación de servicio al grupo de conexiones de servicio predeterminado. Debe tener por lo menos una aplicación de servicio PowerPivot en el grupo de conexiones predeterminado.  
  
     Si ya aparece una aplicación de servicio PowerPivot en el grupo de conexiones predeterminado, no agregue una segunda aplicación de servicio a dicho grupo. En la configuración no se admite agregar dos aplicaciones de servicio del mismo tipo del grupo de conexiones predeterminado. Para obtener más información sobre cómo usar las aplicaciones de servicio adicionales en un grupo de conexiones, vea [conectar una aplicación de servicio PowerPivot a una aplicación Web de SharePoint en administración central](https://docs.microsoft.com/analysis-services/power-pivot-sharepoint/connect-power-pivot-service-app-to-sharepoint-web-app-in-ca).  
  
10. Haga clic en **Aceptar**. La aplicación de servicio aparecerá junto a otros servicios administrados en la lista de aplicaciones de servicio de la granja.  
  
##  <a name="ExcelServ"></a>Paso 4: habilitar Excel Services  
 PowerPivot para SharePoint requiere que Servicios de Excel admita el acceso a datos PowerPivot en la granja. Puede determinar si Servicios de Excel ya está habilitado confirmando si Aplicación de Servicios de Excel aparece en la lista de aplicaciones de servicio en Administración central. Si Servicios de Excel no aparece, siga estos pasos para habilitarlo en este momento.  
  
1.  En Administración central, en Administración de aplicaciones, haga clic en **Administrar aplicaciones de servicio**.  
  
2.  En la cinta de opciones de aplicaciones de servicio, en crear, haga clic en **nuevo**.  
  
3.  Seleccione **aplicación de servicios de Excel**.  
  
4.  En Crear nueva aplicación de los Servicios de Excel, especifique un nombre (por ejemplo, Aplicación de Servicios de Excel).  
  
5.  En Grupo de aplicaciones, seleccione Crear nuevo grupo de aplicaciones y dele un nombre descriptivo (por ejemplo, Grupo de aplicaciones de Excel Services).  
  
6.  En Configurable, seleccione una cuenta de usuario de dominio de Windows para esta identidad de grupo de aplicaciones.  
  
7.  Mantenga la casilla predeterminada que agrega el proxy de aplicación del servicio a la lista de conexiones de servicio predeterminada.  
  
8.  Haga clic en **Aceptar**.  
  
9. Haga clic en la aplicación de Servicios de Excel recién creada.  
  
10. Haga clic en **ubicaciones de archivos de confianza** y, en esta página, seleccione la ubicación de confianza. (Normalmente, se muestra como **http://** en la columna dirección). Para asegurarse de que tanto Excel Services como el servicio PowerPivot tienen acceso al libro, debe incluir SharePoint como una ubicación de confianza de Excel Services. El Servicio de sistema de PowerPivot no puede tener acceso a los libros que están almacenados fuera de una granja de servidores de SharePoint.  
  
11. En el área propiedades del libro, establezca **tamaño máximo del libro** en 50.  
  
12. En datos externos, establezca **permitir datos externos** en **bibliotecas de conexiones de datos de confianza e incrustadas**. Este valor se requiere para el acceso a datos PowerPivot en un libro.  
  
13. Desactive la casilla **advertir en la actualización de datos** para permitir imágenes de vista previa de hojas de cálculo individuales en la galería de PowerPivot. Si decide mantener la advertencia y la configuración del libro especifica que se actualice al abrirse, podría obtener una sola imagen de la vista previa de la advertencia en lugar de las páginas del libro.  
  
14. Haga clic en **Aceptar**.  
  
##  <a name="SSS"></a>Paso 5: habilitación de la Servicio de almacenamiento seguro y configuración de la actualización de datos  
 PowerPivot para SharePoint necesita el Servicio de almacenamiento seguro para almacenar las credenciales y la cuenta de ejecución desatendida para la actualización de datos. Puede determinar si el Servicio de almacenamiento seguro ya está habilitado confirmando si aparece en la lista de aplicaciones de servicio.  
  
> [!IMPORTANT]  
>  Si el Servicio de almacenamiento seguro está habilitado, todavía debería comprobar que se ha generado una clave maestra para él. Para obtener instrucciones, vea la Parte 2: generar la clave maestra en el siguiente procedimiento.  
  
 Si el Servicio de almacenamiento seguro no aparece, siga estos pasos para habilitarlo ahora. Si se habilita el almacenamiento seguro, los autores de libros y los propietarios de documentos pueden tener acceso a más opciones de conexión a orígenes de datos al programar actualizaciones de datos para los libros publicados.  
  
##### <a name="part-1-enable-secure-store-service"></a>Parte 1: habilitar el Servicio de almacenamiento seguro  
  
1.  En Administración central, en Administración de aplicaciones, haga clic en **Administrar aplicaciones de servicio**.  
  
2.  En la cinta de opciones de aplicaciones de servicio, en crear, haga clic en **nuevo**.  
  
3.  Seleccione **servicio de almacenamiento seguro**.  
  
4.  En la página **crear aplicación de almacenamiento seguro** , escriba un nombre para la aplicación.  
  
5.  En **base de datos**, especifique la instancia de SQL Server que hospedará la base de datos para esta aplicación de servicio. El valor predeterminado es la instancia del motor de base de datos de SQL Server que hospeda las bases de datos de configuración de la granja.  
  
6.  En **nombre**de la base de datos, escriba el nombre de la base de datos de aplicación de servicio. El valor predeterminado es Secure_Store_Service_DB_\<GUID >. El nombre predeterminado corresponde al de la aplicación de servicio. Si escribió un nombre de aplicación del servicio único, siga una convención de nomenclatura similar para el nombre de la base de datos, de modo que pueda administrarlos juntos.  
  
7.  En **Autenticación de bases de datos**, el valor predeterminado es Autenticación de Windows. Si elige Authentication SQL, consulte la guía de administrador de SharePoint para obtener información sobre cómo utilizar el tipo de autenticación en la granja.  
  
8.  En grupo de aplicaciones, seleccione **crear nuevo grupo de aplicaciones.** Especifique un nombre descriptivo que ayudará a otros administradores del servidor a identificar cómo se utiliza el grupo de aplicaciones.  
  
9. Seleccione una cuenta de seguridad para el grupo de aplicaciones. Especifique una cuenta administrada para utilizar una cuenta de usuario de dominio.  
  
10. Acepte los valores predeterminados restantes y, a continuación, haga clic en **Aceptar.** La aplicación de servicio aparecerá junto a otros servicios administrados en la lista de aplicaciones de servicio de la granja.  
  
##### <a name="part-2-generate-the-master-key"></a>Parte 2: generar la clave maestra  
  
1.  Haga clic en la aplicación Servicio de almacenamiento seguro en la lista.  
  
2.  En la cinta de opciones de aplicaciones de servicio, haga clic en **administrar**.  
  
3.  En administración de claves, haga clic en **generar nueva clave**.  
  
4.  Especifique y confirme una frase de contraseña. La frase de contraseña se utilizará para agregar más aplicaciones de servicio compartidas del almacén seguro.  
  
5.  Haga clic en **Aceptar**.  
  
##### <a name="part-3-configure-the-unattended-powerpivot-data-refresh-account"></a>Parte 3: configurar la cuenta de actualización de datos PowerPivot desatendida  
 A menudo se requiere crear una cuenta de actualización de datos desatendida para el acceso a datos PowerPivot y el acceso a datos externos durante la actualización de datos. Por ejemplo, si Kerberos no está habilitado, debe crear una cuenta desatendida que el servicio PowerPivot pueda utilizar para conectarse a los orígenes de datos externos.  
  
 Para obtener instrucciones sobre cómo crear la cuenta de actualización de datos PowerPivot desatendida u otras credenciales almacenadas que se utilizan en la actualización de datos, vea [configurar la &#40;cuenta de actualización&#41; de datos desatendida de PowerPivot PowerPivot para SharePoint](../../analysis-services/configure-unattended-data-refresh-account-powerpivot-sharepoint.md) y [configurar credenciales almacenadas para la actualización &#40;de datos PowerPivot&#41;PowerPivot para SharePoint](../../../2014/analysis-services/configure-stored-credentials-data-refresh-powerpivot-sharepoint.md).  
  
##  <a name="Usage"></a>Paso 6: habilitar la recopilación de datos de uso  
 PowerPivot para SharePoint utiliza la infraestructura de recopilación de datos de uso de SharePoint para recopilar información sobre el uso de PowerPivot en toda la granja. Aunque los datos de uso siempre forman parte de una instalación de SharePoint, puede que tenga que habilitarla para poder usarla. Para obtener instrucciones, consulte [configurar la recopilación de &#40;datos de uso para PowerPivot para SharePoint](https://docs.microsoft.com/analysis-services/power-pivot-sharepoint/configure-usage-data-collection-for-power-pivot-for-sharepoint).  
  
##  <a name="Upload"></a>Paso 7: aumentar el tamaño máximo de carga para las aplicaciones Web de SharePoint y Excel Services  
 Dado que los libros PowerPivot pueden ser grandes, quizá desee aumentar el tamaño de archivo máximo. Hay dos valores de tamaño de archivo que puede configurar: el tamaño máximo de carga para la aplicación web y el tamaño de libro máximo en Servicios de Excel. El tamaño máximo de archivo debe estar establecido en el mismo valor en ambas aplicaciones. Para obtener instrucciones, vea [configurar el tamaño &#40;máximo de&#41;carga de archivos PowerPivot para SharePoint](https://docs.microsoft.com/analysis-services/power-pivot-sharepoint/configure-maximum-file-upload-size-power-pivot-for-sharepoint).  
  
##  <a name="activatePP"></a>Paso 8: activar la integración de características de PowerPivot para colecciones de sitios  
 La activación de características en el nivel de colección de sitios hace que las plantillas y las páginas de las aplicaciones estén disponibles para los sitios, incluidas las páginas de configuración para la actualización de datos programada y las páginas de aplicación para las bibliotecas de Galería de PowerPivot y de fuentes de distribución de datos.  
  
1.  En un sitio de SharePoint, haga clic en **Acciones de sitio**.  
  
     De forma predeterminada, se tiene acceso a las aplicaciones web de SharePoint a través del puerto 80. Esto significa que, a menudo, puede tener acceso a un sitio de SharePoint escribiendo http://\<nombre de equipo > para abrir la colección de sitios raíz.  
  
2.  Haga clic en **Configuración del sitio**.  
  
3.  En Administración de la colección de sitios, haga clic en **Características de la colección de sitios**.  
  
4.  Desplácese hacia abajo en la página hasta que encuentre la **característica de colección de sitios de integración de PowerPivot**.  
  
5.  Haga clic en **Activar**.  
  
6.  Repita este procedimiento con las demás colecciones de sitios abriendo cada sitio y haciendo clic en **Acciones de sitio**.  
  
 Para obtener más información, vea [activar la integración de características de PowerPivot para colecciones de sitios en administración central](https://docs.microsoft.com/analysis-services/power-pivot-sharepoint/activate-power-pivot-integration-for-site-collections-in-ca).  
  
##  <a name="bkmk_redist"></a>Paso 9: instalación de la versión SQL Server 2008 R2 del proveedor de OLE DB en una instancia de PowerPivot para SharePoint de SQL Server 2012  
 Si desea ejecutar versiones anteriores y más recientes de los libros PowerPivot en paralelo en el mismo servidor, debe instalar el proveedor OLE DB de Analysis Services que se distribuye con SQL Server 2008 R2 en un servidor de [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] PowerPivot para SharePoint.  
  
 Instalar el proveedor permitirá que los libros que hacen referencia a MSOLAP.4 en la cadena de conexión de datos funcionen según lo previsto en un servidor PowerPivot de [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]. La instalación del proveedor OLE DB de SQL Server 2008 R2 es un método alternativo para actualizar los libros creados en una versión anterior de PowerPivot para Excel.  
  
 Puede descargar el proveedor desde [SQL Server página del Feature Pack de 2008 R2](https://go.microsoft.com/fwlink/?LinkId=159570). Busque **microsoft® proveedor OLE DB de Analysis Services para microsoft® SQL Server® 2008 R2**y, a continuación, descargue el paquete x64 del programa de instalación de `SQLServer2008_ASOLEDB10.msi`.  
  
 Para obtener más información sobre cómo instalar el proveedor, incluidos los pasos de comprobación, vea [instalar el proveedor OLE DB de Analysis Services en servidores de SharePoint](../../../2014/sql-server/install/install-the-analysis-services-ole-db-provider-on-sharepoint-servers.md).  
  
##  <a name="verifyinstall"></a>Paso 10: comprobar la instalación  
 El procesamiento de consultas de PowerPivot en la granja tiene lugar cuando un usuario o una aplicación abren un libro de Excel que contiene datos PowerPivot. Como mínimo, puede consultar las páginas de sitios de SharePoint para comprobar que están disponibles las características de PowerPivot. Sin embargo, para comprobar una instalación por completo, debe tener un libro PowerPivot que pueda publicar en SharePoint y al que pueda tener acceso desde una biblioteca. Para realizar la prueba, puede publicar un libro de ejemplo que contenga datos PowerPivot y usarlo para confirmar que la integración de SharePoint está configurada correctamente.  
  
 Para comprobar la integración de PowerPivot con un sitio de SharePoint, haga lo siguiente:  
  
1.  En un explorador, abra la aplicación web que ha creado. Si ha usado los valores predeterminados, puede especificar http://\<el nombre del equipo > en la dirección URL.  
  
2.  Compruebe que el acceso a datos y las características de procesamiento de PowerPivot están disponibles en la aplicación. Para ello, compruebe la presencia de plantillas de biblioteca proporcionadas por PowerPivot:  
  
    1.  En acciones del sitio, haga clic en **más opciones..** .  
  
    2.  En bibliotecas, debería ver **biblioteca de fuentes** de distribución de datos y Galería de **PowerPivot**. La característica PowerPivot proporciona estas plantillas de biblioteca, que estarán visibles en la lista Bibliotecas si la característica está integrada correctamente.  
  
 Para comprobar el acceso a datos PowerPivot en el servidor, haga lo siguiente:  
  
1.  Cargue un libro PowerPivot en la Galería de PowerPivot o en cualquier biblioteca de SharePoint.  
  
2.  Haga clic en el documento para abrirlo desde la biblioteca.  
  
3.  Haga clic en una segmentación de datos o filtre los datos para iniciar una consulta de PowerPivot. El servidor cargará los datos PowerPivot en segundo plano y devolverá los resultados. En el paso siguiente, se conectará al servidor para comprobar que los datos se cargan y se almacenan en caché.  
  
4.  Inicie SQL Server Management Studio desde el grupo de programas de Microsoft SQL Server 2008 R2 en el menú Inicio. Si esta herramienta no está instalada en el servidor, puede pasar al último paso para confirmar la presencia de archivos almacenados en caché.  
  
5.  En Tipo de servidor, seleccione **Analysis Services**.  
  
6.  En nombre del servidor, escriba **\<nombre del servidor > \powerpivot**, donde **\<nombre del servidor >** es el nombre del equipo que tiene la instalación PowerPivot para SharePoint.  
  
7.  Haga clic en **Conectar**.  
  
8.  En Explorador de objetos, haga clic en **bases** de datos para ver la lista de archivos de datos PowerPivot que se cargan.  
  
9. En el sistema de archivos del equipo, compruebe la siguiente carpeta para determinar si hay archivos almacenados en la memoria caché del disco. La presencia de archivos almacenados en caché es una prueba más de que la implementación está operativa. Para ver la memoria caché de archivos, vaya a la carpeta \Archivos de programa\Microsoft SQL Server\MSAS10_50.POWERPIVOT\OLAP\Backup.  
  
##  <a name="nextsteps"></a>Pasos posteriores a la instalación  
 Después de comprobar la instalación, finalice la configuración del servicio creando una Galería de PowerPivot o ajustando la configuración individual. Para poder usar por completo los componentes del servidor recién instalados, puede descargar [!INCLUDE[ssGeminiClient](../../includes/ssgeminiclient-md.md)] para crear y, a continuación, publicar el primer libro PowerPivot.  
  
### <a name="install-data-providers-used-for-data-refresh"></a>Proveedores de instalación utilizados para la actualización de datos  
 Si habilitó la actualización de datos, el servidor necesitará los proveedores de datos para el acceso a datos externos que usó la aplicación cliente de PowerPivot para importar los datos originales (por ejemplo, si se importaron los datos originalmente mediante un proveedor de 32 bits, la actualización de datos de servidor también necesitará el proveedor de 32 bits cuando tenga acceso al mismo origen de datos externo). Para obtener más información, vea [actualización de datos PowerPivot con SharePoint 2010](../../../2014/analysis-services/powerpivot-data-refresh-with-sharepoint-2010.md).  
  
### <a name="install-adonet-data-services"></a>Instalar ADO.NET Data Services  
 Debe instalar ADO.NET Data Services 3.5 SP1 si desea exportar las listas de SharePoint como fuentes de distribución de datos. Para obtener instrucciones, vea [instalar ADO.NET Data Services para admitir las exportaciones de fuentes de distribución de datos de las listas de SharePoint](../../../2014/sql-server/install/install-ado-net-data-services-to-support-data-feed-exports-of-sharepoint-lists.md).  
  
### <a name="create-a-powerpivot-gallery"></a>Crear una Galería de PowerPivot  
 La Galería de PowerPivot es una biblioteca de opciones de vista previa y de presentación para ver los libros PowerPivot de un sitio de SharePoint. Se recomienda usar la Galería de PowerPivot para publicar y ver libros PowerPivot, por sus capacidades de vista previa. Además, si también implementa Reporting Services en el mismo servidor de SharePoint, un Galería de PowerPivot simplifica el uso de la creación de informes. Puede iniciar el Generador de informes desde la Galería de PowerPivot para crear un informe nuevo a partir de un libro PowerPivot publicado. Para obtener más información acerca de la creación y el uso de la biblioteca, vea [crear y personalizar la galería de PowerPivot](https://docs.microsoft.com/analysis-services/power-pivot-sharepoint/create-and-customize-power-pivot-gallery) y [usar la galería de PowerPivot](https://docs.microsoft.com/analysis-services/power-pivot-sharepoint/use-power-pivot-gallery).  
  
### <a name="create-additional-trusted-sites-in-excel-services"></a>Crear sitios de confianza adicionales en Excel Services  
 Puede agregar sitios de confianza en Excel Services para cambiar los permisos y la configuración de los sitios que proporcionan libros de Excel y datos PowerPivot. Para obtener más información, consulte [Create a trusted location for PowerPivot sites in Central Administration](https://docs.microsoft.com/analysis-services/power-pivot-sharepoint/create-a-trusted-location-for-power-pivot-sites-in-central-administration).  
  
### <a name="tune-configuration-settings"></a>Ajustar las opciones de configuración  
 Una aplicación de servicio PowerPivot se crea con propiedades y valores predeterminados. Las opciones de configuración de cada una de las aplicaciones de servicio se pueden modificar para cambiar la metodología mediante la que se asignan las solicitudes, establecer los tiempos de espera de servidor, cambiar los umbrales de los eventos de informe de respuesta de consulta, o especificar cuánto tiempo se conservan los datos de uso. Para obtener más información acerca de la configuración en administración central o sobre el uso de las características de PowerPivot en aplicaciones Web de SharePoint, vea [Administración y configuración de servidores de PowerPivot en administración central](https://docs.microsoft.com/analysis-services/power-pivot-sharepoint/power-pivot-server-administration-and-configuration-in-central-administration).  
  
### <a name="install-powerpivot-for-excel-and-build-a-powerpivot-workbook"></a>Instalar PowerPivot para Excel y generar un libro PowerPivot  
 Cuando tenga los componentes de servidor instalados en una granja, puede crear su primer libro de Excel 2010 con datos PowerPivot incrustado y, a continuación, publicarlo en una biblioteca de SharePoint en una aplicación web. Para poder generar libros de Excel con datos PowerPivot, debe empezar con una instalación de Excel 2010, seguida por el complemento PowerPivot para Excel que amplía Excel para que admita la importación y mejora de datos PowerPivot.  
  
### <a name="add-servers-or-applications"></a>Agregar servidores o aplicaciones  
 Al implementar la solución de PowerPivot, la integración de características se activa en el nivel de la colección de sitios para todas las colecciones de sitios en la aplicación web. A medida que crea nuevas aplicaciones web, debe implementar la solución powerpivotwebapp en cada una. Para obtener instrucciones, vea [implementar soluciones de PowerPivot en SharePoint](https://docs.microsoft.com/analysis-services/power-pivot-sharepoint/deploy-power-pivot-solutions-to-sharepoint).  
  
 Según cómo configure la aplicación de servicio PowerPivot, el Servicio de sistema de PowerPivot se agregará al grupo de conexiones predeterminado, haciendo que esté disponible para todas las aplicaciones web que utilizan las conexiones predeterminadas. Sin embargo, si configuró las aplicaciones web para utilizar listas personalizadas de conexiones de aplicaciones de servicio, tendrá que agregar la aplicación de servicio PowerPivot a cada aplicación web de SharePoint para la que desea habilitar el procesamiento de datos PowerPivot. Para obtener más información, vea [conectar una aplicación de servicio PowerPivot a una aplicación Web de SharePoint en administración central](https://docs.microsoft.com/analysis-services/power-pivot-sharepoint/connect-power-pivot-service-app-to-sharepoint-web-app-in-ca).  
  
 Con el tiempo, si decide que se necesitan mayores capacidades de almacenamiento y procesamiento de datos, puede agregar una segunda instancia de PowerPivot para SharePoint a la granja. El proceso de instalación es casi idéntico al usado para agregar el primer servidor, salvo los requisitos para especificar los nombres de instancia y la información de la cuenta de servicio. Para obtener instrucciones, consulte [lista de comprobación de implementación: escalado horizontal mediante la adición de servidores de PowerPivot a una granja de servidores de SharePoint 2010](../../../2014/sql-server/install/deployment-checklist-scale-out-adding-powerpivot-servers-sharepoint-2010-farm.md).  
  
## <a name="see-also"></a>Vea también  
 [Características admitidas por las ediciones de SQL Server 2014](../../../2014/getting-started/features-supported-by-the-editions-of-sql-server-2014.md)   
 [Configurar cuentas de servicio PowerPivot](https://docs.microsoft.com/analysis-services/power-pivot-sharepoint/configure-power-pivot-service-accounts)   
 [Crear y configurar una aplicación de servicio PowerPivot en Administración Central](https://docs.microsoft.com/analysis-services/power-pivot-sharepoint/create-and-configure-power-pivot-service-application-in-ca)   
 [Implementar soluciones de PowerPivot en SharePoint](https://docs.microsoft.com/analysis-services/power-pivot-sharepoint/deploy-power-pivot-solutions-to-sharepoint)   
 [Activar la integración de características de PowerPivot para colecciones de sitios en Administración Central](https://docs.microsoft.com/analysis-services/power-pivot-sharepoint/activate-power-pivot-integration-for-site-collections-in-ca)   
 [Instalación de PowerPivot para SharePoint 2010](../../../2014/sql-server/install/powerpivot-for-sharepoint-2010-installation.md)  
