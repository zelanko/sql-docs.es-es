---
title: Referencia de permisos de sitio y lista de SharePoint para los elementos del servidor de informes | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- permissions [Reporting Services], SharePoint integrated mode
- SharePoint integration [Reporting Services], permissions
- security [Reporting Services], SharePoint integrated mode
- permission sets [Reporting Services]
ms.assetid: 1fcb27bd-4c4a-43f4-bfff-e42a59c87c49
author: markingmyname
ms.author: maghan
manager: kfile
ms.openlocfilehash: 2a05787e4e06c7cf178c2618e2fbfbac4de596cd
ms.sourcegitcommit: dfb1e6deaa4919a0f4e654af57252cfb09613dd5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/11/2019
ms.locfileid: "56035066"
---
# <a name="sharepoint-site-and-list-permission-reference-for-report-server-items"></a>Referencia de permisos de sitio y lista de SharePoint para los elementos del servidor de informes
  En este tema se proporciona una referencia de los permisos de SharePoint que se pueden usar para conceder acceso a las operaciones del servidor de informes para un servidor de informes que se ejecuta en el modo integrado de SharePoint. Si va a crear niveles de permisos personalizados, este tema puede ayudarle a elegir qué permisos usar.  
  
 SharePoint proporciona treinta y tres permisos que puede usar para controlar el acceso al contenido y a las operaciones. No todos estos permisos se aplican a los documentos y a las operaciones en las que interviene el servidor de informes de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] . Puede usar las tablas de referencia de permisos de este artículo para saber qué permisos son compatibles con determinadas tareas de informes.  
  
 Cada tabla comienza por una lista de los permisos de SharePoint y una descripción. La tabla incluye tres columnas que indican cómo se usa un permiso en niveles de permiso predefinidos. Entre los niveles de permisos predefinidos se incluyen los siguientes:  
  
|Nivel del permiso|Abreviatura|  
|----------------------|------------------|  
|Control total|**F**|  
|Contribuir|**C**|  
|Visitante|**V**|  
  
 Los permisos que no afectan a un servidor de informes no se muestran en esta referencia. Todos los permisos de personalización se excluyen de este artículo de referencia. Aunque puede incluir elementos del servidor de informes en un sitio web personalizado, el servidor de informes no controla directamente las operaciones o solicitudes de personalización.  
  
||  
|-|  
|[!INCLUDE[applies](../../includes/applies-md.md)]<br /><br /> [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] Modo de SharePoint &#124; SharePoint 2010 y SharePoint 2013.|  
  
## <a name="list-permissions"></a>Permisos de lista  
 Los permisos que se establecen en la biblioteca que contiene los elementos del servidor de informes determinan la forma en que los usuarios obtienen acceso a dichos elementos.  
  
|Permiso|Descripción|F|C|V|Operación del servidor de informes|  
|----------------|-----------------|-------|-------|-------|-----------------------------|  
|Administrar listas|Crear y eliminar listas, agregar o quitar columnas de una lista y agregar o quitar vistas públicas de una lista.|X|||Crear una carpeta en una biblioteca de SharePoint durante una operación de publicación desde una herramienta de creación. También se requiere este permiso para administrar el historial de informes.|  
|Agregar elementos|Agregar elementos a listas, agregar documentos a bibliotecas de documentos y agregar comentarios de discusión web.|X|X||Agregar informes, modelos de informe, orígenes de datos compartidos y recursos (archivos de imagen externos) a bibliotecas de SharePoint. Crear orígenes de datos compartidos. Generar modelos de informe a partir de orígenes de datos compartidos. Iniciar el Generador de informes y crear un nuevo informe o cargar un modelo en el Generador de informes.|  
|Editar elementos|Editar elementos en listas, editar documentos en bibliotecas de documentos, editar comentarios de discusión web en documentos y personalizar páginas de elementos web en bibliotecas de documentos.<br /><br /> Crear suscripciones y editar suscripciones que ha creado.|X|X||Ver las versiones anteriores de un documento, incluidas las instantáneas del historial de informes. Modifican las propiedades de los elementos de los informes y otros documentos. Establecer opciones de procesamiento de informes. Establecer parámetros en un informe. Editar propiedades de orígenes de datos. Crear instantáneas del historial del informes. Abrir un modelo de informe o un informe basado en un modelo en el Generador de informes y guardar sus cambios en el archivo. Asignar informes click-through a entidades en un modelo. Reemplazar una definición de informe, origen de datos compartido, modelo de informe o recurso por una versión más reciente (reemplazar archivo, conservar metadatos). Administrar elementos dependientes a los que se hace referencia en un informe o modelo. Personalizar el elemento web Visor de informes relativo a un informe específico.<br /><br /> Crear, cambiar y eliminar suscripciones que usen las extensiones de entrega de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] para entregar informes en ubicaciones de destino. Tan solo el propietario y los usuarios de la suscripción con el permiso Administrar alertas pueden realizar estas acciones.|  
|Eliminar elementos|Eliminar elementos de una lista, documentos de una biblioteca de documentos y comentarios de discusión web en documentos.|X|X||Eliminar informes, modelos de informe, orígenes de datos compartidos y otros documentos de una biblioteca.|  
|Ver elementos|Ver elementos en listas, documentos en bibliotecas de documentos y comentarios de discusión web.|X|X|X|Abrir un informe, modelo de informe u otro documento y procesarlo en el servidor de informes.|  
|Abrir elementos|Ver el origen de los documentos con identificadores de archivos del servidor.|X|X|X|Ver una lista de orígenes de datos compartidos. Descargar una copia del archivo de origen para una definición de informe o modelo de informe. Ver los informes click-through que usan un modelo de informe como origen de datos.|  
|Ver versiones|Ver las versiones anteriores de un documento o elemento de lista.|X|X|X|Ver las versiones anteriores de un documento e instantáneas de informe.|  
|Eliminar versiones|Eliminar las versiones anteriores de un documento o elemento de lista.|X|X||Eliminar las versiones anteriores de un documento e instantáneas de informe.|  
  
