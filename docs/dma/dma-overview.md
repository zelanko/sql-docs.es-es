---
title: "Información general del Asistente de migración de datos (SQL Server) | Documentos de Microsoft"
ms.custom: 
ms.date: 10/04/2017
ms.prod: sql-non-specified
ms.prod_service: dma
ms.service: 
ms.component: dma
ms.reviewer: 
ms.suite: sql
ms.technology: sql-dma
ms.tgt_pltfrm: 
ms.topic: article
keywords: 
helpviewer_keywords: Data Migration Assistant, overview
ms.assetid: 
caps.latest.revision: 
author: HJToland3
ms.author: jtoland
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: cc543e392818c2fa8ceea1c55e7a065df603b02d
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/20/2017
---
# <a name="overview-of-data-migration-assistant"></a>Información general del Asistente de migración de datos

Asistente de migración de datos (DMA) le permite actualizar a una plataforma de datos modernas al detectar problemas de compatibilidad que pueden afectar a la funcionalidad de la base de datos en la nueva versión de SQL Server y base de datos de SQL Azure. DMA recomienda rendimiento y las mejoras de confiabilidad de su entorno de destino y permite mover el esquema, datos y objetos dependientes desde el servidor de origen al servidor de destino.

## <a name="capabilities"></a>Capabilities

- Evalúe las instancias de SQL Server local migrar a las bases de datos de SQL Azure. El flujo de trabajo de evaluación le ayuda a detectar los siguientes problemas que pueden afectar a la migración de base de datos de SQL Azure y proporcionan instrucciones detalladas sobre cómo resolverlos.

  - Problemas de bloqueo de migración: detecta bases de datos de los problemas de compatibilidad que migrar de bloque en SQL Server local s para bases de datos de SQL Azure. DMA proporciona recomendaciones para ayudarle a resolver esos problemas.

  - Parcialmente compatible o características no admitidas: detecta características no admitidas o admitidas parcialmente que están actualmente en uso en la instancia de SQL Server de origen. DMA proporciona que un amplio conjunto de recomendaciones, alternativas disponibles en Azure y pasos para que se pueden incorporar en los proyectos de migración.

- Detectar problemas que pueden afectar a una actualización a un servidor local de SQL.  Estos se describen como problemas de compatibilidad y se organizan en las siguientes categorías:

  - Cambios importantes

  - Cambios de comportamiento

  - Características desusadas

- Descubra nuevas características de la plataforma de SQL Server de destino que la base de datos puede beneficiarse de tras la actualización. Estos se describen como recomendaciones de la característica y se organizan en las siguientes categorías:

  - Rendimiento

  - Seguridad

  - Almacenamiento

- Migrar una instancia de SQL Server local a una instancia de SQL Server moderna, hospedada de forma local o en una máquina virtual Azure (VM) que sea accesible desde la red local. La máquina virtual de Azure puede tener acceso mediante VPN u otras tecnologías. El flujo de trabajo de migración le ayuda a migrar los siguientes componentes:

  - Esquema de bases de datos

  - Datos y usuarios

  - Roles del servidor

  - Inicios de sesión de SQL Server y Windows

- Después de la migración correcta, las aplicaciones pueden conectarse a las bases de datos de destino SQL server sin problemas.

## <a name="supported-source-and-target-versions"></a>Versiones admitidas de origen y de destino

DMA reemplaza todas las versiones anteriores del Asesor de actualizaciones de SQL Server y se debe usar para las actualizaciones para la mayoría de las versiones de SQL Server. Siguen las versiones admitidas de origen y de destino.

**Orígenes**
- Resultado de
- SQL Server 2008
- SQL Server 2008 R2
- SQL Server 2012 
- SQL Server 2014
- SQL Server 2016

**Destinos**
- SQL Server 2012
- SQL Server 2014
- SQL Server 2016
- Base de datos SQL de Azure

## <a name="installation"></a>Installation

Para instalar DMA, descargue la versión más reciente de la herramienta desde el [Microsoft Download Center](https://www.microsoft.com/download/details.aspx?id=53595)y, a continuación, ejecute el **DataMigrationAssistant.msi** archivo.

## <a name="see-also"></a>Vea también

[Evaluar la migración a SQL Server](../dma/dma-assesssqlonprem.md)

[Asistente para la migración de datos: Opciones de configuración](../dma/dma-configurationsettings.md)

[Migrar local SQL Server mediante el Asistente de migración de datos](../dma/dma-migrateonpremsql.md)

[Asistente de migración de datos: Prácticas recomendadas](../dma/dma-bestpractices.md)



