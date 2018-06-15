---
title: Copia de la tabla remota - almacenamiento de datos paralelos | Documentos de Microsoft
description: Mediante copia de la tabla remota en almacenamiento de datos paralelos de sistema de plataforma de análisis.
author: mzaman1
manager: craigg
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.openlocfilehash: 5ed517a471368e4192ad7393a92274424d37f975
ms.sourcegitcommit: 056ce753c2d6b85cd78be4fc6a29c2b4daaaf26c
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/19/2018
ms.locfileid: "31538725"
---
# <a name="remote-table-copy"></a>Copia de la tabla remota
Describe cómo usar la característica de copia de la tabla remota para copiar tablas de bases de datos de SQL Server PDW a las bases de datos de SMP SQL Server remotos de (que no sea de dispositivo). Usar copia de la tabla remota a habilita escenarios de concentrador y radio para PDW de SQL Server.  
  
## <a name="BasicsPDE"></a>Comprender la copia de la tabla remota de SQL Server PDW  
Copia de la tabla remota es una característica de PDW de SQL Server que permite escenarios de concentrador y radio copiando los resultados de una instrucción SELECT de SQL en una tabla en una base de datos SMP. Se inicia la copia de la tabla remota con la [CREATE remoto TABLE AS SELECT](../t-sql/statements/create-remote-table-as-select-parallel-data-warehouse.md) instrucción.  
  
## <a name="BasicsPrerequisites"></a>Requisitos para usar la copia de la tabla remota  
Puede usar tablas de copiar para copiar de tabla remota de SQL Server PDW a una base de datos de SQL Server cuando se cumplen estas condiciones:  
  
-   La base de datos de destino debe ser una instancia de Microsoft® SQL Server® que se ejecuta en un sistema de Microsoft Windows® que puede conectarse al dispositivo PDW de SQL Server pero que no reside en un servidor en el dispositivo. El servidor SQL Server remoto puede estar conectado a SQL Server PDW con la red InfiniBand o a través de la red Ethernet.  
  
-   Los datos que se va a copiar deben ser seleccionables con un único válido SQL Server PDW [seleccione](../t-sql/queries/select-transact-sql.md) instrucción.  
  
-   El servidor de destino debe ser un servidor que no sea de dispositivo. No se puede copiar datos directamente desde un dispositivo a otro utilizando las instrucciones que aparecen en este tema.  
  
-   El servidor de destino debe ser accesible para todos los nodos en la red del dispositivo Infiniband.  
  
## <a name="ConfigureRemote"></a>Configurar copia de la tabla remota  
Para usar la copia de la tabla remota, se necesita adquirir y configurar un servidor de Windows, configurar SQL Server en el servidor de Windows y configurar SQL Server PDW. Use los vínculos siguientes para realizar estos pasos de configuración de tres.  
  
1.  [Configurar un sistema Windows externo para recibir copias de la tabla remota con InfiniBand](configure-an-external-windows-system-to-receive-remote-table-copies-using-infiniband.md)  
  
2.  [Configurar un servidor externo de SMP de SQL para reciben una copia de la tabla remota](configure-an-external-smp-sql-server-to-receive-remote-table-copies.md)  
  
3.  [Configurar SQL Server PDW para copias de la tabla remota](configure-sql-server-pdw-for-remote-table-copies.md)  
  
## <a name="PerformRemote"></a>Realizar una copia de la tabla remota  
Para realizar una copia de la tabla remota, use la [CREATE remoto TABLE AS SELECT](../t-sql/statements/create-remote-table-as-select-parallel-data-warehouse.md) instrucción SQL. Los ejemplos se incluyen con el tema de crear la tabla remota.  
  
<!-- MISSING LINKS 
## See Also  
[Common Metadata Query Examples &#40;SQL Server PDW&#41;](../sqlpdw/common-metadata-query-examples-sql-server-pdw.md)  
-->
  
