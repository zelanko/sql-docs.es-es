---
title: Cargar previamente la memoria caché (Administrador de informes) | Microsoft Docs
ms.date: 03/14/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.technology: report-server
ms.suite: pro-bi
ms.topic: conceptual
helpviewer_keywords:
- cache [Reporting Services]
- preloading cache
ms.assetid: 152a1051-8aa5-4c01-bc85-f8be8971b0cd
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 9d763e94f1305aabf14c7b92559d91d3d4c927da
ms.sourcegitcommit: d96b94c60d88340224371926f283200496a5ca64
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/30/2018
ms.locfileid: "43265947"
---
# <a name="preload-the-cache-report-manager"></a>Cargar previamente la memoria caché (Administrador de informes)
  Puede cargar previamente la memoria caché para un conjunto de datos compartido creando un plan de actualización de caché para él.  
  
 Puede cargar previamente la memoria caché para un informe de dos maneras:  
  
1.  Cree un plan de actualización de caché para el informe. Éste es el método preferido.  
  
2.  Utilice una suscripción controlada por datos para cargar previamente la memoria caché con instancias de informes con parámetros. Esa era la única manera de cargar previamente la memoria caché en las versiones de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] anteriores a [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]. Para más información, vea [Informes almacenados en caché &#40;SSRS&#41;](../../reporting-services/report-server/caching-reports-ssrs.md).  
  
 Se deben cumplir las siguientes condiciones para poder almacenar en memoria caché un informe o un conjunto de datos compartido:  
  
-   El conjunto de datos compartido o el informe deben tener habilitado el almacenamiento en caché.  
  
-   Los orígenes de datos compartidos para el conjunto de datos compartidos o el informe se deben configurar para utilizar las credenciales almacenadas o para no usar ninguna credencial.  
  
-   Se debe ejecutar el servicio Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
### <a name="to-preload-the-cache-by-creating-a-cache-refresh-plan"></a>Para cargar previamente la memoria caché creando un plan de actualización de caché  
  
1.  Inicie el [Administrador de informes &#40;Modo nativo de SSRS&#41;](http://msdn.microsoft.com/library/80949f9d-58f5-48e3-9342-9e9bf4e57896).  
  
2.  En el Administrador de informes, navegue a la página **Contenido** y después navegue al elemento que desee almacenar en caché.  
  
3.  Mantenga el mouse sobre el elemento, haga clic en la lista desplegable y, después, haga clic en **Administrar**.  
  
4.  Haga clic en la pestaña **Opciones de actualización de caché** .  
  
5.  En la barra de herramientas, haga clic en **Nuevo plan de actualización de caché**.  
  
    > [!NOTE]  
    >  Si el elemento no tiene habilitado el almacenamiento en caché, se solicitará que lo habilite. Para habilitar el almacenamiento en caché, haga clic en **Aceptar**.  
  
     Se abre la página de Plan de actualización de caché.  
  
6.  Escriba una descripción para el plan de actualización.  
  
7.  En una programación compartida, haga clic en **Programación compartida**y seleccione el nombre de la programación que se va a usar.  
  
     En una programación personalizada, haga clic en **Programación específica del elemento**y, después, haga clic en **Configurar**.  
  
8.  Configurar la programación  
  
9. [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
### <a name="to-preload-the-cache-with-a-user-specific-report-by-using-a-data-driven-subscription"></a>Para cargar previamente la memoria caché con un informe específico del usuario utilizando una suscripción controlada por datos  
  
1.  Inicie el [Administrador de informes &#40;Modo nativo de SSRS&#41;](http://msdn.microsoft.com/library/80949f9d-58f5-48e3-9342-9e9bf4e57896).  
  
2.  En el Administrador de informes, navegue a la página **Contenido** y después, al informe para el que desea crear una suscripción.  
  
3.  Haga clic en el informe, en la pestaña **Suscripciones** y, después, en **Nueva suscripción controlada por datos**.  
  
4.  Escriba una descripción de la suscripción (opcional).  
  
5.  En la lista **Especifique cómo se notifica a los destinatarios** , seleccione **Proveedor de entrega NULL**.  
  
6.  Especifique un tipo de origen de datos y haga clic en **Siguiente** para configurar el origen de datos.  
  
7.  Especifique el tipo de conexión, la cadena de conexión y las credenciales para obtener acceso al origen de datos que contiene la información sobre los suscriptores. En el siguiente ejemplo, se muestra la cadena de conexión utilizada para conectarse a una base de datos [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] llamada Subscribers:  
  
    ```  
    data source=<servername>; initial catalog=Subscribers  
    ```  
  
8.  Haga clic en **Siguiente**.  
  
9. Especifique la consulta o el comando que recupera los datos de los suscriptores. Si lo desea, puede incrementar el período de tiempo de espera en el caso de consultas que tarden bastante tiempo en procesarse. Por ejemplo:  
  
    ```  
    Select * from UserInfo  
    ```  
  
10. Haga clic en **Validar**. Antes de continuar, la consulta debe validarse. Cuando aparezca el mensaje **Consulta validada correctamente** , haga clic en **Siguiente**.  
  
11. Dado que no puede configurar extensiones de entrega para el proveedor de entrega NULL, haga clic en **Siguiente**.  
  
12. Especifique valores de parámetro de informe para la suscripción y haga clic en **Siguiente**.  
  
13. Especifique cuándo se procesa la suscripción. No elija **Cuando los datos del informe se actualizan en el servidor de informes**. Este valor solo es para instantáneas. Si quiere usar una programación existente, seleccione **Según una programación compartida**.  
  
     O bien, para crear una programación personalizada, haga clic en **Según una programación creada para esta suscripción** y, a continuación, en **Siguiente**. Configure la programación y, a continuación, haga clic en **Finalizar**.  
  
    > [!NOTE]  
    >  Para que los suscriptores reciban el informe más reciente, el programa que configure debe ser coherente con la programación de entrega del informe que haya definido para los suscriptores. Para más información, vea [Administrador de informes &#40;Modo nativo de SSRS&#41;](http://msdn.microsoft.com/library/80949f9d-58f5-48e3-9342-9e9bf4e57896).  
  
14. Configure las opciones de Ejecución correspondientes al informe de la forma siguiente: En la página del informe, haga clic en la pestaña **Propiedades** .  
  
15. En el marco de la izquierda, haga clic en la pestaña **Ejecución** .  
  
16. En la página, seleccione **Representar este informe con los datos más recientes**.  
  
17. Elija una de las dos opciones de caché siguientes y configure la expiración como se indica a continuación:  
  
    -   Para lograr que la copia en caché expire después de un período de tiempo concreto, haga clic en **Almacenar en caché una copia temporal del informe. La copia expirará después de un número determinado de minutos.** Escriba el número de minutos para la expiración del informe.  
  
    -   Para lograr que la copia en caché expire según una programación, haga clic en **Guardar en caché una copia temporal del informe. La copia del informe debe expirar según la siguiente programación.** Haga clic en **Configurar**o seleccione una programación compartida para establecer una programación para la expiración del informe.  
  
18. Haga clic en **Aplicar**.  
  
## <a name="see-also"></a>Ver también  
 [Suscripciones controladas por datos](../../reporting-services/subscriptions/data-driven-subscriptions.md)   
 [Crear una suscripción controlada por datos &#40;Tutorial de SSRS&#41;](../../reporting-services/create-a-data-driven-subscription-ssrs-tutorial.md)   
 [Rendimiento, instantáneas, almacenamiento en caché &#40;Reporting Services&#41;](../../reporting-services/report-server/performance-snapshots-caching-reporting-services.md)   
 [Establecer las propiedades del procesamiento de informes](../../reporting-services/report-server/set-report-processing-properties.md)   
 [Informes almacenados en caché &#40;SSRS&#41;](../../reporting-services/report-server/caching-reports-ssrs.md)  
  
  
