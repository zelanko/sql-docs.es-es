---
title: MSSQLSERVER_233 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
f1_keywords:
- "233"
helpviewer_keywords:
- 233 (Database Engine error)
ms.assetid: 201665dc-7ac8-4c19-90d3-33354c5caa72
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 4e18ce61356947754423cfb878cf47f90534b40f
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "62869225"
---
# <a name="mssqlserver233"></a>MSSQLSERVER_233
    
## <a name="details"></a>Detalles  
  
|||  
|-|-|  
|Nombre del producto|SQL Server|  
|Identificador del evento|233|  
|Origen del evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nombre simbólico||  
|Texto del mensaje|Se ha establecido una conexión correctamente con el servidor, pero se ha producido un error durante el proceso de inicio de sesión. (proveedor: Proveedor de memoria compartida; error: 0 - No hay ningún proceso en el otro extremo de la canalización). (Microsoft SQL Server, Error: 233)|  
  
## <a name="explanation"></a>Explicación  
 El cliente de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] no se puede conectar al servidor. Este error se puede producir porque el servidor no está configurado para aceptar conexiones remotas.  
  
## <a name="user-action"></a>Acción del usuario  
 Use la herramienta Administrador de configuración de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para que [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] acepte conexiones remotas.  
  
## <a name="see-also"></a>Vea también  
 [Protocolos de red y bibliotecas de red](../../sql-server/install/network-protocols-and-network-libraries.md)   
 [Configuración de red de cliente](../../database-engine/configure-windows/client-network-configuration.md)   
 [Configurar protocolos de cliente](../../database-engine/configure-windows/configure-client-protocols.md)   
 [Habilitar o deshabilitar un protocolo de red de servidor](../../database-engine/configure-windows/enable-or-disable-a-server-network-protocol.md)  
  
  
