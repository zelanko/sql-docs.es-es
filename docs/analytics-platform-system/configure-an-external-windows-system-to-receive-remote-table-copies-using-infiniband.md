---
title: Configurar Windows para recibir copias de la tabla remota
description: Describe cómo adquirir y configurar un sistema de Windows que no es de aplicación conectado mediante la red InfiniBand para su uso con la característica de copia de tabla remota en almacenamiento de datos paralelos. El sistema de Windows hospedará el SQL Server base de datos que recibe la copia de la tabla remota de una base de datos de PDW de SQL Server. Se compra por separado del dispositivo y se conecta a la red InfiniBand de la aplicación.
author: mzaman1
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.custom: seo-dt-2019
ms.openlocfilehash: 837d41cc929d90b2494682645127f985b5768546
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/27/2020
ms.locfileid: "74401313"
---
# <a name="configure-an-external-windows-system-to-receive-remote-table-copies-using-infiniband---parallel-data-warehouse"></a>Configuración de un sistema externo de Windows para recibir copias de la tabla remota mediante el almacenamiento de datos de InfiniBand-Parallel
Describe cómo adquirir y configurar un sistema de Windows que no es de dispositivo conectado mediante la red InfiniBand para su uso con la característica de copia de tabla remota en PDW de SQL Server. El sistema de Windows hospedará el SQL Server base de datos que recibe la copia de la tabla remota de una base de datos de PDW de SQL Server. Se compra por separado del dispositivo y se conecta a la red InfiniBand de la aplicación.  
  
> [!NOTE]  
> La conexión a través de la red InfiniBand no es necesaria para usar la copia de tabla remota. La conexión a través de la red Ethernet puede realizarse si el ancho de banda Ethernet satisface sus necesidades.  
  
En este tema se describe uno de los pasos de configuración para configurar la copia de tabla remota. Para obtener una lista de todos los pasos de configuración, consulte [copia de tabla remota](remote-table-copy.md)  
  
## <a name="before-you-begin"></a>Antes de empezar  
Antes de configurar el sistema externo de Windows, debe:  
  
1.  Compre o proporcione un sistema de Windows que recibirá las copias remotas.  
  
2.  Bastidor del sistema de Windows en el bastidor del control (si hay suficiente espacio) o lo suficientemente cerca del dispositivo para poder conectarlo a la red InfiniBand de la aplicación.  
  
3.  Compre cables InfiniBand y un adaptador de red InfiniBand del fabricante del hardware del dispositivo. Se recomienda adquirir un adaptador de red con dos puertos para la tolerancia a errores al recibir los datos exportados. Se recomienda un adaptador de red de dos puertos, pero no es un requisito.  
  
## <a name="configure-an-external-windows-system-to-receive-remote-table-copies"></a><a name="HowToWindows"></a>Configurar un sistema externo de Windows para recibir copias de la tabla remota  
Para configurar el sistema externo de Windows, siga estos pasos:  
  
1.  Instale el adaptador de red InfiniBand en el sistema Windows.  
  
2.  Conecte el adaptador de red InfiniBand al conmutador InfiniBand principal del bastidor de control mediante cables InfiniBand.  
  
3.  Instale y configure el controlador de Windows adecuado para el adaptador de red InfiniBand.  
  
    Los controladores de InfiniBand para Windows son desarrollados por OpenFabrics Alliance, un consorcio del sector de InfiniBand vendors.  Es posible que se haya distribuido el controlador correcto con el adaptador InfiniBand. Si no es así, el controlador se puede descargar desde www.openfabrics.org.  
  
4.  Configure la dirección IP de cada puerto en el adaptador. Los sistemas SMP deben usar direcciones IP estáticas de un intervalo de direcciones reservadas para este fin. Configure el primer puerto según los parámetros siguientes:  
  
    -   Dirección de red IP: 172.16.132. x  
  
    -   Máscara de subred IP: 255.255.128.0  
  
    -   Intervalo del host IP: 1-254  
  
    Para adaptadores de red de InfiniBand con dos puertos, configure el segundo puerto según los parámetros siguientes:  
  
    -   Dirección de red IP: 172.16.132. x  
  
    -   Máscara de subred IP: 255.255.128.0  
  
    -   Intervalo del host IP: 1-254  
  
5.  Si se usa un adaptador de dos puertos o hay varios sistemas de Windows externos conectados a un dispositivo, asigne a cada sistema un número de host diferente dentro de cada subred IP.  
  
<!-- MISSING LINKS 
## See Also  
[Common Metadata Query Examples &#40;SQL Server PDW&#41;](../sqlpdw/common-metadata-query-examples-sql-server-pdw.md)  
-->
  
