---
title: Características y limitaciones de PolyBase | Microsoft Docs
ms.custom: ''
ms.date: 09/24/2018
ms.prod: sql
ms.technology: polybase
ms.reviewer: ''
ms.topic: conceptual
ms.assetid: 6591994d-6109-4285-9c5b-ecb355f8a111
author: rothja
ms.author: jroth
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: b2d02e13ea7ad1d74274f4412b6ab2bf476f452c
ms.sourcegitcommit: 9c6a37175296144464ffea815f371c024fce7032
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 11/15/2018
ms.locfileid: "51665430"
---
# <a name="polybase-features-and-limitations"></a>Características y limitaciones de PolyBase

[!INCLUDE[appliesto-ss2016-asdb-asdw-pdw-md](../../includes/tsql-appliesto-ss2016-all-md.md)]

Este artículo es un resumen de las características de PolyBase disponibles para los servicios y productos de SQL Server.  
  
## <a name="feature-summary-for-product-releases"></a>Resumen de características para las versiones de productos

En esta tabla se indican las características fundamentales de PolyBase y los productos en los que están disponibles.  
  
||||||
|-|-|-|-|-|   
|**Característica**|**SQL Server 2016**|**Azure SQL Database**|**Azure SQL Data Warehouse**|**Almacenamiento de datos paralelos**| 
|Consultar datos de Hadoop con [!INCLUDE[tsql](../../includes/tsql-md.md)]|Sí|no|no|Sí|
|Importar datos desde Hadoop|Sí|no|no|Sí|
|Exportar datos a Hadoop  |Sí|no|no| Sí|
|Consultar, importar desde y exportar a Azure HDInsight |no|no|no|no
|Aplicar cálculos de consulta a Hadoop|Sí|no|no|Sí|  
|Importar datos desde Azure Blob Storage|Sí|no|Sí|Sí| 
|Exportar datos a Azure Blob Storage|Sí|no|Sí|Sí|  
|Importar datos de Azure Data Lake Store|no|no|Sí|no|    
|Exportar datos de Azure Data Lake Store|no|no|Sí|no|
|Ejecutar consultas de PolyBase desde las herramientas de BI de Microsoft|Sí|no|Sí|Sí|   

## <a name="pushdown-computation-supported-by-t-sql-operators"></a>Cálculo de aplicación compatible con los operadores T-SQL

En SQL Server y APS, no todos los operadores T-SQL se pueden aplicar al clúster de Hadoop. En esta tabla se indican todos los operadores compatibles y un subconjunto de los operadores no admitidos. 

||||
|-|-|-| 
|**Tipo de operador**|**Aplicable a Hadoop**|**Aplicable a Blob Storage**|
|Proyecciones de columna|Sí|no|
|Predicados|Sí|no|
|Agregados|Parcial|no|
|Combinaciones entre tablas externas|no|no|
|Combinaciones entre tablas externas y tablas locales|no|no|
|Ordenaciones|no|no|

La agregación parcial significa que se debe producir una agregación final una vez que los datos lleguen a SQL Server. Pero una parte de la agregación se produce en Hadoop. Este método es habitual a la hora de calcular agregaciones en sistemas de procesamiento paralelo masivo.  

## <a name="known-limitations"></a>Restricciones conocidas

PolyBase presenta las siguientes limitaciones:

- El tamaño máximo posible de fila, que incluye la longitud total de las columnas de longitud variable, no puede superar los 32 KB en SQL Server ni 1 MB en Azure SQL Data Warehouse.

- Cuando se exportan los datos a un formato de archivo ORC desde SQL Server o SQL Data Warehouse, las columnas de texto intensivo podrían limitarse. Se pueden limitar a tan solo 50 columnas debido a los mensajes de error de memoria insuficiente de Java. Para solucionar este problema, exporte solo un subconjunto de las columnas.

- PolyBase no se puede conectar a una instancia de Hortonworks si Knox está habilitado.

- Si usa tablas de Hive con "transactional = true", PolyBase no puede acceder a los datos del directorio de tablas de Hive.

<!--SQL Server 2016-->
::: moniker range="= sql-server-2016 || =sqlallproducts-allversions"

- [PolyBase no se instala cuando se agrega un nodo a un clúster de conmutación por error de SQL Server 2016](https://support.microsoft.com/help/3173087/fix-polybase-feature-doesn-t-install-when-you-add-a-node-to-a-sql-server-2016-failover-cluster).

::: moniker-end

## <a name="next-steps"></a>Pasos siguientes

Para obtener más información sobre PolyBase, consulte [¿Qué es PolyBase?](polybase-guide.md)
