---
title: Actualiza la descripción de la solución en el Asistente de experimentación de base de datos para SQL Server
description: Información general del Asistente para experimentación con base de datos
ms.custom: ''
ms.date: 01/08/2019
ms.prod: sql
ms.prod_service: dea
ms.suite: sql
ms.technology: dea
ms.tgt_pltfrm: ''
ms.topic: conceptual
author: HJToland3
ms.author: ajaykar
ms.reviewer: mathoma
manager: jroth
ms.openlocfilehash: 25b5d051f6241919f34a60a42582e8a101052290
ms.sourcegitcommit: ad2e98972a0e739c0fd2038ef4a030265f0ee788
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/07/2019
ms.locfileid: "66794459"
---
# <a name="overview-of-database-experimentation-assistant"></a>Información general del Asistente para experimentación con base de datos

Ayudante para la base de datos de experimentación (DEA) es una solución de experimentación para actualizaciones de SQL Server. DEA puede ayudarle a evaluar una versión de destino de SQL Server para una carga de trabajo específica. Los clientes que están actualizando desde versiones anteriores de SQL Server (a partir de 2005) a una versión más reciente de SQL Server pueden usar las métricas de análisis que proporciona la herramienta. 

Las métricas de análisis DEA incluyen:
- Consultas que tienen errores de compatibilidad
- Degradado de las consultas y planes de consulta
- Otros datos de comparación de la carga de trabajo

Datos de comparación pueden provocar mayor confianza y una experiencia de actualización correcta.

Para obtener una introducción minutos 19 DEA y una demostración, vea el vídeo siguiente:

