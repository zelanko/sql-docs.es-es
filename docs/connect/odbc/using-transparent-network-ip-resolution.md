---
title: Utilizando la resolución de IP de red transparente | Documentos de Microsoft
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: odbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: d255208f-d486-4ad3-8080-61c6e0261825
caps.latest.revision: 2
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 6e4414da0babbeca3bc8a6f271923613f823248e
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="using-transparent-network-ip-resolution"></a>Utilizando la resolución de IP de red transparente
[!INCLUDE[Driver_ODBC_Download](../../includes/driver_odbc_download.md)]

TransparentNetworkIPResolution es una revisión de la característica de MultiSubnetFailover existente, disponible en Microsoft ODBC Driver 13.1 for SQL Server, que afecta a la secuencia de conexión del controlador en el caso de que no lleva a la primera dirección IP resuelta del nombre de host responder y hay varias direcciones IP asociadas con el nombre de host. Interactúa con MultiSubnetFailover para proporcionar las secuencias de tres de conexión siguientes:

* 0: uno se intenta IP, seguida de todas las direcciones IP en paralelo
* 1: todas las direcciones IP se intentan en paralelo
* 2: todas las direcciones IP se intentan una tras otra

|TransparentNetworkIPResolution|MultiSubnetFailover|Comportamiento|
|:-:|:-:|:-:|
|(predeterminado).|(predeterminado).|0|
|(predeterminado).|Habilitado|1|
|(predeterminado).|Deshabilitado|0|
|Habilitado|(predeterminado).|0|
|Habilitado|Habilitado|1|
|Habilitado|Deshabilitado|0|
|Deshabilitado|(predeterminado).|2|
|Deshabilitado|Habilitado|1|
|Deshabilitado|Deshabilitado|2|

El `TransparentNetworkIPResolution` cadena de conexión y DSN palabra clave controla esta configuración en el nivel de la cadena de conexión. El valor predeterminado está habilitado.

Palabra clave|Valores|Predeterminado
-|-|-
`TransparentNetworkIPResolution`|`Yes`, `No`|`Yes`

El `SQL_COPT_SS_TNIR` anterior a la conexión atributo permite que una aplicación controlar esta configuración mediante programación:

Atributo de conexión|   Tipo de tamaño /|  Predeterminado| Value| Description
-|-|-|-|-
`SQL_COPT_SS_TNIR` (1249)| `SQL_IS_INTEGER`o`SQL_IS_UINTEGER`| `SQL_IS_ON`(1), `SQL_IS_OFF`(0)|`SQL_IS_ON`|Habilita o deshabilita TNIR.

<a name="for-more-information-about-multisubnetfailover-see-odbc-driver-on-linux-and-macos---high-availability-and-disaster-recoveryconnectodbclinux-macodbc-driver-on-linux-support-for-high-availability-disaster-recoverymd"></a>Para obtener más información sobre MultiSubnetFailover, consulte [controlador ODBC en Linux y macOS - alta disponibilidad y recuperación ante desastres](../../connect/odbc/linux-mac/odbc-driver-on-linux-support-for-high-availability-disaster-recovery.md)
--------------------------------------------------
## <a name="see-also"></a>Vea también  
* [Microsoft ODBC Driver for SQL Server en Windows](../../connect/odbc/windows/microsoft-odbc-driver-for-sql-server-on-windows.md)
* [SQL Server varias subredes de agrupación en clústeres (SQL Server)](https://msdn.microsoft.com/library/ff878716.aspx#RelatedContent)
