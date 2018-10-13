---
title: Información general del Asistente de migración de datos (SQL Server) | Microsoft Docs
description: Aprenda a usar Data Migration Assistant para migrar bases de datos de SQL Server a otro servidor de SQL o bases de datos de Azure
ms.custom: ''
ms.date: 08/29/2018
ms.prod: sql
ms.prod_service: dma
ms.reviewer: ''
ms.technology: dma
ms.topic: conceptual
keywords: ''
helpviewer_keywords:
- Data Migration Assistant, overview
ms.assetid: ''
author: HJToland3
ms.author: rajpo
manager: craigg
ms.openlocfilehash: 846fbfdcfb5d99363b98bad09c6efa3a2b46b4ab
ms.sourcegitcommit: 485e4e05d88813d2a8bb8e7296dbd721d125f940
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/11/2018
ms.locfileid: "49100376"
---
# <a name="overview-of-data-migration-assistant"></a>Información general de Data Migration Assistant

El Data Migration Assistant (DMA) le ayuda a que actualizar a una plataforma de datos moderna detectando problemas de compatibilidad que pueden afectar a la funcionalidad de base de datos en la nueva versión de SQL Server o de base de datos de SQL Azure. DMA recomienda mejoras de rendimiento y confiabilidad para su entorno de destino y le permite mover el esquema, datos y objetos dependientes del servidor de origen al servidor de destino.

> [!NOTE] 
> Para las migraciones de gran tamaño (en términos de número y tamaño de las bases de datos), se recomienda que use el [Azure Database Migration Service](https://docs.microsoft.com/azure/dms/dms-overview), que puede migrar las bases de datos a escala.
  
## <a name="capabilities"></a>Capabilities

- Evalúe las instancias de SQL Server local migrar a las bases de datos SQL de Azure. El flujo de trabajo de evaluación le ayuda a detectar los siguientes problemas que pueden afectar a la migración de bases de datos SQL de Azure y proporcionan instrucciones detalladas sobre cómo resolverlos.

  - Problemas de bloqueo de migración: detecta s a las bases de datos SQL de Azure de bases de datos de los problemas de compatibilidad que migrar de bloque en SQL Server local. DMA proporciona recomendaciones para ayudarle a resolver esos problemas.

  - Características no admitidas o parcialmente compatibles: detecta las características no admitidas o parcialmente compatibles que están actualmente en uso en la instancia de SQL Server de origen. DMA proporciona que un completo conjunto de recomendaciones, alternativas disponibles en Azure y pasos de mitigación, por lo que puede incorporar en los proyectos de migración.

- Detectar problemas que pueden afectar a una actualización a un servidor de SQL en el entorno local. Estas se describen como problemas de compatibilidad y se organizan en las siguientes categorías:

  - Cambios importantes
  - Cambios de comportamiento
  - Características en desuso

- Descubra las nuevas características de la plataforma de SQL Server de destino que puede beneficiarse de la base de datos tras una actualización. Estas se describen como recomendación de característica y se organizan en las siguientes categorías:

  - Rendimiento
  - Seguridad
  - Storage

- Migrar una instancia de SQL Server local a una instancia de SQL Server modernas hospedada localmente o en una máquina virtual Azure (VM) que sea accesible desde la red local. Puede tener acceso a la máquina virtual de Azure mediante VPN u otras tecnologías. El flujo de trabajo de migración le ayuda a migrar los siguientes componentes:

  - Esquema de bases de datos
  - Datos y usuarios
  - Roles del servidor
  - Inicios de sesión de SQL Server y Windows

- Después de una migración correcta, las aplicaciones pueden conectarse sin problemas a las bases de datos de destino SQL server.

## <a name="supported-source-and-target-versions"></a>Versiones compatibles de origen y destino

DMA reemplaza todas las versiones anteriores del Asesor de actualizaciones de SQL Server y se debe usar para las actualizaciones para la mayoría de las versiones de SQL Server. Siguen las versiones compatibles de origen y de destino.

**Orígenes**
- SQL Server 2005
- SQL Server 2008
- SQL Server 2008 R2
- SQL Server 2012 
- SQL Server 2014
- SQL Server 2016
- SQL Server 2017 en Windows

**Destinos**
- SQL Server 2012
- SQL Server 2014
- SQL Server 2016
- SQL Server 2017 en Windows y Linux
- Se aplica a: Base de datos SQL de Azure

> [!NOTE] 
> DMA no admite actualmente la instancia administrada de Azure SQL Database como destino.

## <a name="installation"></a>Installation

Para instalar DMA, descargue la versión más reciente de la herramienta desde el [Microsoft Download Center](https://www.microsoft.com/download/details.aspx?id=53595)y, a continuación, ejecute el **DataMigrationAssistant.msi** archivo.

## <a name="see-also"></a>Vea también

[Evaluar la migración a SQL Server](../dma/dma-assesssqlonprem.md)

[Asistente para la migración de datos: Opciones de configuración](../dma/dma-configurationsettings.md)

[Migrate On-Premises SQL Server mediante Data Migration Assistant](../dma/dma-migrateonpremsql.md)

[Asistente para la migración de datos: Procedimientos recomendados](../dma/dma-bestpractices.md)



