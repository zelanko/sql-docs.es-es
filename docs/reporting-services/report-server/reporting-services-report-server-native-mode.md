---
title: Servidor de informes de Reporting Services (modo nativo) | Microsoft Docs
ms.date: 03/15/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.technology: report-server
ms.suite: pro-bi
ms.topic: conceptual
helpviewer_keywords:
- administering Reporting Services
- administering [Reporting Services]
- Reporting Services, administration
ms.assetid: fa0d84e2-4c21-432c-aa7c-23517da75253
author: markingmyname
ms.author: maghan
ms.openlocfilehash: c80762b7abee1913cd7f671f8fd676bd49d57618
ms.sourcegitcommit: d96b94c60d88340224371926f283200496a5ca64
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/30/2018
ms.locfileid: "43272598"
---
# <a name="reporting-services-report-server-native-mode"></a>Servidor de informes de Reporting Services (modo nativo)
  Un servidor de informes configurado para el modo nativo se ejecuta como un servidor de aplicaciones que proporciona todas las funcionalidades de procesamiento y administración exclusivamente a través de los componentes de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)].  
  
 Puede usar [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] o el Administrador de informes para administrar informes de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] . Use el administrador de configuración de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] para administrar un servidor de informes en modo nativo.  
  
 Si el servidor de informes está configurado para el modo de SharePoint, debe usar las páginas de administración de contenido del sitio de SharePoint para administrar informes, orígenes de datos compartidos y otros elementos del servidor de informes.  
  
 Este tema contiene la información siguiente:  
  
