---
title: Procesamiento de consultas inteligente en bases de datos de Microsoft SQL | Microsoft Docs
description: Características de procesamiento de consultas inteligente para mejorar el rendimiento de las consultas en SQL Server y Azure SQL Database.
ms.custom: ''
ms.date: 05/22/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.suite: sql
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords: ''
ms.assetid: ''
author: joesackmsft
ms.author: josack
manager: craigg
monikerRange: = azuresqldb-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 7786fd048f1698c90f379450b31e0bac3457706e
ms.sourcegitcommit: b5ab9f3a55800b0ccd7e16997f4cd6184b4995f9
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/23/2018
ms.locfileid: "34455775"
---
# <a name="intelligent-query-processing-in-sql-databases"></a>Procesamiento de consultas inteligente en bases de datos SQL
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-xx-asdb-xxxx-xxx-md.md)]

La familia de características de **procesamiento de consultas inteligente** contiene características con un gran impacto que mejoran el rendimiento de las cargas de trabajo existentes con un esfuerzo de implementación mínimo.   Esto incluye mejoras de construcciones preexistentes, así como la introducción de métodos y capacidades adaptables.  

## <a name="adaptive-query-processing"></a>Procesamiento de consultas adaptable
Dentro de la familia de características de procesamiento de consultas inteligente se encuentra la familia de características de procesamiento de consultas adaptable, introducida en SQL Server 2017 y en Azure SQL Database, que incorpora nuevas capacidades de procesamiento de consultas que adaptan las estrategias de optimización a las condiciones de tiempo de ejecución de la carga de trabajo de sus aplicaciones:
- **Combinaciones adaptables del modo por lotes**. Esta característica permite cambiar su plan de forma dinámica a una mejor estrategia de combinación durante la ejecución mediante un único plan almacenado en caché.
- **Comentarios de concesión de memoria de modo de proceso por lotes**. Esta característica recalcula la memoria real necesaria para una consulta y actualiza el valor de la concesión del plan almacenado en caché, con lo que se reducen las concesiones de memoria excesivas que afectan a la simultaneidad y se corrigen concesiones de memoria subestimadas que provocan desbordamientos costosos en el disco.
- **Ejecución intercalada de funciones con valores de tabla de múltiples instrucciones (MSTVF)**. Con la ejecución intercalada se usan los recuentos de filas reales de la función para tomar decisiones fundamentadas sobre los planes de consulta descendentes. 

Para más información sobre el procesamiento de consultas adaptable, consulte el [procesamiento de consultas adaptable en las bases de datos SQL](../../relational-databases/performance/adaptive-query-processing.md).

## <a name="see-also"></a>Vea también
[Performance Center for SQL Server Database Engine and Azure SQL Database](../../relational-databases/performance/performance-center-for-sql-server-database-engine-and-azure-sql-database.md)    (Centro de rendimiento para el motor de base de datos SQL Server y Azure SQL Database)  
[Query Processing Architecture Guide](../../relational-databases/query-processing-architecture-guide.md)   (Guía de arquitectura de procesamiento de consultas)  
[Referencia de operadores lógicos y físicos del plan de presentación](../../relational-databases/showplan-logical-and-physical-operators-reference.md)    
[Combinaciones](../../relational-databases/performance/joins.md)    
[Demostración del procesamiento de consultas adaptable](https://github.com/joesackmsft/Conferences/blob/master/Data_AMP_Detroit_2017/Demos/AQP_Demo_ReadMe.md)        
