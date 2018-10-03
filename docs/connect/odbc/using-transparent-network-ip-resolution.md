---
title: Uso de resolución de direcciones IP de red transparente | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: d255208f-d486-4ad3-8080-61c6e0261825
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 767e3e17b67a36bca93bd8a85704d50338fdfd58
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MTE75
ms.contentlocale: es-ES
ms.lasthandoff: 10/01/2018
ms.locfileid: "47610763"
---
# <a name="using-transparent-network-ip-resolution"></a>Uso de resolución de IP de red transparente
[!INCLUDE[Driver_ODBC_Download](../../includes/driver_odbc_download.md)]

TransparentNetworkIPResolution es una revisión de la característica de MultiSubnetFailover existente, disponible en Microsoft ODBC Driver 13.1 para SQL Server, que afecta a la secuencia de conexión del controlador en el caso donde la primera dirección IP resuelta del nombre de host no lo hace responder y hay varias direcciones IP asociada con el nombre de host. Interactúa con MultiSubnetFailover para proporcionar las siguientes secuencias de tres conexiones:

* 0: uno está intentada IP, seguida de todas las direcciones IP en paralelo
* 1: se ha intentado todas las direcciones IP en paralelo
* 2: todas las direcciones IP se ha intentado una tras otra

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

El `TransparentNetworkIPResolution` cadena de conexión y DSN de palabra clave controla esta configuración en el nivel de la cadena de conexión. El valor predeterminado está habilitado.

Palabra clave|Valores|Valor predeterminado
-|-|-
`TransparentNetworkIPResolution`|`Yes`, `No`|`Yes`

El `SQL_COPT_SS_TNIR` atributo de conexión previa permite que una aplicación controlar esta configuración mediante programación:

Atributo de conexión|   Tipo y tamaño|  Valor predeterminado| Valor| Descripción
-|-|-|-|-
`SQL_COPT_SS_TNIR` (1249)| `SQL_IS_INTEGER` o `SQL_IS_UINTEGER`| `SQL_IS_ON`(1), `SQL_IS_OFF`(0)|`SQL_IS_ON`|Habilita o deshabilita TNIR.

<a name="for-more-information-about-multisubnetfailover-see-odbc-driver-on-linux-and-macos---high-availability-and-disaster-recoveryconnectodbclinux-macodbc-driver-on-linux-support-for-high-availability-disaster-recoverymd"></a>Para obtener más información acerca de MultiSubnetFailover, consulte [controlador ODBC en Linux y macOS: alta disponibilidad y recuperación ante desastres](../../connect/odbc/linux-mac/odbc-driver-on-linux-support-for-high-availability-disaster-recovery.md)
--------------------------------------------------
## <a name="see-also"></a>Ver también  
* [Microsoft ODBC Driver for SQL Server en Windows](../../connect/odbc/windows/microsoft-odbc-driver-for-sql-server-on-windows.md)
* [Agrupación en clústeres de varias subredes de SQL Server (SQL Server)](https://msdn.microsoft.com/library/ff878716.aspx#RelatedContent)
