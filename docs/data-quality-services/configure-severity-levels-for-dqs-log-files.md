---
title: Configurar los niveles de gravedad de los archivos de registro de DQS
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: data-quality-services
ms.reviewer: ''
ms.technology: data-quality-services
ms.topic: conceptual
f1_keywords:
- sql13.dqs.admin.config.log.f1
helpviewer_keywords:
- severity levels
- log files,severity levels
- dqs log files,severity levels
- logging,severity levels
- configure severity levels
ms.assetid: 66ffcdec-4bf7-4dd5-a221-fd9baefeeef4
author: swinarko
ms.author: sawinark
ms.openlocfilehash: 4215cda5bfc82f0c6d195f336a1099309ab18154
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/27/2020
ms.locfileid: "75255643"
---
# <a name="configure-severity-levels-for-dqs-log-files"></a>Configurar los niveles de gravedad de los archivos de registro de DQS

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

  En este tema se describe cómo configurar los niveles de gravedad de las distintas actividades y módulos de [!INCLUDE[ssDQSnoversion](../includes/ssdqsnoversion-md.md)] (DQS) mediante [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)]. Los niveles de gravedad definen la intensidad de los eventos que tienen lugar en DQS. Los eventos de DQS tienen los niveles de gravedad siguientes, en orden decreciente:  
  
-   **Fatal**: errores críticos en tiempo de ejecución que pueden producir resultados graves e inesperados.  
  
-   **Error**: otros errores en tiempo de ejecución.  
  
-   **Warn**: advertencia sobre eventos que pueden provocar un error.  
  
-   **Info**: información sobre eventos en general; no se trata ni de un error ni de una advertencia. Por ejemplo, se ha iniciado un proceso de DQS.  
  
-   **Debug**: información detallada sobre el evento.  
  
 Cuando se configuran niveles de gravedad para las actividades y módulos de DQS, lo que se hace en realidad es filtrar la información que quedará registrada en el archivo de registro de DQS para la actividad o el módulo de DQS correspondiente. Por ejemplo, si establece el nivel de gravedad de una actividad de DQS en **Warn**, solo se registrarán los mensajes de advertencia y los de los niveles de gravedad superiores (Error y Fatal) que estén asociados a la actividad de DQS.  
  
##  <a name="before-you-begin"></a><a name="BeforeYouBegin"></a> Antes de comenzar  
  
###  <a name="security"></a><a name="Security"></a> Seguridad  
  
####  <a name="permissions"></a><a name="Permissions"></a> Permisos  
 Para configurar niveles de gravedad, debe disponer del rol dqs_administrator en la base de datos DQS_MAIN.  
  
##  <a name="configure-severity-levels-at-activity-level"></a><a name="ConfigureActivity"></a>Configurar niveles de gravedad en el nivel de actividad  
 Puede configurar los niveles de gravedad del registro para las siguientes actividades de DQS: administración de dominios, detección de conocimiento, directiva de coincidencia, limpieza de datos, coincidencia de datos y servicios de datos de referencia. Para ello:  
  
1.  [!INCLUDE[ssDQSInitialStep](../includes/ssdqsinitialstep-md.md)][Ejecute la aplicación Data Quality Client](../data-quality-services/run-the-data-quality-client-application.md).  
  
2.  En la página de inicio de [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)] , haga clic en **Configuración**.  
  
3.  A continuación, haga clic en la pestaña **configuración del registro** . Se muestran las siguientes actividades de DQS para las que puede seleccionar un nivel de gravedad: **Administración de dominios**, **detección de conocimiento**, proyecto de **limpieza (p. ej., RDS)**, **Directiva de coincidencia y proyecto de búsqueda de coincidencias**, y **RDS**.  
  
