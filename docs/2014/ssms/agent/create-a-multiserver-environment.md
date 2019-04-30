---
title: Crear un entorno multiservidor | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- SQL Server Agent, multiserver environments
- master servers [SQL Server], about master servers
- target servers [SQL Server], about target servers
- multiserver environments [SQL Server]
ms.assetid: edc2b60d-15da-40a1-8ba3-f1d473366ee6
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 0c5c59a8802597b893110a5f2c26c919c16c8e83
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "63192963"
---
# <a name="create-a-multiserver-environment"></a>Crear un entorno multiservidor
  La administración multiservidor requiere que se configure un servidor maestro (MSX) y uno o más servidores de destino (TSX). Los trabajos que se van a procesar en todos los servidores de destino se definen primero en el servidor maestro y luego se descargan en los servidores de destino.  
  
 De forma predeterminada, el cifrado SSL (Capa de sockets seguros) y la validación de certificados completos se habilitan para las conexiones entre los servidores maestros y los servidores de destino. Para más información, [Establecer opciones de cifrado en servidores de destino](set-encryption-options-on-target-servers.md).  
  
 Si tiene un muchos servidores de destino, no defina el servidor maestro en un servidor de producción con requisitos de rendimiento elevados de otras funciones de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , ya que el tráfico del servidor de destino puede afectar negativamente al rendimiento del servidor de producción. Si también reenvía eventos a este servidor maestro dedicado, puede centralizar la administración en un servidor. Para más información, consulte [Administrar eventos](manage-events.md).  
  
> [!NOTE]  
>  Para usar el procesamiento de trabajos multiservidor, la cuenta de servicio del Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] debe ser miembro del rol **TargetServersRole** de la base de datos **msdb** del servidor maestro. El Asistente para servidor maestro agrega automáticamente la cuenta de servicio a este rol como parte del proceso de alta.  
  
## <a name="considerations-for-multiserver-environments"></a>Consideraciones para entornos multiservidor  
 Consulte la tabla siguiente para conocer las configuraciones de MSX/TSX admitidas.  
  
||**TSX = 7.0**|**TSX = 8.0 < SP3**|**TSX = 8.0 SP3 o superior**|**TSX = 9.0**|**TSX= 10.0**|**TSX = 10.5**|**TSX = 11.0**|  
|-|--------------------|---------------------------|----------------------------------|--------------------|--------------------|---------------------|---------------------|  
|**MSX = 7.0**|Sí|Sí|No|No|No|No|No|  
|**MSX = 8.0 &LT; SP3**|Sí|Sí|No|No|No|No|No|  
|**MSX = 8.0 SP3 o superior**|No|No|Sí|Sí|Sí|Sí|Sí|  
|**MSX = 9.0**|No|No|No|Sí|Sí|Sí|Sí|  
|**MSX = 10.0**|No|No|No|No|Sí|Sí|Sí|  
|**MSX = 10.5**|No|No|No|No|No|Sí|Sí|  
|**MSX = 11.0**|No|No|No|No|No|No|Sí|  
  
 Considere lo siguiente cuando cree un entorno multiservidor:  
  
-   Cada servidor de destino notifica únicamente a un servidor maestro. Para dar de alta un servidor de destino en otro servidor maestro, primero debe darlo de baja en el servidor maestro actual.  
  
-   Si desea cambiar el nombre de un servidor de destino, debe darlo de baja antes de cambiar el nombre y volver a darlo de alta después del cambio.  
  
-   Si desea anular una configuración multiservidor, debe dar de baja todos los servidores de destino del servidor maestro.  
  
-   SQL Server Integration Services solo admite servidores de destino que tengan la misma versión que el servidor maestro o una superior.  
  
## <a name="related-tasks"></a>Related Tasks  
 En los temas siguientes se presentan las tareas habituales para crear un entorno multiservidor.  
  
|Descripción|Tema|  
|-----------------|-----------|  
|Describe cómo crear un servidor maestro.|[Establecer un servidor maestro](make-a-master-server.md)|  
|Describe cómo crear un servidor de destino.|[Establecer un servidor de destino](make-a-target-server.md)|  
|Describe cómo dar de alta un servidor de destino en un servidor maestro.|[Dar de alta un servidor de destino en un servidor maestro](enlist-a-target-server-to-a-master-server.md)|  
|Describe cómo dar de baja un servidor de destino en un servidor maestro.|[Dar de baja un servidor de destino desde un servidor maestro](defect-a-target-server-from-a-master-server.md)|  
|Describe cómo dar de baja varios servidores de destino en un servidor maestro.|[Dar de baja varios servidores de destino desde un servidor maestro](defect-multiple-target-servers-from-a-master-server.md)|  
|Describe cómo comprobar el estado de un servidor de destino.|[sp_help_targetserver &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-help-targetserver-transact-sql)<br /><br /> [sp_help_targetservergroup &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-help-targetservergroup-transact-sql)|  
  
## <a name="see-also"></a>Vea también  
 [Solucionar problemas de trabajos multiservidor que usan servidores proxy](troubleshoot-multiserver-jobs-that-use-proxies.md)  
  
  
