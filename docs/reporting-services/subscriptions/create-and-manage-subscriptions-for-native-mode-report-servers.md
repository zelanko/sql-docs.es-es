---
title: Crear y administrar suscripciones para servidores de informes en modo nativo | Microsoft Docs
ms.date: 03/14/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: subscriptions
ms.topic: conceptual
helpviewer_keywords:
- standard subscriptions [Reporting Services]
- subscriptions [Reporting Services], standard
ms.assetid: 5ab1c661-9bfa-434a-b315-faac34ed12b1
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 2efb0c6c246ba8575838acc6d04609a6db406ce6
ms.sourcegitcommit: dda9a1a7682ade466b8d4f0ca56f3a9ecc1ef44e
ms.translationtype: MTE75
ms.contentlocale: es-ES
ms.lasthandoff: 05/14/2019
ms.locfileid: "65578385"
---
# <a name="create-and-manage-subscriptions-for-native-mode-report-servers"></a>Crear y administrar suscripciones para servidores de informes en modo nativo
  Una suscripción estándar es la que crean usuarios individuales que desean recibir un informe por correo electrónico o en una carpeta compartida. Este tema proporciona información sobre las suscripciones estándar que los usuarios individuales crean y administran. Las suscripciones controladas por datos tienen diferentes requisitos y pasos, y se tratan en otro tema. Para obtener más información, vea [Cómo crear, modificar y eliminar suscripciones controladas por datos](../../reporting-services/subscriptions/create-modify-and-delete-data-driven-subscriptions.md).  
  
 **En este tema:**  
  
