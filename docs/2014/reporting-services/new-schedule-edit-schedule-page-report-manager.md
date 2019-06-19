---
title: 'Nueva programación: Editar programación página (Administrador de informes) | Microsoft Docs'
ms.custom: ''
ms.date: 05/24/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
ms.assetid: 52a4d250-e185-4116-a29c-d809940a00fb
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: ea1eed70c3eac8bac1c4141628e72ce0af8099c2
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "66108149"
---
# <a name="new-schedule-edit-schedule-page-report-manager"></a>Nueva programación: Editar página de programación (Administrador de informes)
  Utilice la página Nueva programación/Editar programación para crear una programación para un informe. Las programaciones se usan con las suscripciones para actualizar los informes almacenados en caché y para crear instantáneas como elementos independientes o en un historial de informes.  
  
> [!NOTE]  
>  Esta característica no está disponible en todas las ediciones de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]. Para obtener una lista de las características admitidas por las ediciones de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)], vea [Features Supported by the Editions of SQL Server 2014](../../2014/getting-started/features-supported-by-the-editions-of-sql-server-2014.md).  
  
 Solo se pueden crear programaciones para los informes que se puedan ejecutar en modo desatendido. Para ejecutar un informe en modo desatendido, es necesario almacenar las credenciales del origen de datos de informe en la base de datos del servidor de informes. Para obtener más información, consulte [página de propiedades de orígenes de datos &#40;el Administrador de informes&#41;](../../2014/reporting-services/data-sources-properties-page-report-manager.md).  
  
 Una sola programación no admite todas las combinaciones de frecuencias. Por ejemplo, si desea ejecutar un informe todos los viernes a las 12:00 p. m. y a las 4:00 p. m. debe crear dos programaciones diarias que especifiquen una fecha de ejecución en viernes, una con las 12:00 p. m. como hora de inicio y otra con las 4:00 p. m. como hora de inicio.  
  
 El procesamiento de programaciones se basa en la hora local del servidor de informes que hospeda y procesa la programación.  
  
## <a name="navigation"></a>Navegación  
 Utilice los procedimientos siguientes para navegar hasta esta ubicación en la interfaz de usuario (IU).  
  
### <a name="to-open-the-new-schedule-or-edit-schedule-page-from-the-execution-properties-page-of-a-report"></a>Para abrir las páginas Nueva programación o Editar programación desde la página Propiedades de ejecución de un informe  
  
1.  Abra el Administrador de informes y busque el informe donde desea configurar una programación.  
  
2.  Mantenga el mouse sobre el informe y haga clic en la flecha de lista desplegable.  
  
3.  En el menú desplegable, haga clic en **Administrar**. Se abrirá la página Propiedades generales correspondiente al modelo.  
  
4.  Seleccione la pestaña **Ejecución** .  
  
5.  Seleccione la opción **Representar este informe a partir de una instantánea de ejecución de informes**. A continuación, seleccione **Utilizar la siguiente programación para agregar instantáneas al historial de informe**y seleccione **Programación específica del informe**. A continuación, haga clic en **Configurar**.  
  
### <a name="to-open-the-new-schedule-or-edit-schedule-page-from-the-history-properties-page-of-a-report"></a>Para abrir las páginas Nueva programación o Editar programación desde la página de propiedades Historial de un informe  
  
1.  Abra el Administrador de informes y busque el informe donde desea configurar una programación.  
  
2.  Mantenga el mouse sobre el informe y haga clic en la flecha de lista desplegable.  
  
3.  En el menú desplegable, haga clic en **Administrar**. Se abrirá la página Propiedades generales correspondiente al modelo.  
  
4.  Seleccione la pestaña **Historial** .  
  
5.  Seleccione **Utilizar la siguiente programación para agregar instantáneas al historial de informe**y seleccione **Programación específica del informe**. A continuación, haga clic en **Configurar**.  
  
### <a name="to-open-the-new-schedule-or-edit-schedule-page-from-the-subscriptions-page"></a>Para abrir las páginas Nueva programación o Editar programación en la página Suscripciones  
  
1.  Abra el Administrador de informes y busque el informe donde desea configurar una programación.  
  
2.  Mantenga el mouse sobre el informe y haga clic en la flecha de lista desplegable.  
  
3.  En el menú desplegable,  
  
    -   Haga clic en **Administrar**. Se abrirá la página de propiedades General correspondiente al informe. A continuación, seleccione la pestaña **Suscripciones** .  
  
    -   Haga clic en **Suscribir**. Se abrirá la página de propiedades **Suscripciones** correspondiente al informe.  
  
4.  En la barra de herramientas, haga clic en **Nueva suscripción** o seleccione una suscripción existente para modificarla.  
  
5.  En **Opciones de procesamiento de suscripciones**, haga clic en **Nueva programación**.  
  
## <a name="options"></a>Opciones  
 **Detalles de programación**  
 Seleccione las opciones que determinen cuándo se ejecuta un informe y con qué frecuencia. Las opciones de frecuencia están organizadas por niveles. El primer conjunto de opciones especifica una categoría de frecuencia (horaria, diaria, semanal, etc.). El segundo conjunto de opciones que aparece se basa en la selección inicial.  
  
-   **Hora** define una programación que se ejecuta a intervalos de horas. Use la sección **Fechas de inicio y fin** para especificar el día en el que se va a ejecutar la programación.  
  
-   **Día** define una programación que se ejecuta en los días seleccionados a una hora específica. Puede especificar los días de las maneras siguientes: Cada \< *día*>, todos los días laborables y cada \< *número*> días. Al elegir un método se anulan los demás, aunque los demás días aparezcan seleccionados.  
  
-   **Semana** define una programación que se ejecuta en intervalos semanales a una hora específica. El intervalo puede ser una semana completa (por ejemplo, cada dos semanas) o días de una semana.  
  
-   **Mes** define una programación que se ejecuta mensualmente. En un mes, se puede elegir un día basándose en un modelo (por ejemplo, el último domingo de cada mes) o fechas específicas del calendario (como 1 y 15 para indicar los días uno y quince de cada mes). Puede utilizar comas y guiones para especificar varios días e intervalos; por ejemplo, 1, 5, 7-12, 21.  
  
-   **Una vez** define una programación que se ejecuta una sola vez. Use la sección **Fechas de inicio y fin** para especificar el día en el que se va a ejecutar la programación. Esta programación deja de tener validez en cuanto se procesa.  
  
 **Fechas de inicio y finalización**  
 Especifique una fecha de inicio que determine cuándo entra en vigor la programación y una fecha de finalización que determine cuándo expira.  
  
 Cuando las programaciones dejan de tener validez, no se notifica. Después de la fecha de finalización, ya no vuelven a ejecutarse. Las programaciones expiradas no se eliminan. Las programaciones solo se pueden eliminar manualmente. De esta manera, si decide seguir utilizándola, puede ampliar la fecha de finalización.  
  
## <a name="see-also"></a>Vea también  
 [Administrador de informes &#40;Modo nativo de SSRS&#41;](../../2014/reporting-services/report-manager-ssrs-native-mode.md)   
 [Crear, modificar y eliminar programaciones](subscriptions/create-modify-and-delete-schedules.md)   
 [Administrador de informes (Ayuda F1)](../../2014/reporting-services/report-manager-f1-help.md)  
  
  