-   [Resumen del modo nativo](#bkmk_sum)  
  
-   [Administrar contenido](#bkmk_managecontent)  
  
-   [Proteger y administrar un recurso](#bkmk_manageresources)  
  
-   [Hacer referencia a un recurso de imagen desde un informe](#bkmk_referenceimage)  
  
##  <a name="bkmk_sum"></a> Resumen del modo nativo  
 Una instalación del modo nativo de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] consta de varias características de servidor que es necesario administrar y mantener. Entre estas características figuran las siguientes:  
  
-   El servicio web del servidor de informes, que se ejecuta dentro del servicio del servidor de informes.  
  
-   Las aplicaciones de procesamiento en segundo plano, que controlan las operaciones programadas y la entrega de informes.  
  
-   La base de datos del servidor de informes.  
  
 Para administrar por completo una instalación de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] , debe disponer de los siguientes permisos:  
  
-   Pertenencia al grupo local de administradores en el equipo del servidor de informes. Si la instalación incluye características de servidor que se ejecutan en equipos remotos, debe tener permisos de administrador en dichos equipos si desea administrar esos servidores a través de una conexión remota.  
  
-   Permisos de administrador de base de datos para la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que hospeda la base de datos.  
  
-   Si va a instalar [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] en un controlador de dominio, debe ser un administrador de dominio.  
  
##  <a name="bkmk_managecontent"></a> Administrar contenido  
 En [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)], la administración del contenido hace referencia a la administración de informes, modelos, carpetas, recursos y orígenes de datos compartidos. Es posible administrar todos estos elementos de un modo independiente mediante la configuración de las propiedades y de la seguridad. Cualquier elemento puede moverse a una ubicación diferente en el espacio de nombres de carpetas del servidor de informes. Para administrar estos elementos de un modo eficaz, necesita saber las tareas que realiza un administrador de contenido.  
  
> [!NOTE]  
>  La administración de contenido es diferente de la administración de servidores de informes. Para más información sobre cómo administrar el entorno donde se ejecuta un servidor de informes, vea [Configuración y administración de un servidor de informes &#40;modo de SharePoint de Reporting Services&#41;](../../reporting-services/report-server-sharepoint/configuration-and-administration-of-a-report-server.md).  
  
 La administración de contenido comprende las tareas que se describen a continuación:  
  
-   Proteger el sitio del servidor de informes y los elementos con la aplicación de la seguridad basada en roles que ofrece [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)].  
  
-   Estructurar la jerarquía de carpetas del servidor de informes mediante la inclusión, modificación o eliminación de carpetas.  
  
-   Establecer valores predeterminados y propiedades aplicables a los elementos que administra el servidor de informes. Por ejemplo, puede establecer valores máximos básicos que determinen las directivas de almacenamiento del historial del informe.  
  
-   Crear elementos de orígenes de datos compartidos para utilizar en lugar de las conexiones de orígenes de datos específicos del informe. Un publicador o administrador de contenido puede seleccionar un origen de datos distinto del definido originalmente para un informe, como por ejemplo, para sustituir una referencia a una base de datos de prueba con una referencia a una base de datos de producción.  
  
-   Crear programaciones compartidas que se pueden usar en lugar de las programaciones específicas de informes y de suscripciones, facilitando el mantenimiento de la información de programación con el tiempo.  
  
-   Crear suscripciones controladas por datos que generen listas de destinatarios a partir de los datos obtenidos de un almacén de datos.  
  
-   Equilibrar las peticiones de procesamiento de informes que se envían al servidor mediante la programación del procesamiento de informes y la especificación de los informes que pueden ejecutarse a petición y de los que se cargan desde la memoria caché.  
  
 El permiso para realizar tareas de administración se proporciona a través de dos roles predefinidos: **Administrador del sistema** y **Administrador de contenido**. La administración efectiva del contenido del servidor de informes requiere que esté asignado a ambos roles. Para más información sobre estos roles predefinidos, vea [Roles y permisos &#40;Reporting Services&#41;](../../reporting-services/security/roles-and-permissions-reporting-services.md).  
  
 Las herramientas para administrar contenido del servidor de informes son [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] o el Administrador de informes. [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] permite establecer valores predeterminados y habilitar características. El Administrador de informes se usa para conceder acceso de usuario a las operaciones y elementos del servidor de informes, ver y usar informes y otros tipos de contenido, y ver y usar todos los elementos compartidos y características de distribución de informes.  
  
##  <a name="bkmk_manageresources"></a> Proteger y administrar un recurso  
 Un recurso es un elemento administrado que se almacena en un servidor de informes pero no se procesa allí. Normalmente, un recurso proporciona contenido externo a los usuarios de los informes. Entre los ejemplos se incluye una imagen en un archivo .jpg o un archivo HTML que describe las reglas de negocios usadas en un informe. El archivo JPG o HTML está almacenado en el servidor de informes, pero el servidor de informes pasa el archivo directamente al explorador en lugar de procesarlo primero.  
  
 Para agregar un recurso a un servidor de informes, se carga o se publica un archivo:  
  
|Operación|Tipo de archivo|  
|---------------|---------------|  
|Cargar|Todos los archivos se cargan como recursos excepto los archivos de definición de informe (.rdl) y los de modelo de informe (.smdl).<br /><br /> Para cargar un recurso, debe usar el Administrador de informes si el servidor de informes se ejecuta en modo nativo o una página de aplicación de un sitio de SharePoint si el servidor se ejecuta en el modo integrado con SharePoint. Para más información, vea [Cargar un archivo o un informe &#40;Administrador de informes&#41;](../../reporting-services/reports/upload-a-file-or-report-report-manager.md) y [Cargar documentos en una biblioteca de SharePoint &#40;Reporting Services en modo de SharePoint&#41;](../../reporting-services/report-server-sharepoint/upload-documents-to-a-sharepoint-library-reporting-services-in-sharepoint-mode.md).|  
|Publicar|Todos los archivos de un proyecto se cargan como recursos salvo los archivos de origen de datos .rdl, .smdl y .rds. Para publicar un recurso, agregue un elemento existente a un proyecto en el Diseñador de informes y, a continuación, publique el proyecto en un servidor de informes.|  
  
 Todos los recursos se originan como archivos en un sistema de archivos, que se cargan posteriormente en un servidor de informes. Excepto para las limitaciones de tamaño de archivo predeterminadas de 4 megabytes impuestas por ASP.NET, no hay ninguna restricción en los tipos de archivos que se pueden cargar. Sin embargo, cuando se publica en un servidor de informes como un recurso, los tipos de archivos que tienen tipos MIME equivalentes resultan más óptimos que otros. Por ejemplo, los recursos que se basan en archivos HTML o JPG se abren en una ventana de explorador cuando el usuario hace clic en el recurso, representándose el archivo HTML como una página web y el archivo JPG como una imagen que el usuario puede ver. Por el contrario, los recursos que no tienen tipos MIME equivalentes, como archivos de aplicación de escritorio, por ejemplo, no se pueden representar en la ventana del explorador.  
  
 Si un recurso puede ser visto o no por los usuarios de los informes depende de las opciones de visualización del explorador. Dado que los recursos no se procesan por el servidor de informes, el explorador debe proporcionar la capacidad de visualización para representar un tipo MIME concreto. Si el explorador no puede representar el contenido, los usuarios que vean el recurso solamente podrán ver las propiedades generales del recurso.  
  
 Los recursos existen junto con informes, orígenes de datos compartidos, programaciones compartidas y carpetas como elementos con nombre en la jerarquía de carpetas del servidor de informes. Puede buscar, ver, proteger y establecer propiedades en los recursos de la misma manera que lo haría con cualquier elemento almacenado en un servidor de informes. Para ver o administrar un recurso, debe tener las tareas Ver recursos o Administrar recursos en su asignación de roles.  
  
##  <a name="bkmk_referenceimage"></a> Hacer referencia a un recurso de imagen desde un informe  
 Los recursos pueden contener una imagen a la que hace referencia en un informe. Si entre los requisitos de informe se incluye el uso de imágenes externas, piense en las ventajas siguientes de almacenar la imagen como un recurso:  
  
-   Almacenamiento centralizado en la base de datos del servidor de informes. Si mueve la base de datos del servidor de informes y su contenido a otro equipo, la imagen externa permanece con el informe. No tiene que realizar un seguimiento de los archivos de imagen almacenados en disco en equipos diferentes.  
  
-   Se protege a través de las asignaciones de roles en lugar de la seguridad del sistema de archivos. Los mismos permisos que se usan para ver un informe se pueden aplicar al recurso. Por el contrario, si almacena la imagen en disco, debe asegurarse de que la cuenta de usuario anónimo o la cuenta de ejecución desatendida tienen permiso para tener acceso al archivo.  
  
 Para usar un recurso de imagen de un informe, agregue el archivo de imagen al proyecto y publíquelo junto con el informe. Una vez publicada la imagen, puede actualizar la referencia de la imagen en el informe de manera que señale al recurso del servidor de informes y, a continuación, vuelva a publicar únicamente el informe para guardar sus cambios. Puede actualizar ahora la imagen posteriormente con independencia del informe volviendo a publicar el recurso. El informe usa la versión más actual de la imagen disponible en el servidor de informes.  
  
## <a name="see-also"></a>Ver también  
 [Configurar y administrar un servidor de informes &#40;modo nativo de SSRS&#41;](../../reporting-services/report-server/configure-and-administer-a-report-server-ssrs-native-mode.md)   
 [Solución de problemas en una instalación de Reporting Services](../../reporting-services/install-windows/troubleshoot-a-reporting-services-installation.md)  
  
  
