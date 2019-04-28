---
title: Propiedades OLAP de Analysis Services | Microsoft Docs
ms.date: 03/15/2019
ms.prod: sql
ms.technology: analysis-services
ms.custom: ''
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 8e2643488710548b3a773730e9b9898125783dc3
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "62714592"
---
# <a name="olap-properties"></a>Propiedades OLAP
[!INCLUDE[ssas-appliesto-sqlas-all-aas](../../includes/ssas-appliesto-sqlas-all-aas.md)]

  [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] admite las propiedades de servidor OLAP enumeradas en las tablas siguientes. Para obtener más información sobre otras propiedades de servidor y cómo establecerlas, vea [Configurar las propiedades de servidor en Analysis Services](../../analysis-services/server-properties/server-properties-in-analysis-services.md).  
  
 **Se aplica a:** Modo de servidor multidimensional únicamente  
  
## <a name="memory"></a>Memoria  
 **DefaultPageSizeForData**  
 Una propiedad avanzada que no debería cambiar, salvo a petición de expertos en soporte técnico de [!INCLUDE[msCoName](../../includes/msconame-md.md)] .  
  
 **DefaultPageSizeForDataHeader**  
 Una propiedad avanzada que no debería cambiar, salvo a petición de expertos en soporte técnico de [!INCLUDE[msCoName](../../includes/msconame-md.md)] .  
  
 **DefaultPageSizeForIndex**  
 Una propiedad avanzada que no debería cambiar, salvo a petición de expertos en soporte técnico de [!INCLUDE[msCoName](../../includes/msconame-md.md)] .  
  
 **DefaultPageSizeForIndexHeader**  
 Una propiedad avanzada que no debería cambiar, salvo a petición de expertos en soporte técnico de [!INCLUDE[msCoName](../../includes/msconame-md.md)] .  
  
 **DefaultPageSizeForString**  
 Una propiedad avanzada que no debería cambiar, salvo a petición de expertos en soporte técnico de [!INCLUDE[msCoName](../../includes/msconame-md.md)] .  
  
 **DefaultPageSizeForHash**  
 Una propiedad avanzada que no debería cambiar, salvo a petición de expertos en soporte técnico de [!INCLUDE[msCoName](../../includes/msconame-md.md)] .  
  
 **DefaultPageSizeForProp**  
 Una propiedad avanzada que no debería cambiar, salvo a petición de expertos en soporte técnico de [!INCLUDE[msCoName](../../includes/msconame-md.md)] .  
  
## <a name="lazyprocessing"></a>LazyProcessing  
 **Enabled**  
 Una propiedad booleana que especifica si está habilitado el procesamiento de agregaciones diferidas.  
  
 **SleepIntervalSecs**  
 Una propiedad de entero de 32 bits con signo que define el intervalo, en segundos, durante el que el servidor comprueba si hay trabajos de procesamiento diferido pendientes.  
  
 **MaxCPUUsage**  
 Una propiedad de número de punto flotante de doble precisión de 64 bits con signo que define el uso máximo de la CPU para procesamiento diferido, expresado en forma de porcentaje. El servidor supervisa el uso medio de la CPU basándose en instantáneas. Por encima de este umbral es normal que la CPU no funcione.  
  
 El valor predeterminado para esta propiedad es 0.5, que indica que un máximo del 50% de la CPU se destinará a procesamiento diferido.  
  
 **MaxObjectsInParallel**  
 Una propiedad de entero de 32 bits con signo que especifica el máximo de particiones que se pueden procesar de forma diferida en paralelo.  
  
 **MaxRetries**  
 Una propiedad de entero de 32 bits con signo que define el número de veces que el procesamiento diferido puede intentarse antes de que se produzca un error.  
  
