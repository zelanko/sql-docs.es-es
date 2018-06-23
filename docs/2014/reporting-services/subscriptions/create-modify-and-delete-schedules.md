---
title: Crear, modificar y eliminar programaciones | Microsoft Docs
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
caps.latest.revision: 45
author: markingmyname
ms.author: maghan
manager: mblythe
ms.openlocfilehash: c4ac89d35cfe118cb82e945ef48d87c24b56abed
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36106697"
---
# <a name="create-modify-and-delete-schedules"></a>Create, Modify, and Delete Schedules
  Use este tema para obtener información acerca de cómo crear, modificar y eliminar programaciones.  
  
 En este tema:  
  
-   [Información general de la administración de programaciones compartidas](#bkmk_overview)  
  
-   [Crear y administrar programaciones compartidas (modo de SharePoint)](#bkmk_sharepoint)  
  
-   [Crear y administrar programaciones compartidas (modo nativo)](#bkmk_native)  
  
##  <a name="bkmk_overview"></a> Información general de la administración de programaciones compartidas  
 Para administrar programaciones compartidas para el modo nativo, use la página Programaciones del Administrador de informes o la carpeta Programaciones compartidas de [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]. Para el modo de SharePoint, use las páginas de administración para la aplicación de servicio de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] .  
  
 Puede ver todas las programaciones compartidas definidas para el servidor de informes, pausarlas y reanudarlas (solo en el Administrador de informes) e incluso seleccionar las programaciones que desea modificar o eliminar. La página Programaciones compartidas resume la siguiente información sobre el estado de cada programación: frecuencia, propietario, fecha de expiración y estado.  
  
 Se puede saber si una programación compartida se usa activamente:  
  
-   Inspeccionando los valores de los campos de fecha de Última ejecución y Siguiente ejecución y el campo Estado de la página Programaciones compartidas. Cuando una programación ya no se ejecuta porque ha expirado, aparece su fecha de expiración en el campo Estado.  
  
-   Viendo la página Informes de una programación compartida específica. Esta página enumera todos los informes y los conjuntos de datos compartidos que utilizan la programación compartida.  
  
-   Viendo los archivos de registro de ejecución de informes o registros de seguimiento para determinar si se han ejecutado los informes las veces especificadas por la programación. Para más información, vea [Archivos de registro y orígenes de Reporting Services](../report-server/reporting-services-log-files-and-sources.md).  
  
##  <a name="bkmk_sharepoint"></a> Crear y administrar programaciones compartidas (modo de SharePoint)  
 Una programación compartida es una programación multipropósito que proporciona información de programación lista para utilizar a cualquier número de informes o suscripciones. Estas programaciones se crean una sola vez y se incluyen referencias a las mismas en una página de suscripción o propiedades siempre que se necesita información sobre la programación. Las programaciones compartidas pueden administrarse, pausarse y reanudarse de forma centralizada. Sin embargo, las programaciones personalizadas deben modificarse manualmente para evitar que se ejecute el informe o la suscripción.  
  
 Para poder crear, modificar o eliminar programaciones compartidas, debe ser administrador del sitio de SharePoint.  
  
 Puede identificar una programación específica mediante su nombre descriptivo. Si no se especifica un nombre, se crea un nombre predeterminado en función de las características de la programación, como su patrón de periodicidad o las fechas y horas de ejecución.  
  
> [!NOTE]  
>  Al crear programaciones compartidas, se requiere el servicio Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
### <a name="create-shared-schedules-sharepoint"></a>Crear programaciones compartidas (SharePoint)  
  
##### <a name="to-create-shared-schedules"></a>Para crear programaciones compartidas  
  
1.  Haga clic en **Acciones del sitio**.  
  
2.  Haga clic en **Configuración del sitio**.  
  
3.  En la sección Reporting Services, haga clic en **Administrar programaciones compartidas**.  
  
4.  Haga clic en **Agregar programación** para abrir la página Propiedades de la programación.  
  
5.  Escriba un nombre descriptivo para la programación. En las páginas de la aplicación usadas para trabajar con informes de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] , este nombre aparecerá en listas desplegables en las páginas de definición de la programación en todo el sitio. Evite los nombres largos y difíciles de leer. Siga una convención de nomenclatura que coloque la información más descriptiva al principio del nombre.  
  
6.  Elija una frecuencia. Dependiendo de la frecuencia que seleccione, las opciones de programación que aparecen en la página pueden cambiar para admitir esa frecuencia (por ejemplo, si selecciona **Mes**, el nombre de cada mes aparecerá en la página).  
  
7.  Defina la programación. Una sola programación no admite todas las combinaciones de programaciones.  
  
8.  Establezca una fecha de inicio y de fin.  
  
9. Haga clic en **Aceptar**.  
  
### <a name="delete-shared-schedules-sharepoint"></a>Eliminar programaciones compartidas (SharePoint)  
 Todas las programaciones, sean compartidas o específicas del informe, deben eliminarse manualmente. Si elimina una programación compartida que está utilizándose, todas las referencias a la misma se reemplazarán por programaciones personalizadas sin especificar (es decir, una programación personalizada que no incluye información de fecha u hora).  
  
 Es importante saber que no es lo mismo eliminar una programación que hacer que expire. Las fechas de expiración se utilizan para detener una programación, no para eliminarla. Dado que las programaciones se usan para automatizar operaciones del servidor de informes, nunca se eliminan automáticamente. Las programaciones expiradas constituyen una prueba para los administradores de los servidores de informes con relación a las causas que han detenido un proceso automático. Sin la existencia de la programación expirada, los administradores podrían errar en el diagnóstico del problema o perder demasiado tiempo en intentar solucionar un proceso que en realidad es completamente válido.  
  
 Las programaciones personalizadas que han expirado permanecen adjuntas al informe. Es posible determinar si una programación ha expirado con solo revisar la fecha final. Las programaciones compartidas expiradas se conservan en la lista Programaciones compartidas. El campo Estado indica si la programación ha expirado. Puede volver a aplicar la programación ampliando la fecha de finalización o eliminar la referencia a la programación si ya no la necesita.  
  
##### <a name="to-delete-a-shared-schedule"></a>Eliminar una programación compartida  
  
1.  Haga clic en **Acciones del sitio**.  
  
2.  Haga clic en **Configuración del sitio**.  
  
3.  En la sección Reporting Services, haga clic en **Administrar programaciones compartidas**.  
  
4.  Seleccione la programación y haga clic en **Eliminar**.  
  
##  <a name="bkmk_native"></a> Crear y administrar programaciones compartidas (modo nativo)  
 Las programaciones compartidas se deben eliminar manualmente mediante la página Programaciones del Administrador de informes o la carpeta Programaciones compartidas en [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]. Si se elimina una programación compartida que esté en uso, se sustituirán todas las referencias a la misma por programaciones específicas del informe.  
  
 Se eliminan las programaciones específicas de informes y suscripciones al eliminar el informe o la suscripción, o al elegir un enfoque diferente para ejecutar el informe o la suscripción. Por ejemplo, al elegir **Ejecutar este informe siempre con los datos más recientes** , se eliminará una programación específica de informes que creó para ejecutar un informe como una instantánea de ejecución de informes.  
  
 Es importante saber que no es lo mismo eliminar una programación que hacer que expire. Las fechas de expiración se utilizan para detener una programación, no para eliminarla. Dado que las programaciones se usan para automatizar diversas características, nunca se eliminan automáticamente. Las programaciones expiradas constituyen una prueba para los administradores de los servidores de informes con relación a las causas que han detenido un proceso automático. Sin la existencia de la programación expirada, los administradores podrían errar en el diagnóstico del problema o perder demasiado tiempo en intentar solucionar un proceso que en realidad es completamente válido.  
  
 Las programaciones específicas del informe que han expirado permanecen adjuntas al informe. Es posible determinar si una programación ha expirado con solo revisar la fecha final. Las programaciones compartidas expiradas se conservan en la lista Programaciones compartidas. El campo Estado indica si la programación ha expirado. Puede volver a aplicar la programación ampliando la fecha de finalización o eliminar la referencia a la programación si ya no la necesita.  
  
### <a name="create-delete-or-modify-a-shared-schedule-report-manager"></a>Crear, eliminar o modificar una programación compartida (Administrador de informes)  
 La creación y modificación de una programación consiste en establecer las opciones de frecuencia que determinan el momento en que debe ejecutarse la programación.  
  
-   Las programaciones compartidas se crean como elementos independientes. Una vez creadas, deben incluirse referencias a las mismas durante la definición de una suscripción o cualquier otra operación programada.  
  
-   Las programaciones específicas del informe se crean al definir una suscripción o establecer las propiedades de ejecución del informe. Completar la información de la programación forma parte del proceso de definición de una suscripción o de establecimiento de las propiedades. Para definir una programación específica del informe, abra el informe o la suscripción que la utiliza.  
  
 Una programación compartida contiene la información de programación y periodicidad que se puede usar en un número cualquiera de suscripciones e informes publicados que se ejecutan en un servidor de informes de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] . Si tiene muchos informes y suscripciones que se ejecutan al mismo tiempo, puede crear una programación compartida para dichos trabajos. Si desea cambiar el patrón de periodicidad o la fecha de finalización con posterioridad, puede realizar la modificación en un lugar.  
  
 Las programaciones compartidas son más sencillas de mantener y le permiten mayor flexibilidad para administrar operaciones programadas. Por ejemplo, puede pausar y reanudar las programaciones compartidas. Además, si desea que se ejecuten demasiadas operaciones programadas al mismo tiempo, puede crear varias programaciones compartidas que se ejecuten en momentos diferentes y, a continuación, ajustar la información de programación hasta que la carga de procesamiento se iguale fuera en el servidor de informes.  
  
 Las programaciones pueden crearse o modificarse en cualquier momento. Sin embargo, si se empieza a ejecutar una programación antes de haber completado las modificaciones, se usará la versión anterior de la misma. La programación revisada no surtirá efecto hasta que se guarde.  
  
 Si modifica una programación compartida, puede pausarla para realizar los cambios. Dichos cambios serán efectivos cuando se reanude la programación.  
  
