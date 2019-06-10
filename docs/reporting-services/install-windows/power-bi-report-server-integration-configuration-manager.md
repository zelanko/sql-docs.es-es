---
title: Integración del servidor de informes de Power BI (Administrador de configuración) | Microsoft Docs
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.topic: conceptual
ms.date: 09/17/2017
ms.openlocfilehash: c99eb7091cd72be40f2acb45e5e7bebf8a71526e
ms.sourcegitcommit: 1800fc15075bb17b50d0c18b089d8a64d87ae726
ms.translationtype: MTE75
ms.contentlocale: es-ES
ms.lasthandoff: 06/04/2019
ms.locfileid: "66499608"
---
# <a name="power-bi-report-server-integration-configuration-manager"></a>Integración del servidor de informes de Power BI (Administrador de configuración)

[!INCLUDE[ssrs-appliesto](../../includes/ssrs-appliesto.md)] [!INCLUDE[ssrs-appliesto-2016-and-later](../../includes/ssrs-appliesto-2016-and-later.md)] [!INCLUDE[ssrs-appliesto-pbirsi](../../includes/ssrs-appliesto-pbirs.md)]

La página  **Integración de Power BI** del Administrador de configuración de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] se usa para registrar el servidor de informes con el inquilino administrado de Azure Active Directory (AD) deseado para permitir que los usuarios del servidor de informes anclen elementos de informe admitidos en paneles de [!INCLUDE[sspowerbi](../../includes/sspowerbi-md.md)] . Para obtener una lista de los elementos admitidos que se pueden anclar, vea [Pin Reporting Services items to Power BI Dashboards (Anclar elementos de Reporting Services en paneles de Power BI)](../../reporting-services/pin-reporting-services-items-to-power-bi-dashboards.md).

## <a name="bkmk_requirements"></a> Requisitos para la integración de Power BI

Además de una conexión activa a Internet para que pueda examinar el servicio [!INCLUDE[sspowerbi](../../includes/sspowerbi-md.md)] , se requiere lo siguiente para completar la integración de [!INCLUDE[sspowerbi](../../includes/sspowerbi-md.md)].

- **Azure Active Directory:** su organización debe usar Azure Active Directory, que proporciona administración de identidades y directorios para servicios de Azure y aplicaciones web. Para obtener más información, consulte [¿Qué es Azure Active Directory?](https://azure.microsoft.com/documentation/articles/active-directory-whatis/).

- **Inquilino administrado:** el panel de [!INCLUDE[sspowerbi](../../includes/sspowerbi-md.md)] en el que quiere anclar elementos de informe debe formar parte de un inquilino administrado de Azure AD.  La primera vez que su organización se suscribe a servicios de Azure, como Office 365 y Microsoft Intune, se crea automáticamente un inquilino administrado.   Actualmente no se admiten inquilinos virales.  Para obtener más información, vea las secciones "Qué es un inquilino de Azure AD" y "Obtención de un directorio de Azure AD" en [¿Qué es un directorio de Azure AD?](https://msdn.microsoft.com/library/azure/jj573650.aspx#BKMK_WhatIsAnAzureADTenant).

- El usuario que lleve a cabo la integración de [!INCLUDE[sspowerbi](../../includes/sspowerbi-md.md)] debe ser miembro del inquilino de Azure AD, administrador del sistema de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] y administrador del sistema de la base de datos del catálogo ReportServer.

- El usuario que lleve a cabo la integración de [!INCLUDE[sspowerbi](../../includes/sspowerbi-md.md)] debe iniciar el Administrador de configuración de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] con la cuenta usada para instalar [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]o con la cuenta en la que se ejecuta el servicio de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]

