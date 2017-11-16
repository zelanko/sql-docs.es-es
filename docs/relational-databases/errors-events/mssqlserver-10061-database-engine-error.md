---
title: MSSQLSERVER_10061 | Microsoft Docs
ms.custom: 
ms.date: 04/04/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords: "10061"
helpviewer_keywords: 10061 (Database Engine error)
ms.assetid: 729602f3-08df-474c-8740-8dea13c1eee3
caps.latest.revision: "11"
author: edmacauley
ms.author: edmaca
manager: cguyer
ms.workload: Inactive
ms.openlocfilehash: 11c3bb5f415595555a2e0a4af6d98e2d03c01568
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/09/2017
---
# <a name="mssqlserver10061"></a>MSSQLSERVER_10061
  
## <a name="details"></a>Detalles  
  
|||  
|-|-|  
|Nombre del producto|SQL Server|  
|Identificador del evento|10061|  
|Origen del evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nombre simbólico||  
|Texto del mensaje|Error al establecer una conexión al servidor.  La causa del problema en la conexión a SQL Server puede deberse a que SQL Server no permite conexiones remotas en su configuración predeterminada. (proveedor: proveedor TCP, error: 0 - No se pudo establecer conexión porque el equipo de destino rechazó.) (Microsoft SQL Server, Error: 10061)|  
  
## <a name="explanation"></a>Explicación  
El servidor no respondió a la solicitud del cliente. Este error puede producirse porque el servidor no se ha iniciado.  
  
## <a name="user-action"></a>Acción del usuario  
Asegúrese de que el servidor se haya iniciado.  
  
## <a name="see-also"></a>Vea también  
[Administrar el servicio del motor de base de datos](~/database-engine/configure-windows/manage-the-database-engine-services.md)  
[Configurar protocolos de cliente](~/database-engine/configure-windows/configure-client-protocols.md)  
[Protocolos de red y bibliotecas de red](~/sql-server/install/network-protocols-and-network-libraries.md)  
[Configuración de red de cliente](~/database-engine/configure-windows/client-network-configuration.md)  
[Configurar protocolos de cliente](~/database-engine/configure-windows/configure-client-protocols.md)  
[Habilitar o deshabilitar un protocolo de red de servidor](~/database-engine/configure-windows/enable-or-disable-a-server-network-protocol.md)  
  
