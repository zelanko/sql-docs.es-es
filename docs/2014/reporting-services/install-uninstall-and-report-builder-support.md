---
title: Instalar, desinstalar y asistencia del generador de informes | Microsoft Docs
ms.custom: ''
ms.date: 12/29/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- administering Report Builder
ms.assetid: 2c9a5814-17bf-4947-8fb3-6269e7caa416
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 0272c7598e34d7ba920484b3d2b9c504587212cd
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "63261319"
---
# <a name="install-uninstall-and-report-builder-support"></a>Instalar, desinstalar y asistencia del Generador de informes
  El Generador de informes es una herramienta de creación de informes que puede usar para crear, actualizar y compartir informes, elementos de informe y conjuntos de datos compartidos. El Generador de informes está disponible en dos versiones: independiente y [!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)]. Usted mismo o un administrador pueden instalar la versión independiente en el equipo. La versión [!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)] se instala automáticamente con [!INCLUDE[ssRSCurrent](../includes/ssrscurrent-md.md)] y se descarga en su equipo desde el Administrador de informes o un sitio de SharePoint integrado con [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)].  
  
 La versión independiente del Generador de informes no se instala con [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)]. Necesita descargarla e instalarla por separado desde el [Generador de informes para Microsoft® SQL Server® 2012](https://go.microsoft.com/fwlink/?LinkId=401502).  
  
> [!NOTE]  
>  El Generador de informes no se puede instalar en equipos basados en Itanium. Esto se aplica a las versiones independiente y [!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)] del Generador de informes.  
  
 Un administrador normalmente instala y configura [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)], concede permiso para utilizar la versión [!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)] del Generador de informes y administra carpetas y permisos a los informes, los elementos de informe y los conjuntos de datos compartidos guardados en el servidor de informes. Para obtener más información acerca de [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] administración, consulte [Reporting Services Report Server &#40;modo nativo&#41; ](report-server/reporting-services-report-server-native-mode.md) en [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [libros](https://go.microsoft.com/fwlink/?LinkId=154888) en msdn.microsoft.com.  
  
##  <a name="Installing"></a> Instalar el generador de informes  
 El Generador de informes está disponible en las versiones independiente y [!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)] . Usted o el administrador deberán descargar e instalar la versión independiente en el equipo, mientras que la versión [!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)] se instala con [!INCLUDE[ssRSCurrent](../includes/ssrscurrent-md.md)]. Puede descargar el Generador de informes del [Centro de descarga de Microsoft](https://go.microsoft.com/fwlink/?LinkID=186083).  
  
> [!NOTE]  
>  El Generador de informes no se puede instalar en los equipos basados en Itanium 64. Esto se aplica a las versiones independiente y [!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)] del Generador de informes.  
  
 Antes de instalar cualquiera de las dos versiones del Generador de informes, compruebe los requisitos del sistema e instale los requisitos previos.  
  
