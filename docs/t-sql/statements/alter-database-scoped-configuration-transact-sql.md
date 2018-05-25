---
title: ALTER DATABASE SCOPED CONFIGURATION (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 05/142018
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.component: t-sql|statements
ms.reviewer: ''
ms.suite: sql
ms.technology: t-sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
f1_keywords:
- ALTER_DATABASE_SCOPED_CONFIGURATION
- ALTER_DATABASE_SCOPED_CONFIGURATION_TSQL
- DATABASE_SCOPED_CONFIGURATION_TSQL
- SCOPED_CONFIGURATION_TSQL
- SCOPED_TSQL
- ALTER_DATABASE_SCOPED_TSQL
- DATABASE_SCOPED_TSQL
helpviewer_keywords:
- ALTER DATABASE SCOPED CONFIGURATION statement
- configuration [SQL Server], ALTER DATABASE SCOPED CONFIGURATION statement
ms.assetid: 63373c2f-9a0b-431b-b9d2-6fa35641571a
caps.latest.revision: 32
author: CarlRabeler
ms.author: carlrab
manager: craigg
ms.openlocfilehash: 1fc2b483ff3a3b4a60d02c281041bb403485aaa2
ms.sourcegitcommit: 6fd8a193728abc0a00075f3e4766a7e2e2859139
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/17/2018
---
# <a name="alter-database-scoped-configuration-transact-sql"></a>ALTER DATABASE SCOPED CONFIGURATION (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

  Esta instrucción permite varios valores de configuración de base de datos en el nivel de **base de datos individual**. Esta instrucción está disponible en [!INCLUDE[sssdsfull](../../includes/sssdsfull-md.md)] y en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] a partir de [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]. Los valores son:  
  
