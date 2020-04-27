---
title: affinity mask (opción de configuración del servidor) | Microsoft Docs
ms.custom: ''
ms.date: 10/20/2016
ms.prod: sql-server-2014
ms.reviewer: ''
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
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: a041171d9639429196b09b7a1f9254a30907ab2e
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/26/2020
ms.locfileid: "62814052"
---
# <a name="affinity-mask-server-configuration-option"></a>affinity mask (opción de configuración del servidor)
    
> [!NOTE]  
>  [!INCLUDE[ssNoteDepFutureDontUse](../../includes/ssnotedepfuturedontuse-md.md)] Use [ALTER SERVER CONFIGURATION &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-server-configuration-transact-sql) en su lugar.  
  
 Para realizar varias tareas, [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows a veces mueve subprocesos del proceso entre diferentes procesadores. Aunque esta actividad es eficaz desde el punto de vista del sistema operativo, puede reducir el rendimiento de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] cuando la carga del sistema es grande, ya que la memoria caché de cada procesador se carga repetidamente con datos. La asignación de procesadores a subprocesos específicos puede mejorar el rendimiento en estas condiciones al eliminar las operaciones de repetición de carga del procesador y reducir la migración de subprocesos entre procesadores (con lo que se reduce el cambio de contexto); dicha asociación entre un subproceso y un procesador se denomina afinidad del procesador.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] admite la afinidad del procesador por medio de dos opciones de máscara de afinidad: máscara de afinidad (también conocida como **máscara de afinidad de CPU**) y máscara de afinidad de E/S. Para obtener más información sobre la opción de máscara de afinidad de E/S, vea [affinity I/O mask (opción de configuración del servidor)](affinity-input-output-mask-server-configuration-option.md). La compatibilidad de afinidad de CPU y E/S con servidores con entre 33 y 64 procesadores exige el uso adicional de las opciones [affinity64 mask (opción de configuración del servidor)](affinity64-mask-server-configuration-option.md) y [affinity64 I/O mask (opción de configuración del servidor)](affinity64-input-output-mask-server-configuration-option.md), respectivamente.  
  
