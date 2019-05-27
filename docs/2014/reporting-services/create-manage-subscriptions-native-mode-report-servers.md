---
title: Crear y administrar suscripciones para servidores de informes en modo nativo | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- subscriptions [Reporting Services], managing
ms.assetid: 7f46cbdb-5102-4941-bca2-5e0ff9012c6b
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: d6f18ff05cf6283e4358e8f8afd76a5858b0b41a
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/23/2019
ms.locfileid: "66109597"
---
# <a name="create-and-manage-subscriptions-for-native-mode-report-servers"></a>Crear y administrar suscripciones para servidores de informes en modo nativo
  Esta sección contiene temas sobre el procesamiento, la supervisión y el control de las suscripciones. La administración de suscripciones se realiza de forma distinta para las suscripciones estándar y las controladas por datos. Las suscripciones estándar suelen ser propiedad de un usuario que las administra. Por el contrario, las suscripciones controladas por datos suelen ser creadas y mantenidas por el administrador de un servidor de informes.  
  
 Las características de suscripciones y entrega están habilitadas de manera predeterminada (para poder usar la entrega por correo electrónico hay que configurarla previamente). Las extensiones de entrega predeterminadas incluyen la entrega por correo electrónico y la entrega a recursos compartidos de archivos del servidor de informes. A no ser que cree o instale extensiones de entrega personalizadas, éstos son los únicos métodos de distribución disponibles para las suscripciones en un servidor de informes configurado para el modo nativo.  
  
## <a name="permissions-for-subscribing-to-reports-on-a-native-mode-report-server"></a>Permisos para suscribirse a informes en un servidor de informes configurado para el modo nativo  
 Dependiendo de cómo use los roles, puede proporcionar la funcionalidad de suscripción a grupos de usuarios seleccionados si habilita o deshabilita las tareas de suscripción para diferentes roles. Las características de suscripción están disponibles para los usuarios a través de dos tareas:  
  
-   La tarea "Administrar suscripciones individuales" permite a los usuarios crear, modificar y eliminar suscripciones correspondientes a un informe determinado. En los roles predefinidos, esta tarea forma parte de los roles Explorador y Generador de informes. Las asignaciones de roles que incluyen esta tarea permiten al usuario administrar únicamente las suscripciones que crea.  
  
-   La tarea "Administrar todas las suscripciones" permite a los usuarios tener acceso a todas las suscripciones y modificarlas. Esta tarea es necesaria para crear suscripciones controladas por datos. En los roles predefinidos, solo el rol Administrador de contenido incluye esta tarea.  
  
## <a name="disabling-subscriptions"></a>Deshabilitar suscripciones  
 Para evitar que los usuarios puedan crear suscripciones, desactive la tarea "Administrar suscripciones individuales" del rol. Si quita esta tarea, las páginas de Suscripción no estarán disponibles. En el Administrador de informes, la página Mis suscripciones aparece vacía (no se puede eliminar), incluso aunque antes contuviese suscripciones. Al quitar tareas relacionadas con una suscripción, se evita que los usuarios creen y modifiquen las suscripciones, pero no se eliminan las suscripciones propiamente dichas. Las suscripciones existentes continuarán ejecutándose hasta que se eliminen. Para obtener más información acerca de cómo eliminar las suscripciones, vea [crear, modificar y eliminar suscripciones estándar &#40;Reporting Services en modo nativo&#41;](subscriptions/create-and-manage-subscriptions-for-native-mode-report-servers.md).  
  
 Para deshabilitar el procesamiento de suscripciones en un servidor de informes, puede establecer el `ScheduleEventsAndReportDeliveryEnabled` propiedad `False` en el **configuración de área expuesta para Reporting Services** faceta de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] administración basada en directivas. Ello impedirá que se ejecuten todas las operaciones programadas. No puede desactivar únicamente el procesamiento de suscripciones en el servidor de informes.  
  
 Para obtener instrucciones sobre cómo cancelar la suscripción que se está procesando en el servidor de informes, vea [administrar un proceso en ejecución](subscriptions/manage-a-running-process.md).  
  
## <a name="disabling-delivery-extensions"></a>Deshabilitar extensiones de entrega  
 Todas las extensiones de entrega instaladas en un servidor de informes están disponibles para cualquier usuario que tenga permiso para crear una suscripción para un informe determinado. Las extensiones de entrega siguientes están disponibles y se configuran automáticamente:  
  
-   Recurso compartido de archivos de Windows  
  
-   Biblioteca de SharePoint (solo disponible desde un sitio de SharePoint integrado con un servidor de informes en el modo integrado de SharePoint)  
  
 Para poder usar la entrega por correo electrónico, debe configurarse previamente. Si no se configura, no estará disponible. Para obtener más información, consulte [configurar un servidor de informes para la entrega de correo electrónico &#40;SSRS Configuration Manager&#41;](../../2014/sql-server/install/configure-a-report-server-for-e-mail-delivery-ssrs-configuration-manager.md).  
  
 Si desea desactivar extensiones concretas, puede quitar las entradas de extensión del archivo RSReportServer.config. Para obtener más información, consulte [RSReportServer Configuration File](report-server/rsreportserver-config-configuration-file.md) y [configurar un servidor de informes para la entrega de correo electrónico &#40;SSRS Configuration Manager&#41;](../../2014/sql-server/install/configure-a-report-server-for-e-mail-delivery-ssrs-configuration-manager.md).  
  
 Una vez que quite una extensión de entrega, ya no estará disponible en el Administrador de informes o un sitio de SharePoint. Si quita una extensión de entrega, es posible que algunas suscripciones queden inactivas. Asegúrese de eliminar las suscripciones o configurarlas para usar una extensión de entrega diferente antes de quitar una extensión.  
  
## <a name="in-this-section"></a>En esta sección  
 [Usar Mis suscripciones](subscriptions/use-my-subscriptions-native-mode-report-server.md)  
 Explica cómo utilizar la página Mis suscripciones para administrar sus suscripciones.  
  
 [Pausar el procesamiento de informes y suscripciones](subscriptions/disable-or-pause-report-and-subscription-processing.md)  
 Describe las diversas maneras de pausar el procesamiento de informes; por ejemplo, usando asignaciones de roles o deshabilitando recursos del servidor de informes.  
  
 [Controlar la distribución de informes](../../2014/reporting-services/control-report-distribution.md)  
 Describe los parámetros de configuración y las opciones de entrega que puede utilizar para controlar la distribución de informes.  
  
 [Supervisión de suscripciones de Reporting Services](subscriptions/monitor-reporting-services-subscriptions.md)  
 Describe cómo puede determinar si una suscripción se ha entregado o no, así como los efectos de los cambios en informes sobre las suscripciones existentes.  
  
## <a name="see-also"></a>Vea también  
 [Crear, modificar y eliminar suscripciones estándares &#40;Reporting Services en modo nativo&#41;](subscriptions/create-and-manage-subscriptions-for-native-mode-report-servers.md)  
  
  
