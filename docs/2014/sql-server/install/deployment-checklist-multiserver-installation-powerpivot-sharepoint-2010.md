---
title: 'Lista de comprobación de la implementación: instalación en varios servidores de PowerPivot para SharePoint 2010 | Microsoft Docs'
ms.custom: ''
ms.date: 03/08/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
ms.assetid: 4380040a-1368-4a47-8930-47c65a192e59
author: maggiesMSFT
ms.author: maggies
manager: craigg
ms.openlocfilehash: ed0cd8bad3a99c7f1f59b5121aafb06ccdee63b2
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/27/2020
ms.locfileid: "71952242"
---
# <a name="deployment-checklist-multi-server-installation-of-powerpivot-for-sharepoint-2010"></a>Lista de comprobación de la implementación: instalación en varios servidores de PowerPivot para SharePoint 2010
  Esta lista de comprobación le guía por los pasos [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] necesarios para agregar para SharePoint a una granja de servidores de SharePoint 2010 de tres niveles que se crea desde el principio. Una granja de tres niveles cuenta con los niveles de base de datos, de aplicación y de web. Para [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] agregar a esta topología, es necesario ejecutar el programa de instalación [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] de SQL Server para instalar en la capa de aplicación. Los archivos de programa de PowerPivot se agregan al nivel Web, pero solo como una tarea posterior a la instalación cuando se implementa la solución de aplicación Web. Si bien existen pasos de implementación, no hay ningún paso de instalación independiente en los niveles web o de datos. El único paso de instalación que debe realizar es instalar [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] en los servidores de aplicaciones.  
  
||  
|-|  
|**[!INCLUDE[applies](../../includes/applies-md.md)]** SharePoint 2010|  
  
  
  
## <a name="prerequisites"></a>Prerrequisitos  
 Debe ser administrador local para instalar SQL Server y SharePoint 2010.  
  
 La persona que instale SharePoint también debe configurar la granja. Para configurar la granja, debe tener un inicio de sesión de SQL Server en el servidor de bases de datos. El inicio de sesión debe estar asignado a los siguientes roles: `dbcreator`, `securityadmin` y `public`.  
  
 Debe tener la edición Enterprise o Enterprise Evaluation de SharePoint Server 2010.  
  
 El equipo debe estar unido a un dominio.  
  
 Debe saber qué cuentas utilizará para ejecutar el motor de base de datos, los servicios de la granja de servidores y Analysis Services en modo integrado de SharePoint. Aunque puede cambiar estas cuentas posteriormente, durante la instalación tendrá que especificarlas por primera vez.  
  
 Las cuentas de servicio que especifique durante la instalación deberán ser cuentas de usuario de dominio.  
  
 Antes de comenzar la instalación, compruebe la configuración del explorador para comprobar que tiene una conexión a Internet. El instalador de requisitos previos abre una conexión de Internet para descargar el software necesario. Debe realizar las siguientes modificaciones para asegurarse de que obtiene todo el software necesario:  
  
-   En el Administrador del servidor, deshabilite temporalmente la configuración de seguridad mejorada de Internet Explorer para permitir descargas en el servidor. Con el objeto de descargar el software necesario, puede desactivar solo ESC de IE para Administradores.  
  
-   En Internet Explorer, podría tener que configurar el explorador para omitir un servidor proxy y así permitir el acceso del host local a URL de Internet.  
  
    1.  En Internet Explorer, en el menú Herramientas, haga clic en Opciones de Internet.  
  
    2.  En la pestaña Conexiones, en el área de configuración de Red de área local (LAN), haga clic en Configuración de LAN.  
  
    3.  En el área de configuración automática, desactive la casilla de detección automática de configuración.  
  
    4.  En el área de Servidor de proxy, active la casilla Usar un servidor proxy para la LAN.  
  
    5.  Escriba la dirección del servidor proxy en el cuadro Dirección.  
  
    6.  Escriba el número de puerto del servidor proxy en el cuadro Puerto.  
  
    7.  Active la casilla No usar servidor proxy para direcciones locales.  
  
    8.  Haga clic en Aceptar para cerrar el cuadro de diálogo de configuración de red de área local (LAN).  
  
    9. Haga clic en Aceptar para cerrar el cuadro de diálogo Opciones de Internet.  
  
