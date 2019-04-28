---
title: Opciones de configuración de memoria del servidor | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
helpviewer_keywords:
- Virtual Memory Manager
- max server memory option
- virtual memory [SQL Server]
- VMM
- server memory options [SQL Server]
- servers [SQL Server], memory
- buffer pools [SQL Server]
- min server memory option
- manual memory options [SQL Server]
- memory [SQL Server], servers
ms.assetid: 29ce373e-18f8-46ff-aea6-15bbb10fb9c2
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: d4447d7df594e9542982d6ba05de05f42b0628a7
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "62810069"
---
# <a name="server-memory-server-configuration-options"></a>Opciones de configuración de memoria del servidor
  Use las dos opciones de memoria de servidor **Memoria de servidor mínima** y **Memoria de servidor máxima**para reconfigurar la cantidad de memoria (en megabytes) administrada por el Administrador de memoria de SQL Server para un proceso de SQL Server usado por una instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 El valor de configuración predeterminado para **Memoria de servidor mínima** es 0 y para **Memoria de servidor máxima** es 2147483647 MB. De forma predeterminada, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] puede cambiar sus requisitos de memoria de manera dinámica basándose en los recursos del sistema disponibles.  
  
> [!NOTE]  
>  Si establece el valor **Memoria de servidor máxima** en el valor mínimo, puede reducir significativamente el rendimiento de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e incluso impedir que se inicie. Si no puede iniciar [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tras cambiar esta opción, inicie esta herramienta mediante la opción de inicio **-f** y restablezca la opción **memoria de servidor máxima** a su valor anterior. Para más información, consulte [Opciones de inicio del servicio de motor de base de datos](database-engine-service-startup-options.md).  
  
 Cuando [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] utiliza la memoria de manera dinámica, realiza una consulta periódica en el sistema para determinar la cantidad de memoria libre. El mantenimiento de esta memoria libre evita la paginación en el sistema operativo (SO). Si hay menos memoria libre, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] libera memoria para el sistema operativo. Si hay más memoria libre, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] puede asignar más memoria. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] agrega memoria solo cuando su carga de trabajo así lo requiere; un servidor inactivo no aumenta el tamaño de su espacio de direcciones virtual.  
  
 Vea el ejemplo B sobre una consulta que devuelve la memoria que se está usando en estos momentos. La**memoria máxima del servidor** controla la asignación de memoria de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , incluidos el grupo de búferes, la memoria de compilación, todas las memorias caché, las concesiones de memoria, la memoria del administrador de bloqueos y la memoria de clr (básicamente, cualquier distribuidor de memoria que se encuentre en **sys.dm_os_memory_clerks**). La memoria de pilas de subprocesos, los montones de memoria, los proveedores de servidor vinculado que no sea [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]y cualquier memoria asignada por un DLL que no sea de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , no se controlan mediante la memoria máxima del servidor.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usa la API de notificación de memoria **QueryMemoryResourceNotification** para determinar el momento en que el Administrador de memoria de SQL Server puede asignar y liberar memoria.  
  
 Se recomienda permitir a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] utilizar memoria dinámicamente; sin embargo, puede establecer las opciones de memoria manualmente y restringir la cantidad de memoria a la que [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] puede obtener acceso. Antes de establecer la cantidad de memoria para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], determine la configuración de memoria apropiada restando de la memoria física total la memoria necesaria para el sistema operativo y todas las demás instancias de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (y otros usos del sistema, si el equipo no está dedicado totalmente a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]). Esta diferencia es la cantidad de memoria máxima que puede asignar a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
## <a name="setting-the-memory-options-manually"></a>Establecer manualmente las opciones de memoria  
 Establezca **Memoria de servidor mínima** y **Memoria de servidor máxima** de manera que abarquen un intervalo de valores de memoria. Este método es útil para que los administradores de bases de datos o de sistemas configuren una instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] junto con los requisitos de memoria de otras aplicaciones que se ejecutan en el mismo equipo.  
  
 Use **Memoria de servidor mínima** para garantizar una cantidad mínima de memoria disponible para el Administrador de memoria de SQL Server en una instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] no asignará inmediatamente la cantidad de memoria especificada en **Memoria de servidor mínima** durante el inicio. No obstante, cuando el uso de memoria ha alcanzado este valor debido a una carga del cliente, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] no puede liberar memoria a menos que se reduzca el valor de **Memoria de servidor mínima** .  
  
