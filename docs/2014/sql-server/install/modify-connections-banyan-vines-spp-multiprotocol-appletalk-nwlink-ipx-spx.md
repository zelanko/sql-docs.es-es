---
title: Modificar las conexiones que usan los protocolos de red SPP (Protocolo de paquetes secuenciados) de Banyan VINEs, multiprotocolo, AppleTalk o NWLink IPX SPX | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
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
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: cdbcaa39e3d9630bd4ea50919f31cdbb15a36d14
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "66093898"
---
# <a name="modify-connections-that-use-banyan-vines-sequenced-packet-protocol-spp-multiprotocol-appletalk-or-nwlink-ipx-spx-network-protocols"></a>Modificar las conexiones que utilizan el protocolo de red SPP (Protocolo de paquetes secuenciados) de Banyan VINES o los protocolos Multiprotocolo, AppleTalk o NWLink IPX/SPX.
  El Asesor de actualizaciones ha detectado protocolos de conectividad cliente-servidor que no se admiten en [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]. Las aplicaciones cliente que utilicen el protocolo de red SPP (Protocolo de paquetes secuenciados) de Banyan VINES o los protocolos de red Multiprotocolo (RPC), AppleTalk o NWLink IPX/SPX deben conectarse utilizando uno de los protocolos admitidos.  
  
## <a name="component"></a>Componente  
 [!INCLUDE[ssDE](../../includes/ssde-md.md)]  
  
## <a name="description"></a>Descripción  
 
  [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] no es compatible con los protocolos de red SPP (Protocolo de paquetes secuenciados) de Banyan VINES, Multiprotocolo, AppleTalk o NWLink IPX/SPX. Los clientes anteriormente conectados con estos protocolos deben seleccionar uno distinto.  
  
## <a name="corrective-action"></a>Acción correctora  
 Modifique las aplicaciones cliente para utilizar un protocolo compatible al conectarlas con el servidor. Si ha configurado un alias que utiliza uno de los protocolos no compatibles, deberá modificar el alias para que utilice uno compatible.  
  
 Si la cadena de conexión de la aplicación usa o carga específicamente uno de estos protocolos, especificando NETWORK = DBMSRPCN para RPC, NETWORK = DBMSADSN para AppleTalk o NETWORK = DBMSVINN para la propiedad Banyan VINEs, o mediante un prefijo explícito como "SPX:*servidor\instancia*" para SPX, "BV:*Server*" para Banyan Vines, "ADSP:*Server*" para AppleTalk o "RPC:*Server*" para multiprotocolo, debe modificar la aplicación para que use uno de los protocolos admitidos.  
  
 Para obtener más información, vea "Elegir un protocolo de red" en los Libros en pantalla de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
## <a name="see-also"></a>Consulte también  
 [Problemas de actualización Motor de base de datos](../../../2014/sql-server/install/database-engine-upgrade-issues.md)   
 [SQL Server el asesor de actualizaciones de 2014 &#91;nuevo&#93;](sql-server-2014-upgrade-advisor.md)  
  
  
