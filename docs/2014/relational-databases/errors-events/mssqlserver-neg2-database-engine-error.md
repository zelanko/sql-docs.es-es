---
title: MSSQLSERVER_-2 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- "2"
helpviewer_keywords:
- -2 (Database Engine error)
ms.assetid: f37a7b7d-26e1-4b9e-bcb4-57f7805393d2
caps.latest.revision: 10
author: craigg-msft
ms.author: craigg
manager: jhubbard
ms.openlocfilehash: 118ae8a58abd20771ea5ff9b7bfad308832c4d79
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36106554"
---
# <a name="mssqlserver-2"></a>MSSQLSERVER_-2
    
## <a name="details"></a>Detalles  
  
|||  
|-|-|  
|Nombre del producto|SQL Server|  
|Identificador del evento|-2|  
|Origen del evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nombre simbólico||  
|Texto del mensaje|Valor de tiempo de espera expirado.  El tiempo de espera transcurrió antes de que se completase la operación, o bien el servidor no responde. (Microsoft SQL Server, Error: -2)|   
  
## <a name="explanation"></a>Explicación  
 El cliente de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] no se puede conectar al servidor. Este error puede producirse porque el firewall en el servidor ha rechazado la conexión. 
  
## <a name="user-action"></a>Acción del usuario  
 Asegúrese de haber configurado el firewall en la instancia del servidor de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para aceptar las conexiones.  
  
## <a name="see-also"></a>Vea también  
 [Configurar el Firewall de Windows para permitir el acceso a SQL Server](../../sql-server/install/configure-the-windows-firewall-to-allow-sql-server-access.md)   
 [Configurar Firewall de Windows para obtener acceso al motor de base de datos](../../database-engine/configure-windows/configure-a-windows-firewall-for-database-engine-access.md)   
 [Configurar protocolos de cliente](../../database-engine/configure-windows/configure-client-protocols.md)   
 [Protocolos de red y bibliotecas de red](../../sql-server/install/network-protocols-and-network-libraries.md)   
 [Configuración de red de cliente](../../database-engine/configure-windows/client-network-configuration.md)   
 [Configurar protocolos de cliente](../../database-engine/configure-windows/configure-client-protocols.md)   
 [Habilitar o deshabilitar un protocolo de red de servidor](../../database-engine/configure-windows/enable-or-disable-a-server-network-protocol.md)  
  
