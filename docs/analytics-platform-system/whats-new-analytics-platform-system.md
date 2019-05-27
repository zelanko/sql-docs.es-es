---
title: Novedades de Analytics Platform System - un almacén de datos de escalabilidad horizontal
description: Vea cuáles son las novedades de Microsoft Analytics Platform System, una aplicación de escalabilidad horizontal en el entorno local que hospeda el almacenamiento de datos paralelos de MPP de SQL Server.
author: mzaman1
manager: craigg
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 06/27/2018
ms.author: murshedz
ms.reviewer: martinle
ms.openlocfilehash: b56791e9fd59aef57c2d107e21eb76896ebb4910
ms.sourcegitcommit: 982a1dad0b58315cff7b54445f998499ef80e68d
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/23/2019
ms.locfileid: "66175045"
---
# <a name="whats-new-in-analytics-platform-system-a-scale-out-mpp-data-warehouse"></a>Novedades de Analytics Platform System, un almacén de datos MPP de escalabilidad horizontal
Vea cuáles son las novedades en las últimas actualizaciones de dispositivo de Microsoft Analytics Platform System (APS). APS es una aplicación de escalabilidad horizontal en el entorno local que hospeda el almacenamiento de datos paralelos de MPP de SQL Server. 

::: moniker range=">= aps-pdw-2016-au7 || = sqlallproducts-allversions"
<a name="h2-aps-cu7.4"></a>
## <a name="aps-cu74"></a>APS CU7.4
Fecha de publicación: mayo de 2019

