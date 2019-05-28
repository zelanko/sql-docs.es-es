---
title: Informes almacenados en caché (SSRS) | Microsoft Docs
ms.date: 05/14/2019
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: report-server
ms.topic: conceptual
helpviewer_keywords:
- report execution properties [Reporting Services]
- cache [Reporting Services]
- report processing [Reporting Services], caching
- cached instances [Reporting Services]
- refreshing cache
- cached reports [Reporting Services]
- preloading cache
- invalid cached reports [Reporting Services]
- performance [Reporting Services]
- expiration [Reporting Services]
- snapshots [Reporting Services], caching
ms.assetid: 146542c3-8efd-4b89-a8d8-77d22896630e
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: ba54a5c29245a178fb1b50139d64f1e05bfd92f1
ms.sourcegitcommit: 982a1dad0b58315cff7b54445f998499ef80e68d
ms.translationtype: MTE75
ms.contentlocale: es-ES
ms.lasthandoff: 05/23/2019
ms.locfileid: "66175585"
---
# <a name="caching-reports-ssrs"></a>Informes almacenados en caché (SSRS)
  Un servidor de informes puede almacenar en memoria caché una copia de un informe procesado y devolverla cuando el usuario abra el informe. Para un usuario, la única prueba visible que indica que el informe es una copia en caché es la fecha y la hora de ejecución. Si la fecha o la hora no son actuales y el informe no es una instantánea, significa que éste se ha obtenido de la caché.  
  
 El almacenamiento en caché puede reducir el tiempo necesario para recuperar un informe cuando éste es demasiado grande o se utiliza con frecuencia. Si se reinicia el servidor, las instancias almacenadas en la caché se restablecen cuando el servicio web del servidor de informes vuelve a estar en línea.  
  
 El almacenamiento en caché es una técnica de mejora del rendimiento. El contenido de la caché es volátil y puede cambiar conforme se agregan, reemplazan o eliminan informes. Si precisa una estrategia de almacenamiento en caché más predecible, se recomienda que cree una instantánea del informe. Para más información, vea [Establecer las propiedades del procesamiento de informes](../../reporting-services/report-server/set-report-processing-properties.md).  
  
