---
title: Crear, modificar y eliminar orígenes de datos compartidos (SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- modifying data source properties
- shared data sources [Reporting Services]
- removing shared data sources
- roles [Reporting Services], shared data sources
- data sources [Reporting Services], shared
- data sources [Reporting Services], modifying properties
- deleting shared data sources
ms.assetid: 1e58c1c2-5ecf-4ce6-9d04-0a8acfba17be
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 4a2239e07cc24842c5cbdf44c8743ea2d79ea7cb
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "66107400"
---
# <a name="create-modify-and-delete-shared-data-sources-ssrs"></a>Crear, modificar y eliminar orígenes de datos compartidos (SSRS)
  Un origen de datos compartido es un conjunto de propiedades de conexión de un origen de datos a las que pueden hacer referencia varios informes, modelos y suscripciones controladas por datos que se ejecutan en un servidor de informes de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] . Los orígenes de datos compartidos proporcionan una manera fácil de administrar las propiedades del origen de datos que, a menudo, cambian con el tiempo. Si una cuenta de usuario o una contraseña cambia, o si mueve la base de datos a otro servidor, puede actualizar la información de conexión en un único lugar.  
  
 Los orígenes de datos compartidos son opcionales para los informes y para las suscripciones controladas por datos, pero obligatorios para los modelos de informe. Si tiene previsto usar modelos de informe para la notificación ad hoc, deberá crear y mantener un elemento de origen de datos compartido que proporcione información de conexión al modelo.  
  
 Un origen de datos compartido se compone de las partes siguientes:  
  
