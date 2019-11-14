---
title: Información general sobre el Asistente para experimentación con bases de datos
description: Información general de Asistente para experimentación con bases de datos
ms.custom: seo-lt-2019
ms.date: 11/05/2019
ms.prod: sql
ms.prod_service: dea
ms.suite: sql
ms.technology: dea
ms.tgt_pltfrm: ''
ms.topic: conceptual
author: HJToland3
ms.author: jtoland
ms.reviewer: mathoma
ms.openlocfilehash: 7180656f8a4779c43f4c691f583aaaf5fcbf86d0
ms.sourcegitcommit: d00ba0b4696ef7dee31cd0b293a3f54a1beaf458
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/13/2019
ms.locfileid: "74056581"
---
# <a name="overview-of-database-experimentation-assistant"></a>Información general de Asistente para experimentación con bases de datos

Asistente para experimentación con bases de datos (DEA) es una solución de experimentación para las actualizaciones de SQL Server. DEA puede ayudarle a evaluar una versión de destino de SQL Server para una carga de trabajo específica. Los clientes que están actualizando desde versiones SQL Server anteriores (a partir de 2005) a una versión más reciente de SQL Server pueden utilizar las métricas de análisis que proporciona la herramienta.

Las métricas de análisis de DEA incluyen:

- Consultas que tienen errores de compatibilidad
- Consultas degradadas y planes de consulta
- Otros datos de comparación de carga de trabajo

Los datos de comparación pueden dar lugar a una mayor confianza y una experiencia de actualización correcta.

## <a name="get-dea"></a>Obtener DEA

