---
title: "Informes de administración de contenido de servidor (modo nativo de SSRS) | Documentos de Microsoft"
ms.custom:
- SQL2016_New_Updated
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- administering Reporting Services
- published reports [Reporting Services], managing
- report servers [Reporting Services], content management
- content management [Reporting Services]
ms.assetid: 641961ac-53a5-4997-9d42-cf4ecce1f892
caps.latest.revision: 50
author: guyinacube
ms.author: asaxton
manager: erikre
ms.translationtype: Machine Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 2289f62499f876cc296d6c939c4d9e70ccfe4c3f
ms.contentlocale: es-es
ms.lasthandoff: 06/22/2017

---
# <a name="report-server-content-management-ssrs-native-mode"></a>Administración de contenido del servidor de informes (Modo nativo de SSRS)
  En [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)], la administración de contenido hace referencia a la administración de elementos del servidor de informes. Es posible administrar todos los elementos de un modo independiente mediante la configuración de las propiedades y de la seguridad. Cualquier elemento puede moverse a una ubicación diferente en el espacio de nombres de carpetas del servidor de informes. Para administrar estos elementos de un modo eficaz, necesita saber las tareas que realiza un administrador de contenido. A partir de [!INCLUDE[ssRSCurrent](../../includes/ssrscurrent-md.md)] CTP 3.2, está disponible el portal web de  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] . En este artículo examinaremos el Administrador de informes y la nueva experiencia de portal web.  
  
> [!NOTE]  
>  La administración de contenido es diferente de la administración de servidores de informes. Si quiere obtener más información sobre cómo administrar el entorno en el que se ejecuta un servidor de informes, vea [Servidor de informes de Reporting Services &#40;modo nativo&#41;](../../reporting-services/report-server/reporting-services-report-server-native-mode.md).  
  
 La administración de contenido comprende las tareas que se describen a continuación:  
  
-   Garantizar la seguridad del sitio del servidor de informes y los elementos mediante la aplicación de la seguridad basada en roles que ofrece [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)].  
  
-   Crear una jerarquía de carpetas del servidor de informes mediante la inclusión, modificación o eliminación de carpetas.  
  
-   Establecer valores predeterminados y propiedades aplicables a los elementos que administra el servidor de informes. Por ejemplo, puede establecer valores máximos básicos que determinen las directivas de almacenamiento del historial del informe.  
  
-   Crear elementos de orígenes de datos compartidos para usar en lugar de las conexiones de orígenes de datos específicos del informe. Un publicador o administrador de contenido puede seleccionar un origen de datos distinto del definido originalmente para un informe, como por ejemplo, para sustituir una referencia a una base de datos de prueba con una referencia a una base de datos de producción.  
  
-   Crear programaciones compartidas que se pueden usar en lugar de las programaciones específicas de informes y específicas de suscripciones, facilitando el mantenimiento de la información de programación con el tiempo.  
  
-   Crear suscripciones controladas por datos que generen listas de destinatarios a partir de los datos obtenidos de un almacén de datos.  
  
-   Equilibrar las peticiones de procesamiento de informes que se envían al servidor mediante la programación del procesamiento de informes y la especificación de los informes que pueden ejecutarse a petición y de los que se cargan desde la memoria caché.  
  
-   Proporcionar permiso para realizar tareas de administración mediante los roles predefinidos: **Administrador del sistema** y **Administrador de contenido**. La administración efectiva del contenido del servidor de informes requiere que esté asignado a ambos roles.  
  
 Las herramientas para administrar contenido del servidor de informes son [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)], el Administrador de informes o el portal web. [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] permite establecer valores predeterminados y habilitar características. El Administrador de informes se usa para conceder acceso de usuario a las operaciones y elementos del servidor de informes, ver y usar informes y otros tipos de contenido, y ver y usar todos los elementos compartidos y características de distribución de informes. El portal web es un sitio actualizado que permite la mayoría de las funciones del Administrador de informes. Para obtener más información, vea [Herramientas de Reporting Services](../../reporting-services/tools/reporting-services-tools.md).  
  
