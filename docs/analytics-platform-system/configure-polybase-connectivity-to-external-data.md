---
title: Configuración de la conectividad de polybase
description: Explica cómo configurar polybase en el almacenamiento de datos paralelos para conectarse a orígenes de datos de Hadoop o de almacenamiento de Microsoft Azure BLOB externos. Use polybase para ejecutar consultas que integren datos de varios orígenes, como Hadoop, Azure BLOB Storage y almacenamiento de datos paralelos.
author: mzaman1
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.custom: seo-dt-2019
ms.openlocfilehash: 3b754fb2de33a230bc7d27f239b2778d2849fd5a
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/27/2020
ms.locfileid: "74401277"
---
# <a name="what-is-polybase"></a>¿Qué es PolyBase?
Polybase permite que el sistema de plataforma de análisis (APS) procese consultas de Transact-SQL que pueden leer y escribir datos en orígenes de datos externos. Las mismas consultas que tienen acceso a datos externos también pueden incluir tablas de relaciones en el APS. Esto le permite combinar datos de orígenes externos con datos relacionales de alto valor en las bases de datos de APS.

![PolyBase lógico](media/polybase/polybase-logical.png)

Polybase en APS admite la lectura y escritura en el sistema de archivos de Hadoop (HDFS) y Azure Blob Storage. Polybase también tiene la capacidad de introducir algún cálculo en los nodos de Hadoop como trabajos de MapReduce para optimizar el rendimiento general de las consultas. Polybase en APS puede operar en archivos de texto delimitado, ORC y parquet. Vea [Qué es polybase](https://docs.microsoft.com/sql/relational-databases/polybase/polybase-guide) para obtener una descripción completa y sus funcionalidades.

> [!NOTE]
> APS actualmente solo admite el Azure Blob Storage estándar de uso general (LRS) con redundancia local.

## <a name="features-and-limitations"></a>Características y limitaciones
Vea [características y limitación](https://docs.microsoft.com/sql/relational-databases/polybase/polybase-versioned-feature-summary) para obtener un resumen de las características de polybase disponibles y las limitaciones conocidas de los AP y otros productos de SQL Server.

> [!NOTE] 
> En el resto de los artículos relacionados con polybase se describen cómo configurar polybase en APS 2016 (AU6) y versiones posteriores.

## <a name="see-also"></a>Consulte también
- [Hadoop](polybase-configure-hadoop.md)
- [Azure Blob Storage](polybase-configure-azure-blob-storage.md)
<!-- MISSING LINKS [PolyBase &#40;SQL Server PDW&#41;](../sqlpdw/polybase-sql-server-pdw.md)  -->  
  
