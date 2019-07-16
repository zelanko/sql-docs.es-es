---
title: Limitaciones de seguridad para SQL Server en Linux
description: Este artículo describe SQL Server en Linux restricciones.
author: VanMSFT
ms.author: vanto
ms.date: 01/30/2018
ms.topic: conceptual
ms.prod: sql
ms.technology: linux
ms.assetid: 64da74cc-14bf-4636-a55e-8cc1fce2aaff
ms.openlocfilehash: 9f54197c8613293b36c1eb1ec362a8ed4db835e4
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "68065125"
---
# <a name="security-limitations-for-sql-server-on-linux"></a>Limitaciones de seguridad para SQL Server en Linux

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

SQL Server en Linux actualmente tiene las siguientes limitaciones:

* Se proporciona una directiva de contraseña estándar. MUST_CHANGE es la única opción que puede configurar.  
* No se admite la administración extensible de claves. 
* No es compatible con claves almacenadas en Azure Key Vault.
* SQL Server genera su propio certificado autofirmado para cifrado de conexiones. SQL Server puede configurarse para usar un usuario proporcionado el certificado para TLS. 

Para obtener más información sobre las características de seguridad disponibles en SQL Server, consulte el [Security Center para el motor de base de datos de SQL Server y Azure SQL Database](../relational-databases/security/security-center-for-sql-server-database-engine-and-azure-sql-database.md).

## <a name="next-steps"></a>Pasos siguientes

Para tareas comunes de seguridad, consulte [empezar a trabajar con características de seguridad de SQL Server en Linux](sql-server-linux-security-get-started.md). Para obtener un script cambiar el TCP número de puerto, los directorios de SQL Server y configurar marcas de seguimiento o la intercalación, consulte [configurar SQL Server en Linux con mssql-conf](sql-server-linux-configure-mssql-conf.md).