-   [Requisitos generales de las suscripciones](#bkmk_create_subscription)  
  
-   [Para crear una suscripción a recursos compartidos de archivos](#bkmk_create_fileshare_subscription)  
  
-   [Para crear una suscripción de correo electrónico](#bkmk_create_email_subscription)  
  
-   [Para modificar una suscripción](#bkmk_modify_subscription)  
  
-   [Para eliminar una suscripción](#bkmk_delete_subscription)  
  
##  <a name="bkmk_create_subscription"></a> Requisitos generales de las suscripciones  
 En el contenido de este tema se explica cómo se crean suscripciones en un servidor de informes en modo nativo mediante el Administrador de informes de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] . Una vez definida una suscripción, puede tener acceso a ella en el Administrador de informes a través de la página Mis suscripciones o la pestaña **Suscripciones** de un informe específico.  
  
 En[Crear y administrar suscripciones para servidores de informes en modo de SharePoint](../../reporting-services/subscriptions/create-and-manage-subscriptions-for-sharepoint-mode-report-servers.md) se explica cómo se usan las páginas de aplicación de un sitio de SharePoint para suscribirse a los informes de un servidor de informes que se ejecuta en el modo de SharePoint.  
  
-   Para utilizar la entrega por correo electrónico, el servidor de informes debe estar configurado para una conexión de puerta de enlace o servidor SMTP antes de crear la suscripción.  
  
-   Para utilizar la entrega a recursos compartidos de archivos, se debe haber definido la carpeta de destino. Para obtener más información, vea [Configurar un servidor de informes para la entrega de correo electrónico (Administrador de configuración de SSRS)](https://msdn.microsoft.com/b838f970-d11a-4239-b164-8d11f4581d83).  
  
 Antes de que pueda suscribirse a un informe, hay que configurar el origen de datos del informe de modo que utilice credenciales almacenadas o ninguna credencial. Para obtener más información, vea [Almacenamiento de las credenciales en un origen de datos de Reporting Services](../../reporting-services/report-data/store-credentials-in-a-reporting-services-data-source.md). De lo contrario, el botón **Nueva suscripción** no está disponible.  
  
 En este tema no se explica cómo crear una suscripción controlada por datos. Para obtener instrucciones sobre cómo se crea una suscripción controlada por datos, vea [Crear una suscripción controlada por datos &#40;Tutorial de SSRS&#41;](../../reporting-services/create-a-data-driven-subscription-ssrs-tutorial.md) o la Ayuda en pantalla de la página Crear una suscripción controlada por datos del Administrador de informes.  
  
###  <a name="bkmk_create_fileshare_subscription"></a> Para crear una suscripción a recursos compartidos de archivos  
  
1.  Inicie el [Administrador de informes &#40;Modo nativo de SSRS&#41;](https://msdn.microsoft.com/library/80949f9d-58f5-48e3-9342-9e9bf4e57896).  
  
2.  Vaya al informe al que quiera suscribirse. Haga clic en el menú del informe y haga clic en **Suscribirse**.  
  
     ![menú informe](../../reporting-services/subscriptions/media/ssrs-report-menu-report-manager.png "menú informe")  
  
3.  **Descripción**: escriba una descripción para el informe, con un máximo de 512 caracteres.  
  
4.  **Propietario**: el valor predeterminado del campo de propietario es el usuario actual y no se puede editar cuando se crea la suscripción. Sin embargo, puede cambiar las propiedades de la suscripción después de guardarla, incluido el propietario y la descripción.  
  
5.  **Entregado por**: seleccione **Recurso compartido de archivos de Windows**.  
  
6.  **Nombre de archivo**: escriba un nombre de archivo para el informe.  
  
7.  **Agregar una extensión de archivo cuando se crea el archivo**: esta opción agrega una extensión de archivo de tres caracteres al nombre de archivo. La extensión de archivo está determinada por el formato de salida de informes seleccionado.  
  
8.  **Ruta de acceso**: escriba una ruta UNC (convención de nomenclatura universal) para una carpeta existente en la que quiera entregar los informes (por ejemplo, \\\\<nombreDeServidor\>\\<misInformes\>). Incluya dos barras diagonales inversas al comienzo de la ruta de acceso. No escriba una barra diagonal inversa al final.  
  
     ![Suscripción a un recurso compartido de archivos](../../reporting-services/subscriptions/media/ssrs-file-share-subscription.png "Suscripción a un recurso compartido de archivos")  
  
9. **Formato de representación**: seleccione un formato de salida de informes para la entrega de archivos. Elija el formato correspondiente a la aplicación de escritorio que utilizará para abrir el informe. Evite formatos que no representen los informes en un solo flujo o que especifiquen una interactividad no admitida en un archivo estático (por ejemplo, HTML 4.0).  
  
10. **Credenciales**: seleccione esta opción para usar la cuenta de recurso compartido de archivos o las credenciales de usuario específicas de Windows. La opción **Use file share account** (Usar la cuenta de recurso compartido de archivos) está deshabilitada si el administrador de informes no ha configurado una cuenta de recurso compartido de archivos. Para obtener más información, vea [Configuración de la suscripción y una cuenta de recurso compartido de archivos &#40;Administrador de configuración&#41;](../../reporting-services/install-windows/subscription-settings-and-a-file-share-account-configuration-manager.md). En los cuadros de texto **Nombre de usuario** y **Contraseña**, especifique las credenciales necesarias para obtener acceso al recurso compartido de archivos. Use el formato *\<dominio>*\\*\<nombreDeUsuario>* para el nombre de usuario.  
  
11. **Opciones de sobrescritura**:  
  
    -   **No sobrescribir el archivo si existe una versión anterior**: la entrega no se realizará si se detecta que el archivo ya existe.  
  
    -   **Incrementar los nombres de archivo conforme se agregan versiones más recientes**: el servidor de informes agrega un número al nombre del archivo para distinguirlo de otros archivos existentes que tengan el mismo nombre.  
  
12. **Programación**: especifique cuándo quiere que se entregue el informe.  
  
    -   Para programar una hora de entrega, haga clic en **Cuando termina la ejecución del informe programado** y después en el botón **Seleccionar programación** . Se abre una página de programación.  
  
    -   Para seleccionar una programación compartida predefinida que ya tenga la fecha, hora e información de periodicidad que desea utilizar, haga clic en **Según una programación compartida**y, a continuación, seleccione la programación que se va a utilizar.  
  
    -   Para entregar el informe cuando una instantánea de informe se actualice con una versión más reciente, haga clic en**Cuando se actualiza el contenido del informe**. Si se suscribe a un informe que recupera los datos en intervalos programados, la programación utilizada para actualizar los datos determina cuándo se procesa su suscripción.  
  
        > [!NOTE]  
        >  Esta opción solo está disponible para instantáneas que ya están asociadas a una programación de actualización.  
  
13. En el caso de informes con parámetros, especifique los parámetros que se van a utilizar en el informe de esta suscripción. Los parámetros pueden ser diferentes de los que se utilizaron para ejecutar el informe a petición o en otras operaciones programadas.  
  
 El informe se entrega como un archivo estático. Si el informe contiene características interactivas, como por ejemplo, vínculos a otras filas y columnas, éstas no estarán disponibles.  
  
###  <a name="bkmk_create_email_subscription"></a> Para crear una suscripción de correo electrónico  
  
1.  Inicie el [Administrador de informes &#40;Modo nativo de SSRS&#41;](https://msdn.microsoft.com/library/80949f9d-58f5-48e3-9342-9e9bf4e57896).  
  
2.  Vaya al informe al que quiera suscribirse. Haga clic en el menú del informe y haga clic en **Suscribirse**.  
  
     ![menú informe](../../reporting-services/subscriptions/media/ssrs-report-menu-report-manager.png "menú informe")  
  
3.  **Descripción**: escriba una descripción para el informe, con un máximo de 512 caracteres.  
  
4.  **Propietario**: el valor predeterminado del campo de propietario es el usuario actual y no se puede editar cuando se crea la suscripción. Sin embargo, puede cambiar las propiedades de la suscripción después de guardarla, incluido el propietario y la descripción.  
  
5.  **Entregado por**: seleccione **Correo electrónico**. Si **Correo electrónico** no está disponible, su servidor de informes no se ha configurado para las suscripciones de correo electrónico. Vea [Configurar un servidor de informes para la entrega de correo electrónico (Administrador de configuración de SSRS)](https://msdn.microsoft.com/b838f970-d11a-4239-b164-8d11f4581d83).  
  
6.  **Para**: el nombre del destinatario del campo Para: se rellena automáticamente con su cuenta de usuario de dominio. Compruebe que el formato es [nombre de usuario]@[dominio.com]. La configuración del servidor de informes determina si el campo **Para** se rellena automáticamente con su cuenta de usuario. Para obtener más información sobre cómo cambiar las direcciones de correo electrónico de la configuración, vea [Configurar un servidor de informes para la entrega de correo electrónico (Administrador de configuración de SSRS)](https://msdn.microsoft.com/b838f970-d11a-4239-b164-8d11f4581d83).  
  
    > [!NOTE]  
    >  Dependiendo de sus permisos, podrá escribir la dirección de correo electrónico donde desea recibir el informe. Para especificar varias direcciones de correo electrónico, sepárelas con un punto y coma (;). También puede escribir direcciones de correo electrónico adicionales en los cuadros de texto **CC**, **CCO**y **Responder a** . Esto requiere que tenga permiso para administrar todas las suscripciones.  
  
7.  **Asunto**: el valor predeterminado es "@ReportName se ejecutó a las @ExecutionTime". Puede editar el asunto, pero tenga en cuenta que @ReportName y @ExecutionTime son las únicas variables globales que se admiten en el campo **Asunto**.  
  
8.  Seleccione las opciones de entrega del siguiente modo:  
  
    -   **Incluir informe**: seleccione esta opción para insertar o adjuntar una copia del informe. El formato del informe lo determina el formato de representación de informes seleccionado. No elija esta opción si cree que el tamaño del informe superará el límite definido para el sistema de correo electrónico.  
  
    -   **Incluir vínculo**: seleccione esta opción para incluir en el cuerpo del mensaje de correo electrónico la dirección URL del informe.  
  
    > [!NOTE]  
    >  Si desactiva estas dos opciones, solo se enviará el texto de la notificación de la línea Asunto.  
  
9. Elija un formato de representación en el cuadro de lista **Formato de representación** . Esta opción está disponible si selecciona **Incluir informe** para incrustar o adjuntar una copia del informe.  
  
    -   Para incrustar el informe en el cuerpo del mensaje de correo electrónico, seleccione **Archivo web**.  
  
    -   Para enviar el informe como datos adjuntos, elija cualquiera de los otros formatos de representación.  
  
10. Seleccione una prioridad del cuadro de lista **Prioridad** . En [!INCLUDE[msCoName](../../includes/msconame-md.md)] Exchange, esta configuración establece una marca para el nivel de importancia del mensaje de correo electrónico.  
  
11. Especifique cuándo desea que se entregue el informe:  
  
    -   Para programar una hora de entrega, haga clic en **Cuando termina la ejecución del informe programado** y después en **Seleccionar programación**. Se abre una página de programación.  
  
    -   Para seleccionar una programación compartida predefinida que ya tenga la fecha, hora e información de periodicidad que desea utilizar, haga clic en **Según una programación compartida**y, a continuación, seleccione la programación que se va a utilizar.  
  
    -   Para entregar el informe cuando una instantánea de informe se actualice con una versión más reciente, haga clic en**Cuando se actualiza el contenido del informe**. Si se suscribe a un informe que recupera los datos en intervalos programados, la programación utilizada para actualizar los datos determina cuándo se procesa su suscripción.  
  
    > [!NOTE]  
    >  Esta opción solo está disponible para instantáneas que ya están asociadas a una programación de actualización.  
  
12. En el caso de informes con parámetros, especifique los parámetros que se van a utilizar en el informe de esta suscripción. Los parámetros especificados pueden ser diferentes de los que se utilizaron para ejecutar el informe a petición o en otras operaciones programadas.  
  
##  <a name="bkmk_modify_subscription"></a> Para modificar una suscripción  
 Puede modificar una suscripción en cualquier momento. Si modifica una suscripción mientras se está procesando, la configuración actualizada se usará si se guarda en el servidor de informes antes de que la extensión de entrega reciba los datos de la suscripción. De lo contrario, se utilizará la configuración existente.  
  
 El usuario que crea una suscripción es su propietario. Cada usuario puede modificar o eliminar las suscripciones de las que sea propietario. Puede cambiar el propietario del informe desde la página de propiedades de la suscripción o puede cambiar la propiedad mediante programación. Para obtener más información, vea:  
  
-   [Uso de PowerShell para cambiar y enumerar a los propietarios de una suscripción de Reporting Services y ejecutar una suscripción](../../reporting-services/subscriptions/manage-subscription-owners-and-run-subscription-powershell.md)  
  
-   <xref:ReportService2010.ReportingService2010.ChangeSubscriptionOwner%2A>  
  
 Para buscar una suscripción, utilice la página **Mis suscripciones** o vea las definiciones de suscripción asociadas a un informe. No se pueden buscar suscripciones directamente, ni buscarlas basándose en el nombre del propietario, la información del desencadenador, la información de estado, etc.  
  
 Los administradores del servidor de informes también pueden modificar o eliminar las suscripciones.  
  
> [!NOTE]  
>  El administrador de un servidor de informes no puede administrar desde un lugar todas las suscripciones individuales que estén utilizándose en un servidor de informes determinado. Sin embargo, los administradores del servidor de informes pueden tener acceso a cada suscripción individual para modificarla o eliminarla.  
  
##  <a name="bkmk_delete_subscription"></a> Para eliminar una suscripción  
 Para eliminar una suscripción"  
  
1.  Inicie el [Administrador de informes &#40;Modo nativo de SSRS&#41;](https://msdn.microsoft.com/library/80949f9d-58f5-48e3-9342-9e9bf4e57896).  
  
2.  En el Administrador de informes, haga clic en **Mis suscripciones** en la barra de herramientas y vaya a la suscripción que quiere modificar o eliminar.  
  
3.  Abra el menú del informe y haga clic en **Eliminar**.  
  
     ![menú informe](../../reporting-services/subscriptions/media/ssrs-report-menu-report-manager.png "menú informe")  
  
 Para cancelar una suscripción que se está procesando actualmente en el servidor de informes, vea [Administrar un proceso en ejecución](../../reporting-services/subscriptions/manage-a-running-process.md).  
  
 Si desea terminar una suscripción y no la encuentra, tome nota del informe que reciba y búsquelo por nombre. Una vez que tenga acceso al informe, puede quitarse de la suscripción. Si no encuentra la suscripción, es posible que se trate de una suscripción controlada por datos. Para obtener más información, póngase en contacto con el administrador del servidor de informes.  
  
 La suscripción se elimina automáticamente si se elimina el informe subyacente. Si elimina una suscripción mientras se está procesando, ésta se detiene si la operación de eliminación se produce antes de que la extensión de entrega reciba los datos de la suscripción. De lo contrario, se continúa procesando la suscripción.  
  
## <a name="see-also"></a>Consulte también  
 [Crear y administrar suscripciones para servidores de informes en modo de SharePoint](../../reporting-services/subscriptions/create-and-manage-subscriptions-for-sharepoint-mode-report-servers.md)   
 [Use PowerShell para cambiar y enumerar a los propietarios de una suscripción de Reporting Services y ejecutar una suscripción](../../reporting-services/subscriptions/manage-subscription-owners-and-run-subscription-powershell.md)   
 [Data-Driven Subscriptions](../../reporting-services/subscriptions/data-driven-subscriptions.md)   
 [Suscripciones y entrega &#40;Reporting Services&#41;](../../reporting-services/subscriptions/subscriptions-and-delivery-reporting-services.md)   
 [Administrador de informes &#40;Modo nativo de SSRS&#41;](https://msdn.microsoft.com/library/80949f9d-58f5-48e3-9342-9e9bf4e57896)   
 [Usar Mis suscripciones &#40;servidor de informes en modo nativo&#41;](../../reporting-services/subscriptions/use-my-subscriptions-native-mode-report-server.md)  
  
  
