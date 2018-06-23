---
title: Mejorar el rendimiento de los índices de texto completo | Microsoft Docs
ms.custom: ''
ms.date: 04/26/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- dbe-search
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- performance [SQL Server], full-text search
- full-text queries [SQL Server], performance
- crawls [full-text search]
- full-text indexes [SQL Server], performance
- full-text search [SQL Server], performance
- batches [SQL Server], full-text search
ms.assetid: ef39ef1f-f0b7-4582-8e9c-31d4bd0ad35d
caps.latest.revision: 66
author: craigg-msft
ms.author: craigg
manager: jhubbard
ms.openlocfilehash: fb10d58c2197f422fe59ff2fa9a165bca5f8bf62
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36202491"
---
# <a name="improve-the-performance-of-full-text-indexes"></a>Mejorar el rendimiento de los índices de texto completo
  El rendimiento de la indización y las búsquedas de texto completo se ve afectado por los recursos de hardware; por ejemplo, la memoria, la velocidad de disco y de CPU, y la arquitectura del equipo.  
  
##  <a name="causes"></a> Causas comunes de los problemas de rendimiento  
 La causa principal de un rendimiento reducido de la indización de texto completo son los límites de los recursos de hardware:  
  
-   Si el uso de la CPU que hace el proceso de host de demonio de filtro (fdhost.exe) o el proceso de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (sqlservr.exe) está cercano al 100 por cien, la CPU es el cuello de botella.  
  
-   Si la longitud promedio de la cola de espera del disco es superior al doble del número de cabezales de disco, el cuello de botella está en el disco. La solución principal consiste en crear catálogos de texto completo independientes de los registros y los archivos de base de datos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Coloque los registros, los archivos de base de datos y los catálogos de texto completo en discos independientes. También puede ayudar a mejorar el rendimiento de la indización la adquisición de discos más rápidos y el uso de RAID.  
  
-   Si hay escasez de memoria física (límite de 3 GB), la memoria podría ser el cuello de botella. Las limitaciones de la memoria física son posibles en todos los sistemas y, en los sistemas de 32 bits, la presión de memoria virtual puede ralentizar la indización de texto completo.  
  
    > [!NOTE]  
    >  A partir de [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)], el motor de texto completo puede utilizar la memoria AWE porque forma parte de sqlservr.exe.  
  
 Si el sistema no tiene cuellos de botella de hardware, el rendimiento de la indización de la búsqueda de texto completo depende sobre todo de lo siguiente:  
  
-   El tiempo que tarda [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] en crear lotes de texto completo.  
  
-   La rapidez con la que el denomino de filtro puede consumir dichos lotes.  
  
> [!NOTE]  
>  A diferencia del rellenado completo, el rellenado incremental, manual y de seguimiento automático de cambios no se han diseñado para obtener los máximos recursos de hardware y así aumentar la velocidad. Por ello, estas sugerencias para el ajuste podrían no mejorar el rendimiento de la indización de texto completo.  
  
 Cuando se completa un rellenado, se desencadena un proceso de combinación final que combina los fragmentos de índice en un solo índice de texto completo maestro. Esto permite mejorar el rendimiento de las consultas, ya que únicamente es necesario realizar consultas en el índice maestro, en lugar de hacerlo en varios fragmentos de índice, y se pueden utilizar mejores estadísticas de puntuación para obtener la clasificación por relevancia. Tenga en cuenta que la combinación maestra puede requerir un uso intensivo de E/S, ya que es necesario escribir y leer una gran cantidad de datos cuando se combinan los fragmentos de índice, aunque esto no bloquea las consultas entrantes.  
  
> [!IMPORTANT]  
>  La combinación maestra de una cantidad grande de datos puede crear una transacción de larga duración, con lo que se retrasa el truncamiento del registro de transacciones durante el punto de comprobación. En este caso, bajo el modelo de recuperación completa, el registro de transacciones podría crecer significativamente. Como práctica recomendada, antes de reorganizar un índice de texto completo grande en una base de datos que use el modelo de recuperación completa, asegúrese de que el registro de transacciones contenga el espacio suficiente para una transacción de larga duración. Para obtener más información, vea [Administrar el tamaño del archivo de registro de transacciones](../logs/manage-the-size-of-the-transaction-log-file.md).  
  
  
  
