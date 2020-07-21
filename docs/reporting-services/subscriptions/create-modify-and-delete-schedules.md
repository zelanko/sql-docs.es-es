---
title: Crear, modificar y eliminar programaciones | Microsoft Docs
description: Cree, modifique y elimine programaciones compartidas de Reporting Services. En el modo nativo, use el portal web o Management Studio. En el modo de SharePoint, use la aplicación de servicio.
ms.date: 06/11/2019
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: subscriptions
ms.topic: conceptual
helpviewer_keywords:
- report-specific schedules [Reporting Services]
- shared schedules [Reporting Services]
- modifying schedules
- removing schedules
- shared schedules [Reporting Services], creating
- shared schedules [Reporting Services], modifying
- schedules [Reporting Services], deleting
- deleting schedules
- schedules [Reporting Services], creating
- schedules [Reporting Services], modifying
- shared schedules [Reporting Services], deleting
ms.assetid: 05da5f3d-9222-43a9-893b-aa10f0f690f8
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: ca14dd80ab00e0a2930ddabdf206f8fbaf6c08eb
ms.sourcegitcommit: c6a2efe551e37883c1749bdd9e3c06eb54ccedc9
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/06/2020
ms.locfileid: "80742272"
---
# <a name="create-modify-and-delete-schedules"></a>Create, Modify, and Delete Schedules
  Use este artículo para obtener información sobre cómo crear, modificar y eliminar programaciones compartidas de [!INCLUDE[ssRSnoversion_md](../../includes/ssrsnoversion-md.md)].  Para administrar programaciones compartidas para el modo nativo, use la página Programaciones del portal web o la carpeta Programaciones compartidas de [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]. Para el modo de SharePoint, use las páginas de administración para la aplicación de servicio de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] .

 Use uno de los métodos siguientes para determinar si una programación compartida se usa de forma activa:

-   **Portal web:** en la pestaña **Programaciones** de la **Configuración del sitio**, revise los valores de los campos de fecha Última ejecución, Siguiente ejecución y Estado. Cuando una programación ya no se ejecuta porque ha expirado, aparece su fecha de expiración en el campo Estado. Para más información, vea [Web portal (SSRS Native Mode)](../../reporting-services/web-portal-ssrs-native-mode.md).

-   **SQL Server Management Studio:** visualice la página **Informes** de una programación compartida específica. Esta página enumera todos los informes y los conjuntos de datos compartidos que utilizan la programación compartida. Para más información, consulte [Reporting Services en SQL Server Management Studio](../../reporting-services/tools/reporting-services-in-sql-server-management-studio-ssrs.md).

-  **Registros:** Viendo los archivos de registro de ejecución de informes o registros de seguimiento para determinar si se han ejecutado los informes las veces especificadas por la programación. Para más información, vea [Archivos de registro y orígenes de Reporting Services](../../reporting-services/report-server/reporting-services-log-files-and-sources.md).

## <a name="when-you-delete-a-shared-schedule"></a>Cuándo eliminar una programación compartida
Las programaciones compartidas se deben eliminar manualmente desde la página Programaciones del portal web o la carpeta Programaciones compartidas de [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]. Si se elimina una programación compartida que esté en uso, se sustituirán todas las referencias a la misma por programaciones específicas del informe.

Si elimina una programación compartida usada por varios informes y suscripciones, el servidor de informes creará calendarios individuales para cada informe y suscripción que haya usado anteriormente la programación compartida. Cada nueva programación individual contendrá la fecha, la hora y el patrón de periodicidad que se especificó en la programación compartida. Tenga en cuenta que [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] no proporciona la administración central de las programaciones individuales. Si elimina una programación compartida, tendrá que mantener la información de programación para cada elemento individual.

**Nota:**  Si no está seguro de que se use una programación compartida, considere su eliminación en [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] en lugar de en el portal web. [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] proporciona las mismas características de administración de programación compartida que el Administrador de informes, además de una página adicional Informes que muestra el nombre de cada informe que la programación usa.

 Es importante saber que no es lo mismo eliminar una programación que hacer que expire. Las fechas de expiración se utilizan para detener una programación, no para eliminarla. Dado que las programaciones se usan para automatizar diversas características, nunca se eliminan automáticamente. Las programaciones expiradas constituyen una prueba para los administradores de los servidores de informes con relación a las causas que han detenido un proceso automático. Sin la existencia de la programación expirada, los administradores podrían errar en el diagnóstico del problema o perder demasiado tiempo en intentar solucionar un proceso que en realidad es completamente válido.

 ## <a name="when-you-delete-a-report-specific-schedule"></a>Cuándo eliminar una programación específica de informe
