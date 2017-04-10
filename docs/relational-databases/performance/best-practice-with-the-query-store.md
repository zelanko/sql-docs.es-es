---
title: "Procedimiento recomendado con el Almac&#233;n de consultas | Microsoft Docs"
ms.custom: 
  - "SQL2016_New_Updated"
ms.date: "11/24/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "database-engine"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "Almacén de consultas, procedimientos recomendados"
ms.assetid: 5b13b5ac-1e4c-45e7-bda7-ebebe2784551
caps.latest.revision: 24
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 24
---
# Procedimiento recomendado con el Almac&#233;n de consultas
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

  En este tema se describen los procedimientos recomendados para usar el Almacén de consultas con la carga de trabajo.  
  
##  <a name="a-namessmsa-use-the-latest-sql-server-management-studio"></a><a name="SSMS"></a> Usar la versión más reciente de SQL Server Management Studio  
 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] tiene un conjunto de interfaces de usuario diseñadas para configurar el Almacén de consultas, así como para consumir datos recopilados sobre la carga de trabajo.  
Descargue la versión más reciente de [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] desde: [https://msdn.microsoft.com/library/mt238290.aspx](https://msdn.microsoft.com/library/mt238290.aspx)  
  
 Para obtener una descripción rápida sobre cómo usar el Almacén de consultas en escenarios de solución de problemas, vea los [blogs de @Azure del Almacén de consultas](https://azure.microsoft.com/en-us/blog/query-store-a-flight-data-recorder-for-your-database/).  
  
##  <a name="a-nameinsighta-use-query-performance-insight-in-azure-sql-database"></a><a name="Insight"></a> Uso de Información de rendimiento de consultas en Azure SQL Database  
 Si ejecuta el Almacén de consultas en [!INCLUDE[ssSDS](../../includes/sssds-md.md)] puede usar **Información de rendimiento de consultas** para analizar el consumo de DTU a lo largo del tiempo.  
Aunque puede usar [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] para obtener el consumo de recursos detallado para todas las consultas (CPU, memoria, E/S, etc.), Información de rendimiento de consultas ofrece una forma rápida y eficaz de determinar su impacto en el consumo global de DTU correspondiente a la base de datos.  
Para obtener más información, vea [Información de rendimiento de consultas de Base de datos SQL de Azure](https://azure.microsoft.com/documentation/articles/sql-database-query-performance/).    

##  <a name="using-query-store-with-elastic-pool-databases"></a>Uso del Almacén de consultas con bases de datos del grupo elástico
Puede usar el Almacén de consultas en todas las bases de datos sin problemas, incluso en grupos densamente empaquetados. Se solucionaron todos los problemas relacionados con el uso excesivo de los recursos que pudieron haber surgido cuando el Almacén de consultas estaba habilitado para el gran número de bases de datos en los grupos elásticos.
##  <a name="a-nameconfigurea-keep-query-store-adjusted-to-your-workload"></a><a name="Configure"></a> Mantener el Almacén de consultas ajustado a la carga de trabajo  
 Configure el Almacén de consultas en función de la carga de trabajo y los requisitos de solución de problemas de rendimiento.   
Los parámetros predeterminados son buenos para un inicio rápido pero debe supervisar el comportamiento del Almacén de consultas a lo largo del tiempo y ajustar su configuración en consecuencia:  
  
 ![query-store-properties](../../relational-databases/performance/media/query-store-properties.png "query-store-properties")  
  
 A continuación se indican algunas instrucciones para establecer valores de parámetro:  
  
 **Tamaño máximo (MB):** especifica el límite del espacio de datos que el Almacén de consultas tomará dentro de la base de datos.  Se trata del valor de configuración más importante que afecta directamente al modo de operación del Almacén de consultas.  
  
 Mientras que el Almacén de consultas recopila consultas, planes de ejecución y estadísticas, su tamaño en la base de datos crece hasta que se alcanza este límite. Cuando esto ocurre, el Almacén de consultas cambia automáticamente el modo de operación a solo lectura y deja de recopilar datos nuevos, lo que significa que el análisis de rendimiento ya no es preciso.  
  
 El valor predeterminado (100 MB) puede no ser suficiente si la carga de trabajo genera gran cantidad de planes y consultas diferentes o si desea mantener el historial de consultas durante un período de tiempo más largo. Realice un seguimiento del uso de espacio actual y aumente el valor de Tamaño máximo (MB) para impedir que el Almacén de consultas cambie al modo de solo lectura.  Utilice [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] o ejecute el siguiente script para obtener la información más reciente sobre el tamaño del Almacén de consultas:  
  
```  
USE [QueryStoreDB];  
GO  
  
SELECT actual_state_desc, desired_state_desc, current_storage_size_mb,   
    max_storage_size_mb, readonly_reason  
FROM sys.database_query_store_options;  
```  
  
 El siguiente script establece un nuevo valor para Tamaño de máximo (MB):  
  
```  
ALTER DATABASE [QueryStoreDB]  
SET QUERY_STORE (MAX_STORAGE_SIZE_MB = 1024);  
```  
  
 **Intervalo de recopilación de estadísticas:** define el nivel de granularidad de la estadística recopilada en tiempo de ejecución (el valor predeterminado es 1 hora). Considere el uso de un valor inferior si necesita una granularidad más fina o menos tiempo para detectar y mitigar los problemas, pero tenga en cuenta que afectará directamente al tamaño de los datos del Almacén de consultas. Use SSMS o Transact-SQL para establecer otro valor para Statistics Collection Interval (Intervalo de recopilación de estadísticas):  
  
```  
ALTER DATABASE [QueryStoreDB] SET QUERY_STORE (INTERVAL_LENGTH_MINUTES = 30);  
```  
  
 **Umbral de consulta obsoleta (días):** directiva de limpieza basada en el tiempo que controla el período de retención de las estadísticas en tiempo de ejecución persistentes y las consultas inactivas.  
De forma predeterminada, el Almacén de consultas se configura para conservar los datos durante 30 días, que puede ser un período innecesariamente largo para su escenario.  
  
 Evite mantener datos históricos que no piense utilizar. Esto reducirá cambios al estado de solo lectura. El tamaño de los datos del Almacén de consultas así como el tiempo para detectar y mitigar el problema serán más predecibles. Use [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] o el siguiente script para configurar la directiva de limpieza basada en el tiempo:  
  
```  
ALTER DATABASE [QueryStoreDB]   
SET QUERY_STORE (CLEANUP_POLICY = (STALE_QUERY_THRESHOLD_DAYS = 14));  
```  
  
 **Modo de limpieza basado en el tamaño:** Especifica si la limpieza automática de los datos se llevará a cabo cuando el tamaño de datos del Almacén de consultas se aproxime al límite.  
  
 Se recomienda activar la limpieza basada en el tamaño para asegurar que el Almacén de consultas siempre se ejecuta en modo de lectura y escritura y recopila los datos más recientes.  
  
```  
ALTER DATABASE [QueryStoreDB]   
SET QUERY_STORE (SIZE_BASED_CLEANUP_MODE = AUTO);  
```  
  
 **Modo de captura del Almacén de consultas:** Especifica la directiva de captura de consultas para el Almacén de consultas.  
  
-   **All** : Captura todas las consultas. Esta es la opción predeterminada.  
  
-   **Auto** : Se omiten las consultas poco frecuentes y aquellas con una duración de la compilación y ejecución insignificante. Los umbrales para la duración del tiempo de ejecución, compilación y recuento de ejecuciones se determinan internamente.  
  
-   **None** : El Almacén de consultas deja de capturar nuevas consultas.  
  
 El siguiente script establece el modo de captura de consultas en Automático:  
  
```  
ALTER DATABASE [QueryStoreDB]   
SET QUERY_STORE (QUERY_CAPTURE_MODE = AUTO);  
```  
  
## <a name="how-to-start-with-query-performance-troubleshooting"></a>Inicio de la solución de problemas de rendimiento de consultas  
 El flujo de trabajo de la solución de problemas con el Almacén de consultas es sencillo, tal y como se muestra en el diagrama siguiente:  
  
 ![query-store-troubleshooting](../../relational-databases/performance/media/query-store-troubleshooting.png "query-store-troubleshooting")  
  
 Habilite el Almacén de consultas mediante [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] como se describe en la sección anterior, o ejecute la siguiente instrucción [!INCLUDE[tsql](../../includes/tsql-md.md)] :  
  
```  
ALTER DATABASE [DatabaseOne] SET QUERY_STORE = ON;  
```  
  
 Almacén de consultas tardará algún tiempo en recopilar el conjunto de datos que representa con precisión la carga de trabajo. Normalmente, un día es suficiente incluso para cargas de trabajo muy complejas. Sin embargo, puede empezar a explorar los datos e identificar las consultas que requieran su atención inmediatamente después de haber habilitado la característica.   
Vaya a la subcarpeta Almacén de consultas del nodo de la base de datos en el Explorador de objetos de [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] para abrir las vistas de solución de problemas de escenarios concretos.   
El Almacén de consultas de [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] funciona con el conjunto de métricas de ejecución, cada una expresada como cualquiera de las siguientes funciones estadísticas:  
  
|Métrica de ejecución|Función estadística|  
|----------------------|------------------------|  
|Tiempo de CPU, duración, recuento de ejecuciones, lecturas lógicas, escrituras lógicas, consumo de memoria y lecturas físicas|Promedio, máximo, mínimo, desviación estándar y total|  
  
 En el gráfico siguiente se muestra cómo localizar vistas del Almacén de consultas:  
  
 ![query-store-views](../../relational-databases/performance/media/query-store-views.png "query-store-views")  
  
 En la siguiente tabla se explica cuándo usar cada una de las vistas del Almacén de consultas:  
  
|Vista SSMS|Escenario|  
|---------------|--------------|  
|Regressed Queries (Consultas devueltas)|Consultas de pinpoint para las que las métricas de ejecución se han devuelto recientemente (es decir, han cambiado a peor). <br />Use esta vista para poner en correlación los problemas de rendimiento observados en la aplicación con las consultas reales que se necesita arreglar o mejorar.|  
|Top Resource Consuming Queries (Consultas que consumen más recursos)|Elija una métrica de ejecución de interés e identifique las consultas que tenían los valores más extremos para un intervalo de tiempo proporcionado. <br />Use esta vista para centrar la atención en las consultas más importantes que tienen el mayor impacto en el consumo de recursos de base de datos.|  
|Tracked Queries (Consultas seguidas)|Realice un seguimiento de la ejecución de las consultas más importantes en tiempo real. Normalmente, esta vista se utiliza cuando tiene consultas con planes forzados y desea asegurarse de que el rendimiento de las mismas es estable.|  
|Overall Resource Consumption (Consumo total de recursos)|Analice el consumo total de recursos para la base de datos para cualquiera de las métricas de ejecución.<br />Use esta vista para identificar patrones de recursos (cargas de trabajo por el día frente a cargas de trabajo por la noche) y optimizar el consumo total para la base de datos.|  
  
> [!TIP]  
>  Para obtener una descripción detallada sobre cómo usar [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] para identificar las consultas que consumen más recursos y corregir aquellas devueltas debido al cambio de una opción de plan, vea los [blogs de @Azure sobre el Almacén de consultas](https://azure.microsoft.com/blog/query-store-a-flight-data-recorder-for-your-database/).  
  
 Cuando identifique una consulta con un rendimiento deficiente, la acción depende de la naturaleza del problema.  
  
-   Si la consulta se ejecutó con varios planes y el último plan es mucho peor que el plan anterior, puede utilizar el mecanismo que fuerza el plan para exigir a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que utilice siempre el plan óptimo para ejecuciones futuras.  
  
     ![query-store-force-plan](../../relational-databases/performance/media/query-store-force-plan.png "query-store-force-plan")  
  
-   Se puede concluir que a la consulta le falta un índice la ejecución óptima. Esta información aparece en el plan de ejecución de la consulta. Cree el índice que falta y compruebe el rendimiento de la consulta mediante el Almacén de consultas.  
  
     ![query-store-show-plan](../../relational-databases/performance/media/query-store-show-plan.png "query-store-show-plan")  
  
     Si ejecuta la carga de trabajo en [!INCLUDE[ssSDS](../../includes/sssds-md.md)], suscríbase al Asesor de índices de [!INCLUDE[ssSDS](../../includes/sssds-md.md)] para recibir automáticamente las recomendaciones de índices.  
  
-   En algunos casos, puede exigir la recompilación estadística si ve que la diferencia entre el número de filas estimado y real en el plan de ejecución es significativa.  
  
-   Vuelva a escribir las consultas problemáticas. Por ejemplo, para aprovechar las ventajas de la parametrización de la consulta o para implementar la lógica más óptima.  
  
##  <a name="a-nameverifya-verify-query-store-is-collecting-query-data-continuously"></a><a name="Verify"></a> Comprobación de que el Almacén de consultas está recopilando datos de consulta continuamente  
 El Almacén de consultas puede cambiar el modo de operación automáticamente. Debe supervisar periódicamente el estado del Almacén de consulta para asegurarse de que está funcionando y tomar medidas para evitar errores debido a causas evitables. Ejecute la siguiente consulta para determinar el modo de operación y ver los parámetros más importantes:  
  
```  
USE [QueryStoreDB];  
GO  
  
SELECT actual_state_desc, desired_state_desc, current_storage_size_mb,   
    max_storage_size_mb, readonly_reason, interval_length_minutes,   
    stale_query_threshold_days, size_based_cleanup_mode_desc,   
    query_capture_mode_desc  
FROM sys.database_query_store_options;  
```  
  
 La diferencia entre `actual_state_desc` y `desired_state_desc` indica que se produjo un cambio de modo de operación automáticamente. El cambio más frecuente es que el Almacén de consultas cambie al modo de solo lectura automáticamente. En circunstancias extremadamente raras, el Almacén de consultas puede terminar en el estado ERROR debido a errores internos.  
  
 Cuando el estado real es de solo lectura, use la columna **readonly_reason** para determinar la causa raíz. Normalmente, encontrará que el Almacén de consultas cambió al modo de solo lectura porque se superó la cuota de tamaño. En ese caso, **readonly_reason** se establece en 65536. Por otros motivos, vea [sys.database_query_store_options &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-database-query-store-options-transact-sql.md).  
  
 Tenga en cuenta los pasos siguientes para cambiar el Almacén de consultas al modo de lectura y escritura y activar la recopilación de datos:  
  
-   Aumente el tamaño de almacenamiento máximo mediante la opción **MAX_STORAGE_SIZE_MB** de **ALTER DATABASE**.  
  
-   Limpie los datos del Almacén de consultas mediante la siguiente instrucción:  
  
    ```  
    ALTER DATABASE [QueryStoreDB] SET QUERY_STORE CLEAR;  
    ```  
  
 Puede aplicar uno de estos dos pasos o ambos ejecutando la siguiente instrucción que vuelve a cambiar explícitamente el modo de operación a lectura y escritura:  
  
```  
ALTER DATABASE [QueryStoreDB]   
SET QUERY_STORE (OPERATION_MODE = READ_WRITE);  
```  
  
 Siga estos pasos para ser proactivo:  
  
-   Puede evitar cambios automáticos de modo de operación aplicando procedimientos recomendados. Si está seguro de que el tamaño del Almacén de consultas es siempre menor que el valor máximo permitido, se reducirá considerablemente la posibilidad de cambiar al modo de solo lectura. Active la directiva basada en el tamaño como se describe en la sección de [configuración del Almacén de consultas](#Configure) para que el Almacén de consultas limpie automáticamente los datos cuando el tamaño se aproxime al límite.  
  
-   Para asegurarse de que se retienen los datos más recientes, configure la directiva basada en el tiempo para quitar información obsoleta frecuentemente.  
  
-   Por último, debería plantearse establecer Modo de captura de consultas en Automático ya que filtra las consultas que suelen ser menos relevantes para la carga de trabajo.  
  
### <a name="error-state"></a>Estado de error  
 Para recuperar el Almacén de consultas intente establecer explícitamente el modo de lectura y escritura y compruebe de nuevo el estado real.  
  
```  
ALTER DATABASE [QueryStoreDB]   
SET QUERY_STORE (OPERATION_MODE = READ_WRITE);    
GO  
  
SELECT actual_state_desc, desired_state_desc, current_storage_size_mb,   
    max_storage_size_mb, readonly_reason, interval_length_minutes,   
    stale_query_threshold_days, size_based_cleanup_mode_desc,   
    query_capture_mode_desc  
FROM sys.database_query_store_options;  
```  
  
 Si el problema continúa, significa que los datos del Almacén de consultas siguen estando dañados en el disco. Debe borrar el Almacén de consultas antes de solicitar el modo de lectura y escritura.  
  
```  
ALTER DATABASE [QueryStoreDB]   
SET QUERY_STORE CLEAR;  
GO  
  
ALTER DATABASE [QueryStoreDB]   
SET QUERY_STORE (OPERATION_MODE = READ_WRITE);    
GO  
  
SELECT actual_state_desc, desired_state_desc, current_storage_size_mb,   
    max_storage_size_mb, readonly_reason, interval_length_minutes,   
    stale_query_threshold_days, size_based_cleanup_mode_desc,   
    query_capture_mode_desc  
FROM sys.database_query_store_options;  
```  
  
## <a name="set-the-optimal-query-capture-mode"></a>Establecimiento del modo óptimo de captura de consultas  
 Mantenga los datos más relevantes en el Almacén de consultas. En la tabla siguiente se describen los escenarios típicos para cada modo de captura de consultas:  
  
|Modo de captura de consultas|Escenario|  
|------------------------|--------------|  
|Todos|Analice la carga de trabajo exhaustivamente en cuanto a todas las formas de las consultas y sus frecuencias de ejecución, y otras estadísticas.<br /><br /> Identifique nuevas consultas en la carga de trabajo.<br /><br /> Detecte si las consultas ad hoc se usan para identificar oportunidades de parametrización automática o de usuario.|  
|Automático|Céntrese en las consultas pertinentes y accionables; en las consultas que se ejecutan con regularidad o en las que tienen un consumo significativo de recursos.|  
|Ninguno|Ya ha capturado el conjunto de consultas que desea supervisar en tiempo de ejecución y desea eliminar los objetos innecesarios que pueden introducir otras consultas.<br /><br /> El modo Ninguno es adecuado para entornos de pruebas y evaluación comparativa.<br /><br /> El modo Ninguno también es adecuado para los proveedores de software que incluyen la configuración del Almacén de consultas definida para supervisar la carga de trabajo de la aplicación.<br /><br /> El modo Ninguno debe utilizarse con precaución, ya que podría perder la oportunidad de realizar un seguimiento de consultas nuevas importantes y de optimizarlas. Evite el uso del modo Ninguno a menos que tenga un escenario específico que lo requiera.|  
  
## <a name="keep-the-most-relevant-data-in-query-store"></a>Conservación de los datos más relevantes en el Almacén de consultas  
 Configure el Almacén de consultas para que contenga solo los datos pertinentes y para que se ejecute continuamente proporcionando una magnífica experiencia de solución de problemas con un impacto mínimo en la carga de trabajo normal.  
La tabla siguiente proporciona prácticas recomendadas:  
  
|Práctica recomendada|Configuración|  
|-------------------|-------------|  
|Limitar los datos históricos retenidos.|Configurar la directiva basada en el tiempo para activar la limpieza automática.|  
|Filtrar las consultas no relevantes.|Configurar Modo de captura de consultas en Automático.|  
|Eliminar consultas menos relevantes cuando se alcanza el tamaño máximo.|Activar la directiva de limpieza basada en el tamaño.|  
  
##  <a name="a-nameparameterizea-avoid-using-non-parameterized-queries"></a><a name="Parameterize"></a> Evitar el uso de consultas sin parámetros  
 El uso de consultas sin parámetros cuando no es absolutamente necesario (por ejemplo, en caso de análisis ad hoc) no es una práctica recomendada.  Los planes almacenados no se puede reutilizar, lo que obliga al optimizador de consultas a compilar consultas para cada texto de consulta única.  
  Además, el Almacén de consultas puede superar rápidamente la cuota de tamaño debido a la posibilidad de un gran número de textos de consulta diferentes y, por consiguiente, un gran número de planes de ejecución distintos con forma similar.  
Por tanto, el rendimiento de la carga de trabajo será deficiente y el Almacén de consultas podría cambiar al modo de solo lectura o podría estar eliminando los datos constantemente intentando mantenerse al día con las consultas entrantes.  
  
 Tenga en cuenta las siguientes opciones:  
  
-   Parametrizar consultas donde proceda, por ejemplo encapsular consultas dentro de un procedimiento almacenado.  
  
-   Use la opción **Optimizar para cargas de trabajo ad hoc** si la carga de trabajo contiene muchos lotes ad hoc de un solo uso con distintos planes de consulta.  
  
    -   Comparar el número de valores query_hash distintos con el número total de entradas en sys.query_store_query. Si la relación es cercana a 1, la carga de trabajo ad hoc genera consultas diferentes.  
  
-   Aplicar la PARAMETRIZACIÓN FORZADA para la base de datos o para un subconjunto de consultas si el número de planes de consulta diferentes no es grande.  
  
    -   Usar la guía de plan para forzar la parametrización solo para la consulta seleccionada.  
  
    -   Configurar la PARAMETRIZACIÓN FORZADA para la base de datos si hay un pequeño número de planes de consulta diferentes en la carga de trabajo. (Cuando la relación entre el recuento de valores query_hash distintos y el número total de entradas de sys.query_store_query es mucho menor que 1.)  
  
-   Establezca **Modo de captura de consulta** en AUTOMÁTICO para filtrar las consultas ad hoc con consumo pequeño de recursos automáticamente.  
  
##  <a name="a-namedropa-avoid-a-drop-and-create-pattern-when-maintaining-containing-objects-for-the-queries"></a><a name="Drop"></a> Evitar un patrón DROP y CREATE al mantener de objetos contenedores para las consultas  
 El Almacén de consultas asocia la entrada de consulta a un objeto contenedor (procedimiento almacenado, función y desencadenador).  Cuando se vuelve a crear un objeto contenedor, se genera una nueva entrada de consulta para el mismo texto de consulta. Esto impide realizar un seguimiento de las estadísticas de rendimiento para esa consulta a lo largo del tiempo y usar un mecanismo para forzar el plan. Para evitar esto, utilice el proceso `ALTER <object>` para cambiar una definición de objeto contenedor siempre que sea posible.  
  
##  <a name="a-namecheckforceda-check-the-status-of-forced-plans-regularly"></a><a name="CheckForced"></a> Comprobación periódica del estado de los planes forzados  
 Forzar el plan es un mecanismo conveniente para corregir el rendimiento de las consultas críticas y hacer que sean más predecibles. Sin embargo, al igual que con las sugerencias de plan y las guías de plan, forzar un plan no es una garantía de que se utilizará en ejecuciones futuras. Normalmente, cuando se cambia el esquema de base de datos de forma que se modifican o se quitan objetos a los que hace referencia el plan de ejecución, al forzar el plan se empiezan a generar errores. En ese caso, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] vuelve a la recompilación de consultas mientras el motivo real del error de la operación de forzado aparece en [sys.query_store_plan &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-query-store-plan-transact-sql.md). La siguiente consulta devuelve información sobre planes forzados.  
  
```  
USE [QueryStoreDB];  
GO  
  
SELECT p.plan_id, p.query_id, q.object_id as containing_object_id,  
    force_failure_count, last_force_failure_reason_desc  
FROM sys.query_store_plan AS p  
JOIN sys.query_store_query AS q on p.query_id = q.query_id  
WHERE is_forced_plan = 1;  
```  
  
 Para ver una lista completa de motivos, vea [sys.query_store_plan &#40;Transact-SQL &#41;](../../relational-databases/system-catalog-views/sys-query-store-plan-transact-sql.md). También puede usar el XEvent **query_store_plan_forcing_failed** para realizar un seguimiento de los errores forzados del plan de solución de problemas.  
  
##  <a name="a-namerenaminga-avoid-renaming-databases-if-you-have-queries-with-forced-plans"></a><a name="Renaming"></a> Evitar el cambio de nombre de las bases de datos si hay consultas con planes de forzados  
 Los planes de ejecución hacen referencia a objetos que usan nombres de tres partes (`database.schema.object`).   
Si cambia el nombre de una base de datos, al forzar el plan se producirá un error que provocará la recompilación en todas las ejecuciones de consulta subsiguientes.  
  
## <a name="see-also"></a>Vea también  
 [Query Store Catalog Views &#40;Transact-SQL&#41; (Vistas de catálogo del almacén de consultas &#40;Transact-SQL&#41;)](../../relational-databases/system-catalog-views/query-store-catalog-views-transact-sql.md)   
 [Query Store Stored Procedures &#40;Transact-SQL&#41; (Procedimientos almacenados del Almacén de consultas &#40;Transact-SQL&#41;)](../../relational-databases/system-stored-procedures/query-store-stored-procedures-transact-sql.md)   
 [Uso del almacén de consultas con OLTP en memoria](../../relational-databases/performance/using-the-query-store-with-in-memory-oltp.md)   
 [Supervisar el rendimiento mediante el almacén de consultas](../../relational-databases/performance/monitoring-performance-by-using-the-query-store.md)  
  
  