## <a name="processplan"></a>ProcessPlan  
 **CacheRowsetRows**  
 Una propiedad avanzada que no debería cambiar, salvo a petición de expertos en soporte técnico de [!INCLUDE[msCoName](../../includes/msconame-md.md)] .  
  
 **CacheRowsetToDisk**  
 Una propiedad avanzada que no debería cambiar, salvo a petición de expertos en soporte técnico de [!INCLUDE[msCoName](../../includes/msconame-md.md)] .  
  
 **DistinctBuffer**  
 Una propiedad de entero de 32 bits con signo que define el tamaño de un búfer interno para recuentos diferentes. Aumente este valor para acelerar el procesamiento de recuentos distintos a costa de usar memoria.  
  
 **EnableRolapDimQueryTableGrouping**  
 Una propiedad booleana que especifica si el agrupamiento de tablas está habilitado para dimensiones ROLAP. Si es True, al consultar las dimensiones ROLAP en tiempo de ejecución, todas las tablas de dimensiones ROLAP se consultarán a la vez, en lugar de separar las consultas de cada atributo.  
  
 **EnableTableGrouping**  
 Una propiedad booleana que especifica si está habilitado el agrupamiento de tablas. Si es True, al procesar las dimensiones, todas las tablas de dimensiones se consultarán a la vez, en lugar de separar las consultas de cada atributo.  
  
 **ForceMultiPass**  
 Una propiedad avanzada que no debería cambiar, salvo a petición de expertos en soporte técnico de [!INCLUDE[msCoName](../../includes/msconame-md.md)] .  
  
 **MaxTableDepth**  
 Una propiedad avanzada que no debería cambiar, salvo a petición de expertos en soporte técnico de [!INCLUDE[msCoName](../../includes/msconame-md.md)] .  
  
 **MemoryAdjustConst**  
 Una propiedad avanzada que no debería cambiar, salvo a petición de expertos en soporte técnico de [!INCLUDE[msCoName](../../includes/msconame-md.md)] .  
  
 **MemoryAdjustFactor**  
 Una propiedad avanzada que no debería cambiar, salvo a petición de expertos en soporte técnico de [!INCLUDE[msCoName](../../includes/msconame-md.md)] .  
  
 **MemoryLimit**  
 Una propiedad de número de punto flotante de doble precisión de 64 bits con signo que define el máximo de memoria que se destinará a procesamiento, expresado en forma de porcentaje de memoria física.  
  
 El valor predeterminado para esta propiedad es 65, lo que indica que el 65% de la memoria física puede estar dedicado a procesamiento de dimensiones o cubos.  
  
 **MemoryLimitErrorEnabled**  
 Una propiedad avanzada que no debería cambiar, salvo a petición de expertos en soporte técnico de [!INCLUDE[msCoName](../../includes/msconame-md.md)] .  
  
 **OptimizeSchema**  
 Una propiedad avanzada que no debería cambiar, salvo a petición de expertos en soporte técnico de [!INCLUDE[msCoName](../../includes/msconame-md.md)] .  
  
## <a name="proactivecaching"></a>ProactiveCaching  
 **DefaultRefreshInterval**  
 Una propiedad avanzada que no debería cambiar, salvo a petición de expertos en soporte técnico de [!INCLUDE[msCoName](../../includes/msconame-md.md)] .  
  
 **DimensionLatencyAccuracy**  
 Una propiedad avanzada que no debería cambiar, salvo a petición de expertos en soporte técnico de [!INCLUDE[msCoName](../../includes/msconame-md.md)] .  
  
 **PartitionLatencyAccuracy**  
 Una propiedad avanzada que no debería cambiar, salvo a petición de expertos en soporte técnico de [!INCLUDE[msCoName](../../includes/msconame-md.md)] .  
  
