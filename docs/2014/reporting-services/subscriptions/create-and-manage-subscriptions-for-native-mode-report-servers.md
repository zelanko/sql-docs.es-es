---
title: Crear, modificar y eliminar suscripciones estándares (Reporting Services en modo nativo) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- reporting-services-native
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- standard subscriptions [Reporting Services]
- subscriptions [Reporting Services], standard
ms.assetid: 5ab1c661-9bfa-434a-b315-faac34ed12b1
caps.latest.revision: 46
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: a8c38acc8b25853db76bf89008189928c4cef578
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/02/2018
ms.locfileid: "37230395"
---
# <a name="create-modify-and-delete-standard-subscriptions-reporting-services-in-native-mode"></a>Crear, modificar, y eliminar suscripciones estándar (Reporting Services en modo nativo)
  Una suscripción estándar es la que crean usuarios individuales que desean recibir un informe por correo electrónico o en una carpeta compartida. Una suscripción estándar siempre se define a través del informe en el que se basa.  
  
 El usuario que crea una suscripción es su propietario. Cada usuario puede modificar o eliminar las suscripciones de las que sea propietario.  
  
> [!NOTE]  
>  A partir de [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] puede transferir la propiedad de una suscripción mediante programación. No hay ninguna interfaz de usuario que pueda utilizar para transferir la propiedad de las suscripciones. Para obtener más información, vea <xref:ReportService2010.ReportingService2010.ChangeSubscriptionOwner%2A>  
  
 Según los valores del archivo de configuración **RSReportServer.config** , es posible que los usuarios puedan agregar más usuarios a una suscripción (por ejemplo, un supervisor agrega las direcciones de correo electrónico de sus subordinados para que reciban una copia del informe). La posibilidad de utilizar esta función depende de si el campo Para: está visible cuando se definen las suscripciones individuales. Para obtener más información, consulte [configurar un servidor de informes para la entrega de correo electrónico &#40;SSRS Configuration Manager&#41;](../../sql-server/install/configure-a-report-server-for-e-mail-delivery-ssrs-configuration-manager.md).  
  
 Este tema proporciona información sobre las suscripciones estándar que los usuarios individuales crean y administran. Las suscripciones controladas por datos tienen diferentes requisitos y pasos, y se tratan en otro tema. Para obtener más información, consulte [crear, modificar y eliminar una suscripción controlada por datos](data-driven-subscriptions.md).  
  
 En este tema:  
  
-   [Para crear una suscripción](#bkmk_create_subscription)  
  
-   [Para crear una suscripción a recursos compartidos de archivos](#bkmk_create_fileshare_subscription)  
  
-   [Para crear una suscripción de correo electrónico](#bkmk_create_email_subscription)  
  
-   [Para modificar una suscripción](#bkmk_modify_subscription)  
  
-   [Para eliminar una suscripción](#bkmk_delete_subscription)  
  
##  <a name="bkmk_create_subscription"></a> Para crear una suscripción  
 Para crear una suscripción, elija la herramienta y el enfoque válidos para su implementación del servidor de informes:  
  
-   En el contenido de este tema se explica cómo se crean suscripciones en un servidor de informes en modo nativo mediante el Administrador de informes de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] . Una vez definida una suscripción, puede tener acceso a ella en el Administrador de informes a través de la página Mis suscripciones o la pestaña **Suscripciones** de un informe específico.  
  
-   [Crear y administrar suscripciones para servidores de informes de modo de SharePoint](create-and-manage-subscriptions-for-sharepoint-mode-report-servers.md) explica cómo usar las páginas de aplicación en un sitio de SharePoint para suscribirse a informes en un servidor de informes que se ejecuta en modo integrado de SharePoint.  
  
 En este tema se ofrecen instrucciones para crear una suscripción de correo electrónico y una suscripción de entrega a recursos compartidos de archivos.  
  
-   Para utilizar la entrega por correo electrónico, el servidor de informes debe estar configurado para una conexión de puerta de enlace o servidor SMTP antes de crear la suscripción.  
  
-   Para utilizar la entrega a recursos compartidos de archivos, se debe haber definido la carpeta de destino. Para obtener más información, consulte [configurar un servidor de informes para la entrega de correo electrónico &#40;SSRS Configuration Manager&#41;](../../sql-server/install/configure-a-report-server-for-e-mail-delivery-ssrs-configuration-manager.md).  
  
 Antes de que pueda suscribirse a un informe, hay que configurar el origen de datos del informe de modo que utilice credenciales almacenadas o ninguna credencial. Para obtener más información, consulte [Store credenciales en un origen de datos de Reporting Services](../report-data/store-credentials-in-a-reporting-services-data-source.md). De lo contrario, el botón **Nueva suscripción** no está disponible.  
  
 En este tema no se explica cómo crear una suscripción controlada por datos. Para obtener instrucciones sobre cómo se crea una suscripción controlada por datos, vea [Crear una suscripción controlada por datos &#40;Tutorial de SSRS&#41;](../create-a-data-driven-subscription-ssrs-tutorial.md) o la Ayuda en pantalla de la página Crear una suscripción controlada por datos del Administrador de informes.  
  
###  <a name="bkmk_create_fileshare_subscription"></a> Para crear una suscripción a recursos compartidos de archivos  
  
1.  Inicie el [Administrador de informes &#40;Modo nativo de SSRS&#41;](../report-manager-ssrs-native-mode.md).  
  
2.  En el Administrador de informes, navegue por la página **Contenido** hasta el informe al que desea suscribirse. Haga clic en el informe para abrirlo.  
  
3.  Haga clic en la pestaña **Suscripciones** y, a continuación, en **Nueva suscripción**.  
  
4.  En **Entregado por**, seleccione **Recurso compartido de archivos de Windows**.  
  
5.  En **Nombre de archivo**, escriba un nombre de archivo para el informe.  
  
6.  Seleccione **Agregar una extensión de archivo cuando se crea el archivo**. Esta opción agrega una extensión de archivo de tres caracteres al nombre del archivo. La extensión de archivo está determinada por el formato de salida de informes seleccionado.  
  
7.  En el **ruta** texto, escriba una ruta de acceso de convención de nomenclatura Universal (UNC) a una carpeta existente en la que desee entregar los informes (por ejemplo, \\ \\< servername\>\\< misinformes\>). Incluya dos barras diagonales inversas al comienzo de la ruta de acceso. No escriba una barra diagonal inversa al final.  
  
8.  En Formato de representación, seleccione un formato de salida de informes para la entrega de archivos. Elija el formato correspondiente a la aplicación de escritorio que utilizará para abrir el informe. Evite formatos que no representen los informes en un solo flujo o que especifiquen una interactividad no admitida en un archivo estático (por ejemplo, HTML 4.0).  
  
9. En los cuadros de texto **Nombre de usuario** y **Contraseña**, especifique las credenciales necesarias para obtener acceso al recurso compartido de archivos. Use el formato *\<dominio>*\\*\<nombreDeUsuario>* para el nombre de usuario.  
  
10. Especifique las opciones de sobrescritura. Si hace clic en **No sobrescribir el archivo si existe una versión anterior**, la entrega no se realizará cuando se detecte que el archivo ya existe. Si hace clic en **Incrementar los nombres de archivo conforme se agregan versiones más recientes**, el servidor de informes agrega un número al nombre del archivo para distinguirlo de otros archivos existentes que tengan el mismo nombre.  
  
11. Especifique cuándo desea que se entregue el informe:  
  
    -   Para programar una hora de entrega, haga clic en **Cuando termina la ejecución del informe programado** y después en el botón **Seleccionar programación** . Se abre una página de programación.  
  
    -   Para seleccionar una programación compartida predefinida que ya tenga la fecha, hora e información de periodicidad que desea utilizar, haga clic en **Según una programación compartida**y, a continuación, seleccione la programación que se va a utilizar.  
  
    -   Para entregar el informe cuando una instantánea de informe se actualice con una versión más reciente, haga clic en**Cuando se actualiza el contenido del informe**. Si se suscribe a un informe que recupera los datos en intervalos programados, la programación utilizada para actualizar los datos determina cuándo se procesa su suscripción.  
  
        > [!NOTE]  
        >  Esta opción solo está disponible para instantáneas que ya están asociadas a una programación de actualización.  
  
12. En el caso de informes con parámetros, especifique los parámetros que se van a utilizar en el informe de esta suscripción. Los parámetros pueden ser diferentes de los que se utilizaron para ejecutar el informe a petición o en otras operaciones programadas.  
  
 El informe se entrega como un archivo estático. Si el informe contiene características interactivas, como por ejemplo, vínculos a otras filas y columnas, éstas no estarán disponibles.  
  
###  <a name="bkmk_create_email_subscription"></a> Para crear una suscripción de correo electrónico  
  
1.  En el Administrador de informes, navegue por la página **Contenido** hasta el informe al que desea suscribirse. Haga clic en el informe para abrirlo.  
  
2.  Haga clic en la pestaña **Suscripciones** y, a continuación, en **Nueva suscripción**.  
  
3.  En **Entregado por**, seleccione **Correo electrónico**. Si este tipo de entrega no está disponible, su servidor de informes no se ha configurado para las suscripciones de correo electrónico.  
  
4.  En el cuadro de texto **Para** , el nombre del destinatario del campo Para: se rellena automáticamente mediante su cuenta de usuario de dominio. La configuración del servidor de informes determina si el campo **Para** se rellena automáticamente mediante su cuenta de usuario. Para obtener más información acerca de cómo cambiar las direcciones de correo electrónico configuración, consulte [configurar un servidor de informes para la entrega de correo electrónico &#40;SSRS Configuration Manager&#41;](../../sql-server/install/configure-a-report-server-for-e-mail-delivery-ssrs-configuration-manager.md).  
  
    > [!NOTE]  
    >  Dependiendo de sus permisos, podrá escribir la dirección de correo electrónico donde desea recibir el informe. Para especificar varias direcciones de correo electrónico, sepárelas con un punto y coma (;). También puede escribir direcciones de correo electrónico adicionales en los cuadros de texto **CC**, **CCO**y **Responder a** . Esto requiere que tenga permiso para administrar todas las suscripciones.  
  
5.  Seleccione las opciones de entrega del siguiente modo:  
  
    -   Para incrustar o adjuntar una copia del informe, seleccione **Incluir informe**. El formato del informe lo determina el formato de representación de informes seleccionado. No elija esta opción si cree que el tamaño del informe superará el límite definido para el sistema de correo electrónico.  
  
    -   Para incluir en el cuerpo del mensaje de correo electrónico la dirección URL del informe, seleccione **Incluir vínculo**.  
  
    > [!NOTE]  
    >  Si desactiva estas dos opciones, solo se enviará el texto de la notificación de la línea Asunto.  
  
6.  Elija un formato de representación en el cuadro de lista **Formato de representación** . Esta opción está disponible si selecciona **Incluir informe** para incrustar o adjuntar una copia del informe.  
  
    -   Para incrustar el informe en el cuerpo del mensaje de correo electrónico, seleccione **Archivo web**.  
  
    -   Para enviar el informe como datos adjuntos, elija cualquiera de los otros formatos de representación.  
  
7.  Seleccione una prioridad del cuadro de lista **Prioridad** . En [!INCLUDE[msCoName](../../includes/msconame-md.md)] Exchange, esta configuración establece una marca para el nivel de importancia del mensaje de correo electrónico.  
  
8.  Especifique cuándo desea que se entregue el informe:  
  
    -   Para programar una hora de entrega, haga clic en **Cuando termina la ejecución del informe programado** y después en **Seleccionar programación**. Se abre una página de programación.  
  
    -   Para seleccionar una programación compartida predefinida que ya tenga la fecha, hora e información de periodicidad que desea utilizar, haga clic en **Según una programación compartida**y, a continuación, seleccione la programación que se va a utilizar.  
  
    -   Para entregar el informe cuando una instantánea de informe se actualice con una versión más reciente, haga clic en**Cuando se actualiza el contenido del informe**. Si se suscribe a un informe que recupera los datos en intervalos programados, la programación utilizada para actualizar los datos determina cuándo se procesa su suscripción.  
  
    > [!NOTE]  
    >  Esta opción solo está disponible para instantáneas que ya están asociadas a una programación de actualización.  
  
9. En el caso de informes con parámetros, especifique los parámetros que se van a utilizar en el informe de esta suscripción. Los parámetros especificados pueden ser diferentes de los que se utilizaron para ejecutar el informe a petición o en otras operaciones programadas.  
  
##  <a name="bkmk_modify_subscription"></a> Para modificar una suscripción  
 Puede modificar una suscripción en cualquier momento. Si modifica una suscripción mientras se está procesando, la configuración actualizada se utilizará si se guarda en la base de datos del servidor de informes antes de que la extensión de entrega reciba los datos de la suscripción. De lo contrario, se utilizará la configuración existente.  
  
 Para buscar una suscripción, utilice la página **Mis suscripciones** o vea las definiciones de suscripción asociadas a un informe. No se pueden buscar suscripciones directamente, ni buscarlas basándose en el nombre del propietario, la información del desencadenador, la información de estado, etc.  
  
 Los administradores del servidor de informes también pueden modificar o eliminar las suscripciones.  
  
> [!NOTE]  
>  El administrador de un servidor de informes no puede administrar desde un lugar todas las suscripciones individuales que estén utilizándose en un servidor de informes determinado. Sin embargo, los administradores del servidor de informes pueden tener acceso a cada suscripción individual para modificarla o eliminarla.  
  
##  <a name="bkmk_delete_subscription"></a> Para eliminar una suscripción  
 Para eliminar una suscripción"  
  
1.  Inicie el [Administrador de informes &#40;Modo nativo de SSRS&#41;](../report-manager-ssrs-native-mode.md).  
  
2.  En el Administrador de informes, haga clic en **Mis suscripciones** en la barra de herramientas global y navegue hasta la suscripción que desea modificar o eliminar.  
  
3.  O bien, en la pestaña **Suscripciones** de un informe abierto, busque la suscripción que desea modificar o eliminar. Realice una de las siguientes acciones:  
  
    1.  Para modificar una suscripción, haga clic en **Edición**.  
  
    2.  Para eliminar una suscripción, active la casilla situada junto a la suscripción y, a continuación, haga clic en **Eliminar**.  
  
 En este tema no se explica cómo cancelar una suscripción que se está procesando actualmente en el servidor de informes. Para obtener más información sobre la cancelación de suscripciones, vea [administrar un proceso en ejecución](manage-a-running-process.md)  
  
 Si desea terminar una suscripción y no la encuentra con facilidad, tome nota del informe que reciba y búsquelo por nombre. Una vez que tenga acceso al informe, puede quitarse de la suscripción. Si no encuentra la suscripción, es posible que se trate de una suscripción controlada por datos. Para obtener más información, póngase en contacto con el administrador del servidor de informes.  
  
 La suscripción se elimina automáticamente si se elimina el informe subyacente. Si elimina una suscripción mientras se está procesando, ésta se detiene si la operación de eliminación se produce antes de que la extensión de entrega reciba los datos de la suscripción. De lo contrario, se continúa procesando la suscripción.  
  
## <a name="see-also"></a>Vea también  
 [Tareas y permisos](../security/tasks-and-permissions.md)   
 [Crear y administrar suscripciones para servidores de informes en modo de SharePoint](create-and-manage-subscriptions-for-sharepoint-mode-report-servers.md)   
 [Crear y administrar suscripciones para servidores de informes en modo nativo](../create-manage-subscriptions-native-mode-report-servers.md)   
 [Suscripciones controladas por datos](data-driven-subscriptions.md)   
 [Suscripciones y entrega &#40;Reporting Services&#41;](subscriptions-and-delivery-reporting-services.md)   
 [El Administrador de informes &#40;modo nativo de SSRS&#41;](../report-manager-ssrs-native-mode.md)   
 [Usar Mis suscripciones](use-my-subscriptions-native-mode-report-server.md)  
  
  
