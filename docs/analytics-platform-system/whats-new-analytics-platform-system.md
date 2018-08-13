---
title: 'Novedades de Analytics Platform System: un almacén de datos de escalabilidad horizontal'
description: Vea cuáles son las novedades de Microsoft® Analytics Platform System, una aplicación de escalabilidad horizontal en el entorno local que hospeda el almacenamiento de datos paralelos de MPP de SQL Server.
author: mzaman1
manager: craigg
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 06/27/2018
ms.author: murshedz
ms.reviewer: martinle
ms.openlocfilehash: b4059d9460eec5cd69e6e8b4a2f2ac95af5b3d0e
ms.sourcegitcommit: 2e038db99abef013673ea6b3535b5d9d1285c5ae
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/01/2018
ms.locfileid: "39400648"
---
# <a name="whats-new-in-analytics-platform-system-a-scale-out-mpp-data-warehouse"></a>Novedades de Analytics Platform System, un almacén de datos MPP de escalabilidad horizontal
Vea cuáles son las novedades en las últimas actualizaciones de dispositivo para Microsoft® Analytics Platform System (APS). APS es una aplicación de escalabilidad horizontal en el entorno local que hospeda el almacenamiento de datos paralelos de MPP de SQL Server. 

::: moniker range=">= aps-pdw-2016-au7 || = sqlallproducts-allversions"

## <a name="aps-au7"></a>APS AU7
APS 2016 es un requisito previo para actualizar a AU7. Estas son las novedades en APS AU7:

### <a name="auto-create-and-auto-update-statistics"></a>Automático: creación y actualización automática de estadísticas
APS AU7 crea y actualiza las estadísticas automáticamente, de forma predeterminada. Para actualizar la configuración de estadísticas, los administradores pueden usar un nuevo elemento de menú de conmutador de característica en el [Configuration Manager](appliance-configuration.md#CMTasks). El [modificador de característica](appliance-feature-switch.md) controla la auto-create, la actualización automática y el comportamiento de actualización asincrónica de estadísticas. También puede actualizar la configuración de las estadísticas con la [ALTER DATABASE (almacenamiento de datos paralelos)](../t-sql/statements/alter-database-transact-sql.md?tabs=sqlpdw) instrucción.

### <a name="t-sql"></a>T-SQL
Seleccione @var ahora se admite. Para obtener más información, consulte [variable local seleccione] (/ sql/t-sql/language-elements/select-local-variable-transact-sql) 

Ahora se admiten las sugerencias de consulta HASH y el grupo de pedidos. Para obtener más información, consulte [Hints(Transact-SQL) - consulta] (/ sql/t-sql/consultas/sugerencias-transact-sql-query)

### <a name="feature-switch"></a>Modificador de característica
APS AU7 presenta el modificador de característica en [Configuration Manager](launch-the-configuration-manager.md). AutoStatsEnabled y DmsProcessStopMessageTimeoutInSeconds ahora son opciones configurables que los administradores pueden cambiar.

### <a name="known-issues"></a>Problemas conocidos
Con el software AU7 de APS, se proporciona una actualización de BIOS de Intel que corrige un problema que se describe como *ataques de canal lateral de ejecución especulativa*. Los ataques tienen como objetivo aprovechar lo que se denomina *vulnerabilidades Spectre y Meltdown*. Aunque se empaquetan junto con puntos de acceso, la actualización del BIOS se instala manualmente y no como parte de la instalación del software AU7 APS.

Microsoft aconseja todos los clientes para instalar la actualización del BIOS. Microsoft ha medido el efecto de sombreado de dirección Virtual (KVAS) de Kernel, direccionamiento indirecto de tabla de página de Kernel (KPTI) y mitigación de predicción de ramas indirecta (IBP) en diversas cargas de trabajo SQL en diversos entornos. Las medidas encontraron una degradación significativa en algunas cargas de trabajo. En función de los resultados, la recomendación es que pruebe el efecto de rendimiento de la habilitación de la actualización del BIOS antes de implementarlos en un entorno de producción. Consulte las instrucciones de SQL Server [aquí](https://support.microsoft.com/en-us/help/4073225/guidance-protect-sql-server-against-spectre-meltdown).

::: moniker-end
::: moniker range=">= aps-pdw-2016 || = sqlallproducts-allversions"

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
- [SELECCIONE... EN][] 
- [sp_spaceused()][] muestra el espacio en disco utilizado o reservadas en una tabla o una base de datos.
- [Tablas anchas][] compatibilidad es igual que SQL Server 2016. El límite anterior de 32 KB para el tamaño de fila ya no existe. 

**Tipos de datos**

- [Varchar (max)][], [nvarchar (max)][] y [varbinary (max)][]. Estos tipos de datos LOB tienen un tamaño máximo de 2 GB. Para cargar estos objetos utilizan [bcp (utilidad)][]. Polybase y dwloader no admite actualmente estos tipos de datos. 
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
- [RAND][]

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
[NVARCHAR (MAX)]:/sql/t-sql/data-types/nchar-and-nvarchar-transact-sql
[VARBINARY (MAX)]:/sql/t-sql/data-types/binary-and-varbinary-transact-sql
[SYSNAME]:/sql/relational-databases/system-catalog-views/sys-types-transact-sql
[SELECCIONE... EN]:/sql/t-sql/queries/select-into-clause-transact-sql
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
[RAND]:/sql/t-sql/functions/rand-transact-sql


  

  


