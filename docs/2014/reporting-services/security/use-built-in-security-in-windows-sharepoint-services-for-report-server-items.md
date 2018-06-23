---
title: Usar la seguridad integrada de Windows SharePoint Services para los elementos del servidor de informes | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- reporting-services-native
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- permissions [Reporting Services], SharePoint integrated mode
- SharePoint integration [Reporting Services], permissions
- security [Reporting Services], SharePoint integrated mode
ms.assetid: 9577e88d-c22b-4934-936f-e0f1400cedf5
caps.latest.revision: 13
author: markingmyname
ms.author: maghan
manager: mblythe
ms.openlocfilehash: 4d9231800ea1cf583ae554fe10ecc217fa1e9a49
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36111498"
---
# <a name="use-built-in-security-in-windows-sharepoint-services-for-report-server-items"></a>Usar la seguridad integrada de Windows SharePoint Services para los elementos del servidor de informes
  SharePoint proporciona características de seguridad integradas que se pueden usar para tener acceso a elementos del servidor de informes desde bibliotecas y sitios de SharePoint. Si ya asignó permisos de sitio y lista a los usuarios, dichos usuarios tendrán acceso a los elementos y las operaciones del servidor de informes inmediatamente después de configurar la integración entre SharePoint y un servidor de informes.  
  
## <a name="securable-items"></a>Elementos protegibles  
 Los permisos definidos en el sitio o la biblioteca se pueden usar para conceder acceso a los elementos del servidor de informes. Sin embargo, si desea proteger elementos concretos, puede establecer permisos para los siguientes tipos de contenido:  
  
|Tipo de archivo|Descripción|  
|---------------|-----------------|  
|.rdl|Un archivo de definición de informe que define el diseño del informe y los comandos usados para recuperar datos. Una definición de informe usa información sobre la conexión del origen de datos para recuperar datos al procesar el informe. Si la definición del informe es un informe ad hoc que se creó en el Generador de informes, el informe se empareja con un archivo de modelo de informe (.smdl) que define el ámbito de exploración de datos en el informe representado.|  
|.smdl|Un archivo de modelo de informe que describe las estructuras de datos y cómo se relacionan. Se usa para crear y ejecutar informes del Generador de informes.|  
|.rsds|Un archivo de origen de datos compartido que especifica la información de conexión a un origen de datos externo. Lo usan los archivos de definiciones de informes (.rdl) y de modelo de informe (.smdl). Los modelos de informe siempre usan archivos .rsds para obtener información de conexión a un origen de datos subyacente. Las definiciones de informe pueden usar archivos .rsds o la información de conexión definida en las propiedades del origen de datos en el informe.|  
|.rsc|Archivo de elementos de informe que define el diseño y la estructura de un elemento de informe o región de datos. Se utiliza para publicar el elemento de informe en un servidor de modo que otros autores de informes puedan reutilizarlo en la Galería de elementos de informe.|  
|.rsd|Archivo de conjunto de datos compartido que define la sintaxis de consulta y las propiedades de un conjunto de datos. Los conjuntos de datos compartidos se pueden compartir, almacenar, procesar y guardar en la memoria caché desde un informe.|  
  
 Las programaciones, las suscripciones y el historial del informe son elementos protegibles. Puede establecer permisos para el sitio o la biblioteca que determinen si un usuario puede crear o usar programaciones, suscripciones y el historial del informe, pero no puede proteger dichos elementos directamente.  
  
 Para proteger elementos concretos, seleccione el elemento en la biblioteca, haga clic en la flecha hacia abajo y seleccione **Administrar permisos**. En el menú **Acciones** , seleccione **Editar permisos**.  
  
## <a name="using-built-in-groups-and-permission-levels-to-access-report-server-items"></a>Usar niveles de permiso y grupos integrados para el acceso a los elementos del servidor de informes  
 Cuando se usa la herencia de permisos y los grupos de SharePoint estándar, se tiene acceso a la mayoría de las operaciones del servidor de informes inmediatamente después de configurarse la integración en el servidor de informes e instancias de SharePoint.  
  
 SharePoint proporciona grupos estándar que se asignan a niveles de permisos predefinidos que determinan el acceso a los documentos y las páginas de un sitio de SharePoint. Si está usando grupos estándar y niveles de permiso predeterminados, y los sitios están configurados para heredar permisos, es de esperar que trabajará con las características de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] de las siguientes formas:  
  
