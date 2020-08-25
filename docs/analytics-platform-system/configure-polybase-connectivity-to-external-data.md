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
ms.openlocfilehash: 98527bf770da61c98368171e75b3a9b82ceba13c
ms.sourcegitcommit: 7345e4f05d6c06e1bcd73747a4a47873b3f3251f
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/24/2020
ms.locfileid: "88767184"
---
# <a name="configure-polybase-connectivity"></a>Configuración de la conectividad de polybase
Polybase permite que el sistema de plataforma de análisis (APS) procese consultas de Transact-SQL que pueden leer y escribir datos en orígenes de datos externos. Las mismas consultas que tienen acceso a datos externos también pueden incluir tablas de relaciones en el APS. Esto le permite combinar datos de orígenes externos con datos relacionales de alto valor en las bases de datos de APS.

![PolyBase lógico](media/polybase/polybase-logical.png)

Polybase en APS admite la lectura y escritura en el sistema de archivos de Hadoop (HDFS) y Azure Blob Storage. Polybase también tiene la capacidad de introducir algún cálculo en los nodos de Hadoop como trabajos de MapReduce para optimizar el rendimiento general de las consultas. Polybase en APS puede operar en archivos de texto delimitado, ORC y parquet. Vea [Qué es polybase](../relational-databases/polybase/polybase-guide.md) para obtener una descripción completa y sus funcionalidades.

> [!NOTE]
> APS actualmente solo admite el Azure Blob Storage estándar de uso general (LRS) con redundancia local.

## <a name="features-and-limitations"></a>Características y limitaciones
Vea [características y limitación](../relational-databases/polybase/polybase-versioned-feature-summary.md) para obtener un resumen de las características de polybase disponibles y las limitaciones conocidas de los AP y otros productos de SQL Server.

> [!NOTE] 
> En el resto de los artículos relacionados con polybase se describen cómo configurar polybase en APS 2016 (AU6) y versiones posteriores.

## <a name="see-also"></a>Consulte también
- [Hadoop](polybase-configure-hadoop.md)
- [Azure Blob Storage](polybase-configure-azure-blob-storage.md)
<!-- MISSING LINKS [PolyBase &#40;SQL Server PDW&#41;](../sqlpdw/polybase-sql-server-pdw.md)  -->  
