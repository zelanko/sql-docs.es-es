---
title: Solución de problemas de representación de informes de Reporting Services | Microsoft Docs
ms.date: 02/27/2016
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.technology: troubleshooting
ms.suite: pro-bi
ms.topic: conceptual
ms.assetid: 1e0fb399-4c16-438a-92cb-db3e877896d0
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 73b5fe3ae626076b6579671038c50ccc8cd87380
ms.sourcegitcommit: d96b94c60d88340224371926f283200496a5ca64
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/30/2018
ms.locfileid: "43281942"
---
# <a name="troubleshoot-reporting-services-report-rendering-issues"></a>Solución de problemas de representación de informes de Reporting Services
Una vez combinados los datos y la información de diseño, el informe compilado se envía a un representador de informes. Por ejemplo, al obtener una vista previa de un informe localmente, se utiliza el representador de HTML para ver el informe compilado. Utilice este tema para ayudar a solucionar problemas concretos de la representación de informes.   
  
## <a name="why-do-i-have-extra-white-space-including-blank-pages-in-my-report"></a>¿Por qué hay espacios en blanco adicionales, incluidas páginas en blanco, en mi informe?  
Los elementos de informe se ajustan automáticamente durante el procesamiento del informe para conservar el espacio en blanco que se define como parte del informe. Se conserva el espacio en blanco de la vista de diseño del informe. En la superficie de diseño del informe, el fondo blanco representa el espacio en blanco que se conservará al ver, exportar o imprimir un informe, dependiendo del medio de destino.  
  
### <a name="white-space-and-page-breaks-interact-during-rendering"></a>El espacio en blanco y los saltos de página interactúan durante la representación  
Al ver un informe o exportarlo en un formato de archivo, la extensión de representación asociada procesa el informe y lo guarda en el formato de archivo especificado. Cada extensión de representación procesa el espacio en blanco de un informe según reglas concretas. Las propiedades de configuración de las páginas también afectan al espacio en blanco, los saltos de página establecidos en los elementos de informe, la posición relativa de los elementos de informe colocados en el cuerpo del informe, la propiedad KeepTogether para ciertos elementos de informe y si los elementos de informe están en contenedores primarios.   
  
Para eliminar las páginas adicionales debidas al ancho del informe, arrastre el borde de la superficie de diseño del informe para alinearlo con el elemento más externo del mismo. En el caso de un informe con presentación de izquierda a derecha, arrastre el borde derecho para que quede alineado con el elemento más externo del informe. Para más información, consulte los [Comportamientos de la representación (Generador de informes y SSRS)](../../reporting-services/report-design/rendering-behaviors-report-builder-and-ssrs.md).  
  
### <a name="white-space-is-not-preserved-at-the-end-of-a-report"></a>El espacio en blanco no se conserva al final de un informe  
Reporting Services proporciona una opción que permite controlar si conservar o eliminar el espacio en blanco al final de un informe.   
  
Para conservar el espacio en blanco al final de un informe, seleccione el informe y, en el panel Propiedades, desplácese a ConsumeContainerWhitespace y escriba False.   
  
## <a name="why-do-my-reports-look-different-when-exported-to-different-formats"></a>¿Por qué mis informes parecen diferentes cuando los exporto a formatos diferentes?  
Después de ejecutar un informe, puede exportarlo a otro formato, como Excel, Word o PDF. Dependiendo del formato al que exporta el informe, ciertas reglas y limitaciones se podrían aplicar. Puede solucionar muchas limitaciones teniéndolas en cuenta al crear el informe. Podría necesitar usar un diseño ligeramente diferente en el informe, alinear cuidadosamente los elementos dentro del mismo, restringir los pies de página del informe a una sola línea de texto, etc. También puede usar la función RenderFormat integrada para usar un diseño de informe diferente para representadores diferentes. Otras funciones globales integradas pueden ayudar a administrar la paginación en el formato exportado y asignar nombres a las pestañas de las hojas de cálculo en Excel. Para más información, consulte [Exportar informes (Generador de informes y SSRS)](../../reporting-services/report-builder/export-reports-report-builder-and-ssrs.md) y [Referencias a campos globales y de usuario integrados (Generador de informes y SSRS)](../../reporting-services/report-design/built-in-collections-built-in-globals-and-users-references-report-builder.md).  
  
## <a name="how-can-i-view-all-my-report-data-on-one-page"></a>¿Cómo puedo ver todos los datos del informe en una página?  
Para obtener una experiencia de vista interactiva de los informes que no tienen cantidades excesivas de datos, podría ser aconsejable ver todos los datos en una página.   
  
En los representadores de saltos de página automáticos, para ver todos los datos en una página, en las propiedades del informe, establezca InteractiveHeight en 0. En estos representadores, los saltos de página existentes son los omitidos.   
  
> [!NOTE]  
> Cuando un informe no tiene saltos de página, todo el informe se debe procesar para poder ver la primera página.   
  
Para más información sobre las categorías de representadores, consulte [Comportamientos de la representación (Generador de informes y SSRS)](../../reporting-services/report-design/rendering-behaviors-report-builder-and-ssrs.md).  
  
## <a name="reports-do-not-run-when-your-browser-is-configured-to-prompt-for-credentials"></a>Los informes no se ejecutan cuando el explorador se configura para solicitar credenciales  
La visualización puede causar un error cuando el explorador está configurado para solicitar credenciales y los datos de origen están configurados para autenticación de Windows integrada. Esto se produce cuando el origen de datos está en un equipo distinto que el servidor de informes, el origen de datos se configura para usar la autenticación de Windows y el explorador está establecido para solicitar credenciales. Los siguientes son ejemplos de mensajes que verá.  
  
Cuando el origen de datos está configurado para un tipo de conexión de Microsoft SQL Server:  
`An error has occurred during report processing.`  
`Cannot create a connection to data source 'localhost'.`  
`Login failed for user '(null)'. Reason: Not associated with a trusted SQL Server connection.`  
  
Cuando el origen de datos se configura para un tipo de conexión de Lista de Microsoft SharePoint:  
`An error occurred during client rendering.`   
`An error has occurred during report processing.`   
`Query execution failed for dataset 'DataSet1'.`   
`The request failed with HTTP status 401: Unauthorized.`  
  
**Para evitar este problema:** modifique el origen de datos para usar las credenciales almacenadas en lugar de las credenciales de Windows.  
  
**Este problema se aplica a:** exploradores configurados para pedir credenciales.  
  
## <a name="see-also"></a>Ver también  
[Errores y eventos (Reporting Services)](../../reporting-services/troubleshooting/errors-and-events-reference-reporting-services.md)  
[Solución de problemas de recuperación de datos de informes de Reporting Services](../../reporting-services/troubleshooting/troubleshoot-data-retrieval-issues-with-reporting-services-reports.md)  
[Solución de problemas de suscripciones y entrega de Reporting Services](../../reporting-services/troubleshooting/troubleshoot-reporting-services-subscriptions-and-delivery.md)  
  
  
  
  

[!INCLUDE[feedback_stackoverflow_msdn_connect](../../includes/feedback-stackoverflow-msdn-connect-md.md)]