> [!NOTE]  
>  La compatibilidad de la afinidad con servidores que tienen entre 33 y 64 procesadores solo está disponible en sistemas operativos de 64 bits.  
  
 La opción affinity mask, que existía en versiones anteriores de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], controla la afinidad de la CPU de forma dinámica.  
  
 En [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], la opción affinity mask se puede configurar sin necesidad de reiniciar la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Si usa sp_configure, debe ejecutar RECONFIGURE o RECONFIGURE WITH OVERRIDE después de establecer una opción de configuración. Cuando se utiliza [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)], es necesario reiniciar después de modificar la opción affinity mask.  
  
 Los cambios en las máscaras de afinidad se producen de forma dinámica, lo que permite el inicio y cierre a petición de los programadores de CPU que enlazan los subprocesos en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Esto puede ocurrir cuando cambien las condiciones del servidor. Por ejemplo, si se agrega al servidor una nueva instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , puede ser necesario realizar ajustes en la opción affinity mask para redistribuir la carga del procesador.  
  
 Las modificaciones de las máscaras de bits de afinidad requieren que [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] habilite un nuevo programador de CPU y deshabilite el programador de CPU existente. A continuación se pueden procesar otros lotes en los programadores nuevos o restantes.  
  
 Para iniciar un nuevo programador de CPU, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] crea un nuevo programador y lo agrega a la lista de programadores estándar. El nuevo programador solo se tiene en cuenta para los nuevos procesos por lotes entrantes. Los procesos por lotes actuales continúan ejecutándose en el mismo programador. Los subprocesos de trabajo migran al nuevo programador cuando se liberan o cuando se crean nuevos subprocesos de trabajo.  
  
 Para cerrar un programador, es necesario que todos los procesos por lotes del programador finalicen sus actividades y se cierren. Los programadores que se han cerrado se marcan como sin conexión para que no se programe ningún proceso por lotes nuevo en ellos.  
  
 Tanto si se agrega un nuevo programador como si se quita, las tareas permanentes del sistema, como lockmonitor, checkpoint, subproceso de tarea del sistema (DTC en procesamiento) y el proceso de señal, continúan ejecutándose en el programador mientras el servidor esté operativo. Estas tareas permanentes del sistema no se migran de forma dinámica. Para redistribuir la carga del procesador para estas tareas del sistema entre los programadores, es necesario reiniciar la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Si [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] intenta cerrar un programador asociado con una tarea permanente del sistema, ésta continúa ejecutándose en el programador sin conexión (sin migración). Este programador está enlazado a los procesadores de la máscara de afinidad modificada y no debe imponer ninguna carga en el procesador con el que se estableció la afinidad antes del cambio. La existencia de programadores sin conexión adicionales no debería afectar significativamente a la carga del sistema. En caso contrario, es necesario reiniciar el servidor de base de datos para volver a configurar las tareas.  
  
 La máscara de afinidad de E/S afecta directamente a las tareas de afinidad de E/S (como lazywriter y logwriter). Si no se ha establecido la afinidad para las tareas lazywriter y logwriter, siguen las mismas reglas definidas para las demás tareas permanentes, como lockmonitor o checkpoint.  
  
 Para asegurarse de que la nueva máscara de afinidad es válida, el comando RECONFIGURE comprueba que las afinidades normales de CPU y E/S se excluyen mutuamente. En caso contrario, se envía un mensaje de error a la sesión de cliente y al registro de errores de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para indicar que no se recomienda dicha configuración. La ejecución de la opción RECONFIGURE WITH OVERRIDE permite afinidades de CPU y E/S que no se excluyen mutuamente.  
  
 Si especifica una máscara de afinidad que intenta asignarse a una CPU inexistente, el comando RECONFIGURE envía un mensaje de error a la sesión de cliente y al registro de errores de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . El uso de la opción RECONFIGURE WITH OVERRIDE no tiene efecto en este caso y se vuelve a enviar el mismo error de configuración.  
  
 También puede excluir la actividad de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] de los procesadores a los que el sistema operativo Windows 2000 o Windows Server 2003 han asignado cargas de trabajo específicas. Si establece el valor 1 para un bit que representa un procesador, el motor de base de datos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] selecciona dicho procesador para la asignación de subprocesos. Cuando se establece `affinity mask` en 0 (valor predeterminado), los algoritmos de programación de Microsoft Windows 2000 o windows Server 2003 establecen la afinidad del subproceso. Si establece `affinity mask` en cualquier valor distinto de cero, la afinidad de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] interpreta el valor como una máscara de bits que especifica los procesadores que se pueden seleccionar.  
  
 Mediante la separación de los subprocesos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para que se ejecuten en determinados procesadores, Microsoft Windows 2000 o Windows Server 2003 pueden evaluar mejor el control de los procesos específicos de Windows por parte del sistema. Por ejemplo, en un servidor de 8 CPU en el que se ejecutan dos instancias de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (instancias A y B), el administrador del sistema puede utilizar la opción affinity mask para asignar el primer conjunto de 4 CPU a la instancia A y el segundo conjunto de 4 CPU a la instancia B. Para configurar más de 32 procesadores, establezca las opciones affinity mask y affinity64 mask. Estos son los valores para `affinity mask`:  
  
-   Una opción `affinity mask` de un byte cubre hasta 8 CPU en un equipo con varios procesadores.  
  
-   Una opción `affinity mask` de dos bytes cubre hasta 8 CPU en un equipo con varios procesadores.  
  
-   Una opción `affinity mask` de tres bytes cubre hasta 24 CPU en un equipo con varios procesadores.  
  
-   Una opción `affinity mask` de cuatro bytes cubre hasta 32 CPU en un equipo con varios procesadores.  
  
-   Para cubrir más de 32 CPU, configure una opción affinity mask de cuatro bytes para las primeras 32 CPU y una opción affinity64 mask de hasta cuatro bytes para las restantes CPU.  
  
 Como la configuración de la afinidad del procesador de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] es una operación especial, se recomienda utilizarla solo cuando sea necesario. En la mayor parte de los casos, el mejor rendimiento se obtiene con la afinidad predeterminada de Microsoft Windows 2000 o Windows Server 2003. Al configurar las máscaras de afinidad, también debe considerar los requisitos de CPU para otras aplicaciones. Para obtener más información, vea la documentación del sistema operativo Windows.  
  
> [!NOTE]  
>  Puede utilizar el Monitor de sistema de Windows para ver y analizar el uso individual del procesador.  
  
 Al especificar la opción affinity I/O mask, debe usarla en conexión con la opción de configuración affinity mask. No habilite la misma CPU en el modificador `affinity mask` y la opción affinity I/O mask. Los bits correspondientes a cada CPU deben estar en uno de los tres estados siguientes:  
  
