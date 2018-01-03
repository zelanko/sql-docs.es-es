---
title: Configurar el sistema externo de Windows para obtener copias de la tabla remota InfiniBand PDW
author: barbkess
ms.author: barbkess
manager: jhubbard
ms.prod: analytics-platform-system
ms.prod_service: mpp-data-warehouse
ms.service: 
ms.component: 
ms.technology: mpp-data-warehouse
ms.custom: 
ms.date: 01/13/2017
ms.reviewer: na
ms.suite: sql
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: f866890b-cad5-49ac-bbeb-848bfb26c2d5
caps.latest.revision: "11"
ms.openlocfilehash: efebff74a8c17952b39efb43006051603c624a03
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/21/2017
---
# <a name="configure-an-external-windows-system-to-receive-remote-table-copies-using-infiniband"></a>Configurar un sistema Windows externo para recibir copias de la tabla remota con InfiniBand
Describe cómo adquirir y configurar un sistema de Windows no sea de dispositivo conectado con la red InfiniBand para su uso con la característica de copia de la tabla remota en PDW de SQL Server. El sistema de Windows va a hospedar la base de datos de SQL Server que recibe la copia de la tabla remota de una base de datos de SQL Server PDW. Es comprado por separado en el dispositivo y conectado a la red InfiniBand de dispositivo.  
  
> [!NOTE]  
> Conexión a través de la red InfiniBand no es necesaria para poder usar copia de la tabla remota. Conexión a través de la red Ethernet puede realizarse si el ancho de banda de Ethernet satisface sus necesidades.  
  
En este tema se describe uno de los pasos de configuración para configurar la copia de la tabla remota. Para obtener una lista de todos los pasos de configuración, consulte [copia de tabla remota](remote-table-copy.md)  
  
## <a name="before-you-begin"></a>Antes de comenzar  
Antes de configurar el sistema externo de Windows, debe:  
  
1.  Adquirir o proporcionar un sistema de Windows que van a recibir copias remotas.  
  
2.  El sistema de Windows en el bastidor de Control en bastidor (si no hay suficiente espacio) o lo suficiente para el dispositivo para que se puedan conectarse a la red InfiniBand de dispositivo.  
  
3.  Adquirir InfiniBand cables y un adaptador de red InfiniBand de su proveedor de hardware de dispositivo. Se recomienda adquirir un adaptador de red con dos puertos de tolerancia a errores al recibir los datos exportados. Un adaptador de red de dos puertos se recomienda, pero no es un requisito.  
  
## <a name="HowToWindows"></a>Configurar un sistema Windows externo para recibir copias de la tabla remota  
Para configurar el sistema Windows externo, siga estos pasos:  
  
1.  Instalar al adaptador de red InfiniBand en el sistema de Windows.  
  
2.  Conectar el adaptador de red InfiniBand en el interruptor de InfiniBand principal en el bastidor de Control mediante cables de InfiniBand.  
  
3.  Instalar y configurar el controlador de Windows adecuado para el adaptador de red InfiniBand.  
  
    InfiniBand controladores para Windows se desarrollan mediante el OpenFabrics Alliance, un consorcio de la industria de proveedores de InfiniBand.  Puede que el controlador correcto se han distribuido con el adaptador de InfiniBand. De lo contrario, el controlador puede descargarse desde www.openfabrics.org.  
  
4.  Configure la dirección IP para cada puerto en el adaptador. Los sistemas SMP son necesarios para usar direcciones IP estáticas de un intervalo de direcciones reservadas para este propósito. Configurar el primer puerto según los parámetros siguientes:  
  
    -   Dirección de red IP: 172.16.132.x  
  
    -   Máscara de subred IP: 255.255.128.0  
  
    -   Intervalo IP host: 1-254  
  
    Para adaptadores de red InfiniBand con dos puertos, configure el segundo puerto de acuerdo con los parámetros siguientes:  
  
    -   Dirección de red IP: 172.16.132.x  
  
    -   Máscara de subred IP: 255.255.128.0  
  
    -   Intervalo IP host: 1-254  
  
5.  Si se usa un adaptador de dos puerto o varios sistemas externos de Windows están conectados a un dispositivo, asignar a cada sistema de un número de host diferente dentro de cada subred IP.  
  
<!-- MISSING LINKS 
## See Also  
[Common Metadata Query Examples &#40;SQL Server PDW&#41;](../sqlpdw/common-metadata-query-examples-sql-server-pdw.md)  
-->
  