> [!NOTE]  
>  No es seguro que [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] asigne la cantidad de memoria especificada en **Memoria de servidor mínima**. Si la carga en el servidor no precisa nunca que se asigne la cantidad de memoria especificada en **Memoria de servidor mínima**, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] se ejecutará con menos memoria.  
  
|Tipo de SO|Mínimo memoria cantidades permitida para **memoria máxima del servidor**|  
|-------------|----------------------------------------------------------------|  
|32 bits|64 MB|  
|64 bits|128 MB|  
  
## <a name="how-to-configure-memory-options-using-sql-server-management-studio"></a>Cómo configurar las opciones de memoria utilizando SQL Server Management Studio  
 Use las dos opciones de memoria de servidor **Memoria del servidor mínima** y **Memoria del servidor máxima**para reconfigurar la cantidad de memoria (en megabytes) administrada por el Administrador de memoria de SQL Server para una instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. De forma predeterminada, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] puede cambiar sus requisitos de memoria de manera dinámica basándose en los recursos del sistema disponibles.  
  
### <a name="procedure-for-configuring-a-fixed-amount-of-memory"></a>Procedimiento para configurar una cantidad fija de memoria  
 **Para establecer una cantidad fija de memoria:**  
  
1.  En el Explorador de objetos, haga clic con el botón derecho en un servidor y seleccione **Propiedades**.  
  
2.  Haga clic en el nodo **Memoria** .  
  
3.  En **Opciones de memoria del servidor**, escriba la cantidad que desea para **Cantidad mínima de memoria del servidor** y **Cantidad máxima de memoria del servidor**.  
  
     Use la configuración predeterminada si desea que [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] pueda cambiar dinámicamente sus requisitos de memoria según los recursos del sistema disponibles. La configuración predeterminada para la **memoria de servidor mínima** es 0, y para la **memoria de servidor máxima** es 2147483647 megabytes (MB).  
  
## <a name="maximize-data-throughput-for-network-applications"></a>Maximizar el rendimiento para aplicaciones de red  
 Para optimizar el uso de memoria del sistema para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]se debe limitar la cantidad de memoria utilizada por el sistema para el almacenamiento en memoria caché de archivos. Para limitar la memoria caché del sistema de archivos, hay que asegurarse de que no esté activada la opción **Maximizar el rendimiento para compartir archivos** . Puede especificar la cantidad mínima de memoria caché del sistema de archivos seleccionando **Minimizar la memoria usada** o **Balance**.  
  
#### <a name="to-check-the-current-setting-on-your-operating-system"></a>Para comprobar la configuración actual de su sistema operativo  
  
1.  Haga clic en **Inicio**, luego en **Panel de control**, después haga doble clic en **Conexiones de red**y, por último, haga doble clic en **Conexión de área local**.  
  
2.  En la pestaña **General** , haga clic en **Propiedades**, seleccione **Compartir impresoras y archivos para redes Microsoft**y, a continuación, haga clic en **Propiedades**.  
  
3.  Si está seleccionada la opción **Maximizar el rendimiento para aplicaciones de red** , elija cualquier otra opción, haga clic en **Aceptar**y, a continuación, cierre el resto de cuadros de diálogo.  
  
## <a name="lock-pages-in-memory"></a>Bloquear páginas en la memoria  
 Esta directiva de Windows determina qué cuentas pueden usar un proceso para mantener los datos en la memoria física, impidiendo que el sistema realice la paginación de los datos en la memoria virtual del disco. El bloqueo de páginas en memoria puede mantener el servidor activo cuando se produce la paginación en la memoria del disco. El servidor SQL Server **Lock Pages in Memory** opción está establecida en ON en las instancias de 32 bits y 64 bits de [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] Standard edition y posterior cuando la cuenta con privilegios para ejecutar sqlservr.exe se le ha otorgado el Windows "bloqueado en páginas Derecho de usuario de "Memoria" (LPIM). En versiones anteriores de SQL Server, establecer la opción de bloqueo de páginas para una instancia de 32 bits de SQL Server requiere que la cuenta con privilegios para ejecutar sqlservr.exe tenga el derecho del usuario LPIM y que la opción de configuración “awe_enabled” esté establecida en ON.  
  
 Para deshabilitar la **Lock Pages In Memory** opción [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], quite el usuario "Bloquear páginas en memoria" adecuado para la cuenta de inicio de SQL Server.  
  
