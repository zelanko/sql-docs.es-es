---
title: Crear una sesión de eventos extendidos utilizando el Asistente (Explorador de objetos) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
f1_keywords:
- Sql12.ssms.XeWizard.Summary.f1
- Sql12.ssms.XeWizard.SetSessionProperties.f1
- Sql12.ssms.XeWizard.CaptureAddFields.f1
- Sql12.ssms.XeWizard.SelectEvents.f1
- Sql12.ssms.XeWizard.SpecifySessionTargets.f1
- Sql12.ssms.XeWizard.Welcome.f1
- sql12.ssms.XeWizard.Welcome.f1
- Sql12.ssms.XeWizard.ChooseTemplate.f1
- Sql12.ssms.XeWizard.SetSessionEventFilters.f1
- Sql12.ssms.XeWizard.Results.f1
helpviewer_keywords:
- Sql11.ssms.XeWizard.CaptureAddFields.f1
- Sql11.ssms.XeWizard.SetSessionEventFilters.f1
- Sql11.ssms.XeWizard.SpecifySessionTargets.f1
- Sql11.ssms.XeWizard.Results.f1
- Sql11.ssms.XeWizard.ChooseTemplate.f1
- Sql11.ssms.XeWizard.SetSessionProperties.f1
- Sql11.ssms.XeWizard.Welcome.f1
- Sql11.ssms.XeWizard.Summary.f1
- Sql11.ssms.XeWizard.SelectEvents.f1
ms.assetid: 80c0456f-17c0-41d8-b2aa-502a2f3bb6de
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: cdc50e81bcc58722a3c04fc8516b9158072533cf
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/23/2019
ms.locfileid: "66065058"
---
# <a name="create-an-extended-events-session-using-the-wizard-object-explorer"></a>Crear una sesión de Extended Events utilizando el asistente (Explorador de objetos)
  Para ayudarle a seleccionar y capturar eventos en el servidor, los eventos extendidos incluyen un Asistente para nueva sesión que le guía a través de los pasos necesarios para crear una sesión de eventos extendidos. El Asistente para nueva sesión expone la mayor parte de la funcionalidad de Extended Events. El [cuadro de diálogo Nueva sesión](../../2014/database-engine/create-an-extended-events-session-using-the-new-session-dialog.md) también permite definir una sesión de Eventos extendidos que capture, presente y analice los datos. El cuadro de diálogo Nueva sesión expone toda la funcionalidad de Extended Events.  
  
### <a name="to-open-the-new-session-wizard"></a>Para abrir el Asistente para nueva sesión  
  
1.  En el Explorador de objetos, expanda el nodo **Administración** y, a continuación, expanda **Eventos extendidos**.  
  
2.  Haga clic con el botón derecho en **Sesiones** y, después, haga clic en **Asistente para nueva sesión**.  
  
### <a name="use-the-following-new-session-wizard-pages-to-create-an-event-session"></a>Utilizar las páginas siguientes del Asistente para nueva sesión para crear una sesión de eventos  
  
