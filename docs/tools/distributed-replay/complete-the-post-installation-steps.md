---
title: Completar los pasos posteriores a la instalación
titleSuffix: SQL Server Distributed Replay
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: install
ms.topic: conceptual
ms.assetid: 0a788a2a-9b4f-4bfc-b1b5-83eeb1ea9ab2
author: MikeRayMSFT
ms.author: mikeray
ms.custom: seo-lt-2019
ms.date: 03/14/2017
ms.openlocfilehash: fade888b904b6be436e78cc38f9fc77bc8ee734d
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 03/29/2020
ms.locfileid: "75307073"
---
# <a name="complete-the-post-installation-steps"></a>Completar los pasos posteriores a la instalación

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

Después de instalar Distributed Replay debe modificar las cuentas de los servicios de controlador y de cliente de Distributed Replay.  
  
## <a name="to-complete-the-post-installation-steps"></a>Para completar los pasos posteriores a la instalación  
  
1. **Cree reglas de firewall**: en los equipos del controlador y cliente, debe permitir el tráfico entrante a través del firewall para el servicio correspondiente. Especifique las reglas de firewall para los ejecutables del servicio, ubicados en las carpetas de instalación.  
  
    1. Para el servicio del controlador, cree una regla para **DReplayController.exe**, ubicada en la carpeta de instalación. Por ejemplo, el comando siguiente habilita esta regla, donde `%InstallPath%` es la carpeta de instalación del servicio:  
  
         `netsh advfirewall firewall add rule name="allow dreplay controller" dir=in program="%InstallPath%\DReplayController\DReplayController.exe" action=allow`  
  
    2. Para el servicio de cliente, en cada equipo cliente, cree una regla para **DReplayClient.exe**, ubicada en la carpeta de instalación. Por ejemplo, el comando siguiente habilita esta regla, donde `%InstallPath%` es la carpeta de instalación del servicio:  
  
         `netsh advfirewall firewall add rule name="allow dreplay client" dir=in program="%InstallPath%\DReplayClient\DReplayClient.exe" action=allow`  
  
2. **Conceda permisos a todos los clientes en el servidor de destino**: después de completar la instalación del servicio de cliente en los equipos cliente, debe agregar manualmente las cuentas del servicio de cliente al rol sysadmin en la instancia de destino de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
## <a name="net-framework-security"></a>Seguridad de .NET Framework

Debe disponer de permisos administrativos para instalar cualquiera de las características de Distributed Replay. Solo un inicio de sesión de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] con permisos sysadmin puede agregar las cuentas del servicio de cliente al rol de servidor sysadmin del servidor de prueba. Para obtener más información sobre las consideraciones de seguridad de Distributed Replay, vea [Distributed Replay Security](../../tools/distributed-replay/distributed-replay-security.md).