---
title: Enlazar una base de datos con tablas con optimización para memoria a un grupo de recursos de servidor | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: in-memory-oltp
ms.topic: conceptual
ms.assetid: f222b1d5-d2fa-4269-8294-4575a0e78636
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: cd163c5d3bc7a2cd9051b8d37b8127a1cc88c30b
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/18/2020
ms.locfileid: "85050350"
---
# <a name="bind-a-database-with-memory-optimized-tables-to-a-resource-pool"></a>Enlazar una base de datos con tablas con optimización para memoria a un grupo de recursos de servidor
  Un grupo de recursos de servidor representa un subconjunto de recursos físicos que se pueden regular. De forma predeterminada, las bases de datos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] están enlazadas a los recursos del grupo de recursos de servidor predeterminado y los consumen. Para proteger [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] de manera que una o más tablas optimizadas para memoria no consuman sus recursos, y evitar que otros usuarios consuman memoria que las tablas optimizadas para memoria necesitan, debe crear un grupo de recursos de servidor diferente para administrar el consumo de memoria para la base de datos con tablas optimizadas para memoria.  
  
 Una base de datos solo se puede enlazar a un grupo de recursos de servidor. Sin embargo, puede enlazar varias bases de datos al mismo grupo. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] permite enlazar una base de datos sin tablas optimizadas para memoria a un grupo de recursos de servidor, pero ello no tiene ningún efecto. Puede enlazar una base de datos a un grupo de recursos de servidor con nombre si en el futuro desea crear tablas optimizadas para memoria en la base de datos.  
  
 Para poder enlazar una base de datos a un grupo de recursos de servidor, tanto la base de datos como el grupo de recursos de servidor deben existir. El enlace surte efecto la próxima vez que la base de datos pase a estar en línea. Consulte [Database States](../databases/database-states.md) para obtener más información.  
  
 Para obtener más información acerca de los grupos de recursos de servidor, vea [Resource Governor Resource Pool](../resource-governor/resource-governor-resource-pool.md).  
  
  
## <a name="create-the-database-and-resource-pool"></a>Crear la base de datos y el grupo de recursos de servidor  
 Puede crear la base de datos y el grupo de recursos de servidor en cualquier orden. Lo que importa es que ambos existan antes de enlazar la base de datos al grupo de recursos de servidor.  
  
### <a name="create-the-database"></a>Creación de la base de datos  
 El código [!INCLUDE[tsql](../../includes/tsql-md.md)] siguiente crea una base de datos denominada IMOLTP_DB que contendrá una o varias tablas optimizadas para memoria. La ruta de acceso \<driveAndPath> debe existir antes de ejecutar este comando.  
  
```sql  
CREATE DATABASE IMOLTP_DB  
GO  
ALTER DATABASE IMOLTP_DB ADD FILEGROUP IMOLTP_DB_fg CONTAINS MEMORY_OPTIMIZED_DATA  
ALTER DATABASE IMOLTP_DB ADD FILE( NAME = 'IMOLTP_DB_fg' , FILENAME = 'c:\data\IMOLTP_DB_fg') TO FILEGROUP IMOLTP_DB_fg;  
GO  
```  
  
### <a name="determine-the-minimum-value-for-min_memory_percent-and-max_memory_percent"></a>Determinar el valor mínimo de MIN_MEMORY_PERCENT y MAX_MEMORY_PERCENT  
 Una vez que determine las necesidades de memoria para las tablas optimizadas para memoria, debe determinar qué porcentaje de memoria disponible se necesita y establecer los porcentajes de memoria en ese valor o uno superior.  
  
 **Ejemplo:**    
