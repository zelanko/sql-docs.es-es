---
title: Configurar la conectividad de PolyBase - Analytics Platform System | Microsoft Docs
description: Explica cómo configurar PolyBase en almacenamiento de datos paralelos para conectarse a Hadoop o Microsoft Azure storage blob orígenes de datos externos. Uso de PolyBase para ejecutar consultas que se integran datos desde varios orígenes, como Hadoop, Azure blob storage y almacenamiento de datos paralelos.
author: mzaman1
manager: craigg
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.openlocfilehash: da6d71521f72ff23b4caf2f27dbc663dee684592
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "63057826"
---
# <a name="what-is-polybase"></a>¿Qué es PolyBase?
PolyBase permite su Analytics Platform System (APS) para procesar consultas Transact-SQL que pueden leer y escribir datos en orígenes de datos externos. Las mismas consultas que tienen acceso a datos externos también pueden incluir tablas de relaciones en los puntos de acceso. Esto le permite combinar datos de orígenes externos con datos relacionales de gran valor en las bases de datos de puntos de acceso.

![Lógica de PolyBase](media/polybase/polybase-logical.png)

PolyBase en puntos de acceso es compatible con la lectura y escritura en el sistema de archivos Hadoop (HDFS) y Azure Blob Storage. PolyBase también tiene la capacidad para insertar algún cálculo en nodos de Hadoop como trabajos de mapreduce para optimizar el rendimiento general de las consultas. PolyBase en puntos de acceso puede operar en texto delimitado, ORC y Parquet archivos. Consulte [¿qué es PolyBase](https://docs.microsoft.com/sql/relational-databases/polybase/polybase-guide) para obtener una descripción completa y sus capacidades.

> [!NOTE]
> APS actualmente solo admite el estándar de uso general v1 con redundancia local (LRS) de Azure Blob Storage.

## <a name="features-and-limitations"></a>Características y limitaciones
Consulte [características y limitaciones](https://docs.microsoft.com/sql/relational-databases/polybase/polybase-versioned-feature-summary) para un resumen de PolyBase presenta limitaciones conocidas y disponibles en los puntos de acceso y otros productos de SQL Server.

> [!NOTE] 
> El resto de PolyBase relacionados con artículos describen cómo configurar PolyBase (AU6) de APS 2016 y versiones posteriores.

## <a name="see-also"></a>Vea también
- [Hadoop](polybase-configure-hadoop.md)
- [Azure Blob Storage](polybase-configure-azure-blob-storage.md)
<!-- MISSING LINKS [PolyBase &#40;SQL Server PDW&#41;](../sqlpdw/polybase-sql-server-pdw.md)  -->  
  