-   [Introducción](#BKMK_Welcome)  
  
-   [Establecer propiedades de sesión](#BKMK_SetSessionProperties)  
  
-   [Elegir plantilla](#BKMK_ChooseTemplate)  
  
-   [Seleccionar eventos para capturar](#BKMK_SelectEventsToCapture)  
  
-   [Capturar campos globales](#BKMK_CaptureGlobalFields)  
  
-   [Establecer filtros de eventos de sesión](#BKMK_SetSessionEventFilters)  
  
-   [Especificar almacenamiento de datos de sesión](#BKMK_SpecifySessionDataOutput)  
  
-   [Resumen](#BKMK_Summary)  
  
-   [Crear sesión de eventos](#BKMK_CreateEventSession)  
  
##  <a name="BKMK_Welcome"></a> Introducción  
 En la página **Introducción** realice lo siguiente:  
  
-   En la página **Introducción** del Asistente para nueva sesión, haga clic en **Siguiente**.  
  
     Active la casilla **No volver a mostrar esta página** si va a usar el asistente más de una vez y no quiere leer la introducción cada vez que se inicie el asistente.  
  
##  <a name="BKMK_SetSessionProperties"></a> Establecer propiedades de sesión  
 En la página **Establecer propiedades de la sesión** realice lo siguiente:  
  
-   En el cuadro **Nombre de sesión** , escriba un nombre descriptivo para la sesión de eventos.  
  
     Si desea que la sesión se inicie al iniciarse el servidor, active la casilla **Iniciar la sesión de eventos al iniciar el servidor** y, a continuación, haga clic en **Siguiente**.  
  
##  <a name="BKMK_ChooseTemplate"></a> Elegir plantilla  
 En la página **Elegir plantilla** realice los pasos siguientes:  
  
-   Seleccione la opción **Usar esta plantilla de sesión de eventos** para seleccionar entre un conjunto de plantillas preconfiguradas diseñadas para solucionar problemas comunes. Seleccione la plantilla que quiera usar en la lista desplegable y, después, haga clic en **Siguiente**.  
  
     -O bien-  
  
-   Seleccione la opción **No usar una plantilla** si no quiere usar una plantilla preconfigurada y, después, haga clic en **Siguiente**.  
  
##  <a name="BKMK_SelectEventsToCapture"></a> Seleccionar eventos para capturar  
 En la página **Seleccionar eventos para capturar** realice lo siguiente:  
  
1.  Seleccione los eventos que desee capturar de la **Biblioteca de eventos**y, a continuación, haga clic en la flecha derecha. Puede seleccionar varios eventos en la biblioteca de eventos con Mayúsculas+Clic o Ctrl+Clic.  
  
     Puede seleccionar cómo desea que se busquen los eventos que desea capturar del cuadro de lista desplegable. Por ejemplo, puede buscar nombres de evento o nombres de evento con sus descripciones. Puede buscar cualquier palabra en la tabla especificando el texto que desea buscar en el cuadro **Biblioteca de eventos** . Por ejemplo, si quiere buscar el evento **lock_acquired** , puede especificar **lock**o **lock acquire**.  
  
     Los eventos que seleccione aparecerán en el cuadro **Eventos seleccionados** . Para quitar eventos del cuadro **Eventos seleccionados** , haga clic en la flecha izquierda.  
  
2.  Después de seleccionar los eventos que desee capturar, haga clic en **Siguiente**.  
  
    > [!NOTE]  
    >  Los eventos del canal **Depurar** permanecen ocultos de forma predeterminada. Para mostrar eventos de depuración, seleccione **Depurar** en la lista desplegable **Canal** .  
  
##  <a name="BKMK_CaptureGlobalFields"></a> Capturar campos globales  
 Los campos globales (también denominados acciones) se utilizan para asociar una o varias acciones para los eventos seleccionados. Si se selecciona una plantilla en la página **Elegir plantilla** , todos los campos que están definidas en la plantilla se muestran en esta página.  
  
 En la página **Capturar campos globales** realice lo siguiente:  
  
-   Seleccione los campos que desee capturar para la sesión de eventos y, a continuación, haga clic en **Siguiente**.  
  
     Puede quitar o agregar campos globales activando o desactivando la casilla situada junto al campo global.  
  
    > [!NOTE]  
    >  Las acciones seleccionadas se ordenan por **Nombre** permitiéndole ver las acciones asociadas en orden alfabético. Puede ordenar por descripción o por estado habilitado/deshabilitado haciendo clic en el encabezado de columna situado junto al nombre de campo.  
  
##  <a name="BKMK_SetSessionEventFilters"></a> Establecer filtros de eventos de sesión  
 Puede aplicar filtros (también denominados predicados) para limitar los eventos que desee capturar. En la página **Establecer filtros de eventos de la sesión** realice lo siguiente:  
  
1.  Si no usa una plantilla preconfigurada, cree los criterios de filtro y, después, haga clic en **Siguiente**.  
  
     Si usa una plantilla preconfigurada, en la sección **Filtros de plantilla (de solo lectura)** , el Asistente para nueva sesión enumera los filtros ya creados de la plantilla.  
  
2.  En la sección **Filtros adicionales** puede configurar filtros adicionales para la sesión de eventos.  
  
     Los filtros que configure se aplican a todos los eventos seleccionados. El Asistente para nueva sesión no admite la configuración de filtros para cada evento.  
  
    > [!NOTE]  
    >  Cuando configure una cláusula de grupo para el filtro, se quitarán los paréntesis redundantes del filtro después de guardar el resultado. Por ejemplo, si crea un filtro que agrupe **Cláusula 1** y **Cláusula 2**, aparecerán paréntesis alrededor de las cláusulas. Después de guardar el filtro, se quitan los paréntesis redundantes. La eliminación de los paréntesis no afecta a la lógica del filtro.  
  
##  <a name="BKMK_SpecifySessionDataOutput"></a> Especificar almacenamiento de datos de sesión  
 Utilice la página **Especificar almacenamiento de datos de la sesión** para especificar cómo desea recopilar los datos para el análisis. SQL Server Extended Events utiliza destinos para la salida de datos. Los destinos almacenan los datos de evento y pueden realizar acciones como escribir en un archivo y agregar datos de evento. Decida cómo desea recopilar los datos para el análisis y, en la página **Especificar almacenamiento de datos de la sesión** , realice lo siguiente:  
  
1.  Para los conjuntos de datos grandes y para la creación de registros históricos, active la casilla **Guardar los datos en un archivo para su posterior análisis** y, a continuación, realice lo siguiente:  
  
    1.  En el cuadro **Nombre de archivo en el servidor** , escriba la ruta de acceso y el nombre de archivo o haga clic en **Examinar** para especificar el directorio de archivos del servidor donde desea guardar los datos.  
  
    2.  En el cuadro **Tamaño máximo del archivo** , especifique el tamaño máximo de archivo que se ha de utilizar para el destino de archivos. Si no especifica el tamaño máximo de archivo, el archivo crecerá hasta llenar el disco. El tamaño de archivo predeterminado es 1 gigabyte (GB).  
  
    3.  Active la casilla **Habilitar sustitución incremental de archivos** para habilitar la sustitución incremental de archivos para el destino de archivos.  
  
    4.  En el cuadro **Número máximo de archivos** , especifique el número máximo de archivos que desea conservar en el sistema de archivos.  
  
2.  Para recopilar datos recientes, active la casilla **Trabajar solo con los datos más recientes (destino ring_buffer)** y, después, realice lo siguiente:  
  
    1.  En el cuadro **Número de eventos para mantener** , escriba o seleccione el número de eventos que desea mantener utilizando las flechas arriba y abajo.  
  
    2.  En el cuadro **Tamaño máximo del búfer de memoria** , especifique la cantidad máxima de memoria de búfer que desea usar. Los eventos existentes se quitan al alcanzar este valor.  
  
    3.  Si quiere conservar un número específico de eventos de cada tipo en el búfer, active la casilla **Mantener un número especificado de eventos (por tipo) cuando el búfer esté lleno** .  
  
    4.  En el cuadro **Número de eventos para mantener (por tipo)** , escriba o seleccione el número de eventos (por tipo) que quiere mantener al usar las flechas arriba y abajo.  
  
##  <a name="BKMK_Summary"></a> Resumen  
 En la página **Resumen** realice lo siguiente:  
  
1.  Asegúrese de que las selecciones sean correctas. Expanda los nodos de la sesión de eventos para comprobar que todas las selecciones se incluirán en la sesión de eventos.  
  
2.  Haga clic en **Script** para exportar el script de creación de la sesión a una nueva ventana del Editor de consultas.  
  
3.  Haga clic en **Finalizar** para crear la sesión de eventos.  
  
##  <a name="BKMK_CreateEventSession"></a> Crear sesión de eventos  
 En la página **Crear sesión de eventos** , una vez creada correctamente la sesión de eventos, realice lo siguiente:  
  
1.  Haga clic en **Iniciar la sesión de eventos inmediatamente después de crear la sesión** para iniciar la sesión después de cerrar el asistente. Debe iniciar la sesión de eventos inmediatamente después de crear la sesión para poder observar datos en directo.  
  
2.  Haga clic en **Observar datos en directo en la pantalla mientras se capturan** para ver los datos en directo de la sesión de eventos. Los datos en directo iniciarán la presentación del seguimiento inmediatamente después de crearse la sesión.  
  
## <a name="see-also"></a>Vea también  
 [Crear una sesión de eventos extendidos utilizando el cuadro de diálogo Nueva sesión](../../2014/database-engine/create-an-extended-events-session-using-the-new-session-dialog.md)  
  
  