### <a name="system-requirements"></a>Requisitos del sistema  
 El Generador de informes exige que esté instalada en el equipo local la versión 3.5 de [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../includes/dnprdnshort-md.md)] . Si [!INCLUDE[dnprdnshort](../includes/dnprdnshort-md.md)] no está instalado en el equipo local al instalar el Generador de informes, se le solicitará que lo instale para poder continuar y completar la instalación.  
  
 .NET Framework 3.5 es una aplicación gratuita. Puede descargar .NET Framework 3.5 en el [Centro de descargas de Microsoft](https://go.microsoft.com/fwlink/?LinkID=110520).  
  
 Puede instalar el Generador de informes en cualquier sistema operativo [!INCLUDE[msCoName](../includes/msconame-md.md)] Windows compatible con [!INCLUDE[dnprdnshort](../includes/dnprdnshort-md.md)] 3.5. Por ejemplo, puede instalar el Generador de informes en Windows Vista o Windows 7.  
  
 Es recomendable que los equipos donde vaya a ejecutarse el Generador de informes tengan 512 MB de RAM. Sin embargo, en función de la complejidad de los informes que ejecute, es posible que desee contar con más o menos RAM.  
  
### <a name="installing-the-stand-alone-version-of-report-builder-directly-on-your-computer"></a>Instalar la versión independiente del Generador de informes directamente en el equipo  
 Puede instalar el Generador de informes desde el sitio de descarga, [Centro de descarga de Microsoft](https://go.microsoft.com/fwlink/?LinkID=186083)o un administrador puede hacer que el archivo ReportBuilder3.msi, el paquete de Windows Installer para el Generador de informes, esté disponible en un recurso compartido desde el que podrá instalarlo.  
  
 También puede realizar una instalación de línea de comandos e incluir opciones como, por ejemplo, hacer que la instalación sea silenciosa y escribir archivos de registro para la instalación. En la documentación de Windows Installer que ejecuta los archivos .msi se proporciona información sobre las opciones disponibles.  
  
 Para obtener más información, consulte [instalar la versión independiente del generador de informes &#40;Report Builder&#41;](install-windows/install-report-builder.md).  
  
 Un administrador también puede utilizar software, como Microsoft Systems Manager Server (SM), para insertar el programa en su equipo. Para obtener información sobre la forma de usar software específico para instalar el Generador de informes, consulte la documentación del software.   
  
### <a name="installing-the-clickonce-version-of-report-builder-on-your-computer"></a>Instalar en el equipo la versión ClickOnce del Generador de informes  
 La versión [!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)] del Generador de informes se instala con [!INCLUDE[ssRSCurrent](../includes/ssrscurrent-md.md)]. Se instala mediante instalaciones tanto en modo como en modo integrado de SharePoint de [!INCLUDE[ssRSCurrent](../includes/ssrscurrent-md.md)].  
  
 [!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)] es una tecnología de Microsoft para implementar aplicaciones Windows. [!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)] permite a los usuarios instalar y ejecutar una aplicación Windows, como el Generador de informes, haciendo clic un vínculo de una página web. Para obtener más información acerca de la implementación [!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)] aplicaciones, aplicar [!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)] seguridad de la aplicación o al ejecutar [!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)] aplicaciones en la zona de Internet, consulte la "implementación de Windows Forms aplicaciones ClickOnce", "la seguridad en Información general de Windows Forms"o"Trusted Application Deployment Overview"los artículos sobre la [!INCLUDE[msCoName](../includes/msconame-md.md)] sitio Web Developer Network en [ https://developer.microsoft.com/ ](https://developer.microsoft.com/).  
  
 La versión [!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)] del Generador de informes se encuentra en el servidor de informes y se instalará en su equipo al hacer clic en el botón **Generador de informes** en Administrador de informes o en la opción **Informe del Generador de informes** del menú **Nuevo documento** de una biblioteca de SharePoint.  
  
> [!NOTE]  
>  Si en el menú **Nuevo documento** no aparecen las opciones **Informe del Generador de informes**, **Modelo del Generador de informes**y **Origen de datos de informe** , será necesario agregar sus tipos de contenido a la biblioteca de SharePoint.   
  
 Puede abrir el Generador de informes desde el Administrador de informes o desde una biblioteca de SharePoint. Para obtener más información acerca de cómo abrir el generador de informes, vea [iniciar el generador de informes &#40;Report Builder&#41;](report-builder/start-report-builder.md).  
  
### <a name="report-builder-languages"></a>Idiomas del Generador de informes  
 El Generador de informes está disponible en 21 idiomas además del inglés. Al descargar la versión independiente del Generador de informes, elija la versión de idioma que desee instalar. Deberá repetir la descarga para cada versión de idioma que desee utilizar.  
  
 En la versión [!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)] , todas las versiones de idioma se instalan en el servidor de informes al instalar [!INCLUDE[ssRSCurrent](../includes/ssrscurrent-md.md)]. La referencia cultural del equipo del usuario determina la versión de idioma que se instala en el equipo. Si esa referencia cultural no coincide con ninguno de los idiomas del Generador de informes, se instalará la versión inglesa.  
  
 En la tabla siguiente se incluye información sobre las versiones de idioma disponibles.  
  