|Parte|Descripción|  
|----------|-----------------|  
|Name|Un nombre que identifica el origen dentro de la jerarquía de carpetas del servidor de informes.|  
|Descripción|Una descripción que aparece con el elemento en el Administrador de informes cuando el usuario ve el contenido de la carpeta.|  
|Tipo de conexión|La extensión de procesamiento de datos usada con el origen de datos. Solo puede usar extensiones de procesamiento de datos implementadas en el servidor de informes. Para más información sobre las extensiones de procesamiento de datos que se incluyen con [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)], vea [Orígenes de datos admitidos por Reporting Services &#40;SSRS&#41;](../create-deploy-and-manage-mobile-and-paginated-reports.md).|  
|Cadena de conexión|La cadena de conexión para la base de datos. Para obtener más información y ver ejemplos de cadenas de conexión a orígenes de datos usados con frecuencia, consulte [conexiones de datos, orígenes de datos y cadenas de conexión en Reporting Services](../data-connections-data-sources-and-connection-strings-in-reporting-services.md).|  
|Tipo de credencial|Especifica cómo se obtienen las credenciales para la conexión y si se van a usar una vez establecida la conexión. Para más información, consulte [Especificar información de credenciales y conexión para los orígenes de datos de informes](../../integration-services/connection-manager/data-sources.md).|  
  
 El origen de datos compartido no contiene información de consulta utilizada para recuperar datos. La consulta siempre se conserva en la definición de informe.  
  
## <a name="creating-and-modifying-a-shared-data-source"></a>Crear y modificar un origen de datos compartido  
 Para crear un origen de datos compartido o modificar sus propiedades, debe tener permisos de tipo **Administrar orígenes de datos** en el servidor de informes. Si el servidor de informes se ejecuta en modo nativo, puede usar el Administrador de informes para crear y configurar el origen de datos compartido. Si el servidor de informes se ejecuta en el modo integrado de SharePoint, puede usar las páginas de aplicación de un sitio de SharePoint. Para cualquier servidor de informes, sea cual sea su modo, puede crear un origen de datos compartido en el Diseñador de informes y, a continuación, publicarlo en un servidor de destino.  
  
 Para obtener más información acerca de cómo crear un origen de datos compartido, vea:  
  
-   [Crear un origen de datos incrustado o compartido &#40;SSRS&#41;](../create-an-embedded-or-shared-data-source-ssrs.md)  
  
-   [Crear y administrar orígenes de datos compartidos &#40;Reporting Services en el modo integrado de SharePoint&#41;](../create-manage-shared-data-sources-reporting-services-sharepoint-integrated-mode.md)  
  
 Después de crear un origen de datos compartido en el servidor de informes, puede crear asignaciones de roles para controlar el acceso a él, moverlo a otra ubicación, cambiar su nombre o ponerlo en modo sin conexión para evitar el procesamiento de informes mientras se realizan operaciones de mantenimiento en el origen de datos externos. Si cambia de nombre o mueve un origen de datos compartido a otra ubicación en la jerarquía de carpetas del servidor de informes, la información de ruta de acceso en todos los informes o suscripciones que hagan referencia a él se actualiza en consecuencia. Si pone el origen de datos en modo sin conexión, todos los informes, modelos y suscripciones dejarán de ejecutarse hasta que vuelva a habilitar el origen de datos.  
  
 Para más información sobre cómo controlar el acceso a orígenes de datos compartidos en la jerarquía de carpetas del servidor de informes, vea [Proteger elementos de orígenes de datos compartidos](../security/secure-shared-data-source-items.md).  
  
## <a name="deleting-a-shared-data-source"></a>Eliminar un origen de datos compartido  
 Puede eliminar un origen de datos compartido de la misma manera que eliminaría cualquier elemento del servidor de informes. En el Administrador de informes abra la carpeta en la vista de detalles, seleccione el elemento y haga clic en **eliminar**. En una página de aplicación en un sitio de SharePoint, abra la biblioteca de SharePoint, seleccione el elemento y haga clic en **eliminar**.  
  
 Si elimina un origen de datos compartido, se desactivarán todos los informes, modelos y suscripciones controladas por datos que lo usan. Sin la información de conexión de un origen de datos, los elementos dejan de ejecutarse. Para activar estos elementos, deberá abrir cada uno de ellos y hacer lo siguiente:  
  
-   Para los informes y las suscripciones controladas por datos que hacen referencia al origen de datos compartido, puede especificar información de conexión del origen de datos en las propiedades de informe o de suscripción, o puede seleccionar un nuevo origen de datos compartido que tenga los valores que desea usar.  
  
-   Para los modelos e informes del Generador de informes que usan ese modelo, debe especificar un nuevo origen de datos compartido. Los modelos solo obtienen información de conexión de un origen de datos a través de orígenes de datos compartidos.  
  
 Si desea ver una lista de informes y modelos que usan el origen de datos, abra la página Elementos dependientes para el origen de datos compartido. Puede tener acceso a esta página al abrir el origen de datos en el Administrador de informes o en una página de aplicación de SharePoint. Observe que la página Elementos dependientes no muestra las suscripciones controladas por datos. Si una suscripción usa un origen de datos compartido, la suscripción no aparecerá en la lista de elementos dependientes.  
  
 No hay ninguna operación de deshacer para eliminar un origen de datos compartido. Sin embargo, si elimina accidentalmente un origen de datos compartido, puede crear uno nuevo usando las mismas propiedades que las del origen eliminado. Tendrá que abrir cada uno de los informes, modelos y suscripciones controladas por datos para volver a enlazar el origen de datos compartido al elemento que lo usa, pero siempre y cuando las propiedades del origen de datos sean las mismas, los informes, modelos y suscripciones continuarán funcionando como antes.  
  
## <a name="see-also"></a>Vea también  
 [Crear y administrar orígenes de datos compartidos &#40;Reporting Services en el modo integrado de SharePoint&#41;](../create-manage-shared-data-sources-reporting-services-sharepoint-integrated-mode.md)   
 [Conexiones de datos, orígenes de datos y cadenas de conexión en Reporting Services](../data-connections-data-sources-and-connection-strings-in-reporting-services.md)   
 [Administrar orígenes de datos de informe](manage-report-data-sources.md)   
 [Administrador de informes &#40;Modo nativo de SSRS&#41;](../report-manager-ssrs-native-mode.md)   
 [Conexiones de datos u orígenes de datos compartidos e incrustados &#40;Generador de informes y SSRS&#41;](../embedded-and-shared-data-connections-or-data-sources-report-builder-and-ssrs.md)   
 [Orígenes de datos &#40;página de propiedades del Administrador de informes&#41;](../data-sources-properties-page-report-manager.md)   
 [Crear, eliminar o modificar un origen de datos compartido &#40;Administrador de informes&#41;](../create-delete-or-modify-a-shared-data-source-report-manager.md)   
 [Configurar propiedades de origen de datos para un informe &#40;Administrador de informes&#41;](configure-data-source-properties-for-a-report-report-manager.md)  
  
  
