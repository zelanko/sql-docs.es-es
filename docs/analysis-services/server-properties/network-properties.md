---
title: Propiedades de red | Documentos de Microsoft
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: server-properties
ms.reviewer: 
ms.suite: sql
ms.technology: analysis-services
ms.tgt_pltfrm: 
ms.topic: reference
helpviewer_keywords:
- LingerTimeout property
- EnableNagleAlgorithm property
- MinPendingAcceptExCount property
- MaxPendingSendCount property
- EnableBinaryXML property
- MinPendingReceiveCount property
- MaxCompletedReceiveCount property
- DisableNonblockingMode property
- RequestSizeThreshold property
- CompressionLevel property
- ReceiveBufferSize property
- EnableCompression property
- ServerSendTimeout property
- IPV4Support property
- MaxPendingReceiveCount property
- MaxPendingAcceptExCount property
- IPV6Support property
- MaxAllowedRequestSize property
- ServerReceiveTimeout property
- EnableLingerOnClose property
- InitialConnectTimeout property
- SendBufferSize property
- ScatterReceiveMultiplier property
- network properties [Analysis Services]
ms.assetid: ef4251e2-abe5-4c5b-9868-7549782d0244
caps.latest.revision: "15"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 0fa82c8c8f63c7a268c057f1009c44acde809893
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/17/2017
---
# <a name="network-properties"></a>Propiedades de red
  [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] admite las propiedades de servidor descritas en las siguientes tablas. Para más información sobre otras propiedades de servidor y cómo establecerlas, vea [Configurar las propiedades de servidor en Analysis Services](../../analysis-services/server-properties/server-properties-in-analysis-services.md).  
  
 **Se aplica a:** modo de servidor multidimensional y tabular  
  
## <a name="general"></a>General  
 **ListenOnlyOnLocalConnections**  
 Una propiedad booleana que identifica si se va a escuchar solo en conexiones locales, por ejemplo localhost.  
  
## <a name="listener"></a>Escucha  
 **IPV4Support**  
 Una propiedad de entero de 32 bits con signo que define la compatibilidad con el protocolo IPv4. Esta propiedad tiene uno de los valores descritos en la tabla siguiente:  
  
|Value|Descripción|  
|-----------|-----------------|  
|*0*|IPv4 deshabilitado; los clientes no pueden conectarse.|  
|*1*|(Predeterminado) IPv4 es obligatorio; el servidor no se iniciará si no puede escuchar a IPv4.|  
|*2*|IPv4 es opcional; el servidor intenta escuchar a IPv4 pero se inicia en caso de no poder hacerlo.|  
  
 **IPV6Support**  
 Una propiedad de entero de 32 bits con signo que define la compatibilidad con el protocolo IPv6. Esta propiedad tiene uno de los valores descritos en la tabla siguiente:  
  
|Value|Descripción|  
|-----------|-----------------|  
|*0*|IPv6 deshabilitado; los clientes no pueden conectarse.|  
|*1*|(Predeterminado) IPv6 es obligatorio; el servidor no se iniciará si no puede escuchar a IPv6.|  
|*2*|IPv4 es opcional; el servidor intenta escuchar a IPv6 pero se inicia en caso de no poder hacerlo.|  
  
 **MaxAllowedRequestSize**  
 Una propiedad avanzada que no debería cambiar, salvo a petición de expertos en soporte técnico de [!INCLUDE[msCoName](../../includes/msconame-md.md)] .  
  
 **RequestSizeThreshold**  
 Una propiedad avanzada que no debería cambiar, salvo a petición de expertos en soporte técnico de [!INCLUDE[msCoName](../../includes/msconame-md.md)] .  
  
 **ServerReceiveTimeout**  
 Una propiedad avanzada que no debería cambiar, salvo a petición de expertos en soporte técnico de [!INCLUDE[msCoName](../../includes/msconame-md.md)] .  
  
 **ServerSendTimeout**  
 Una propiedad avanzada que no debería cambiar, salvo a petición de expertos en soporte técnico de [!INCLUDE[msCoName](../../includes/msconame-md.md)] .  
  
## <a name="requests"></a>Solicitudes  
 **EnableBinaryXML**  
 Una propiedad booleana que especifica si el servidor reconoce el formato XML binario de las solicitudes.  
  
 **EnableCompression**  
 Una propiedad booleana que especifica si la compresión está habilitada para las solicitudes.  
  
