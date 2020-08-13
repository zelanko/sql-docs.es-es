---
title: Uso de resolución de IP de red transparente
description: Obtenga información sobre la resolución de IP de red transparente en el controlador ODBC para SQL Server y cómo ello afecta a la característica MultiSubnetFailover.
ms.custom: ''
ms.date: 05/06/2020
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: d255208f-d486-4ad3-8080-61c6e0261825
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 12a8a151902bd4f191fbc79f165f936e991a0226
ms.sourcegitcommit: 216f377451e53874718ae1645a2611cdb198808a
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/28/2020
ms.locfileid: "87245004"
---
# <a name="using-transparent-network-ip-resolution-with-the-odbc-driver"></a>Uso de la resolución de IP de red transparente con el controlador ODBC
[!INCLUDE[Driver_ODBC_Download](../../includes/driver_odbc_download.md)]

TransparentNetworkIPResolution es una revisión de la característica existente MultiSubnetFailover, disponible en Microsoft ODBC Driver 13.1 for SQL Server, que afecta a la secuencia de conexión del controlador en el caso donde la primera IP resuelta del nombre de host no responde y hay varias direcciones IP asociadas al nombre de host. Interactúa con MultiSubnetFailover para proporcionar las tres secuencias de conexión siguientes:

* 0: se intenta una IP, seguida de todas las direcciones IP en paralelo.
* 1: todas las direcciones IP se intentan en paralelo.
* 2: todas las direcciones IP se intentan una tras otra.

|TransparentNetworkIPResolution|MultiSubnetFailover|Comportamiento|
|:-:|:-:|:-:|
|(predeterminado).|(predeterminado).|0|
|(predeterminado).|habilitado|1|
|(predeterminado).|Disabled|0|
|habilitado|(predeterminado).|0|
|habilitado|habilitado|1|
|habilitado|Disabled|0|
|Disabled|(predeterminado).|2|
|Disabled|habilitado|1|
|Disabled|Disabled|2|

La palabra clave de DNS y cadena de conexión `TransparentNetworkIPResolution` controla esta configuración en el nivel de cadena de conexión. El valor predeterminado es habilitado.

Palabra clave|Valores|Valor predeterminado
-|-|-
`TransparentNetworkIPResolution`|`Yes`, `No`|`Yes`

El atributo previo a la conexión `SQL_COPT_SS_TNIR` permite que una aplicación controle esta configuración mediante programación:

Atributo de conexión|   Tamaño/Tipo|  Valor predeterminado| Value| Descripción
-|-|-|-|-
`SQL_COPT_SS_TNIR` (1249)| `SQL_IS_INTEGER` o `SQL_IS_UINTEGER`| `SQL_IS_ON`(1), `SQL_IS_OFF`(0)|`SQL_IS_ON`|Habilita o deshabilita TNIR.

<a name="for-more-information-about-multisubnetfailover-see-odbc-driver-on-linux-and-macos---high-availability-and-disaster-recovery"></a>Para más información sobre MultiSubnetFailover, vea [Controlador ODBC en Linux y macOS: alta disponibilidad y recuperación ante desastres](linux-mac/odbc-driver-on-linux-support-for-high-availability-disaster-recovery.md).
--------------------------------------------------
## <a name="see-also"></a>Consulte también  
* [Microsoft ODBC Driver for SQL Server en Windows](windows/microsoft-odbc-driver-for-sql-server-on-windows.md)
* [Agrupación en clústeres de varias subredes de SQL Server (SQL Server)](../../sql-server/failover-clusters/windows/sql-server-multi-subnet-clustering-sql-server.md)
