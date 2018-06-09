---
title: Información general del Asistente de migración de datos (SQL Server) | Documentos de Microsoft
ms.custom: ''
ms.date: 03/15/2018
ms.prod: sql
ms.prod_service: dma
ms.reviewer: ''
ms.suite: sql
ms.technology: dma
ms.tgt_pltfrm: ''
ms.topic: conceptual
keywords: ''
helpviewer_keywords:
- Data Migration Assistant, overview
ms.assetid: ''
caps.latest.revision: ''
author: HJToland3
ms.author: jtoland
manager: craigg
ms.openlocfilehash: dd681a6445c6759b0ec17e06dc0b4dbf24b3b72f
ms.sourcegitcommit: 808d23a654ef03ea16db1aa23edab496b73e5072
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/04/2018
ms.locfileid: "34707973"
---
# <a name="overview-of-data-migration-assistant"></a>Información general del Asistente de migración de datos

El Asistente para la migración de datos (DMA) le permite actualizar a una plataforma de datos modernas al detectar problemas de compatibilidad que pueden afectar a la funcionalidad de la base de datos en la nueva versión de SQL Server y base de datos de SQL Azure. DMA recomienda rendimiento y las mejoras de confiabilidad de su entorno de destino y permite mover el esquema, datos y objetos dependientes desde el servidor de origen al servidor de destino.

> [!NOTE] 
> Para grandes (en términos de número y tamaño de las bases de datos) de las migraciones, se recomienda utilizar la [servicio de migración de base de datos de Azure](https://docs.microsoft.com/azure/dms/dms-overview), que puede migrar las bases de datos a escala.
  
## <a name="capabilities"></a>Capabilities

- Evalúe las instancias de SQL Server local migrar a las bases de datos de SQL Azure. El flujo de trabajo de evaluación le ayuda a detectar los siguientes problemas que pueden afectar a la migración de base de datos de SQL Azure y proporcionan instrucciones detalladas sobre cómo resolverlos.

  - Problemas de bloqueo de migración: detecta bases de datos de los problemas de compatibilidad que migrar de bloque en SQL Server local s para bases de datos de SQL Azure. DMA proporciona recomendaciones para ayudarle a resolver esos problemas.

  - Parcialmente compatible o características no admitidas: detecta características no admitidas o admitidas parcialmente que están actualmente en uso en la instancia de SQL Server de origen. DMA proporciona que un amplio conjunto de recomendaciones, alternativas disponibles en Azure y pasos para que se pueden incorporar en los proyectos de migración.

- Detectar problemas que pueden afectar a una actualización a un servidor local de SQL. Estos se describen como problemas de compatibilidad y se organizan en las siguientes categorías:

  - Cambios importantes
  - Cambios de comportamiento
  - Características desusadas

- Descubra nuevas características de la plataforma de SQL Server de destino que la base de datos puede beneficiarse de tras la actualización. Estos se describen como recomendaciones de la característica y se organizan en las siguientes categorías:

  - Rendimiento
  - Seguridad
  - Storage

- Migrar una instancia de SQL Server local a una instancia de SQL Server moderna, hospedada de forma local o en una máquina virtual Azure (VM) que sea accesible desde la red local. La máquina virtual de Azure puede tener acceso mediante VPN u otras tecnologías. El flujo de trabajo de migración le ayuda a migrar los siguientes componentes:

  - Esquema de bases de datos
  - Datos y usuarios
  - Roles del servidor
  - Inicios de sesión de SQL Server y Windows

- Después de la migración correcta, las aplicaciones pueden conectarse a las bases de datos de destino SQL server sin problemas.

## <a name="supported-source-and-target-versions"></a>Versiones admitidas de origen y de destino

DMA reemplaza todas las versiones anteriores del Asesor de actualizaciones de SQL Server y se debe usar para las actualizaciones para la mayoría de las versiones de SQL Server. Siguen las versiones admitidas de origen y de destino.

**Orígenes**
- SQL Server 2005
- SQL Server 2008
- SQL Server 2008 R2
- SQL Server 2012 
- SQL Server 2014
- SQL Server 2016
- SQL Server de 2017 en Windows

**Destinos**
- SQL Server 2012
- SQL Server 2014
- SQL Server 2016
- SQL Server de 2017 en Windows y Linux
- Se aplica a: Base de datos SQL de Azure

> [!NOTE] 
> DMA no admite actualmente la instancia de base de datos administrada de SQL de Azure como destino.

## <a name="installation"></a>Installation

Para instalar DMA, descargue la versión más reciente de la herramienta desde el [Microsoft Download Center](https://www.microsoft.com/download/details.aspx?id=53595)y, a continuación, ejecute el **DataMigrationAssistant.msi** archivo.

## <a name="see-also"></a>Vea también

[Evaluar la migración a SQL Server](../dma/dma-assesssqlonprem.md)

[Asistente para la migración de datos: Opciones de configuración](../dma/dma-configurationsettings.md)

[Migrar local SQL Server mediante el Asistente de migración de datos](../dma/dma-migrateonpremsql.md)

[Asistente de migración de datos: Prácticas recomendadas](../dma/dma-bestpractices.md)