|**Grupos de SharePoint**|**Nivel del permiso**|**Resumen**|**Acceso al servidor de informes**|  
|---------------------------|--------------------------|-----------------|------------------------------|  
|**Propietarios**|Control total|Los propietarios tienen permiso total para crear, administrar y proteger los elementos y operaciones del servidor de informes.|Establecen los permisos que controlan el acceso a todos los elementos del servidor de informes almacenados en las bibliotecas del sitio. Establecen los permisos dentro de un modelo de informe (también llamado seguridad de elementos de modelo). Personalizan un elemento web Visor de informes. Agregan informes y otros elementos a las bibliotecas. Modifican las propiedades de los elementos de los informes y otros documentos. Eliminan informes y otros elementos. Ven informes, incluidos los informes que usan modelos de informe para la exploración de datos. Establecen los parámetros de los informes. Establecen las opciones de procesamiento de un informe. Generan modelos de informe. Crean informes con el Generador de informes. Crean y administran orígenes de datos compartidos. Crean, cambian y eliminan suscripciones que pertenecen a cualquier usuario. Crean y administran programaciones compartidas usadas en todo el sitio. Crean y administran versiones de un documento, incluido el historial del informe. Descargan el archivo de origen para una definición de informe o un modelo de informe. Reemplazan una definición de informe, un modelo de informe, un origen de datos compartido o un recurso (manteniendo las propiedades de los elementos y los permisos).|  
|**Miembros**|Contribuir|Los miembros pueden crear elementos y publicar elementos, informes y modelos desde herramientas de diseño en una biblioteca de SharePoint.|Agregan informes y otros elementos a las bibliotecas. Modifican las propiedades de los elementos de los informes y otros documentos. Eliminan informes y otros elementos. Ven informes, incluidos los informes que usan modelos de informe para la exploración de datos. Ven versiones anteriores de un documento, incluidas las instantáneas del historial del informe (requiere que un usuario también tenga permiso para abrir el informe para el que se creó el historial del informe). Establecen los parámetros de los informes. Establecen las opciones de procesamiento de un informe. Generan modelos de informe. Crean informes con el Generador de informes. Crean y administran orígenes de datos compartidos. Crean, cambian y eliminan suscripciones que pertenecen al usuario. Usan programaciones compartidas con una suscripción. Crean y administran versiones de un documento, incluido el historial del informe. Descargan el archivo de origen para una definición de informe o un modelo de informe. Reemplazan una definición de informe, un modelo de informe, un origen de datos compartido o un recurso (manteniendo las propiedades de los elementos y los permisos).|  
|**Visitantes** y **Visores**|Lectura|Los visitantes pueden ver informes|Ven informes, incluidos los informes que usan modelos de informe para la exploración de datos.|  
  
 Si no está usando los niveles de permiso y grupos integrados, debe incluir permisos específicos para tener acceso a las características de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] . Para obtener más información, consulte [establecer permisos para las operaciones del servidor de informes en una aplicación Web de SharePoint](set-permissions-for-report-server-operations-in-a-sharepoint-web-application.md).  
  
## <a name="see-also"></a>Vea también  
 [Conceder permisos sobre elementos de servidor de informes en un sitio de SharePoint](granting-permissions-on-report-server-items-on-a-sharepoint-site.md)   
 [Comparar Roles y tareas de Reporting Services con permisos y grupos de SharePoint](../reporting-services-roles-tasks-vs-sharepoint-groups-permissions.md)   
 [Establecimiento de permisos para las operaciones del servidor de informes en una aplicación web de SharePoint](set-permissions-for-report-server-operations-in-a-sharepoint-web-application.md)   
 [Concesión de permisos sobre elementos del servidor de informes en un sitio de SharePoint](granting-permissions-on-report-server-items-on-a-sharepoint-site.md)  
  
  