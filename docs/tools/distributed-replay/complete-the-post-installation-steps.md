---
title: "Complete los pasos posteriores a la instalación | Documentos de Microsoft"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: sql-non-specified
ms.service: 
ms.component: distributed-replay
ms.reviewer: 
ms.suite: sql
ms.technology: setup-install
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 0a788a2a-9b4f-4bfc-b1b5-83eeb1ea9ab2
caps.latest.revision: "8"
author: MikeRayMSFT
ms.author: mikeray
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 375f63cb25259ca3bfcc966d6b41809ad1fa992b
ms.sourcegitcommit: b2d8a2d95ffbb6f2f98692d7760cc5523151f99d
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/05/2017
---
# <a name="complete-the-post-installation-steps"></a>Completar los pasos posteriores a la instalación
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]Después de instalar Distributed Replay debe modificar las cuentas de servicios de cliente y el controlador de Distributed Replay.  
  
### <a name="to-complete-the-post-installation-steps"></a>Para completar los pasos posteriores a la instalación  
  
1.  **Cree reglas de firewall**: en los equipos del controlador y cliente, debe permitir el tráfico entrante a través del firewall para el servicio correspondiente. Especifique las reglas de firewall para los ejecutables del servicio, ubicados en las carpetas de instalación.  
  
    1.  Para el servicio del controlador, cree una regla para **DReplayController.exe**, ubicada en la carpeta de instalación. Por ejemplo, el comando siguiente habilita esta regla, donde `%InstallPath%` es la carpeta de instalación del servicio:  
  
         `netsh advfirewall firewall add rule name="allow dreplay controller" dir=in program="%InstallPath%\DReplayController\DReplayController.exe" action=allow`  
  
    2.  Para el servicio de cliente, en cada equipo cliente, cree una regla para **DReplayClient.exe**, ubicada en la carpeta de instalación. Por ejemplo, el comando siguiente habilita esta regla, donde `%InstallPath%` es la carpeta de instalación del servicio:  
  
         `netsh advfirewall firewall add rule name="allow dreplay client" dir=in program="%InstallPath%\DReplayClient\DReplayClient.exe" action=allow`  
  
2.  **Conceda permisos a todos los clientes en el servidor de destino**: después de completar la instalación del servicio de cliente en los equipos cliente, debe agregar manualmente las cuentas del servicio de cliente al rol sysadmin en la instancia de destino de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
## <a name="net-framework-security"></a>Seguridad de .NET Framework  
 Debe disponer de permisos administrativos para instalar cualquiera de las características de Distributed Replay. Solo un inicio de sesión de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] con permisos sysadmin puede agregar las cuentas del servicio de cliente al rol de servidor sysadmin del servidor de prueba. Para obtener más información sobre las consideraciones de seguridad de Distributed Replay, vea [Distributed Replay Security](../../tools/distributed-replay/distributed-replay-security.md).  
  
  
