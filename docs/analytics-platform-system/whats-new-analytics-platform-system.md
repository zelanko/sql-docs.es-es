---
title: Novedades
description: Vea las novedades de Microsoft Analytics Platform System, un dispositivo local de escalado horizontal que hospeda MPP SQL Server Parallel Data Warehouse.
author: mzaman1
manager: craigg
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 06/27/2018
ms.author: murshedz
ms.reviewer: martinle
ms.custom: seo-dt-2019
ms.openlocfilehash: faf3bd1f487fb5c850759fdde3ddecd32bdd3b1f
ms.sourcegitcommit: d818a307725983c921987749915fe1a381233d98
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/03/2020
ms.locfileid: "80625540"
---
# <a name="whats-new-in-analytics-platform-system-a-scale-out-mpp-data-warehouse"></a>Novedades de Analytics Platform System, un almacén de datos MPP de escalabilidad horizontal
Vea las novedades de las últimas actualizaciones de dispositivos para Microsoft Analytics Platform System (APS). APS es un dispositivo local de escalado horizontal que hospeda MPP SQL Server Parallel Data Warehouse. 

::: moniker range=">= aps-pdw-2016-au7 || = sqlallproducts-allversions"
<a name="h2-aps-cu7.6"></a>
## <a name="aps-cu76"></a>APS CU7.6
Fecha de lanzamiento - Abril 2020