##### <a name="to-create-or-modify-a-shared-schedule-report-manager"></a>Para crear o modificar una programación compartida (Administrador de informes)  
  
1.  Inicie el [Administrador de informes &#40;Modo nativo de SSRS&#41;](../report-manager-ssrs-native-mode.md).  
  
2.  En el Administrador de informes, haga clic en la opción **Configuración del sitio**de la barra de herramientas global.  
  
3.  Haga clic en **Programaciones**.  
  
4.  Haga clic en **Nueva programación**. Para modificar una programación existente, haga clic en el nombre de la programación.  
  
5.  Escriba un nombre descriptivo para la programación.  
  
6.  Haga clic en **Hora**, **Día**, **Semana**o **Mes**. Haga clic en **Una vez** para crear una programación que se ejecute solo una vez. Cuando se especifica la base de la programación, se muestran más opciones.  
  
7.  Opcionalmente, puede seleccionar la fecha en que comenzará la programación. El valor predeterminado es el día actual. Elija una fecha posterior si desea posponer el inicio de la programación.  
  
8.  Seleccione la fecha en que finalizará la programación (opcional). La programación se detiene en esa fecha pero no se elimina.  
  
9. [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
##### <a name="to-delete-a-shared-schedule-report-manager"></a>Para eliminar una programación compartida (Administrador de informes)  
  
1.  En el Administrador de informes, haga clic en la opción **Configuración del sitio**de la barra de herramientas global.  
  
    > [!NOTE]  
    >  Si **Configuración del sitio** no está disponible, significa que no tiene permiso de acceso a la configuración del sitio.  
  
2.  En la sección **Otros** de la página, haga clic en **Administrar programaciones compartidas**.  
  
3.  Active la casilla situada junto a la programación que desea eliminar y haga clic en **Eliminar**.  
  
 Si elimina una programación compartida usada por varios informes y suscripciones, el servidor de informes creará calendarios individuales para cada informe y suscripción que haya usado anteriormente la programación compartida. Cada nueva programación individual contendrá la fecha, la hora y el patrón de periodicidad que se especificó en la programación compartida. Tenga en cuenta que [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] no proporciona la administración central de las programaciones individuales. Si elimina una programación compartida, tendrá que mantener la información de programación para cada elemento individual.  
  
 Si no está seguro de que se use una programación compartida, considere su eliminación [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] en su lugar. [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] proporciona las mismas características de administración de programación compartida que el Administrador de informes, además de una página adicional Informes que muestra el nombre de cada informe que la programación usa.  
  
### <a name="create-delete-or-modify-a-shared-schedule-management-studio"></a>Crear, eliminar o modificar una programación compartida (Management Studio)  
 Una programación compartida contiene la información de programación y periodicidad que se puede usar en un número cualquiera de suscripciones e informes publicados que se ejecutan en un servidor de informes de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] . Si tiene muchos informes y suscripciones que se ejecutan al mismo tiempo, puede crear una programación compartida para dichos trabajos. Si desea cambiar el patrón de periodicidad o la fecha de finalización con posterioridad, puede realizar la modificación en un lugar.  
  
 Las programaciones compartidas son más sencillas de mantener y le permiten mayor flexibilidad para administrar operaciones programadas. Por ejemplo, puede pausar y reanudar las programaciones compartidas. Además, si desea que se ejecuten demasiadas operaciones programadas al mismo tiempo, puede crear varias programaciones compartidas que se ejecuten en momentos diferentes y, a continuación, ajustar la información de programación hasta que la carga de procesamiento se iguale fuera en el servidor de informes.  
  
##### <a name="to-create-or-modify-a-shared-schedule-management-studio"></a>Para crear o modificar una programación compartida (Management Studio)  
  
1.  Inicie SQL Server Management Studio y conéctese a una instancia del servidor de informes.  
  
2.  En el Explorador de objetos, expanda un nodo de servidor de informes.  
  
3.  Haga clic con el botón secundario en la carpeta Programaciones compartidas y, a continuación, haga clic en **Nueva programación**. De este modo se muestra la página General del cuadro de diálogo **Nueva programación compartida** .  
  
     Para modificar una programación compartida existente, expanda la carpeta Programaciones compartidas, haga clic con el botón derecho en la programación que quiere modificar y, luego, haga clic en **Propiedades**.  
  
4.  Escriba un nombre descriptivo para la programación.  
  
5.  Opcionalmente, puede seleccionar la fecha en que comenzará la programación. El valor predeterminado es el día actual.  
  
6.  Opcionalmente, puede seleccionar la fecha en que finalizará la programación. La programación se detiene en esa fecha pero no se elimina.  
  
7.  Para configurar una programación de repetición, seleccione **Hora**, **Día**, **Semana**o **Mes**. De este modo se muestran más opciones. Utilice estas otras opciones para configurar la frecuencia de la programación, en función de su hora, día, semana o mes preferidos.  
  
     También puede especificar una programación para una vez (no periódica) seleccionando **Una vez**y, luego, especificando una **Hora de inicio**.  
  
8.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
##### <a name="to-delete-a-shared-schedule-management-studio"></a>Para eliminar una programación compartida (Management Studio)  
  
1.  En el Explorador de objetos, expanda un nodo de servidor de informes.  
  
2.  Expanda la carpeta Programaciones compartidas, haga clic con el botón secundario en la programación que desea eliminar y, a continuación, haga clic en **Eliminar**. Aparece el cuadro de diálogo **Eliminar elementos del catálogo** .  
  
3.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
 Si elimina una programación compartida usada por varios informes y suscripciones, el servidor de informes creará calendarios individuales para cada informe y suscripción que haya usado anteriormente la programación compartida. Cada nueva programación individual contendrá la fecha, la hora y el patrón de periodicidad que se especificó en la programación compartida. Tenga en cuenta que [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] no proporciona la administración central de las programaciones individuales. Si elimina una programación compartida, tendrá que mantener la información de programación para cada elemento individual. Antes de eliminar una programación compartida, use la [página Informes](../tools/schedule-properties-reports-page.md) para determinar qué informes usan actualmente la programación compartida.  
  
## <a name="see-also"></a>Vea también  
 [Programaciones](schedules.md)   
 [Pausar y reanudar las programaciones compartidas](pause-and-resume-shared-schedules.md)   
 [Almacenar en caché un informe &#40;Administrador de informes&#41;](../report-server/cache-a-report-report-manager.md)   
 [Agregar una instantánea al historial de informes &#40;Administrador de informes&#41;](../report-server/add-a-snapshot-to-report-history-report-manager.md)  
  
  