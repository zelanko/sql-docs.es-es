---
title: Cómo recopila datos el almacén de consultas | Microsoft Docs
ms.custom: ''
ms.date: 11/29/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
helpviewer_keywords:
- Query Store, data collection
ms.assetid: 8d5eec36-0013-480a-9c11-183e162e4c8e
author: julieMSFT
ms.author: jrasnick
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||= azure-sqldw-latest||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: f60ded18e88d57c5a2975b567fa246923ece7ebe
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 03/30/2020
ms.locfileid: "71974360"
---
# <a name="how-query-store-collects-data"></a>Cómo recopila datos el almacén de consultas
[!INCLUDE[appliesto-ss-asdb-asdw-xxx-md](../../includes/appliesto-ss-asdb-asdw-xxx-md.md)]

El almacén de consultas de SQL Server funciona como una caja negra de datos y recopila en todo momento información de compilación y tiempo de ejecución relacionada con las consultas y los planes. Los datos relacionados con las consultas se guardan en las tablas internas y se presentan a los usuarios a través de un conjunto de vistas.
  
## <a name="views"></a>Vistas 
 En el diagrama siguiente se muestran las vistas del almacén de consultas y sus relaciones lógicas (la información de tiempo de compilación se presenta como entidades de color azul):
  
 ![Vistas de proceso del almacén de consultas](../../relational-databases/performance/media/query-store-process-2views.png "query-store-process-2views")  
**Descripciones de las vistas**  
  
|Ver|Descripción|  
|----------|-----------------|  
|**sys.query_store_query_text**|Presenta los textos de consultas únicas ejecutadas en la base de datos. Se omiten los comentarios y espacios antes y después del texto de consulta. No se omiten los comentarios y espacios dentro del texto. Cada instrucción del lote genera una entrada de texto de consulta independiente.|  
|**sys.query_context_settings**|Presenta las combinaciones únicas de configuraciones que afectan al plan con las que se ejecutan las consultas. El mismo texto de consulta ejecutado con otras configuraciones que afecten al plan genera una entrada de consulta distinta en el almacén de consultas porque `context_settings_id` forma parte de la clave de consulta.|  
|**sys.query_store_query**|Entradas de consulta de las que se realiza el seguimiento y que se aplican por separado en el almacén de consultas. Un mismo texto de consulta puede generar varias entradas de consulta si se ejecuta con otras opciones de contexto, o bien si se ejecuta fuera, en lugar de dentro de otros módulos de [!INCLUDE[tsql](../../includes/tsql-md.md)], como procedimientos almacenados y desencadenadores.|  
|**sys.query_store_plan**|Presenta el plan estimado para la consulta con las estadísticas de tiempo de compilación. El plan almacenado equivale al que se obtiene mediante `SET SHOWPLAN_XML ON`.|  
|**sys.query_store_runtime_stats_interval**|El almacén de consultas divide el tiempo en periodos (intervalos) generados de forma automática y almacena estadísticas agregadas en ese intervalo para cada plan ejecutado. El tamaño del intervalo se controla mediante la opción de configuración **Intervalo de recopilación de estadísticas** (en [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]) o `INTERVAL_LENGTH_MINUTES` con [Opciones de ALTER DATABASE SET &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql-set-options.md).|  
|**sys.query_store_runtime_stats**|Estadísticas agregadas del runtime para los planes ejecutados. Todas las métricas capturadas se expresan en forma de cuatro funciones estadísticas: Average, Minimum, Maximum y Standard Deviation.|  
  
 Para más información sobre las vistas del almacén de consultas, vea la sección "Vistas, funciones y procedimientos relacionados" de [Supervisión del rendimiento mediante el almacén de consultas](monitoring-performance-by-using-the-query-store.md). 
  
## <a name="query-processing"></a>Procesamiento de consultas
 El almacén de consultas interactúa con la canalización de procesamiento de consultas en los siguientes puntos clave:
  
1.  Cuando una consulta se compila por primera vez, el texto de la consulta y el plan inicial se envían al almacén de consultas.
  
2.  Cuando una consulta se vuelve a compilar, el plan se actualiza en el almacén de consultas. Si se crea un plan, el almacén de consultas agrega la nueva entrada de plan para la consulta y conserva los anteriores junto con sus estadísticas de ejecución.
  