-   0 tanto en la opción affinity mask como en la opción affinity I/O mask.  
  
-   1 en la opción affinity mask y 0 en la opción affinity I/O mask.  
  
-   0 en la opción affinity mask y 1 en la opción affinity I/O mask.  
  
> [!CAUTION]  
>  No configure la afinidad de CPU en el sistema operativo Windows y la máscara de afinidad en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Esta configuración intenta lograr el mismo resultado y, si las configuraciones no son coherentes, puede obtener resultados impredecibles. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] La afinidad de CPU se configura mejor mediante la opción sp_configure de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
## <a name="example"></a>Ejemplo  
 Como ejemplo de configuración de la opción affinity mask, si los procesadores 1, 2 y 5 están seleccionados como disponibles con el valor 1 para los bits 1, 2 y 5, y el valor 0 para los bits 0, 3, 4, 6 y 7, se especifica el valor hexadecimal 0x26 o el valor decimal equivalente `38` . Enumere los bits de derecha a izquierda. La opción affinity mask comienza a contar los procesadores de 0 a 31, de modo que en el ejemplo siguiente el contador `1` representa el segundo procesador del servidor.  
  
```  
sp_configure 'show advanced options', 1;  
RECONFIGURE;  
GO  
sp_configure 'affinity mask', 38;  
RECONFIGURE;  
GO  
```  
  
 A continuación se indican los valores de `affinity mask` para un sistema con 8 CPU.  
  
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
  
 La opción affinity mask es una opción avanzada. Si usa el sp_configure procedimiento almacenado del sistema para cambiar la configuración, solo puede cambiar `affinity mask` si **Mostrar opciones avanzadas** está establecido en 1. Después de ejecutar el comando RECONFIGURE de [!INCLUDE[tsql](../../includes/tsql-md.md)] , la nueva configuración se aplica inmediatamente sin necesidad de reiniciar la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
## <a name="non-uniform-memory-access-numa"></a>Acceso no uniforme a memoria (NUMA)  
 Cuando se utiliza el acceso no uniforme a memoria (NUMA) basado en hardware y se ha establecido affinity mask, se establecerá la afinidad de cada programador de un nodo con su propia CPU. Cuando no se establece la opción affinity mask, se establece la afinidad de cada programador con el grupo de CPU en un nodo NUMA y un programador asignado al nodo NUMA N1 puede programar trabajos en cualquier CPU del nodo, pero no en las CPU asociadas a otro nodo.  
  
 Cualquier operación que se ejecute en un solo nodo NUMA únicamente puede utilizar las páginas de búfer de ese nodo. Cuando una operación se ejecuta en paralelo en las CPU de varios nodos, se puede utilizar la memoria de cualquiera de estos nodos.  
  
## <a name="licensing-issues"></a>Consideraciones acerca de las licencias  
 La afinidad dinámica está estrictamente restringida por las licencias de CPU. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] no permite la configuración de las opciones de máscara de afinidad que infrinjan las directivas de las licencias.  
  
### <a name="startup"></a>Inicio  
 Si una máscara de afinidad especificada infringe las directivas de las licencias durante el inicio de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o al adjuntar la base de datos, el nivel del motor completará el proceso de inicio o la operación para adjuntar o restaurar la base de datos; después, volverá a establecer en cero el valor de ejecución de sp_configure para la opción affinity mask y enviará un mensaje de error al registro de errores de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
### <a name="reconfigure"></a>Volver a configurar  
 Si una máscara de afinidad determinada infringe las directivas de las licencias en la ejecución del comando RECONFIGURE de [!INCLUDE[tsql](../../includes/tsql-md.md)] , se envía un mensaje de error a la sesión de cliente y al registro de errores de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] solicitando que el administrador de la base de datos vuelva a configurar la máscara de afinidad. En este caso no se acepta ningún comando RECONFIGURE WITH OVERRIDE.  
  
## <a name="see-also"></a>Consulte también  
 [Supervisar el uso de recursos &#40;Monitor de sistema&#41;](../../relational-databases/performance-monitor/monitor-resource-usage-system-monitor.md)   
 [RECONFIGURE &#40;Transact-SQL&#41;](/sql/t-sql/language-elements/reconfigure-transact-sql)   
 [Opciones de configuración de servidor &#40;SQL Server&#41;](server-configuration-options-sql-server.md)   
 [sp_configure &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-configure-transact-sql)   
 [ALTER SERVER CONFIGURATION &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-server-configuration-transact-sql)  
  
  
