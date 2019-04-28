---
title: MSSQLSERVER_10060 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
f1_keywords:
- "10060"
helpviewer_keywords:
- 10060 (Database Engine error)
ms.assetid: 28c21277-cad8-406c-a955-07933a56982a
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: ee37bfd2c2ba17377589f8a3e744cc018b9d5775
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "62870792"
---
# <a name="mssqlserver10060"></a>MSSQLSERVER_10060
    
## <a name="details"></a>Detalles  
  
|||  
|-|-|  
|Nombre del producto|SQL Server|  
|Identificador del evento|10060|  
|Origen del evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nombre simbólico||  
|Texto del mensaje|Error al establecer una conexión al servidor.  La causa del problema en la conexión a SQL Server puede deberse a que SQL Server no permite conexiones remotas en su configuración predeterminada. (proveedor: Proveedor TCP, error: 0 - Se produjo un error durante el intento de conexión ya que la parte conectada no respondió adecuadamente tras un periodo de tiempo, o bien se produjo un error en la conexión establecida ya que el host conectado no ha podido responder). (Microsoft SQL Server, Error: 10060)|  
  
## <a name="explanation"></a>Explicación  
 El cliente de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] no se puede conectar al servidor. Este error se puede producir porque el firewall en el servidor ha rechazado la conexión o el servidor no está configurado para aceptar conexiones remotas.  
  
## <a name="user-action"></a>Acción del usuario  
 Para resolver este error, intente una de las siguientes acciones:  
  
-   Asegúrese de haber configurado el firewall en el equipo de modo que esta instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] acepte conexiones.  
  
-   Use la herramienta Administrador de configuración de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para que [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] acepte conexiones remotas.  
  
## <a name="see-also"></a>Vea también  
 [Configurar un Firewall de Windows para acceder al motor de base de datos](../../database-engine/configure-windows/configure-a-windows-firewall-for-database-engine-access.md)   
 [Configurar protocolos de cliente](../../database-engine/configure-windows/configure-client-protocols.md)   
 [Protocolos de red y bibliotecas de red](../../sql-server/install/network-protocols-and-network-libraries.md)   
 [Configuración de red de cliente](../../database-engine/configure-windows/client-network-configuration.md)   
 [Configurar protocolos de cliente](../../database-engine/configure-windows/configure-client-protocols.md)   
 [Habilitar o deshabilitar un protocolo de red de servidor](../../database-engine/configure-windows/enable-or-disable-a-server-network-protocol.md)  
  
  