##  <a name="tuning"></a> Ajustar el rendimiento de los índices de texto completo  
 Para obtener el máximo rendimiento de los índices de texto completo, implemente las prácticas recomendadas siguientes:  
  
-   Para utilizar todos los procesadores o núcleos al máximo, establezca [sp_configure](/sql/relational-databases/system-stored-procedures/sp-configure-transact-sql)'`max full-text crawl ranges`' para el número de CPU en el sistema. Para obtener más información sobre esta opción de configuración, vea [max full-text crawl range (opción de configuración del servidor)](../../database-engine/configure-windows/max-full-text-crawl-range-server-configuration-option.md).  
  
-   Asegúrese de que la tabla base tiene un índice clúster. Use un tipo de datos entero para la primera columna del índice clúster. No use GUID en la primera columna del índice clúster. Un rellenado de varios intervalos en un índice clúster puede conseguir que el rellenado se realice a la mayor velocidad. Recomendamos que la columna que actúa como clave de texto completo sea de un tipo de datos entero.  
  
-   Actualice las estadísticas de la tabla base mediante la instrucción [UPDATE STATISTICS](/sql/t-sql/statements/update-statistics-transact-sql) . Es muy importante que actualice las estadísticas del índice clúster o la clave de texto completo para un rellenado completo. De este modo se ayuda a que un rellenado de varios intervalos genere bien las particiones de la tabla.  
  
-   Cree un índice secundario en un `timestamp` columna si desea mejorar el rendimiento del rellenado incremental.  
  
-   Antes de realizar un rellenado completo en un equipo grande con varias CPU, es recomendable que limite temporalmente el tamaño del grupo de búferes estableciendo el valor `max server memory` a fin de dejar suficiente memoria para el uso del sistema operativo y el proceso fdhost.exe. Para obtener más información, vea "Estimar los requisitos de memoria del proceso de host de demonio de filtro (fdhost.exe)" más adelante en este tema.  
  
  
  
##  <a name="full"></a> Solucionar problemas de rendimiento de los rellenados completos  
 Para diagnosticar problemas de rendimiento, examine los registros de rastreo de texto completo. Para obtener información acerca de los registros de rastreo, vea [rellenar índices de texto completo](../indexes/indexes.md).  
  
 Es recomendable que se siga el orden que se indica a continuación a la hora de solucionar los problemas si el rendimiento de los rellenados completos no es satisfactorio.  
  
### <a name="physical-memory-usage"></a>Uso de la memoria física  
 Durante un rellenado de texto completo, es posible que fdhost.exe o sqlservr.exe no dispongan de suficiente memoria o se queden sin memoria. Si el registro de rastreo de texto completo muestra que fdhost.exe se reinicia con frecuencia o que se devuelve el código de error 8007008, significa que uno de estos procesos se está quedando sin memoria. Si fdhost.exe produce volcados, especialmente en equipos grandes con varias CPU, es posible que se esté quedando sin memoria.  
  
