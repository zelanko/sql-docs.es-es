---
title: Asignación de puertos TCP/IP a nodos NUMA (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: high-availability
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
helpviewer_keywords:
- NUMA
- memory [SQL Server], NUMA
- affinity NUMA
- ports [SQL Server], working with NUMA
- CPU [SQL Server], NUMA support
- NUMA, How to map a port to a NUMA node
- NUMA affinity
- TCP/IP [SQL Server], NUMA support
- non-uniform memory access
ms.assetid: 07727642-0266-4cbc-8c55-3c367e4458ca
author: MikeRayMSFT
ms.author: mikeray
manager: jroth
ms.openlocfilehash: b5179b48634aae9a55e2670ddb0a0055861ffa31
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "66783263"
---
# <a name="map-tcp-ip-ports-to-numa-nodes-sql-server"></a>Asignación de puertos TCP/IP a nodos NUMA (SQL Server)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  En este tema se describe cómo asignar puertos TCP/IP a los nodos de acceso a memoria no uniforme (NUMA) mediante el Administrador de configuración de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Durante el inicio, el [!INCLUDE[ssDE](../../includes/ssde-md.md)] escribe la información del nodo en el registro de errores.  
  
 Para determinar el número de nodo correspondiente al nodo que quiere usar, lea la información del nodo en el registro de errores o en la vista **sys.dm_os_schedulers** . Para asignar una dirección y un puerto TCP/IP a uno o a varios nodos, adjunte un mapa de bits de identificación del nodo (una máscara de afinidad) entre paréntesis después del número de puerto. Los nodos se pueden especificar en formato decimal o hexadecimal. Para crear el mapa de bits, primero numere los nodos de derecha a izquierda empezando por cero, como en 76543210. Cree una representación binaria de la lista de nodos, especificando 1 para los nodos que desee usar y 0 para los que no vaya a utilizar. Por ejemplo, para usar los nodos NUMA 0, 2 y 5, deberá especificar 00100101.  
  
|||  
|-|-|  
|Número de nodo NUMA|76543210|  
|Máscara para 0, 2 y 5 contando desde la derecha|00100101|  
  
 Convierta la representación binaria (00100101) en decimal `[37]`o en hexadecimal `[0x25]`. Para escuchar en todos los nodos, no especifique ningún identificador de nodo.  
  
 Si un puerto está asignado a varios nodos NUMA, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] asigna conexiones a los nodos por turnos sin intentar equilibrar la carga entre los nodos.  
  
> [!NOTE]  
>  Para habilitar [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] de modo que escuche en varios puertos TCP para cada dirección IP, vea [Configurar el motor de base de datos para escuchar en varios puertos TCP](../../database-engine/configure-windows/configure-the-database-engine-to-listen-on-multiple-tcp-ports.md).  
  
##  <a name="SSMSProcedure"></a> Usar el Administrador de configuración de SQL Server  
  
#### <a name="to-map-a-tcpip-port-to-a-numa-node"></a>Para asignar un puerto TCP/IP a un nodo NUMA  
  
1.  En el Administrador de configuración de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], expanda **Configuración de red de SQL Server** y, después, haga clic en **Protocolos de** *\<nombre de instancia>*.  
  
2.  En el panel de detalles, haga doble clic en **TCP/IP**.  
  
3.  En la pestaña **Direcciones IP** , en la sección correspondiente a la dirección IP que se va a configurar, en el cuadro **Puerto TCP** , agregue el identificador del nodo NUMA entre paréntesis a continuación del número de puerto. Por ejemplo, para el puerto TCP 1500 y los nodos 0, 2 y 5, use **1500[37]** o **1500[0x25]**.  
  
## <a name="see-also"></a>Consulte también  
 [Soft-NUMA &#40;SQL Server&#41;](../../database-engine/configure-windows/soft-numa-sql-server.md)  
  
  
