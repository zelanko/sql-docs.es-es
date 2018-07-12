---
title: Configuración de Distributed Replay Client | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: ccf03e32-6bd9-43c0-b9b6-9fe0d9163339
caps.latest.revision: 15
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 83863c8bc5547ec0839eed7e0883de4d22c4f693
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/02/2018
ms.locfileid: "37168146"
---
# <a name="distributed-replay-client-configuration"></a>Configuración de Distributed Replay Client
  Use la página **Configuración de Distributed Replay Client** del Asistente para la instalación de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] con el fin de especificar los usuarios a los que desee conceder permisos administrativos para el servicio Distributed Replay Client.  
  
 Los usuarios con permisos administrativos tendrán acceso ilimitado al servicio Distributed Replay Client.  
  
## <a name="options"></a>Opciones  
 **Nombre del controlador**  
 Este es un parámetro opcional y el valor predeterminado es \< *en blanco*>.  
  
 Escriba el nombre del controlador con el que se comunicará el equipo cliente para el servicio Distributed Replay Client. Observe lo siguiente:  
  
-   El nombre debe ser un nombre de dominio completo (FQDN). Por ejemplo, un llamado servidor1 en la jerarquía de productos de Microsoft puede tener un FQDN de servidor1.productos.microsoft.com.  
  
-   Si ya ha configurado un controlador, escriba el nombre del controlador mientras configura cada cliente.  
  
-   Si aún no ha configurado ningún controlador, puede dejar el nombre del controlador en blanco. Sin embargo, debe escribir manualmente el nombre del controlador en el archivo de **configuración de cliente** .  
  
 **Directorio de trabajo**  
 Especifique el directorio de trabajo para el servicio Distributed Replay Client.  
  
 El directorio de trabajo predeterminado es \<*letra de unidad*>:\Archivos de programa\\[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]\DReplayClient\WorkingDir\\.  
  
 **Directorio de resultados**  
 Especifique el directorio de resultados para el servicio Distributed Replay Client.  
  
 El directorio de resultados predeterminado es \<*letra de unidad*>:\Archivos de programa\\[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]\DReplayClient\ResultDir\\.  
  
  
