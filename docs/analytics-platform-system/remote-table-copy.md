---
title: Copia de la tabla remota
description: Uso de la copia de tabla remota en el almacenamiento de datos paralelos de la plataforma de análisis.
author: mzaman1
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.custom: seo-dt-2019
ms.openlocfilehash: ecbbdced731e940de46dbde4a65adc486f602c2f
ms.sourcegitcommit: d587a141351e59782c31229bccaa0bff2e869580
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/22/2019
ms.locfileid: "74400478"
---
# <a name="remote-table-copy"></a>Copia de tabla remota
Describe cómo usar la característica de copia de tabla remota para copiar tablas de PDW de SQL Server bases de datos en bases de datos de SMP SQL Server remoto (no de aplicación). Use la copia de tabla remota para habilitar escenarios de concentrador y radio para PDW de SQL Server.  
  
## <a name="BasicsPDE"></a>Descripción de la copia de tabla remota para PDW de SQL Server  
La copia remota de tabla es una característica de PDW de SQL Server que permite escenarios de concentrador y radio mediante la copia de los resultados de una instrucción SELECT de SQL en una tabla de una base de datos SMP. La copia de la tabla remota se inicia con la instrucción [Create REMOTE Table as Select](../t-sql/statements/create-remote-table-as-select-parallel-data-warehouse.md) .  
  
## <a name="BasicsPrerequisites"></a>Requisitos para usar la copia de tabla remota  
Puede usar la copia de tabla remota para copiar tablas de PDW de SQL Server a una base de datos de SQL Server cuando se cumplan estas condiciones:  
  
-   La base de datos de destino debe ser una instancia de Microsoft® SQL Server® que se esté ejecutando en un sistema de Microsoft Windows® que pueda conectarse al dispositivo de PDW de SQL Server, pero que no se encuentre en un servidor del dispositivo. El SQL Server remoto se puede conectar al PDW de SQL Server mediante la red InfiniBand o a través de la red Ethernet.  
  
-   Los datos que se van a copiar deben seleccionarse mediante una sola instrucción [Select](../t-sql/queries/select-transact-sql.md) de PDW de SQL Server válida.  
  
-   El servidor de destino debe ser un servidor que no sea de dispositivo. Los datos no se pueden copiar directamente de un dispositivo a otro siguiendo las instrucciones de este tema.  
  
-   El servidor de destino debe ser accesible para todos los nodos de la red InfiniBand del dispositivo.  
  
## <a name="ConfigureRemote"></a>Configurar la copia de tabla remota  
Para usar la copia de tabla remota, debe adquirir y configurar un servidor de Windows, configurar SQL Server en el servidor de Windows y configurar PDW de SQL Server. Use los vínculos siguientes para realizar estos tres pasos de configuración.  
  
1.  [Configurar un sistema externo de Windows para recibir copias de la tabla remota mediante InfiniBand](configure-an-external-windows-system-to-receive-remote-table-copies-using-infiniband.md)  
  
2.  [Configurar un SQL Server SMP externo para recibir copias de la tabla remota](configure-an-external-smp-sql-server-to-receive-remote-table-copies.md)  
  
3.  [Configurar PDW de SQL Server para copias de tablas remotas](configure-sql-server-pdw-for-remote-table-copies.md)  
  
## <a name="PerformRemote"></a>Realización de una copia de tabla remota  
Para realizar una copia de la tabla remota, use la instrucción [Create REMOTE Table as Select](../t-sql/statements/create-remote-table-as-select-parallel-data-warehouse.md) SQL. Los ejemplos se incluyen en el tema CREATE Remote TABLE.  
  
<!-- MISSING LINKS 
## See Also  
[Common Metadata Query Examples &#40;SQL Server PDW&#41;](../sqlpdw/common-metadata-query-examples-sql-server-pdw.md)  
-->
  
