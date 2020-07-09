---
title: Limitaciones de seguridad para SQL Server en Linux
description: En este artículo se describen las restricciones de SQL Server en Linux.
author: VanMSFT
ms.author: vanto
ms.date: 09/12/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: linux
ms.assetid: 64da74cc-14bf-4636-a55e-8cc1fce2aaff
ms.openlocfilehash: f1820b54532a820a47babdaf79e28d1baa0f096b
ms.sourcegitcommit: f7ac1976d4bfa224332edd9ef2f4377a4d55a2c9
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/02/2020
ms.locfileid: "85895299"
---
# <a name="security-limitations-for-sql-server-on-linux"></a>Limitaciones de seguridad para SQL Server en Linux

[!INCLUDE [SQL Server - Linux](../includes/applies-to-version/sql-linux.md)]

Actualmente, SQL Server en Linux tiene las siguientes limitaciones:

* Se proporciona una directiva de contraseñas estándar. MUST_CHANGE es la única opción que se puede configurar. No se admite la opción CHECK_POLICY.
* No se admite la Administración extensible de claves. 
* No se admite el uso de claves almacenadas en Azure Key Vault.
* SQL Server genera su propio certificado autofirmado para cifrar las conexiones. SQL Server puede configurarse para usar un certificado proporcionado por el usuario para TLS. 

Para obtener más información sobre las características de seguridad disponibles en SQL Server, consulte [Centro de seguridad para el motor de base de datos SQL Server y Azure SQL Database](../relational-databases/security/security-center-for-sql-server-database-engine-and-azure-sql-database.md).

## <a name="next-steps"></a>Pasos siguientes

Para conocer las tareas comunes de seguridad, consulte una [introducción a las características de seguridad de SQL Server en Linux](sql-server-linux-security-get-started.md). Si quiere obtener un script que le permita cambiar el número del puerto TCP y los directorios de SQL Server, así como configurar las marcas de seguimiento o la intercalación, consulte [Configurar SQL Server en Linux con la herramienta mssql-conf](sql-server-linux-configure-mssql-conf.md).