##  <a name="install-a-database-server"></a><a name="installdb"></a>Instalar un servidor de base de datos  
 En este tema se supone que la topología de la granja de servidores se basa en la que se describe en el artículo [varios servidores para una granja de tres niveles](https://go.microsoft.com/fwlink/?LinkId=182771). Si ya tiene una granja de servidores operativa, vaya directamente a [instalar PowerPivot para SharePoint](#installppapp).  
  
 Si parte de la creación de la topología, comience instalando un motor de base de datos de SQL Server. Mediante estas instrucciones se crea un servidor de base de datos al que pueden tener acceso los servidores de SharePoint de la granja.  
  
1.  En el equipo que usa para el servidor de base de datos, ejecute SQL Server setup para instalar SQL Server Motor de base de datos (consulte Instalación [de SQL Server 2014 desde el Asistente para la instalación &#40;&#41;de instalación ](../../database-engine/install-windows/install-sql-server-from-the-installation-wizard-setup.md)).  
  
     Seleccione las siguientes características para que se instalen:  
  
    -   Servicios de Motor de base de datos  
  
    -   Conectividad con las herramientas de cliente  
  
    -   Herramientas de administración - Completas (las básicas se incluyen automáticamente)  
  
2.  Una vez instalado el motor de base de datos, habilite TCP/IP para las conexiones remotas y reinicie el servicio.  
  
    1.  Inicie el Administrador de configuración de SQL Server.  
  
    2.  Abra Configuración de red de SQL Server.  
  
    3.  Seleccione **Protocolos de MSSQLSERVER**.  
  
    4.  Haga clic con el botón derecho en **TCP/IP** y seleccione **Habilitar**.  
  
    5.  Haga clic en **SQL Server Services**.  
  
    6.  Haga clic con el botón secundario en **SQL Server (MSSQLSERVER)** y haga clic en **reiniciar**.  
  
3.  Habilite el acceso entrante al servidor de base de datos a través de Firewall de Windows. Así, los servidores de SharePoint de la granja se pueden conectar a las bases de datos SharePoint. Para obtener más información, consulte [configurar Firewall de Windows para permitir el acceso a SQL Server](../../../2014/sql-server/install/configure-the-windows-firewall-to-allow-sql-server-access.md).  
  
    1.  En el panel de control de Windows, en herramientas administrativas, haga clic en **firewall de Windows con seguridad avanzada**.  
  
    2.  Haga clic en **Reglas de entrada**.  
  
    3.  Haga clic en **nueva regla**.  
  
    4.  En tipo de regla, haga clic en **personalizado**.  
  
    5.  Haga clic en **Next**.  
  
    6.  En programa, en la sección servicios, haga clic en **personalizar**.  
  
    7.  Haga clic en **aplicar a este servicio**.  
  
    8.  Seleccione **SQL Server (MSSQLSERVER)** si instaló SQL Server como instancia predeterminada y, a continuación, haga clic en **Aceptar**.  
  
    9. Haga clic en **Next**.  
  
    10. En protocolo y puertos, acepte la configuración predeterminada y haga clic en **siguiente**.  
  
    11. En ámbito, acepte la configuración predeterminada y haga clic en **siguiente**.  
  
    12. En acción, acepte la configuración predeterminada y haga clic en **siguiente**.  
  
    13. En perfil, desactive las casillas de **privado** y **público**y, a continuación, haga clic en **siguiente**.  
  
    14. En nombre, escriba un nombre descriptivo para la regla de entrada (por ejemplo, **SQL Server**).  
  
    15. Haga clic en **Finalizar**.  
  
##  <a name="install-and-configure-a-three-tier-sharepoint-2010-farm"></a><a name="installsp"></a>Instalación y configuración de una granja de SharePoint 2010 de tres niveles  
 En cada uno de los equipos que utilice como servidores de SharePoint, ejecute el programa de instalación de requisitos previos de SharePoint y, a continuación, el Programa de instalación de SharePoint Server.  
  
 Use las instrucciones siguientes de la documentación de SharePoint 2010 para instalar y configurar una granja de SharePoint 2010 con dos servidores web y un servidor de aplicaciones:  
  
 [Varios servidores para una granja de tres niveles (SharePoint Server 2010)](https://go.microsoft.com/fwlink/?LinkId=182771)  
  
 Cuando se le pida que especifique un servidor de base de datos, especifique el servidor de base de datos que instaló anteriormente.  
  
 En los procedimientos que siguen, se supone que ha configurado la granja con las instrucciones proporcionadas para instalar la granja de tres niveles. La granja debería incluir los siguientes servicios y características:  
  
-   Excel Services, servicio de búsqueda y servicio de almacenamiento seguro  
  
-   Una aplicación web y una colección de sitios  
  
-   Recopilación de datos de uso y estado  
  
-   Registro de diagnóstico  
  
##  <a name="install-powerpivot-for-sharepoint-on-an-application-server"></a><a name="installppapp"></a>Instalación de PowerPivot para SharePoint en un servidor de aplicaciones  
 Ejecute el programa de instalación de SQL Server para agregar PowerPivot para SharePoint a una granja de servidores de SharePoint. Si la granja está compuesta por varios servidores de SharePoint, debe ejecutar el programa de instalación de SQL Server en un servidor de aplicaciones que ya forme parte de la granja.  
  
 Instale siempre PowerPivot para SharePoint en un servidor de aplicaciones. Aunque los servidores front-end web también ejecutarán los componentes de servidor de PowerPivot para SharePoint, los componentes que se ejecutan en el front-end web se instalan durante el paso de configuración de PowerPivot para SharePoint, al implementar las soluciones en la granja. Para obtener más información acerca del programa de instalación, consulte [instalación de PowerPivot para SharePoint 2010](../../../2014/sql-server/install/install-powerpivot-for-sharepoint-2010.md).  
  
 Si su topología de implementación reclama dos instancias de PowerPivot para SharePoint, ejecute el programa de instalación de SQL Server en cada servidor de aplicaciones. Solo puede tener una instancia de PowerPivot para SharePoint en un equipo. Si requiere varias instancias, debe utilizar servidores adicionales. Para obtener más información acerca de cómo agregar varios servidores PowerPivot para SharePoint a la misma granja, consulte [lista de comprobación de implementación: escalado horizontal mediante la adición de servidores de PowerPivot a una granja de servidores de SharePoint 2010](../../../2014/sql-server/install/deployment-checklist-scale-out-adding-powerpivot-servers-sharepoint-2010-farm.md).  
  
##  <a name="install-analysis-services-client-libraries-on-sharepoint-applications-servers-that-do-not-have-an-installation-of-powerpivot-for-sharepoint"></a><a name="installclientlib"></a>Instalar Analysis Services bibliotecas de cliente en servidores de aplicaciones de SharePoint que no tienen una instalación de PowerPivot para SharePoint  
 Una topología de granja que incluye un servidor de aplicaciones o web-front ejecutándose en las aplicaciones siguientes, sin una instalación de PowerPivot para SharePoint en el mismo equipo, requerirá software adicional para admitir las características y el acceso a datos PowerPivot:  
  
-   Excel Services o PerformancePoint Services  
  
-   Administración central, cuando se ejecuta como aplicación independiente en su propio servidor  
  
 Tanto Excel Services como PerformancePoint Services requieren una versión más reciente del proveedor OLE DB de Analysis Services para admitir el acceso a datos PowerPivot. Si ejecuta una aplicación en un equipo que no tiene el proveedor OLE DB más reciente, debe instalar el proveedor de modo manual. Para obtener más información, vea [instalar el proveedor OLE DB de Analysis Services en servidores de SharePoint](../../../2014/sql-server/install/install-the-analysis-services-ole-db-provider-on-sharepoint-servers.md) .  
  
 De igual modo, un equipo que tenga Administración central, sin PowerPivot para SharePoint en el mismo equipo, requerirá la biblioteca cliente ADOMD.NET. El panel de administración de PowerPivot usa esta biblioteca para tener acceso a los datos internos que se utilizan para rellenar el panel. Para obtener más información, vea [Instalar ADOMD.NET en servidores front-end web ejecutando Administración central](../../../2014/sql-server/install/install-adomd-net-on-web-front-end-servers-running-central-administration.md).  
  
##  <a name="configure-the-server"></a><a name="configsrvr"></a>Configurar el servidor  
 Use la herramienta de configuración de PowerPivot para configurar PowerPivot para SharePoint. La herramienta examinará la configuración existente de la granja y proporcionará opciones para instalar o activar las características de SharePoint necesarias para PowerPivot para SharePoint. Durante este paso, se iniciarán las Notificaciones al servicio de token de Windows. Además, si otras características de SharePoint necesarias no están habilitadas todavía, la herramienta de configuración las agregará a la lista e incluirá acciones para habilitarlas.  
  
 Para obtener más información, vea [configurar o reparar PowerPivot para SharePoint 2010 &#40;herramienta de configuración de PowerPivot&#41;](../../../2014/analysis-services/configure-repair-powerpivot-sharepoint-2010.md).  
  
##  <a name="configure-alternate-access-mapping-for-web-front-end-servers"></a><a name="AAM"></a>Configuración de la asignación de acceso alternativa para servidores front-end web  
 Para asegurarse de que cada servidor front-end web administra las solicitudes de acceso o actualización de datos PowerPivot, debe asignar las URL de cada servidor a la misma aplicación web.  
  
1.  En administración central, en administración de aplicaciones, haga clic en **configurar asignaciones de acceso alternativas**.  
  
2.  En la colección de asignaciones de acceso alternativas, seleccione su aplicación web.  
  
3.  Haga clic en **Agregar dirección URL interna**.  
  
4.  Especifique la URL del primer servidor front-end web.  
  
5.  Repita los pasos anteriores para agregar la dirección URL del segundo servidor front-end web.  
  
##  <a name="activate-powerpivot-feature-integration-for-site-collections"></a><a name="activatePP"></a>Activar la integración de características de PowerPivot para colecciones de sitios  
 La activación de características en el nivel de colección de sitios hace que las plantillas y las páginas de las aplicaciones estén disponibles para los sitios, incluidas las páginas de configuración para la actualización de datos programada y las páginas de aplicación para las bibliotecas de Galería de PowerPivot y de fuentes de distribución de datos.  
  
 La Herramienta de configuración de PowerPivot activará la integración de características para la colección de sitios que especifique. Puede ejecutar varias veces la herramienta para seleccionar colecciones de sitios adicionales. O bien, los administradores de sitio pueden configurar la activación de características desde dentro de SharePoint. Para obtener más información, vea [activar la integración de características de PowerPivot para colecciones de sitios en administración central](https://docs.microsoft.com/analysis-services/power-pivot-sharepoint/activate-power-pivot-integration-for-site-collections-in-ca).  
  
##  <a name="verify-integration-and-server-availability"></a><a name="verify"></a>Comprobar la integración y la disponibilidad del servidor  
 El procesamiento de consultas de PowerPivot en la granja tiene lugar cuando un usuario o una aplicación abren un libro de Excel que contiene datos PowerPivot. Como mínimo, puede consultar las páginas de sitios de SharePoint para comprobar que están disponibles las características de PowerPivot. Sin embargo, para comprobar una instalación por completo, debe tener un libro PowerPivot que pueda publicar en SharePoint y al que pueda tener acceso desde una biblioteca. Para realizar la prueba, puede publicar un libro de ejemplo que contenga datos PowerPivot y usarlo para confirmar que la integración de SharePoint está configurada correctamente.  
  
 Para comprobar la integración de PowerPivot con un sitio de SharePoint, haga lo siguiente:  
  
1.  En un explorador, abra la aplicación web que ha creado. Si ha usado los valores predeterminados, puede\<especificar http://el nombre del equipo> en la dirección URL.  
  
2.  Compruebe que el acceso a datos y las características de procesamiento de PowerPivot están disponibles en la aplicación. Para ello, compruebe la presencia de plantillas de biblioteca proporcionadas por PowerPivot:  
  
    1.  En acciones del sitio, haga clic en **más opciones..**.  
  
    2.  En bibliotecas, debería ver **biblioteca de fuentes** de distribución de datos y Galería de **PowerPivot**. La característica PowerPivot proporciona estas plantillas de biblioteca, que estarán visibles en la lista Bibliotecas si la característica está integrada correctamente.  
  
 Para comprobar el acceso a datos PowerPivot en el servidor, haga lo siguiente:  
  
1.  [Descargue](https://go.microsoft.com/fwlink/?LinkID=219108) el ejemplo de datos Picnic que acompaña a un tutorial de Reporting Services. Utilizará el libro de ejemplo de esta descarga para comprobar el acceso a datos PowerPivot. Extraiga los archivos.  
  
2.  Cargue un libro PowerPivot en la Galería de PowerPivot o en cualquier biblioteca de SharePoint.  
  
3.  Haga clic en el documento para abrirlo desde la biblioteca.  
  
4.  Haga clic en una segmentación de datos o filtre los datos para iniciar una consulta de PowerPivot. El servidor cargará los datos PowerPivot en segundo plano y devolverá los resultados. En el paso siguiente, se conectará al servidor para comprobar que los datos se cargan y se almacenan en caché.  
  
5.  Inicie SQL Server Management Studio desde el grupo de programas de Microsoft SQL Server 2008 R2 en el menú Inicio. Si esta herramienta no está instalada en el servidor, puede pasar al último paso para confirmar la presencia de archivos almacenados en caché.  
  
6.  En Tipo de servidor, seleccione **Analysis Services**.  
  
7.  En nombre del servidor, escriba ** \<el nombre del servidor> \powerpivot**, donde ** \<nombre** del servidor>es el nombre del equipo que tiene la PowerPivot para SharePoint instalación.  
  
8.  Haga clic en **Conectar**.  
  
9. En Explorador de objetos, haga clic en **bases** de datos para ver la lista de archivos de datos PowerPivot que se cargan.  
  
10. En el sistema de archivos del equipo, compruebe la siguiente carpeta para determinar si hay archivos almacenados en la memoria caché del disco. La presencia de archivos almacenados en caché es una prueba más de que la implementación está operativa. Para ver la memoria caché de archivos, vaya a la carpeta \Archivos de programa\Microsoft SQL Server\MSAS10_50.POWERPIVOT\OLAP\Backup.  
  
##  <a name="post-installation-steps"></a><a name="nextsteps"></a>Pasos posteriores a la instalación  
 Después de comprobar la instalación, finalice la configuración del servicio creando una Galería de PowerPivot o ajustando la configuración individual. Para poder usar por completo los componentes del servidor recién instalados, puede descargar [!INCLUDE[ssGeminiClient](../../includes/ssgeminiclient-md.md)] para crear y, a continuación, publicar el primer libro PowerPivot.  
  
####  <a name="set-upper-limits-on-disk-space-usage"></a><a name="bkmk_disk"></a>Establecer límites superiores en el uso del espacio en disco  
 Puede establecer un límite máximo en cuanto al espacio en disco que se usa para los archivos de datos PowerPivot almacenados en memoria caché en el disco. El valor predeterminado es usar todo el espacio de disco disponible. Para obtener instrucciones sobre cómo limitar el uso del espacio en disco, vea [configurar el uso del espacio en disco &#40;PowerPivot para SharePoint&#41;](https://docs.microsoft.com/analysis-services/power-pivot-sharepoint/configure-disk-space-usage-power-pivot-for-sharepoint).  
  
####  <a name="increase-file-maximum-upload-size-for-sharepoint-web-applications"></a><a name="Upload"></a>Aumentar el tamaño máximo de carga de archivo para las aplicaciones Web de SharePoint  
 Dado que los libros PowerPivot pueden ser grandes, quizá desee aumentar el tamaño de carga máxima de archivos. Hay dos valores de tamaño de archivo que puede configurar: el tamaño máximo de carga para la aplicación web y el tamaño de libro máximo en Servicios de Excel. El tamaño máximo de archivo debe estar establecido en el mismo valor en ambas aplicaciones. Para obtener instrucciones, vea [configurar el tamaño máximo de carga de archivos &#40;PowerPivot para SharePoint&#41;](https://docs.microsoft.com/analysis-services/power-pivot-sharepoint/configure-maximum-file-upload-size-power-pivot-for-sharepoint).  
  
#### <a name="grant-sharepoint-permissions-to-workbook-users"></a>Conceder permisos de SharePoint a los usuarios del libro  
 Los usuarios necesitarán permisos de SharePoint para poder publicar o ver los libros. Asegúrese de conceder permisos de **vista** a los usuarios que necesiten ver los libros publicados y **contribuir** a los usuarios que publican o administran libros. Debe ser administrador de la colección de sitios para conceder permisos.  
  
1.  En el sitio, haga clic en **acciones del sitio**.  
  
2.  Haga clic en **permisos del sitio**.  
  
3.  Active la casilla correspondiente al grupo **miembros** de la colección de sitios.  
  
4.  En la cinta de opciones, haga clic en **conceder permisos**.  
  
5.  Especifique las cuentas de usuario o grupo del dominio de Windows que deben tener permiso para agregar o quitar documentos.  
  
6.  Haga clic en **OK**.  
  
7.  Active la casilla correspondiente al grupo **visitantes** de la colección de sitios.  
  
8.  En la cinta de opciones, haga clic en **conceder permisos**.  
  
9. Especifique las cuentas de grupo o de usuario del dominio de Windows que deben tener permiso para ver documentos. En este caso, no use direcciones de correo electrónico ni grupos de distribución si la aplicación está configurada para la autenticación clásica.  
  
10. Haga clic en **OK**.  
  
#### <a name="install-adonet-data-services-35-sp1"></a>Instalar ADO.NET Data Services 3.5 SP1  
 ADO.NET Data Services se requiere para exportar fuentes de distribución de datos de las listas de SharePoint. SharePoint 2010 no incluye este componente en el programa PrerequisiteInstaller, de modo que debe instalarlo manualmente. Para obtener más información sobre cómo instalar ADO.NET Data Services, consulte [instalar ADO.NET Data Services para admitir las exportaciones de fuentes de distribución de datos de las listas de SharePoint](../../../2014/sql-server/install/install-ado-net-data-services-to-support-data-feed-exports-of-sharepoint-lists.md).  
  
#### <a name="install-data-providers-used-in-data-refresh-and-check-user-permissions"></a>Proveedores de datos de configuración utilizados en los permisos de actualización de datos y comprobación de usuario  
 La actualización de datos del lado servidor permite a los usuarios reimportar los datos actualizados en sus libros en modo desatendido. Para que la actualización de datos se realice correctamente, el servidor debe tener el mismo proveedor de datos que se usó para importar originalmente los datos. Además, la cuenta de usuario en la que se ejecuta la actualización de datos requiere a menudo permisos de lectura en los orígenes de datos externos. Asegúrese de comprobar los requisitos para habilitar y configurar la actualización de datos a fin de garantizar que el resultado es correcto. Para obtener más información, vea [actualización de datos PowerPivot con SharePoint 2010](../../../2014/analysis-services/powerpivot-data-refresh-with-sharepoint-2010.md).  
  
#### <a name="create-a-powerpivot-gallery"></a>Crear una Galería de PowerPivot  
 La Galería de PowerPivot es una biblioteca de opciones de vista previa y de presentación para ver los libros PowerPivot de un sitio de SharePoint. Se recomienda usar la Galería de PowerPivot para publicar y ver libros PowerPivot, por sus capacidades de vista previa. Además, si también implementa Reporting Services en el mismo servidor de SharePoint, un Galería de PowerPivot simplifica el uso de la creación de informes. Puede iniciar el Generador de informes desde la Galería de PowerPivot para crear un informe nuevo a partir de un libro PowerPivot publicado. Para obtener más información acerca de la creación y el uso de la biblioteca, vea [crear y personalizar la galería de PowerPivot](https://docs.microsoft.com/analysis-services/power-pivot-sharepoint/create-and-customize-power-pivot-gallery) y [usar la galería de PowerPivot](https://docs.microsoft.com/analysis-services/power-pivot-sharepoint/use-power-pivot-gallery).  
  
#### <a name="tune-configuration-settings"></a>Ajustar las opciones de configuración  
 Una aplicación de servicio PowerPivot se crea con propiedades y valores predeterminados. Las opciones de configuración de cada una de las aplicaciones de servicio se pueden modificar para cambiar la metodología mediante la que se asignan las solicitudes, establecer los tiempos de espera de servidor, cambiar los umbrales de los eventos de informe de respuesta de consulta, o especificar cuánto tiempo se conservan los datos de uso. Para obtener más información acerca de la configuración en administración central o sobre el uso de las características de PowerPivot en aplicaciones Web de SharePoint, vea [Administración y configuración de servidores de PowerPivot en administración central](https://docs.microsoft.com/analysis-services/power-pivot-sharepoint/power-pivot-server-administration-and-configuration-in-central-administration).  
  
## <a name="see-also"></a>Consulte también  
 [Características admitidas por las ediciones de SQL Server 2012](https://go.microsoft.com/fwlink/?linkid=232473)   
 [Instalación de PowerPivot para SharePoint 2010](../../../2014/sql-server/install/install-powerpivot-for-sharepoint-2010.md)   
 [Lista de comprobación de implementación: escalado horizontal agregando servidores de PowerPivot a una granja de servidores de SharePoint 2010](../../../2014/sql-server/install/deployment-checklist-scale-out-adding-powerpivot-servers-sharepoint-2010-farm.md)  
  
  