> [!NOTE]  
>  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] almacena los archivos temporales en una base de datos para su uso en las sesiones de usuario y el procesamiento de informes. Estos archivos se almacenan en la caché para uso interno y para lograr coherencia en la visualización durante una sesión única del explorador. Para más información sobre cómo se almacenan en la memoria caché los archivos temporales de uso interno, vea [Base de datos del servidor de informes &#40;Modo nativo de SSRS&#41;](../../reporting-services/report-server/report-server-database-ssrs-native-mode.md).  
  
## <a name="cached-instances"></a>Instancias almacenadas en caché  
 Una instancia de un informe almacenada en caché se basa en el formato intermedio del informe. Por lo general, el servidor de informes almacena en caché una instancia de un informe según el nombre del informe. Sin embargo, si un informe puede incluir datos diferentes basados en parámetros de consulta, es posible que se almacenen en caché varias versiones del informe. Por ejemplo, supongamos que dispone de un informe con parámetros que utiliza el código de región como un valor de parámetro. Si cuatro usuarios distintos especifican cuatro códigos de región diferentes, se crearán cuatro copias en la memoria caché.  
  
 El primer usuario que ejecuta el informe con un código de región exclusivo crea un informe en caché que contiene los datos correspondientes a la región indicada. Los siguientes usuarios que soliciten el informe con el mismo código de región obtendrán la copia almacenada en la caché.  
  
 No todos los informes se pueden almacenar en caché. Por ejemplo, no se pueden almacenar en la memoria caché los informes que incluyen datos dependientes del usuario, que solicitan las credenciales a los usuarios o que utilizan la autenticación de Windows.  
  
## <a name="refreshing-the-cache"></a>Actualizar la memoria caché  
 Un informe almacenado en caché se sustituye por una versión más reciente cuando un usuario selecciona el informe después de que haya expirado la copia en caché anterior. Los informes que se hayan configurado para ejecutarse como instancias en caché se quitan de la caché a intervalos regulares, en función de los parámetros de expiración. La expiración de un informe se puede establecer en minutos o en un momento programado, según se determina mediante el requisito de inmediatez de los datos. No se pueden eliminar informes de la caché directamente salvo que se use la API de SOAP.  
  
 Para configurar la expiración de la caché, puede usar una programación compartida o una específica del informe. Si usa una programación compartida y ésta se detiene posteriormente, la caché no expirará mientras la programación no esté operativa. Si más adelante se elimina la programación compartida, se guardará una copia de la configuración de la programación como programación específica del informe.  
  
 Si expira una programación o si deja de estar disponible el motor de programación en la fecha de expiración de la caché, el servidor de informes ejecutará un informe activo hasta que puedan reanudarse las operaciones programadas (ya sea ampliando la programación o iniciando el servicio de programación).  
  
## <a name="preloading-the-cache"></a>Cargar previamente la memoria caché  
 Para mejorar el rendimiento del servidor, se puede cargar previamente la memoria caché. Puede cargar previamente la memoria caché con una recopilación de instancias del informe parametrizadas de dos maneras:  
  
1.  Cree un plan de actualización de la memoria caché. Al crear un plan de actualización, puede especificar una programación para un informe único o especificar una programación compartida.  
  
2.  Cree una suscripción controlada por datos que use el proveedor de entrega NULL. Cuando se especifica el proveedor de entrega NULL como método de entrega en la suscripción, el servidor de informes toma la base de datos del servidor de informes como destino de entrega y utiliza una extensión de representación especializada, denominada extensión de representación NULL. A diferencia de otras extensiones de entrega, el proveedor de entrega NULL no permite establecer ninguna configuración de entrega mediante una definición de suscripción.  
  
 Almacenar en caché un informe resulta especialmente útil si se desea almacenar en caché varias instancias de un informe con parámetros, en el que se utilizan distintos valores de parámetros para generar diferentes instancias de informe. Tenga en cuenta que en el informe solamente se pueden especificar parámetros basados en consultas.  
  
 Cuando se especifica una programación o se crea la suscripción controlada por datos, se debe programar la frecuencia con que se entregan los informes en la memoria caché. Para que se entreguen copias nuevas en la memoria caché, las antiguas deben haber expirado. Por lo tanto, las propiedades de Ejecución del informe se deben configurar de modo que se incluyan parámetros de expiración de la caché. La configuración de expiración debe ser coherente con la programación definida para la suscripción. Por ejemplo, si se crea una suscripción que se ejecute cada noche, la caché también debería expirar cada noche antes de la ejecución de la suscripción. Si las propiedades de ejecución no contemplan las horas de expiración, se omitirán las entregas más recientes. Para más información sobre los planes de actualización de la memoria caché, vea [Programaciones](../../reporting-services/subscriptions/schedules.md). Para más información sobre cómo establecer las propiedades, vea [Establecer las propiedades de procesamiento de informes](../../reporting-services/report-server/set-report-processing-properties.md). Para más información sobre cómo usar suscripciones controladas por datos, vea [Suscripciones controladas por datos](../../reporting-services/subscriptions/data-driven-subscriptions.md).  
  
## <a name="conditions-that-cause-cache-expiration"></a>Situaciones que pueden provocar la expiración de la memoria caché  
 Un informe en caché pierde su validez como consecuencia de las siguientes situaciones: una modificación de la definición de informe o de los parámetros del informe, un cambio de las credenciales del origen de datos o un cambio de las opciones de ejecución del informe. Si elimina un informe almacenado en caché, también se elimina la versión en caché.  
  
 Si un informe no puede representarse desde una instancia en caché por cualquier motivo (por ejemplo, si los valores de los parámetros que especifica un usuario son distintos de los que se utilizan para generar el informe en caché), el servidor de informes vuelve a ejecutar el informe.  
  
## <a name="see-also"></a>Vea también  
 [Establecer opciones de procesamiento &#40;Reporting Services en el modo integrado de SharePoint&#41;](../../reporting-services/report-server-sharepoint/set-processing-options-reporting-services-in-sharepoint-integrated-mode.md)   
 [Establecer las propiedades del procesamiento de informes](../../reporting-services/report-server/set-report-processing-properties.md)   
 [Conceptos de Reporting Services &#40;SSRS&#41;](../../reporting-services/reporting-services-concepts-ssrs.md)   
 [Carga previa de la memoria caché](../../reporting-services/report-server/preload-the-cache-report-manager.md)   
 [Programaciones](../../reporting-services/subscriptions/schedules.md)   
 [Almacenar en caché conjuntos de datos compartidos &#40;SSRS&#41;](../../reporting-services/report-server/cache-shared-datasets-ssrs.md)   
  
  