3.  Tras la ejecución de la consulta, se envían estadísticas de tiempo de ejecución al almacén de consultas. El almacén de consultas mantiene precisas estadísticas agregadas para todos los planes que se ejecutan dentro del intervalo activo en ese momento. 
  
4.  Durante las fases de compilación y de comprobación para detectar una nueva compilación, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] determina si hay algún plan en el almacén de consultas que se deba aplicar para la consulta actualmente en ejecución. Si hay un plan forzado y el plan de la caché de procedimientos es distinto al forzado, la consulta se vuelve a compilar. Es lo mismo que si se aplicara PLAN HINT a esa consulta. Este proceso se produce de forma transparente para la aplicación de usuario. 
  
 En el diagrama siguiente se muestran los puntos de la integración explicados en los pasos anteriores:
  
 ![Proceso del almacén de consultas](../../relational-databases/performance/media/query-store-process-2processor.png "query-store-process-2processor") 

## <a name="remarks"></a>Observaciones
 Para minimizar la sobrecarga de E/S, los nuevos datos se capturan en memoria. Las operaciones de escritura se ponen en cola y se vacían posteriormente en el disco. La información de consulta y del plan (que se muestra como Planear el almacén en el diagrama siguiente) se vacían con una latencia mínima. Las estadísticas en tiempo de ejecución (mostradas como Estadísticas en tiempo de ejecución) se mantienen en memoria durante un período de tiempo definido con la opción `DATA_FLUSH_INTERVAL_SECONDS` de la instrucción `SET QUERY_STORE`. Puede usar el cuadro de diálogo Almacén de consultas de [!INCLUDE[ssManStudio](../../includes/ssManStudio-md.md)] para especificar un valor para **Intervalo del vaciado de datos (minutos)** , que de forma interna se convierte a segundos. 
  
 ![Plan de proceso del almacén de consultas](../../relational-databases/performance/media/query-store-process-3.png "query-store-process-3plan") 
  
 Si el sistema se bloquea o se produce un cierre mientras se usa la [marca de seguimiento 7745](../../relational-databases/performance/best-practice-with-the-query-store.md#Recovery), el almacén de consultas puede perder los datos en tiempo de ejecución que se han recopilado, pero todavía no se han conservado, hasta un período de tiempo definido con `DATA_FLUSH_INTERVAL_SECONDS`. Se recomienda el valor predeterminado de 900 segundos (15 minutos) como un equilibrio entre el rendimiento de la captura de consultas y la disponibilidad de los datos.
 
 > [!IMPORTANT] 
 > El límite **Tamaño máximo (MB)** no se aplica de forma estricta. El tamaño de almacenamiento solo se comprueba cuando el almacén de consultas escribe datos en el disco. Este intervalo lo establece el valor de **Intervalo de vaciado de datos**. Si Almacén de consultas ha infringido el límite de tamaño máximo entre las comprobaciones de tamaño de almacenamiento, pasa al modo de solo lectura. Si **Modo de limpieza basada en tamaño** está habilitado, también se desencadena el mecanismo de limpieza para aplicar el límite de tamaño máximo.
 
 > [!NOTE]
 > Si el sistema está bajo presión de memoria, es posible vaciar las estadísticas del runtime en el disco antes de lo definido con `DATA_FLUSH_INTERVAL_SECONDS`.
 
 Durante la lectura del almacén de consultas, los datos en memoria y en disco se unifican de manera transparente. 
 
 Si se termina una sesión o la aplicación cliente se reinicia o bloquea, las estadísticas de consulta no se registrarán. 
  
 ![Información del plan de proceso del almacén de consultas](../../relational-databases/performance/media/query-store-process-4planinfo.png "query-store-process-4planinfo")    

## <a name="see-also"></a>Consulte también
 [Supervisión del rendimiento mediante el Almacén de consultas](../../relational-databases/performance/monitoring-performance-by-using-the-query-store.md)  
 [Procedimiento recomendado con el almacén de consultas](../../relational-databases/performance/best-practice-with-the-query-store.md)  
 [Query Store Catalog Views (Vistas de catálogo del almacén de consultas) &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/query-store-catalog-views-transact-sql.md) 
  
  