En este ejemplo supondremos que en sus cálculos ha determinado que las tablas y los índices optimizados para memoria necesitan 16 GB de memoria. Suponga que tiene 32 GB de memoria asignada para su uso.  
  
 A primera vista, podría parecer que necesita establecer MIN_MEMORY_PERCENT y MAX_MEMORY_PERCENT en 50 (16 es el 50 % de 32).  Sin embargo, ese valor no proporcionaría suficiente memoria a las tablas optimizadas para memoria. Si miramos la tabla siguiente ([Porcentaje de memoria disponible para tablas e índices optimizados para memoria](#percent-of-memory-available-for-memory-optimized-tables-and-indexes)), vemos que si hay 32 GB de memoria asignada, solo el 80 % está disponible para tablas e índices optimizados para memoria.  Por tanto, calculamos los porcentajes mínimo y máximo en función de la memoria disponible, no de la memoria asignada.  
  
 `memoryNeedeed = 16`   
 `memoryCommitted = 32`   
 `availablePercent = 0.8`   
 `memoryAvailable = memoryCommitted * availablePercent`   
 `percentNeeded = memoryNeeded / memoryAvailable`  
  
 Es decir, en números reales sería:   
`percentNeeded = 16 / (32 * 0.8) = 16 / 25.6 = 0.625`  
  
 Necesita al menos el 62,5 % de la memoria disponible para satisfacer el requisito de 16 GB de las tablas y los índices optimizados para memoria.  Puesto que los valores de MIN_MEMORY_PERCENT y MAX_MEMORY_PERCENT deben ser enteros, los estableceremos como mínimo en el 63 %.  
  
### <a name="create-a-resource-pool-and-configure-memory"></a>Crear un grupo de recursos de servidor y configurar la memoria  
 A la hora de configurar memoria para las tablas optimizadas para memoria, el planeamiento de capacidad debe realizarse en función de MIN_MEMORY_PERCENT, no de MAX_MEMORY_PERCENT.  Vea [ALTER RESOURCE POOL &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-resource-pool-transact-sql) para obtener más información sobre MIN_MEMORY_PERCENT y MAX_MEMORY_PERCENT. Esto proporciona una disponibilidad de memoria más predecible en las tablas optimizadas para memoria, ya que MIN_MEMORY_PERCENT produce presión de memoria en otros grupos de recursos de servidor para asegurarse de que se respeta. Para asegurarse de que hay memoria disponible e impedir condiciones de memoria insuficiente, los valores de MIN_MEMORY_PERCENT y MAX_MEMORY_PERCENT deben ser iguales. Vea la tabla [Porcentaje de memoria disponible para tablas e índices optimizados para memoria](#percent-of-memory-available-for-memory-optimized-tables-and-indexes) de abajo para conocer el porcentaje de memoria disponible para las tablas optimizadas para memoria según la cantidad de memoria asignada.  
  
 Vea [Prácticas recomendadas: usar OLTP en memoria en un entorno de máquinas virtuales](../../database-engine/using-in-memory-oltp-in-a-vm-environment.md) para obtener más información sobre cómo trabajar en un entorno de máquinas virtuales.  
  
 El siguiente código [!INCLUDE[tsql](../../includes/tsql-md.md)] crea un grupo de recursos de servidor denominado Pool_IMOLTP con la mitad de memoria disponible para su uso.  Una vez creado el grupo, hay que reconfigurar el Regulador de recursos para incluir Pool_IMOLTP.  
  
```sql  
-- set MIN_MEMORY_PERCENT and MAX_MEMORY_PERCENT to the same value  
CREATE RESOURCE POOL Pool_IMOLTP   
  WITH   
    ( MIN_MEMORY_PERCENT = 63,   
    MAX_MEMORY_PERCENT = 63 );  
GO  
  
ALTER RESOURCE GOVERNOR RECONFIGURE;  
GO  
```  
  
## <a name="bind-the-database-to-the-pool"></a>Enlazar la base de datos al grupo  
 Use la función del sistema `sp_xtp_bind_db_resource_pool` para enlazar la base de datos al grupo de recursos de servidor. La función utiliza dos parámetros: el nombre de la base de datos y el nombre del grupo de recursos de servidor.  
  
 El siguiente código [!INCLUDE[tsql](../../includes/tsql-md.md)] define un enlace de la base de datos IMOLTP_DB con el grupo de recursos de servidor Pool_IMOLTP. El enlace no surte efecto hasta que la base de datos pase a estar en línea.  
  
```sql  
EXEC sp_xtp_bind_db_resource_pool 'IMOLTP_DB', 'Pool_IMOLTP'  
GO  
```  
  
 La función del sistema sp_xtp_bind_db_resource_pool usa dos parámetros de cadena: database_name y pool_name.  
  
## <a name="confirm-the-binding"></a>Confirmar el enlace  
 Confirme el enlace, teniendo en cuenta el identificador del grupo de recursos de servidor para IMOLTP_DB. No puede ser NULL.  
  
```sql  
SELECT d.database_id, d.name, d.resource_pool_id  
FROM sys.databases d  
GO  
```  
  
## <a name="make-the-binding-effective"></a>Activar el enlace  
 Debe poner la base de datos sin conexión y volver a ponerla en línea después de enlazarla al grupo de recursos de servidor para que el enlace surta efecto. Si la base de datos se enlazó a otro grupo diferente, esto quita la memoria asignada del grupo de recursos de servidor anterior y las asignaciones de memoria para la tabla y los índices optimizados para memoria provendrán ahora del grupo de recursos de servidor recién enlazado a la base de datos.  
  
```sql  
USE master  
GO  
  
ALTER DATABASE IMOLTP_DB SET OFFLINE  
GO  
ALTER DATABASE IMOLTP_DB SET ONLINE  
GO  
  
USE IMOLTP_DB  
GO  
```  
  
 Ahora, la base de datos está enlazada al grupo de recursos de servidor.  
  
## <a name="change-min-memory-percent-and-max-memory-percent-on-an-existing-pool"></a>Cambiar el porcentaje de memoria mínima y el porcentaje máximo de memoria en un grupo existente  
 Si agrega memoria adicional al servidor o si cambia la cantidad de memoria necesaria para las tablas optimizadas para memoria, puede ser necesario modificar el valor de MIN_MEMORY_PERCENT y MAX_MEMORY_PERCENT. Los pasos siguientes muestran cómo modificar el valor de MIN_MEMORY_PERCENT y MAX_MEMORY_PERCENT en un grupo de recursos de servidor. Vea la próxima sección para obtener información sobre qué valores se deben usar para MIN_MEMORY_PERCENT y MAX_MEMORY_PERCENT.  Vea el tema [Prácticas recomendadas: usar OLTP en memoria en un entorno de máquinas virtuales](../../database-engine/using-in-memory-oltp-in-a-vm-environment.md) para obtener más información.  
  
1.  Utilice `ALTER RESOURCE POOL` para cambiar el valor de MIN_MEMORY_PERCENT y MAX_MEMORY_PERCENT.  
  
2.  Use `ALTER RESURCE GOVERNOR` para reconfigurar el regulador de recursos con los nuevos valores.  
  
 **Código de ejemplo**  
  
```sql  
ALTER RESOURCE POOL Pool_IMOLTP  
WITH  
     ( MIN_MEMORY_PERCENT = 70,  
       MAX_MEMORY_PERCENT = 70 )   
GO  
  
-- reconfigure the Resource Governor  
ALTER RESOURCE GOVERNOR RECONFIGURE  
GO  
```  
  
## <a name="percent-of-memory-available-for-memory-optimized-tables-and-indexes"></a>Porcentaje de memoria disponible para tablas e índices optimizados para memoria  
 Si asigna una base de datos con tablas optimizadas para memoria y una carga de trabajo de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] al mismo grupo de recursos de servidor, el regulador de recursos establece un umbral interno para uso de [!INCLUDE[hek_2](../../../includes/hek-2-md.md)] de modo que los usuarios del grupo no experimenten conflictos al usar el grupo. En general, el umbral para el uso de [!INCLUDE[hek_2](../../../includes/hek-2-md.md)] es aproximadamente el 80 % del valor del grupo. En la tabla siguiente se muestran los umbrales reales para diversos tamaños de memoria.  
  
 Al crear un grupo de recursos de servidor dedicado para la base de datos de [!INCLUDE[hek_2](../../../includes/hek-2-md.md)] , debe evaluar cuánta memoria física necesita para las tablas en memoria después de tener en cuenta las versiones de filas y el aumento de datos. Una vez que se calcula la memoria necesaria, se crea un grupo de recursos de sistema con un porcentaje de la memoria de destino de confirmación para la instancia de SQL como se refleja en la columna ' committed_target_kb ' en la DMV `sys.dm_os_sys_info` (vea [sys. dm_os_sys_info](/sql/relational-databases/system-dynamic-management-views/sys-dm-os-sys-info-transact-sql)). Por ejemplo, puede crear un grupo de recursos de servidor P1 con el 40 % de la memoria total disponible para la instancia. Fuera de este 40 %, el motor de [!INCLUDE[hek_2](../../../includes/hek-2-md.md)] obtiene un porcentaje inferior para almacenar los datos de [!INCLUDE[hek_2](../../../includes/hek-2-md.md)] .  Esto se hace para asegurarse de que [!INCLUDE[hek_2](../../../includes/hek-2-md.md)] no usa toda la memoria de este grupo.  Este valor del porcentaje menor depende de la memoria confirmada de destino. En la siguiente tabla se describe la memoria disponible para la base de datos de [!INCLUDE[hek_2](../../../includes/hek-2-md.md)] en un grupo de recursos de servidor (designado o predeterminado) antes de que se genere un error de OOM.  
  
|Memoria asignada de destino|Porcentaje disponible para tablas en memoria|  
|-----------------------------|---------------------------------------------|  
|<= 8 GB|70%|  
|<= 16 GB|75 %|  
|<= 32 GB|80 %|  
|\<= 96 GB|85%|  
|>96 GB|90%|  
  
 Por ejemplo, si la "memoria confirmada de destino" es de 100 GB y calcula que las tablas e índices optimizados para memoria necesitan 60 GB de memoria, puede crear un grupo de recursos de servidor con MAX_MEMORY_PERCENT = 67 (60 GB necesarios / 0,90 = 66,667 GB - redondear hasta 67 GB; 67 GB / 100 GB instalados = 67 %) para garantizar que los objetos de [!INCLUDE[hek_2](../../../includes/hek-2-md.md)] tengan los 60 GB que necesitan.  
  
 Una vez que una base de datos se ha enlazado a un grupo de recursos de servidor con nombre, utilice la consulta siguiente para ver las asignaciones de memoria en distintos grupos de recursos de servidor.  
  
```sql  
SELECT pool_id  
     , Name  
     , min_memory_percent  
     , max_memory_percent  
     , max_memory_kb/1024 AS max_memory_mb  
     , used_memory_kb/1024 AS used_memory_mb   
     , target_memory_kb/1024 AS target_memory_mb  
   FROM sys.dm_resource_governor_resource_pools  
```  
  
 Esta salida de ejemplo muestra que la memoria usada por los objetos optimizados para memoria es de 1356 MB en el grupo de recursos de servidor, PoolIMOLTP, con un límite superior de 2307 MB. Este límite superior controla la memoria total que el usuario puede emplear y los objetos del sistema optimizados para memoria asignados a este grupo.  
  
 **Salida de ejemplo**   
Esta salida es de la base de datos y las tablas que hemos creado antes.  
  
```  
pool_id     Name        min_memory_percent max_memory_percent max_memory_mb used_memory_mb target_memory_mb  
----------- ----------- ------------------ ------------------ ------------- -------------- ----------------   
1           internal    0                  100                3845          125            3845  
2           default     0                  100                3845          32             3845  
259         PoolIMOLTP 0                  100                3845          1356           2307  
```  
  
 Para obtener más información, vea [sys.dm_resource_governor_resource_pools (Transact-SQL)](/sql/relational-databases/system-dynamic-management-views/sys-dm-resource-governor-resource-pools-transact-sql).  
  
 Si no enlaza la base de datos a un grupo de recursos de servidor con nombre, se enlaza al grupo "default". Puesto que [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usa el grupo de recursos de servidor predeterminado para la mayoría de las demás asignaciones, no podrá supervisar con precisión la memoria usada por las tablas optimizadas para memoria mediante la DMV sys.dm_resource_governor_resource_pools para la base de datos de interés.  
  
## <a name="see-also"></a>Consulte también  
 [Sys. sp_xtp_bind_db_resource_pool &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sys-sp-xtp-bind-db-resource-pool-transact-sql)   
 [Sys. sp_xtp_unbind_db_resource_pool &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sys-sp-xtp-unbind-db-resource-pool-transact-sql)   
 [Regulador de recursos](../resource-governor/resource-governor.md)   
 [Grupo de recursos de servidor del regulador de recursos](../resource-governor/resource-governor-resource-pool.md)   
 [Crear un grupo de recursos](../resource-governor/create-a-resource-pool.md)   
 [Cambiar la configuración del grupo de recursos](../resource-governor/change-resource-pool-settings.md)   
 [Eliminar un grupo de recursos de servidor](../resource-governor/delete-a-resource-pool.md)  
  
  