|LCID|Lenguaje|Culture|  
|----------|--------------|-------------|  
|1028|Chino (tradicional)|zh-TW|  
|1029|Czech|cs-CZ|  
|1030|Danish|da-DK|  
|1031|German|de-DE|  
|1032|Greek|el-GR|  
|3082|Inglés|es-ES|  
|1035|Finlandés|fi-FI|  
|1036|Francés|fr-FR|  
|1038|Húngaro|hu-HU|  
|1040|Italiano|it-IT|  
|1041|Japonés|ja-JP|  
|1042|Coreano|ko-KR|  
|1043|Neerlandés|nl-NL|  
|1044|Noruego (Bokmal)|nb-NO|  
|1045|Polaco|pl-PLl|  
|1046|Portugués (Brasil)|pt-BR|  
|1049|Ruso|ru-RU|  
|1053|Sueco|sv-SE|  
|1055|Turco|tr-TR|  
|2052|Chino (simplificado)|zh-CN|  
|2070|Portugués (Portugal)|pt-PT|  
|3082|Español (España)|es-ES|  
  
  
##  <a name="Uninstalling"></a> Desinstalar el generador de informes  
 Podrá desinstalar la versión independiente del Generador de informes desde el panel de control o la línea de comandos. Esto se aplica solo a la versión independiente y del Generador de informes. No se puede desinstalar [!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)] del Generador de informes de forma independiente. Siempre se instala o se desinstala con [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)].  
  
 Para obtener más información, consulte [desinstalar la versión independiente del generador de informes &#40;Report Builder&#41;](install-windows/uninstall-report-builder.md).  
  
  
##  <a name="Supporting"></a> Asistencia del generador de informes  
 Para prestar asistencia a los autores de informes, un administrador se encarga de administrar las carpetas, los informes y los elementos relacionados con los informes en el servidor de informes, conceder permiso a los recursos del servidor de informes y configurar el acceso a él.  
  
### <a name="folders-reports-and-report-related-items"></a>Carpetas, informes y elementos relacionados con los informes  
 Las siguientes carpetas, informes y elementos relacionados con los informes se administran en el servidor de informes:  
  
-   Las carpetas en las que se almacenan los informes, los orígenes de datos compartidos, los modelos, etc.  
  
-   Mis informes, la carpeta privada en la que almacena sus propios informes y elementos relacionados con los informes.  
  
-   Orígenes de datos compartidos que permiten a los autores del informe utilizar orígenes de datos que están almacenados externamente en informes.  
  
-   Conjuntos de datos compartidos que pueden proporcionar datos consultados listos para su uso en diferentes informes para usuarios distintos.  
  
-   Elementos de informe, como tablas y gráficos, que permiten a los usuarios mejorar y reutilizar partes de informes, creadas por otros, en un entorno de colaboración.  
  
-   Modelos de informe que pueden hacer más sencillo y fácil obtener datos para los informes de orígenes de datos complejos.  
  
-   Imágenes, como imágenes de fondo y logotipos, que se pueden utilizar en diferentes informes y se almacenan fuera de los informes para facilitar su mantenimiento.  
  
 Para obtener más información, consulte [administración de contenido de servidor de informes &#40;modo nativo de SSRS&#41; ](report-server/report-server-content-management-ssrs-native-mode.md) en [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [libros](https://go.microsoft.com/fwlink/?LinkId=154888) en msdn.microsoft.com.  
  
### <a name="permissions"></a>Permisos  
 El administrador concede permiso al servidor de informes. Como usuario del Generador de informes, deberá contar con permisos al servidor de informes para poder tener acceso a sus contenidos y funcionalidad. Por ejemplo, es posible que desee utilizar elementos de informe almacenados en el servidor de informes, actualizar informes y volver a guardarlos en el servidor de informes o ejecutar informes en el Administrador de informes. En función de sus necesidades y de las tareas que realice, el nivel de los permisos concedidos puede ser mayor o menor. Por ejemplo, los permisos con menos privilegios se conceden a los usuarios que solo necesitan abrir informes compartidos a diferencia de los usuarios que necesitan modificar un informe compartido.  
  
 Cuando [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] se instala en modo nativo, un administrador puede:  
  
-   Habilitar la característica Mis informes para proporcionarle una carpeta privada donde crear y guardar sus propios informes.  
  
-   Utilizar el rol del Generador de informes en carpetas públicas para permitirle abrir una copia de un informe compartido y, a continuación, guardar una versión modificada en una carpeta privada.  
  
-   Utilizar el rol de Publicador para permitirle administrar informes y orígenes de datos compartidos en las carpetas públicas. Este rol se concede a los usuarios con más experiencia.  
  
 Cuando [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] se instala en el modo integrado de SharePoint, un administrador puede:  
  
-   Utilizar el nivel del permiso de lectura, que se concede al grupo Visitantes de forma predeterminada, para permitirle abrir una copia de un informe en una carpeta pública y, a continuación, guardar la versión modificada del informe en una carpeta privada o en su equipo.  
  
-   Utilizar el nivel de permiso Colaborar, que se concede a los grupos de miembros de forma predeterminada, para permitirle administrar informes y orígenes de datos compartidos en carpetas públicas. Este nivel de permiso se concede a los usuarios con más experiencia.  
  
 Para obtener información general sobre los permisos y la creación y utilización de roles, consulte la documentación relativa a [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] en los [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [de](https://go.microsoft.com/fwlink/?LinkId=154888) en msdn.microsoft.com.  
  
### <a name="configuration-of-report-server"></a>Configuración del servidor de informes  
 Al crear informes en el Generador de informes y conectarse a una instancia de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] que esté instalada en Windows Vista, Windows Server 2008 o Windows 7, podría encontrarse con un error de acceso denegado al intentar tener acceso al servidor de informes para abrir o guardar un informe. Esto se debe a que la característica de seguridad, Control de cuentas de usuario (UAC), de Windows Vista, Windows Server 2008 y Windows 7 limita el uso excesivo de permisos elevados quitando los permisos de administrador al tener acceso a las aplicaciones.  
  
 Sin embargo, con una configuración adicional el servidor de informes está disponible para los usuarios del Generador de informes. Puede agregar direcciones URL de [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] a los sitios de confianza. De forma predeterminada, Internet Explorer 7.0 o posterior se ejecuta en modo protegido en Windows Vista, Windows Server 2008 y Windows 7. El modo protegido es una característica que impide que las solicitudes del explorador lleguen a los procesos de alto nivel que se ejecuten en el mismo equipo. Puede deshabilitar el modo protegido para las aplicaciones del servidor de informes agregándolas como sitios de confianza. Debe tener permiso de administrador para realizar esta modificación.  
  
 Para obtener más información acerca de cómo configurar [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)], consulte [Reporting Services Configuration Manager &#40;SUPR&#41; ](/sql/2014/sql-server/install/reporting-services-configuration-manager-native-mode) en el [documentación de Reporting Services](https://go.microsoft.com/fwlink/?linkid=121312) en msdn.microsoft.com.  
  
  
##  <a name="SampleDatabases"></a> Bases de datos de ejemplo SQL Server  
 La familia Adventure Works de bases de datos proporciona datos que se pueden utilizar para obtener información sobre la creación de informes y la escritura de informes de ejemplo.  
  
 Las bases de datos están disponibles en las siguientes versiones:  
  
-   La base de datos OLTP de Adventure Works admite los escenarios del procesamiento de transacciones en línea estándar para un fabricante de bicicletas ficticio (Adventure Works Cycles). Los escenarios incluyen Fabricación, Ventas, Compras, Administración de productos, Administración de contactos y Recursos humanos.  
  
-   La base de datos [!INCLUDE[ssSampleDBDWobject](../includes/sssampledbdwobject-md.md)] demuestra cómo compilar un almacén de datos.  
  
-   El proyecto [!INCLUDE[ssAWDWsp](../includes/ssawdwsp-md.md)] se puede usar para crear una base de datos AS para escenarios de Business Intelligence.  
  
 Las bases de datos de ejemplo no se incluyen con [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] y no se instalan al instalar [!INCLUDE[ssRSCurrent](../includes/ssrscurrent-md.md)] o la versión independiente del Generador de informes. En su lugar, deberá descargar las bases de datos de ejemplo de [CodePlex](https://go.microsoft.com/fwlink/?LinkId=87843). Todas las versiones de las bases de datos de ejemplo se descargan juntas. También puede descargar versiones anteriores de base de datos que se lanzaron con [!INCLUDE[ssVersion2005](../includes/ssversion2005-md.md)], [!INCLUDE[ssKatmai](../includes/sskatmai-md.md)]y [!INCLUDE[ssKilimanjaro](../includes/sskilimanjaro-md.md)].  
  
 Para obtener información sobre los requisitos previos e instrucciones acerca de la descarga e instalación de las bases de datos de ejemplo de [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] , vea los apartados sobre [los requisitos previos para la instalación de bases de datos de muestra de SQL Server 2008](https://go.microsoft.com/fwlink/?LinkId=166648) y la [instalación de bases de datos de ejemplo](https://go.microsoft.com/fwlink/?LinkId=166649) de CodePlex.  
  
  
##  <a name="HowTo"></a> Temas de procedimientos  
 En esta sección se enumeran los procedimientos que muestran cómo instalar y desinstalar el Generador de informes.  
  
 [Instalar la versión independiente del generador de informes &#40;generador de informes&#41;](install-windows/install-report-builder.md)  
  
 [Desinstalar la versión independiente del generador de informes &#40;generador de informes&#41;](install-windows/uninstall-report-builder.md)  
  
 [Iniciar el generador de informes &#40;generador de informes&#41;](report-builder/start-report-builder.md)  
  
  
## <a name="see-also"></a>Vea también  
 [Generador de informes en SQL Server 2014](report-builder/report-builder-in-sql-server-2016.md)  
  
  
