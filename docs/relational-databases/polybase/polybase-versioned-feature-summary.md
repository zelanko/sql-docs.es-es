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
ms.openlocfilehash: 2052b098f0be7ab377cf38a36b896794d3caa07a
ms.sourcegitcommit: 8dccf20d48e8db8fe136c4de6b0a0b408191586b
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 10/09/2018
ms.locfileid: "48874353"
---
# <a name="polybase-features-and-limitations"></a>Características y limitaciones de PolyBase

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

## <a name="known-limitations"></a>Restricciones conocidas

PolyBase presenta las siguientes limitaciones:

- El tamaño máximo posible de fila, incluida la longitud total de las columnas de longitud variable, no puede superar los 32 KB en SQL Server o 1 MB en Azure SQL Data Warehouse.

- PolyBase no admite los tipos de datos de Hive 0.12+ (es decir, Char(), VarChar())

- Al exportar datos en un formato de archivo ORC desde SQL Server o Azure SQL Data Warehouse, las columnas pesadas de texto pueden limitarse a tan solo 50 columnas debido a errores de memoria insuficiente de Java. Para solucionar este problema, exporte solo un subconjunto de las columnas.

- No se pueden leer o escribir datos cifrados en reposo en Hadoop. Se incluyen las zonas cifradas de HDFS y el cifrado transparente.

- PolyBase no se puede conectar a una instancia de Hortonworks si KNOX está habilitado.

- Si usa tablas de Hive con el valor "transactional = true", PolyBase no podrá acceder a los datos del directorio de la tabla de Hive.

<!--SQL Server 2016-->
::: moniker range="= sql-server-2016 || =sqlallproducts-allversions"

- [PolyBase no se instala cuando se agrega un nodo a un clúster de conmutación por error de SQL Server 2016](https://support.microsoft.com/en-us/help/3173087/fix-polybase-feature-doesn-t-install-when-you-add-a-node-to-a-sql-server-2016-failover-cluster)

::: moniker-end
- No se admite la autenticación de integración. Por el momento solo se admiten el nombre de usuario y la contraseña.  
- El cifrado se habilita de forma predeterminada. Para deshabilitar el cifrado, debe... (hablar con thanh)
- [Limitaciones de asignación de tipos](polybase-type-mapping.md)


## <a name="security-and-authentication"></a>Autenticación y seguridad 

## <a name="see-also"></a>Ver también  

[Guía de PolyBase](../../relational-databases/polybase/polybase-guide.md)  