##  <a name="bkmk_ReportServerItems"></a> Elementos del servidor de informes  
 Los elementos del servidor de informes incluyen informes, orígenes de datos compartidos, conjuntos de datos compartidos, elementos de informe, recursos (elementos que se almacenan pero que no procesa el servidor de informes) y carpetas. Los elementos pueden depender de otros elementos; por ejemplo, un informe puede depender de los orígenes de datos compartidos a los que hace referencia. Si mueve un elemento dependiente, el servidor de informes actualiza automáticamente la información de referencia.  
  
 Puede mover elementos del servidor de informes a diversas ubicaciones de carpeta en la jerarquía de carpetas del servidor de informes. Al mover un elemento, también se mueven todas las propiedades (incluida la configuración de seguridad) a la nueva ubicación. Cuando mueve una carpeta, se mueven todos los elementos de la carpeta.  
  
> [!NOTE]  
>  Para CTP 3.2, si quiere mover la ubicación de un elemento, debe realizar esa acción en el Administrador de informes. La capacidad de mover un elemento en el portal web no está disponible.  
  
 En el Administrador de informes, los elementos que se pueden mover aparecen indicados en la jerarquía de carpetas. La siguiente tabla muestra el icono correspondiente a cada uno de los elementos que se pueden mover.  
  
|Icono|Elemento que puede moverse|  
|----------|-------------------|  
|![Icono de informe](../../reporting-services/report-server/media/hlp-16doc.gif "el icono de informe")|Informe|  
|![Icono de informe vinculado](../../reporting-services/report-server/media/hlp-16linked.gif "icono de informe vinculado")|Informe vinculado|  
|![Icono de carpeta](../../reporting-services/report-server/media/hlp-16folder.gif "icono de carpeta")|Carpeta|  
|![icono de recurso genérico](../../reporting-services/report-server/media/hlp-16file.gif "icono de recurso genérico")|Recurso genérico|  
|![Icono de origen de datos compartido](../../reporting-services/report-data/media/hlp-16datasource.png "icono de origen de datos compartido")|Origen de datos compartido|  
||Conjunto de datos compartidos|  
  
 No todos los elementos se pueden mover. Por ejemplo, los elementos asociados a un informe, tales como las suscripciones o el historial del informe, no pueden moverse. Estos elementos se mueven con los informes asociados. Asimismo, tampoco pueden moverse elementos como las programaciones compartidas que existen fuera de la jerarquía de carpetas. No pueden moverse elementos para los que no se tienen los permisos adecuados. Este permiso se concede mediante la selección de las siguientes tareas durante la asignación de roles del elemento en cuestión: "Administrar informes", "Administrar modelos", "Administrar carpetas" y "Administrar orígenes de datos".  
  