Para instalar DEA, [Descargue](https://www.microsoft.com/download/details.aspx?id=54090) la versión más reciente de la herramienta. A continuación, ejecute el archivo **DatabaseExperimentationAssistant. exe** .

## <a name="solution-architecture-for-comparing-workloads"></a>Arquitectura de la solución para comparar cargas de trabajo

En el diagrama siguiente se muestra la arquitectura de la solución para una comparación de carga de trabajo. La comparación de la carga de trabajo usa DEA y Distributed Replay durante una actualización de SQL Server 2008 a SQL Server 2016.

![Arquitectura de la solución de comparación de carga de trabajo](./media/database-experimentation-assistant-overview/dea-overview-compare-solution-architecture.png)

## <a name="dea-prerequisites"></a>Requisitos previos de DEA

A continuación se indican algunos requisitos previos para ejecutar DEA:

- Requisito de hardware mínimo: una máquina de un solo núcleo con 3,5 GB de RAM.
- Requisito de hardware ideal: una CPU de ocho núcleos (con 3,5 GB de RAM o más). Los procesadores que tienen más de ocho núcleos no mejoran los tiempos de ejecución de DEA.
- Se necesita un 33% de tamaño de seguimiento de rendimiento adicional para almacenar las bases de datos de análisis de informes, B y.

## <a name="configure-dea"></a>Configuración de DEA

En la arquitectura de entorno de requisito previo, se recomienda instalar DEA *en el mismo equipo que el controlador de Distributed Replay*. Esta práctica evita las llamadas entre equipos y simplifica la configuración.

### <a name="required-configuration-for-workload-comparison-by-using-dea"></a>Configuración necesaria para la comparación de cargas de trabajo mediante DEA

DEA se conecta a los servidores de bases de datos mediante la autenticación de Windows. Asegúrese de que un usuario que ejecute DEA pueda conectarse a los servidores de bases de datos (origen, destino y análisis) mediante la autenticación de Windows.

**Capturar los requisitos de configuración**:

- El usuario que ejecuta DEA puede conectarse al servidor de base de datos de origen mediante la autenticación de Windows.
- El usuario que ejecuta DEA tiene derechos de administrador del servidor en el servidor de base de datos de origen.
- La cuenta de servicio que ejecuta el servidor de base de datos de origen tiene acceso de escritura a la ruta de la carpeta de seguimiento.

Para obtener más información, consulte las [preguntas más frecuentes sobre capturas](database-experimentation-assistant-capture-trace.md#frequently-asked-questions-about-trace-capture)

**Requisitos de configuración de reproducción**: 

- El usuario que ejecuta DEA puede conectarse al servidor de base de datos de destino mediante la autenticación de Windows.
- El usuario que ejecuta DEA tiene derechos de administrador del servidor en el servidor de base de datos de destino.
- La cuenta de servicio que ejecuta los servidores de base de datos de destino tiene acceso de escritura a la ruta de la carpeta de seguimiento.
- La cuenta de servicio que se ejecuta Distributed Replay clientes puede conectarse al servidor de base de datos de destino mediante la autenticación de Windows.
- DEA se comunica con el controlador de Distributed Replay mediante el uso de interfaces COM. Asegúrese de que los puertos TCP estén abiertos para las solicitudes entrantes en el controlador de Distributed Replay.

Para obtener más información, vea las [preguntas más frecuentes sobre la reproducción](database-experimentation-assistant-replay-trace.md#frequently-asked-questions-about-trace-replay)

**Requisitos de configuración de análisis**:

- El usuario que ejecuta DEA puede conectarse al servidor de base de datos de análisis mediante la autenticación de Windows.
- El usuario que ejecuta DEA tiene derechos de administrador del servidor en el servidor de base de datos de origen.

Para obtener más información, vea las [preguntas más frecuentes sobre análisis](database-experimentation-assistant-create-report.md#frequently-asked-questions-about-analysis-reports)

## <a name="set-up-telemetry"></a>Configuración de la telemetría

DEA tiene una característica habilitada para Internet que puede enviar información de telemetría a Microsoft. Microsoft recopila la telemetría para mejorar la experiencia del producto. La telemetría es opcional. La información recopilada también se guarda en el equipo para la auditoría local. Siempre puede ver lo que se ha recopilado. Todos los archivos de registro de DEA se guardan en la carpeta% Temp%\\DEA.

Puede decidir qué eventos se recopilan. También puede decidir si los eventos recopilados se envían a Microsoft. Hay cuatro tipos de eventos:

- **TraceEvent**: eventos de uso para la aplicación (por ejemplo, "desencadenar detención de captura").
- **Excepción**: excepción producida durante el uso de la aplicación.
- **DiagnosticEvent**: un registro de eventos para ayudar con el diagnóstico cuando se producen problemas (*no* se envían a Microsoft).
- **FeedbackEvent**: comentarios del usuario enviados a través de la aplicación.

En estos pasos se muestra cómo elegir qué eventos se recopilan y si los eventos se envían a Microsoft:

1. Vaya a la ubicación donde se instala DEA (por ejemplo, C:\\archivos de programa (x86)\\Microsoft Corporation\\Asistente para experimentación con bases de datos).
2. Abra los dos archivos. config: DEA. exe. config (para la aplicación) y DEACmd. exe. config (para la CLI).
3. Para dejar de recopilar un tipo de evento, establezca el valor de *evento* (por ejemplo, **TraceEvent**) en **false**. Para empezar a recopilar el evento de nuevo, establezca el valor en **true**.
4. Para dejar de guardar las copias locales de los eventos, establezca el valor de **TraceLoggerEnabled** en **false**. Para volver a guardar las copias locales, establezca el valor en **true**.
5. Para dejar de enviar eventos a Microsoft, establezca el valor de **AppInsightsLoggerEnabled** en **false**. Para empezar a enviar eventos a Microsoft de nuevo, establezca el valor en **true**.

DEA se rige por la [declaración de privacidad de Microsoft](https://aka.ms/dea-privacy).

## <a name="next-steps"></a>Pasos siguientes

[Introducción](database-experimentation-assistant-get-started.md) le guía a través de los pasos necesarios para capturar, reproducir y analizar un seguimiento.
