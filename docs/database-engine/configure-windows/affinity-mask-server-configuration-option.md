---
title: affinity mask (opción de configuración del servidor)
description: Obtenga información sobre la opción "affinity mask" en SQL Server. Vea un ejemplo que la usa para enlazar procesadores a subprocesos específicos.
ms.prod: sql
ms.prod_service: high-availability
ms.technology: configuration
ms.topic: conceptual
helpviewer_keywords:
- default affinity mask option
- reloading processor cache
- processor cache [SQL Server]
- CPU [SQL Server], licensing
- deferred process call
- affinity mask option
- processor affinity [SQL Server]
- SMP
- DPC
ms.assetid: 5823ba29-a75d-4b3e-ba7b-421c07ab3ac1
author: markingmyname
ms.author: maghan
ms.reviewer: mikeray
ms.custom: ''
ms.date: 06/11/2020
ms.openlocfilehash: 94f8406af013bc0720bc16063d1a9881eda94c5a
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/01/2020
ms.locfileid: "85715589"
---
# <a name="affinity-mask-server-configuration-option"></a>affinity mask (opción de configuración del servidor)

 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

> [!NOTE]
> [!INCLUDE[ssNoteDepFutureDontUse](../../includes/ssnotedepfuturedontuse-md.md)] Use [ALTER SERVER CONFIGURATION &#40;Transact-SQL&#41;](../../t-sql/statements/alter-server-configuration-transact-sql.md) en su lugar.

Para realizar varias tareas, [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows a veces mueve subprocesos del proceso entre diferentes procesadores. Aunque es eficaz desde el punto de vista del sistema operativo, esta actividad puede reducir el rendimiento de SQL Server en casos de elevadas cargas, ya que cada caché de procesador se vuelve a cargar repetidamente con los datos. La asignación de procesadores a subprocesos específicos puede mejorar el rendimiento en estas condiciones mediante la eliminación de las recargas de procesador y la reducción de la migración de subprocesos en los procesadores, lo que a su vez reduce el cambio de contexto. Este tipo de asociación entre un subproceso y un procesador se denomina afinidad del procesador.

SQL Server admite la afinidad del procesador por medio de dos opciones de máscara de afinidad: "affinity mask" (también conocida como **CPU affinity mask**) y "affinity I/O mask". Para obtener más información sobre la opción "affinity I/O mask", vea [affinity Input-Output mask (opción de configuración del servidor)](../../database-engine/configure-windows/affinity-input-output-mask-server-configuration-option.md). La compatibilidad de afinidad de CPU y E/S con servidores con entre 33 y 64 procesadores exige el uso adicional de las opciones [affinity64 mask (opción de configuración del servidor)](../../database-engine/configure-windows/affinity64-mask-server-configuration-option.md) y [affinity64 I/O mask (opción de configuración del servidor)](../../database-engine/configure-windows/affinity64-input-output-mask-server-configuration-option.md), respectivamente.

> [!NOTE]  
> La compatibilidad de la afinidad con servidores que tienen entre 33 y 64 procesadores solo está disponible en sistemas operativos de 64 bits.

La opción "affinity mask", que existía en versiones anteriores de SQL Server, controla la afinidad de la CPU de forma dinámica.

En SQL Server, la opción "affinity mask" se puede configurar sin necesidad de reiniciar la instancia de SQL Server. Si usa sp_configure, debe ejecutar RECONFIGURE o RECONFIGURE WITH OVERRIDE después de establecer una opción de configuración. Cuando se utiliza [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)], es necesario reiniciar después de modificar la opción "affinity mask".

Los cambios en las máscaras de afinidad se producen de forma dinámica, lo que permite el inicio y apagado a petición de los programadores de CPU que enlazan los subprocesos en SQL Server. Esto puede ocurrir cuando cambien las condiciones del servidor. Por ejemplo, si se agrega al servidor una nueva instancia de SQL Server, puede ser necesario realizar ajustes en la opción "affinity mask" para redistribuir la carga del procesador.

Las modificaciones de las máscaras de bits de afinidad requieren que SQL Server habilite un nuevo programador de CPU y deshabilite el programador de CPU existente. A continuación se pueden procesar otros lotes en los programadores nuevos o restantes.

Para iniciar un nuevo programador de CPU, SQL Server crea uno nuevo y lo agrega a la lista de programadores estándar. El nuevo programador solo se tiene en cuenta para los nuevos procesos por lotes entrantes. Los procesos por lotes actuales continúan ejecutándose en el mismo programador. Los subprocesos de trabajo migran al nuevo programador cuando se liberan o cuando se crean nuevos subprocesos de trabajo.

Para cerrar un programador, es necesario que todos los procesos por lotes del programador finalicen sus actividades y se cierren. Los programadores que se han cerrado se marcan como sin conexión para que no se programe ningún proceso por lotes nuevo en ellos.

Tanto si se agrega un nuevo programador como si se quita, las tareas permanentes del sistema, como el monitor de bloqueo, el punto de control, el subproceso de tarea del sistema (DTC en procesamiento) y el proceso de señal, continúan ejecutándose en el programador mientras el servidor esté operativo. Estas tareas permanentes del sistema no se migran de forma dinámica. A fin de redistribuir la carga del procesador para estas tareas del sistema entre los programadores, es necesario reiniciar la instancia de SQL Server. Si SQL Server intenta apagar un programador asociado con una tarea permanente del sistema, esta continúa ejecutándose en el programador sin conexión (sin migración). Este programador está enlazado a los procesadores de la máscara de afinidad modificada y no impone ninguna carga en el procesador con el que se ha enlazado antes del cambio. La existencia de programadores sin conexión adicionales no debería afectar significativamente a la carga del sistema. Si lo hace, se requiere un reinicio del servidor de bases de datos para volver a configurar estas tareas en los programadores disponibles con la máscara de afinidad modificada.

No establezca los valores de configuración "affinity mask" y "affinity I/O mask" de SQL Server para utilizar las mismas CPU. El rendimiento puede verse afectado si elige enlazar un procesador para la programación de subprocesos de trabajo de SQL Server y el procesamiento de E/S. Por lo tanto, asegúrese de que los valores de configuración no están establecidos para el mismo procesador. La misma recomendación se aplica a "affinity64 mask" y "affinity64 I/O mask".  Para asegurarse de que la máscara de afinidad no se superpone con "affinity I/O mask", el comando [RECONFIGURE](../../t-sql/language-elements/reconfigure-transact-sql.md) comprueba que las afinidades normales de CPU y E/S se excluyen mutuamente. En caso contrario, se envía un mensaje de error a la sesión de cliente y al registro de errores de SQL Server para indicar que no se recomienda dicha configuración.

```sql
 Msg 5834, Level 16, State 1, Line 1
 The affinity mask specified conflicts with the IO affinity mask specified. Use the override option to force this configuration
```

La ejecución de la opción RECONFIGURE WITH OVERRIDE permite que las afinidades de CPU y E/S se superpongan y no se excluyan mutuamente.  

La máscara de afinidad de E/S afecta directamente a las tareas de afinidad de E/S (como la escritura diferida y la escritura de registro). Si no se han enlazado las tareas de escritura diferida y escritura de registro, seguirán las mismas reglas definidas para las demás tareas permanentes, como monitor de bloqueo o punto de control.
Si especifica una máscara de afinidad que intenta asignarse a una CPU inexistente, el comando RECONFIGURE envía un mensaje de error a la sesión de cliente y al registro de errores de SQL Server. El uso de la opción RECONFIGURE WITH OVERRIDE no tiene efecto en este caso y se vuelve a enviar el mismo error de configuración.

También puede excluir la actividad de SQL Server de las asignaciones de carga de trabajo específicas del sistema operativo Windows. Si establece el valor 1 para un bit que representa un procesador, el Motor de base de datos de SQL Server seleccionará dicho procesador para la asignación de subprocesos. Si establece **affinity mask** en 0 (el valor predeterminado), los algoritmos de programación de Microsoft Windows establecen la afinidad del subproceso. Si establece **affinity mask** en cualquier valor distinto de cero, la afinidad de SQL Server interpreta el valor como una máscara de bits que especifica los procesadores que se pueden seleccionar.  

Mediante la separación de los subprocesos de SQL Server para que se ejecuten en determinados procesadores, Microsoft Windows puede evaluar mejor el control de los procesos específicos de Windows por parte del sistema. Por ejemplo, en un servidor de 8 CPU en el que se ejecutan dos instancias de SQL Server (instancias A y B), el administrador del sistema puede utilizar la opción "affinity mask" para asignar el primer conjunto de 4 CPU a la instancia A y el segundo conjunto de 4 CPU a la instancia B. Para configurar más de 32 procesadores, establezca las opciones "affinity mask" y "affinity64 mask". Los valores de **máscara de afinidad** son los siguientes:

- Una **máscara de afinidad** de un byte cubre hasta ocho CPU en un equipo multiprocesador.

- Una **máscara de afinidad** de dos bytes cubre hasta 16 CPU en un equipo multiprocesador.

- Una **máscara de afinidad** de tres bytes cubre hasta 24 CPU en un equipo multiprocesador.

- Una **máscara de afinidad** de cuatro bytes cubre hasta 32 CPU en un equipo multiprocesador.

- Para cubrir más de 32 CPU, configure una opción affinity mask de cuatro bytes para las primeras 32 CPU y una opción affinity64 mask de hasta cuatro bytes para las restantes CPU.

Como la configuración de la afinidad del procesador de SQL Server es una operación especializada, se recomienda utilizarla solo cuando sea necesario. En la mayor parte de los casos, el mejor rendimiento se obtiene con la afinidad predeterminada de Microsoft Windows. Al configurar las máscaras de afinidad, considere los requisitos de CPU para otras aplicaciones. Para obtener más información, vea la documentación del sistema operativo Windows.

> [!NOTE]
> Puede utilizar el Monitor de sistema de Windows para ver y analizar el uso individual del procesador.

Al especificar la opción "affinity I/O mask", se debe usar junto con la opción de configuración "affinity mask". Sin embargo, tal como se ha mencionado anteriormente, no habilite la misma CPU en el modificador de **affinity mask** y la opción "affinity I/O mask". Los bits correspondientes a cada CPU deben estar en uno de los tres estados siguientes:

- 0 tanto en la opción affinity mask como en la opción affinity I/O mask.

- 1 en la opción affinity mask y 0 en la opción affinity I/O mask.

- 0 en la opción affinity mask y 1 en la opción affinity I/O mask.

> [!CAUTION]
> No configure la afinidad de CPU en el sistema operativo Windows y la máscara de afinidad en SQL Server. Esta configuración intenta lograr el mismo resultado y, si las configuraciones no son coherentes, puede obtener resultados impredecibles. La afinidad de CPU de SQL Server se configura mejor mediante la opción sp_configure de SQL Server.

## <a name="example"></a>Ejemplo

Como ejemplo de configuración de la opción "affinity mask", si los procesadores 1, 2 y 5 están seleccionados como disponibles con el valor 1 para los bits en las posiciones 1, 2 y 5, y el valor 0 para los bits 0, 3, 4, 6 y 7, se debe usar el valor hexadecimal 0x26 o el valor decimal equivalente de 38. Enumere las posiciones de los bits de derecha a izquierda.

```sql
sp_configure 'show advanced options', 1;
RECONFIGURE;
GO
sp_configure 'affinity mask', 38;
RECONFIGURE;
GO
```

A continuación se indican los valores de **máscara de afinidad** para un sistema con ocho CPU.  

|Valor decimal|Máscara de bits binarios|Permitir subprocesos de SQL Server en procesadores|  
|-------------------|---------------------|--------------------------------------------|  
|1|00000001|0|  
|3|00000011|0 y 1|  
|7|00000111|0, 1 y 2|  
|15|00001111|0, 1, 2 y 3|  
|31|00011111|0, 1, 2, 3 y 4|  
|63|00111111|0, 1, 2, 3, 4 y 5|  
|127|01111111|0, 1, 2, 3, 4, 5 y 6|  
|255|11111111|0, 1, 2, 3, 4, 5, 6 y 7|  

La opción affinity mask es una opción avanzada. Si está usando el procedimiento almacenado del sistema sp_configure para cambiar la configuración, solo podrá cambiar el valor de **affinity mask** si **Mostrar opciones avanzadas** está establecido en 1. Después de ejecutar el comando RECONFIGURE de [!INCLUDE[tsql](../../includes/tsql-md.md)], la nueva configuración se aplica de inmediato sin necesidad de reiniciar la instancia de SQL Server.  

## <a name="non-uniform-memory-access-numa"></a>Acceso no uniforme a memoria (NUMA)

Cuando se utiliza el acceso no uniforme a memoria (NUMA) basado en hardware y se ha establecido máscara de afinidad, se enlazará cada programador de un nodo con su propia CPU. Cuando no se establece la opción máscara de afinidad, se enlaza cada programador con el grupo de CPU en un nodo NUMA y un programador asignado al nodo NUMA N1 puede programar trabajos en cualquier CPU del nodo, pero no en las CPU asociadas a otro nodo.  

Cualquier operación que se ejecute en un solo nodo NUMA únicamente puede utilizar las páginas de búfer de ese nodo. Cuando una operación se ejecuta en paralelo en las CPU de varios nodos, se puede utilizar la memoria de cualquiera de estos nodos.  
  
## <a name="licensing-issues"></a>Incidencias relativas a las licencias

La afinidad dinámica está estrictamente restringida por las licencias de CPU. SQL Server no permite la configuración de las opciones de "affinity mask" que infrinjan las directivas de las licencias.  

### <a name="startup"></a>Inicio

Si una máscara de afinidad especificada infringe las directivas de las licencias durante el inicio de SQL Server o al adjuntar la base de datos, el nivel del motor completará el proceso de inicio o la operación para adjuntar o restaurar la base de datos; después, restablecerá en cero el valor de ejecución de sp_configure para la opción "affinity mask" y enviará un mensaje de error al registro de errores de SQL Server.  
  
### <a name="reconfigure"></a>Volver a configurar

Si una máscara de afinidad determinada infringe las directivas de las licencias en la ejecución del comando RECONFIGURE de [!INCLUDE[tsql](../../includes/tsql-md.md)], se envía un mensaje de error a la sesión de cliente y al registro de errores de SQL Server solicitando que el administrador de la base de datos vuelva a configurar la máscara de afinidad. En este caso no se acepta ningún comando RECONFIGURE WITH OVERRIDE.  

## <a name="next-steps"></a>Pasos siguientes

- [Supervisar el uso de recursos&#40;Monitor de sistema&#41;](../../relational-databases/performance-monitor/monitor-resource-usage-system-monitor.md)
- [RECONFIGURE &#40;Transact-SQL&#41;](../../t-sql/language-elements/reconfigure-transact-sql.md)
- [Opciones de configuración de servidor &#40;SQL Server&#41;](../../database-engine/configure-windows/server-configuration-options-sql-server.md)
- [sp_configure &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md)
- [ALTER SERVER CONFIGURATION &#40;Transact-SQL&#41;](../../t-sql/statements/alter-server-configuration-transact-sql.md)