> [!NOTE]  
>  Otros permisos de lista son Omitir desprotección, Aprobar elementos y Ver páginas de aplicaciones. El servidor de informes no evalúa estos permisos. El servidor de informes no controla estas operaciones.  
  
## <a name="site-permissions"></a>Permisos de sitio  
 Los permisos de sitio determinan el acceso a las operaciones del servidor de informes que no están directamente relacionadas con los elementos almacenados en una biblioteca específica. Entre los ejemplos se incluye la creación y administración de programaciones compartidas, que los elementos pueden usar en varias bibliotecas, y la configuración del elemento web Visor de informes, que se puede usar en todo un sitio.  
  
|Permiso|Descripción|F|C|V|Operación del servidor de informes|  
|----------------|-----------------|-------|-------|-------|-----------------------------|  
|Administrar permisos|Crear y cambiar niveles de permiso en el sitio web y asignar permisos a usuarios y grupos.|X|||Puede cambiar los permisos de todos los elementos y operaciones del servidor de informes. Puede establecer la seguridad de elementos de modelo.|  
|Administración del sitio web|Realizar todas las tareas de administración para el sitio web y administrar el contenido.|X|||Crear, modificar y eliminar programaciones compartidas.|  
|Agregar y personalizar páginas|Agregar, modificar o eliminar páginas HTML o páginas de elementos web y editar el sitio web con un editor compatible con [!INCLUDE[winSPServ](../../includes/winspserv-md.md)].|X|||Agregar o quitar un elemento web Visor de informes.|  
|Examinar información de usuario|Vea información sobre los usuarios del sitio web.|X|X|X|Examinar informes y otros elementos en distintos sitios, bibliotecas y carpetas. Publicar informes y otros elementos en una biblioteca.|  
|Enumerar permisos|Enumerar permisos en el sitio web, lista, carpeta, documento o elemento de lista.|X|||Leer permisos para todos los elementos del servidor de informes. Ver un informe click-through que use un modelo de informe que contenga la configuración de seguridad de los elementos de un modelo.|  
|Administrar alertas|Administrar alertas para todos los usuarios del sitio web.|X|||Crear, modificar y eliminar cualquier suscripción en un sitio.|  
|Utilizar interfaces remotas|Usar las interfaces de SOAP, Web DAV o SharePoint Designer para tener acceso al sitio web.|X|X|X|Se usa para llamar al extremo proxy de dirección URL del servidor de informes.|  
|Abrir|Abrir un sitio web, una lista o una carpeta para obtener acceso a los elementos incluidos en dicho contenedor.|X|X|X|Leer programaciones y propiedades de elementos.|  
  
## <a name="see-also"></a>Vea también  
 [Comparar roles y tareas de Reporting Services con grupos y permisos de SharePoint](../reporting-services-roles-tasks-vs-sharepoint-groups-permissions.md)   
 [Concesión de permisos sobre elementos del servidor de informes en un sitio de SharePoint](granting-permissions-on-report-server-items-on-a-sharepoint-site.md)  
  
  
