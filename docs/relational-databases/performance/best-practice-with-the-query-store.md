---
title: Procedimiento recomendado con el Almacén de consultas | Microsoft Docs
ms.custom: ''
ms.date: 08/21/2019
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
helpviewer_keywords:
- Query Store, best practices
ms.assetid: 5b13b5ac-1e4c-45e7-bda7-ebebe2784551
author: pmasl
ms.author: jrasnick
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||= azure-sqldw-latest||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 4627118daa91305dc905eb5f306e6bd2fcc1b91c
ms.sourcegitcommit: 7625f78617a5b4fd0ff68b2c6de2cb2c758bb0ed
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 09/20/2019
ms.locfileid: "71163895"
---
# <a name="best-practice-with-the-query-store"></a>Procedimiento recomendado con el Almacén de consultas
[!INCLUDE[appliesto-ss-asdb-asdw-xxx-md](../../includes/appliesto-ss-asdb-asdw-xxx-md.md)]

  En este artículo se describen los procedimientos recomendados para usar el Almacén de consultas con la carga de trabajo.  
  
##  <a name="SSMS"></a> Utilice la versión más reciente de [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]  
 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] tiene un conjunto de interfaces de usuario diseñadas para configurar el Almacén de consultas, así como para consumir datos recopilados sobre la carga de trabajo.  