##  <a name="bkmk_Folders"></a> Carpetas  
 Para tener acceso a los elementos que se almacenan y administran en un servidor de informes se utiliza una jerarquía de carpetas.  De forma predeterminada, la estructura de carpetas consta de un nodo raíz denominado Inicio y de carpetas reservadas compatibles con la característica opcional Mis informes. Las carpetas adicionales las define el usuario. Las carpetas del servidor de informes son útiles si desea conceder el mismo nivel de acceso a varios elementos. Los permisos que establece en la carpeta pueden heredarlos los elementos de la carpeta y las carpetas adicionales que cuelgan de esa carpeta. Por ejemplo, puede crear un conjunto de carpetas bajo la carpeta Inicio, asignar permisos de equipo a cada carpeta y permitir que los miembros del equipo personalicen las carpetas incluidas bajo la carpeta de equipo según sea necesario.  
  
 Si utiliza un explorador para conectarse directamente a un servidor de informes, el nodo raíz de la estructura de carpeta tendrá el nombre del directorio virtual del servidor de informes. Desde el nodo raíz, puede crear, modificar y eliminar carpetas según sus necesidades, para organizar el contenido del servidor de informes. Puede agregarse contenido a una carpeta, mover elementos entre carpetas, modificar los nombres o las ubicaciones de las carpetas y eliminar carpetas que hayan dejado de ser necesarias.  
  
 Las carpetas son contenedores virtuales para los elementos publicados a los que se accede desde el Generador de informes o mediante una conexión del explorador al servidor de informes. Ni las carpetas ni su contenido existen en realidad en un sistema de archivos. En lugar de ello, se almacenan en la base de datos del servidor de informes; el acceso a las carpetas y su contenido se obtiene a través del extremo de servicios web del servidor de informes. El espacio de nombres de las carpetas del servidor de informes es una jerarquía con un nodo raíz, carpetas predefinidas y carpetas definidas por el usuario. El espacio de nombres identifica de forma exclusiva los elementos almacenados en un servidor de informes. Proporciona un esquema de direcciones para especificar elementos en una dirección URL. Al seleccionar o buscar un informe, la ruta de acceso de la carpeta pasa a formar parte de la dirección URL del informe.  
  
 El modo que adopte para trabajar con las carpetas dependerá de las tareas de su asignación de roles. Si usa la seguridad predeterminada, solo los administradores de contenido y los publicadores podrán crear y administrar carpetas. Si utiliza asignaciones de roles personalizados, deberán incluir las tareas compatibles con la administración de carpetas. Para obtener más información sobre asignaciones de roles y tareas, vea [Conceder permisos en un servidor de informes en modo nativo](../../reporting-services/security/granting-permissions-on-a-native-mode-report-server.md) y [Tareas y permisos](../../reporting-services/security/tasks-and-permissions.md).  
  
 Las carpetas del servidor de informes pueden contener los elementos siguientes:  
  
-   Informes  
  
-   Orígenes de datos compartidos  
  
-   Conjuntos de datos compartidos  
  
-   Elementos de informe  
  
-   KPI  
  
-   Mobile Reports (Informes móviles)  
  
-   Recursos (elementos que se almacenan, pero no se procesan, en un servidor de informes)  
  
-   Otras carpetas  
  
### <a name="reserved-folders"></a>Carpetas reservadas  
 Las carpetas predefinidas están reservadas por Reporting Services; no se pueden mover, cambiar de nombre ni eliminar. Las carpetas definidas por el usuario son todas las carpetas creadas por un usuario o un administrador del servidor de informes con permiso para agregar elementos a una carpeta.  
  
 En la siguiente tabla, se describen las carpetas predefinidas que fijan la jerarquía de carpetas y proporcionan un marco para varias características.  
  
|Carpeta|Finalidad|  
|------------|-------------|  
|Inicio|Nodo raíz de la jerarquía de carpetas.|  
|Usuarios|Esta carpeta aparece cuando se habilita la característica Mis informes. Contiene subcarpetas para todos los usuarios que utilizan la característica Mis informes, y solo los administradores del servidor de informes tienen acceso a ella. El nombre de cada subcarpeta coincide con el de un usuario.|  
|Mis informes|Proporciona un área de trabajo personal para cada usuario.|  
  
### <a name="creating-folders"></a>Crear carpetas  
 Puede crear una carpeta en cualquier carpeta disponible de la jerarquía.  
  
 Si está creando las carpetas con el propósito de restringir el acceso a informes y modelos concretos, debería especificar asignaciones de roles que les permitan a los usuarios examinar, pero no ver el contenido de, las carpetas primarias que se encuentran en la ruta de la carpeta.  
  
### <a name="modifying-folder-properties"></a>Modificar las propiedades de carpetas  
 Una vez que haya creado la carpeta, puede modificar sus propiedades para cambiarle el nombre, agregar o modificar una descripción, o mover la carpeta a otra ubicación. Estas propiedades están disponibles desde la página de propiedades General de la carpeta. Para obtener más información sobre cómo establecer las propiedades que conceden acceso a una carpeta, vea [Proteger carpetas](../../reporting-services/security/secure-folders.md).  
  
