---
title: Crear, modificar y eliminar suscripciones controladas por datos | Microsoft Docs
ms.date: 03/01/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.technology: subscriptions
ms.topic: conceptual
helpviewer_keywords:
- query-based subscriptions [Reporting Services]
- queries [Reporting Services], data-driven subscriptions
- subscriptions [Reporting Services], data-driven
- data-driven subscriptions
ms.assetid: 0ba2093e-9393-4eb6-af06-9da10988cfaf
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 3a7759473698ebdae0a9e97e7487f8812983d5b8
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 10/01/2018
ms.locfileid: "47849153"
---
# <a name="create-modify-and-delete-data-driven-subscriptions"></a>Cómo crear, modificar y eliminar suscripciones controladas por datos
  Una suscripción controlada por datos es una suscripción basada en consultas que obtiene los valores de los datos que se utilizan para procesar la suscripción en tiempo de ejecución. Cuando se desencadena la suscripción, se procesa una consulta para obtener información actualizada sobre destinatarios, opciones de entrega del informe, formatos de representación y valores de los parámetros. Los resultados de la consulta se combinan con la definición de la suscripción para crear una suscripción dinámica que utiliza datos que se mantienen en una base de datos de empleados, de clientes o de cualquier otro tipo que contenga información que se pueda utilizar como datos de suscriptor.  
  
 Para crear una nueva suscripción controlada por datos o modificar una existente, use las páginas Crear suscripción controlada por datos del Administrador de informes. Estas páginas le guían por los pasos necesarios para crear o modificar una suscripción. Para tener acceso a una suscripción una vez creada, utilice la página Mis suscripciones y la lista Suscripciones de un informe. Para más información sobre cómo crear una suscripción controlada por datos, vea [Crear una suscripción controlada por datos &#40;Tutorial de SSRS&#41;](../../reporting-services/create-a-data-driven-subscription-ssrs-tutorial.md).  
  
 En este tema:  
  
-   [Administrar y eliminar una suscripción controlada por datos](#bkmk_manage_and_delete)  
  
-   [Crear y modificar una suscripción controlada por datos](#bkmk_create_and_modify)  
  
-   [Definir una consulta que recupera información de suscripción](#bkmk_define_query)  
  
-   [Ejecutar la suscripción](#bkmk_run_subscription)  
  
##  <a name="bkmk_manage_and_delete"></a> Administrar y eliminar una suscripción controlada por datos  
 Una suscripción controlada por datos que se está procesando no puede detenerse o eliminarse mediante la página Administrar trabajos del Administrador de informes. Por esta razón, resulta ventajoso usar una programación compartida para desencadenar la suscripción controlada por datos. De esa manera, si desea impedir temporalmente que se procese una suscripción, puede pausar la programación que la desencadena. Para más información, vea [Crear y administrar suscripciones para servidores de informes en modo nativo](http://msdn.microsoft.com/7f46cbdb-5102-4941-bca2-5e0ff9012c6b).  
  
 Para eliminar una suscripción controlada por datos, selecciónela en la página Mis suscripciones o en la página Suscripciones de un informe y, después, haga clic en **Eliminar**.  
  
 Para obtener instrucciones sobre cómo cancelar una suscripción controlada por datos, vea [Administrar un proceso en ejecución](../../reporting-services/subscriptions/manage-a-running-process.md).  
  
##  <a name="bkmk_create_and_modify"></a> Crear y modificar una suscripción controlada por datos  
 Para crear una suscripción controlada por datos, seleccione un informe que utilice credenciales almacenadas o que no utilice ninguna credencial. Cuando cree la suscripción controlada por datos, considere la posibilidad de usar una convención de nomenclatura en los campos de descripción para que pueda diferenciar fácilmente las suscripciones estándar de las suscripciones controladas por datos.  
  
#### <a name="to-create-a-data-driven-subscription-native-mode"></a>Para crear una suscripción controlada por datos (modo nativo)  
  
1.  En el Administrador de informes, navegue hasta la carpeta que contiene el informe, mantenga el mouse sobre el informe, abra el menú de opciones y haga clic en **Administrar**.  
  
2.  Haga clic en la pestaña **Suscripciones** .  
  
3.  Haga clic en el botón **Nueva suscripción controlada por datos** .  
  
#### <a name="to-create-a-data-driven-subscription-sharepoint-mode"></a>Para crear una suscripción controlada por datos (modo de SharePoint)  
  
1.  En la biblioteca de documentos de SharePoint, mantenga el mouse sobre el informe, abra las opciones de menú y haga clic en **Administrar suscripciones**.  
  
2.  Haga clic en **Agregar suscripción controlada por datos**.  
  
#### <a name="to-modify-an-existing-data-driven-subscription-native-mode"></a>Para modificar una suscripción controlada por datos existente (modo nativo)  
  
1.  En el Administrador de informes, navegue hasta la carpeta que contiene el informe, mantenga el mouse sobre el informe, abra el menú de opciones y haga clic en **Administrar**.  
  
2.  Haga clic en la pestaña **Suscripciones** . También puede hacer clic en el vínculo **Mis suscripciones**, situado en la parte superior del administrador de informes.  
  
3.  Seleccione la suscripción que desea modificar. El siguiente icono indica una suscripción controlada por datos: ![Icono de suscripción controlada por datos](../../reporting-services/subscriptions/media/hlp-16subscriptiondd.gif "Icono de suscripción controlada por datos")  
  
#### <a name="to-modify-an-existing-data-driven-subscription-sharepoint-mode"></a>Para modificar una suscripción controlada por datos existente (modo de SharePoint)  
  
1.  En la biblioteca de documentos de SharePoint, mantenga el mouse sobre el informe, abra las opciones de menú y haga clic en **Administrar suscripciones**.  
  
2.  Seleccione la suscripción que desea modificar.  
  
> [!NOTE]  
>  Puede modificar cualquier valor que ya se haya especificado. Todos los valores aparecen como se crearon en primer lugar, excepto la contraseña que se utiliza para obtener acceso al almacén de datos de suscriptores. Debe volver a escribir la contraseña cada vez que modifique valores en la segunda página o cualquier página posterior.  
  
 Antes de crear una suscripción controlada por datos, asegúrese de cumplir los requisitos siguientes:  
  
-   **Requisitos de informes** El informe debe utilizar credenciales almacenadas o ninguna credencial para recuperar datos en tiempo de ejecución. No es posible suscribirse a un informe que utilice credenciales suplantadas o delegadas para conectarse a un origen de datos externo; las credenciales del usuario que crea la suscripción o es propietario de ella no estarán disponibles cuando se procese la suscripción. Las credenciales almacenadas pueden ser una cuenta de Windows o una cuenta de usuario de base de datos. Para más información, consulte [Especificar información de credenciales y conexión para los orígenes de datos de informes](../../reporting-services/report-data/specify-credential-and-connection-information-for-report-data-sources.md).  
  
     No es posible suscribirse a un informe del Generador de informes que utilice como origen de datos un modelo con una configuración de seguridad de elementos de modelo. Esta restricción solo se aplica a los informes que utilizan seguridad de elementos de modelo.  
  
     No es posible crear una suscripción controlada por datos en un informe que contenga la expresión `User!UserID` .  
  
-   **Requisitos de datos** Debe disponer de acceso a un origen de datos externo que contenga la información sobre los suscriptores.  
  
-   **Requisitos de usuarios** El autor de la suscripción debe tener permiso para "Administrar informes" y "Administrar todas las suscripciones". Para más información sobre los permisos de tarea de nivel de elemento, vea [Tareas y permisos](../../reporting-services/security/tasks-and-permissions.md). El autor también debe disponer de las credenciales necesarias para obtener acceso al origen de datos externo que contiene los datos de los suscriptores.  
  
##  <a name="bkmk_define_query"></a> Definir una consulta que recupera información de suscripción  
 En una suscripción controlada por datos se debe especificar una consulta o un comando que recupere los datos de los suscriptores. La consulta debería producir una fila por suscriptor. Si utiliza la extensión de entrega por correo electrónico, la consulta debería devolver un alias de correo electrónico válido para cada suscriptor. El número de entregas que se realice se basa en el número de filas que devuelva la consulta. Si el conjunto de filas contiene 10.000 filas, la suscripción entregará 10.000 informes.  
  
 Si la consulta tarda mucho en ejecutarse, puede aumentar el valor de tiempo de espera para adaptarse al procesamiento adicional.  
  
 Para este paso, la consulta debe validarse antes de continuar. La validación no procesa la consulta, sino que devuelve una lista de todas las columnas del conjunto de filas para que pueda hacer referencia a ellas en selecciones posteriores. Si la consulta no se valida, no podrá continuar. Una consulta no se valida si su sintaxis es incorrecta o si la conexión al origen de datos no es válida. Use el botón **Atrás** para hacer correcciones en el origen de datos.  
  
##  <a name="bkmk_run_subscription"></a> Ejecutar la suscripción  
 Se deben especificar las condiciones necesarias para procesar la suscripción. Puede especificar una programación o puede desencadenar la suscripción para que coincida con actualizaciones en una instantánea de ejecución de informes. El procesamiento de las suscripciones controladas por datos es igual al de las suscripciones estándar.  
  
## <a name="see-also"></a>Ver también  
 [Crear y administrar suscripciones para servidores de informes en modo nativo](../../reporting-services/subscriptions/create-and-manage-subscriptions-for-native-mode-report-servers.md)   
 [Suscripciones y entrega &#40;Reporting Services&#41;](../../reporting-services/subscriptions/subscriptions-and-delivery-reporting-services.md)   
 [Administrador de informes &#40;Modo nativo de SSRS&#41;](http://msdn.microsoft.com/library/80949f9d-58f5-48e3-9342-9e9bf4e57896)   
 [old_Crear y administrar suscripciones para servidores de informes en modo nativo](http://msdn.microsoft.com/7f46cbdb-5102-4941-bca2-5e0ff9012c6b)   
 [Suscripciones &#40;página del Administrador de informes&#41;](http://msdn.microsoft.com/library/cf3a6bd0-e0b2-4875-a532-63ef34cfa860)   
 [Mis suscripciones &#40;página del Administrador de informes&#41;](http://msdn.microsoft.com/library/491a85a3-f323-4155-a0a8-de2779899995)  
  
  