Se eliminan las programaciones específicas de informes y suscripciones al eliminar el informe o la suscripción, o al elegir un enfoque diferente para ejecutar el informe o la suscripción. Por ejemplo, al seleccionar **Ejecutar este informe siempre con los datos más recientes** , se eliminará una programación específica de informes que creó para ejecutar un informe como una instantánea de ejecución de informes.

Las programaciones específicas del informe que han expirado permanecen adjuntas al informe. Es posible determinar si una programación ha expirado con solo revisar la fecha final. Las programaciones compartidas expiradas se conservan en la lista Programaciones compartidas. El campo Estado indica si la programación ha expirado. Puede volver a aplicar la programación ampliando la fecha de finalización o eliminar la referencia a la programación si ya no la necesita.

## <a name="create-delete-or-modify-a-shared-schedule-web-portal"></a><a name="bkmk_native"></a> Crear, eliminar o modificar una programación compartida (portal web)
 La creación y modificación de una programación consiste en establecer las opciones de frecuencia que determinan el momento en que debe ejecutarse la programación.

 Las programaciones pueden crearse o modificarse en cualquier momento. Sin embargo, si se empieza a ejecutar una programación antes de haber completado las modificaciones, se usará la versión anterior de la misma. La programación revisada no surtirá efecto hasta que se guarde.

 Si modifica una programación compartida, puede pausarla para realizar los cambios. Dichos cambios serán efectivos cuando se reanude la programación.

1. En el portal web, seleccione **Configuración** ![ssrs_portal_settings_gear](../../reporting-services/subscriptions/media/ssrs-portal-settings-gear.png) en la barra de herramientas.  

   >[!NOTE]  
   >Si **Configuración** no está disponible, significa que no tiene permiso de acceso a la configuración del sitio.  

1. Seleccione **Configuración del sitio** en el menú desplegable.
1. Seleccione la pestaña **Programaciones** .
1. Seleccione **+ Nueva programación**. (Para modificar una programación existente, haga clic en el nombre de la programación).
1. Escriba un nombre descriptivo para la programación.
1. Haga clic en **Hora**, **Día**, **Semana**o **Mes**. Haga clic en **Una vez** para crear una programación que se ejecute solo una vez. Cuando se especifica la base de la programación, se muestran más opciones.
1. Opcionalmente, puede seleccionar la fecha en que comenzará la programación. El valor predeterminado es el día actual. Elija una fecha posterior si desea posponer el inicio de la programación.
1. Seleccione la fecha en que finalizará la programación (opcional). La programación se detiene en esa fecha pero no se elimina.
1. Seleccione una hora para la ejecución de la programación.
1. Seleccione **Aceptar**.

### <a name="to-delete-a-shared-schedule-web-portal"></a>Para eliminar una programación compartida (portal web)

1. En el portal web, seleccione **Configuración** ![ssrs_portal_settings_gear](../../reporting-services/subscriptions/media/ssrs-portal-settings-gear.png) en la barra de herramientas.
2. Seleccione **Configuración del sitio** en el menú desplegable.
3. Seleccione la pestaña **Programaciones** .
4. Active la casilla situada junto a la programación compartida que quiere eliminar y, a continuación, seleccione **Eliminar**.

### <a name="create-delete-or-modify-a-shared-schedule--management-studio"></a>Crear, eliminar o modificar una programación compartida (Management Studio)
 Una programación compartida contiene la información de programación y periodicidad que se puede usar en un número cualquiera de suscripciones e informes publicados que se ejecutan en un servidor de informes de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] . Si tiene muchos informes y suscripciones que se ejecutan al mismo tiempo, puede crear una programación compartida para dichos trabajos. Si desea cambiar el patrón de periodicidad o la fecha de finalización con posterioridad, puede realizar la modificación en un lugar.

 Las programaciones compartidas son más sencillas de mantener y le permiten mayor flexibilidad para administrar operaciones programadas. Por ejemplo, puede pausar y reanudar las programaciones compartidas. Además, si desea que se ejecuten demasiadas operaciones programadas al mismo tiempo, puede crear varias programaciones compartidas que se ejecuten en momentos diferentes y, a continuación, ajustar la información de programación hasta que la carga de procesamiento se iguale fuera en el servidor de informes.

#### <a name="to-create-or-modify-a-shared-schedule-management-studio"></a>Para crear o modificar una programación compartida (Management Studio)

1.  Inicie [!INCLUDE[ssManStudioFull_md](../../includes/ssmanstudiofull-md.md)] y conéctese a una instancia de servidor de informes.
2.  En el Explorador de objetos, expanda un nodo de servidor de informes.
3.  Haga clic con el botón derecho en la carpeta **Programaciones compartidas** y, luego, haga clic en **Nueva programación**. De este modo se muestra la página General del cuadro de diálogo **Nueva programación compartida** .

     Para modificar una programación compartida existente, expanda la carpeta Programaciones compartidas, haga clic con el botón derecho en la programación que quiere modificar y, luego, haga clic en **Propiedades**.

