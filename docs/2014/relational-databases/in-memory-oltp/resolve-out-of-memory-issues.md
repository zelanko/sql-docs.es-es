---
title: Resolver problemas de memoria insuficiente | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine-imoltp
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: f855e931-7502-44bd-8a8b-b8543645c7f4
caps.latest.revision: 15
author: CarlRabeler
ms.author: carlrab
manager: craigg
ms.openlocfilehash: 2e866c2899ff4172e969cba97e4b10f1ce0fac3a
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/02/2018
ms.locfileid: "37253987"
---
# <a name="resolve-out-of-memory-issues"></a>Resolver problemas de memoria insuficiente
  [!INCLUDE[hek_1](../../includes/hek-1-md.md)] usa más memoria y de maneras diferentes que [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Es posible que la cantidad de memoria que instaló y asignó para [!INCLUDE[hek_2](../../includes/hek-2-md.md)] no sea suficiente para sus necesidades en crecimiento. En ese caso, podría quedarse sin memoria. En este tema se describe cómo recuperarse de una situación de OOM (memoria insuficiente). Vea [Supervisar y solucionar problemas del uso de la memoria](monitor-and-troubleshoot-memory-usage.md) para obtener instrucciones específicas que pueden ayudarle a evitar muchas situaciones de memoria insuficiente.  
  
## <a name="covered-in-this-topic"></a>Las secciones de este tema son:  
  
|Tema|Información general|  
|-----------|--------------|  
|[Resolver errores de restauración de bases de datos debidos a memoria insuficiente](resolve-out-of-memory-issues.md#bkmk_resolverecoveryfailures)|Se indica lo que debe hacer si aparece el mensaje de error "Error en la operación de restauración para la base de datos '*\<nombreDeBaseDeDatos>*' debido a memoria insuficiente en el grupo de recursos de servidor '*\<nombreDeGrupoDeRecursos>*'".|  
|[Resolver el impacto de las condiciones de memoria insuficiente u OOM en la carga de trabajo](resolve-out-of-memory-issues.md#bkmk_recoverfromoom)|Se describe lo que hay que hacer si percibe que las condiciones de memoria insuficiente están afectando negativamente al rendimiento.|  
|[Resolver los errores de asignación de páginas debidos a memoria insuficiente cuando hay suficiente memoria disponible](resolve-out-of-memory-issues.md#bkmk_pageallocfailure)|Se indica lo que debe hacer si aparece el mensaje de error "No se permiten asignaciones de páginas para la base de datos '*\<nombreDeBaseDeDatos>*' debido a memoria insuficiente en el grupo de recursos '*\<nombreDeGrupoDeRecursos>*'". …" cuando hay suficiente memoria disponible para la operación.|  
  
##  <a name="bkmk_resolveRecoveryFailures"></a> Resolver errores de restauración de bases de datos debidos a memoria insuficiente  
 Cuando intente restaurar una base de datos, es posible que obtenga el mensaje de error: "Error en la operación de restauración para la base de datos '*\<NombreBasedeDatos>*' debido a que la memoria es insuficiente en el grupo de recursos '*\<NombreGrupoRecursos>*'". Antes de poder restaurar correctamente la base de datos, debe resolver el problema de memoria insuficiente aumentando la memoria disponible.  
  
 Para resolver el error de recuperación debido a memoria insuficiente, aumente la memoria disponible mediante alguno de estos medios (o todos ellos) para incrementar temporalmente la memoria disponible para la operación de recuperación.  
  
-   Cierre provisionalmente las aplicaciones en ejecución.   
    Al cerrar una o varias aplicaciones en ejecución, como Visual Studio, Internet Explorer, OneNote y otras, dejará libre la memoria que están usando para la operación de restauración. Puede reiniciarlas una vez haya completado correctamente la restauración.  
  
-   Aumente el valor de MAX_MEMORY_PERCENT.   
    Este fragmento de código cambia el valor MAX_MEMORY_PERCENT para el grupo de recursos de servidor PoolHk y lo establece en el 70 % de la memoria instalada.  
  
    > [!IMPORTANT]  
    >  Si el servidor se está ejecutando en una máquina virtual y no está dedicado, establezca el valor de MIN_MEMORY_PERCENT en el mismo valor que MAX_MEMORY_PERCENT.   
    > Vea el tema [Prácticas recomendadas: usar OLTP en memoria en un entorno de máquinas virtuales](../../database-engine/using-in-memory-oltp-in-a-vm-environment.md) para obtener más información.  
  
    ```tsql  
  
    -- disable resource governor  
    ALTER RESOURCE GOVERNOR DISABLE  
  
    -- change the value of MAX_MEMORY_PERCENT  
    ALTER RESOURCE POOL PoolHk  
    WITH  
         ( MAX_MEMORY_PERCENT = 70 )  
    GO  
  
    -- reconfigure the Resource Governor  
    --    RECONFIGURE enables resource governor  
    ALTER RESOURCE GOVERNOR RECONFIGURE  
    GO  
  
    ```  
  
     Para obtener información sobre los valores máximos para MAX_MEMORY_PERCENT, vea la sección del tema [Porcentaje de memoria disponible para tablas e índices optimizados para memoria](bind-a-database-with-memory-optimized-tables-to-a-resource-pool.md#bkmk_PercentAvailable).  
  
-   Reconfigurar la **memoria máxima del servidor**.  
    Para obtener información sobre la configuración de la **memoria máxima del servidor** see the topic [Optimizar el rendimiento del servidor mediante las opciones de configuración de memoria](http://technet.microsoft.com/library/ms177455\(v=SQL.105\).aspx).  
  
##  <a name="bkmk_recoverFromOOM"></a> Resolver el impacto de las condiciones de memoria insuficiente u OOM en la carga de trabajo  
 Evidentemente, es mejor no verse en una situación de memoria insuficiente u OOM. Un planeamiento y supervisión adecuados puede ayudar a evitar situaciones OOM. Aún así, incluso el mejor planeamiento no siempre puede prever lo que sucede en realidad y podría terminar con un problema de memoria insuficiente u OOM. Hay dos pasos para recuperarse de una situación OOM:  
  
1.  [Abrir una DAC (conexión de administrador dedicada)](resolve-out-of-memory-issues.md#bkmk_opendac)  
  
2.  [Tomar una acción correctora](resolve-out-of-memory-issues.md#bkmk_takecorrectiveaction)  
  
###  <a name="bkmk_openDAC"></a> Abrir una DAC (conexión de administrador dedicada)  
 Microsoft SQL Server ofrece una conexión de administrador dedicada (DAC). La DAC permite a los administradores obtener acceso a una instancia en ejecución del motor de base de datos de SQL Server para solucionar problemas en el servidor, aunque el servidor no responda a otras conexiones de cliente. La DAC está disponible a través de la utilidad `sqlcmd` y SQL Server Management Studio (SSMS).  
  
 Para obtener información sobre cómo utilizar `sqlcmd` y la DAC, vea [Usar una conexión de administrador dedicada](http://msdn.microsoft.com/library/ms189595\(v=sql.100\).aspx/css). Para obtener información sobre cómo utilizar la DAC a través de SSMS, vea [Cómo utilizar la conexión de administrador dedicada con SQL Server Management Studio](http://msdn.microsoft.com/library/ms178068.aspx).  
  
###  <a name="bkmk_takeCorrectiveAction"></a> Tomar una acción correctora  
 Para resolver la situación OOM, deberá liberar memoria existente reduciendo su uso u obtener más memoria disponible para las tablas en memoria.  
  
#### <a name="free-up-existing-memory"></a>Libere memoria existente  
  
##### <a name="delete-non-essential-memory-optimized-table-rows-and-wait-for-garbage-collection"></a>Elimine las filas que no sean esenciales de la tabla con optimización para memoria y espere a la recolección de elementos no utilizados  
 Puede quitar filas no esenciales de una tabla con optimización para memoria. El recolector de elementos no utilizados devuelve la memoria que usaban estas filas a la memoria disponible. . El motor de OLTP en memoria recopila filas de elementos no utilizados de forma intensa. Sin embargo, una transacción de ejecución prolongada puede impedir la recolección de elementos no utilizados. Por ejemplo, si hay una transacción que se ejecuta durante 5 minutos, no se pueden recopilar las versiones de filas creadas con las operaciones de actualización o eliminación mientras la transacción estaba activa.  
  
##### <a name="move-one-or-more-rows-to-a-disk-based-table"></a>Mover una o varias filas a una tabla basada en disco  
 Los siguientes artículos de TechNet proporcionan instrucciones para mover filas de una tabla optimizada para memoria a una tabla basada en disco.  
  
-   [Creación de particiones en el nivel de aplicación](http://technet.microsoft.com/library/dn296452\(v=sql.120\).aspx)  
  
-   [Patrón de aplicación para crear particiones de tablas con optimización para memoria](http://technet.microsoft.com/library/dn133171\(v=sql.120\).aspx)  
  
#### <a name="increase-available-memory"></a>Aumente la cantidad de memoria disponible  
  
##### <a name="increase-value-of-maxmemorypercent-on-the-resource-pool"></a>Aumente el valor de MAX_MEMORY_PERCENT en el grupo de recursos de servidor  
 Si no ha creado un grupo de recursos de servidor con nombre para las tablas en memoria, debe hacerlo y enlazar las bases de datos de [!INCLUDE[hek_2](../../includes/hek-2-md.md)] al mismo. Vea el tema [Enlazar una base de datos con tablas con optimización para memoria a un grupo de recursos de servidor](bind-a-database-with-memory-optimized-tables-to-a-resource-pool.md) para obtener instrucciones sobre cómo crear y enlazar sus bases de datos de [!INCLUDE[hek_2](../../includes/hek-2-md.md)] a un grupo de recursos.  
  
 Si la base de datos de [!INCLUDE[hek_2](../../includes/hek-2-md.md)] está enlazada a un grupo de recursos de servidor, es posible que pueda aumentar el porcentaje de memoria a la que puede tener acceso el grupo. Vea el subtema [Cambiar MIN_MEMORY_PERCENT y MAX_MEMORY_PERCENT en un grupo existente](bind-a-database-with-memory-optimized-tables-to-a-resource-pool.md#bkmk_ChangeAllocation) para obtener instrucciones sobre cómo cambiar el valor de MIN_MEMORY_PERCENT y MAX_MEMORY_PERCENT de un grupo de recursos.  
  
 Aumente el valor de MAX_MEMORY_PERCENT.   
Este fragmento de código cambia el valor MAX_MEMORY_PERCENT para el grupo de recursos de servidor PoolHk y lo establece en el 70 % de la memoria instalada.  
  
> [!IMPORTANT]  
>  Si el servidor se está ejecutando en una máquina virtual y no está dedicado, establezca el valor de MIN_MEMORY_PERCENT en el mismo valor que MAX_MEMORY_PERCENT.   
> Vea el tema [Prácticas recomendadas: usar OLTP en memoria en un entorno de máquinas virtuales](../../database-engine/using-in-memory-oltp-in-a-vm-environment.md) para obtener más información.  
  
```tsql  
  
-- disable resource governor  
ALTER RESOURCE GOVERNOR DISABLE  
  
-- change the value of MAX_MEMORY_PERCENT  
ALTER RESOURCE POOL PoolHk  
WITH  
     ( MAX_MEMORY_PERCENT = 70 )  
GO  
  
-- reconfigure the Resource Governor  
--    RECONFIGURE enables resource governor  
ALTER RESOURCE GOVERNOR RECONFIGURE  
GO  
  
```  
  
 Para obtener información sobre los valores máximos para MAX_MEMORY_PERCENT, vea la sección del tema [Porcentaje de memoria disponible para tablas e índices optimizados para memoria](bind-a-database-with-memory-optimized-tables-to-a-resource-pool.md#bkmk_PercentAvailable).  
  
##### <a name="install-additional-memory"></a>Instale memoria adicional  
 En última instancia, si es posible, la mejor solución es instalar memoria física adicional. Si lo hace, recuerde que seguramente podrá aumentar también el valor de MAX_MEMORY_PERCENT (vea el subtema [Cambiar MIN_MEMORY_PERCENT y MAX_MEMORY_PERCENT en un grupo existente](bind-a-database-with-memory-optimized-tables-to-a-resource-pool.md#bkmk_ChangeAllocation)), ya que [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] probablemente no necesitará más memoria, lo cual le permitirá asignar toda o gran parte de la memoria nueva instalada al grupo de recursos de servidor.  
  
> [!IMPORTANT]  
>  Si el servidor se está ejecutando en una máquina virtual y no está dedicado, establezca el valor de MIN_MEMORY_PERCENT en el mismo valor que MAX_MEMORY_PERCENT.   
> Vea el tema [Prácticas recomendadas: usar OLTP en memoria en un entorno de máquinas virtuales](../../database-engine/using-in-memory-oltp-in-a-vm-environment.md) para obtener más información.  
  
##  <a name="bkmk_PageAllocFailure"></a> Resolver los errores de asignación de páginas debidos a memoria insuficiente cuando hay suficiente memoria disponible  
 Si aparece el mensaje de error "No se permiten asignaciones de páginas para la base de datos '*\<nombreDeBaseDeDatos>*' debido a memoria insuficiente en el grupo de recursos de servidor '*\<nombreDeGrupoDeRecursos>*'". Consulte 'http://go.microsoft.com/fwlink/?LinkId=330673' para obtener más información. " en el registro de errores cuando hay suficiente memoria física disponible para asignar la página, puede ser debido a un regulador de recursos deshabilitado. Cuando el Regulador de recursos está deshabilitado, MEMORYBROKER_FOR_RESERVE induce una presión de memoria artificial.  
  
 Para resolver este problema necesita habilitar el Regulador de recursos.  
  
 Vea [Habilitar el regulador de recursos](http://technet.microsoft.com/library/bb895149.aspx) para obtener información sobre los límites y las restricciones, así como instrucciones para habilitar el Regulador de recursos mediante el Explorador de objetos, propiedades del Regulador de recursos o Transact-SQL.  
  
## <a name="see-also"></a>Vea también  
 [Administrar memoria para OLTP en memoria](../../database-engine/managing-memory-for-in-memory-oltp.md)   
 [Supervisar y solucionar problemas del uso de la memoria](monitor-and-troubleshoot-memory-usage.md)   
 [Enlazar una base de datos con tablas con optimización para memoria a un grupo de recursos de servidor](bind-a-database-with-memory-optimized-tables-to-a-resource-pool.md)   
 [Prácticas recomendadas: usar OLTP en memoria en un entorno de máquinas virtuales](../../database-engine/using-in-memory-oltp-in-a-vm-environment.md)  
  
  