## <a name="process"></a>Procesar  
 **AggregationMemoryLimitMax**  
 Una propiedad de número de punto flotante de doble precisión de 64 bits con signo que define el máximo de memoria que se puede destinar a procesamiento, expresado en forma de porcentaje de memoria física.  
  
 El valor predeterminado para esta propiedad es 80, lo que indica que el 80% de la memoria física puede estar dedicado a procesamiento de agregaciones.  
  
 **AggregationMemoryLimitMin**  
 Una propiedad de número de punto flotante de doble precisión de 64 bits con signo que define el mínimo de memoria que se puede destinar a procesamiento, expresado en forma de porcentaje de memoria física. Un valor más grande puede acelerar el procesamiento de agregaciones a costa de usar memoria.  
  
 El valor predeterminado para esta propiedad es 10, lo que indica que al menos el 10% de la memoria física estará dedicado a procesamiento de agregaciones.  
  
 **AggregationNewAlgo**  
 Una propiedad avanzada que no debería cambiar, salvo a petición de expertos en soporte técnico de [!INCLUDE[msCoName](../../includes/msconame-md.md)] .  
  
 **AggregationPerfLog2**  
 Una propiedad avanzada que no debería cambiar, salvo a petición de expertos en soporte técnico de [!INCLUDE[msCoName](../../includes/msconame-md.md)] .  
  
 **AggregationsBuildEnabled**  
 Una propiedad booleana que especifica si está habilitada la generación de agregaciones. Se trata de un mecanismo para realizar pruebas comparativas de la generación de agregaciones sin cambiar el diseño de las mismas.  
  
 **BufferMemoryLimit**  
 Una propiedad de número de punto flotante de doble precisión de 64 bits con signo que define el límite de memoria de búfer de procesamiento, expresado en forma de porcentaje de memoria física.  
  
 El valor predeterminado para esta propiedad es 60, lo que indica que se puede utilizar hasta el 60% de la memoria física para la memoria de búfer.  
  
 **BufferRecordLimit**  
 Una propiedad de entero de 32 bits con signo que define el número de registros que se pueden almacenar en el búfer durante el procesamiento.  
  
 El valor predeterminado para esta propiedad es 1048576 (registros).  
  
 **CacheRecordLimit**  
 Una propiedad avanzada que no debería cambiar, salvo a petición de expertos en soporte técnico de [!INCLUDE[msCoName](../../includes/msconame-md.md)] .  
  
 **CheckDistinctRecordSortOrder**  
 Una propiedad booleana que define si el criterio de ordenación de los resultados de una consulta de recuento distinto tienen sentido al procesar particiones. True indica que el criterio de ordenación no tiene sentido y debe ser "comprobado" por el servidor. Al procesar particiones con medidas de recuento distintivas, consulta enviada a SQL con "order by". Establézcala en False para acelerar el procesamiento.  
  
 El valor predeterminado de esta propiedad es True, que indica que el criterio de ordenación no tiene sentido y debe comprobarse.  
  
 **DatabaseConnectionPoolConnectTimeout**  
 Una propiedad de entero de 32 bits con signo que especifica el tiempo de espera que se tarda en abrir una nueva conexión, expresado en segundos.  
  
 **DatabaseConnectionPoolGeneralTimeout**  
 Una propiedad de entero de 32 bits con signo que especifica el tiempo de espera de conexión de la base de datos que se utiliza con conexiones OLEDB externas, expresado en segundos.  
  
 **DatabaseConnectionPoolMax**  
 Una propiedad de entero de 32 bits con signo que especifica el máximo de conexiones agrupadas de base de datos.  
  
 El valor predeterminado para esta propiedad es 50 (conexiones).  
  
 **DatabaseConnectionPoolTimeout**  
 Una propiedad avanzada que no debería cambiar, salvo a petición de expertos en soporte técnico de [!INCLUDE[msCoName](../../includes/msconame-md.md)] .  
  
 **DataFileInitEnabled**  
 Una propiedad avanzada que no debería cambiar, salvo a petición de expertos en soporte técnico de [!INCLUDE[msCoName](../../includes/msconame-md.md)] .  
  
 **DataPlacementOptimization**  
 Una propiedad avanzada que no debería cambiar, salvo a petición de expertos en soporte técnico de [!INCLUDE[msCoName](../../includes/msconame-md.md)] .  
  
 **DataSliceInitEnabled**  
 Una propiedad avanzada que no debería cambiar, salvo a petición de expertos en soporte técnico de [!INCLUDE[msCoName](../../includes/msconame-md.md)] .  
  
 **DeepCompressValue**  
 Una propiedad booleana que se aplica a medidas con datos de tipo doble que especifica si se pueden comprimir los números, lo que produce una pérdida en precisión numérica. Un valor Fase indica que no hay compresión ni pérdida de precisión.  
  
 El valor predeterminado para esta propiedad es True, que indica que la compresión está habilitada y que se perderá la precisión.  
  
 **DimensionPropertyKeyCache**  
 Una propiedad booleana que especifica si las claves de la propiedad de dimensión están almacenadas en caché. Debe establecerse en True si las claves no son únicas.  
  
 **IndexBuildEnabled**  
 Una propiedad booleana que especifica si se generan índices al procesar. Esta propiedad sirve para realizar pruebas comparativas y con fines informativos.  
  
 **IndexBuildThreshold**  
 Una propiedad de entero de 32 bits con signo que especifica un umbral de recuento de filas por debajo del cual no se generarán índices para las particiones.  
  
 El valor predeterminado para esta propiedad es 4096 (filas).  
  
 **IndexFileInitEnabled**  
 Una propiedad avanzada que no debería cambiar, salvo a petición de expertos en soporte técnico de [!INCLUDE[msCoName](../../includes/msconame-md.md)] .  
  
 **MapFormatMask**  
 Una propiedad avanzada que no debería cambiar, salvo a petición de expertos en soporte técnico de [!INCLUDE[msCoName](../../includes/msconame-md.md)] .  
  
 **RecordsReportGranularity**  
 Una propiedad de entero de 32 bits con signo que especifica la frecuencia con la que el servidor registra los eventos de seguimiento durante el procesamiento, en filas.  
  
 El valor predeterminado para esta propiedad es 1000, que indica que se registra un evento de seguimiento una vez cada 1000 filas.  
  
 **ROLAPDimensionProcessingEffort**  
 Una propiedad avanzada que no debería cambiar, salvo a petición de expertos en soporte técnico de [!INCLUDE[msCoName](../../includes/msconame-md.md)] .  
  
