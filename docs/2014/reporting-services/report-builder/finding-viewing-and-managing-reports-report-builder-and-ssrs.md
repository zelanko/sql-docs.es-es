---
title: Buscar, ver y administrar informes (Generador de informes y SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 12/29/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
ms.assetid: 5599300d-6bcd-4704-aba5-fa98e01c78a9
author: markingmyname
ms.author: maghan
manager: kfile
ms.openlocfilehash: e02d6bb985d7b18c7e1401882ad9bd926168c6a1
ms.sourcegitcommit: dfb1e6deaa4919a0f4e654af57252cfb09613dd5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/11/2019
ms.locfileid: "56040816"
---
# <a name="finding-viewing-and-managing-reports-report-builder-and-ssrs-"></a>Buscar, ver y administrar informes (Generador de informes y SSRS)
  En el Generador de informes, puede examinar las carpetas en un servidor de informes o un sitio de SharePoint para buscar informes, orígenes de datos compartidos, modelos y otros elementos de informe relacionados, y examinar su equipo para buscar informes locales. Para que buscar informes sea más fácil, el Generador de informes cuenta con una lista de servidores y sitios utilizados recientemente, y proporciona acceso directo a las carpetas Escritorio, Mis documentos y Mi PC del sistema de archivos del equipo.  
  
 En el Diseñador de informes, también puede examinar su equipo para buscar informes locales. Después de implementar informes en un servidor de informes o un sitio de SharePoint, podrá examinar el servidor de informes utilizando el Administrador de informes o buscar en el sitio de SharePoint para encontrar informes. Los informes y elementos relacionados siguen estando disponibles localmente después de implementarse.  
  
> [!NOTE]  
>  Puede usar el Generador de informes en modo local o conectado a un servidor de informes. Se aplican ciertas limitaciones si no tiene una conexión activa a un servidor de informes.  
  
 Para buscar un informe en un servidor de informes o un sitio de SharePoint desde el Generador de informes, debe proporcionar la dirección URL para el servidor de informes o el sitio de SharePoint. La primera vez que instale el Generador de informes puede especificar la dirección URLque se debe usar. El Generador de informes se conecta de forma predeterminada a este servidor o sitio cuando se guardan o abren informes.  
  
 Se puede obtener una vista previa de los informes en el Generador de informes y el Diseñador de informes cuando se crean o se actualizan, y se pueden ver y administrar en un servidor de informes utilizando el Administrador de informes, o en un sitio de SharePoint integrado con Reporting Services utilizando las herramientas y características integradas de SharePoint después de publicarlos. Para más información, vea [Mostrar la vista previa de informes en el Generador de informes](previewing-reports-in-report-builder.md) y [Obtener la vista previa de informes](../reports/previewing-reports.md).  
  
 Cuando obtiene una vista previa de los informes en el Generador de informes y el Diseñador de informes, o los ve en el Administrador de informes o un sitio de SharePoint, los datos se actualizan y los informes muestran los datos actuales del origen de datos que el informe utiliza. Si desea ver un informe sin actualizar sus datos, puede usar el historial del informe y los datos almacenados en caché de los informes publicados. Estas características no se pueden usar al obtener una vista previa de los informes en el Generador de informes y el Diseñador de informes.  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
##  <a name="FindingAndViewingReportsRB30"></a> Buscar y ver informes en el Generador de informes  
 Para buscar un informe con el que desea trabajar o para seleccionar un origen de datos compartido, una imagen o un subinforme para usarlos en un informe, puede examinar el equipo, las carpetas de un servidor de informes, o el sitio de SharePoint integrado con Reporting Services.  
  
 Para encontrar informes en un servidor de informes, debe especificar una dirección URL correspondiente al servidor de informes, así como tener para las carpetas los permisos adecuados para leer y guardar los elementos de informe. Pida el administrador del sistema del servidor de informes los permisos y la dirección URL que correspondan.  
  
 Cuando haya encontrado y abierto el informe en el Generador de informes, puede obtener una vista previa del informe y realizar cambios. Al obtener la vista previa, ve los datos actuales. Para obtener más información, consulte [Previewing Reports in Report Builder](previewing-reports-in-report-builder.md).  
  
 El Generador de informes puede ayudarle con las siguientes tareas:  
  
-   **Buscar informes** Al buscar un informe, puede usar el conocido cuadro de diálogo **Abrir archivo** del estilo de Microsoft Office que se ha personalizado para el Generador de informes. Puede examinar las carpetas de un servidor de informes o de un sistema de archivos, incluyendo Mis Informes, Sitios y Servidores, Escritorio, Mis documentos, Mi PC. Sitios y Servidores proporciona una lista de los servidores utilizados recientemente.  
  
-   **Buscar los orígenes de datos compartidos** Al buscar un origen de datos compartido, puede escoger en una lista de los utilizados recientemente o ir a otra carpeta en el mismo servidor de informes del informe.  
  
-   **Ver informes** Puede obtener una vista previa de un informe en el Generador de informes al crear o actualizar los informes. Cuando el Generador de informes está conectado a un servidor de informes, éste carga y procesa el informe; en caso contrario, los informes se procesan localmente. El visor de informes del Generador de informes muestra el informe representado.  
  

  
##  <a name="ViewingAndManagingReportServer"></a> Ver y administrar informes en un servidor de informes  
 Para ver y administrar los informes del servidor de informes se usa el Administrador de informes. Examine las carpetas del servidor para buscar informes, ejecute los informes para verlos en un explorador y realice las tareas de administración.  
  
 El Administrador de informes puede ayudarle con las siguientes tareas de administración:  
  
-   Ver y actualizar las propiedades de informes, orígenes de datos compartidos y otros elementos de informe.  
  
-   Cargar informes y crear nuevos orígenes de datos compartidos para los informes.  
  
-   Crear calendarios para ejecutar los informes en los momentos e intervalos especificados.  
  
-   Crear, cambiar o eliminar suscripciones a los informes.  
  
-   Crear el historial del informe y especificar el número de instantáneas de informe que se deben guardar en el historial del informe.  
  
-   Crear nuevas carpetas en el servidor para organizar los informes de la manera más adecuada.  
  
 El administrador del servidor de informes podría realizar algunas de estas tareas. Para más información sobre las tareas realizadas en un servidor de informes, vea [Servidor de informes de Reporting Services &#40;modo nativo&#41;](../report-server/reporting-services-report-server-native-mode.md).  
  
 Normalmente, el Administrador de informes contiene carpetas, informes, orígenes de datos y modelos de informe, además de la carpeta Mis informes. Mis informes es un área de trabajo personal que puede utilizar para trabajar con sus informes y almacenarlos. Otras carpetas del servidor de informes son públicas y suelen requerir que los usuarios dispongan de permisos avanzados para agregar o modificar su contenido. Puede crear carpetas dentro de MisiInformes para organizar mejor sus informes. Para más información, vea [Usar Mis informes &#40;Generador de informes y SSRS&#41;](using-my-reports-report-builder-and-ssrs.md).  
  
 El Administrador de informes muestra los informes en el Visor HTML de Reporting Services. El Visor HTML proporciona un marco para ver los informes en HTML, e incluye una barra de herramientas de informe, una sección de parámetros, una sección de credenciales y un mapa del documento. La barra de herramientas de informe ofrece funciones de navegación por la página, zoom, actualización, búsqueda, exportación, impresión y fuente de distribución de datos. Esta barra de herramientas también aparece en las ventanas de explorador, en la parte superior del informe, cuando se obtiene acceso a los informes mediante una dirección URL. La funcionalidad de impresión es opcional y la debe activar el administrador. Si está disponible, en la barra de herramientas de informe se mostrará el icono de la impresora. Las ilustraciones siguientes muestran la barra de herramientas de informe en una ventana del Administrador de informes y las características de la barra de herramientas de informe en primer plano.  
  
 ![Barra de herramientas de informes del Administrador de informes](../media/hs-reportserver-blowout.gif "Barra de herramientas de informes del Administrador de informes")  
Ventana del Administrador de informes  
  
 ![Barra de herramientas de informe](../media/htmlviewer-toolbar.gif "Barra de herramientas de informe")  
Barra de herramientas de informe  
  
 Después de ejecutar un informe, puede exportarlo a otro formato, como [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Excel o PDF. También puede exportar el informe mediante una extensión de representación de datos, como CSV (valores separados por comas), y utilizar después el archivo de datos CSV como entrada para otra aplicación. Para obtener más información sobre cómo exportar informes, vea [exportar informes &#40;generador de informes y SSRS&#41; ](export-reports-report-builder-and-ssrs.md) y [exportar un informe como otro tipo de archivo &#40;generador de informes y SSRS&#41; ](../export-a-report-as-another-file-type-report-builder-and-ssrs.md).  
  
 La forma más sencilla de seleccionar y ejecutar un informe consiste en abrir el Administrador de informes y buscar el informe que se desea ver, o desplazarse hasta el mismo. Para obtener instrucciones paso a paso sobre cómo abrir informes, vea [Abrir y cerrar un informe &#40;Administrador de informes&#41;](../reports/open-and-close-a-report-report-manager.md).  
  
 Después de ejecutar un informe, puede actualizarlo para ver los nuevos datos.  
  
### <a name="refreshing-reports"></a>Actualizar informes  
 Los datos del informe cambian frecuentemente; puede actualizar el informe para ver los datos más recientes. Existen tres modos de actualizar un informe.  
  
|Opción|Resultado|  
|------------|------------|  
|Botón**Actualizar** de la ventana del explorador|Muestra el informe almacenado en la memoria caché de la sesión. Cuando un usuario abre un informe, se crea una memoria caché de la sesión. [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] usa las sesiones del explorador para mantener una experiencia de visualización coherente mientras permanece abierto un informe.|  
|![Botón para actualizar el explorador de la barra de herramientas](../media/htmlviewer-refresh.GIF "Botón para actualizar el explorador de la barra de herramientas")|Al hacer clic en el botón **Actualizar** de la barra de herramientas de informes, el servidor de informes vuelve a ejecutar la consulta y actualiza los datos del informe si este se ejecuta a petición. Si el informe está almacenado en la memoria caché o es una instantánea, **Actualizar** muestra el informe almacenado en la base de datos del servidor de informes.|  
|Combinación de teclas CTRL+F5|Produce el mismo efecto que hacer clic en el botón **Actualizar** de la barra de herramientas de informe.|  
  

  
##  <a name="ViewingAndManagingSharePointSite"></a> Ver y administrar elementos del servidor de informes desde un sitio de SharePoint  
 Cuando el administrador de sistema configura un servidor de informes para que se ejecute en el modo integrado de SharePoint, puede ver y administrar informes y otros elementos del servidor de informes desde un sitio de SharePoint.  
  
 El sitio de SharePoint contiene páginas donde se pueden establecer propiedades del origen de datos, el historial de informes, opciones de procesamiento de informes, programaciones, suscripciones y parámetros de informe, así como crear programaciones compartidas. Puede administrar elementos del servidor de informes en un sitio de SharePoint del mismo modo que los crearía y administraría desde otras herramientas de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
 Para tener acceso a las páginas de aplicación, seleccione acciones específicas del elemento en un menú desplegable en un informe u otro elemento de servidor de informes que previamente haya agregado a una biblioteca de SharePoint. En función del elemento y de sus permisos, es probable que también pueda crear informes en el Generador de informes, generar modelos y establecer la seguridad de los elementos de modelo.  
  
 Para más información sobre Reporting Services y la tecnología de SharePoint, vea [Configuración y administración de un servidor de informes &#40;modo de SharePoint de Reporting Services&#41;](../configure-administer-report-server-reporting-services-sharepoint-mode.md) de [Libros en pantalla](https://go.microsoft.com/fwlink/?LinkId=154888) de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] en msdn.microsoft.com.  
  
### <a name="finding-report-server-items-on-a-sharepoint-site"></a>Buscar elementos del servidor de informes en un sitio de SharePoint  
 Para poder establecer propiedades, antes debe poder localizar el elemento. Los elementos del servidor de informes siempre están almacenados en bibliotecas o en una carpeta dentro de una biblioteca.  
  
 Al tener acceso al sitio de SharePoint, verá la página Examinar y la pestaña Herramientas de bibliotecas. La página Examinar enumera las bibliotecas y el contenido de la biblioteca seleccionada. Podrá ver el informe, los modelos de informe y otros elementos de la biblioteca, explorar carpetas y localizar elementos en el sitio.  
  
 Para distinguir los elementos del servidor de informes de otros elementos de un sitio de SharePoint, puede utilizar el icono para identificar visualmente un elemento o colocar el cursor del mouse (ratón) sobre el tipo y leer la extensión de archivo. La siguiente imagen muestra carpetas, un modelo de informe y una definición de informe de la biblioteca **Informes** :  
  
 ![Biblioteca de SharePoint con elementos del servidor de informes](../media/rs-sharepointlibrary.gif "Biblioteca de SharePoint con elementos del servidor de informes")  
  
### <a name="viewing-reports"></a>Ver informes  
 Las definiciones de informe (archivos .rdl) que cargue en una biblioteca de SharePoint se ven mediante un elemento web Visor de informes instalado por el complemento Reporting Services. Al instalar el complemento, se define automáticamente una asociación a archivos .rdl. Al seleccionar un informe, se abre automáticamente en el elemento web. Después de abrir el informe, puede utilizar la barra de herramientas de informe que se incluye en el elemento web para navegar por las páginas del informe, realizar búsquedas, acercarlo o alejarlo e imprimirlo. La barra de herramientas incluye la opción Exportar a fuente de distribución de datos para exportar el informe como una fuente datos de Atom y un menú **Acciones** con opciones para imprimir informes, suscribirse a ellos y exportarlos en diferentes formatos, como PDF, Word y Excel. En el menú **Acciones** , podrá abrir también el informe en el Generador de informes. La siguiente imagen muestra un informe y las opciones de exportación del menú **Acción** .  
  
 ![rs_SharePointRunReport](../media/rs-sharepointrunreport.gif "rs_SharePointRunReport")  
  
### <a name="managing-items-through-actions"></a>Administrar elementos mediante acciones  
 Se permite la realización de tareas de administración mediante las acciones de un menú desplegable para cada elemento. En función de sus permisos, cada elemento tiene acciones comunes que son estándar para los elementos que se almacenan en una biblioteca de SharePoint. **Ver propiedades** y **Editar propiedades** son ejemplos de acciones comunes. Las acciones personalizadas ofrecen una funcionalidad de administración específica de los elementos. En la siguiente imagen se muestran las acciones de una definición de informe. Entre algunos de los ejemplos de acciones personalizadas de una definición de informe se incluyen **Administrar suscripciones** y **Administrar opciones de procesamiento**:  
  
 ![Comandos de menú para elementos del servidor de informes](../media/rs-ecbforrsitems.gif "Comandos de menú para elementos del servidor de informes")  
  

  
##  <a name="DeskTop"></a> Ver informes en una aplicación de escritorio  
 Si lo prefiere, puede omitir la visualización con el explorador y, en su lugar, usar una aplicación de escritorio (como [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Excel) como el visor de informes. Para ello, defina una suscripción que especifique un formato de aplicación de escritorio y un destino para la carpeta compartida. El servidor de informes generará el informe como si se tratara de un archivo de la aplicación, le anexará una extensión al nombre de archivo y lo guardará como archivo en el disco duro. Después, podrá usar [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Excel (u otra aplicación) en lugar de un explorador para ver el informe.  
  

  
##  <a name="AboutUserSessions"></a> Acerca de las sesiones de usuario  
 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] utiliza las sesiones del explorador para mantener la coherencia durante la visualización de los informes. Las sesiones se basan en conexiones de explorador en lugar de en usuarios autenticados. Cada vez que un usuario abre un informe en una nueva ventana del explorador, se crea una sesión nueva. Una vez establecida una sesión de explorador, puede continuar trabajando en la versión del informe abierta al iniciar la sesión, incluso si el informe se modifica en el servidor de informes. Por ejemplo, si abre un informe a las 11:00 p. m. y un autor lo vuelve a publicar a las 11:01 p. m., la sesión que tenga abierta contendrá la versión que ha abierto para la sesión.  
  
 Si actualiza un informe en la misma sesión mediante el botón **Actualizar** del explorador, se muestra la versión de la sesión original del informe. Si actualiza un informe a petición con el botón **Actualizar** de la barra de herramientas del informe, se volverá a ejecutar el informe y, si hay nuevos datos, se mostrarán.  
  
 La información relativa a la sesión se almacena en la base de datos temporal del servidor de informes. El servidor de informes no utiliza la administración de sesiones de [!INCLUDE[vstecasp](../../includes/vstecasp-md.md)] . Si reinicia el servidor o realiza una operación de recuperación de la base de datos, no podrá restaurar el estado de la sesión. Para más información sobre la administración de sesiones, vea [Identificar el estado de ejecución](../report-server-web-service-net-framework-soap-headers/identifying-execution-state.md).  
  

  
##  <a name="InThisSection"></a> En esta sección  
 En los temas siguientes se proporciona información adicional sobre cómo ver y administrar informes.  
  
 [Buscar y ver informes en el Administrador de informes &#40;generador de informes y SSRS&#41;](finding-and-viewing-reports-in-the-web-portal-report-builder-and-ssrs.md)  
 Describe cómo utilizar el Administrador de informes para buscar, ver y administrar sus informes.  
  
 [Buscar y ver informes con un explorador &#40;Generador de informes y SSRS&#41;](finding-and-viewing-reports-with-a-browser-report-builder-and-ssrs.md)  
 Describe cómo utilizar una dirección URL para encontrar y ver un informe.  
  
 [Buscar informes y otros elementos &#40;Generador de informes y SSRS&#41;](searching-for-reports-and-other-items-report-builder-and-ssrs.md)  
 Describe cómo utilizar la funcionalidad de búsqueda del Administrador de informes para buscar elementos en el servidor de informes.  
  
 [Usar Mis informes &#40;Generador de informes y SSRS&#41;](using-my-reports-report-builder-and-ssrs.md)  
 Describe cómo usar la carpeta Mis informes como área de trabajo personal para trabajar con sus informes y almacenarlos.  
  
 [Mostrar la vista previa de informes en el Generador de informes](previewing-reports-in-report-builder.md)  
 Describe cómo obtener una vista previa de los informes mientras se crean o actualizan.  
  

  
## <a name="see-also"></a>Vea también  
 [Guardar informes &#40;Generador de informes&#41;](saving-reports-report-builder.md)   
 [Generador de informes en SQL Server 2014](report-builder-in-sql-server-2016.md)   
 [Instalar, desinstalar y asistencia del Generador de informes](../install-uninstall-and-report-builder-support.md)  
  
  
