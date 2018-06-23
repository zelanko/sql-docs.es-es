---
title: Modificar las conexiones que utilizan protocolos de red de protocolo de paquetes de secuencia (SPP) de Banyan VINES, Multiprotocolo, AppleTalk o NWLink IPX | Documentos de Microsoft
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- network protocols [SQL Server], modifying connections
- SPP [SQL Server]
- NWLink IPX/SPX [SQL Server]
- connections [SQL Server]
- AppleTalk [SQL Server]
- Sequenced Packet Protocol [SQL Server]
- Multiprotocol Net-Library [SQL Server]
- Banyan VINES Sequenced Package Protocol [SQL Server]
- IPX/SPX [SQL Server]
- protocols [SQL Server], modifying connections
- RPC [SQL Server]
ms.assetid: 5c5ae453-cc5b-4898-95c7-ad34157b1f60
caps.latest.revision: 20
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: 0167af6c11abb12e8aa38a52a77707b81aecbe78
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36107815"
---
# <a name="modify-connections-that-use-banyan-vines-sequenced-packet-protocol-spp-multiprotocol-appletalk-or-nwlink-ipx-spx-network-protocols"></a>Modificar las conexiones que utilizan protocolos de red de protocolo de paquetes de secuencia (SPP) de Banyan VINES, Multiprotocolo, AppleTalk o NWLink IPX
  El Asesor de actualizaciones ha detectado protocolos de conectividad cliente-servidor que no se admiten en [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]. Las aplicaciones cliente que utilicen el protocolo de red SPP (Protocolo de paquetes secuenciados) de Banyan VINES o los protocolos de red Multiprotocolo (RPC), AppleTalk o NWLink IPX/SPX deben conectarse utilizando uno de los protocolos admitidos.  
  
## <a name="component"></a>Componente  
 [!INCLUDE[ssDE](../../includes/ssde-md.md)]  
  
## <a name="description"></a>Descripción  
 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] no es compatible con los protocolos de red SPP (Protocolo de paquetes secuenciados) de Banyan VINES, Multiprotocolo, AppleTalk o NWLink IPX/SPX. Los clientes anteriormente conectados con estos protocolos deben seleccionar uno distinto.  
  
## <a name="corrective-action"></a>Acción correctora  
 Modifique las aplicaciones cliente para utilizar un protocolo compatible al conectarlas con el servidor. Si ha configurado un alias que utiliza uno de los protocolos no compatibles, deberá modificar el alias para que utilice uno compatible.  
  
 Si la conexión de aplicación cadena específicamente utiliza o carga uno de estos protocolos, ya sea especificando red = DBMSRPCN para RPC, red = DBMSADSN para Appletalk o red = DBMSVINN para la propiedad de Banyan VINES, o mediante un prefijo explícito como "spx: *servidor\instancia*"para SPX," bv:*server*"para Banyan VINES," adsp:*server*"para AppleTalk o" rpc:*server*"para multiprotocolo, a continuación, debe modificar la aplicación para usar uno de los protocolos admitidos.  
  
 Para obtener más información, vea "Elegir un protocolo de red" en los Libros en pantalla de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
## <a name="see-also"></a>Vea también  
 [Problemas de actualización de motor de base de datos](../../../2014/sql-server/install/database-engine-upgrade-issues.md)   
 [Asesor de actualizaciones de SQL Server 2014 &#91;nuevo&#93;](/sql/2014/sql-server/install/sql-server-2014-upgrade-advisor)  
  
  
