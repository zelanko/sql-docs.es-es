---
title: Novedades en el Asistente para migración de datos (SQL Server) | Documentos de Microsoft
ms.custom: ''
ms.date: 06/01/2018
ms.prod: sql
ms.prod_service: dma
ms.reviewer: ''
ms.suite: sql
ms.technology: dma
ms.tgt_pltfrm: ''
ms.topic: conceptual
keywords: ''
helpviewer_keywords:
- Data Migration Assistant, new features
ms.assetid: ''
caps.latest.revision: ''
author: HJToland3
ms.author: jtoland
manager: craigg
ms.openlocfilehash: 1d7d749aae4b5086e44961f9fbcb6967269ccf1c
ms.sourcegitcommit: 6fe7b5e8818bd0d94fce693c560d63cc6883d76f
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/04/2018
ms.locfileid: "34758125"
---
# <a name="whats-new-in-data-migration-assistant"></a>Novedades en el Asistente de migración de datos
Este tema enumeran las adiciones en cada versión del Ayudante de datos de migración (DMA).

## <a name="dma-v35"></a>DMA v3.5
La versión de v3.5 de DMA incluye las siguientes adiciones:
- Mejoras de rendimiento significativas para migrar a base de datos de SQL de Azure (pruebas comparativas indican que el proceso es cuatro veces más rápido que con las versiones anteriores de DMA).
- El consumo de memoria se optimiza aún más para mejorar la estabilidad del flujo de trabajo de migración.
- La capacidad de omitir las evaluaciones durante las migraciones de esquema y los datos (si ya ha realizado la evaluación y direccionar los objetos de esquema importantes antes de la migración).
- Una revisión para resolver un problema con la herramienta de bloqueo cuando se proporciona una ruta de acceso del recurso compartido de red no válido para los archivos de copia de seguridad, al realizar una actualización de una versión heredada de SQL Server local a una versión posterior o a SQL Server en máquinas virtuales de Azure.

## <a name="dma-v34"></a>DMA v3.4
La versión de v3.4 de DMA incluye las siguientes adiciones:
- Compatibilidad con SQL Server 2017 como origen para las migraciones a la base de datos de SQL Azure.
- Mejoras para la estabilidad, el rendimiento y la evaluación de la exactitud de regla.

## <a name="dma-v33"></a>DMA v3.3
La versión v3.3 de DMA permite la migración de una instancia de SQL Server local a la nueva versión de SQL Server 2017, en Windows y Linux. Mientras el flujo de trabajo general de migración de Windows y Linux es la misma, el movimiento a 2017 de SQL Server para Linux requiere un par de consideraciones adicionales.

### <a name="specifying-the-back-up-path"></a>Especifica la ruta de acceso de copia de seguridad
Linux y Windows usan formatos diferentes rutas de acceso. Como resultado, la migración a SQL Server 2017 en Linux requiere que el usuario proporcione versiones de Windows y Linux de la ruta de acceso a la ubicación del archivo físico. Puede proporcionar ambas versiones de la ruta de acceso de maneras diferentes según la ubicación del archivo físico.
Si el archivo de copia de seguridad físico se encuentra en un equipo que ejecute:
- Linux, utilice un 'samba' comparte para compartir el archivo con otros equipos de la red.
- Windows, use el comando 'mnt' para montar el recurso compartido en el equipo que ejecuta Linux.

> [!NOTE]
> Detalles de uso de un recurso compartido 'samba' o el comando 'mnt' quedan fuera del ámbito de este artículo.

### <a name="migrating-windows-logins"></a>Migrar los inicios de sesión de Windows
Mientras la migración de los inicios de sesión de Active Directory (AD) es compatible oficialmente con SQL Server 2017 en Linux, requiere configuración adicional para que funcione correctamente. Consulte el tema [autenticación de Active Directory con SQL Server en Linux](https://docs.microsoft.com/en-us/sql/linux/sql-server-linux-active-directory-authentication) para obtener información detallada acerca de cómo configurar los inicios de sesión de Active Directory en SQL Server 2017 en Linux. Después de realizar la configuración necesaria, el programa de instalación está completa y puede migrar los inicios de sesión de Active Directory como de costumbre. Autenticación de SQL estándar funciona como se esperaba sin ninguna configuración adicional.

## <a name="dma-v32"></a>V3.2 DMA
La versión de v3.2 de DMA incluye las siguientes adiciones:

- Migración de datos y esquemas están habilitados de bases de datos de SQL Server local a la base de datos de SQL Azure con un nuevo flujo de trabajo de migración.
- Durante la migración de esquema para la base de datos de SQL Azure, DMA secuencias de comandos de los objetos de base de datos de origen, proporciona instrucciones sobre cómo solucionar los posibles problemas de compatibilidad y, a continuación, implementa el esquema en Azure.

## <a name="dma-v31"></a>DMA v3.1
La versión de v3.1 de DMA incluye las siguientes adiciones:

- Recomendaciones de evaluación mejorada para bases de datos de SQL Azure en cuanto a las intercalaciones de base de datos, el uso de procedimientos almacenados del sistema no compatibles y objetos CLR.
- Guía de evaluación para niveles de compatibilidad 130, 120, 110 y 100 durante la migración de bases de datos de SQL Azure.

## <a name="dma-v30"></a>DMA v3.0
La versión v3.0 de DMA extiende la evaluación de la base de datos de SQL Azure para proporcionar recomendaciones exhaustivas para ayudar a solucionar problemas relacionados con:

- Problemas de bloqueo de migración.
- Parcialmente o no admite las características y funciones.

## <a name="dma-v21"></a>DMA v2.1
La versión de v2.1 de DMA incluye las siguientes adiciones:
- Compatibilidad de línea de comandos para ejecutar las evaluaciones en modo desatendido, lo que ayuda a ejecutar las evaluaciones a escala. Para obtener detalles adicionales, consulte el tema [ejecutar datos Migration Assistant desde la línea de comandos](dma-commandline.md).
- Mejoras de rendimiento cuando los usuarios iniciarán y cerrar DMA.
- La capacidad para configurar el tiempo de espera de conexión de SQL. Para obtener detalles adicionales, consulte el tema [valores de configuración para el Asistente de migración de datos](dma-configurationsettings.md).

## <a name="dma-v20"></a>DMA v2.0
La versión 2.0 de DMA incluye recomendaciones de característica de base de datos de Stretch mejoradas para proporcionar tablas apropiadas de prioridades que maximizan el ahorro de almacenamiento.

## <a name="dma-v10"></a>DMA v1.0
La versión 1.0 de DMA es la versión inicial, así como para:
- Detección de problemas que pueden afectar a una actualización a una versión local de SQL Server. Todas las observaciones se describen como problemas de compatibilidad y se clasifica por categorías en las siguientes áreas:
    - Cambios importantes
    - Cambios de comportamiento
    - Características desusadas
- Detección de nuevas características de la plataforma de SQL Server de destino que la base de datos puede beneficiarse de una actualización. Todas las observaciones se describen como recomendaciones de la característica y se clasifica por categorías en las siguientes áreas:
    - Rendimiento
    - Seguridad
    - Storage
-   Experiencia de usuario moderna para realizar evaluaciones.

## <a name="see-also"></a>Vea también
[Información general del Asistente de migración de datos](../dma/dma-overview.md)