### <a name="rename-column"></a>Cambio del nombre de columna
Después de actualizar a CU7.6, los clientes podrán cambiar el nombre de una columna de una tabla creada por el usuario. Consulte [RENAME (Transact-SQL)](https://docs.microsoft.com/sql/t-sql/statements/rename-transact-sql) para obtener sintaxis, ejemplos, limitaciones y más información.

### <a name="alter-view"></a>Alterar vista
Los clientes ahora podrán modificar las vistas. Consulte [ALTER VIEW (Transact-SQL)](https://docs.microsoft.com/sql/t-sql/statements/alter-view-transact-sql) para obtener más información.

<a name="h2-aps-cu7.5"></a>
## <a name="aps-cu75"></a>APS CU7.5
Fecha de lanzamiento - Septiembre 2019

### <a name="alter-external-data-source"></a>Modificar origen de datos externo
Los clientes podrán modificar la definición del origen de datos externo con la actualización CU7.5. Los clientes con alta disponibilidad del nodo de nombre de Hadoop ahora pueden modificar el origen de datos para cambiar los argumentos cuando se produce una conmutación por error. Para el APS, solamente la ubicación, RESOURCE_MANAGER_LOCATION y EL CREDENTIAL se pueden cambiar. Consulte Modificar origen de [datos externo](https://docs.microsoft.com/sql/t-sql/statements/alter-external-data-source-transact-sql?view=sql-server-2017) para obtener más información.

### <a name="cdh-515-and-516-support-with-polybase"></a>Compatibilidad con CDH 5.15 y 5.16 con PolyBase
PolyBase en APS con actualización CU7.5 ahora es compatible con CDH 5.15 y 5.16 versiones de distribución Hadoop desde Cloudera. Utilice la opción 6 para las versiones CDH 5.x. 

### <a name="try_convert-and-try_cast-support"></a>soporte Try_Convert y Try_Cast
CU7.5 APS ahora admite [TRY_CAST](https://docs.microsoft.com/sql/t-sql/functions/try-cast-transact-sql?view=sql-server-2017) y [TRY_CONVERT](https://docs.microsoft.com/sql/t-sql/functions/try-convert-transact-sql?view=sql-server-2017) funciones tsql. Ambas funciones devuelven un valor convertido al tipo de datos especificado si la conversión se realiza correctamente; de lo contrario, devuelve null.

<a name="h2-aps-cu7.4"></a>
## <a name="aps-cu74"></a>APS CU7.4
Fecha de lanzamiento - Mayo 2019

### <a name="loading-large-rows-with-dwloader"></a>Cargando filas grandes con dwloader
A partir de APS CU7.4, los clientes podrán utilizar un nuevo cargador de discos para cargar filas en tablas que sean mayores que 32 KB (32,768 bytes). El nuevo dwloader admite el modificador -l que toma un valor entero entre 32768 y 33554432 (en bytes) para cargar filas de más de 32 KB. Utilice esta opción únicamente al cargar filas grandes (superiores a 32 KB), ya que este modificador asignará más memoria en el cliente y el servidor y puede ralentizar las cargas. Puede descargar el nuevo dwloader desde el sitio de [descarga.](https://www.microsoft.com/download/details.aspx?id=57472)  

### <a name="hdp-30-and-31-support-with-polybase"></a>Soporte HDP 3.0 y 3.1 con PolyBase
PolyBase en APS ahora es compatible con HDP 3.0 y 3.1 con esta actualización. Utilice la opción 7 para las versiones HDP 3.x. Para obtener más información, consulte la página [de conectividad de PolyBase.](https://docs.microsoft.com/sql/database-engine/configure-windows/polybase-connectivity-configuration-transact-sql)

### <a name="utf16-file-support-with-polybase"></a>Compatibilidad con archivos UTF16 con PolyBase
PolyBase ahora admite la lectura de archivos de texto delimitados que se encuentran en codificación UTF16 (LE). Consulte Crear formato de [archivo externo](https://docs.microsoft.com/sql/t-sql/statements/create-external-file-format-transact-sql) para obtener más información sobre la configuración. 

<a name="h2-aps-cu7.3"></a>
## <a name="aps-cu73"></a>APS CU7.3
Fecha de lanzamiento - Diciembre 2018

### <a name="common-subexpression-elimination"></a>Eliminación de subexpresiones comunes
APS CU7.3 mejora el rendimiento de las consultas con la eliminación de subexpresiones comunes en el optimizador de consultas SQL. La mejora mejora las consultas de dos maneras. La primera ventaja es la capacidad de identificar y eliminar estas expresiones ayudan a reducir el tiempo de compilación de SQL. La segunda y más importante ventaja es que las operaciones de movimiento de datos para estas subexpresiones redundantes se eliminan, por lo que el tiempo de ejecución de las consultas se vuelve más rápido. La explicación detallada de esta característica se puede encontrar [aquí](common-sub-expression-elimination.md).

### <a name="aps-informatica-connector-for-informatica-1020-published"></a>Conector APS Informatica para Informatica 10.2.0 publicado
Hemos lanzado una nueva versión de conectores de Informatica para APS que funciona con Informatica versión 10.2.0 y 10.2.0 Hotfix 1. Los nuevos conectores se pueden descargar desde el sitio de [descarga.](https://www.microsoft.com/download/details.aspx?id=57472)

#### <a name="supported-versions"></a>Versiones admitidas

| Versión APS | Informatica PowerCenter | Controlador |
|:---|:---|:---|
| APS 2016 | 9.6.1 | SQL Server Native Client 11.x |
| APS 2016 y versiones posteriores | 10.2.0, 10.2.0 Hotfix 1 | SQL Server Native Client 11.x |

<a name="h2-aps-cu7.2"></a>
## <a name="aps-cu72"></a>APS CU7.2
Fecha de lanzamiento - Octubre 2018

### <a name="support-for-tls-12"></a>Compatibilidad con TLS 1.2
APS CU7.2 soporta TLS 1.2. La máquina del cliente a la comunicación intra-nodo APS y APS ahora se puede fijar para comunicar solamente sobre TLS1.2. Las herramientas como SSDT, SSIS y Dwloader instaladas en equipos cliente que están configurados para comunicarse solo a través de TLS 1.2 ahora pueden conectarse a APS mediante TLS 1.2. De forma predeterminada, APS admitirá todas las versiones TLS (1.0, 1.1 y 1.2) para la compatibilidad con versiones anteriores. Si desea configurar el dispositivo APS para que utilice estrictamente TLS 1.2, puede hacerlo cambiando la configuración del Registro. 

Para obtener más información, consulte configuración de [TLS1.2 en APS](configure-tls12-aps.md).

### <a name="hadoop-encryption-zone-support-for-polybase"></a>Compatibilidad con la zona de cifrado de Hadoop para PolyBase
PolyBase ahora puede comunicarse con las zonas de cifrado de Hadoop. Consulte Cambios de configuración de APS necesarios en la configuración de la seguridad de [Hadoop.](polybase-configure-hadoop-security.md#encryptionzone)

### <a name="insert-select-maxdop-options"></a>Insertar-Seleccionar opciones de maxdop
Hemos añadido un conmutador de [características](appliance-feature-switch.md) que le permite seleccionar la configuración de maxdop mayor que 1 para las operaciones de selección de inserción. Ahora puede establecer el ajuste maxdop en 0, 1, 2 o 4. El valor predeterminado es 1.

> [!IMPORTANT]  
> El aumento de maxdop a veces puede dar lugar a operaciones más lentas o errores de interbloqueo. Si esto ocurre, cambie la configuración a maxdop 1 y vuelva a intentar la operación.

### <a name="columnstore-index-health-dmv"></a>DMV de estado del índice ColumnStore
Puede ver la información de estado del índice del almacén de columnas mediante **dm_pdw_nodes_db_column_store_row_group_physical_stats** dmv. Utilice la vista siguiente para determinar la fragmentación y decidir cuándo volver a generar o reorganizar un índice de almacén de columnas.

```sql
create view dbo.vCS_rg_physical_stats
as 
with cte
as
(
select   tb.[name]                    AS [logical_table_name]
,        rg.[row_group_id]            AS [row_group_id]
,        rg.[state]                   AS [state]
,        rg.[state_desc]              AS [state_desc]
,        rg.[total_rows]              AS [total_rows]
,        rg.[trim_reason_desc]        AS trim_reason_desc
,        mp.[physical_name]           AS physical_name
FROM    sys.[schemas] sm
JOIN    sys.[tables] tb               ON  sm.[schema_id]          = tb.[schema_id]                             
JOIN    sys.[pdw_table_mappings] mp   ON  tb.[object_id]          = mp.[object_id]
JOIN    sys.[pdw_nodes_tables] nt     ON  nt.[name]               = mp.[physical_name]
JOIN    sys.[dm_pdw_nodes_db_column_store_row_group_physical_stats] rg      ON  rg.[object_id]     = nt.[object_id]
                                                                            AND rg.[pdw_node_id]   = nt.[pdw_node_id]
                                        AND rg.[pdw_node_id]    = nt.[pdw_node_id]                                          
)
select *
from cte;
```

### <a name="polybase-date-range-increase-for-orc-and-parquet-files"></a>Aumento del intervalo de fechas de PolyBase para archivos ORC y Parquet
La lectura, importación y exportación de tipos de datos de fecha mediante PolyBase ahora admite fechas anteriores a 1970-01-01 y posteriores a 2038-01-20 para los tipos de archivo ORC y Parquet.

### <a name="ssis-destination-adapter-for-sql-server-2017-as-target"></a>Adaptador de destino SSIS para SQL Server 2017 como destino
El nuevo adaptador de destino de SSIS de APS que admite SQL Server 2017 como destino de implementación se puede descargar desde el sitio de [descarga.](https://www.microsoft.com/download/details.aspx?id=57472)

<a name="h2-aps-cu7.1"></a>
## <a name="aps-cu71"></a>APS CU7.1
Fecha de lanzamiento - Julio 2018

### <a name="dbcc-commands-do-not-consume-concurrency-slots-behavior-change"></a>Los comandos DBCC no consumen ranuras de simultaneidad (cambio de comportamiento)
APS admite un subconjunto de los [mandatos DBCC](https://docs.microsoft.com/sql/t-sql/database-console-commands/dbcc-transact-sql) de T-SQL como [DBCC DROPCLEANBUFFERS](https://docs.microsoft.com/sql/t-sql/database-console-commands/dbcc-dropcleanbuffers-transact-sql). Anteriormente, estos comandos consumían un [espacio de simultaneidad](https://docs.microsoft.com/sql/analytics-platform-system/workload-management?view=aps-pdw-2016-au7#concurrency-slots) reduciendo el número de cargas y consultas de usuario que podían ejecutarse. Los `DBCC` comandos ahora se ejecutan en una cola local que no consumen una ranura de simultaneidad de usuario que mejora el rendimiento general de la ejecución de consultas.

### <a name="replaces-some-metadata-calls-with-catalog-objects"></a>Reemplaza algunas llamadas de metadatos por objetos de catálogo
El uso de objetos de catálogo para llamadas de metadatos en lugar de usar SMO ha demostrado una mejora del rendimiento en APS. A partir de CU7.1, algunas de estas llamadas de metadatos ahora usan objetos de catálogo de forma predeterminada. Este comportamiento se puede desactivar mediante el conmutador de [características](appliance-feature-switch.md) si los clientes que usan consultas de metadatos se ejecutan en algún problema.

### <a name="bug-fixes"></a>Corrección de errores
Hemos actualizado a SQL Server 2016 SP2 CU2 con APS CU7.1. La actualización corrige algunos problemas que se describen a continuación.

| Título | Descripción |
|:---|:---|
| **Posible bloqueo de movimiento de tuplas** |La actualización corrige una posibilidad de interbloqueo de larga data en una transacción distribuida y subproceso en segundo plano de movimiento de tupla. Después de instalar CU7.1, los clientes que usaron TF634 para detener el movimiento de tuplas como parámetro de inicio de SQL ServerSQL Server o marca de seguimiento global pueden quitarlo de forma segura. | 
| **Cierto retraso/error en la consulta de plomo** |Ciertas consultas en tablas CCI con funciones de retraso/plomo anidadas que podrían error ahora se corrigen con esta actualización. | 


<a name="h2-aps-au7"></a>
## <a name="aps-au7"></a>APS AU7
Fecha de lanzamiento - Mayo 2018

APS 2016 es un requisito previo para actualizar a AU7. Las siguientes son nuevas características en APS AU7:

### <a name="auto-create-and-auto-update-statistics"></a>Crear automáticamente y actualizar automáticamente estadísticas
APS AU7 crea y actualiza las estadísticas automáticamente, de forma predeterminada. Para actualizar la configuración de estadísticas, los administradores pueden usar un nuevo elemento de menú de modificador de características en [Configuration Manager](appliance-configuration.md#CMTasks). El modificador de [características](appliance-feature-switch.md) controla el comportamiento de creación automática, actualización automática y actualización asincrónica de las estadísticas. También puede actualizar la configuración de estadísticas con la instrucción [ALTER DATABASE (Almacenamiento de datos paralelos).](../t-sql/statements/alter-database-transact-sql.md?tabs=sqlpdw)

### <a name="t-sql"></a>T-SQL
Ahora @var se admite la opción Seleccionar. Para obtener más información, consulte [Seleccionar variable local](/sql/t-sql/language-elements/select-local-variable-transact-sql) 

Ahora se admiten las sugerencias de consulta HASH y ORDER GROUP. Para obtener más información, vea [Sugerencias (Transact-SQL) - Consulta](/sql/t-sql/queries/hints-transact-sql-query)

### <a name="feature-switch"></a>Interruptor de características
APS AU7 presenta el Feature Switch en [Configuration Manager.](launch-the-configuration-manager.md) AutoStatsEnabled y DmsProcessStopMessageTimeoutInSeconds ahora son opciones configurables que los administradores pueden cambiar.

### <a name="known-issues"></a>Problemas conocidos
Con el software APS AU7, se proporciona una actualización del BIOS DeIntel que corrige un problema descrito como ataques de canal lateral de *ejecución especulativa.* Los ataques tienen como objetivo explotar lo que se llaman *vulnerabilidades Spectre y Meltdown*. Aunque se empaqueta junto con APS, la actualización del BIOS se instala manualmente, y no como parte de la instalación del software APS AU7.

Microsoft aconseja a todos los clientes que instalen el BIOS actualizado. Microsoft ha medido el efecto del sombreado de direcciones virtuales del núcleo (KVAS), la direccionamiento indirecto de la tabla de páginas del núcleo (KPTI) y la mitigación de predicción de ramas indirectas (IBP) en varias cargas de trabajo SQL en varios entornos. Las mediciones encontraron una degradación significativa en algunas cargas de trabajo. En función de los resultados, la recomendación es que pruebe el efecto de rendimiento de habilitar la actualización del BIOS antes de implementarlos en un entorno de producción. Consulte las instrucciones de SQL Server [aquí](https://support.microsoft.com/help/4073225/guidance-protect-sql-server-against-spectre-meltdown).

::: moniker-end
::: moniker range=">= aps-pdw-2016 || = sqlallproducts-allversions"
<a name="h2-aps-au6"></a>
## <a name="aps-2016"></a>APS 2016
Esta sección describió las nuevas características para APS 2016-AU6.

### <a name="sql-server-2016"></a>SQL Server 2016

APS AU6 se ejecuta en la última versión de SQL Server 2016 y usa el nivel de compatibilidad de base de datos predeterminado 130. SQL Server 2016 permite la compatibilidad con nuevas características como:

- Datos secundarios para índices de almacén de columnas agrupados.
- Kerberos para PolyBase.

### <a name="t-sql"></a>T-SQL
APS AU6 admite estas mejoras de compatibilidad de T-SQL.  Estos elementos de lenguaje adicionales facilitan la migración desde SQL ServerSQL Server y otros orígenes de datos. 

- Ahora se admiten [las intercalaciones SQL de nivel][] de columna, además de las intercalaciones de Windows.
- [Los índices no clúster][] de los índices de almacén de columnas agrupados mejoran el rendimiento de las consultas que buscan valores específicos en el índice de almacén de columnas agrupado. 
- [SELECT...INTO][] 
- [sp_spaceused()][] muestra el espacio en disco utilizado o reservado en una tabla o base de datos.
- La compatibilidad con [tablas anchas][] es la misma que la de SQL Server 2016. El límite anterior de 32 K para el tamaño de fila ya no existe. 

**Tipos de datos**

- [VARCHAR(MAX)][], [NVARCHAR(MAX)][] y [VARBINARY(MAX)][]. Estos tipos de datos LOB tienen un tamaño máximo de 2 GB. Para cargar estos objetos, utilice [bcp Utility][]. PolyBase y dwloader no admiten actualmente estos tipos de datos. 
- [SYSNAME][]
- [Uniqueidentifier][]
- [Tipos][] de datos NUMERIC y DECIMAL.

**Funciones de ventana**

- [ROWS o RANGE][] en la cláusula OVER de la instrucción SELECT.
- [FIRST_VALUE][]
- [LAST_VALUE][]
- [CUME_DIST][]
- [PERCENT_RANK][]

**Funciones de seguridad**

- [CHECKSUM()][] y [BINARY_CHECKSUM()][]
- [HAS_PERMS_BY_NAME()][]

**Funciones adicionales**

- [NEWID()][]
- [RAND()][]

### <a name="polybasehadoop-enhancements"></a>Mejoras de PolyBase/Hadoop

- Compatibilidad con Hortonworks HDP 2.4 y HDP 2.5
- Compatibilidad con Kerberos a través de credenciales de ámbito de base de datos
- Compatibilidad con credenciales con blobs de Azure Storage

### <a name="install-and-upgrade-enhancements"></a>Mejoras de instalación y actualización

**Actualizaciones de arquitectura empresarial** La actualización del dispositivo existente a APS AU6 instala las actualizaciones de firmware y controladores más recientes, que incluyen correcciones de seguridad. 

Un nuevo dispositivo de HPE o DELL incluye todas las actualizaciones más recientes además:

- Soporte para procesadores de última generación (Broadwell)
- Actualización a DIMM DDR4
- Rendimiento DIMM mejorado

**Integración**

- La compatibilidad con el nombre de dominio completo (FQDN) permite configurar una confianza de dominio en el dispositivo. 
- Para usar el FQDN, debe realizar una actualización completa y darse de baja durante la actualización. 

**Reducción del tiempo de inactividad** La instalación o actualización a APS AU6 es más rápida y requiere menos tiempo de inactividad que las versiones anteriores. Para reducir el tiempo de inactividad, la instalación o actualización: 

 - Optimiza la aplicación de actualizaciones WSUS mediante una imagen que contiene todas las actualizaciones hasta junio de 2016
 - Aplica actualizaciones de seguridad con las actualizaciones de controlador y firmware
 - Coloca las revisiones más recientes y la utilidad de verificación del dispositivo (PAV) en el dispositivo para que estén listas para instalarlas sin necesidad de descargarlas.

::: moniker-end

<!--
Link references to other articles in this same GitHub repo.

The link format that starts with '/sql/what-ever/my-artlcle' is not appropriate for common links within the same repo (as most of these link are).  The first couple links have been edited to show the proper syntax, but all other links in this article need to be similarly edited.
The proper formats have at least two big advantages.  One big advantage is that the proper formats enable the OPS Build system to detect broken links at Pull Request build time, instead of only later during run time.
-->
[database compatibility level 130]: ../t-sql/statements/alter-database-transact-sql-compatibility-level.md
[Intercalaciones SQL a nivel de columna]: ~/relational-databases/collations/collation-and-unicode-support.md

[Los índices no agrupados en índices de almacén de columnas agrupados]:/sql/t-sql/statements/create-index-transact-sql
[VARCHAR(MAX)]:/sql/t-sql/data-types/char-and-varchar-transact-sql
[NVARCHAR(MAX)]:/sql/t-sql/data-types/nchar-and-nvarchar-transact-sql
[VARBINARY(MAX)]:/sql/t-sql/data-types/binary-and-varbinary-transact-sql
[SYSNAME]:/sql/relational-databases/system-catalog-views/sys-types-transact-sql
[SELECT...INTO]:/sql/t-sql/queries/select-into-clause-transact-sql
[sp_spaceused()]:/sql/relational-databases/system-stored-procedures/sp-spaceused-transact-sql
[Mesas anchas]:/sql/sql-server/maximum-capacity-specifications-for-sql-server
[BULK INSERT]:/sql/t-sql/statements/bulk-insert-transact-sql
[bcp (utilidad)]:/sql/tools/bcp-utility
[Uniqueidentifier]:/sql/t-sql/data-types/uniqueidentifier-transact-sql
[Numérico]:/sql/t-sql/data-types/decimal-and-numeric-transact-sql
[ROWS o RANGE]:/sql/t-sql/queries/select-over-clause-transact-sql
[FIRST_VALUE]:/sql/t-sql/functions/first-value-transact-sql
[LAST_VALUE]:/sql/t-sql/functions/last-value-transact-sql
[CUME_DIST]:/sql/t-sql/functions/cume-dist-transact-sql
[PERCENT_RANK]:/sql/t-sql/functions/percent-rank-transact-sql
[SUMA DE COMPROBACIÓN()]:/sql/t-sql/functions/checksum-transact-sql
[BINARY_CHECKSUM()]:/sql/t-sql/functions/binary-checksum-transact-sql
[HAS_PERMS_BY_NAME()]:/sql/t-sql/functions/has-perms-by-name-transact-sql
[NEWID()]:/sql/t-sql/functions/newid-transact-sql
[RAND()]:/sql/t-sql/functions/rand-transact-sql


  

  