- Los informes desde los que quiera anclar elementos deben usar credenciales almacenadas. Esto no es un requisito de la integración de [!INCLUDE[sspowerbi](../../includes/sspowerbi-md.md)] propiamente dicha, sino del proceso de actualización de los elementos anclados.  Al anclar un elemento de informe se crea una suscripción de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] para administrar la programación de actualización de los iconos de [!INCLUDE[sspowerbi](../../includes/sspowerbi-md.md)]. [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] requieren credenciales almacenadas. Si un informe no usa credenciales almacenadas, los usuarios seguirán pudiendo anclar elementos de informe, pero cuando la suscripción asociada intente actualizar los datos a [!INCLUDE[sspowerbi](../../includes/sspowerbi-md.md)], verán un mensaje de error similar al siguiente en la página **My Subscriptions** (Mis suscripciones).

    PowerBI Delivery error: dashboard: IT Spend Analysis Sample, visual: Chart2, error: (Error de entrega de PowerBI: panel: ejemplo de análisis de gasto en TI, objeto visual: gráfico 2, error:) La acción actual no se puede completar. Las credenciales del origen de datos del usuario no cumplen los requisitos necesarios para ejecutar este informe o conjunto de datos compartido. O bien la credencial del origen de datos del usuario.

Para más información sobre cómo almacenar credenciales, vea la sección "Configurar credenciales almacenadas para un origen de datos específico de informe (modo Nativo)" de [Almacenar credenciales en un origen de datos de Reporting Services](../../reporting-services/report-data/store-credentials-in-a-reporting-services-data-source.md).

Un administrador puede revisar los archivos de registro de  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] para obtener más información.  Verá mensajes similares a los siguientes. Una excelente manera de revisar y supervisar los archivos de registro de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] es usar [!INCLUDE[msCoName](../../includes/msconame-md.md)] Power Query en los archivos.  Para obtener más información y ver un breve vídeo, consulte [Report Server Service Trace Log](../../reporting-services/report-server/report-server-service-trace-log.md).

- subscription!WindowsService_1!1458!09/24/2015-00:09:27:: e ERROR: PowerBI Delivery error: dashboard: IT Spend Analysis Sample, visual: Chart2, error: The current action cannot be completed. (subscription!WindowsService_1!1458!09/24/2015-00:09:27:: e ERROR: error de entrega de PowerBI: panel: ejemplo de análisis de gasto en TI, visual: Chart2, error: La acción actual no se puede completar). Las credenciales del origen de datos del usuario no cumplen los requisitos necesarios para ejecutar este informe o conjunto de datos compartido. Es posible que las credenciales del origen de datos del usuario no estén almacenadas en la base de datos del servidor de informes, o bien que el origen de datos del usuario esté configurado para no requerir credenciales pero no se haya configurado la cuenta de ejecución desatendida.

- notification!WindowsService_1!1458!09/24/2015-00:09:27:: e ERROR: Error occurred processing subscription fcdb8581-d763-4b3b-ba3e-8572360df4f9: PowerBI Delivery error: dashboard: IT Spend Analysis Sample, visual: Chart2, error: The current action cannot be completed. (notification!WindowsService_1!1458!09/24/2015-00:09:27:: e ERROR: Error al procesar la suscripción fcdb8581-d763-4b3b-ba3e-8572360df4f9: Error de entrega de PowerBI: panel: ejemplo de análisis de gasto en TI, objeto visual: gráfico 2, error: La acción actual no se puede completar). Las credenciales del origen de datos del usuario no cumplen los requisitos necesarios para ejecutar este informe o conjunto de datos compartido. Es posible que las credenciales del origen de datos del usuario no estén almacenadas en la base de datos del servidor de informes, o bien que el origen de datos del usuario esté configurado para no requerir credenciales pero no se haya configurado la cuenta de ejecución desatendida.

## <a name="bkmk_steps2integrate"></a> Para integrar y registrar el servidor de informes

Complete los pasos siguientes desde el Administrador de configuración de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] . Para más información, vea [Administrador de configuración de Reporting Services](../../reporting-services/install-windows/reporting-services-configuration-manager-native-mode.md).

1. Seleccione la página de integración de [!INCLUDE[sspowerbi](../../includes/sspowerbi-md.md)] .

2. Seleccione **Registrarse con Power BI**.

    >[!Note]
    > Asegúrese de que el puerto 443 no está bloqueado.

3. En el cuadro de diálogo de inicio de sesión de [!INCLUDE[msCoName](../../includes/msconame-md.md)] , escriba las credenciales que use para iniciar sesión en [!INCLUDE[sspowerbi](../../includes/sspowerbi-md.md)].