4.  Escriba un nombre descriptivo para la programación.
5.  Opcionalmente, puede seleccionar la fecha en que comenzará la programación. El valor predeterminado es el día actual.
6.  Opcionalmente, puede seleccionar la fecha en que finalizará la programación. La programación se detiene en esa fecha pero no se elimina.
7.  Para configurar una programación de repetición, seleccione **Hora**, **Día**, **Semana**o **Mes**. De este modo se muestran más opciones. Utilice estas otras opciones para configurar la frecuencia de la programación, en función de su hora, día, semana o mes preferidos.

     También puede especificar una programación para una vez (no periódica) seleccionando **Una vez**y, luego, especificando una **Hora de inicio**.

8.  Seleccione **Aceptar**.

##### <a name="to-delete-a-shared-schedule-management-studio"></a>Para eliminar una programación compartida (Management Studio)

1.  En el Explorador de objetos, expanda un nodo de servidor de informes.
2.  Para comprobar que los informes no usan actualmente la programación compartida, expanda la carpeta Programaciones compartidas, haga clic con el botón derecho en la programación y haga clic en **Propiedades**.
3. Haga clic en la pestaña **Informes** para ver la lista de informes que actualmente usan la programación.
Haga clic en **Cancelar**.
4.  Expanda la carpeta Programaciones compartidas, haga clic con el botón derecho en la programación que quiere eliminar y, luego, haga clic en **Eliminar**. Aparece el cuadro de diálogo **Eliminar elementos del catálogo** .
5.  Seleccione **Aceptar**.

 Si elimina una programación compartida usada por varios informes y suscripciones, el servidor de informes creará calendarios individuales para cada informe y suscripción que haya usado anteriormente la programación compartida. Cada nueva programación individual contendrá la fecha, la hora y el patrón de periodicidad que se especificó en la programación compartida.

##  <a name="create-and-manage-shared-schedules-sharepoint-mode"></a><a name="bkmk_sharepoint"></a> Crear y administrar programaciones compartidas (modo de SharePoint)
 Para poder crear, modificar o eliminar programaciones compartidas, debe ser administrador del sitio de SharePoint.

 Puede identificar una programación específica mediante su nombre descriptivo. Si no se especifica un nombre, se crea un nombre predeterminado en función de las características de la programación, como su patrón de periodicidad o las fechas y horas de ejecución.

> [!NOTE]
> Al crear programaciones compartidas, se requiere el servicio Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .

### <a name="create-shared-schedules-sharepoint-mode"></a>Crear programaciones compartidas (modo SharePoint)
1.  Haga clic en **Acciones del sitio**.
2.  Haga clic en **Configuración del sitio**.
3.  En la sección Reporting Services, haga clic en **Administrar programaciones compartidas**.
4.  Haga clic en **Agregar programación** para abrir la página Propiedades de la programación.
5.  Escriba un nombre descriptivo para la programación. En las páginas de la aplicación usadas para trabajar con informes de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] , este nombre aparecerá en listas desplegables en las páginas de definición de la programación en todo el sitio. Evite los nombres largos y difíciles de leer. Siga una convención de nomenclatura que coloque la información más descriptiva al principio del nombre.
6.  Elija una frecuencia. Dependiendo de la frecuencia que seleccione, las opciones de programación que aparecen en la página pueden cambiar para admitir esa frecuencia (por ejemplo, si selecciona **Mes**, el nombre de cada mes aparecerá en la página).
7.  Defina la programación. Una sola programación no admite todas las combinaciones de programaciones.
8.  Establezca una fecha de inicio y de fin.
9. Haga clic en **OK**.

### <a name="delete-shared-schedules-sharepoint-mode"></a>Eliminar programaciones compartidas (modo SharePoint)
 Todas las programaciones, sean compartidas o específicas del informe, deben eliminarse manualmente. Si elimina una programación compartida que está utilizándose, todas las referencias a la misma se reemplazarán por programaciones personalizadas sin especificar (es decir, una programación personalizada que no incluye información de fecha u hora).

1.  Haga clic en **Acciones del sitio**.
2.  Haga clic en **Configuración del sitio**.
3.  En la sección Reporting Services, haga clic en **Administrar programaciones compartidas**.
4.  Seleccione la programación y haga clic en **Eliminar**.


## <a name="see-also"></a>Consulte también
 [Programaciones](../../reporting-services/subscriptions/schedules.md)  
 [Pausa y reanudación de programaciones compartidas](../../reporting-services/subscriptions/pause-and-resume-shared-schedules.md)  
 [Informes almacenados en caché (SSRS)](../../reporting-services/report-server/caching-reports-ssrs.md)  
 [Creación, modificación y eliminación de instantáneas del historial de informes](../report-server/create-modify-and-delete-snapshots-in-report-history.md)

