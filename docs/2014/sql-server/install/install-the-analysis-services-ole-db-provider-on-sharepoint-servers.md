---
title: Instalar el Proveedor OLE DB de Analysis Services en servidores de SharePoint | Microsoft Docs
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
ms.assetid: 2c62daf9-1f2d-4508-a497-af62360ee859
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: 43049a9ae1230f25f3fd23800e489e247af60b74
ms.sourcegitcommit: a1adc6906ccc0a57d187e1ce35ab7a7a951ebff8
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/09/2019
ms.locfileid: "68890043"
---
# <a name="install-the-analysis-services-ole-db-provider-on-sharepoint-servers"></a>Instalar el proveedor OLE DB de Analysis Services en servidores de SharePoint
  El Proveedor Microsoft OLE DB para Analysis Services (MSOLAP) es una interfaz que las aplicaciones cliente emplean para interactuar con datos de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]. En un entorno de SharePoint que incluye [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)], el proveedor administra las solicitudes de conexión para datos [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)].  
  
 El proveedor de datos se incluye en el paquete de instalación de [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] (spPowerPivot.msi), pero puede requerir una instalación manual. Hay dos razones por las que puede necesitar instalar manualmente una biblioteca cliente o un proveedor de datos en un servidor de SharePoint.  
  
-   **Habilite la compatibilidad con versiones anteriores**. Los libros [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] especifican la versión de [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] del proveedor OLE DB de Analysis Services en su cadena de conexión. Por tanto, esta versión del proveedor debe estar presente en el equipo para que la solicitud se lleve a cabo correctamente.  
  
-   **Habilite el acceso a datos en una instancia de Excel Services dedicada**. Si la granja de SharePoint incluye Excel Services en un servidor que tampoco tiene [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)], instale la versión [!INCLUDE[ssSQL11SP1](../../includes/sssql11sp1-md.md)] del proveedor y otros componentes de conectividad de cliente mediante el paquete de instalación de [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)].  
  
    > [!NOTE]  
    >  Estos escenarios no se excluyen mutuamente. El hospedaje de varias versiones de libro en una granja que incluye servidores de aplicaciones que ejecutan Excel Services sin una instancia de [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] requerirá la instalación tanto de las versiones anteriores como las recientes del proveedor de datos en cada equipo con Excel Services.  
  
  
##  <a name="bkmk_vers"></a>Versiones del proveedor de OLE DB que admiten el acceso a datos PowerPivot  
 Una granja de servidores de SharePoint podría incluir varias versiones del proveedor OLE DB de Analysis Services, incluso las versiones anteriores que no admiten el acceso a datos PowerPivot.  
  
 De forma predeterminada, SharePoint 2010 instala la versión de [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] del proveedor. Aunque se identifica como MSOLAP.4 (el mismo número de versión que se usa para [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]), esta versión no funciona para el acceso a datos PowerPivot. Para que las conexiones tengan éxito, debe tener la versión de [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] o [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] del proveedor.  
  
 Una versión posterior de [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] del proveedor OLE DB incluye transportes y compatibilidad con conexiones para estructuras de datos de [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)]. Los libros [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] usan versiones más recientes de este proveedor para solicitar el procesamiento de consultas de los servidores [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] de la granja. Para obtener la versión actualizada, puede descargarla e instalarla a través de la página de SQL Server 2008 R2 Feature Pack.  
  
 En la tabla siguiente se describen las versiones válidas:  
  
|Versión del producto|Versión del archivo|Válido para:|  
|---------------------|------------------|----------------|  
|[!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]|MSOLAP100.dll en el sistema de archivos<br /><br /> MSOLAP.4 en una cadena de conexión de Excel<br /><br /> 10.50.1600 o posteriores en los detalles de la versión de archivo|Use los modelos de datos creados con la versión [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] de PowerPivot para Excel.|  
|[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]|MSOLAP110.dll en el sistema de archivos<br /><br /> MSOLAP.5 en una cadena de conexión de Excel<br /><br /> 11.0.0000 o posteriores en los detalles de la versión de archivo|Use los modelos de datos creados con la versión [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] o [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] de [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] para Excel.|  
|[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]|MSOLAP120.dll en el sistema de archivos<br /><br /> 12.0.20000 o posteriores en los detalles de la versión de archivo|Use modelos de datos que no sean modelos de [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)].|  
  
  
##  <a name="bkmk_why"></a>Por qué es necesario instalar el proveedor de OLE DB  
 Hay dos escenarios que requieren la instalación manual del proveedor OLE DB en los servidores de la granja.  
  
 **El escenario más común** es cuando tiene versiones anteriores y más recientes de [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] los libros que se guardan en las bibliotecas de documentos de la granja. Si los analistas de la organización usan la versión [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] de [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] para Excel y guardan esos libros en una instalación de [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)][!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)], el libro anterior no funcionará. Su cadena de conexión hará referencia a una versión anterior del proveedor, que no estará en el servidor a menos que lo instale. Al instalar ambas versiones se habilitará el acceso a los datos para los libros PowerPivot creados en las versiones anteriores y recientes de [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] para Excel. El programa de instalación de [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] no instala la versión [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] del proveedor, de modo que debe instalarla manualmente si usa libros de una versión anterior.  
  
 **El segundo escenario** es cuando se tiene un servidor en una granja de servidores de SharePoint que ejecuta Excel Services [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)], pero no. En este caso, el servidor de aplicaciones que ejecuta Excel Services debe actualizarse manualmente para utilizar una versión más reciente del proveedor. Esto es necesario para conectarse a una instancia de PowerPivot para SharePoint. Si Excel Services está usando una versión anterior del proveedor, la solicitud de conexión generará un error. Tenga en cuenta que el proveedor debe instalarse mediante el programa de instalación de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o el paquete de instalación de [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] (spPowerPivot.msi) para garantizar que se instalan todos los componentes necesarios para [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)].  
  
  
