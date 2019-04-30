---
title: Configurar Windows para recibir copias de la tabla remota - almacenamiento de datos paralelos | Microsoft Docs
description: Describe cómo comprar y configurar un sistema de Windows que no sea de dispositivo conectado con la red InfiniBand para su uso con la característica de copia de la tabla remota en el almacenamiento de datos paralelos. El sistema de Windows va a hospedar la base de datos de SQL Server que recibe la copia de la tabla remota de una base de datos de SQL Server PDW. Se se compran por separado desde el dispositivo y conectado a la red InfiniBand de dispositivo.
author: mzaman1
manager: craigg
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.openlocfilehash: ed7122f497b0bdebd893eec75606bbb6382e9a73
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "63224858"
---
# <a name="configure-an-external-windows-system-to-receive-remote-table-copies-using-infiniband---parallel-data-warehouse"></a>Configurar un sistema externo de Windows para recibir copias de la tabla remota con InfiniBand - almacenamiento de datos paralelos
Describe cómo comprar y configurar un sistema de Windows que no sea de dispositivo conectado con la red InfiniBand para su uso con la característica de copia de la tabla remota en PDW de SQL Server. El sistema de Windows va a hospedar la base de datos de SQL Server que recibe la copia de la tabla remota de una base de datos de SQL Server PDW. Se se compran por separado desde el dispositivo y conectado a la red InfiniBand de dispositivo.  
  
> [!NOTE]  
> Conexión a través de la red InfiniBand no es necesario para poder usar la copia de la tabla remota. Conexión a través de la red Ethernet puede realizarse si el ancho de banda de Ethernet satisface sus necesidades.  
  
Este tema describe uno de los pasos de configuración para configurar la copia de la tabla remota. Para obtener una lista de todos los pasos de configuración, consulte [copia de la tabla remota](remote-table-copy.md)  
  
## <a name="before-you-begin"></a>Antes de empezar  
Antes de configurar el sistema externo de Windows, debe:  
  
1.  Adquirir o proporcionar un sistema de Windows que va a recibir la copia remota.  
  
2.  El sistema de Windows en el bastidor de Control en bastidor (si hay suficiente espacio) o cerrar lo suficiente como para el dispositivo de manera que puede conectarse a la red InfiniBand de dispositivo.  
  
3.  Comprar InfiniBand cables y un adaptador de red InfiniBand de su proveedor de hardware del dispositivo. Se recomienda adquirir un adaptador de red con dos puertos para tolerancia a errores al recibir los datos exportados. Se recomienda un adaptador de red de dos puertos, pero no es un requisito.  
  
## <a name="HowToWindows"></a>Configurar un sistema externo de Windows para recibir copias de la tabla remota  
Para configurar el sistema externo de Windows, siga estos pasos:  
  
1.  Instalar al adaptador de red InfiniBand en el sistema de Windows.  
  
2.  Conecte el adaptador de red InfiniBand al conmutador InfiniBand principal en el bastidor de Control con cables InfiniBand.  
  
3.  Instale y configure el controlador de Windows adecuado para el adaptador de red InfiniBand.  
  
    Controladores de InfiniBand para Windows se desarrollan por OpenFabrics Alliance, un consorcio del sector de los proveedores de InfiniBand.  Es posible que el controlador correcto se han distribuido con el adaptador de InfiniBand. Si no es así, el controlador puede descargarse desde www.openfabrics.org.  
  
4.  Configurar la dirección IP para cada puerto en el adaptador. Los sistemas SMP son necesarios para usar direcciones IP estáticas desde un intervalo de direcciones reservados para este propósito. Configurar el primer puerto de acuerdo con los parámetros siguientes:  
  
    -   Dirección IP de red: 172.16.132.x  
  
    -   Máscara de subred IP: 255.255.128.0  
  
    -   Intervalo de host IP: 1-254  
  
    Para adaptadores de red InfiniBand con dos puertos, configure el segundo puerto de acuerdo con los parámetros siguientes:  
  
    -   Dirección IP de red: 172.16.132.x  
  
    -   Máscara de subred IP: 255.255.128.0  
  
    -   Intervalo de host IP: 1-254  
  
5.  Si se usa un adaptador de puerto de dos o varios sistemas externos de Windows están conectados a un dispositivo, asigne cada sistema un número diferente de host dentro de cada subred IP.  
  
<!-- MISSING LINKS 
## See Also  
[Common Metadata Query Examples &#40;SQL Server PDW&#41;](../sqlpdw/common-metadata-query-examples-sql-server-pdw.md)  
-->
  