> [!VIDEO https://channel9.msdn.com/Shows/Data-Exposed/Introducing-the-Database-Experimentation-Assistant/player]

## <a name="get-dea"></a>Obtener DEA

Para instalar DEA, [descargar](https://www.microsoft.com/download/details.aspx?id=54090) la versión más reciente de la herramienta. A continuación, ejecute el **DatabaseExperimentationAssistant.exe** archivo.

## <a name="solution-architecture-for-comparing-workloads"></a>Arquitectura de la solución para comparar las cargas de trabajo

El siguiente diagrama muestra la arquitectura de solución para obtener una comparación de la carga de trabajo. La comparación de la carga de trabajo utiliza DEA y Distributed Replay durante una actualización desde SQL Server 2008 a SQL Server 2016.

![Arquitectura de solución de comparación de carga de trabajo](./media/database-experimentation-assistant-overview/dea-overview-compare-solution-architecture.png)

## <a name="dea-prerequisites"></a>Requisitos previos DEA

Estos son algunos requisitos previos para ejecutar DEA:
- Requisitos mínimos de hardware: Una máquina de núcleo único con 3,5 GB de RAM.
- Requisito de hardware ideal: Una CPU de ocho núcleos (con 3,5 GB de RAM o más). Procesadores que tienen más de ocho núcleos no mejoran los tiempos de ejecución DEA.
- Se necesita un 33% adicional del tamaño de seguimiento del rendimiento de almacén A, B y bases de datos de análisis de informes.

## <a name="configure-dea"></a>Configurar DEA

En la arquitectura de requisitos previos de entorno, le recomendamos que instale DEA *en el mismo equipo que el controlador de Distributed Replay*. Esta práctica evita las llamadas entre equipos y simplifica la configuración.

### <a name="required-configuration-for-workload-comparison-by-using-dea"></a>Configuración necesaria para la comparación de la carga de trabajo mediante el uso de DEA

DEA se conecta a servidores de base de datos mediante la autenticación de Windows. Asegúrese de que un usuario que ejecuta DEA puede conectarse a servidores de base de datos (origen, destino y análisis) mediante la autenticación de Windows.

**Capturar los requisitos de configuración**:

*   Usuario que ejecuta DEA puede conectarse al servidor de base de datos de origen mediante la autenticación de Windows.
*   Usuario que ejecuta DEA tiene derechos de sysadmin en el servidor de base de datos de origen.
*   Cuenta de servicio que ejecuta el servidor de base de datos de origen tiene acceso de escritura a la ruta de acceso de carpeta de seguimiento.

Para obtener más información, consulte el [capturar las preguntas más frecuentes](database-experimentation-assistant-capture-trace.md#frequently-asked-questions-about-trace-capture)

**Requisitos de configuración de reproducción**: 

*   Usuario que ejecuta DEA puede conectarse al servidor de base de datos de destino mediante la autenticación de Windows.
*   Usuario que ejecuta DEA tiene derechos de sysadmin en el servidor de base de datos de destino.
*   Cuenta de servicio que ejecuta los servidores de base de datos de destino tiene acceso de escritura a la ruta de acceso de carpeta de seguimiento.
*   Cuenta de servicio que usan clientes de Distributed Replay puede conectarse al servidor de base de datos de destino mediante la autenticación de Windows.
*   DEA se comunica con el controlador de Distributed Replay mediante interfaces COM. Asegúrese de que estén abiertos los puertos TCP para las solicitudes entrantes en el controlador de Distributed Replay.

Para obtener más información, consulte el [preguntas más frecuentes de reproducción](database-experimentation-assistant-replay-trace.md#frequently-asked-questions-about-trace-replay)

**Los requisitos de configuración de análisis**: 

*   Usuario que ejecuta DEA puede conectarse al servidor de base de datos de análisis mediante la autenticación de Windows.
*   Usuario que ejecuta DEA tiene derechos de sysadmin en el servidor de base de datos de origen.

Para obtener más información, consulte el [preguntas más frecuentes sobre análisis](database-experimentation-assistant-create-report.md#frequently-asked-questions-about-analysis-reports)

## <a name="set-up-telemetry"></a>Configurar la telemetría

DEA tiene una característica habilitadas para internet que puede enviar información de telemetría a Microsoft. Microsoft recopila datos de telemetría para mejorar la experiencia del producto. La telemetría es opcional. También se guarda la información que se recopila en el equipo para auditoría local. Siempre puede ver lo que se recopilan. Todos los archivos de registro de DEA se guardan en % temp %\\carpeta DEA.

Puede decidir qué eventos se recopilan. También decide si los eventos recopilados se envían a Microsoft. Hay cuatro tipos de eventos:

*   **TraceEvent**: Eventos de uso de la aplicación (por ejemplo, "captura desencadenadas stop").
*   **Excepción**: Excepción iniciada durante el uso de la aplicación.
*   **DiagnosticEvent**: Un registro de eventos para ayudar con el diagnóstico cuando se producen problemas (*no* envía a Microsoft).
*   **FeedbackEvent**: Comentarios del usuario que se envían a través de la aplicación.

Estos pasos muestra cómo elegir qué eventos se recopilan y si los eventos se envían a Microsoft:

1.  Vaya a la ubicación donde está instalado DEA (por ejemplo, C:\\archivos de programa (x86)\\Microsoft Corporation\\Ayudante de experimentación de base de datos).
2.  Abra los archivos .config dos: DEA.exe.config (para la aplicación) y DEACmd.exe.config (para la CLI).
3.  Para detener la recopilación de un tipo de evento, establezca el valor de *eventos* (por ejemplo, **TraceEvent**) a **false**. Para iniciar la recopilación de nuevo el evento, establezca el valor en **true**.
4.  Para dejar de guardar copias locales de los eventos, establezca el valor de **TraceLoggerEnabled** a **false**. Para empezar a guardar copias locales de nuevo, establezca el valor en **true**.
5.  Para detener el envío de eventos a Microsoft, establezca el valor de **AppInsightsLoggerEnabled** a **false**. Para empezar a enviar eventos a Microsoft de nuevo, establezca el valor en **true**.

DEA se rige por el [declaración de privacidad de Microsoft](https://aka.ms/dea-privacy).

## <a name="next-steps"></a>Pasos siguientes

[Introducción a](database-experimentation-assistant-get-started.md) le guiará a través de los pasos necesarios para capturar, reproducir y analizar un seguimiento.