- Borrar la caché de procedimientos.  
- Establecer el parámetro MAXDOP en un valor arbitrario (1, 2, ...) para la base de datos principal en función del valor que funciona mejor para esa base de datos concreta y establecer un valor distinto (por ejemplo, 0) para todas las bases de datos secundarias que se usan (por ejemplo, para notificar consultas).  
- Definir el modelo de estimación de la cardinalidad del optimizador de consultas independiente de la base de datos en el nivel de compatibilidad.  
- Habilitar o deshabilitar el examen de parámetros en el nivel de base de datos.
- Habilitar o deshabilitar las revisiones de optimización de consulta en el nivel de base de datos.
- Habilitar o deshabilitar la caché de identidad en el nivel de base de datos.
- Habilitar o deshabilitar un código auxiliar de plan compilado que se almacenará en caché cuando se compile un lote por primera vez.  
- Habilitar o deshabilitar la recolección de estadísticas de ejecución para los módulos de T-SQL compilados de forma nativa.
- Habilitar o deshabilitar ONLINE mediante opciones predeterminadas para las instrucciones de DDL que admiten la sintaxis ONLINE=.
- Habilitar o deshabilitar RESUMABLE mediante opciones predeterminadas para las instrucciones de DDL que admiten la sintaxis RESUMABLE=. 

 ![Icono de vínculo](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
ALTER DATABASE SCOPED CONFIGURATION  
{        
     {  [ FOR SECONDARY] SET <set_options>  }    
}  
| CLEAR PROCEDURE_CACHE  
| SET < set_options >
[;]    
  
< set_options > ::=    
{  
    MAXDOP = { <value> | PRIMARY}    
    | LEGACY_CARDINALITY_ESTIMATION = { ON | OFF | PRIMARY}    
    | PARAMETER_SNIFFING = { ON | OFF | PRIMARY}    
    | QUERY_OPTIMIZER_HOTFIXES = { ON | OFF | PRIMARY}
    | IDENTITY_CACHE = { ON | OFF }
    | OPTIMIZE_FOR_AD_HOC_WORKLOADS = { ON | OFF }
    | XTP_PROCEDURE_EXECUTION_STATISTICS = { ON | OFF } 
    | XTP_QUERY_EXECUTION_STATISTICS = { ON | OFF }    
    | ELEVATE_ONLINE = { OFF | WHEN_SUPPORTED | FAIL_UNSUPPORTED } 
    | ELEVATE_RESUMABLE = { OFF | WHEN_SUPPORTED | FAIL_UNSUPPORTED }  
}  
```  
  
## <a name="arguments"></a>Argumentos  
 
FOR SECONDARY  
 
Especifica la configuración de las bases de datos secundarias (todas las bases de datos secundarias deben tener valores idénticos).  
  
MAXDOP **=** {\<valor> | PRIMARY }  
**\<valor>**  
  
Especifica el valor predeterminado MAXDOP que se debe usar para las instrucciones. 0 es el valor predeterminado e indica que en su lugar se usará la configuración del servidor. En el ámbito de la base de datos, MAXDOP reemplaza (a menos que se establezca en 0) el **grado máximo de paralelismo** establecido en el nivel de servidor mediante sp_configure. Las sugerencias de consulta aún pueden reemplazar el valor MAXDOP con ámbito de base de datos con el fin de optimizar las consultas específicas que requieran otra configuración. Todas estas configuraciones están limitadas por el valor MAXDOP establecido para el grupo de cargas de trabajo.   

Puede utilizar la opción Grado máximo de paralelismo para limitar el número de procesadores que debe utilizarse en la ejecución de planes en paralelo. SQL Server considera los planes de ejecución en paralelo para las consultas, las operaciones de lenguaje de definición de datos (DDL) de índice, la inserción en paralelo, la modificación de columna en línea, la colección de estadísticas en paralelo y el rellenado de cursor estático y controlado por conjuntos de claves.
 
Para establecer esta opción en el nivel de instancia, vea [Establecer la opción de configuración del servidor Grado máximo de paralelismo](../../database-engine/configure-windows/configure-the-max-degree-of-parallelism-server-configuration-option.md). 

> [!TIP] 
> Para realizar esta acción en el nivel de consulta, agregue la [sugerencia de consulta](../../t-sql/queries/hints-transact-sql-query.md) **MAXDOP**.  
  
PRIMARY  
  
Solo se puede establecer para las secundarias, mientras la base de datos está en la principal, e indica que la configuración será la definida para la principal. Si cambia la configuración de la principal, el valor en las secundarias cambiará en consecuencia sin necesidad de establecer explícitamente el valor de las secundarias. **PRIMARY** es la configuración predeterminada para las secundarias.  
  
LEGACY_CARDINALITY_ESTIMATION **=** { ON | **OFF** | PRIMARY }  

Permite establecer el modelo de estimación de la cardinalidad del optimizador de consultas en SQL Server 2012 y versiones anteriores, independientemente del nivel de compatibilidad de la base de datos. El valor predeterminado es **OFF**, que establece el modelo de estimación de la cardinalidad del optimizador de consultas en función del nivel de compatibilidad de la base de datos. Establecer este valor en **ON** es equivalente a habilitar la [marca de seguimiento 9481](../../t-sql/database-console-commands/dbcc-traceon-trace-flags-transact-sql.md). 

> [!TIP] 
> Para realizar esta acción en el nivel de consulta, agregue la [sugerencia de consulta](../../t-sql/database-console-commands/dbcc-traceon-trace-flags-transact-sql.md) **QUERYTRACEON**. A partir de [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] SP1, para realizar esta acción en el nivel de consulta, agregue la [sugerencia de consulta](../../t-sql/queries/hints-transact-sql-query.md) **USE HINT** en lugar de usar la marca de seguimiento. 
  
PRIMARY  
  
Este valor solo es válido en las bases de datos secundarias mientras la base de datos se encuentra en la principal y especifica que la configuración del modelo de estimación de cardinalidad del optimizador de consultas en todas las bases de datos será el valor establecido para la principal. Si cambia la configuración en la base de datos principal para el modelo de estimación de cardinalidad del optimizador de consultas, el valor en las bases de datos secundarias cambiará en consecuencia. **PRIMARY** es la configuración predeterminada para las secundarias.  
  
PARAMETER_SNIFFING **=** { **ON** | OFF | PRIMARY}  

Habilita o deshabilita el [examen de parámetros](../../relational-databases/query-processing-architecture-guide.md#ParamSniffing). El valor predeterminado es ON. Es equivalente a la [Marca de seguimiento 4136](../../t-sql/database-console-commands/dbcc-traceon-trace-flags-transact-sql.md).   

> [!TIP] 
> Para realizar esta acción en el nivel de consulta, vea la [sugerencia de consulta](../../t-sql/queries/hints-transact-sql-query.md) **OPTIMIZE FOR UNKNOWN**. A partir de [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] SP1, para realizar esta acción en el nivel de consulta, también está disponible la [sugerencia de consulta](../../t-sql/queries/hints-transact-sql-query.md) **USE HINT**. 
  
PRIMARY  
  
Este valor solo es válido en las bases de datos secundarias mientras la base de datos se encuentra en la principal y especifica que el valor de esta configuración en todas las bases de datos secundarias será el valor establecido para la principal. Si cambia la configuración de la principal para usar el [examen de parámetros](../../relational-databases/query-processing-architecture-guide.md#ParamSniffing), el valor en las secundarias cambiará en consecuencia sin necesidad de establecer explícitamente el valor de las secundarias. Esta es la configuración predeterminada para las secundarias.  
  
QUERY_OPTIMIZER_HOTFIXES **=** { ON | **OFF** | PRIMARY }  

Habilita o deshabilita las revisiones de optimización de consulta independientemente del nivel de compatibilidad de la base de datos. El valor predeterminado es **OFF**, que deshabilita las revisiones de optimización de consulta que se publicaron después de que se introdujo el máximo nivel de compatibilidad disponible para una versión específica (posterior a RTM). Establecer este valor en **ON** es equivalente a habilitar la [marca de seguimiento 4199](../../t-sql/database-console-commands/dbcc-traceon-trace-flags-transact-sql.md).   

> [!TIP] 
> Para realizar esta acción en el nivel de consulta, agregue la [sugerencia de consulta](../../t-sql/database-console-commands/dbcc-traceon-trace-flags-transact-sql.md) **QUERYTRACEON**. A partir de [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] SP1, para realizar esta acción en el nivel de consulta, agregue la [sugerencia de consulta](../../t-sql/queries/hints-transact-sql-query.md) USE HINT en lugar de usar la marca de seguimiento.  
  
PRIMARY  
  
Este valor solo es válido en las bases de datos secundarias mientras la base de datos se encuentra en la principal y especifica que el valor de esta configuración en todas las bases de datos secundarias es el valor establecido para la principal. Si cambia la configuración de la principal, el valor en las secundarias cambia en consecuencia sin necesidad de establecer explícitamente el valor de las secundarias. Esta es la configuración predeterminada para las secundarias.  
  
CLEAR PROCEDURE_CACHE  

Borra la caché de procedimientos (plan) para la base de datos. Esto se puede ejecutar en la base de datos principal y en las secundarias.  

IDENTITY_CACHE **=** { **ON** | OFF }  

**Se aplica a**: [!INCLUDE[ssSQL17](../../includes/sssql17-md.md)] y[!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] 

Habilita o deshabilita la caché de identidad en el nivel de base de datos. El valor predeterminado es **ON**. El almacenamiento en caché de la identidad se usa para mejorar el rendimiento de INSERT en tablas con columnas de identidad. Para evitar lagunas en los valores de una columna de identidad en los casos en que el servidor se reinicia inesperadamente o conmuta por error a un servidor secundario, deshabilite la opción IDENTITY_CACHE. Esta opción es similar a la [marca de seguimiento 272](../../t-sql/database-console-commands/dbcc-traceon-trace-flags-transact-sql.md) existente, excepto en que se puede establecer en el nivel de base de datos, en lugar de hacerlo solo en el nivel de servidor.   

> [!NOTE] 
> Esta opción solo se puede establecer para PRIMARY. Para obtener más información, vea las [columnas de identidad](create-table-transact-sql-identity-property.md).  

OPTIMIZE_FOR_AD_HOC_WORKLOADS **=** { ON | **OFF** }  

**Se aplica a**: [!INCLUDE[sssdsfull](../../includes/sssdsfull-md.md)] 

Habilita o deshabilita un código auxiliar de plan compilado que se almacenará en caché cuando se compile un lote por primera vez. El valor predeterminado es OFF. Una vez que la configuración de ámbito de base de datos OPTIMIZE_FOR_AD_HOC_WORKLOADS está habilitada para una base de datos, se almacena un código auxiliar de plan compilado en caché al compilar por primera vez un lote. Los códigos auxiliares de plan tienen una superficie de memoria menor en comparación con el tamaño del plan compilado completo.  Si un lote se compila o se ejecuta de nuevo, se quitará el código auxiliar del plan compilado y se reemplazará con un plan compilado completo.

XTP_PROCEDURE_EXECUTION_STATISTICS **=** { ON | **OFF** }  

**Se aplica a**: [!INCLUDE[ssSDSFull](../../includes/sssdsfull-md.md)] 

Habilita o deshabilita la recopilación de estadísticas de ejecución a nivel de módulo para los módulos de T-SQL compilados de forma nativa en la base de datos actual. El valor predeterminado es OFF. Las estadísticas de ejecución se reflejan en [sys.dm_exec_procedure_stats](../../relational-databases/system-dynamic-management-views/sys-dm-exec-procedure-stats-transact-sql.md).

Las estadísticas de ejecución a nivel de módulo de los módulos de T-SQL compilados de forma nativa se recopilan si esta opción está activada o si se habilita la recopilación de estadísticas mediante [sp_xtp_control_proc_exec_stats](../../relational-databases/system-stored-procedures/sys-sp-xtp-control-proc-exec-stats-transact-sql.md).

XTP_QUERY_EXECUTION_STATISTICS **=** { ON | **OFF** }  

**Se aplica a**: [!INCLUDE[ssSDSFull](../../includes/sssdsfull-md.md)]

Habilita o deshabilita la recopilación de estadísticas de ejecución a nivel de instrucción para los módulos de T-SQL compilados de forma nativa en la base de datos actual. El valor predeterminado es OFF. Las estadísticas de ejecución se reflejan en [sys.dm_exec_query_stats](../../relational-databases/system-dynamic-management-views/sys-dm-exec-query-stats-transact-sql.md) y en el [Almacén de consultas](../../relational-databases/performance/monitoring-performance-by-using-the-query-store.md).

Las estadísticas de ejecución a nivel de instrucción de los módulos de T-SQL compilados de forma nativa se recopilan si esta opción está activada o si se habilita la recopilación de estadísticas mediante [sp_xtp_control_query_exec_stats](../../relational-databases/system-stored-procedures/sys-sp-xtp-control-query-exec-stats-transact-sql.md).

Para obtener información más detallada sobre la supervisión del rendimiento de los módulos de T-SQL compilados de forma nativa, vea [Supervisar el rendimiento de los procedimientos almacenados compilados de forma nativa](../../relational-databases/in-memory-oltp/monitoring-performance-of-natively-compiled-stored-procedures.md).

ELEVATE_ONLINE = { OFF | WHEN_SUPPORTED | FAIL_UNSUPPORTED }

**Se aplica a**: [!INCLUDE[ssSDSFull](../../includes/sssdsfull-md.md)] (la característica está en versión preliminar pública)

Le permite seleccionar opciones que hacen que el motor eleve automáticamente las operaciones admitidas a ONLINE. El valor predeterminado es OFF, que significa que las operaciones no se elevarán a ONLINE a menos que se especifique en la instrucción. [Sys.database_scoped_configurations](../../relational-databases/system-catalog-views/sys-database-scoped-configurations-transact-sql.md) refleja el valor actual de ELEVATE_ONLINE. Estas opciones solo se aplicarán a las operaciones que generalmente son compatibles con ONLINE.  

FAIL_UNSUPPORTED

Este valor eleva todas las operaciones DDL compatibles a ONLINE. Se producirá un error en las operaciones que no admiten la ejecución ONLINE y se generará una advertencia.

WHEN_SUPPORTED  

Este valor eleva las operaciones que admiten ONLINE. Las operaciones que no admiten ONLINE se ejecutarán sin conexión.

> [!NOTE]
> Puede invalidar la configuración predeterminada enviando una instrucción con la opción ONLINE especificada. 
 
ELEVATE_RESUMABLE= { OFF | WHEN_SUPPORTED | FAIL_UNSUPPORTED }

**Se aplica a**: [!INCLUDE[ssSDSFull](../../includes/sssdsfull-md.md)] (la característica está en versión preliminar pública)

Le permite seleccionar opciones que hacen que el motor eleve automáticamente las operaciones admitidas a RESUMABLE. El valor predeterminado es OFF, que significa que las operaciones no se elevarán a RESUMABLE a menos que se especifique en la instrucción. [Sys.database_scoped_configurations](../../relational-databases/system-catalog-views/sys-database-scoped-configurations-transact-sql.md) refleja el valor actual de ELEVATE_RESUMABLE. Estas opciones solo se aplican a las operaciones que generalmente son compatibles con RESUMABLE. 

FAIL_UNSUPPORTED

Este valor eleva todas las operaciones DDL compatibles a RESUMABLE. Se produce un error en las operaciones que no admiten la ejecución RESUMABLE y se genera una advertencia.

WHEN_SUPPORTED  

Este valor eleva las operaciones que admiten RESUMABLE. Las operaciones que no son compatibles con RESUMABLE se ejecutan como no reanudables.  

> [!NOTE]
> Puede invalidar la configuración predeterminada enviando una instrucción con la opción RESUMABLE especificada. 

##  <a name="Permissions"></a> Permissions  
 Requiere ALTER ANY DATABASE SCOPE CONFIGURATION   
en la base de datos. Este permiso se puede conceder por un usuario con permiso CONTROL en una base de datos.  
  
## <a name="general-remarks"></a>Notas generales  
 Aunque se pueden configurar bases de datos secundarias con valores de configuración de ámbito diferentes a los de su principal, en todas las bases de datos secundarias se usa la misma configuración. No se pueden configurar otros valores para bases de datos secundarias individuales.  
  
 La ejecución de esta instrucción borra la caché de procedimientos en la base de datos actual, lo que significa que se tendrán que volver a compilar todas las consultas.  
  
 Para las consultas con nombres de tres elementos, la configuración de la conexión de base de datos actual para la consulta se cumplirá, menos para los módulos SQL (como procedimientos, funciones y desencadenadores) que se compilan en el contexto de base de datos actual y, por tanto, se usan las opciones de la base de datos en la que residen.  
  
 El evento ALTER_DATABASE_SCOPED_CONFIGURATION se agrega como un evento de DDL que se puede usar para activar un desencadenador DDL. Se trata de un elemento secundario del grupo de desencadenador ALTER_DATABASE_EVENTS.  
 
 Las opciones de configuración con ámbito de base de datos se transfieren con la base de datos. Esto significa que cuando se restaura o adjunta una base de datos, se conservan las opciones de configuración existentes.
  
## <a name="limitations-and-restrictions"></a>Limitaciones y restricciones  
**MAXDOP**  
  
 La configuración granular puede invalidar las globales y Resource Governor puede limitar todas las demás opciones de MAXDOP.  La lógica para el valor MAXDOP es la siguiente:  
  
-   La sugerencia de consulta invalida tanto sp_configure como la configuración con ámbito de base de datos. Si el valor MAXDOP del grupo de recursos se establece para el grupo de cargas de trabajo:  
  
    -   Si la sugerencia de consulta se establece en 0, se reemplaza por la configuración de Resource Governor.  
  
    -   Si la sugerencia de consulta no es 0, se limita por la configuración de Resource Governor.  
  
-   La configuración con ámbito de base de datos (a menos que sea 0) invalida el valor de sp_configure a menos que haya una sugerencia de consulta y esté limitada por la configuración de Resource Governor.  
  
-   La configuración de Resource Governor reemplaza el valor de sp_configure.  
  
**QUERY_OPTIMIZER_HOTFIXES**  
  
 Cuando se usa la sugerencia QUERYTRACEON para habilitar el optimizador de consultas heredado o las revisiones del optimizador de consultas, sería una condición OR entre la sugerencia de consulta y el valor de configuración con ámbito de base de datos, lo que significa que si una de las dos está habilitada, las opciones se aplican.  
  
**GeoDR**  
  
 Las bases de datos secundarias legibles (por ejemplo, los Grupos de disponibilidad AlwaysOn y GeoReplication) usan el valor secundario comprobando el estado de la base de datos. Aunque la nueva compilación no se produce en la conmutación por error y técnicamente la nuevo base de datos principal tiene consultas que usan la configuración de la secundaria, la idea es que la configuración entre principal y secundaria solo varía cuando la carga de trabajo es diferente y, por tanto, las consultas en caché usan la configuración óptima, mientras que las consultas nuevas eligen la configuración nueva que es adecuada para ellas.  
  
**DacFx**  
  
 Como ALTER DATABASE SCOPED CONFIGURATION es una característica nueva de Azure SQL Database y SQL Server a partir de SQL Server 2016 que afecta al esquema de base de datos, las exportaciones del esquema (con o sin datos) no se pueden importar a una versión anterior de SQL Server como [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] o [!INCLUDE[ssSQLv14](../../includes/sssqlv14-md.md)]. Por ejemplo, una exportación a un [DACPAC](https://msdn.microsoft.com/library/ee210546.aspx#Anchor_3) o un [BACPAC](https://msdn.microsoft.com/library/ee210546.aspx#Anchor_4) desde una base de datos de [!INCLUDE[ssSDS](../../includes/sssds-md.md)] o [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] que usara esta nueva característica no podría importarse a un servidor de nivel inferior.  

**ELEVATE_ONLINE** 

Esta opción solo se aplica a las instrucciones de DDL que admiten la sintaxis WITH(ONLINE =. Los índices XML no se ven afectados. 

**ELEVATE_RESUMABLE**

Esta opción solo se aplica a las instrucciones de DDL que admiten la sintaxis WITH(ONLINE =. Los índices XML no se ven afectados. 

  
## <a name="metadata"></a>Metadatos  

En la vista del sistema [sys.database_scoped_configurations &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-database-scoped-configurations-transact-sql.md) se proporciona información sobre las configuraciones con ámbito en una base de datos. Las opciones de configuración con ámbito de base de datos solo se muestran en sys.database_scoped_configurations por ser invalidaciones de la configuración predeterminada de todo el servidor. En la vista del sistema [sys.configurations &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-configurations-transact-sql.md) solo se muestra la configuración de todo el servidor.  
  
## <a name="examples"></a>Ejemplos  
En estos ejemplos se muestra el uso de ALTER DATABASE SCOPED CONFIGURATION  
  
### <a name="a-grant-permission"></a>A. Conceder permiso  

En este ejemplo se concede el permiso necesario para ejecutar ALTER DATABASE SCOPED CONFIGURATION     
al usuario [Joe].  
  
```sql  
GRANT ALTER ANY DATABASE SCOPED CONFIGURATION to [Joe] ;  
```  
  
### <a name="b-set-maxdop"></a>B. Configuración de MAXDOP  

En este ejemplo se establece MAXDOP = 1 para una base de datos principal y MAXDOP = 4 para una base de datos secundaria en un escenario de replicación geográfica.  
  
```sql  
ALTER DATABASE SCOPED CONFIGURATION SET MAXDOP = 1 ;  
ALTER DATABASE SCOPED CONFIGURATION FOR SECONDARY SET MAXDOP=4 ;  
```  
  
En este ejemplo se establece MAXDOP para una base de datos secundaria de la misma forma que se establece para su base de datos principal en un escenario de replicación geográfica.  
  
```sql  
ALTER DATABASE SCOPED CONFIGURATION FOR SECONDARY SET MAXDOP=PRIMARY ;
```  
  
### <a name="c-set-legacycardinalityestimation"></a>C. Configuración de LEGACY_CARDINALITY_ESTIMATION  

En este ejemplo se establece LEGACY_CARDINALITY_ESTIMATION en ON para una base de datos secundaria en un escenario de replicación geográfica.  
  
```sql  
ALTER DATABASE SCOPED CONFIGURATION FOR SECONDARY SET LEGACY_CARDINALITY_ESTIMATION=ON ;  
```  
  
En este ejemplo se establece LEGACY_CARDINALITY_ESTIMATION para una base de datos secundaria de la misma forma que para su base de datos principal en un escenario de replicación geográfica.  
  
```sql  
ALTER DATABASE SCOPED CONFIGURATION FOR SECONDARY SET LEGACY_CARDINALITY_ESTIMATION=PRIMARY ;  
```  
  
### <a name="d-set-parametersniffing"></a>D. Configuración de PARAMETER_SNIFFING  

En este ejemplo se establece PARAMETER_SNIFFING en OFF para una base de datos principal en un escenario de replicación geográfica.  
  
```sql  
ALTER DATABASE SCOPED CONFIGURATION SET PARAMETER_SNIFFING =OFF ;  
```  
  
En este ejemplo se establece PARAMETER_SNIFFING en OFF para una base de datos principal en un escenario de replicación geográfica.  
  
```sql  
ALTER DATABASE SCOPED CONFIGURATION FOR SECONDARY SET PARAMETER_SNIFFING=OFF ;  
```  
  
En este ejemplo se establece PARAMETER_SNIFFING para una base de datos secundaria de la misma forma que en la base de datos principal en un escenario de replicación geográfica.  
  
```sql  
ALTER DATABASE SCOPED CONFIGURATION FOR SECONDARY SET PARAMETER_SNIFFING=PRIMARY ;  
```  
  
### <a name="e-set-queryoptimizerhotfixes"></a>E. Configuración de QUERY_OPTIMIZER_HOTFIXES  

Se establece QUERY_OPTIMIZER_HOTFIXES en ON para una base de datos principal en un escenario de replicación geográfica.  

```sql  
ALTER DATABASE SCOPED CONFIGURATION SET QUERY_OPTIMIZER_HOTFIXES=ON ;  
```  
  
### <a name="f-clear-procedure-cache"></a>F. Borrado de la caché de procedimientos  

En este ejemplo se borra la caché de procedimientos (solo es posible para una base de datos principal).  
  
```sql  
ALTER DATABASE SCOPED CONFIGURATION CLEAR PROCEDURE_CACHE ;  
```  

### <a name="g-set-identitycache"></a>G. Configuración de IDENTITY_CACHE

**Se aplica a**: [!INCLUDE[ssSQL17](../../includes/sssql17-md.md)] y [!INCLUDE[ssSDS](../../includes/sssds-md.md)] (la característica está en versión preliminar pública) 

En este ejemplo se deshabilita la caché de identidad.

```sql 
ALTER DATABASE SCOPED CONFIGURATION SET IDENTITY_CACHE=OFF ; 
```

### <a name="h-set-optimizeforadhocworkloads"></a>H. Configuración de OPTIMIZE_FOR_AD_HOC_WORKLOADS

**Se aplica a**: [!INCLUDE[ssSDS](../../includes/sssds-md.md)] 

En este ejemplo se habilita o deshabilita un código auxiliar de plan compilado que se almacenará en caché cuando se compile un lote por primera vez.

```sql 
ALTER DATABASE SCOPED CONFIGURATION SET OPTIMIZE_FOR_AD_HOC_WORKLOADS = ON;
```

### <a name="i--set-elevateonline"></a>I.  Establecer ELEVATE_ONLINE 

**Se aplica a**: [!INCLUDE[ssSDSFull](../../includes/sssdsfull-md.md)] (la característica está en versión preliminar pública)
 
Este ejemplo establece ELEVATE_ONLINE en FAIL_UNSUPPORTED.  tsqlCopy 

```sql
ALTER DATABASE SCOPED CONFIGURATION SET ELEVATE_ONLINE=FAIL_UNSUPPORTED ;
```  

### <a name="j-set-elevateresumable"></a>J. Establecer ELEVATE_RESUMABLE 

**Se aplica a**: [!INCLUDE[ssSDSFull](../../includes/sssdsfull-md.md)] (la característica está en versión preliminar pública)

Este ejemplo establece ELEVEATE_RESUMABLE en WHEN_SUPPORTED.  tsqlCopy 

```sql
ALTER DATABASE SCOPED CONFIGURATION SET ELEVATE_RESUMABLE=WHEN_SUPPORTED ;  
``` 

## <a name="additional-resources"></a>Recursos adicionales

### <a name="maxdop-resources"></a>Recursos de MAXDOP 
* [Grado de paralelismo](../../relational-databases/query-processing-architecture-guide.md#DOP)
* [Recommendations and guidelines for the "max degree of parallelism" configuration option in SQL Server ](https://support.microsoft.com/en-us/kb/2806535) (Recomendaciones e instrucciones para la opción de configuración "Grado máximo de paralelismo" de SQL Server) 

### <a name="legacycardinalityestimation-resources"></a>Recursos de LEGACY_CARDINALITY_ESTIMATION    
* [Estimación de cardinalidad (SQL Server)](../../relational-databases/performance/cardinality-estimation-sql-server.md)
* [Optimizar los planes de consulta con el estimador de cardinalidad de SQL Server 2014](https://msdn.microsoft.com/library/dn673537.aspx)

### <a name="parametersniffing-resources"></a>Recursos de PARAMETER_SNIFFING    
* [Examen de parámetros](../../relational-databases/query-processing-architecture-guide.md#ParamSniffing)
* ["I smell a parameter!"](https://blogs.msdn.microsoft.com/queryoptteam/2006/03/31/i-smell-a-parameter/) ("¡Huelo un parámetro!")

### <a name="queryoptimizerhotfixes-resources"></a>Recursos de QUERY_OPTIMIZER_HOTFIXES    
* [Marcas de seguimiento](../../t-sql/database-console-commands/dbcc-traceon-trace-flags-transact-sql.md)
* [SQL Server query optimizer hotfix trace flag 4199 servicing model](https://support.microsoft.com/en-us/kb/974006) (Modelo de servicios de la marca de seguimiento 4199 de revisión del optimizador de consultas de SQL Server)

### <a name="elevateonline-resources"></a>Recursos ELEVATE_ONLINE 

- [Directrices para operaciones de índices en línea](../../relational-databases/indexes/guidelines-for-online-index-operations.md) 

### <a name="elevateresumable-resources"></a>Recursos ELEVATE_RESUMABLE 

- [Directrices para operaciones de índices en línea](../../relational-databases/indexes/guidelines-for-online-index-operations.md) 
 
## <a name="more-information"></a>Más información  
 [sys.database_scoped_configurations](../../relational-databases/system-catalog-views/sys-database-scoped-configurations-transact-sql.md)   
 [sys.configurations](../../relational-databases/system-catalog-views/sys-configurations-transact-sql.md)   
 [Vistas de catálogo de archivos y bases de datos (Transact-SQL)](../../relational-databases/system-catalog-views/databases-and-files-catalog-views-transact-sql.md)   
 [Opciones de configuración de servidor (SQL Server)](../../database-engine/configure-windows/server-configuration-options-sql-server.md) [sys.configurations](../../relational-databases/system-catalog-views/sys-configurations-transact-sql.md)  
 