## <a name="query"></a>Consultar  
 **AggregationsUseEnabled**  
 Una propiedad booleana que define si se utilizan agregaciones almacenadas en el tiempo de ejecución. Esta propiedad permite deshabilitar las agregaciones sin cambiar el diseño de la agregación y sin necesidad de repetir el procesamiento. Sirve para realizar pruebas comparativas y con fines informativos.  
  
 El valor predeterminado para esta propiedad es True, que indica que las agregaciones están habilitadas.  
  
 **AllowSEFiltering**  
 Una propiedad avanzada que no debería cambiar, salvo a petición de expertos en soporte técnico de [!INCLUDE[msCoName](../../includes/msconame-md.md)] .  
  
 **CalculationCacheRegistryMaxIterations**  
 Una propiedad avanzada que no debería cambiar, salvo a petición de expertos en soporte técnico de [!INCLUDE[msCoName](../../includes/msconame-md.md)] .  
  
 **CalculationEvaluationPolicy**  
 Una propiedad avanzada que no debería cambiar, salvo a petición de expertos en soporte técnico de [!INCLUDE[msCoName](../../includes/msconame-md.md)] .  
  
 **ConvertDeletedToUnknown**  
 Una propiedad booleana que especifica si los miembros de dimensión eliminada se convierten en miembro desconocido.  
  
 **CopyLinkedDataCacheAndRegistry**  
 Una propiedad avanzada que no debería cambiar, salvo a petición de expertos en soporte técnico de [!INCLUDE[msCoName](../../includes/msconame-md.md)] .  
  
 **DataCacheRegistryMaxIterations**  
 Una propiedad avanzada que no debería cambiar, salvo a petición de expertos en soporte técnico de [!INCLUDE[msCoName](../../includes/msconame-md.md)] .  
  
 **DefaultDrillthroughMaxRows**  
 Una propiedad de entero de 32 bits con signo que especifica el máximo de filas que devolverá una consulta de obtención de detalles.  
  
 El valor predeterminado para esta propiedad es 10000 (filas).  
  
 **DimensionPropertyCacheSize**  
 Una propiedad de entero de 32 bits con signo que especifica la cantidad de memoria (en bytes) utilizada para almacenar en memoria caché miembros de dimensión que se utilizan en una consulta.  
  
 El valor predeterminado es 4.000.000 bytes (o 4 MB) por jerarquía de atributo, por consulta activa. El valor predeterminado proporciona un tamaño de caché equilibrado para las soluciones que tienen jerarquías típicas. Sin embargo, las dimensiones con un gran número de miembros (varios millones) o jerarquías profundas funcionan mejor si se aumenta este valor.  
  
 Implicaciones de aumentar el tamaño de la memoria caché:  
  