4. Una vez completado el registro, en la sección **Detalles de registro de Power BI** , se indicará el identificador del inquilino de Azure y las direcciones URL de redireccionamiento.  Las direcciones URL se usan como parte del proceso de inicio de sesión y de comunicación para que el panel de [!INCLUDE[sspowerbi](../../includes/sspowerbi-md.md)] se vuelva a comunicar con el servidor de informes registrado.

5. Seleccione el botón **Copiar** de la ventana **Resultados** para copiar los detalles de registro en el Portapapeles de Windows. De este modo, podrá guardarlos para consultarlos en el futuro.

## <a name="bkmk_unregister"></a> Anular el registro con Power BI

**Anular el registro** : la anulación del registro del servidor de informes de Azure Active Directory tendrá como resultado lo siguiente:

- El vínculo **My Settings** (Mi configuración) ya no estará visible en la barra de menús del portal web.

- Los elementos de informe que se hayan anclado seguirán anclados en los paneles, pero los iconos ya no se actualizarán en el panel.

- Las suscripciones de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] que estaban actualizando los iconos seguirán existiendo en el servidor de informes, pero cuando se ejecuten según la programación configurada, mostrarán un mensaje de error similar al siguiente.

    **No se pudo cargar la extensión de entrega para esta suscripción.**

En la página **Power BI** del Administrador de configuración, seleccione el botón **Anular el registro con Power BI** .

##  <a name="bkmk_updateregistration"></a> Actualizar el registro

Use la opción **Update Registration** (Actualizar el registro) si ha cambiado la configuración del servidor de informes. Por ejemplo, si quiere agregar o quitar las direcciones URL que los usuarios usan para ir al [!INCLUDE[ssRSWebPortal](../../includes/ssrswebportal.md)].

- En el Administrador de configuración de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] , seleccione la **Dirección URL del Portal web**.

     Seleccione **Avanzado**.

- Seleccione **Agregar** para agregar una nueva identidad HTTP al [!INCLUDE[ssRSWebPortal](../../includes/ssrswebportal.md)] y, después, seleccione **Aceptar**.

     El icono [!INCLUDE[sspowerbi](../../includes/sspowerbi-md.md)] cambiará para indicar que la configuración del servidor ha cambiado.  ![ssrs_powebi_icon_warning](../../reporting-services/install-windows/media/ssrs-powebi-icon-warning.png "ssrs_powebi_icon_warning")

- En la página **Integración de Power BI** , haga clic en **Actualizar registro**.

     Se le pedirá que inicie sesión en Azure AD. La página se actualizará y verá la nueva dirección URL en la lista **Redirect URLs**(Direcciones URL de redireccionamiento).

##  <a name="bkmk_integration_process"></a> Resumen del proceso de integración y anclaje de Power BI

En esta sección se resumen los pasos básicos y las tecnologías implicadas en la integración del servidor de informes con [!INCLUDE[sspowerbi](../../includes/sspowerbi-md.md)] y el anclaje de un elemento de informe a un panel.

 **Integración:**

1. En el Administrador de configuración, al seleccionar el botón **Registrarse con Power BI** , se le pedirá que inicie sesión en Azure Active Directory.

2. La aplicación cliente de [!INCLUDE[sspowerbi](../../includes/sspowerbi-md.md)] se registra con el inquilino administrado.

3. El inquilino administrado dentro de Azure Active Directory es donde se crea la aplicación cliente de Power BI.

4. El registro incluye una o varias direcciones URL de redireccionamiento que se usan cuando los usuarios inician sesión desde el servidor de informes.  El identificador de la aplicación y las direcciones URL se guardan en la base de datos ReportServer. La dirección URL de redireccionamiento se usa durante las llamadas de autenticación a Azure, para que la llamada pueda regresar al servidor de informes. Por ejemplo, cuando los usuarios inician sesión o anclan elementos a un panel.

5. El identificador de la aplicación y las direcciones URL se muestran en el Administrador de configuración.

 ![ssrs_pbiflow_integration](../../reporting-services/install-windows/media/ssrs-pbiflow-integration.png "ssrs_pbiflow_integration")

 **Cuando un usuario ancla un elemento de informe a un panel:**