##  <a name="bkmk_sql11"></a>Instalar el proveedor de OLE DB de SQL Server 2012 en un servidor de Excel Services mediante el programa de instalación de SQL Server  
 Siga estas instrucciones para agregar el proveedor OLE DB y otros componentes de conectividad de cliente a los servidores de SharePoint que aún no los tengan instalados, como los servidores de aplicaciones que ejecutan Excel Services sin PowerPivot para SharePoint en el mismo hardware.  
  
 Siga estas instrucciones para instalar el proveedor de OLE DB de Analysis Services actual y para agregar **Microsoft. AnalysisServices. XMLA. dll** al ensamblado global.  
  
#### <a name="run-sql-server-setup-and-install-the-client-connectivity-tools"></a>Ejecutar el programa de instalación de SQL Server e instalar Conectividad con las herramientas de cliente  
  
1.  En el servidor de aplicaciones que hospeda Excel Services, ejecute el programa de instalación de SQL Server.  
  
2.  En la página instalación, elija **nuevo SQL Server instalación independiente o agregar características a una instalación existente**.  
  
3.  En la página tipo de instalación, seleccione **realizar una nueva instalación de SQL Server 2012**.  
  
4.  En la página rol de instalación, elija **SQL Server instalación de características**.  
  
5.  En la página **selección de características** , haga clic en conectividad con **las herramientas de cliente**. Esta opción instala **Microsoft. AnalysisServices. XMLA. dll**  
  
     No seleccione ninguna otra característica.  
  
6.  Haga clic en **siguiente** para finalizar el asistente y, a continuación, haga clic en **instalar** para ejecutar el programa de instalación.  
  
7.  Repita los pasos anteriores si tiene otros servidores que ejecutan Excel Services y PowerPivot para SharePoint no está instalado en el mismo servidor.  
  
#### <a name="verify-msolap5-is-a-trusted-provider"></a>Comprobar que MSOLAP.5 es un proveedor de confianza  
  
1.  En Administración central, haga clic en **Administrar aplicaciones de servicio**y haga clic en la aplicación de servicios de Excel Services.  
  
2.  Haga clic en **Proveedores de datos de confianza**.  
  
3.  Compruebe que MSOLAP.5 aparece en la lista. Según el modo en que configuró PowerPivot para SharePoint, MSOLAP.5 podría ya ser de confianza. Si usó la herramienta de configuración de PowerPivot, pero excluyó esta acción de la lista de tareas, MSOLAP.5 no será de confianza para Excel Services y ahora se debe agregar manualmente.  
  
4.  Si MSOLAP no aparece en la lista, haga clic en **Agregar proveedor de datos de confianza**.  
  
5.  En el identificador del proveedor, escriba `MSOLAP.5`.  
  
6.  En Tipo de proveedor, asegúrese de que está seleccionado OLE DB.  
  
7.  En Descripción del proveedor, escriba **Proveedor OLE DB de Microsoft para OLAP Services 11.0**.  
  
#### <a name="verify-installation"></a>Comprobar la instalación  
  
1.  Vaya a Archivos de programa\Microsoft Analysis Services\AS OLEDB\110.  
  
2.  Haga clic con el botón secundario en msolap110.dll y seleccione **Propiedades**.  
  
3.  Haga clic en **Detalles**.  
  
4.  Vea la información de la versión del archivo. La versión debe incluir 11,00. \<BuildNumber >.  
  
5.  En la carpeta Windows\Assembly, compruebe que Microsoft.AnalysisServices.Xmla.dll, versión 11.0.0.0, aparece en la lista.  
  
  
##  <a name="bkmk_install2012_from_sppowerpivot_msi"></a>Use el paquete de instalación de PowerPivot para SharePoint (spPowerPivot. msi) para instalar el proveedor de OLE DB de SQL Server 2012  
 Instale el [!INCLUDE[ssSQL11SP1](../../includes/sssql11sp1-md.md)] proveedor de OLE DB en y el servidor de Excel Services [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] mediante el paquete de instalación de **(spPowerPivot. msi)** .  
  
