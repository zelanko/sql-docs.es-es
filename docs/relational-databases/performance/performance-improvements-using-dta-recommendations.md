---
title: Mejoras de rendimiento con las recomendaciones de DTA | Microsoft Docs
ms.custom: 
ms.date: 03/07/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: performance
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- Database Engine Tuning Advisor, performance improvements
ms.assetid: 2e51ea06-81cb-4454-b111-da02808468e6
caps.latest.revision: 
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 935483efd524b85c24e11716c5499b25b81ff651
ms.sourcegitcommit: dcac30038f2223990cc21775c84cbd4e7bacdc73
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 01/18/2018
---
# <a name="performance-improvements-using-dta-recommendations"></a>Mejoras de rendimiento con las recomendaciones de DTA
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]


---
El rendimiento del almacenamiento de datos y las cargas de trabajo analíticas pueden beneficiarse de los índices de **almacén de columnas**, especialmente para las consultas que necesitan examinar tablas de gran tamaño. Los índices de **almacén de filas** (árbol B+) son más eficaces para las consultas que tienen acceso a cantidades relativamente pequeñas de datos que buscan un valor o un rango de valores determinados. Puesto que los índices de almacén de filas pueden entregar filas ordenadas, también pueden reducir el costo de ordenación en los planes de ejecución de consultas. Por lo tanto, la elección de la combinación de índices de almacén de columnas y de filas que se generará es dependiente de la carga de trabajo de la aplicación.

El Asistente para la optimización de motor de base de datos (DTA), a partir de SQL Server 2016, puede recomendar una **combinación adecuada de índices de almacén de columnas y de filas** al examinar una carga de trabajo de la base de datos determinada. 

Para demostrar las ventajas de las recomendaciones de DTA en el rendimiento de las cargas de trabajo, hemos probado varias cargas de trabajo de clientes reales. Para cada carga de trabajo de cliente, dejamos que DTA examinara las consultas individuales, así como la carga de trabajo completa de las consultas. Tuvimos en cuenta tres alternativas:
  
  1. **Solo el almacén de columnas**: genere solo los índices de almacén de columnas para todas las tablas sin utilizar DTA. 
  2. **DTA (solo el almacén de filas)**:ejecute DTA con la opción para recomendar solo los índices de almacén.
  3. **DTA (almacén de filas y de columnas)**: ejecute DTA con la opción recomendar índices de almacén de filas y de columnas.  
   
En cada caso, implementamos los índices recomendados. Informamos sobre el promedio de tiempo de CPU (en milisegundos) en varias ejecuciones de la consulta o la carga de trabajo. En la figura siguiente se traza el tiempo de CPU en milisegundos de las cargas de trabajo de dos bases de datos de cliente distintas. Tenga en cuenta que el eje y (tiempo de CPU) utiliza una escala logarítmica.   


![DTA-columnstore-rowstore-performance](../../relational-databases/performance/media/dta-columnstore-rowstore-performance.gif)



**Necesario para los diseños físicos mixtos**: el primer conjunto de barras correspondientes a la consulta 1 del cliente 1. DTA (almacén de filas y de columnas) recomienda un conjunto de 4 índices de columnas y 6 índices de almacén de filas, con lo que se obtiene un tiempo de CPU entre 2,5 y 4 veces inferior en comparación con solo el índice de almacén de columnas y DTA (solo el almacén de filas). Esto muestra las ventajas de los diseños físicos mixtos que constan de indices de almacén de filas y de columnas *incluso para una sola consulta*. 

**Eficacia de las recomendaciones de índices de almacén de filas**: el segundo y tercer conjunto de barras (correspondiente a la consulta 2 del cliente 1 y a la consulta del cliente 1 del cliente 2) son casos en los que las consultas tienen predicados de filtro selectivos que aprovechan los índices de almacén de filas adecuados. Para estas dos consultas, DTA (solo el almacén de filas) y DTA (almacén de filas y de columnas) recomienda solo los índices de almacén de filas. Estos ejemplos también demuestran que incluso cuando se invoca DTA con la opción para recomendar índices de almacén de columnas, el enfoque basado en costos garantiza que recomiende un índice de almacén solo si la carga de trabajo puede realmente beneficiarse de él.

**Eficacia de las recomendaciones de índices de almacén de columnas**: el cuarto conjunto de barras correspondiente a la consulta 2 del cliente 2 representa un caso en el que la consulta examina las tablas de gran tamaño que aprovecharían los índices de almacén de columnas. DTA (solo el almacén de filas) genera una recomendación cuyo tiempo de CPU es superior en comparación con cuando estaban los índices de almacén de columnas. DTA (almacén de filas y de columnas) recomienda los índices de almacén de columnas adecuados, con lo que los hace coincidir con el rendimiento de ejecución de consultas de la opción de solo el almacén de columnas.

**Eficacia de las recomendaciones para la carga de trabajo con varias consultas**: el conjunto final de barras correspondiente a la carga de trabajo completa del cliente 2 ejemplifica la capacidad de DTA para examinar varias consultas en la carga de trabajo con el objetivo de recomendar un conjunto apropiado de índices de almacén de columnas y de filas que pueda mejorar el costo de ejecución de la carga de trabajo general. DTA (almacén de filas y de columnas) recomienda 4 índices de almacén de columnas y decenas de índices de almacén de filas que dan lugar a través de una mejora de orden de magnitud de la carga de trabajo en comparación con la opción que crea solo los índices de almacén de columnas; y aproximadamente una mejora entre 4 y 5 veces superior en comparación con DTA (solo el almacén de filas).

En resumen, los ejemplos anteriores muestran la capacidad de DTA para aprovechar adecuadamente los índices de almacén de columnas y de filas compatibles en el motor de base de datos de SQL Server y recomienda una combinación adecuada de índices que puede reducir significativamente el tiempo de CPU para la carga de trabajo. 

<a name="see-also"></a>Ver también
---
[Asistente para la optimización de motor de base de datos](../../relational-databases/performance/database-engine-tuning-advisor.md)

[Recomendaciones de índice de almacén de columnas en el Asistente para la optimización de motor de base de datos (DTA)](../../relational-databases/performance/columnstore-index-recommendations-in-database-engine-tuning-advisor-dta.md)

[Guía de índices de almacén de columnas](~/relational-databases/indexes/columnstore-indexes-overview.md)

[Índices de almacén de columnas para el almacenamiento de datos](~/relational-databases/indexes/columnstore-indexes-data-warehouse.md)

[CREATE COLUMNSTORE INDEX (Transact-SQL)](../../t-sql/statements/create-columnstore-index-transact-sql.md)

[CREATE INDEX (Transact-SQL)](../../t-sql/statements/create-index-transact-sql.md)