### <a name="to-disable-lock-pages-in-memory"></a>Para deshabilitar Bloquear páginas en la memoria  
 **Para deshabilitar la opción Bloquear páginas en memoria:**  
  
1.  En el menú **Inicio** , haga clic en **Ejecutar**. En el **abierto** , escriba `gpedit.msc`.  
  
     Se abrirá el cuadro de diálogo **Directiva de grupo** .  
  
2.  En la consola **Directiva de grupo** , expanda **Configuración del equipo**y, a continuación, expanda **Configuración de Windows**.  
  
3.  Expanda **Configuración de seguridad**y, a continuación, expanda **Directivas locales**.  
  
4.  Seleccione la carpeta **Asignación de derechos de usuario** .  
  
     Las directivas se mostrarán en el panel de detalles.  
  
5.  En el panel, haga doble clic en **Bloquear páginas en la memoria**.  
  
6.  En el cuadro de diálogo **Configuración de la directiva de seguridad local** , seleccione la cuenta con privilegios para ejecutar sqlservr.exe y haga clic en **Quitar**.  
  
## <a name="virtual-memory-manager"></a>Administrador de memoria virtual  
 Los sistemas operativos de 32 bits proporcionan acceso a un espacio de direcciones virtuales de 4 GB. Los 2 GB de memoria virtual son privados para cada proceso y están disponibles para el uso de las aplicaciones. Esta cantidad de 2 GB está reservada para uso del sistema operativo. Todas las ediciones de sistemas operativos incluyen un modificador que puede proporcionar a las aplicaciones acceso a 3 GB de espacio de direcciones virtuales, quedando limitado el sistema operativo a 1 GB. Para obtener más información acerca del uso de la configuración de memoria del modificador, vea la documentación de Windows acerca de la optimización de 4 gigabytes (4 GB). Cuando [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] de 32 bits se ejecuta en un sistema operativo de 64 bits, el espacio de direcciones virtuales disponible para el usuario es el total de 4 GB.  
  
 El Administrador de memoria virtual (VMM) de Windows asigna las regiones confirmadas de espacio de direcciones a la memoria física disponible.  
  
 Para obtener más información sobre la cantidad de memoria física admitida por los distintos sistemas operativos, vea la documentación de Windows titulada "Límites de memoria para versiones de Windows".  
  
 Los sistemas de memoria virtual permiten una mayor asignación de memoria física, de forma que la proporción de memoria virtual a memoria física puede ser superior a 1:1. Como resultado, los programas más grandes se pueden ejecutar en equipos con una diversidad de configuraciones de memoria física. No obstante, el uso de una cantidad de memoria virtual significativamente superior al promedio combinado de los espacios de trabajo de todos los procesos puede provocar un rendimiento bajo.  
  
 **Memoria de servidor mínima** y **Memoria de servidor máxima** son opciones avanzadas. Si usa el procedimiento almacenado del sistema **sp_configure** para cambiar estos valores, podrá cambiarlos solo si **Mostrar opciones avanzadas** tiene establecido el valor 1. Estos valores surten efecto inmediatamente, sin necesidad de reiniciar el servidor.  
  
## <a name="running-multiple-instances-of-sql-server"></a>Ejecutar varias instancias de SQL Server  
 Cuando esté ejecutando varias instancias de [!INCLUDE[ssDE](../../includes/ssde-md.md)], existen tres maneras con las que puede administrar la memoria:  
  
-   Utilizar **max server memory** para controlar el uso de memoria. Establezca los valores máximos de cada instancia, teniendo cuidado de que la asignación total no sea mayor que la memoria física total de su equipo. Es buena idea proporcionar a cada instancia memoria proporcional a la carga de trabajo o al tamaño de la base de datos esperados. Este método tiene la ventaja de que cuando se inician nuevos procesos o instancias, habrá memoria libre para ellos de forma inmediata. El inconveniente es que si no está ejecutando todas las instancias, ninguna de las instancias que se están ejecutando podrá utilizar el resto de la memoria libre.  
  
