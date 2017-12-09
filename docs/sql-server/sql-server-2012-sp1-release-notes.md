---
title: "Notas de la versión de SQL Server 2012 SP1 | Microsoft Docs"
ms.prod: sql-non-specified
ms.prod_service: sql-non-specified
ms.service: 
ms.component: sql-non-specified
ms.technology: server-general
ms.custom: 
ms.date: 01/31/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 72171357-28de-4edd-bdfd-194f97225a6f
caps.latest.revision: "49"
author: craigg-msft
ms.author: craigg
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: ac1dcd75aa97cb12142d142c82d5c0c6d3f59791
ms.sourcegitcommit: b2d8a2d95ffbb6f2f98692d7760cc5523151f99d
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 12/05/2017
---
# <a name="sql-server-2012-sp1-release-notes"></a>SQL Server 2012 SP1 Release Notes
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)] Este documento de notas de la versión describe problemas conocidos que es conveniente que conozca antes de instalar [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssSQL11](../includes/sssql11-md.md)] Service Pack 1 o solucionar sus problemas. Este documento de notas de la versión solo está disponible en línea, no en el disco de instalación, y se actualiza periódicamente.  
  
## <a name="bkmk_top"></a>Contenido  
[1.0 Antes de la instalación](#bmk_Install)  
  
[2.0 Analysis Services y PowerPivot](#bkmk_AS)  
  
[3.0 Reporting Services](#bkmk_RS)  
  
[4.0 Data Quality Services](#bkmk_DQS)  
  
[5.0 SQL Server Express](#bkmk_Express)  
  
[6.0 Servicio y diseñador de captura de datos modificados para Oracle de Attunity](#bkmk_CDC)  
  
[7.0 Marco de trabajo de la aplicación de capa de datos (DACFx) de SQL Server](#DACFx)  
  
[8.0 Problemas conocidos corregidos en este Service Pack](#bkmk_known_issues_fixed)  
  
## <a name="bmk_Install"></a>1.0 Antes de la instalación  
Antes de instalar SQL Server 2012 SP1, tenga en cuenta la siguiente información.  
  
### <a name="11-reinstalling-an-instance-of-sql-server-failover-custer-fails-if-you-use-the-same-ip-address"></a>1.1 Reinstalar una instancia de clúster de conmutación por error de SQL Server produce un error si utiliza la misma dirección IP  
**Problema:** si especifica una dirección IP incorrecta durante la instalación de una instancia de clúster de conmutación por error de SQL Server, la instalación produce errores. Después de desinstalar la instancia con errores, y si intenta reinstalar la instancia de clúster de conmutación por error de SQL Server con el mismo nombre de instancia, y la dirección IP correcta, la instalación produce errores. El error se debe al grupo de recursos duplicados que deja atrás la instalación anterior.  
  
**Solución alternativa:** para resolver este problema, utilice un nombre de instancia diferente durante la reinstalación, o elimine manualmente el grupo de recursos antes de reinstalar. Para obtener más información, vea [Agregar o quitar nodos en un clúster de conmutación por error de SQL Server](http://msdn.microsoft.com/library/ms191545).  
  
### <a name="12-choose-the-correct-file-to-download-and-install"></a>1.2 Elegir el archivo correcto para su descarga e instalación  
Use la tabla siguiente para determinar qué archivo va a descargar e instalar. Compruebe que cumple los requisitos del sistema correctos antes de instalar el Service Pack. Los requisitos del sistema se proporcionan en las páginas de descarga cuyos vínculos aparecen en la tabla.  
  
|Si la versión que tiene instalada actualmente es...|Y desea...|Descargue e instale...|  
|-------------------------------------------|----------------------|---------------------------|  
|**Instalaciones de&32; bits:**|||  
|Una versión de 32 bits de cualquier edición de SQL Server 2012|Actualizar a la versión de 32 bits de SQL Server 2012 SP1|SQLServer2012SP1-KB2674319-x86-ENU.exe desde [aquí](http://go.microsoft.com/fwlink/p/?LinkID=268158)|  
|Una versión de 32 bits de SQL Server 2012 RTM Express|Actualizar a la versión de 32 bits de SQL Server 2012 Express SP1|SQLServer2012SP1-KB2674319-x86-ENU.exe desde [aquí](http://go.microsoft.com/fwlink/p/?LinkID=268158)|  
|Una versión de 32 bits únicamente las herramientas de cliente y de administración para SQL Server 2012 (incluido SQL Server 2012 Management Studio)|Actualizar las herramientas de cliente y de administración a la versión de 32 bits de SQL Server 2012 SP1|SQLManagementStudio_x86_ENU.exe desde [aquí](http://go.microsoft.com/fwlink/p/?LinkID=267905)|  
|Una versión de 32 bits de SQL Server 2012 Management Studio Express|Actualizar a la versión de 32 bits de SQL Server 2012 SP1 Management Studio Express|SQLManagementStudio_x86_ENU.exe desde [aquí](http://go.microsoft.com/fwlink/p/?LinkID=267905)|  
|Una versión de 32 bits de cualquier edición de SQL Server 2012 **y** una versión de 32 bits de las herramientas de cliente y de administración (incluido SQL Server 2012 RTM Management Studio)|Actualizar todos los productos a la versión de 32 bits de SQL Server 2012 SP1|SQLServer2012SP1-KB2674319-x86-ENU.exe desde [aquí](http://go.microsoft.com/fwlink/p/?LinkID=268158)|  
|Una versión de 32 bits de una o más herramientas del [Microsoft SQL Server 2012 RTM Feature Pack](http://www.microsoft.com/download/details.aspx?id=16978)|Actualizar las herramientas a la versión de 32 bits del Microsoft SQL Server 2012 SP1 Feature Pack|Uno o más archivos del [Microsoft SQL Server 2012 SP1 Feature Pack](http://go.microsoft.com/fwlink/p/?LinkID=268266)|  
|No instalar la versión de 32 bits de SQL Server 2012|Instalar una versión de 32 bits de Server 2012 incluido SP1 (nueva instancia con SP1 preinstalado)|SQLServer2012SP1-FullSlipstream-x86-ENU.exe **y** SQLServer2012SP1-FullSlipstream-x86-ENU.box desde [aquí](http://go.microsoft.com/fwlink/p/?LinkID=268158)|  
|No instalar la versión de 32 bits de SQL Server 2012 Management Studio|Instalar la versión de 32 bits de SQL Server 2012 Management Studio junto con el SP1|SQLManagementStudio_x86_ENU.exe desde [aquí](http://go.microsoft.com/fwlink/p/?LinkId=267905)|  
|Sin versión de 32 bits de SQL Server 2012 RTM Express|Instalar versión de 32 bits de SQL Server 2012 Express incluido el SP1|SQLEXPR32_x86_ENU.exe desde [aquí](http://go.microsoft.com/fwlink/p/?LinkId=267905)|  
|Instalación de una versión de 32 bits de **SQL Server 2008** o **SQL Server 2008 R2**|**Actualización en contexto** a la versión de 32 bits de SQL Server 2012 incluido el SP1|SQLServer2012SP1-FullSlipstream-x86-ENU.exe **y** SQLServer2012SP1-FullSlipstream-x86-ENU.box desde [aquí](http://go.microsoft.com/fwlink/p/?LinkID=268158)|  
|**Instalaciones de&64; bits:**|||  
|Una versión de 64 bits de cualquier edición de SQL Server 2012|Actualizar a la versión de 64 bits de SQL Server 2012 SP1|SQLServer2012SP1-KB2674319-x64-ENU.exe desde [aquí](http://go.microsoft.com/fwlink/p/?LinkID=268158)|  
|Una versión de 64 bits de SQL Server 2012 RTM Express|Actualizar a la versión de 64 bits de SQL Server 2012 SP1|SQLServer2012SP1-KB2674319-x64-ENU.exe desde [aquí](http://go.microsoft.com/fwlink/p/?LinkID=268158)|  
|Una versión de 64 bits únicamente las herramientas de cliente y de administración para SQL Server 2012 (incluido SQL Server 2012 Management Studio)|Actualizar las herramientas de cliente y de administración a la versión de 64 bits de SQL Server 2012 SP1|SQLManagementStudio_x64_ENU.exe desde [aquí](http://go.microsoft.com/fwlink/p/?LinkID=267905)|  
|Una versión de 64 bits de SQL Server 2012 Management Studio Express|Actualizar a la versión de 64 bits de SQL Server 2012 SP1 Management Studio Express|SQLManagementStudio_x64_ENU.exe desde [aquí](http://go.microsoft.com/fwlink/p/?LinkID=267905)|  
|Una versión de 64 bits de cualquier edición de SQL Server 2012 **y** una versión de 64 bits de las herramientas de cliente y de administración (incluido SQL Server 2012 RTM Management Studio)|Actualizar todos los productos a la versión de 64 bits de SQL Server 2012 SP1|SQLServer2012SP1-KB2674319-x64-ENU.exe desde [aquí](http://go.microsoft.com/fwlink/p/?LinkID=268158)|  
|Una versión de 64 bits de una o más herramientas del [Microsoft SQL Server 2012 RTM Feature Pack](http://www.microsoft.com/download/en/details.aspx?id=16978)|Actualizar las herramientas a la versión de 64 bits del Microsoft SQL Server 2012 SP1 Feature Pack|Uno o más archivos del [Microsoft SQL Server 2012 SP1 Feature Pack](http://go.microsoft.com/fwlink/p/?LinkID=268266)|  
|No instalar la versión de 64 bits de SQL Server 2012|Instalar una versión de 64 bits de Server 2012 incluido SP1 (nueva instancia con SP1 preinstalado)|SQLServer2012SP1-FullSlipstream-x64-ENU.exe **y** SQLServer2012SP1-FullSlipstream-x64-ENU.box desde [aquí](http://go.microsoft.com/fwlink/p/?LinkID=268158)|  
|No instalar la versión de 64 bits de SQL Server 2012 Management Studio|Instalar la versión de 64 bits de SQL Server 2012 Management Studio junto con el SP1|SQLManagementStudio_x64_ENU.exe desde [aquí](http://go.microsoft.com/fwlink/p/?LinkID=267905)|  
|Sin versión de 64 bits de SQL Server 2012 RTM Express|Instalar versión de 64 bits de SQL Server 2012 Express incluido el SP1|SQLEXPR_x64_ENU.exe desde [aquí](http://go.microsoft.com/fwlink/p/?LinkID=267905)|  
|Instalación de una versión de 64 bits de **SQL Server 2008** o **SQL Server 2008 R2**|**Actualización en contexto** a la versión de 64 bits de SQL Server 2012 incluido el SP1|SQLServer2012SP1-FullSlipstream-x64-ENU.exe **y** SQLServer2012SP1-FullSlipstream-x64-ENU.box desde [aquí](http://go.microsoft.com/fwlink/p/?LinkID=268158)|  
  
![Icono de flecha usado con el vínculo Volver al principio](../sql-server/media/uparrow16x16.gif "Icono de flecha usado con el vínculo Volver al principio")[Contenido](#bkmk_top)  
  
## <a name="bkmk_AS"></a>2.0 Analysis Services y PowerPivot  
  
### <a name="21-powerpivot-configuration-tool-does-not-create-the-powerpivot-gallery"></a>2.1 La herramienta de configuración de PowerPivot no crea la Galería de PowerPivot  
**Problema** : la herramienta de configuración de PowerPivot aprovisiona un sitio de grupo y, por tanto, la Galería de PowerPivot no se crea.  
  
**Solución alternativa** : cree una nueva aplicación (biblioteca).  
  
1.  Compruebe si la característica **Integración de características de PowerPivot para colecciones de sitios** está activa.  
  
2.  En la página **Contenido del sitio** de un sitio existente, haga clic en **Agregar aplicación**.  
  
3.  Haga clic en **Galería de PowerPivot**.  
  
### <a name="22-to-use-powerpivot-for-excel-with-excel-2013-you-must-use-the-add-in-that-is-installed-with-excel"></a>2.2 Para usar PowerPivot para Excel con Excel 2013, debe usar el complemento que se instala con Excel  
**Problema:** con Office 2010, PowerPivot para Excel es un complemento independiente que se puede descargar de [http://www.microsoft.com/bi/powerpivot.aspx](http://www.microsoft.com/bi/powerpivot.aspx). También se puede descargar desde el [Centro de descarga Microsoft](http://www.microsoft.com/download/details.aspx?id=29074). Tenga en cuenta que se pueden descargar dos versiones del complemento PowerPivot: una incluida con SQL Server 2008 R2y otra incluida con SQL Server 2012. Sin embargo, en el caso de Office 2013, PowerPivot para Excel se incluye con Office y se instala al instalar Excel. Si bien las versiones de SQL Server 2008 R2 y SQL Server 2012 de PowerPivot para Excel 2010 no son compatibles con Excel 2013, puede instalar PowerPivot para Excel 2010 en el equipo cliente si desea ejecutar Excel 2010 en paralelo con Excel 2013. Es decir, las dos versiones de Excel pueden coexistir, así como sus complementos PowerPivot correspondientes.  
  
**Solución alternativa** : para usar PowerPivot para Excel 2013 debe habilitar el complemento COM. En Excel 2013, seleccione **Archivo** | **Opciones** | **Complementos**. En el cuadro desplegable **Administrar** , seleccione **Complementos COM** y haga clic en **Ir**. En **Complementos COM**, seleccione **Microsoft Office PowerPivot para Excel 2013** y haga clic en **Aceptar**.  
  
![Icono de flecha usado con el vínculo Volver al principio](../sql-server/media/uparrow16x16.gif "Icono de flecha usado con el vínculo Volver al principio")[Contenido](#bkmk_top)  
  
## <a name="bkmk_RS"></a>3.0 Reporting Services  
  
### <a name="31-install-and-configure-sharepoint-server-2013-prior-to-installing-reporting-services"></a>3.1 Instalar y configurar SharePoint Server 2013 antes de instalar Reporting Services  
**Problema:** complete los requisitos siguientes **antes** de instalar SQL Server Reporting Services (SSRS).  
  
1.  Ejecutar la herramienta de preparación de Productos de SharePoint 2013.  
  
2.  Instalar SharePoint Server 2013.  
  
3.  Ejecutar el Asistente para configuración de Productos de SharePoint 2013 o completar un conjunto equivalente de pasos de configuración para configurar la granja de SharePoint.  
  
**Solución alternativa:**  si instaló el modo SharePoint de [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] antes de configurar la granja de SharePoint, la solución alternativa necesaria depende de los otros componentes que están instalados.  
  
### <a name="32-power-view-in-sharepoint-server-2013-requires-microsoftanalysisservicesspclientdll"></a>3.2 Power View en SharePoint Server 2013 requiere Microsoft.AnalysisServices.SPClient.dll  
**Problema:**[!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] no instala un componente requerido, **Microsoft.AnalysisServices.SPClient.dll**. Si instala Vista previa de SharePoint Server 2013 y [!INCLUDE[ssSQL11SP1](../includes/sssql11sp1-md.md)][!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] en modo SharePoint, pero no descarga e instala el paquete del instalador de PowerPivot para SharePoint 2013, **spPowerPivot.msi** , Power View no funcionará y Power View presentará los siguientes síntomas.  
  
**Síntomas:** cuando intenta crear un informe de Power View, ve un mensaje de error similar al siguiente:  
  
-   "No se puede crear una conexión al origen de datos...''.  
  
Los detalles del error interno contendrán un mensaje similar al siguiente:  
  
-   "El valor 'SharePoint Principal' no es compatible con la propiedad de la cadena de conexión 'User Identity'."  
  
**Solución alternativa:** instale el paquete del instalador de PowerPivot para SharePoint 2013 (**spPowerPivot.msi**) en SharePoint Server 2013. El paquete del instalador está disponible como parte de [!INCLUDE[ssSQL11SP1](../includes/sssql11sp1-md.md)] Feature Pack. Feature Pack se puede descargar desde el centro de descargas de [!INCLUDE[msCoName](../includes/msconame-md.md)] en [SQL Server 2012 SP1 Feature Pack](http://go.microsoft.com/fwlink/p/?LinkID=268266)(http://go.microsoft.com/fwlink/p/?LinkID=268266).  
  
### <a name="33-power-view-sheets-in-a-powerpivot-workbook-are-deleted-after-a-scheduled-data-refresh"></a>3.3 Las hojas de Power View en un libro PowerPivot se borran tras una actualización de datos programada  
**Problema**: en el complemento PowerPivot para SharePoint, con **Actualización de datos programada** en un libro con Power View se eliminarán todas las hojas de Power View.  
  
**Solución alternativa**: para utilizar **Scheduled Data Refresh** con libros Power View, cree un libro PowerPivot que sea el modelo de datos. Cree otro libro con las hojas de Excel y Power View que se vincule al libro PowerPivot con el modelo de datos. Para la actualización de datos, solo se debe programar el libro PowerPivot con el modelo de datos.  
  
## <a name="bkmk_DQS"></a>4.0 Data Quality Services  
  
### <a name="41-dqs-available-in-the-incorrect-edition-of-sql-server-2012"></a>4.1 DQS disponible en la edición incorrecta de SQL Server 2012  
**Problema** : en la versión [!INCLUDE[ssSQL11](../includes/sssql11-md.md)] RTM, la característica Data Quality Services (DQS) está disponible en ediciones de SQL Server distintas de Enterprise, Business Intelligence y Developer. Después de instalar SQL Server 2012 SP1, DQS no estará disponible en todas las ediciones salvo en Enterprise, Business Intelligence y Developer.  
  
**Solución alternativa**: si está usando DQS en una edición no admitida, actualícese a una edición admitida o quite la dependencia en esta característica de sus aplicaciones.  
  
![Icono de flecha usado con el vínculo Volver al principio](../sql-server/media/uparrow16x16.gif "Icono de flecha usado con el vínculo Volver al principio")[Contenido](#bkmk_top)  
  
## <a name="bkmk_Express"></a>5.0 SQL Server Express  
  
### <a name="51-full-version-of-sql-server-management-studio-available-in-sql-server-2012-express-sp1"></a>5.1 La versión completa de SQL Server Management Studio está disponible en SQL Server 2012 Express SP1  
SQL Server 2012 Express Service Pack 1 (SP1) incluye la versión completa de SQL Server 2012 Management Studio (que antes solo estaba disponible en el DVD de SQL Server 2012) en lugar de SQL Server 2012 Management Studio Express. Para descargar e instalar SQL Server 2012 Express SP1, vea [SQL Server 2012 Express Service Pack 1](http://go.microsoft.com/fwlink/p/?linkid=267905).  
  
![Icono de flecha usado con el vínculo Volver al principio](../sql-server/media/uparrow16x16.gif "Icono de flecha usado con el vínculo Volver al principio")[Contenido](#bkmk_top)  
  
## <a name="bkmk_CDC"></a>6.0 Servicio y diseñador de captura de datos modificados para Oracle de Attunity  
  
### <a name="61-upgrading-the-cdc-service-and-designer"></a>6.1 Actualizar CDC Service y CDC Designer  
**Problema** : si Change Data Capture Designer para Oracle y Change Data Capture Service para Oracle de Attunity están instalados en el equipo cuando se instala SQL Server 2012 SP1, estos componentes no se actualizarán con la instalación de SP1.  
  
**Solución alternativa** : para actualizar los componentes de CDC a la versión más reciente:  
  
1.  Descargue los archivos .msi para Change Data Capture Service para Oracle de Attunity desde la [Página de descarga de Feature Pack de SQL Server 2012 SP1](http://go.microsoft.com/fwlink/p/?LinkID=268266).  
  
2.  Ejecute el archivo .msi.  
  
![Icono de flecha usado con el vínculo Volver al principio](../sql-server/media/uparrow16x16.gif "Icono de flecha usado con el vínculo Volver al principio")[Contenido](#bkmk_top)  
  
## <a name="DACFx"></a>7.0 Marco de trabajo de la aplicación de capa de datos (DACFx) de SQL Server  
**Compatibilidad con la actualización en contexto**  
  
Esta versión del Marco de trabajo de la aplicación de capa de datos (DACFx) es compatible con la actualización en contexto de versiones anteriores por lo que no es necesario quitar instalaciones anteriores de DACFx antes de la actualización a esta versión. Puede encontrar próximas versiones de DACFx [aquí](https://msdn.microsoft.com/library/dn702988.aspx).  
  
**Compatibilidad con índice XML selectivo**  
  
SQL Server 2012 SP1 es compatible con [Índice XML selectivo (SXI)](http://msdn.microsoft.com/en-us/598ecdcd-084b-4032-81b2-eed6ae9f5d44), una nueva característica de SQL Server que proporciona una nueva manera de indizar datos de columnas XML y mejorar así el rendimiento y la eficacia.  
  
DACFx ahora es compatible con índices SXI en todos los escenarios DAC y herramientas cliente. SXI solo es compatible con la versión más reciente de SSDT. La versión RTM y la versión de septiembre de 2012 de SSDT no son compatibles con SXI.  
  
**Compatibilidad con el formato de datos BCP nativo**  
  
Anteriormente, el formato de datos utilizado para almacenar datos de tabla en los paquetes DACPAC y BACPAC era JSON. Con esta actualización, el formato de datos BCP nativo es ahora el formato de persistencia de datos. Este cambio proporciona una fidelidad a DACFx mejorada de los tipos de datos de SQL Server, incluida la compatibilidad para tipos SQL_Variant y una implementación y rendimiento de datos mejorados para bases de datos a gran escala.  
  
**Conservación del estado de la restricción CHECK en la creación e implementación de paquetes**  
  
Anteriormente, DACFx no conservaba el estado (WITH CHECK/NOCHECK) de las restricciones CHECK definidas en tablas en el esquema de base de datos ni almacenaba esta información dentro de los DACPAC. Este comportamiento podía crear posibles problemas en la implementación de paquetes cuando existieran datos de tabla que incumplieran las restricciones CHECK. Con esta actualización, DACFx ahora almacena el estado actual de las restricciones CHECK dentro del DACPAC cuando se extrae de una base de datos y restaura adecuadamente este estado durante la implementación del paquete.  
  
**Actualizaciones de SqlPackage.exe (herramienta de línea de comandos DACFx)**  
  
-   Extraer DACPAC con datos – Crea un archivo de captura de pantalla de base de datos (.dacpac) a partir de una Base de datos SQL de Windows Azure o de SQL Server que contiene datos de tablas de usuario además del esquema de la base de datos. Estos paquetes se pueden publicar en una Base de datos SQL de Windows Azure o de SQL Server nueva o existente con la acción Publicar de SqlPackage.exe. Los datos contenidos en el paquete reemplazan a los datos existentes en la base de datos de destino.  
  
-   Exportar BACPAC - Crea un archivo de copia de seguridad lógica (.bacpac) a partir de una Base de datos SQL de Windows Azure o SQL Server que contiene el esquema de base de datos y los datos de usuario que se pueden usar para migrar una base de datos de una Base de datos SQL de Windows Azure a un SQL Server local. Las bases de datos compatibles con Azure se pueden exportar y a continuación importar entre versiones compatibles de SQL Server.  
  
-   Importar BACPAC – Importa un archivo .bacpac para crear una nueva Base de datos SQL de Windows Azure o de SQL Server o para rellenar una vacía.  
  
La documentación completa de SqlPackage.exe en MSDN se puede encontrar [aquí](http://msdn.microsoft.com/library/hh550080%28v=vs.103%29.aspx).  
  
**Compatibilidad de los paquetes**  
  
Esta versión presenta varios escenario de compatibilidad con versiones posteriores para los paquetes DAC.  
  
-   Los paquetes DAC creados por esta versión que no contengan elementos SXI o datos de tabla se pueden utilizar en versiones anteriores de DACFx (SQL Server 2012 RTM, SQL Server 2012 CU1 y DACFx de septiembre de 2012).  
  
-   Todos los paquetes DAC creados por versiones anteriores de DACFx se pueden utilizar en esta versión.  
  
## <a name="bkmk_known_issues_fixed"></a>8.0 Problemas conocidos corregidos en este Service Pack  
Para obtener una lista completa de errores y de problemas conocidos corregidos en este Service Pack, vea [este artículo de KB](http://support.microsoft.com/kb/2674319).  
  
[Contenido](#bkmk_top)  
  
## <a name="see-also"></a>Vea también  
[Cómo determinar la versión y la edición de SQL Server](http://support.microsoft.com/kb/321185)  
[Características compatibles con las ediciones de SQL Server 2014](http://msdn.microsoft.com/en-us/5da61ff5-12b9-48e6-b3c8-0dacca1751c4)  
  
