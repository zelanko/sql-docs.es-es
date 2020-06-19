---
title: MSSQLSERVER_10061 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
f1_keywords:
- "10061"
helpviewer_keywords:
- 10061 (Database Engine error)
ms.assetid: 729602f3-08df-474c-8740-8dea13c1eee3
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: d1b93e48814a1d092e2d39982f198c1779c8396e
ms.sourcegitcommit: f71e523da72019de81a8bd5a0394a62f7f76ea20
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/17/2020
ms.locfileid: "84969855"
---
# <a name="mssqlserver_10061"></a>MSSQLSERVER_10061
    
## <a name="details"></a>Detalles  
  
|||  
|-|-|  
|Nombre de producto|SQL Server|  
|Id. de evento|10061|  
|Origen de eventos|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nombre simbólico||  
|Texto del mensaje|Error al establecer una conexión al servidor.  La causa del problema en la conexión a SQL Server puede deberse a que SQL Server no permite conexiones remotas en su configuración predeterminada. (proveedor: proveedor TCP, error: 0 - No se pudo establecer conexión porque el equipo de destino rechazó.) (Microsoft SQL Server, Error: 10061)|  
  
## <a name="explanation"></a>Explicación  
 El servidor no respondió a la solicitud del cliente. Este error puede producirse porque el servidor no se ha iniciado.  
  
## <a name="user-action"></a>Acción del usuario  
 Asegúrese de que el servidor se haya iniciado.  
  
## <a name="see-also"></a>Consulte también  
 [Administrar los servicios de Motor de base de datos](../../database-engine/configure-windows/manage-the-database-engine-services.md)   
 [Configurar protocolos de cliente](../../database-engine/configure-windows/configure-client-protocols.md)   
 [Protocolos de red y bibliotecas de red](../../sql-server/install/network-protocols-and-network-libraries.md)   
 [Configuración de red de cliente](../../database-engine/configure-windows/client-network-configuration.md)   
 [Configurar protocolos de cliente](../../database-engine/configure-windows/configure-client-protocols.md)   
 [Habilitar o deshabilitar un protocolo de red de servidor](../../database-engine/configure-windows/enable-or-disable-a-server-network-protocol.md)  
  
  
