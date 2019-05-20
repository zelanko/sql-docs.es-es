---
title: Novedades de Data Migration Assistant (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 05/18/2019
ms.prod: sql
ms.prod_service: dma
ms.reviewer: ''
ms.technology: dma
ms.topic: conceptual
keywords: ''
helpviewer_keywords:
- Data Migration Assistant, new features
ms.assetid: ''
author: HJToland3
ms.author: jtoland
manager: craigg
ms.openlocfilehash: 5b000a420867428116403fb067cf79215b6ea196
ms.sourcegitcommit: 179ab0e55f918f58a18c43af076130f4ac3decd6
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/19/2019
ms.locfileid: "65875187"
---
# <a name="whats-new-in-data-migration-assistant"></a>Novedades de Data Migration Assistant
En este artículo se enumera las adiciones en cada versión de Data Migration Assistant (DMA).

## <a name="dma-v43"></a>V. 4.3 DMA

La versión v. 4.3 de DMA ofrece compatibilidad para:

* Recomendaciones de SKU de Azure SQL Database administra instancias según la evaluación de la carga de trabajo.
* RDS SQL Server como origen para las evaluaciones.
* Instancia administran de evaluaciones de trabajo de agente de Azure SQL Database como destino.
* La capacidad de omitir ciertas reglas de evaluación; la lista de códigos de error especificado en la propiedad 'ignoreErrorCodes' configurada en DMA no aparece en los resultados de la evaluación de DMA.
* Evaluación de las consultas de T-SQL en los pasos de la actividad de trabajo y proporcionar recomendaciones adecuadas
* Evaluaciones de eventos extendidos (versión preliminar pública).

Además, esta versión de DMA proporciona un rendimiento mejorado para controlar un gran número de objetos de esquema en bases de datos, así como correcciones de errores relacionados con:

* Procedimientos compilados con la compilación nativa, en algunos casos.
* Esquemas de base de datos complejas.

## <a name="dma-v42"></a>DMA v4.2

La versión v4.2 de DMA proporciona compatibilidad de línea de comandos para evaluación de preparación para una o varias instancias del servidor de destino cuando la instancia administrada de migración desde un entorno local de SQL Server a Azure SQL Database. Los clientes ahora pueden usar la línea de comandos DMA para recopilar metadatos acerca de su esquema de base de datos, detectar los bloqueadores de elementos y conozca las características no admitidas o parcialmente compatibles que afectan a la migración a una instancia administrada de Azure SQL Database. A continuación, se pueden representar los resultados mediante la plantilla de Power BI proporcionada.

## <a name="dma-v41"></a>DMA v4.1

La versión de la versión 4.1 de DMA incorpora compatibilidad para una evaluación completa de bases de datos de SQL Server en el entorno local la migración a instancia administrada de Azure SQL Database.

El flujo de trabajo de evaluación le ayuda a detectar los problemas siguientes, que pueden afectar a la migración a instancia administrada de Azure SQL Database:

* **No admitido o características admitidas parcialmente**. DMA evalúa la base de datos de SQL Server de origen para las características de uso que son parcialmente compatibles o no admitido en el destino de la instancia administrada de Azure SQL Database. La herramienta, a continuación, proporciona un conjunto completo de recomendaciones, alternativas disponibles en Azure y mitigar los pasos para que los clientes pueden aprovechar esta información en cuenta al planear sus proyectos de migración.

* **Problemas de compatibilidad**. DMA también identifica los problemas de compatibilidad relacionados con las siguientes áreas:

  * Cambios importantes:  Los objetos de esquema específico que se pueden interrumpir la funcionalidad de migración a la base de datos de destino.  Se recomienda corregir estos objetos de esquema después de la migración de base de datos.
  * Cambios de comportamiento: Notifica los objetos de esquema pueden seguir trabajando, pero es posible que exhiben un comportamiento diferente, por ejemplo una degradación del rendimiento.
  * Problemas informativos:  Estos objetos no afectarán a la migración, pero es posible que se han quedado en desuso desde la característica de que versiones de SQL Server.

Una vez completada la evaluación, use nuestro [Azure Database Migration Service](https://azure.microsoft.com/services/database-migration/) (DMS) para realizar la migración de las bases de datos de SQL Server a instancia administrada de Azure SQL Database.  DMS es compatible con ambos [sin conexión](https://docs.microsoft.com/azure/dms/tutorial-sql-server-to-managed-instance) (única) y [online](https://docs.microsoft.com/azure/dms/tutorial-sql-server-managed-instance-online) migraciones de base de datos (tiempo de inactividad mínimo) a la instancia administrada de Azure SQL Database.

## <a name="dma-v40"></a>DMA v4.0

La versión v4.0 de DMA presenta la característica de recomendaciones de SKU de base de datos de SQL Azure, que permite a los usuarios identificar las mínimas recomendadas SKU de base de datos de SQL Azure en función de los contadores de rendimiento recopilados de los equipos que aloja las bases de datos. Esta característica proporciona recomendaciones relacionadas con los precios de nivel, el nivel de proceso y tamaño máximo de datos, así como el costo estimado por mes. También ofrece la posibilidad de aprovisionar todas las bases de datos a Azure de forma masiva.

> [!NOTE]
> Esta funcionalidad está actualmente esté disponible solo mediante la interfaz de línea de comandos (CLI).

Para obtener detalles adicionales, consulte el artículo [identificar la SKU de base de datos SQL de Azure adecuada para la base de datos local](dma-sku-recommend-sql-db.md).

## <a name="dma-v36"></a>DMA v3.6

La versión 3.6 de DMA presenta "Corrección automática" para los objetos de esquema que se ven afectadas por los bloqueadores de migración más comunes.

Esta versión proporciona corrección automática para el bloqueador de migración siguientes y problemas de cambio de comportamiento:

* Los objetos de esquema que utilizan la sintaxis de combinación no calificado.
* Los objetos de esquema que utilice la instrucción RAISEERROR heredada.
* Instrucciones SQL que usan el orden por entero Literal.

DMA realiza la conversión automática de esquemas para los objetos afectados por los problemas indicados y solicita al usuario confirmación antes de continuar con la conversión de esquema. Los usuarios pueden revisar los cambios de código sugerido y, a continuación, Aceptar o rechazar todas las conversiones para cualquier objeto de base de datos determinada.

DMA usa tecnología de síntesis de programa de Microsoft (PROSE) para sugerir que corrige el código. Obtenga más información sobre [PROSE](https://microsoft.github.io/prose/).

## <a name="dma-v35"></a>DMA v3.5

La versión 3.5 de DMA incluye las siguientes adiciones:

* Mejoras de rendimiento significativas para migrar a Azure SQL Database (pruebas comparativas indican que el proceso es cuatro veces más rápido que con versiones anteriores de DMA).
* La superficie de memoria se optimiza aún más para mejorar la estabilidad del flujo de trabajo de migración.
* La capacidad de omitir las evaluaciones durante las migraciones de datos y el esquema (si ya ha realizado la evaluación y direccionar los objetos de esquema importantes antes de la migración).
* Una corrección para solucionar un problema con la herramienta de bloqueo cuando se proporciona una ruta de acceso del recurso compartido de red no válido para los archivos de copia de seguridad, al realizar una actualización de una versión heredada de SQL Server locales a una versión posterior o SQL Server en máquinas virtuales de Azure.

## <a name="dma-v34"></a>3.4 DMA

La versión 3.4 de DMA incluye las siguientes adiciones:

* Compatibilidad con SQL Server 2017 como origen para las migraciones a Azure SQL Database.
* Mejoras de estabilidad, rendimiento y evaluación de la corrección de regla.

## <a name="dma-v33"></a>DMA v3.3

La versión v3.3 de DMA permite la migración de una instancia de SQL Server local a la nueva versión de SQL Server 2017 en Windows y Linux. Aunque el flujo de trabajo de migración general para Windows y Linux es el mismo, la migración a SQL Server 2017 para Linux requiere algunas consideraciones adicionales.

### <a name="specifying-the-back-up-path"></a>Especifica la ruta de acceso de copia de seguridad

Linux y Windows usan formatos de ruta de acceso diferente. Como resultado, la migración a SQL Server 2017 en Linux requiere que el usuario proporcione versiones de la Windows y Linux de la ruta de acceso a la ubicación del archivo físico. Puede proporcionar ambas versiones de la ruta de acceso de maneras diferentes según la ubicación del archivo físico.
Si el archivo de copia de seguridad físico está en un equipo que ejecute:

* Linux, use un 'samba' comparte para compartir el archivo con otros equipos de la red.
* Windows, use el comando "mnt" montar el recurso compartido en el equipo que ejecuta Linux.

> [!NOTE]
> Detalles de uso de un recurso compartido de 'samba' o el comando "mnt" están fuera del ámbito de este artículo.

### <a name="migrating-windows-logins"></a>Migrar los inicios de sesión de Windows

Mientras la migración de los inicios de sesión de Active Directory (AD) es compatible oficialmente con SQL Server 2017 en Linux, requiere configuración adicional para funcionar correctamente. Consulte el artículo [autenticación de Active Directory con SQL Server en Linux](https://docs.microsoft.com/sql/linux/sql-server-linux-active-directory-authentication) para obtener información detallada acerca de cómo configurar los inicios de sesión de Active Directory en SQL Server 2017 en Linux. Después de realizar la configuración necesaria, el programa de instalación está completa y puede migrar los inicios de sesión de Active Directory como de costumbre. Autenticación de SQL estándar funciona según lo esperado sin ninguna configuración adicional.

## <a name="dma-v32"></a>V3.2 DMA

La versión v3.2 de DMA incluye las siguientes adiciones:

* Migración de esquema y los datos están habilitadas de bases de datos de SQL Server local a Azure SQL Database con un nuevo flujo de trabajo de migración.
* Durante la migración de esquema a Azure SQL Database, DMA scripts los objetos de base de datos de origen, proporciona instrucciones sobre cómo solucionar los posibles problemas de compatibilidad y, a continuación, implementa el esquema en Azure.

## <a name="dma-v31"></a>DMA v3.1

La versión de v3.1 de DMA incluye las siguientes adiciones:

* Las recomendaciones de evaluación mejorada para bases de datos de SQL Azure en cuanto a las intercalaciones de base de datos, el uso de procedimientos almacenados del sistema no compatibles y objetos de CLR.
* Guía de evaluación para los niveles de compatibilidad 100 al migrar a Azure SQL Database, 110, 120 y 130.

## <a name="dma-v30"></a>DMA v3.0

La versión v3.0 de DMA amplía la evaluación de la base de datos SQL de Azure para proporcionar recomendaciones integrales para ayudar a solucionar problemas relacionados con:

* Problemas de bloqueo de migración.
* Parcialmente o las funciones y características no admitidas.

## <a name="dma-v21"></a>DMA v2.1

La versión de v2.1 de DMA incluye las siguientes adiciones:

* Compatibilidad de línea de comandos para ejecutar las evaluaciones en modo desatendido, lo que ayuda a ejecutar las evaluaciones a escala. Para obtener detalles adicionales, consulte el artículo [ejecutar Data Migration Assistant desde la línea de comandos](dma-commandline.md).
* Mejoras de rendimiento cuando los usuarios iniciarán y cerrar DMA.
* La capacidad de configurar el tiempo de espera de conexión de SQL. Para obtener detalles adicionales, consulte el artículo [opciones de configuración de Data Migration Assistant](dma-configurationsettings.md).

## <a name="dma-v20"></a>DMA v2.0

La versión de la versión 2.0 de DMA incluye recomendaciones de características de base de datos de Stretch mejoradas para proporcionar las tablas apropiadas de prioridades que maximicen el ahorro de almacenamiento.

## <a name="dma-v10"></a>DMA v1.0

La versión 1.0 de DMA es la versión inicial, y proporciona para:

* Detección de problemas que pueden afectar a una actualización a una versión local de SQL Server. Se describen todas las observaciones como problemas de compatibilidad y se clasifica por categorías en las siguientes áreas:
  * Cambios importantes
  * Cambios de comportamiento
  * Características en desuso
* Detección de nuevas características de la plataforma de SQL Server de destino que puede beneficiarse de la base de datos tras una actualización. Se describen todas las observaciones como recomendación de característica y se clasifica por categorías en las siguientes áreas:
  * Rendimiento
  * Seguridad
  * Storage
* Experiencia de usuario moderna a realizar evaluaciones.

## <a name="see-also"></a>Vea también

[Información general de Data Migration Assistant](../dma/dma-overview.md)