### <a name="loading-large-rows-with-dwloader"></a>Carga de filas grandes con dwloader
A partir de APS CU7.4, los clientes podrán usar un nuevo dwloader para cargar las filas en las tablas que son mayores de 32 KB (32.768 bytes). El nuevo dwloader es compatible con el modificador -l que toma un valor entero entre 32768 y 33554432 (en bytes) para cargar filas mayores que 32 KB. Use esta opción solo cuando se cargan filas grandes (mayores que 32 KB) como este modificador asignará más memoria en el cliente y el servidor y puede ralentizar la carga. Puede descargar el nuevo dwloader desde [sitio de descarga](https://www.microsoft.com/download/details.aspx?id=57472).  

### <a name="hdp-30-and-31-support-with-polybase"></a>HDP 3.0 y 3.1 de soporte técnico con PolyBase
PolyBase en puntos de acceso ahora admite HDP 3.0 y 3.1 con esta actualización. Utilice la opción 7 para las versiones HDP 3.x. Para obtener más información, consulte [conectividad de PolyBase](https://docs.microsoft.com/sql/database-engine/configure-windows/polybase-connectivity-configuration-transact-sql) página.

### <a name="utf16-file-support-with-polybase"></a>Compatibilidad con archivos de UTF16 con PolyBase
PolyBase ahora admite la lectura de archivos de texto delimitado en codificación UTF16 (LE). Consulte [crear formato de archivo externo](https://docs.microsoft.com/sql/t-sql/statements/create-external-file-format-transact-sql) para obtener información detallada del programa de instalación. 

<a name="h2-aps-cu7.3"></a>
## <a name="aps-cu73"></a>APS CU7.3
Fecha de publicación: diciembre de 2018

### <a name="common-subexpression-elimination"></a>Eliminación de subexpresiones comunes
APS CU7.3 mejora el rendimiento de consultas con la eliminación de subexpresiones comunes en el optimizador de consultas SQL. La mejora de la mejora de las consultas de dos maneras. La primera ventaja es la capacidad de identificar y eliminar, las expresiones ayudan a reducir el tiempo de compilación de SQL. La ventaja de segundo y lo más importante es las operaciones de movimiento de datos para estas subexpresiones redundantes se eliminan, por tanto, el tiempo de ejecución para las consultas se convierte en más rápido. Puede encontrar una explicación detallada de esta característica [aquí](common-sub-expression-elimination.md).

### <a name="aps-informatica-connector-for-informatica-1020-published"></a>Conector de Informatica APS Informatica 10.2.0 publicado
Hemos publicado una nueva versión de conectores de Informatica para puntos de acceso que funciona con Informatica versión 10.2.0 y 10.2.0 revisión 1. Los nuevos conectores pueden descargarse desde [sitio de descarga](https://www.microsoft.com/download/details.aspx?id=57472).

#### <a name="supported-versions"></a>Versiones admitidas

| Versión APS | Informatica PowerCenter | Controlador |
|:---|:---|:---|
| APS 2016 | 9.6.1 | SQL Server Native Client 11.x |
| APS 2016 y versiones posteriores | 10.2.0, 10.2.0 1 revisión | SQL Server Native Client 11.x |

<a name="h2-aps-cu7.2"></a>
## <a name="aps-cu72"></a>APS CU7.2
Fecha de publicación: octubre de 2018

### <a name="support-for-tls-12"></a>Compatibilidad con TLS 1.2
APS CU7.2 es compatible con TLS 1.2. Equipo cliente para puntos de acceso y puntos de acceso ahora se puede establecer comunicación entre nodos para comunicarse solo a través de TLS 1.2. Herramientas como SSDT, SSIS y Dwloader instalado en los equipos cliente configurados para comunicarse solo a través de TLS 1.2, ahora pueden conectarse a puntos de acceso con TLS 1.2. De forma predeterminada, los puntos de acceso será compatible con todas las versiones TLS (1.0, 1.1 y 1.2) para compatibilidad con versiones anteriores. Si desea establecer su dispositivo APS para usar TLS 1.2 de forma estricta, puede hacerlo mediante el cambio de configuración del registro. 

Para obtener más información, consulte [configurar TLS 1.2 en AP](configure-tls12-aps.md).

### <a name="hadoop-encryption-zone-support-for-polybase"></a>Compatibilidad de zona de cifrado de Hadoop para PolyBase
Ahora, PolyBase puede comunicarse con las zonas de cifrado de Hadoop. Vea los cambios de configuración de puntos de acceso que son necesarios en [configurar la seguridad de Hadoop](polybase-configure-hadoop-security.md#encryptionzone).

### <a name="insert-select-maxdop-options"></a>Opciones de maxdop INSERT-Select
Hemos agregado un [modificador de característica](appliance-feature-switch.md) que le permite seleccionar la configuración de maxdop mayor que 1 para las operaciones insert-select. Ahora puede establecer la configuración de maxdop en 0, 1, 2 o 4. El valor predeterminado es 1.

> [!IMPORTANT]  
> Aumento de maxdop a veces puede dar lugar en las operaciones más lentas o errores de interbloqueo. Si esto sucede, cambie la configuración a maxdop 1 y vuelva a intentar la operación.

### <a name="columnstore-index-health-dmv"></a>Estado del índice de almacén de columnas DMV
Puede ver la información de estado de índice de almacén de columnas mediante **dm_pdw_nodes_db_column_store_row_group_physical_stats** dmv. Utilice la siguiente vista para determinar la fragmentación y decidir cuándo se debe volver a generar o reorganizar un índice de almacén de columnas.

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

### <a name="polybase-date-range-increase-for-orc-and-parquet-files"></a>Aumento de intervalo de fecha de PolyBase para archivos ORC y Parquet
Leer, importar y exportar tipos de datos de fecha mediante PolyBase ahora admiten fechas antes 1970-01-01 y después 2038-01-20 para los tipos de archivo ORC y Parquet.

### <a name="ssis-destination-adapter-for-sql-server-2017-as-target"></a>Adaptador de destino de SSIS para SQL Server 2017 como destino
Nuevo adaptador de destino de APS SSIS que admite SQL Server 2017 como destino de implementación puede descargarse desde [sitio de descarga](https://www.microsoft.com/download/details.aspx?id=57472).

<a name="h2-aps-cu7.1"></a>
## <a name="aps-cu71"></a>APS CU7.1
Fecha de lanzamiento: julio de 2018

### <a name="dbcc-commands-do-not-consume-concurrency-slots-behavior-change"></a>Los comandos DBCC no consumen espacios de simultaneidad (cambio de comportamiento)
APS admite un subconjunto de T-SQL [comandos DBCC](https://docs.microsoft.com/sql/t-sql/database-console-commands/dbcc-transact-sql) como [DBCC DROPCLEANBUFFERS](https://docs.microsoft.com/sql/t-sql/database-console-commands/dbcc-dropcleanbuffers-transact-sql). Anteriormente, estos comandos consumiría un [espacio de simultaneidad](https://docs.microsoft.com/sql/analytics-platform-system/workload-management?view=aps-pdw-2016-au7#concurrency-slots) reduciendo el número de cargas y consultas de usuario que se puede ejecutar. El `DBCC` comandos ahora se ejecutan en una cola local que no consumen una ranura de simultaneidad de usuario mejora el rendimiento general de la ejecución de consulta.

### <a name="replaces-some-metadata-calls-with-catalog-objects"></a>Reemplaza algunas llamadas de metadatos con los objetos de catálogo
Uso de los objetos de catálogo para las llamadas de metadatos en lugar de usar SMO ha mostrado mejora del rendimiento en puntos de acceso. A partir de CU7.1, ahora algunas de estas llamadas metadatos utilizan los objetos de catálogo predeterminada. Este comportamiento puede desactivarse por [modificador de característica](appliance-feature-switch.md) si los clientes que usan las consultas de metadatos surgen algún problema.

### <a name="bug-fixes"></a>Correcciones de errores
Hemos actualizado a SQL Server 2016 SP2 CU2 con CU7.1 APS. La actualización corrige algunos problemas que se describen a continuación.

| Título | Descripción |
|:---|:---|
| **Interbloqueo potencial de motor de tupla** |La actualización corrige una posibilidad eterno de interbloqueo en un subproceso en segundo plano distribuido transacciones y la tupla motriz. Después de instalar CU7.1, los clientes que utilizaron TF634 para detener el motor de tupla como parámetro de inicio de SQL Server o la marca de seguimiento global pueden quitarla con seguridad. | 
| **Se produce un error en determinadas consultas lag/lead** |Algunas consultas en tablas CCI con funciones anidadas lag/lead que lo haría con error se ha corregido con esta actualización. | 


<a name="h2-aps-au7"></a>
## <a name="aps-au7"></a>APS AU7
Fecha de publicación: mayo de 2018

APS 2016 es un requisito previo para actualizar a AU7. Los siguientes son las nuevas características de APS AU7:

### <a name="auto-create-and-auto-update-statistics"></a>Automático: creación y actualización automática de estadísticas
APS AU7 crea y actualiza las estadísticas automáticamente, de forma predeterminada. Para actualizar la configuración de estadísticas, los administradores pueden usar un nuevo elemento de menú de conmutador de característica en el [Configuration Manager](appliance-configuration.md#CMTasks). El [modificador de característica](appliance-feature-switch.md) controla la auto-create, la actualización automática y el comportamiento de actualización asincrónica de estadísticas. También puede actualizar la configuración de las estadísticas con la [ALTER DATABASE (almacenamiento de datos paralelos)](../t-sql/statements/alter-database-transact-sql.md?tabs=sqlpdw) instrucción.

### <a name="t-sql"></a>T-SQL
Seleccione @var ahora se admite. Para obtener más información, consulte [seleccione una variable local](/sql/t-sql/language-elements/select-local-variable-transact-sql) 

Ahora se admiten las sugerencias de consulta HASH y el grupo de pedidos. Para obtener más información, consulte [Hints(Transact-SQL) - consulta](/sql/t-sql/queries/hints-transact-sql-query)

### <a name="feature-switch"></a>Modificador de característica
APS AU7 presenta el modificador de característica en [Configuration Manager](launch-the-configuration-manager.md). AutoStatsEnabled y DmsProcessStopMessageTimeoutInSeconds ahora son opciones configurables que los administradores pueden cambiar.

### <a name="known-issues"></a>Problemas conocidos
Con el software AU7 de APS, se proporciona una actualización de BIOS de Intel que corrige un problema que se describe como *ataques de canal lateral de ejecución especulativa*. Los ataques tienen como objetivo aprovechar lo que se denomina *vulnerabilidades Spectre y Meltdown*. Aunque se empaquetan junto con puntos de acceso, la actualización del BIOS se instala manualmente y no como parte de la instalación del software AU7 APS.

Microsoft aconseja todos los clientes para instalar la actualización del BIOS. Microsoft ha medido el efecto de sombreado de dirección Virtual (KVAS) de Kernel, direccionamiento indirecto de tabla de página de Kernel (KPTI) y mitigación de predicción de ramas indirecta (IBP) en diversas cargas de trabajo SQL en diversos entornos. Las medidas encontraron una degradación significativa en algunas cargas de trabajo. En función de los resultados, la recomendación es que pruebe el efecto de rendimiento de la habilitación de la actualización del BIOS antes de implementarlos en un entorno de producción. Consulte las instrucciones de SQL Server [aquí](https://support.microsoft.com/help/4073225/guidance-protect-sql-server-against-spectre-meltdown).

::: moniker-end
::: moniker range=">= aps-pdw-2016 || = sqlallproducts-allversions"
<a name="h2-aps-au6"></a>
## <a name="aps-2016"></a>APS 2016
En esta sección se describe las nuevas características de APS 2016 AU6.

### <a name="sql-server-2016"></a>SQL Server 2016

APS AU6 se ejecuta en la versión más reciente de SQL Server 2016 y usa el nivel de compatibilidad de base de datos 130 de forma predeterminada. SQL Server 2016 habilita la compatibilidad con nuevas características, como:

- Índices secundarios para los índices de almacén de columnas agrupado.
- Protocolo Kerberos para PolyBase.

### <a name="t-sql"></a>T-SQL
APS AU6 es compatible con estas mejoras de compatibilidad de Transact-SQL.  Estos elementos adicionales del lenguaje facilitan la migración desde SQL Server y otros orígenes de datos. 

- [Intercalaciones de SQL de nivel de columna][] ahora son compatibles, además de las intercalaciones de Windows.
- [Índices no clúster en índices de almacén de columnas agrupado][] mejorar el rendimiento de las consultas que buscan valores específicos en el índice de almacén de columnas agrupado. 
- [SELECT...INTO][] 
- [sp_spaceused()][] muestra el espacio en disco utilizado o reservadas en una tabla o una base de datos.
- [Tablas anchas][] compatibilidad es igual que SQL Server 2016. El límite anterior de 32 KB para el tamaño de fila ya no existe. 

**Tipos de datos**

- [Varchar (max)][], [NVARCHAR(MAX)][] y [VARBINARY(MAX)][]. Estos tipos de datos LOB tienen un tamaño máximo de 2 GB. Para cargar estos objetos utilizan [bcp (utilidad)][]. PolyBase y dwloader no admite actualmente estos tipos de datos. 
- [SYSNAME][]
- [UNIQUEIDENTIFIER][]
- [NUMERIC][] y tipos de datos DECIMAL.

**Funciones de ventana**

- [ROWS o RANGE][] en la cláusula OVER de la instrucción SELECT.
- [FIRST_VALUE][]
- [LAST_VALUE][]
- [CUME_DIST][]
- [PERCENT_RANK][]

**Funciones de seguridad**

- [Checksum()][] y [BINARY_CHECKSUM()][]
- [HAS_PERMS_BY_NAME()][]

**Funciones adicionales**

- [NEWID()][]
- [RAND()][]

### <a name="polybasehadoop-enhancements"></a>Mejoras de PolyBase/Hadoop

- Compatibilidad con Hortonworks HDP 2.4 y 2.5 de HDP
- Compatibilidad con Kerberos a través de credenciales con ámbito de base de datos
- Compatibilidad con credenciales con Blobs de Azure Storage

### <a name="install-and-upgrade-enhancements"></a>Instalación y mejoras de actualización

**Las actualizaciones de arquitectura empresarial** actualizar el dispositivo existente para APS AU6 instala las actualizaciones de controlador, que incluyen revisiones de seguridad y el firmware más reciente. 

Una nueva aplicación de HPE o DELL incluye todas las actualizaciones más recientes plus:

- Compatibilidad con procesadores de última generación (Broadwell)
- Actualizar a DDR4 DIMM
- Rendimiento mejorado de DIMM

**Integración**

- Compatibilidad con el nombre de dominio completo (FQDN) totalmente permite configurar una confianza de dominio para el dispositivo. 
- Para usar FQDN, deberá realizar una actualización completa y darse de alta durante la actualización. 

**Menor tiempo de inactividad** instalando o actualizando a AU6 APS es más rápido y requiere menos tiempo de inactividad que en versiones anteriores. Para reducir el tiempo de inactividad, la instalación o actualización: 

 - Optimiza la aplicación de actualizaciones WSUS con una imagen que contiene todas las actualizaciones hasta junio de 2016
 - Aplica las actualizaciones de seguridad con las actualizaciones de firmware y controlador
 - Coloca las revisiones más recientes y la utilidad de comprobación de dispositivo (PAV) en el dispositivo para que estén listas para instalar sin necesidad de descargarlos.

::: moniker-end

<!--
Link references to other articles in this same GitHub repo.

The link format that starts with '/sql/what-ever/my-artlcle' is not appropriate for common links within the same repo (as most of these link are).  The first couple links have been edited to show the proper syntax, but all other links in this article need to be similarly edited.
The proper formats have at least two big advantages.  One big advantage is that the proper formats enable the OPS Build system to detect broken links at Pull Request build time, instead of only later during run time.
-->
[database compatibility level 130]: ../t-sql/statements/alter-database-transact-sql-compatibility-level.md
[Intercalaciones de SQL de nivel de columna]: ~/relational-databases/collations/collation-and-unicode-support.md

[Índices no clúster en índices de almacén de columnas agrupado]:/sql/t-sql/statements/create-index-transact-sql
[VARCHAR (MAX)]:/sql/t-sql/data-types/char-and-varchar-transact-sql
[NVARCHAR(MAX)]:/sql/t-sql/data-types/nchar-and-nvarchar-transact-sql
[VARBINARY(MAX)]:/sql/t-sql/data-types/binary-and-varbinary-transact-sql
[SYSNAME]:/sql/relational-databases/system-catalog-views/sys-types-transact-sql
[SELECT...INTO]:/sql/t-sql/queries/select-into-clause-transact-sql
[sp_spaceused()]:/sql/relational-databases/system-stored-procedures/sp-spaceused-transact-sql
[Tablas anchas]:/sql/sql-server/maximum-capacity-specifications-for-sql-server
[BULK INSERT]:/sql/t-sql/statements/bulk-insert-transact-sql
[bcp (utilidad)]:/sql/tools/bcp-utility
[UNIQUEIDENTIFIER]:/sql/t-sql/data-types/uniqueidentifier-transact-sql
[NUMERIC]:/sql/t-sql/data-types/decimal-and-numeric-transact-sql
[ROWS o RANGE]:/sql/t-sql/queries/select-over-clause-transact-sql
[FIRST_VALUE]:/sql/t-sql/functions/first-value-transact-sql
[LAST_VALUE]:/sql/t-sql/functions/last-value-transact-sql
[CUME_DIST]:/sql/t-sql/functions/cume-dist-transact-sql
[PERCENT_RANK]:/sql/t-sql/functions/percent-rank-transact-sql
[CHECKSUM()]:/sql/t-sql/functions/checksum-transact-sql
[BINARY_CHECKSUM()]:/sql/t-sql/functions/binary-checksum-transact-sql
[HAS_PERMS_BY_NAME()]:/sql/t-sql/functions/has-perms-by-name-transact-sql
[NEWID()]:/sql/t-sql/functions/newid-transact-sql
[RAND()]:/sql/t-sql/functions/rand-transact-sql


  

  


