---
title: "Resumen de características de PolyBase con versiones | Microsoft Docs"
ms.custom: 
ms.date: 08/29/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-data-warehouse, pdw
ms.service: 
ms.component: polybase
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 6591994d-6109-4285-9c5b-ecb355f8a111
caps.latest.revision: 
author: barbkess
ms.author: barbkess
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: ff2d8cb28ff4d1ae4960d183ce73524ecf24d7d3
ms.sourcegitcommit: ab25b08a312d35489a2c4a6a0d29a04bbd90f64d
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 03/08/2018
---
# <a name="polybase-versioned-feature-summary"></a>Resumen de características de PolyBase con versiones
[!INCLUDE[appliesto-ss2016-asdb-asdw-pdw-md](../../includes/tsql-appliesto-ss2016-all-md.md)]
Resumen de las características de PolyBase disponibles para los servicios y productos de SQL Server.  
  
## <a name="feature-summary-for-product-releases"></a>Resumen de las características para cada versión del producto  
 En esta tabla se resumen las características fundamentales de PolyBase y los productos en los que están disponibles.  
  
||||||
|-|-|-|-|-|   
|**Característica**|**SQL Server 2016**|**Azure SQL Database**|**Azure SQL Data Warehouse**|**Almacenamiento de datos paralelos**| 
|Consultar datos de Hadoop con [!INCLUDE[tsql](../../includes/tsql-md.md)]|sí|no|no|sí|
|Importar datos desde Hadoop|sí|no|no|sí|
|Exportar datos a Hadoop  |sí|no|no| sí|
|Consultas, importación y exportación en HDInsight |no|no|no|no
|Aplicar cálculos de consulta a Hadoop|sí|no|no|sí|  
|Importar datos desde el almacenamiento de blobs de Azure|sí|no|sí|sí| 
|Exportar datos al almacenamiento de blobs de Azure|sí|no|sí|sí|  
|Importar datos de Azure Data Lake Store|no|no|sí|no|    
|Exportar datos de Azure Data Lake Store|no|no|sí|no|
|Ejecutar consultas de PolyBase desde las herramientas de BI de Microsoft|sí|no|sí|sí|   


## <a name="pushdown-computation-supported-t-sql-operators"></a>Operadores T-SQL compatibles con el cálculo de aplicación
En SQL Server y APS, no todos los operadores T-SQL se pueden aplicar al clúster de Hadoop. En la tabla siguiente se muestran todos los operadores admitidos y un subconjunto de los operadores no admitidos. 

||||
|-|-|-| 
|**Tipo de operador**|**Aplicable a Hadoop**|**Aplicable a Blob Storage**|
|Proyecciones de columna|sí|no|
|Predicados|sí|no|
|Agregados|parcialmente|no|
|Combinaciones entre tablas externas|no|no|
|Combinaciones entre tablas externas y tablas locales|no|no|
|Ordenaciones|no|no|

Por "agregación parcial" se entiende que se debe producir una agregación final cuando los datos lleguen a SQL Server, pero una parte de la agregación tiene lugar en Hadoop. Se trata de un método común para calcular agregaciones en los sistemas de procesamiento paralelo masivo.  
## <a name="see-also"></a>Ver también  
 [Guía de PolyBase](../../relational-databases/polybase/polybase-guide.md)  
  
  
