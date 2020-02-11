---
title: affinity Input-Output mask (opción de configuración del servidor) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
helpviewer_keywords:
- affinity I/O mask option
- processor affinity [SQL Server]
- binding processors [SQL Server]
- CPU affinity mask option
ms.assetid: 9950a8c9-9fe0-4003-95df-6f0d1becb0e7
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 65e412a3dfdfc71931e6af4d449c5be88ae351b7
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "62813683"
---
# <a name="affinity-input-output-mask-server-configuration-option"></a>affinity Input-Output mask (opción de configuración del servidor)
  Para llevar a cabo una multitarea, [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows 2000 y Windows Server 2003 a veces mueven subprocesos entre distintos procesadores. Aunque esta actividad es eficaz desde el punto de vista del sistema operativo, puede reducir el rendimiento de [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] cuando la carga del sistema es grande, ya que la memoria caché de cada procesador se carga repetidamente con datos. La asignación de procesadores a subprocesos específicos puede mejorar el rendimiento en estas condiciones, ya que se eliminan las recargas de procesador; esta asociación entre un subproceso y un procesador se denomina afinidad del procesador.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]admite la afinidad del procesador por medio de dos opciones de máscara de afinidad: **affinity mask** (también conocida como **CPU affinity mask**) y **affinity I/o Mask**. Para obtener más información sobre la opción **affinity mask** , vea [affinity mask (opción de configuración del servidor)](affinity-mask-server-configuration-option.md). La compatibilidad de la afinidad de CPU y e/s con servidores con procesadores de 33 a 64 requiere el uso adicional de la [opción de configuración del servidor Mask de affinity64](affinity64-mask-server-configuration-option.md) y la [opción de configuración del servidor máscara de entrada-salida de affinity64](affinity64-input-output-mask-server-configuration-option.md) respectivamente.  
  
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
  
 La opción **affinity I/O mask** es una opción avanzada. Si está utilizando el `sp_configure` procedimiento almacenado del sistema para cambiar la configuración, solo podrá cambiar la opción máscara de afinidad de **e/s** si **Mostrar opciones avanzadas** está establecido en 1. En [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], para reconfigurar la opción **affinity I/O mask** hay que reiniciar la instancia [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
> [!CAUTION]  
>  No configure la afinidad de CPU en el sistema operativo Windows y la máscara de afinidad en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Esta configuración intenta lograr el mismo resultado y, si las configuraciones no son coherentes, puede obtener resultados impredecibles. La afinidad de CPU de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] se configura mejor mediante la opción `sp_configure` de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
## <a name="see-also"></a>Consulte también  
 [Supervisar el uso de recursos &#40;Monitor de sistema&#41;](../../relational-databases/performance-monitor/monitor-resource-usage-system-monitor.md)   
 [RECONFIGURE &#40;Transact-SQL&#41;](/sql/t-sql/language-elements/reconfigure-transact-sql)   
 [Opciones de configuración de servidor &#40;SQL Server&#41;](server-configuration-options-sql-server.md)   
 [sp_configure &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-configure-transact-sql)  
  
  
