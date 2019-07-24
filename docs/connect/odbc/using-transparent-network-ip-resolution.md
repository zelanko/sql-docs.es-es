---
title: Usar la resolución de IP de red transparente | Microsoft Docs
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
ms.openlocfilehash: df5b0233168c52b4f79cdc6d2d03cd7b72e16046
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "68008478"
---
# <a name="using-transparent-network-ip-resolution"></a>Uso de resolución de IP de red transparente
[!INCLUDE[Driver_ODBC_Download](../../includes/driver_odbc_download.md)]

TransparentNetworkIPResolution es una revisión de la característica MultiSubnetFailover existente, disponible en Microsoft ODBC driver 13,1 for SQL Server, que afecta a la secuencia de conexión del controlador en caso de que la primera dirección IP resuelta del nombre de host no responda y hay varias direcciones IP asociadas con el nombre de host. Interactúa con MultiSubnetFailover para proporcionar las tres secuencias de conexión siguientes:

* 0: se intenta una IP, seguida de todas las direcciones IP en paralelo.
* 1: se intentan todas las direcciones IP en paralelo
* 2: todas las direcciones IP se intentan una tras otra

|TransparentNetworkIPResolution|MultiSubnetFailover|Químicos|
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

La `TransparentNetworkIPResolution` palabra clave de conexión y DSN controla esta configuración en el nivel de cadena de conexión. El valor predeterminado es habilitado.

Palabra clave|Valores|Valor predeterminado
-|-|-
`TransparentNetworkIPResolution`|`Yes`, `No`|`Yes`

El `SQL_COPT_SS_TNIR` atributo anterior a la conexión permite a una aplicación controlar esta configuración mediante programación:

Atributo de conexión|   Tamaño/Tipo|  Valor predeterminado| Valor| Descripción
-|-|-|-|-
`SQL_COPT_SS_TNIR` (1249)| `SQL_IS_INTEGER` o `SQL_IS_UINTEGER`| `SQL_IS_ON`(1), `SQL_IS_OFF`(0)|`SQL_IS_ON`|Habilita o deshabilita TNIR.

<a name="for-more-information-about-multisubnetfailover-see-odbc-driver-on-linux-and-macos---high-availability-and-disaster-recoveryconnectodbclinux-macodbc-driver-on-linux-support-for-high-availability-disaster-recoverymd"></a>Para más información sobre MultiSubnetFailover, vea [Controlador ODBC en Linux y macOS: alta disponibilidad y recuperación ante desastres](../../connect/odbc/linux-mac/odbc-driver-on-linux-support-for-high-availability-disaster-recovery.md).
--------------------------------------------------
## <a name="see-also"></a>Consulte también  
* [Microsoft ODBC Driver for SQL Server en Windows](../../connect/odbc/windows/microsoft-odbc-driver-for-sql-server-on-windows.md)
* [Agrupación en clústeres de varias subredes de SQL Server (SQL Server)](https://msdn.microsoft.com/library/ff878716.aspx#RelatedContent)