### <a name="deleting-folders-and-folder-contents"></a>Eliminar carpetas y su contenido  
 Al eliminar una carpeta, también se eliminan todos los elementos que contiene. Antes de eliminar una carpeta, debería revisar el contenido para decidir si incluye elementos a los que hacen referencia otros elementos o que utilizan otros elementos de la jerarquía de carpetas. Entre los elementos a los que se hace referencia, figuran las definiciones de informe compatibles con informes vinculados, orígenes de datos compartidos y recursos.  
  
 Si elimina un informe al que hacen referencia uno o más informes vinculados, éstos dejarán de ser válidos una vez eliminado el informe en cuestión. No es posible determinar por adelantado los informes vinculados que se verán afectados porque los informes no conservan información sobre los informes vinculados que se basan en ellos. En cambio, sí que es posible revisar las propiedades de un informe vinculado para determinar el informe en el que se basa. Por su parte, los elementos de orígenes de datos compartidos incluyen una lista de todos los informes que utilizan actualmente el elemento para que pueda determinar con facilidad si la información de conexión está en uso o no. Para obtener más información, vea [Crear, modificar y eliminar orígenes de datos compartidos &#40;SSRS&#41;](../../reporting-services/report-data/create-modify-and-delete-shared-data-sources-ssrs.md). Por último, los recursos que utilizan los informes no los identifican.  
  
 Antes de eliminar una carpeta, es preciso considerar si es necesario conservar el historial del informe de alguno de los informes que vaya a eliminar o una construcción de informe específica (como las suscripciones controladas por datos) que forme parte del informe. Si necesita alguna de estas informaciones, quite el elemento de la carpeta antes de eliminarla.  
  
 La visibilidad de un elemento en una carpeta depende de las asignaciones de roles (es decir, el permiso para ver un elemento) y de las opciones de visualización establecidas para la carpeta. En el Administrador de informes, se puede configurar la página Contenido como vista de lista o como vista de detalles. En algunos casos, un informe o un elemento puede estar oculto en una vista de lista. Es aconsejable ver una carpeta con la vista de detalles antes de eliminar su contenido.  
  
##  <a name="bkmk_Resources"></a> Recursos  
 Un recurso es un elemento administrado que se almacena en un servidor de informes pero no se procesa allí. Normalmente, un recurso proporciona contenido externo a los usuarios de los informes. Algunos ejemplos son una imagen de un archivo .jpg, un archivo de forma ESRI que contiene datos espaciales o un archivo HTML que describe las reglas de negocios usadas en un informe. El archivo JPG, SHP o HTML está almacenado en el servidor de informes, pero el servidor de informes pasa el archivo directamente al explorador en lugar de procesarlo primero. Para obtener más información, vea [Imágenes &#40;Generador de informes y SSRS&#41;](../../reporting-services/report-design/images-report-builder-and-ssrs.md) y la sección "Agregar datos a un mapa" en [Mapas &#40;Generador de informes y SSRS&#41;](../../reporting-services/report-design/maps-report-builder-and-ssrs.md).  
  
### <a name="adding-and-viewing-a-resource"></a>Agregar y ver un recurso  
 Para agregar un recurso a un servidor de informes, se carga o se publica un archivo:  
  
|Operación|Tipo de archivo|  
|---------------|---------------|  
|Cargar|Para cargar un recurso, debe usar el Administrador de informes si el servidor de informes se ejecuta en modo nativo o una página de aplicación de un sitio de SharePoint si el servidor se ejecuta en el modo integrado con SharePoint. Para más información, vea [Cargar un archivo o un informe &#40;Administrador de informes&#41;](../../reporting-services/reports/upload-a-file-or-report-report-manager.md) y [Cargar documentos en una biblioteca de SharePoint &#40;Reporting Services en modo de SharePoint&#41;](../../reporting-services/report-server-sharepoint/upload-documents-to-a-sharepoint-library-reporting-services-in-sharepoint-mode.md).|  
|Publicar|Todos los archivos de un proyecto que no son informes, elementos de informe, orígenes de datos o conjuntos de datos se cargan como recursos. Para publicar un recurso, agregue un elemento existente a un proyecto en el Diseñador de informes y, a continuación, publique el proyecto en un servidor de informes.|  
  
 Todos los recursos se originan como archivos en un sistema de archivos, que se cargan posteriormente en un servidor de informes. Excepto para las limitaciones de tamaño de archivo predeterminadas de 4 megabytes impuestas por ASP.NET, no hay ninguna restricción en los tipos de archivos que se pueden cargar. Sin embargo, cuando se publica en un servidor de informes como un recurso, los tipos de archivos que tienen tipos MIME equivalentes resultan más óptimos que otros. Por ejemplo, los recursos que se basan en archivos HTML o JPG se abren en una ventana de explorador cuando el usuario hace clic en el recurso, representándose el archivo HTML como una página web y el archivo JPG como una imagen que el usuario puede ver. Por el contrario, los recursos que no tienen tipos MIME equivalentes, como archivos de aplicación de escritorio, por ejemplo, no se pueden representar en la ventana del explorador.  
  
 Si un recurso puede ser visto o no por los usuarios de los informes depende de las opciones de visualización del explorador. Dado que los recursos no se procesan por el servidor de informes, el explorador debe proporcionar la capacidad de visualización para representar un tipo MIME concreto. Si el explorador no puede representar el contenido, los usuarios que vean el recurso solamente podrán ver las propiedades generales del recurso.  
  
### <a name="securing-and-managing-a-resource"></a>Proteger y administrar un recurso  
 Los recursos existen junto con informes, orígenes de datos compartidos, programaciones compartidas y carpetas como elementos con nombre en la jerarquía de carpetas del servidor de informes. Puede buscar, ver, proteger y establecer propiedades en los recursos de la misma manera que lo haría con cualquier elemento almacenado en un servidor de informes. Para ver o administrar un recurso, debe tener las tareas Ver recursos o Administrar recursos en su asignación de roles.  
  
### <a name="referencing-an-image-resource-from-a-report"></a>Hacer referencia a un recurso de imagen desde un informe  
 Los recursos pueden contener una imagen a la que hace referencia en un informe. Si entre los requisitos de informe se incluye el uso de imágenes externas, piense en las ventajas siguientes de almacenar la imagen como un recurso:  
  
-   Almacenamiento centralizado en la base de datos del servidor de informes. Si mueve la base de datos del servidor de informes y su contenido a otro equipo, la imagen externa permanece con el informe. No tiene que realizar un seguimiento de los archivos de imagen almacenados en disco en equipos diferentes.  
  
-   Se protege a través de las asignaciones de roles en lugar de la seguridad del sistema de archivos. Los mismos permisos que se usan para ver un informe se pueden aplicar al recurso. Por el contrario, si almacena la imagen en disco, debe asegurarse de que la cuenta de usuario anónimo o la cuenta de ejecución desatendida tienen permiso para tener acceso al archivo.  
  
 Para usar un recurso de imagen de un informe, agregue el archivo de imagen al proyecto y publíquelo junto con el informe. Una vez publicada la imagen, puede actualizar la referencia de la imagen en el informe de manera que señale al recurso del servidor de informes y, a continuación, vuelva a publicar únicamente el informe para guardar sus cambios. Puede actualizar ahora la imagen posteriormente con independencia del informe volviendo a publicar el recurso. El informe usa la versión más actual de la imagen disponible en el servidor de informes.  
  
 Para obtener más información, vea [Actualizar un recurso &#40;Administrador de informes&#41;](../../reporting-services/report-server/update-a-resource-report-manager.md).  
  
##  <a name="bkmk_MyReports"></a> Mis informes  
 La carpeta Mis informes es un área de trabajo personal para cada usuario que inicia una sesión en el servidor de informes con una cuenta de dominio válida. Esta carpeta especial ofrece un espacio de almacenamiento para los informes que están en curso y que no se han concebido para una distribución amplia, o para informes que se han modificado para adaptarlos a alguna necesidad especial. No es posible restringir el número o el tamaño de elementos que se almacenan en una carpeta Mis informes, ni tampoco configurar la carpeta para el uso compartido entre usuarios.  
  
 Desde el punto de vista técnico, Mis informes asigna el nombre de una carpeta virtual que ve cada usuario (Mis informes) a una carpeta maestra Carpetas de usuarios y a una subcarpeta única basada en el nombre del usuario. Cuando un usuario tiene acceso a su carpeta Mis informes, lo que sucede realmente es que es redireccionado a la subcarpeta de Carpetas de usuarios que tiene asignada. Cada subcarpeta ofrece espacio de almacenamiento para los informes y elementos que el usuario agrega a su carpeta Mis informes. En el portal web, no verá Mis informes en el nivel raíz. Deberá profundizar en la carpeta Usuarios.  
  
 La carpeta Carpetas de usuarios se crea al instalar el servidor de informes. Las subcarpetas de usuario posteriores se crean cada vez que un usuario abre por primera vez Mis informes (por ejemplo, al hacer clic en Mis informes en el Administrador de informes). El nombre de cada carpeta adopta el siguiente formato:  
  
```  
/Users Folders/<username>/My Reports  
```  
  
 Únicamente pueden asignarse carpetas a los usuarios con cuentas de sistema válidas. Si un nombre de usuario contiene caracteres especiales, la carpeta se creará con caracteres de escape equivalentes. En la siguiente tabla encontrará una lista de los caracteres de escape equivalentes.  
  
|Carácter|Valor de escape|Ejemplo|  
|---------------|------------------|-------------|  
|(espacio)|[ ]|*Nombre Apellido* se convierte en *Nombre[ ]Apellido*|  
|\ (barra diagonal inversa)|Se sustituye por un carácter de espacio simple.|*nombreDeDominio\nombreDeUsuario* se convierte en *nombreDeDominio nombreDeUsuario*|  
|@ (arroba)|[arroba]|*nombreDeUsuario*@hotmail.com se convierte en *nombreDeUsuario*[arroba]hotmail.com|  
|& (y comercial)|[y comercial]|*nombreDeUsuario*@*empresa*&*empresa.com* se convierte en *nombreDeUsuario*[arroba]*empresa*[y comercial]*empresa.com*|  
|$ (signo de moneda)|[signo de moneda]|*Usuario* $*Nombre* se convierte en *Usuario*[ ][dólar]*Nombre*|  
  
 La característica Mis informes es opcional. Cuando se instala un servidor de informes, la característica Mis informes está deshabilitada de forma predeterminada. Para obtener más información sobre cómo habilitar esta característica, vea [Habilitar y deshabilitar Mis informes](../../reporting-services/report-server/enable-and-disable-my-reports.md). Para obtener más información, vea [Proteger Mis informes](../../reporting-services/security/secure-my-reports.md).  
  
## <a name="tasks"></a>Tareas  
 [Cargar archivos a una carpeta](../../reporting-services/report-server/upload-files-to-a-folder.md)  
  
 [Crear, eliminar o modificar una carpeta &#40;Administrador de informes&#41;](../../reporting-services/report-server/create-delete-or-modify-a-folder-report-manager.md)  
  
 [Actualizar un recurso &#40;Administrador de informes&#41;](../../reporting-services/report-server/update-a-resource-report-manager.md)  
  
 [Cargar archivos a una carpeta](../../reporting-services/report-server/upload-files-to-a-folder.md)  
  
## <a name="see-also"></a>Vea también  
 [Herramientas de Reporting Services](../../reporting-services/tools/reporting-services-tools.md)   
 [Roles y permisos &#40;Reporting Services&#41;](../../reporting-services/security/roles-and-permissions-reporting-services.md)   
 [Informes de Reporting Services &#40;SSRS&#41;](../../reporting-services/reports/reporting-services-reports-ssrs.md)  
  
  