4.  Para una actividad de DQS, seleccione el nivel de gravedad que desea registrar. Puede seleccionar uno de los siguientes: **Fatal**, **Error**, **Warn**, **Info**y **Debug**. Por ejemplo, si desea que en los archivos de registro de DQS solo aparezcan mensajes de tipo Fatal para la actividad de detección de conocimiento, seleccione **Fatal** en la lista desplegable de la actividad **KnowledgeDiscovery** .  
  
    > [!NOTE]  
    >  De forma predeterminada, todas las actividades tienen seleccionado el nivel de gravedad **Error** . Esto significa que, de forma predeterminada, en los archivos de registro de DQS se escribirán los mensajes de tipo Error y Fatal para todas las actividades.  
  
5.  Haga clic en **Cerrar**.  
  
##  <a name="configure-severity-levels-at-module-level-advanced"></a><a name="ConfigureModule"></a>Configurar niveles de gravedad en el nivel de módulo (avanzado)  
 La sección **Avanzadas** de la pestaña **Configuración del registro** permite configurar los niveles de gravedad del registro en el nivel de módulo. Los módulos son ensamblados del sistema de DQS que implementan funcionalidades en una característica de DQS. Por ejemplo, la actividad de administración de dominios contiene funcionalidades tales como la definición de reglas de dominio, la definición de condiciones de regla, la definición de reglas entre dominios para dominios compuestos, etc.  
  
 En ocasiones, el nivel de granularidad en el nivel de actividad no es suficiente. Es posible que desee investigar un problema que aparece en un determinado módulo de una actividad. Resulta de ayuda disponer de una opción que permita configurar los niveles de gravedad del registro en el nivel de módulo para poder aislar el problema y seguir su evolución con mayor precisión.  
  
 La configuración de los niveles de gravedad del registro en el nivel de actividad determina la configuración de los niveles de gravedad del registro de todos los módulos que constituyen la actividad. Sin embargo, si existe un conflicto entre la configuración de los niveles de gravedad del registro en el nivel de actividad y en el nivel de módulo, prevalecen los niveles de gravedad del registro en el nivel de módulo.  
  
> [!NOTE]
>  -   De forma predeterminada, el módulo **Microsoft.Ssdqs.Core.Startup** se preconfigura en la sección **Avanzadas** con un nivel de gravedad **Info**. Esto tiene como finalidad habilitar el registro de los eventos con un nivel de gravedad Info o superior (Warn, Error y Fatal) que están relacionados con el inicio y finalización de los servicios de DQS.  
> -   Debe configurar los niveles de gravedad del registro en el nivel de módulo solo si es un usuario avanzado de DQS que está familiarizado con los ensamblados del sistema de DQS.  
  
 Para configurar los niveles de gravedad del registro en el nivel de módulo:  
  
1.  En la pestaña **Configuración del registro** , haga clic en la flecha abajo de **Avanzadas** para mostrar el área.  
  
2.  En la cuadrícula que aparece, seleccione el nombre de un módulo en la lista desplegable de la columna **Módulo** .  
  
3.  A continuación, seleccione un nivel de gravedad para el módulo en la lista desplegable de la columna **Gravedad** . Puede seleccionar uno de los siguientes: **Fatal**, **Error**, **Warn**, **Info**y **Debug**.  
  
     Por ejemplo, en la actividad de administración de dominios, puede establecer un nivel de granularidad para la funcionalidad de definición de reglas de dominio distinto del de la actividad de administración de dominios; para ello, solo tiene que seleccionar el módulo **Microsoft.Ssdqs.DomainRules.Define** y elegir otro nivel de gravedad del registro. Del mismo modo, puede establecer otro nivel de granularidad para la funcionalidad de reglas entre dominios: seleccione el módulo **Microsoft.Ssdqs.DomainRules.Condition.CrossDomain** y elija otro nivel de gravedad del registro.  
  
4.  Repita los pasos 2 y 3 para otros módulos, si procede. También puede agregar o eliminar filas de la cuadrícula haciendo clic en los iconos **Agregar módulo** y **Quitar módulo** .  
  
5.  Haga clic en **Cerrar**.  
  
## <a name="see-also"></a>Consulte también  
 [Configurar las opciones avanzadas de los archivos de registro de DQS](../data-quality-services/configure-advanced-settings-for-dqs-log-files.md)  
  
  