-   Los costos de utilización de memoria aumentan cuando se permite que la caché de dimensión utilice más memoria. El uso real depende de la ejecución de consultas. No todas las consultas utilizarán el máximo permitido.  
  
     Tenga en cuenta que la memoria utilizada por estas memorias caché se considera no reducible y se incluirá en el valor de **TotalMemoryLimit**.  
  
-   Afecta a todas las bases de datos del servidor. **DimensionPropertyCachesize** es una propiedad de todo el servidor. El cambio de esta propiedad afecta a todas las bases de datos que se ejecutan en la instancia actual.  
  
Enfoque para calcular los requisitos de memoria caché de dimensión:  
  
1.  Empiece aumentando mucho el tamaño para determinar si hay alguna ventaja en aumentar el tamaño de memoria caché de dimensión. Por ejemplo, puede duplicar el valor predeterminado como paso inicial.  
  
2.  Si hay una mejora del rendimiento evidente, reduzca incrementalmente el valor hasta que se alcance un equilibrio entre el rendimiento y la utilización de memoria.  


 **ExpressNonEmptyUseEnabled**  
 Una propiedad avanzada que no debería cambiar, salvo a petición de expertos en soporte técnico de [!INCLUDE[msCoName](../../includes/msconame-md.md)] .  
  
 **IgnoreNullRolapRows**  
 Una propiedad avanzada que no debería cambiar, salvo a petición de expertos en soporte técnico de [!INCLUDE[msCoName](../../includes/msconame-md.md)] .  
  
 **IndexUseEnabled**  
 Una propiedad booleana que define si se utilizan índices en el tiempo de ejecución. Esta propiedad sirve para realizar pruebas comparativas y con fines informativos.  
  
 **MapHandleAlgorithm**  
 Una propiedad avanzada que no debería cambiar, salvo a petición de expertos en soporte técnico de [!INCLUDE[msCoName](../../includes/msconame-md.md)] .  
  
 **MaxRolapOrConditions**  
 Una propiedad avanzada que no debería cambiar, salvo a petición de expertos en soporte técnico de [!INCLUDE[msCoName](../../includes/msconame-md.md)] .  
 
 **RowsetSerializationLimit**   
 Se aplica a Azure Analysis Services. Limita el número de filas devueltas en un conjunto de filas a los clientes. Valor predeterminado es -1, lo que significa que no hay ningún límite se aplica. Se aplica a las consultas DAX y MDX. Puede usar para proteger los recursos del servidor de exportación de todos los datos. Las consultas enviadas al servidor que superan el límite se cancelan y se devuelve un error.  

 **UseCalculationCacheRegistry**  
 Una propiedad avanzada que no debería cambiar, salvo a petición de expertos en soporte técnico de [!INCLUDE[msCoName](../../includes/msconame-md.md)] .  
  
 **UseDataCacheFreeLastPageMemory**  
 Una propiedad avanzada que no debería cambiar, salvo a petición de expertos en soporte técnico de [!INCLUDE[msCoName](../../includes/msconame-md.md)] .  
  
 **UseDataCacheRegistry**  
 Una propiedad booleana que especifica si habilitar el Registro en caché de los datos, donde se almacenan en caché los resultados de las consultas (aunque no los resultados calculados).  
  
 **UseDataCacheRegistryHashTable**  
 Una propiedad avanzada que no debería cambiar, salvo a petición de expertos en soporte técnico de [!INCLUDE[msCoName](../../includes/msconame-md.md)] .  
  
 **UseDataCacheRegistryMultiplyKey**  
 Una propiedad avanzada que no debería cambiar, salvo a petición de expertos en soporte técnico de [!INCLUDE[msCoName](../../includes/msconame-md.md)] .  
  
 **UseDataSlice**  
 Una propiedad booleana que define si se utilizan segmentos de datos de partición en tiempo de ejecución para la optimización de consultas. Esta propiedad sirve para realizar pruebas comparativas y con fines informativos.  
  
 **UseMaterializedIterators**  
 Una propiedad avanzada que no debería cambiar, salvo a petición de expertos en soporte técnico de [!INCLUDE[msCoName](../../includes/msconame-md.md)] .  
  
 **UseSinglePassForDimSecurityAutoExist**  
 Una propiedad avanzada que no debería cambiar, salvo a petición de expertos en soporte técnico de [!INCLUDE[msCoName](../../includes/msconame-md.md)] .  
  
 **UseVBANet**  
 Una propiedad booleana que define si se utiliza el ensamblado .net de VBA para funciones definidas por el usuario.  
  
 **CalculationPrefetchLocality\ApplyIntersect**  
 Una propiedad avanzada que no debería cambiar, salvo a petición de expertos en soporte técnico de [!INCLUDE[msCoName](../../includes/msconame-md.md)] .  
  
 **CalculationPrefetchLocality\ApplySubtract**  
 Una propiedad avanzada que no debería cambiar, salvo a petición de expertos en soporte técnico de [!INCLUDE[msCoName](../../includes/msconame-md.md)] .  
  
 **CalculationPrefetchLocality\PrefetchLowerGranularities**  
 Una propiedad avanzada que no debería cambiar, salvo a petición de expertos en soporte técnico de [!INCLUDE[msCoName](../../includes/msconame-md.md)] .  
  
 **DataCache\CachedPageAlloc\Income**  
 Una propiedad avanzada que no debería cambiar, salvo a petición de expertos en soporte técnico de [!INCLUDE[msCoName](../../includes/msconame-md.md)] .  
  
 **DataCache\CachedPageAlloc\InitialBonus**  
 Una propiedad avanzada que no debería cambiar, salvo a petición de expertos en soporte técnico de [!INCLUDE[msCoName](../../includes/msconame-md.md)] .  
  
 **DataCache\CachedPageAlloc\MaximumBalance**  
 Una propiedad avanzada que no debería cambiar, salvo a petición de expertos en soporte técnico de [!INCLUDE[msCoName](../../includes/msconame-md.md)] .  
  
 **DataCache\CachedPageAlloc\MinimumBalance**  
 Una propiedad avanzada que no debería cambiar, salvo a petición de expertos en soporte técnico de [!INCLUDE[msCoName](../../includes/msconame-md.md)] .  
  
 **DataCache\CachedPageAlloc\Tax**  
 Una propiedad avanzada que no debería cambiar, salvo a petición de expertos en soporte técnico de [!INCLUDE[msCoName](../../includes/msconame-md.md)] .  
  
 **DataCache\CellStore\Income**  
 Una propiedad avanzada que no debería cambiar, salvo a petición de expertos en soporte técnico de [!INCLUDE[msCoName](../../includes/msconame-md.md)] .  
  
 **DataCache\CellStore\InitialBonus**  
 Una propiedad avanzada que no debería cambiar, salvo a petición de expertos en soporte técnico de [!INCLUDE[msCoName](../../includes/msconame-md.md)] .  
  
 **DataCache\CellStore\MaximumBalance**  
 Una propiedad avanzada que no debería cambiar, salvo a petición de expertos en soporte técnico de [!INCLUDE[msCoName](../../includes/msconame-md.md)] .  
  
 **DataCache\CellStore\MinimumBalance**  
 Una propiedad avanzada que no debería cambiar, salvo a petición de expertos en soporte técnico de [!INCLUDE[msCoName](../../includes/msconame-md.md)] .  
  
 **DataCache\CellStore\Tax**  
 Una propiedad avanzada que no debería cambiar, salvo a petición de expertos en soporte técnico de [!INCLUDE[msCoName](../../includes/msconame-md.md)] .  
  
 **DataCache\MemoryModel\Income**  
 Una propiedad avanzada que no debería cambiar, salvo a petición de expertos en soporte técnico de [!INCLUDE[msCoName](../../includes/msconame-md.md)] .  
  
 **DataCache\MemoryModel\InitialBonus**  
 Una propiedad avanzada que no debería cambiar, salvo a petición de expertos en soporte técnico de [!INCLUDE[msCoName](../../includes/msconame-md.md)] .  
  
 **DataCache\MemoryModel\MaximumBalance**  
 Una propiedad avanzada que no debería cambiar, salvo a petición de expertos en soporte técnico de [!INCLUDE[msCoName](../../includes/msconame-md.md)] .  
  
 **DataCache\MemoryModel\MinimumBalance**  
 Una propiedad avanzada que no debería cambiar, salvo a petición de expertos en soporte técnico de [!INCLUDE[msCoName](../../includes/msconame-md.md)] .  
  
 **DataCache\MemoryModel\Tax**  
 Una propiedad avanzada que no debería cambiar, salvo a petición de expertos en soporte técnico de [!INCLUDE[msCoName](../../includes/msconame-md.md)] .  
  
