---
title: MSSQLSERVER_33128 | Microsoft Docs
ms.custom: 
ms.date: 04/04/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: errors-events
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
helpviewer_keywords:
- 33128 (Database Engine error)
ms.assetid: 12c1096f-d120-439b-85f3-f794859503c9
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 3ce51b520a52bc799bb987a1c4e6851c75029fcf
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 11/21/2017
---
# <a name="mssqlserver33128"></a>MSSQLSERVER_33128
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>Detalles  
  
|||  
|-|-|  
|Nombre del producto|SQL Server|  
|Identificador del evento|33128|  
|Origen del evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nombre simbólico|SEC_DEPRECATED_ALGO|  
|Texto del mensaje|Error de cifrado. La clave usa el algoritmo desusado “%.*ls” que ya no se admite.|  
  
## <a name="explanation"></a>Explicación  
Este mensaje se produce cuando se hace referencia el algoritmo de cifrado RC4 (o RC4_128). RC4 y RC4_128 son algoritmos débiles y están desusados. Use un algoritmo más seguro como uno de los algoritmos AES en su lugar.  
  
Cuando el nivel de compatibilidad de la base de datos es 90 o 100, la operación se realiza correctamente, se genera el evento de degradación y el mensaje solamente aparece en el búfer en anillo.  
  
Cuando el nivel de compatibilidad de la base de datos es 110 o superior, la operación de descifrado se realiza correctamente, se genera el evento de degradación y el mensaje solamente aparece en el búfer en anillo. Las operaciones de cifrado producirán un error, se genera el evento de degradación, se muestra el mensaje al usuario y el mensaje aparece en el búfer en anillo.  
  
> [!NOTE]  
> El búfer en anillo es un componente interno que no está completamente documentado y no está previsto que lo usen los clientes. Los mensajes de búfer en anillo son útiles para ponerse en contacto con el soporte técnico de [!INCLUDE[msCoName](../../includes/msconame-md.md)]. Para ver el búfer en anillo, consulte la vista de administración dinámica sys.dm_os_ring_buffers.  
  
|State|Description|  
|---------|---------------|  
|1|Una clave RC4 se usa en la función integrada encryptbykey(). La función integrada devuelve NULL. Este mensaje aparece únicamente en el búfer en anillo.|  
|2|Una clave RC4 se usa en la función integrada decryptbykey(). Este mensaje aparece únicamente en el búfer en anillo.|  
|3|Una clave RC4 desusada está cifrada mediante una clave simétrica. Vista por los usuarios y en el búfer en anillo. Las claves simétricas RC4 desusadas no se pueden modificar en el nivel de compatibilidad 110. Intente usar claves que no sean RC4 para las operaciones de cifrado. Si fuera necesario, establezca el nivel de compatibilidad con versiones anteriores en 90 o 100.|  
|4|Una clave que no es RC4 está cifrada mediante una clave simétrica RC4 desusada. Vista por los usuarios y en el búfer en anillo. Modificar la aplicación para usar las claves simétricas que no son RC4 o establecer el nivel de compatibilidad con versiones anteriores en 90 o 100.|  
|5|Una clave RC4 desusada está descifrada mediante una clave simétrica. Este mensaje aparece únicamente en el búfer en anillo.|  
|6|Una clave que no es RC4 está descifrada mediante una clave simétrica RC4. Este mensaje aparece únicamente en el búfer en anillo.|  
|7|Una clave simétrica RC4 está cifrada mediante el certificado. Vista por los usuarios y en el búfer en anillo.|  
|8|Una clave simétrica RC4 está descifrada mediante el certificado. Este mensaje aparece únicamente en el búfer en anillo.|  
|9|Una clave simétrica RC4 está cifrada mediante la clave EKM.|  
|10|Una clave simétrica RC4 está descifrada mediante la clave EKM. Este mensaje aparece únicamente en el búfer en anillo.|  
  
## <a name="user-action"></a>Acción del usuario  
Use un algoritmo más seguro como uno de los algoritmos AES en su lugar. (Se recomienda)  
  
Use ALTER DATABASE SET COMPATIBILITY_LEVEL para establecer el nivel de compatibilidad de la base de datos en 100. (No se recomienda).  
  
