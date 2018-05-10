---
title: affinity Input-Output mask (opción de configuración del servidor) | Microsoft Docs
ms.custom: ''
ms.date: 07/06/2017
ms.prod: sql
ms.prod_service: high-availability
ms.reviewer: ''
ms.suite: sql
ms.technology: configuration
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- affinity I/O mask option
- processor affinity [SQL Server]
- binding processors [SQL Server]
- CPU affinity mask option
ms.assetid: 9950a8c9-9fe0-4003-95df-6f0d1becb0e7
caps.latest.revision: 29
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: c449fccc6aa19b85329d75272119d16e6fb5802c
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="affinity-input-output-mask-server-configuration-option"></a>affinity Input-Output mask (opción de configuración del servidor)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

  Para realizar varias tareas, [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows a veces mueve subprocesos del proceso entre diferentes procesadores. Aunque es eficaz desde el punto de vista del sistema operativo, esta actividad puede reducir el rendimiento de [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] en casos de elevadas cargas de trabajo, ya que cada caché de procesador se recarga repetidamente con los datos. La asignación de procesadores a subprocesos específicos puede mejorar el rendimiento en estas condiciones, ya que se eliminan las recargas de procesador; esta asociación entre un subproceso y un procesador se denomina afinidad del procesador.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] admite la afinidad del procesador por medio de dos opciones de máscara de afinidad: **affinity mask** (también conocida como **CPU affinity mask**) y **affinity I/O mask**. Para obtener más información sobre la opción **affinity mask** , vea [affinity mask (opción de configuración del servidor)](../../database-engine/configure-windows/affinity-mask-server-configuration-option.md). La compatibilidad de afinidad de CPU y E/S con servidores con entre 33 y 64 procesadores exige el uso adicional de las opciones de configuración del servidor [affinity64 mask](../../database-engine/configure-windows/affinity64-mask-server-configuration-option.md) y [affinity64 I/O mask](../../database-engine/configure-windows/affinity64-input-output-mask-server-configuration-option.md) , respectivamente.  
  
> [!NOTE]  
>  La compatibilidad de la afinidad con servidores que tienen entre 33 y 64 procesadores solo está disponible en sistemas operativos de 64 bits.  
  
 La opción **affinity I/O mask** enlaza la E/S del disco de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] a un subconjunto específico de CPU. En entornos de procesamiento de transacciones en línea (OLTP) de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] de grandes prestaciones, esta extensión puede mejorar el rendimiento de los subprocesos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que emiten E/S. Esta mejora no admite la afinidad de hardware para controladores de discos o discos individuales.  
  
 El valor de **affinity I/O mask** especifica las CPU de un equipo con varios procesadores que se pueden seleccionar para procesar operaciones de E/S del disco de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . La máscara es un mapa de bits en el que el primer bit de la derecha especifica la CPU(0) de menor orden, el bit inmediatamente a su izquierda especifica la CPU(1) siguiente a la de menor orden, y así sucesivamente. Para configurar más de 32 procesadores, establezca tanto **affinity I/O mask** como **affinity64 I/O mask**.  
  
 Los valores de **affinity I/O mask** son los siguientes:  
  
-   Una máscara **affinity I/O mask** de 1 byte cubre hasta 8 CPU en un equipo con varios procesadores.  
  
-   Una máscara **affinity I/O mask** de 2 bytes cubre hasta 16 CPU en un equipo con varios procesadores.  
  
-   Una máscara **affinity I/O mask** de 3 bytes cubre hasta 24 CPU en un equipo con varios procesadores.  
  
-   Una máscara **affinity I/O mask** de 4 bytes cubre hasta 32 CPU en un equipo con varios procesadores.  
  
-   Para cubrir más de 32 CPU, configure una opción **affinity I/O mask** de cuatro bytes para las 32 primeras CPU y una opción **affinity64 I/O mask** de hasta 4 bytes para las CPU restantes.  
  
 El valor 1 bit en el patrón de afinidad de E/S especifica que la CPU correspondiente se puede seleccionar para realizar operaciones de E/S del disco de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ; El valor 0 bit especifica que no se debería programar ninguna operación de E/S del disco de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para la CPU correspondiente. Cuando todos los bits se establecen como cero, o bien no se especifica **affinity I/O mask** , la E/S del disco de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] se programa en cualquiera de las CPU que se pueden seleccionar para procesar subprocesos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
 Dado que establecer la opción [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **Máscara de afinidad de E/S** es una operación especializada, solo debería usarse en caso necesario. En la mayoría de los casos, la afinidad predeterminada de Windows 2000 o Windows Server 2003 proporciona el mejor rendimiento.  
  
 Al especificar la opción **affinity I/O mask** , hay que usarla junto con la opción de configuración **affinity mask** . No habilite la misma CPU en el modificador **affinity I/O mask** y la opción **affinity mask** . Los bits correspondientes a cada CPU deberían estar en uno de los tres estados siguientes:  
  
-   0 tanto en la opción **affinity I/O mask** como en la opción **affinity mask** .  
  
-   1 en la opción **affinity I/O mask** y 0 en la opción **affinity mask** .  
  
-   0 en la opción **affinity I/O mask** y 1 en la opción **affinity mask** .  
  
 La opción **affinity I/O mask** es una opción avanzada. Si usa el procedimiento almacenado del sistema **sp_configure** para cambiar la configuración, solo podrá cambiar el valor de **affinity I/O mask** si **Mostrar opciones avanzadas** está establecido en 1. En [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], para reconfigurar la opción **affinity I/O mask** hay que reiniciar la instancia [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
> [!CAUTION]  
>  No configure la afinidad de CPU en el sistema operativo Windows y la máscara de afinidad en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Esta configuración intenta lograr el mismo resultado y, si las configuraciones no son coherentes, puede obtener resultados impredecibles. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] La afinidad de CPU se configura mejor con la opción **sp_configure** de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
## <a name="see-also"></a>Ver también  
 [Supervisar el uso de recursos &#40;Monitor de sistema&#41;](../../relational-databases/performance-monitor/monitor-resource-usage-system-monitor.md)   
 [RECONFIGURE &#40;Transact-SQL&#41;](../../t-sql/language-elements/reconfigure-transact-sql.md)   
 [Opciones de configuración de servidor &#40;SQL Server&#41;](../../database-engine/configure-windows/server-configuration-options-sql-server.md)   
 [sp_configure &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md)  
  
  