> [!NOTE]  
>  Para obtener información acerca de los búferes de memoria utilizados por un rastreo de texto completo, vea [sys.dm_fts_memory_buffers &#40;Transact-SQL&#41;](/sql/relational-databases/system-dynamic-management-views/sys-dm-fts-memory-buffers-transact-sql).  
  
 Las causas posibles son las siguientes:  
  
-   Si la cantidad de memoria física que está disponible durante un rellenado completo es cero, el grupo de búferes de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] podría estar consumiendo la mayor parte de la memoria física del sistema.  
  
     El proceso sqlservr.exe intenta obtener toda la memoria disponible para el grupo de búferes hasta el valor máximo de memoria del servidor configurado. Si la asignación de `max server memory` es demasiado grande, pueden producirse condiciones de memoria insuficiente y errores para asignar memoria compartida al proceso fdhost.exe.  
  
    > [!NOTE]  
    >  Durante un rellenado de texto completo en un equipo con varias CPU, puede producirse una contención de la memoria del grupo de búferes entre fdhost.exe o sqlservr.exe. La falta de memoria compartida resultante produce reintentos de lotes, una paginación excesiva de la memoria y volcados por parte del proceso fdhost.exe.  
  
     Puede resolver este problema estableciendo apropiadamente el valor `max server memory` del grupo de búferes de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Para obtener más información, vea "Estimar los requisitos de memoria del proceso de host de demonio de filtro (fdhost.exe)" más adelante en este tema. Reducir el tamaño de lote utilizado para la indización de texto completo también puede ayudar.  
  
-   Un problema de paginación  
  
     Un tamaño insuficiente del archivo de paginación, como ocurre en un sistema que tiene un archivo de paginación pequeño con un crecimiento restringido, también puede hacer que fdhost.exe o sqlservr.exe se queden sin memoria.  
  
     Si los registros de rastreo no indican ningún error relacionado con la memoria, es probable que el rendimiento sea lento debido a una paginación excesiva.  
  
  
  