-   Utilizar **min server memory** para controlar el uso de memoria. Establezca la configuración mínima de cada instancia, de manera que la suma de estos mínimos sea 1-2 GB menos que la memoria física total de su equipo. De nuevo, puede establecer estos mínimos proporcionalmente a la carga de trabajo que se espera por cada instancia. Este método tiene la ventaja de que si no se ejecutan todas las instancias a la vez, las que se estén ejecutando pueden utilizar el resto de la memoria libre. Este método también resulta útil cuando en el equipo se está ejecutando otro proceso que consuma mucha memoria, puesto que asegura que [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] recibirá, al menos, una cantidad de memoria razonable. El inconveniente es que cuando se inicia una nueva instancia (o cualquier otro proceso), es posible que pase algún tiempo hasta que las instancias que se están ejecutando liberen memoria, especialmente si para ello deben escribir páginas modificadas en sus bases de datos.  
  
-   No hacer nada (no se recomienda). Las primeras instancias que se presenten con una carga de trabajo intentarán asignar toda la memoria. Puede que las instancias inactivas o las instancias que se inician más tarde terminen ejecutándose con una cantidad mínima de memoria disponible. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] no intenta equilibrar el uso de memoria en todas las instancias. Sin embargo, todas las instancias responderán a las señales de notificación de memoria de Windows para ajustar el tamaño de su superficie de memoria. Windows no equilibra la memoria entre las aplicaciones con la API de notificación de memoria. Simplemente proporciona informes globales acerca de la disponibilidad de memoria del sistema.  
  
 Esta configuración se puede cambiar sin tener que reiniciar las instancias; por tanto, se puede experimentar fácilmente para encontrar la mejor configuración para el patrón de uso.  
  
## <a name="providing-the-maximum-amount-of-memory-to-sql-server"></a>Proporcionar la cantidad máxima de memoria a SQL Server  
  
||32 bits|64 bits|  
|-|-------------|-------------|  
|Memoria convencional|Hasta el límite de espacio de direcciones virtuales del proceso en todas las ediciones de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]:<br /><br /> 2 GB<br /><br /> / 3 GB con **/3 gb** arranque parámetro *<br /><br /> 4 GB en WOW64\*\*|Hasta el límite de espacio de direcciones virtuales del proceso en todas las ediciones de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]:<br /><br /> 8 TB en la arquitectura x64|  
  
 ***/3gb** es un parámetro de arranque del sistema operativo. Para obtener más información, visite [MSDN Library](https://go.microsoft.com/fwlink/?LinkID=10257&clcid=0x409).  
  
 ** WOW64 (Windows on Windows 64) es un modo en que 32-bit [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] se ejecuta en un sistema operativo de 64 bits. Para obtener más información, visite [MSDN Library](https://go.microsoft.com/fwlink/?LinkID=10257&clcid=0x409).  
  
## <a name="examples"></a>Ejemplos  
  
### <a name="example-a"></a>Ejemplo A  
 En el ejemplo siguiente se establece la opción `max server memory` en 4 GB:  
  
```  
sp_configure 'show advanced options', 1;  
GO  
RECONFIGURE;  
GO  
sp_configure 'max server memory', 4096;  
GO  
RECONFIGURE;  
GO  
```  
  
### <a name="example-b-determining-current-memory-allocation"></a>Ejemplo B: Determinación de la asignación de memoria actual  
 La consulta siguiente devuelve información acerca de la memoria asignada actual.  
  
```  
SELECT  
(physical_memory_in_use_kb/1024) AS Memory_usedby_Sqlserver_MB,  
(locked_page_allocations_kb/1024) AS Locked_pages_used_Sqlserver_MB,  
(total_virtual_address_space_kb/1024) AS Total_VAS_in_MB,  
process_physical_memory_low,  
process_virtual_memory_low  
FROM sys.dm_os_process_memory;  
```  
  
## <a name="see-also"></a>Vea también  
 [Supervisión y optimización del rendimiento](../../relational-databases/performance/monitor-and-tune-for-performance.md)   
 [RECONFIGURE &#40;Transact-SQL&#41;](/sql/t-sql/language-elements/reconfigure-transact-sql)   
 [Opciones de configuración de servidor &#40;SQL Server&#41;](server-configuration-options-sql-server.md)   
 [sp_configure &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-configure-transact-sql)  
  
  
