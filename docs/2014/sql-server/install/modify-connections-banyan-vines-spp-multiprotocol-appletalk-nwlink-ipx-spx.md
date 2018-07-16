---
title: Modificar las conexiones que utilizan protocolos de red de Banyan VINES protocolo (paquetes Secuenciados), Multiprotocolo, AppleTalk o NWLink IPX | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: conceptual
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
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 5b2b8e2d6ead66108b76d03bbfc020d9345afcd7
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/02/2018
ms.locfileid: "37296015"
---
# <a name="modify-connections-that-use-banyan-vines-sequenced-packet-protocol-spp-multiprotocol-appletalk-or-nwlink-ipx-spx-network-protocols"></a>Modificar las conexiones que utilizan protocolos de red de Banyan VINES protocolo (paquetes Secuenciados), Multiprotocolo, AppleTalk o NWLink IPX
  El Asesor de actualizaciones ha detectado protocolos de conectividad cliente-servidor que no se admiten en [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]. Las aplicaciones cliente que utilicen el protocolo de red SPP (Protocolo de paquetes secuenciados) de Banyan VINES o los protocolos de red Multiprotocolo (RPC), AppleTalk o NWLink IPX/SPX deben conectarse utilizando uno de los protocolos admitidos.  
  
## <a name="component"></a>Componente  
 [!INCLUDE[ssDE](../../includes/ssde-md.md)]  
  
## <a name="description"></a>Descripción  
 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] no es compatible con los protocolos de red SPP (Protocolo de paquetes secuenciados) de Banyan VINES, Multiprotocolo, AppleTalk o NWLink IPX/SPX. Los clientes anteriormente conectados con estos protocolos deben seleccionar uno distinto.  
  
## <a name="corrective-action"></a>Acción correctora  
 Modifique las aplicaciones cliente para utilizar un protocolo compatible al conectarlas con el servidor. Si ha configurado un alias que utiliza uno de los protocolos no compatibles, deberá modificar el alias para que utilice uno compatible.  
  
 Si la conexión de la aplicación de cadena específicamente utiliza o carga uno de estos protocolos, por cualquier red especificando = DBMSRPCN para RPC, NETWORK = DBMSADSN para Appletalk o NETWORK = DBMSVINN para la propiedad de Banyan VINES, o bien con un prefijo explícito como "spx: *servidor\instancia*"para SPX," bv:*server*"para Banyan VINES," adsp:*server*"para AppleTalk o" rpc:*server*"para multiprotocolo, a continuación, debe modificar la aplicación para usar uno de los protocolos admitidos.  
  
 Para obtener más información, vea "Elegir un protocolo de red" en los Libros en pantalla de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
## <a name="see-also"></a>Vea también  
 [Problemas de actualización de motor de base de datos](../../../2014/sql-server/install/database-engine-upgrade-issues.md)   
 [Asesor de actualizaciones de SQL Server 2014 &#91;nuevo&#93;](/sql/2014/sql-server/install/sql-server-2014-upgrade-advisor)  
  
  