## <a name="jobs"></a>trabajos  
 **ProcessAggregation\MemoryModel\Income**  
 Una propiedad avanzada que no debería cambiar, salvo a petición de expertos en soporte técnico de [!INCLUDE[msCoName](../../includes/msconame-md.md)] .  
  
 **ProcessAggregation\MemoryModel\InitialBonus**  
 Una propiedad avanzada que no debería cambiar, salvo a petición de expertos en soporte técnico de [!INCLUDE[msCoName](../../includes/msconame-md.md)] .  
  
 **ProcessAggregation\MemoryModel\MaximumBalance**  
 Una propiedad avanzada que no debería cambiar, salvo a petición de expertos en soporte técnico de [!INCLUDE[msCoName](../../includes/msconame-md.md)] .  
  
 **ProcessAggregation\MemoryModel\MinimumBalance**  
 Una propiedad avanzada que no debería cambiar, salvo a petición de expertos en soporte técnico de [!INCLUDE[msCoName](../../includes/msconame-md.md)] .  
  
 **ProcessAggregation\MemoryModel\Tax**  
 Una propiedad avanzada que no debería cambiar, salvo a petición de expertos en soporte técnico de [!INCLUDE[msCoName](../../includes/msconame-md.md)] .  
  
 **ProcessAggregation\ProcessPartition\Income**  
 Una propiedad avanzada que no debería cambiar, salvo a petición de expertos en soporte técnico de [!INCLUDE[msCoName](../../includes/msconame-md.md)] .  
  
 **ProcessAggregation\ProcessPartition\InitialBonus**  
 Una propiedad avanzada que no debería cambiar, salvo a petición de expertos en soporte técnico de [!INCLUDE[msCoName](../../includes/msconame-md.md)] .  
  
 **ProcessAggregation\ProcessPartition\MaximumBalance**  
 Una propiedad avanzada que no debería cambiar, salvo a petición de expertos en soporte técnico de [!INCLUDE[msCoName](../../includes/msconame-md.md)] .  
  
 **ProcessAggregation\ProcessPartition\MinimumBalance**  
 Una propiedad avanzada que no debería cambiar, salvo a petición de expertos en soporte técnico de [!INCLUDE[msCoName](../../includes/msconame-md.md)] .  
  
 **ProcessAggregation\ProcessPartition\Tax**  
 Una propiedad avanzada que no debería cambiar, salvo a petición de expertos en soporte técnico de [!INCLUDE[msCoName](../../includes/msconame-md.md)] .  
  
 **ProcessAggregation\ProcessProperty\Income**  
 Una propiedad avanzada que no debería cambiar, salvo a petición de expertos en soporte técnico de [!INCLUDE[msCoName](../../includes/msconame-md.md)] .  
  
 **ProcessAggregation\ProcessProperty\InitialBonus**  
 Una propiedad avanzada que no debería cambiar, salvo a petición de expertos en soporte técnico de [!INCLUDE[msCoName](../../includes/msconame-md.md)] .  
  
 **ProcessAggregation\ProcessProperty\MaximumBalance**  
 Una propiedad avanzada que no debería cambiar, salvo a petición de expertos en soporte técnico de [!INCLUDE[msCoName](../../includes/msconame-md.md)] .  
  
 **ProcessAggregation\ProcessProperty\MinimumBalance**  
 Una propiedad avanzada que no debería cambiar, salvo a petición de expertos en soporte técnico de [!INCLUDE[msCoName](../../includes/msconame-md.md)] .  
  
 **ProcessAggregation\ProcessProperty\Tax**  
 Una propiedad avanzada que no debería cambiar, salvo a petición de expertos en soporte técnico de [!INCLUDE[msCoName](../../includes/msconame-md.md)] .  
  
## <a name="see-also"></a>Vea también  
 [Propiedades de servidor en Analysis Services](../../analysis-services/server-properties/server-properties-in-analysis-services.md)   
 [Determinar el modo de servidor de una instancia de Analysis Services](../../analysis-services/instances/determine-the-server-mode-of-an-analysis-services-instance.md)  
  
  