Descargue la última versión de [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] [aquí](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms).  
  
 Para obtener una descripción rápida sobre cómo usar el Almacén de consultas en escenarios de solución de problemas, vea los [blogs de @Azure del Almacén de consultas](https://azure.microsoft.com/blog/query-store-a-flight-data-recorder-for-your-database/).  
  
##  <a name="Insight"></a> Uso de Información de rendimiento de consultas en Azure SQL Database  
 Si ejecuta el Almacén de consultas en [!INCLUDE[ssSDS](../../includes/sssds-md.md)] puede usar **Información de rendimiento de consultas** para analizar el consumo de DTU a lo largo del tiempo.  
Aunque se puede usar [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] para obtener el consumo de recursos detallado para todas las consultas (CPU, memoria, E/S, etc.), Información de rendimiento de consultas ofrece una forma rápida y eficaz de determinar su impacto en el consumo global de DTU de la base de datos.  
Para obtener más información, vea [Información de rendimiento de consultas de Base de datos SQL de Azure](https://azure.microsoft.com/documentation/articles/sql-database-query-performance/).    

##  <a name="using-query-store-with-elastic-pool-databases"></a>Uso del Almacén de consultas con bases de datos del grupo elástico
Puede usar el Almacén de consultas en todas las bases de datos sin problemas, incluso en grupos densamente empaquetados. Se solucionaron todos los problemas relacionados con el uso excesivo de los recursos que pudieron haber surgido cuando el Almacén de consultas estaba habilitado para el gran número de bases de datos en los grupos elásticos.

##  <a name="Configure"></a>Mantener el Almacén de consultas ajustado a la carga de trabajo  
 Configure el Almacén de consultas en función de la carga de trabajo y los requisitos de solución de problemas de rendimiento.   
Los parámetros predeterminados son lo suficientemente buenos para iniciarse, pero debe supervisar el comportamiento del Almacén de consultas a lo largo del tiempo y ajustar su configuración en consecuencia:  
  
 ![query-store-properties](../../relational-databases/performance/media/query-store-properties.png "query-store-properties")  
  
 A continuación se indican algunas instrucciones para establecer valores de parámetro:  
  
 **Tamaño máximo (MB):** especifica el límite del espacio de datos que el Almacén de consultas tomará dentro de la base de datos. Se trata del valor de configuración más importante que afecta directamente al modo de operación del Almacén de consultas.  
  
 Mientras que el Almacén de consultas recopila consultas, planes de ejecución y estadísticas, su tamaño en la base de datos crece hasta que se alcanza este límite. Cuando esto ocurre, el Almacén de consultas cambia automáticamente el modo de operación a solo lectura y deja de recopilar datos nuevos, lo que significa que el análisis de rendimiento ya no es preciso.  
  
 El valor predeterminado en [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] y [!INCLUDE[ssSQL17](../../includes/sssql17-md.md)] (100 MB) puede no que no sea suficiente si la carga de trabajo genera una gran cantidad de planes y consultas diferentes, o bien si quiere mantener el historial de consultas durante un mayor período de tiempo. A partir de [!INCLUDE[sql-server-2019](../../includes/sssqlv15-md.md)], el valor predeterminado es de 1 GB. Realice un seguimiento del uso de espacio actual y aumente el valor de Tamaño máximo (MB) para impedir que el Almacén de consultas cambie al modo de solo lectura. Utilice [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] o ejecute el siguiente script para obtener la información más reciente sobre el tamaño del Almacén de consultas:  
  
```sql 
USE [QueryStoreDB];  
GO  
  
SELECT actual_state_desc, desired_state_desc, current_storage_size_mb,   
    max_storage_size_mb, readonly_reason  
FROM sys.database_query_store_options;  
```  
  
 El siguiente script establece un nuevo valor para Tamaño de máximo (MB):  
  
```sql  
ALTER DATABASE [QueryStoreDB]  
SET QUERY_STORE (MAX_STORAGE_SIZE_MB = 1024);  
```  

 **Intervalo de vaciado de datos:** define la frecuencia en segundos para conservar en disco las estadísticas en tiempo de ejecución recopiladas (el valor predeterminado es de 900 segundos, es decir, 15 minutos). Considere la posibilidad de usar un valor más alto si la carga de trabajo no genera gran cantidad de consultas y planes diferentes, o bien si puede soportar más tiempo de conservación de los datos antes de cerrar la base de datos. 
 
> [!NOTE]
> El uso de la marca de seguimiento 7745 impedirá que los datos del Almacén de consultas se escriban en el disco en el caso de un comando de conmutación por error o apagado. Vea la sección [Uso de marcas de seguimiento en servidores críticos para mejorar la recuperación ante desastres](#Recovery) para obtener más información.

Use [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] o [!INCLUDE[tsql](../../includes/tsql-md.md)] para establecer otro valor para el intervalo de vaciado de datos:  
  
```sql  
ALTER DATABASE [QueryStoreDB] 
SET QUERY_STORE (DATA_FLUSH_INTERVAL_SECONDS = 900);  
```  

 **Intervalo de la recopilación de estadísticas:** define el nivel de granularidad de la estadística recopilada en tiempo de ejecución (el valor predeterminado es 60 minutos). Considere el uso de un valor inferior si necesita una granularidad más fina o menos tiempo para detectar y mitigar los problemas, pero tenga en cuenta que afectará directamente al tamaño de los datos del Almacén de consultas. Use [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] o [!INCLUDE[tsql](../../includes/tsql-md.md)] para establecer otro valor para el intervalo de recopilación de estadísticas:  
  
```sql  
ALTER DATABASE [QueryStoreDB] 
SET QUERY_STORE (INTERVAL_LENGTH_MINUTES = 60);  
```  
  
 **Umbral de consultas obsoletas (días):** directiva de limpieza basada en el tiempo que controla el período de retención de las estadísticas en tiempo de ejecución persistentes y las consultas inactivas.  
De forma predeterminada, el Almacén de consultas se configura para conservar los datos durante 30 días, que puede ser un período innecesariamente largo para su escenario.  
  
 Evite mantener datos históricos que no piense utilizar. Esto reducirá cambios al estado de solo lectura. El tamaño de los datos del Almacén de consultas así como el tiempo para detectar y mitigar el problema serán más predecibles. Use [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] o el siguiente script para configurar la directiva de limpieza basada en el tiempo:  
  
```sql  
ALTER DATABASE [QueryStoreDB]   
SET QUERY_STORE (CLEANUP_POLICY = (STALE_QUERY_THRESHOLD_DAYS = 90));  
```  
  
 **Modo de limpieza basado en el tamaño:** especifica si la limpieza automática de los datos se llevará a cabo cuando el tamaño de datos del Almacén de consultas se aproxime al límite.  
  
 Se recomienda activar la limpieza basada en el tamaño para asegurar que el Almacén de consultas siempre se ejecuta en modo de lectura y escritura y recopila los datos más recientes.  
  
```sql  
ALTER DATABASE [QueryStoreDB]   
SET QUERY_STORE (SIZE_BASED_CLEANUP_MODE = AUTO);  
```  
  
 **Modo de captura del almacén de consultas:** especifica la directiva de captura de consultas para el Almacén de consultas.  
  
-   **All**: captura todas las consultas. Esta es la opción predeterminada en [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] y [!INCLUDE[ssSQL17](../../includes/sssql17-md.md)].  
  
-   **Auto**: se omiten las consultas poco frecuentes y aquellas con una duración de compilación y ejecución insignificante. Los umbrales para la duración del tiempo de ejecución, compilación y recuento de ejecuciones se determinan internamente. A partir de [!INCLUDE[sql-server-2019](../../includes/sssqlv15-md.md)], esta es la opción predeterminada.  
  
-   **None**: el Almacén de consultas deja de capturar consultas nuevas.  

-   **Personalizado**: permite controles adicionales y ajustar la directiva de recopilación de datos. Las nuevas opciones de configuración personalizadas definen lo que ocurre durante el umbral de tiempo de la directiva de captura interna: un límite de tiempo durante el que se evalúan las condiciones configurables y, si alguna de ellas es verdadera, la consulta puede registrarse en el Almacén de consultas.
  
 El siguiente script establece el modo de captura de consultas en Automático:  
  
```sql  
ALTER DATABASE [QueryStoreDB]   
SET QUERY_STORE (QUERY_CAPTURE_MODE = AUTO);  
```  

### <a name="examples"></a>Ejemplos
En el ejemplo siguiente, se establece el modo de captura de consultas en automático y se configuran otras opciones recomendadas en [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]:  
  
```sql  
ALTER DATABASE [QueryStoreDB]   
SET QUERY_STORE = ON
    (
      OPERATION_MODE = READ_WRITE,
      CLEANUP_POLICY = ( STALE_QUERY_THRESHOLD_DAYS = 90 ),
      DATA_FLUSH_INTERVAL_SECONDS = 900,
      QUERY_CAPTURE_MODE = AUTO,
      MAX_STORAGE_SIZE_MB = 1000,
      INTERVAL_LENGTH_MINUTES = 60
    );
```  

En el ejemplo siguiente, se establece el modo de captura de consultas en automático y se configuran otras opciones recomendadas en [!INCLUDE[ssSQL17](../../includes/sssql17-md.md)] para incluir estadísticas de espera:  

```sql
ALTER DATABASE [QueryStoreDB] 
SET QUERY_STORE = ON
    (
      OPERATION_MODE = READ_WRITE, 
      CLEANUP_POLICY = ( STALE_QUERY_THRESHOLD_DAYS = 90 ),
      DATA_FLUSH_INTERVAL_SECONDS = 900,
      QUERY_CAPTURE_MODE = AUTO,
      MAX_STORAGE_SIZE_MB = 1000, 
      INTERVAL_LENGTH_MINUTES = 60,
      SIZE_BASED_CLEANUP_MODE = AUTO, 
      MAX_PLANS_PER_QUERY = 200,
      WAIT_STATS_CAPTURE_MODE = ON,
    );
```

En el ejemplo siguiente, se establece el modo de captura de consultas en automático y se configuran otras opciones recomendadas en [!INCLUDE[sql-server-2019](../../includes/sssqlv15-md.md)]. **De manera opcional**, se establece la directiva de captura personalizada con los valores predeterminados, en lugar del nuevo modo de captura automático predeterminado:  

```sql
ALTER DATABASE [QueryStoreDB]  
SET QUERY_STORE = ON 
    (
      OPERATION_MODE = READ_WRITE, 
      CLEANUP_POLICY = ( STALE_QUERY_THRESHOLD_DAYS = 90 ),
      DATA_FLUSH_INTERVAL_SECONDS = 900,
      MAX_STORAGE_SIZE_MB = 1000, 
      INTERVAL_LENGTH_MINUTES = 60,
      SIZE_BASED_CLEANUP_MODE = AUTO, 
      MAX_PLANS_PER_QUERY = 200,
      WAIT_STATS_CAPTURE_MODE = ON,
      QUERY_CAPTURE_MODE = CUSTOM,
      QUERY_CAPTURE_POLICY = (
        STALE_CAPTURE_POLICY_THRESHOLD = 24 HOURS,
        EXECUTION_COUNT = 30,
        TOTAL_COMPILE_CPU_TIME_MS = 1000,
        TOTAL_EXECUTION_CPU_TIME_MS = 100 
      )
    );
```

## <a name="how-to-start-with-query-performance-troubleshooting"></a>Inicio de la solución de problemas de rendimiento de consultas  
 El flujo de trabajo de la solución de problemas con el Almacén de consultas es sencillo, tal y como se muestra en el diagrama siguiente:  
  
 ![query-store-troubleshooting](../../relational-databases/performance/media/query-store-troubleshooting.png "query-store-troubleshooting")  
  
 Habilite el Almacén de consultas mediante [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] como se describe en la sección anterior, o ejecute la siguiente instrucción [!INCLUDE[tsql](../../includes/tsql-md.md)] :  
  
```sql  
ALTER DATABASE [DatabaseOne] SET QUERY_STORE = ON;  
```  

Almacén de consultas tardará algún tiempo en recopilar el conjunto de datos que representa con precisión la carga de trabajo. Normalmente, un día es suficiente incluso para cargas de trabajo muy complejas. Sin embargo, puede empezar a explorar los datos e identificar las consultas que requieran su atención inmediatamente después de haber habilitado la característica.   
Vaya a la subcarpeta Almacén de consultas del nodo de la base de datos en el Explorador de objetos de [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] para abrir las vistas de solución de problemas de escenarios concretos.   
El Almacén de consultas de[!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] funciona con el conjunto de métricas de ejecución, cada una expresada como cualquiera de las siguientes funciones estadísticas:  
  
|Versión de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|Métrica de ejecución|Función estadística|  
|----------------------|----------------------|------------------------|  
|[!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]|Tiempo de CPU, duración, recuento de ejecuciones, lecturas lógicas, escrituras lógicas, consumo de memoria, lecturas físicas, tiempo de CLR, grado de paralelismo (DOP) y recuento de filas|Promedio, máximo, mínimo, desviación estándar y total|
|[!INCLUDE[ssSQL17](../../includes/sssql17-md.md)]|Tiempo de CPU, duración, recuento de ejecuciones, lecturas lógicas, escrituras lógicas, consumo de memoria, lecturas físicas, tiempo de CLR, grado de paralelismo (DOP), recuento de filas, memoria de registro, memoria de TempDB y tiempos de espera|Promedio, máximo, mínimo, desviación estándar y total|
  
 En el gráfico siguiente se muestra cómo localizar vistas del Almacén de consultas:  
  
 ![Vistas del Almacén de consultas](../../relational-databases/performance/media/objectexplorerquerystore_sql17.png "Query Store views")  
  
 En la siguiente tabla se explica cuándo usar cada una de las vistas del Almacén de consultas:  
  
|Vista SSMS|Escenario|  
|---------------|--------------|  
|Regressed Queries (Consultas devueltas)|Consultas de pinpoint para las que las métricas de ejecución se han devuelto recientemente (es decir, han cambiado a peor). <br />Use esta vista para poner en correlación los problemas de rendimiento observados en la aplicación con las consultas reales que se necesita arreglar o mejorar.|  
|Overall Resource Consumption (Consumo total de recursos)|Analice el consumo total de recursos para la base de datos para cualquiera de las métricas de ejecución.<br />Use esta vista para identificar patrones de recursos (cargas de trabajo por el día frente a cargas de trabajo por la noche) y optimizar el consumo total para la base de datos.|  
|Top Resource Consuming Queries (Consultas que consumen más recursos)|Elija una métrica de ejecución de interés e identifique las consultas que tenían los valores más extremos para un intervalo de tiempo proporcionado. <br />Use esta vista para centrar la atención en las consultas más importantes que tienen el mayor impacto en el consumo de recursos de base de datos.|  
|Consultas con planes forzados|Enumera los planes forzados anteriormente mediante el Almacén de consultas. <br />Use esta vista para obtener acceso rápidamente a todos los planes forzados actualmente.|  
|Consultas con gran variación|Analice consultas con una gran variación de ejecución en lo referente a cualquiera de las dimensiones disponibles, como la duración, el tiempo de CPU, la E/S y el uso de memoria en el intervalo de tiempo deseado.<br />Use esta vista para identificar consultas con un rendimiento muy variable que pueda afectar a la experiencia del usuario a través de las aplicaciones.|  
|Estadísticas de espera de consulta|Analice las categorías de espera más activas en una base de datos y qué consultas contribuyen más a la categoría de espera seleccionada.<br />Use esta vista para analizar las estadísticas de espera e identificar las consultas que pueden estar afectando a la experiencia del usuario entre las aplicaciones.<br /><br />**Se aplica a:** A partir de [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] v18.0 y [!INCLUDE[ssSQL17](../../includes/sssql17-md.md)]|  
|Tracked Queries (Consultas seguidas)|Realice un seguimiento de la ejecución de las consultas más importantes en tiempo real. Normalmente, esta vista se utiliza cuando tiene consultas con planes forzados y desea asegurarse de que el rendimiento de las mismas es estable.|
  
> [!TIP]
> Para obtener una descripción detallada sobre cómo usar [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] para identificar las consultas que consumen más recursos y corregir aquellas devueltas debido al cambio de una opción de plan, vea los [blogs de @Azure sobre el Almacén de consultas](https://azure.microsoft.com/blog/query-store-a-flight-data-recorder-for-your-database/).  
  
 Cuando identifique una consulta con un rendimiento deficiente, la acción dependerá de la naturaleza del problema.  
  
-   Si la consulta se ejecutó con varios planes y el último plan es mucho peor que el anterior, puede utilizar el mecanismo que fuerza el plan. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] intenta forzar el plan en el optimizador. Si se produce un error al exigir el plan, se producirá un evento XEvent y el optimizador realizará su trabajo de forma normal. 
  
     ![query-store-force-plan](../../relational-databases/performance/media/query-store-force-plan.png "query-store-force-plan")  

> [!NOTE]
> El gráfico anterior puede presentar distintas formas para planes de consulta específicos, con los significados siguientes para cada estado posible:<br />  
> 
> |Forma|Significado|  
> |-------------------|-------------|
> |Circle|Consulta completada (ejecución normal finalizada correctamente)|
> |Square|Cancelado (ejecución del cliente iniciada anulada)|
> |Triangle|Error (ejecución de excepción anulada)|
> 
> Además, el tamaño de la forma refleja el recuento de la ejecución de consulta dentro del intervalo de tiempo especificado, aumentando de tamaño con un número mayor de ejecuciones.  

-   Se puede concluir que a la consulta le falta un índice la ejecución óptima. Esta información aparece en el plan de ejecución de la consulta. Cree el índice que falta y compruebe el rendimiento de la consulta mediante el Almacén de consultas.  
  
     ![query-store-show-plan](../../relational-databases/performance/media/query-store-show-plan.png "query-store-show-plan")  
  
     Si ejecuta la carga de trabajo en [!INCLUDE[ssSDS](../../includes/sssds-md.md)], suscríbase al Asesor de índices de [!INCLUDE[ssSDS](../../includes/sssds-md.md)] para recibir automáticamente las recomendaciones de índices.  
  
-   En algunos casos, puede exigir la recompilación estadística si ve que la diferencia entre el número de filas estimado y real en el plan de ejecución es significativa.  
  
-   Vuelva a escribir las consultas problemáticas. Por ejemplo, para aprovechar las ventajas de la parametrización de la consulta o para implementar la lógica más óptima.  
  
##  <a name="Verify"></a> Comprobación de que el Almacén de consultas está recopilando datos de consulta continuamente  
 El Almacén de consultas puede cambiar el modo de operación automáticamente. Debe supervisar periódicamente el estado del Almacén de consulta para asegurarse de que está funcionando y tomar medidas para evitar errores debido a causas evitables. Ejecute la siguiente consulta para determinar el modo de operación y ver los parámetros más importantes:  
  
```sql
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
  
    ```sql  
    ALTER DATABASE [QueryStoreDB] SET QUERY_STORE CLEAR;  
    ```  
  
Puede aplicar uno de estos dos pasos o ambos ejecutando la siguiente instrucción que vuelve a cambiar explícitamente el modo de operación a lectura y escritura:  
  
```sql  
ALTER DATABASE [QueryStoreDB]   
SET QUERY_STORE (OPERATION_MODE = READ_WRITE);  
```  
  
 Siga estos pasos para ser proactivo:  
  
-   Puede evitar cambios automáticos de modo de operación aplicando procedimientos recomendados. Si está seguro de que el tamaño del Almacén de consultas es siempre menor que el valor máximo permitido, se reducirá considerablemente la posibilidad de cambiar al modo de solo lectura. Active la directiva basada en el tamaño como se describe en la sección de [configuración del Almacén de consultas](#Configure) para que el Almacén de consultas limpie automáticamente los datos cuando el tamaño se aproxime al límite.  
  
-   Para asegurarse de que se retienen los datos más recientes, configure la directiva basada en el tiempo para quitar información obsoleta frecuentemente.  
  
-   Por último, debería plantearse establecer Modo de captura de consultas en Automático ya que filtra las consultas que suelen ser menos relevantes para la carga de trabajo.  
  
### <a name="error-state"></a>Estado de error  
 Para recuperar el Almacén de consultas intente establecer explícitamente el modo de lectura y escritura y compruebe de nuevo el estado real.  
  
```sql  
ALTER DATABASE [QueryStoreDB]   
SET QUERY_STORE (OPERATION_MODE = READ_WRITE);    
GO  
  
SELECT actual_state_desc, desired_state_desc, current_storage_size_mb,   
    max_storage_size_mb, readonly_reason, interval_length_minutes,   
    stale_query_threshold_days, size_based_cleanup_mode_desc,   
    query_capture_mode_desc  
FROM sys.database_query_store_options;  
```  
  
 Si el problema continúa, significa que los datos del Almacén de consultas siguen dañados en el disco.
 
 A partir de [!INCLUDE[ssSQL17](../../includes/sssql17-md.md)], el Almacén de consultas se puede recuperar si se ejecuta el procedimiento **sp_query_store_consistency_check** almacenado en la base de datos afectada. El Almacén de consultas debe deshabilitarse antes de intentar la operación de recuperación. Para [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)], tendrá que borrar los datos del Almacén de consultas, como se muestra a continuación.
 
 Si la recuperación no se realizó correctamente, puede intentar borrar el Almacén de consultas antes de establecer el modo de lectura y escritura.  
  
```sql  
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
|All|Analice la carga de trabajo exhaustivamente en cuanto a todas las formas de las consultas y sus frecuencias de ejecución, y otras estadísticas.<br /><br /> Identifique nuevas consultas en la carga de trabajo.<br /><br /> Detecte si las consultas ad hoc se usan para identificar oportunidades de parametrización automática o de usuario.<br /><br />**Nota:** Este es el modo de captura predeterminado en [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] y [!INCLUDE[ssSQL17](../../includes/sssql17-md.md)].|  
|Auto|Céntrese en las consultas pertinentes y accionables; en las consultas que se ejecutan con regularidad o en las que tienen un consumo significativo de recursos.<br /><br />**Nota:** A partir de [!INCLUDE[sql-server-2019](../../includes/sssqlv15-md.md)], este es el modo de captura predeterminado.|  
|None|Ya ha capturado el conjunto de consultas que desea supervisar en tiempo de ejecución y desea eliminar los objetos innecesarios que pueden introducir otras consultas.<br /><br /> El modo Ninguno es adecuado para entornos de pruebas y evaluación comparativa.<br /><br /> El modo Ninguno también es adecuado para los proveedores de software que incluyen la configuración del Almacén de consultas definida para supervisar la carga de trabajo de la aplicación.<br /><br /> El modo Ninguno debe utilizarse con precaución, ya que podría perder la oportunidad de realizar un seguimiento de consultas nuevas importantes y de optimizarlas. Evite el uso del modo Ninguno a menos que tenga un escenario específico que lo requiera.|  
|Personalizado|[!INCLUDE[sql-server-2019](../../includes/sssqlv15-md.md)] introduce un modo de captura PERSONALIZADO en el comando `ALTER DATABASE SET QUERY_STORE`. Cuando se habilita, una nueva configuración de la directiva de captura del Almacén de consultas incluye más configuraciones del Almacén para optimizar la recopilación de datos en un servidor específico.<br /><br />Las nuevas opciones de configuración personalizadas definen lo que ocurre durante el umbral de tiempo de la directiva de captura interna: un límite de tiempo durante el que se evalúan las condiciones configurables y, si alguna de ellas es verdadera, la consulta puede registrarse en el Almacén de consultas. Para obtener más información, vea [ALTER DATABASE SET Options &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql-set-options.md).|  

> [!NOTE]
> Los cursores, las consultas dentro de los procedimientos almacenados y las consultas compiladas de forma nativa siempre se capturan cuando el modo de captura de consultas se establece en Todo, Automático o Personalizado. Para capturar consultas compiladas de forma nativa, habilite la recopilación de estadísticas por consulta mediante [sys.sp_xtp_control_query_exec_stats](../../relational-databases/system-stored-procedures/sys-sp-xtp-control-query-exec-stats-transact-sql.md). 

## <a name="keep-the-most-relevant-data-in-query-store"></a>Conservación de los datos más relevantes en el Almacén de consultas  
 Configure el Almacén de consultas para que contenga solo los datos pertinentes y para que se ejecute continuamente proporcionando una magnífica experiencia de solución de problemas con un impacto mínimo en la carga de trabajo normal.  
La tabla siguiente proporciona prácticas recomendadas:  
  
|Práctica recomendada|Configuración|  
|-------------------|-------------|  
|Limitar los datos históricos retenidos.|Configurar la directiva basada en el tiempo para activar la limpieza automática.|  
|Filtrar las consultas no relevantes.|Configurar Modo de captura de consultas en Automático.|  
|Eliminar consultas menos relevantes cuando se alcanza el tamaño máximo.|Activar la directiva de limpieza basada en el tamaño.|  
  
##  <a name="Parameterize"></a> Evitar el uso de consultas sin parámetros  
El uso de consultas sin parámetros cuando no es absolutamente necesario (por ejemplo, en caso de análisis ad hoc) no es una práctica recomendada.  Los planes almacenados no se puede reutilizar, lo que obliga al optimizador de consultas a compilar consultas para cada texto de consulta única. Para obtener más información, consulte [Directrices para usar la parametrización forzada](../../relational-databases/query-processing-architecture-guide.md#ForcedParamGuide).  
Además, el Almacén de consultas puede superar rápidamente la cuota de tamaño debido a la posibilidad de un gran número de textos de consulta diferentes y, por consiguiente, un gran número de planes de ejecución distintos con forma similar.  
Por tanto, el rendimiento de la carga de trabajo será deficiente y el Almacén de consultas podría cambiar al modo de solo lectura o podría estar eliminando los datos constantemente intentando mantenerse al día con las consultas entrantes.  
  
Tenga en cuenta las siguientes opciones:  

-   Parametrice consultas donde proceda, por ejemplo, el encapsulamiento de consultas dentro de un procedimiento almacenado osp_executesql. Para obtener más información, consulte [Parámetros y reutilización de un plan de ejecución](../../relational-databases/query-processing-architecture-guide.md#PlanReuse).    
  
-   Use la opción [**Optimizar para cargas de trabajo ad hoc**](../../database-engine/configure-windows/optimize-for-ad-hoc-workloads-server-configuration-option.md) si la carga de trabajo contiene muchos lotes ad hoc de un solo uso con distintos planes de consulta.  
  
    -   Comparar el número de valores query_hash distintos con el número total de entradas en sys.query_store_query. Si la relación es cercana a 1, la carga de trabajo ad hoc genera consultas diferentes.  
  
-   Aplique la [**parametrización forzada**](../../relational-databases/query-processing-architecture-guide.md#ForcedParam) para la base de datos o para un subconjunto de consultas si el número de planes de consulta diferentes no es grande.  
  
    -   Use la [guía de plan](../../relational-databases/performance/specify-query-parameterization-behavior-by-using-plan-guides.md) para forzar la parametrización solo para la consulta seleccionada.  
  
    -   Configure la parametrización forzada mediante el comando [opción de base de datos Parametrización](../../relational-databases/databases/database-properties-options-page.md#miscellaneous) si hay un pequeño número de planes de consulta diferentes en la carga de trabajo: cuando la relación entre el recuento de valores query_hash distintos y el número total de entradas de sys.query_store_query es mucho menor que 1.  
  
-   Establezca **Modo de captura de consulta** en AUTOMÁTICO para filtrar las consultas ad hoc con consumo pequeño de recursos automáticamente.  
  
##  <a name="Drop"></a>Evitar un patrón DROP y CREATE al mantener de objetos contenedores para las consultas  
El Almacén de consultas asocia la entrada de consulta a un objeto contenedor (procedimiento almacenado, función y desencadenador).  Cuando se vuelve a crear un objeto contenedor, se genera una nueva entrada de consulta para el mismo texto de consulta. Esto impide realizar un seguimiento de las estadísticas de rendimiento para esa consulta a lo largo del tiempo y usar un mecanismo para forzar el plan. Para evitar esto, utilice el proceso `ALTER <object>` para cambiar una definición de objeto contenedor siempre que sea posible.  
  
##  <a name="CheckForced"></a> Comprobación periódica del estado de los planes forzados  
Forzar el plan es un mecanismo conveniente para corregir el rendimiento de las consultas críticas y hacer que sean más predecibles. Sin embargo, al igual que con las sugerencias de plan y las guías de plan, forzar un plan no es una garantía de que se utilizará en ejecuciones futuras. Normalmente, cuando se cambia el esquema de base de datos de forma que se modifican o se quitan objetos a los que hace referencia el plan de ejecución, al forzar el plan se empiezan a generar errores. En ese caso, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] vuelve a la recompilación de consultas mientras el motivo real del error de la operación de forzado aparece en [sys.query_store_plan](../../relational-databases/system-catalog-views/sys-query-store-plan-transact-sql.md). La siguiente consulta devuelve información sobre planes forzados.  
  
```sql  
USE [QueryStoreDB];  
GO  
  
SELECT p.plan_id, p.query_id, q.object_id as containing_object_id,  
    force_failure_count, last_force_failure_reason_desc  
FROM sys.query_store_plan AS p  
JOIN sys.query_store_query AS q on p.query_id = q.query_id  
WHERE is_forced_plan = 1;  
```  
  
 Para ver una lista completa de motivos, vea [sys.query_store_plan](../../relational-databases/system-catalog-views/sys-query-store-plan-transact-sql.md). También puede usar el XEvent **query_store_plan_forcing_failed** para realizar un seguimiento de los errores forzados del plan y solucionarlos.  
  
##  <a name="Renaming"></a> Evitar el cambio de nombre de las bases de datos si hay consultas con planes de forzados  

Los planes de ejecución hacen referencia a objetos que usan nombres de tres partes `database.schema.object`.   

Si cambia el nombre de una base de datos, al forzar el plan se producirá un error que provocará la recompilación en todas las ejecuciones de consulta subsiguientes.  

##  <a name="Recovery"></a> Uso de marcas de seguimiento en servidores críticos
 
Las marcas de seguimiento globales 7745 y 7752 pueden usarse para mejorar la disponibilidad de las bases de datos mediante el Almacén de consultas. Para más información, consulte [Marcas de seguimiento](../../t-sql/database-console-commands/dbcc-traceon-trace-flags-transact-sql.md).
  
-  La marca de seguimiento 7745 evitará el comportamiento predeterminado en el que el almacén de consultas escribe datos en el disco antes de que [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] pueda apagarse. Esto significa que los datos del Almacén de consultas que se han recopilado, pero que aún no han almacenado en el disco, se perderán. 
  
-  La marca de seguimiento 7752 permite la carga asincrónica del Almacén de consultas. De esta manera, la base de datos se pone en línea y las consultas se ejecutan antes de que el Almacén de consultas se haya recuperado completamente. El comportamiento predeterminado consiste en realizar la carga sincrónica del Almacén de consultas. Dicho comportamiento impide que se ejecuten las consultas antes de que el Almacén de consultas se haya recuperado, pero también impide que se pierdan las consultas en la colección de datos.

   > [!NOTE]
   > A partir de [!INCLUDE[sql-server-2019](../../includes/sssqlv15-md.md)], este comportamiento se controla mediante el motor, y la marca de seguimiento 7752 no tiene ningún efecto.

> [!IMPORTANT]
> Si usa el Almacén de consultas para conclusiones de la carga de trabajo just-in-time en [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)], tenga previsto instalar las correcciones de escalabilidad de rendimiento en [KB 4340759](https://support.microsoft.com/help/4340759) lo antes posible. 

## <a name="see-also"></a>Consulte también  
[Opciones de ALTER DATABASE SET &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql-set-options.md)     
[Query Store Catalog Views &#40;Transact-SQL&#41; (Vistas de catálogo del Almacén de consultas &#40;Transact-SQL&#41;)](../../relational-databases/system-catalog-views/query-store-catalog-views-transact-sql.md)     
[Query Store Stored Procedures &#40;Transact-SQL&#41; (Procedimientos almacenados del Almacén de consultas &#40;Transact-SQL&#41;)](../../relational-databases/system-stored-procedures/query-store-stored-procedures-transact-sql.md)     
[Uso del almacén de consultas con OLTP en memoria](../../relational-databases/performance/using-the-query-store-with-in-memory-oltp.md)     
[Monitoring Performance By Using the Query Store](../../relational-databases/performance/monitoring-performance-by-using-the-query-store.md)      
[Guía de arquitectura de procesamiento de consultas](../../relational-databases/query-processing-architecture-guide.md)     
  