#### <a name="download-the-msolap5-provider-from-the-includesssql11sp1includessssql11sp1-mdmd-feature-pack"></a>Descargue el proveedor MSOLAP.5 desde [!INCLUDE[ssSQL11SP1](../../includes/sssql11sp1-md.md)] Feature Pack.  
  
1.  Vaya al [Feature Pack de Microsoft® SQL Server® 2012 SP1](https://www.microsoft.com/download/details.aspx?id=35580)  
  
2.  Haga clic en **instrucciones de instalación**.  
  
3.  Vea la sección "Proveedor OLE DB de Microsoft Analysis Services para Microsoft SQL Server 2012 SP1". Descargue el archivo e inicie la instalación.  
  
4.  En la página **selección de características** , seleccione **proveedor OLE DB de Analysis Services para SQL Server**. Anule la selección de los demás componentes y complete la instalación. Para obtener más información sobre spPowerPivot. msi, vea [instalar o desinstalar el complemento PowerPivot para SharePoint de &#40;SharePoint 2013&#41;](https://docs.microsoft.com/analysis-services/instances/install-windows/install-or-uninstall-the-power-pivot-for-sharepoint-add-in-sharepoint-2013).  
  
5.  Registre MSOLAP.5 como proveedor de confianza con Servicios de Excel de SharePoint. Para obtener más información, vea [Agregar MSOLAP.5 como proveedor de datos de confianza en Excel Services](https://technet.microsoft.com/library/hh758436.aspx).  
  
  
##  <a name="bkmk_kj"></a>Instalar el proveedor de OLE DB de SQL Server 2008 R2 para hospedar libros de versiones anteriores  
 Use las siguientes instrucciones para instalar la versión de [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] del proveedor MSOLAP.4 y registrar el archivo Microsoft.AnalysisServices.ChannelTransport.dll. ChannelTransport es un subcomponente del proveedor OLE DB de Analysis Services. La versión de [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] del proveedor lee el Registro al usar ChannelTransport para establecer una conexión. El registro de este archivo es un paso posterior a la instalación que solo se requiere para las conexiones administradas por el proveedor de [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] en un servidor de [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)].  
  
#### <a name="step-1-download-and-install-the-client-library"></a>Paso 1: Descargar e instalar la biblioteca de cliente  
  
1.  En la [página SQL Server 2008 R2 Feature Pack](https://go.microsoft.com/fwlink/?LinkId=159570), busque proveedor OLE DB de Microsoft Analysis Services para Microsoft SQL Server 2008 R2.  
  
2.  Descargue el paquete x64 del programa de instalación de `SQLServer2008_ASOLEDB10.msi`. Aunque el nombre de archivo contiene SQLServer2008, es el archivo correcto para la versión de SQL Server 2008 R2 del proveedor.  
  
3.  En el equipo que tiene una instalación de [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)], ejecute el archivo .msi para instalar la biblioteca.  
  
4.  Si tiene otros servidores en la granja que solo ejecutan Excel Services, sin [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] en el mismo servidor, repita los pasos anteriores para instalar la versión 2008 R2 del proveedor en el equipo de Excel Services.  
  
#### <a name="step-2-register-the-microsoftanalysisserviceschanneltransportdll-file"></a>Paso 2: Registrar el archivo Microsoft. AnalysisServices. ChannelTransport. dll  
  
1.  Use la herramienta regasm.exe para registrar el archivo. Si no ha ejecutado Regasm. exe antes, agregue su carpeta principal, C:\Windows\Microsoft.NET\Framework64\v4.0.30319\\, a la variable de ruta de acceso del sistema.  
  
2.  Abra un símbolo del sistema con permisos de administrador.  
  
3.  Vaya a esta carpeta: C:\Windows\assembly\GAC_MSIL\Microsoft.AnalysisServices.ChannelTransport\10.0.0.0__89845dcd8080cc91  
  
4.  Escriba el comando siguiente: `regasm microsoft.analysisservices.channeltransport.dll`  
  
5.  Repita los pasos anteriores para cualquier equipo en el que instaló manualmente la versión 2008 R2 del proveedor.  
  
#### <a name="verify-installation"></a>Comprobar la instalación  
  
1.  Ahora debe poder segmentar o filtrar los libros [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]. Si se produce un error, compruebe que usó la versión de 64 bits de regasm.exe para registrar el archivo.  
  
2.  Además, puede comprobar la versión del archivo.  
  
     Vaya a `C:\Program files\Microsoft Analysis Services\AS OLEDB\10`. Haga clic con el botón secundario en **msolap100. dll** y seleccione **propiedades**. Haga clic en **Detalles**.  
  
     Vea la información de la versión del archivo. La versión debe incluir 10,50. \<BuildNumber >.  
  
  
## <a name="see-also"></a>Vea también  
 [Instalación de PowerPivot para SharePoint 2010](../../../2014/sql-server/install/powerpivot-for-sharepoint-2010-installation.md)  
  
  