### <a name="estimating-the-memory-requirements-of-the-filter-daemon-host-process-fdhostexe"></a>Estimar los requisitos de memoria del proceso de host de demonio de filtro (fdhost.exe)  
 La cantidad de memoria requerida por el proceso fdhost.exe para un rellenado depende principalmente del número de intervalos de rastreo de texto completo que utiliza, del tamaño de la memoria compartida entrante (ISM) y del número máximo de instancias de ISM.  
  
 La cantidad de memoria (en bytes) consumida por el host de demonio de filtro puede calcularse de forma aproximada utilizando esta fórmula:  
  
 *number_of_crawl_ranges* \`ism_size'*max_outstanding_isms* \* 2  
  
 Los valores predeterminados de las variables de la fórmula anterior son los siguientes:  
  
|**Variable**|**Valor predeterminado**|  
|------------------|-----------------------|  
|*number_of_crawl_ranges*|Número de CPU|  
|*ism_size*|1 MB para equipos x86<br /><br /> 4 MB, 8 MB o 16MB para equipos x64, en función de la memoria física total|  
|*max_outstanding_isms*|25 para equipos x86<br /><br /> 5 para equipos x64|  
  
 En la tabla siguiente se muestran instrucciones sobre cómo evaluar los requisitos de memoria de fdhost.exe. En las fórmulas de esta tabla se usan los valores siguientes:  
  
-   *F*, que es un cálculo de la memoria que fdhost.exe necesita (en MB).  
  
-   *T*, que es la memoria física total disponible en el sistema (en MB).  
  
-   *M*, que es el óptimo `max server memory` configuración.  
  
> [!IMPORTANT]  
>  Para obtener información esencial sobre las fórmulas, consulte <sup>1</sup>, <sup>2</sup>, y <sup>3</sup>, más adelante.  
  
|Plataforma|Evaluar los requisitos de memoria de fdhost.exe en MB —*F*<sup>1</sup>|Fórmula para calcular max server memory:*M*<sup>2</sup>|  
|--------------|---------------------------------------------------------------------|---------------------------------------------------------------|  
|x86|*F* **=** *Number of crawl ranges* **\*** 50|*M* **= mínimo (** *T* **,** 2000 **):*`F`*–** 500|  
|x64|*F* **=** *Number of crawl ranges* **\*** 10 **\*** 8|*M* **=** *T* **–** *F* **–** 500|  
  
 <sup>1</sup> si hay varios procesos de rellenado completos en curso, calcule los requisitos de memoria de fdhost.exe de cada uno de ellos por separado, como *F1*, *F2*, y así sucesivamente. Después calcule *M* como *T***–** sigma **(***F*i**)**.  
  
 <sup>2</sup> 500 MB es una estimación de la memoria requerida por otros procesos en el sistema. Si el sistema está realizando trabajo adicional, aumente este valor en consecuencia.  
  
 <sup>3</sup> . *ism_size* se supone que es 8 MB para x64 plataformas.  
  
 **Ejemplo: Evaluar los requisitos de memoria de fdhost.exe**  
  
 Este ejemplo corresponde a un equipo AMD64 que tiene 8 GB de RAM y 4 procesadores de doble núcleo. El primer cálculo evalúa la memoria que necesita fdhost.exe (*F*). El número de rangos de rastreo es `8`.  
  
 `F = 8*10*8=640`  
  
 El cálculo siguiente obtiene el valor óptimo de `max server memory`:*M*. *T*otal de memoria física disponible en este sistema en MB—*T*— es `8192`.  
  
 `M = 8192-640-500=7052`  
  
 **Ejemplo: Establecer max server memory**  
  
 Este ejemplo se utiliza la [sp_configure](/sql/relational-databases/system-stored-procedures/sp-configure-transact-sql) y [volver a configurar](/sql/t-sql/language-elements/reconfigure-transact-sql) [!INCLUDE[tsql](../../../includes/tsql-md.md)] instrucciones para establecer `max server memory` en el valor calculado para *M* en el ejemplo anterior , `7052`:  
  
```  
USE master;  
GO  
EXEC sp_configure 'max server memory', 7052;  
GO  
RECONFIGURE;  
GO  
```  
  
 **Para establecer a la opción max server memory, opción de configuración**  
  
-   [Opciones de configuración de memoria del servidor](../../database-engine/configure-windows/server-memory-server-configuration-options.md)  
  
  
  
### <a name="factors-that-can-reduce-cpu-consumption"></a>Factores que pueden reducir el consumo de CPU  
 Es de esperar que el rendimiento de los rellenados completos no sea el óptimo cuando el consumo de CPU medio sea inferior a un 30 por ciento, aproximadamente. En esta sección se discuten algunos factores que afectan al consumo de CPU.  
  
-   Una espera alta de las páginas  
  
     Para averiguar si el tiempo de espera de una página es elevado, ejecute el siguiente [!INCLUDE[tsql](../../../includes/tsql-md.md)] instrucción:  
  
    ```  
    Execute SELECT TOP 10 * FROM sys.dm_os_wait_stats ORDER BY wait_time_ms DESC;  
    ```  
  
     En la tabla siguiente se describen los tipos de espera de interés aquí.  
  
    |Tipo de espera|Descripción|Solución posible:|  
    |---------------|-----------------|-------------------------|  
    |PAGEIO_LATCH_SH (_EX o _UP)|Esto podría indicar un cuello de botella de la E/S, en cuyo caso normalmente vería también una longitud promedio de la cola del disco alta.|Al mover el índice de texto completo a un grupo de archivos diferente de un disco diferente, podría ayudar a reducir el cuello de botella de la E/S.|  
    |PAGELATCH_EX (o _UP)|Podría indicar una gran contención entre los subprocesos que están intentando escribir en el mismo archivo de base de datos.|Al agregar los archivos al grupo de archivos en el que el índice de texto completo reside podría ayudar a aliviar tal contención.|  
  
     Para obtener más información, vea [sys.dm_os_wait_stats &#40;Transact-SQL&#41;](/sql/relational-databases/system-dynamic-management-views/sys-dm-os-wait-stats-transact-sql).  
  
-   Deficiencias en el recorrido de la tabla base  
  
     Un rellenado completo examina la tabla base para generar lotes. Este recorrido de la tabla podría ser ineficaz en los escenarios siguientes:  
  
    -   Si la tabla base tiene un porcentaje alto de columnas sin filas que están siendo indizadas con índices de texto completo, el recorrido de la tabla base para generar los lotes podría constituir el cuello de botella. En este caso, podría ser de ayuda pasar los datos menores de la fila usando `varchar(max)` o `nvarchar(max)`.  
  
    -   Si la tabla base está muy fragmentada, el recorrido podría ser ineficaz. Para más información sobre cómo calcular los datos de la fila y la fragmentación de índices, vea [sys.dm_db_partition_stats &#40;Transact-SQL&#41;](/sql/relational-databases/system-dynamic-management-views/sys-dm-db-partition-stats-transact-sql) y [sys.dm_db_index_physical_stats &#40;Transact-SQL&#41;](/sql/relational-databases/system-dynamic-management-views/sys-dm-db-index-physical-stats-transact-sql).  
  
         Para reducir la fragmentación, puede reorganizar o volver a generar el índice clúster. Para obtener más información, vea [Reorganizar y volver a generar índices](../indexes/reorganize-and-rebuild-indexes.md).  
  
  
  
##  <a name="filters"></a> Solución de problemas de rendimiento lento debido a los filtros de la indización  
 Al rellenar un índice de texto completo, el motor de texto completo utiliza dos tipos de filtros: multiproceso y de un solo subproceso. Algunos documentos, como los de Word [!INCLUDE[msCoName](../../includes/msconame-md.md)] , se filtran utilizando un filtro multiproceso. Otros, como los documentos Portable Document Format (PDF) de Adobe Acrobat, se filtran por medio de filtros de un solo subproceso.  
  
 Por razones de seguridad, los procesos de host de demonio de filtro cargan los filtros. Una instancia del servidor utiliza un proceso multiproceso para todos los filtros multiproceso y un proceso de un solo subproceso para todos los filtros de un solo subproceso. Cuando un documento que utiliza un filtro multiproceso contiene un documento incrustado que utiliza un filtro de un solo subproceso, el motor de texto completo inicia un proceso de un solo subproceso para el documento incrustado. Por ejemplo, al encontrar un documento de Word que contiene un documento PDF, el motor de texto completo usa el proceso multiproceso para el contenido de Word e inicia un proceso de un solo subproceso para el contenido PDF. Sin embargo, un filtro de un solo subproceso podría no funcionar bien en este entorno y desestabilizar el proceso de filtrado. En ciertas circunstancias en las que tal incrustación es común, la desestabilización podría provocar el bloqueo del proceso de filtrado. Cuando esto ocurre, el motor de texto completo vuelve a enrutar cualquier documento con error (por ejemplo, un documento de Word que incluya contenido PDF incrustado) al proceso del filtrado de un solo subproceso. Si esto sucede con frecuencia, se produce una disminución del rendimiento del proceso de indización de texto completo.  
  
 Para solucionar este problema, marque el filtro para el documento contenedor (Word en este caso) como filtro de un solo subproceso. Puede cambiar el valor del Registro del filtro para marcar un determinado filtro como de un solo subproceso. Para marcar un filtro como un único subproceso, tiene que establecer la **ThreadingModel** valor del registro para el filtro para `Apartment Threaded`. Para obtener más información sobre los contenedores uniproceso, vea las notas del producto [Understanding and Using COM Threading Models](http://go.microsoft.com/fwlink/?LinkId=209159)(Descripción y uso de modelos de subprocesos COM).  
  
  
  
## <a name="see-also"></a>Vea también  
 [Opciones de configuración de memoria del servidor](../../database-engine/configure-windows/server-memory-server-configuration-options.md)   
 [max full-text crawl range (opción de configuración del servidor)](../../database-engine/configure-windows/max-full-text-crawl-range-server-configuration-option.md)   
 [Rellenar índices de texto completo](populate-full-text-indexes.md)   
 [Crear y administrar índices de texto completo](create-and-manage-full-text-indexes.md)   
 [sys.dm_fts_memory_buffers &#40;Transact-SQL&#41;](/sql/relational-databases/system-dynamic-management-views/sys-dm-fts-memory-buffers-transact-sql)   
 [sys.dm_fts_memory_pools &#40;Transact-SQL&#41;](/sql/relational-databases/system-dynamic-management-views/sys-dm-fts-memory-pools-transact-sql)   
 [Solucionar problemas de indización de texto completo](troubleshoot-full-text-indexing.md)  
  
  