1. Los usuarios obtienen una vista previa de los informes en el [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] [!INCLUDE[ssRSWebPortal](../../includes/ssrswebportal.md)] y la primera vez que hacen clic para anclar un elemento de informe desde el [!INCLUDE[ssRSWebPortal](../../includes/ssrswebportal.md)].

2. Se les redirigirá a la página de inicio de sesión de Azure AD. También pueden iniciar sesión desde la página [!INCLUDE[ssRSWebPortal](../../includes/ssrswebportal.md)] **My Settings** page. Cuando los usuarios inicien sesión en el inquilino administrado de Azure, se establecerá una relación entre su cuenta de Azure y los permisos de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] .  Para obtener más información, consulte [La configuración de la integración de Power BI &#40;portal web&#41;](../my-settings-for-power-bi-integration-web-portal.md).

3. Se devuelve un token de seguridad del usuario al servidor de informes.

4. El token de seguridad del usuario se guarda en la base de datos ReportServer.

5. Se recupera del servicio de [!INCLUDE[sspowerbi](../../includes/sspowerbi-md.md)] una lista de grupos y paneles a los que tiene acceso el usuario.  El usuario selecciona el panel y el grupo de destino y configura la frecuencia con la que quiere que los datos se actualicen en el icono de [!INCLUDE[sspowerbi](../../includes/sspowerbi-md.md)] .

6. El elemento de informe se ancla al panel.

7. Se crea una suscripción de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] para administrar la actualización programada del elemento de informe en el icono del panel. La suscripción usa el token de seguridad que se creó cuando el usuario inició sesión.

     El token es válido durante **90 días**. Transcurrido este tiempo, los usuarios deben iniciar sesión de nuevo para crear un nuevo token de usuario. Cuando el token expire, los iconos anclados seguirán mostrándose en el panel, pero ya no se actualizarán los datos.  Las suscripciones de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] que se usan para los elementos anclados generarán un error hasta que se cree un nuevo token de usuario. Vea [La configuración de la integración de Power BI &#40;portal web&#41;](../my-settings-for-power-bi-integration-web-portal.md). para obtener más información.

La segunda vez que un usuario ancle un elemento, se omitirán los pasos de 1 a 4. En su lugar, se recuperarán el identificador de la aplicación y las direcciones URL de la base de datos ReportServer y el flujo continuará con el paso 5.

![ssRS-pin-to-powerbi-flow](../../reporting-services/install-windows/media/ssrs-pin-to-powerbi-flow.png)

 **Cuando se active una suscripción para actualizar un icono del panel:**

1. Cuando la suscripción de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] se activa, el informe se representa.

2. El token de usuario se recupera de la base de datos ReportServer.

3. Se envían los datos y el estado del elemento de informe con el token al servicio de [!INCLUDE[sspowerbi](../../includes/sspowerbi-md.md)].

4. El token se envía a Azure AD para la validación. Si el token es válido, los datos del elemento de informe se envían al icono del panel y se actualiza la propiedad de fecha del icono.

5. Si el token no es válido, se devuelve un error que se registra con el servidor de informes.  No se envía el estado ni otra información al panel.

![ssRS-subscription-to-powerbi-flow](../../reporting-services/install-windows/media/ssrs-subscription-to-powerbi-flow.png)

   <iframe width="560" height="315" src="https://www.youtube.com/embed/QhPQObqmMPc" frameborder="0" allowfullscreen></iframe>

## <a name="considerations-and-limitations"></a>Consideraciones y limitaciones

* No se admiten inquilinos virales y gubernamentales.

## <a name="next-steps"></a>Pasos siguientes

[La configuración de la integración de Power BI &#40;portal web&#41;](../my-settings-for-power-bi-integration-web-portal.md)  
[Anclado de elementos de Reporting Services en paneles de Power BI](../../reporting-services/pin-reporting-services-items-to-power-bi-dashboards.md)
[Paneles de Power BI](https://powerbi.microsoft.com/documentation/powerbi-service-dashboards/)  

¿Tiene alguna pregunta más? [Puede plantear sus dudas en el foro de Reporting Services](https://go.microsoft.com/fwlink/?LinkId=620231).
