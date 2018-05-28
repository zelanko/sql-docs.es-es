---
title: 'Novedades de Analytics Platform System: un almacén de datos de escalabilidad horizontal'
description: Vea cuáles son las novedades en Microsoft® Analytics Platform System, un dispositivo de escalado horizontal local que hospeda el almacenamiento de datos paralelos de MPP de SQL Server.
author: mzaman1
manager: craigg
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/24/2018
ms.author: murshedz
ms.reviewer: martinle
ms.openlocfilehash: c2408e84e7ff81f54ad00a98f85cd8dce7b04131
ms.sourcegitcommit: fc3cd23685c6b9b6972d6a7bab2cc2fc5ebab5f2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/25/2018
---
# <a name="whats-new-in-analytics-platform-system-a-scale-out-mpp-data-warehouse"></a>Novedades de sistema de la plataforma de análisis, un almacén de datos MPP de escalabilidad horizontal
Vea cuáles son las novedades en las últimas actualizaciones de dispositivo para Microsoft® Analytics Platform System (APS). Puntos de acceso es un dispositivo de escalado horizontal local que hospeda el almacenamiento de datos paralelos de MPP de SQL Server. 


## <a name="aps-au7"></a>APS AU7
APS2016 es un requisito previo para actualizar a AU7. A continuación es las nuevas características de APS AU7:

### <a name="auto-create-and-auto-update-statistics"></a>Creación automática y las estadísticas de la actualización automática
APS AU7 crea y actualiza las estadísticas automáticamente, de forma predeterminada. Para actualizar la configuración de las estadísticas, los administradores pueden usar un nuevo elemento de menú de conmutador de característica en el [Configuration Manager](appliance-configuration.md#CMTasks). El [modificador de características](appliance-feature-switch.md) controla la auto-create, la actualización automática y el comportamiento de actualización asincrónica de estadísticas. También puede actualizar la configuración de las estadísticas con la [ALTER DATABASE (almacenamiento de datos paralelos)](/sql/t-sql/statements/alter-database-parallel-data-warehouse) instrucción.

### <a name="t-sql"></a>T-SQL
Seleccione @var ahora es compatible. Para obtener más información, consulte [variable local seleccione] (/ sql/t-sql/language-elements/select-local-variable-transact-sql) 

Ahora se admiten sugerencias de consulta HASH y el grupo de pedidos. Para obtener más información, consulte [Hints(Transact-SQL) - consulta] (/ sql/t-sql/consultas/sugerencias-transact-sql-query)

### <a name="feature-switch"></a>Modificador de características
APS AU7 presenta el modificador de características en [Configuration Manager](launch-the-configuration-manager.md). AutoStatsEnabled y DmsProcessStopMessageTimeoutInSeconds ahora son opciones configurables que los administradores pueden cambiar.

### <a name="known-issues"></a>Problemas conocidos
Con el software de AU7 de APS, estamos empaquetado y proporcionando la actualización de BIOS de Intel que corrige "ataques del lado de canal de ejecución especulativa" (también conocido como. Vulnerabilidades Spectre y colapso). Aunque empaqueta juntos, la actualización del BIOS se instala manualmente y no forma parte del software de APS AU7 instalar. Microsoft recomienda que todos los clientes para instalar la actualización del BIOS. Microsoft ha mide el efecto de mitigación de vigilancia de la dirección Virtual (KVAS) de Kernel, direccionamiento indirecto de tabla de página de Kernel (KPTI) y predicción de bifurcación indirecta (IBP) en diversas cargas de trabajo SQL en varios entornos y se ha encontrado una importante degradación en algunas cargas de trabajo. Le recomendamos que pruebe el efecto de rendimiento de la habilitación de la actualización del BIOS antes de implementarlas en un entorno de producción. Si el efecto de rendimiento de habilitar estas características es demasiado alto para una aplicación existente, puede considerar si aislar su aplicación de puntos de acceso de código no es de confianza que se ejecuta es una mitigación mejor para su aplicación. Consulte las instrucciones de SQL Server [aquí](https://support.microsoft.com/en-us/help/4073225/guidance-protect-sql-server-against-spectre-meltdown).

## <a name="aps-2016"></a>APS 2016
Estas son las nuevas características de 2016 de puntos de acceso:

### <a name="sql-server-2016"></a>SQL Server 2016

APS 2016 se ejecuta en la versión más reciente de SQL Server 2016 y usa el nivel de compatibilidad de base de datos predeterminado 130.  SQL Server 2016 hace posible admitir algunas de las nuevas características, como los índices secundarios para los índices de almacén de columnas agrupado y Kerberos para PolyBase. 


### <a name="t-sql"></a>T-SQL
APS 2016 admite estas mejoras de compatibilidad de T-SQL.  Estos elementos adicionales del lenguaje sea más fácil migrar de SQL Server y otros orígenes de datos. 

- [Intercalaciones de SQL de nivel de columna][] ahora se admiten además de las intercalaciones de Windows.
- [Índices no agrupados en clúster][] mejorar el rendimiento de las consultas que buscan valores específicos en el índice de almacén de columnas agrupado. 
- [SELECCIONE... EN][] 
- [sp_spaceused()][] muestra el espacio en disco utilizado o reservado en una tabla o una base de datos.
- [Tablas anchas][] soporte es el mismo que SQL Server 2016. El límite de 32K anterior para el tamaño de fila ya no existe. 

**Tipos de datos**

- [Varchar (max)][], [nvarchar (max)][] y [varbinary (max)][]. Estos tipos de datos LOB tienen un tamaño máximo de 2 GB. Para cargar estos objetos utilizan [bcp (utilidad)][]. Polybase y dwloader no admiten actualmente estos tipos de datos. 
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

- Compatibilidad con Hortonworks HDP 2.4 y HDP 2.5
- Compatibilidad con Kerberos a través de credenciales de ámbito de la base de datos
- Compatibilidad con la credencial con Blobs de almacenamiento de Azure

### <a name="install-and-upgrade-enhancements"></a>Instalación y actualización mejoras

**Las actualizaciones de arquitectura empresarial** actualizar el dispositivo existente a APS 2016 instala el firmware más reciente y las actualizaciones de controladores, que incluyen revisiones de seguridad. 

Un nuevo dispositivo de HPE o DELL incluye todas las actualizaciones más recientes más:

- Compatibilidad de procesador de última generación (Broadwell)
- Actualizar a DDR4 DIMM
- Mejorar el rendimiento DIMM

**Integración**

- Compatibilidad con el nombre de dominio completo (FQDN) totalmente permite configurar una confianza de dominio para el dispositivo. 
- Para usar FQDN, debe realizar una actualización completa y darse de alta durante la actualización. 

**Menor tiempo de inactividad** instalar o actualizar a APS 2016 es más rápido y requiere menos tiempo de inactividad que las versiones anteriores. Para reducir el tiempo de inactividad, la instalación o una actualización: 

 - Optimiza aplicar actualizaciones WSUS mediante el uso de una imagen que contiene todas las actualizaciones a través de junio de 2016
 - Aplica actualizaciones de seguridad con las actualizaciones de controladores y firmware
 - Coloca las revisiones más recientes y la utilidad de comprobación de dispositivo (PAV) en el dispositivo para que estén preparados instalar sin necesidad de descargarlos.


<!--MSDN references-->
[database compatibility level 130]:/sql/t-sql/statements/alter-database-transact-sql-compatibility-level
[Intercalaciones de SQL de nivel de columna]:/sql/relational-databases/collations/collation-and-unicode-support
[Índices no agrupados en clúster]:/sql/t-sql/statements/create-index-transact-sql
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


  

  


