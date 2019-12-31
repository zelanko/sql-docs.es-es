---
title: Información general del proceso de comparación de cargas de trabajo
description: Asistente para experimentación con bases de datos (DEA) es una solución de prueba A/B para los cambios en entornos SQL Server, como actualizaciones o nuevos índices.
ms.date: 12/12/2019
ms.prod: sql
ms.prod_service: dea
ms.suite: sql
ms.technology: dea
ms.tgt_pltfrm: ''
ms.topic: conceptual
author: HJToland3
ms.author: rajsell
ms.reviewer: mathoma
ms.custom: seo-lt-2019
ms.openlocfilehash: 36e36060e16ff85ba2b1fa58d9d900231cf6581f
ms.sourcegitcommit: 792c7548e9a07b5cd166e0007d06f64241a161f8
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/19/2019
ms.locfileid: "75258522"
---
# <a name="overview-of-the-workload-comparison-process"></a>Información general del proceso de comparación de cargas de trabajo

Asistente para experimentación con bases de datos (DEA) le ayuda a evaluar cómo realizará la carga de trabajo en el servidor de origen (en su entorno actual) en el nuevo entorno. DEA le guía a través de la ejecución de una prueba A/B mediante la realización de tres fases:

- Captura de un seguimiento de carga de trabajo en el servidor de origen.
- Reproducir el seguimiento de la carga de trabajo capturado en el destino 1 y el destino 2.
- Analizar los seguimientos de carga de trabajo reproducidos recopilados del destino 1 y el destino 2.

En este artículo se proporciona información general sobre este proceso.

## <a name="capturing-a-workload-trace"></a>Capturar un seguimiento de carga de trabajo

La primera fase de SQL Server prueba a/B es capturar un seguimiento en el servidor de origen. Por lo general, el servidor de origen es el servidor de producción. Los archivos de seguimiento capturan toda la carga de trabajo de consultas en ese servidor, incluidas las marcas de tiempo.

Consideraciones:

- Antes de empezar, asegúrese de hacer una copia de seguridad de las bases de datos desde las que va a capturar el seguimiento.
- El usuario de DEA debe poder conectarse a la base de datos mediante la autenticación de Windows.
- Una cuenta de servicio de SQL Server debe poder tener acceso a la ruta de acceso del archivo de seguimiento de origen.
- Para que DEA determine si el rendimiento de una consulta se ha mejorado o degradado, dicha consulta debe ejecutarse al menos 15 veces durante el período de captura.

## <a name="replaying-a-workload-trace"></a>Reproducir un seguimiento de carga de trabajo

La segunda fase de SQL Server pruebas A/B es reproducir el archivo de seguimiento capturado en dos servidores de destino:

Destino 1, que imita el destino del servidor de origen 2, que imita el entorno de destino propuesto.

Las configuraciones de hardware de destino 1 y destino 2 deben ser lo más parecidas posible para que SQL Server pueda analizar con precisión el efecto de rendimiento de los cambios propuestos.

Consideraciones:

- Para reproducir un seguimiento de la carga de trabajo, los equipos deben estar configurados para ejecutar seguimientos de Distributed Replay (DReplay).
- Asegúrese de restaurar las bases de datos en los servidores de destino mediante la copia de seguridad del servidor de origen.
- Se recomienda reiniciar el servicio de SQL Server (MSSQLSERVER) en la aplicación de servicios para mejorar la coherencia en los resultados de la evaluación. El almacenamiento en caché de consultas en SQL Server puede afectar a los resultados de la evaluación.

## <a name="analyzing-the-replayed-workload-traces"></a>Análisis de los seguimientos de carga de trabajo reproducidos

La fase final del proceso es generar un informe de análisis mediante los seguimientos de reproducción y revisar el informe para obtener información sobre las posibles implicaciones de rendimiento del cambio propuesto.

Consideraciones:

- Si faltan uno o más componentes, aparecerá una página de requisitos previos con vínculos para descargas al intentar generar un nuevo informe de análisis (se requiere conexión a Internet).
- Para ver un informe generado en una versión anterior de la herramienta, primero debe actualizar el esquema.

## <a name="see-also"></a>Vea también

- Para obtener información sobre cómo generar un archivo de seguimiento con un registro de eventos que se producen en un servidor, vea el artículo [capturar un seguimiento en Asistente para experimentación con bases de datos](database-experimentation-assistant-capture-trace.md).