## <a name="responses"></a>Respuestas  
 **CompressionLevel**  
 Una propiedad avanzada que no debería cambiar, salvo a petición de expertos en soporte técnico de [!INCLUDE[msCoName](../../includes/msconame-md.md)] .  
  
 **EnableBinaryXML**  
 Una propiedad booleana que especifica si el servidor está habilitado para respuestas XML binarias.  
  
 **EnableCompression**  
 Una propiedad booleana que especifica si la compresión está habilitada para respuestas a solicitudes de cliente.  
  
## <a name="tcp"></a>TCP  
 **InitialConnectTimeout**  
 Una propiedad avanzada que no debería cambiar, salvo a petición de expertos en soporte técnico de [!INCLUDE[msCoName](../../includes/msconame-md.md)] .  
  
 **MaxCompletedReceiveCount**  
 Una propiedad avanzada que no debería cambiar, salvo a petición de expertos en soporte técnico de [!INCLUDE[msCoName](../../includes/msconame-md.md)] .  
  
 **MaxPendingAcceptExCount**  
 Una propiedad avanzada que no debería cambiar, salvo a petición de expertos en soporte técnico de [!INCLUDE[msCoName](../../includes/msconame-md.md)] .  
  
 **MaxPendingReceiveCount**  
 Una propiedad avanzada que no debería cambiar, salvo a petición de expertos en soporte técnico de [!INCLUDE[msCoName](../../includes/msconame-md.md)] .  
  
 **MaxPendingSendCount**  
 Una propiedad avanzada que no debería cambiar, salvo a petición de expertos en soporte técnico de [!INCLUDE[msCoName](../../includes/msconame-md.md)] .  
  
 **MinPendingAcceptExCount**  
 Una propiedad avanzada que no debería cambiar, salvo a petición de expertos en soporte técnico de [!INCLUDE[msCoName](../../includes/msconame-md.md)] .  
  
 **MinPendingReceiveCount**  
 Una propiedad avanzada que no debería cambiar, salvo a petición de expertos en soporte técnico de [!INCLUDE[msCoName](../../includes/msconame-md.md)] .  
  
 **ScatterReceiveMultiplier**  
 Una propiedad avanzada que no debería cambiar, salvo a petición de expertos en soporte técnico de [!INCLUDE[msCoName](../../includes/msconame-md.md)] .  
  
 **SocketOptions\ DisableNonblockingMode**  
 Una propiedad avanzada que no debería cambiar, salvo a petición de expertos en soporte técnico de [!INCLUDE[msCoName](../../includes/msconame-md.md)] .  
  
 **SocketOptions\ EnableLingerOnClose**  
 Una propiedad avanzada que no debería cambiar, salvo a petición de expertos en soporte técnico de [!INCLUDE[msCoName](../../includes/msconame-md.md)] .  
  
 **SocketOptions\EnableNagleAlgorithm**  
 Una propiedad avanzada que no debería cambiar, salvo a petición de expertos en soporte técnico de [!INCLUDE[msCoName](../../includes/msconame-md.md)] .  
  
 **SocketOptions\ LingerTimeout**  
 Una propiedad avanzada que no debería cambiar, salvo a petición de expertos en soporte técnico de [!INCLUDE[msCoName](../../includes/msconame-md.md)] .  
  
 **SocketOptions\ ReceiveBufferSize**  
 Una propiedad avanzada que no debería cambiar, salvo a petición de expertos en soporte técnico de [!INCLUDE[msCoName](../../includes/msconame-md.md)] .  
  
 **SocketOptions\ SendBufferSize**  
 Una propiedad avanzada que no debería cambiar, salvo a petición de expertos en soporte técnico de [!INCLUDE[msCoName](../../includes/msconame-md.md)] .  
  
## <a name="see-also"></a>Vea también  
 [Configurar las propiedades de servidor en Analysis Services](../../analysis-services/server-properties/server-properties-in-analysis-services.md)   
 [Determinar el modo de servidor de una instancia de Analysis Services](../../analysis-services/instances/determine-the-server-mode-of-an-analysis-services-instance.md)  
  
  
