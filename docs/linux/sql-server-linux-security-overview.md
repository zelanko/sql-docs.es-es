---
title: Limitaciones de seguridad de SQL Server en Linux | Documentos de Microsoft
description: Este tema describe SQL Server en las restricciones de Linux.
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.date: 10/02/2017
ms.topic: article
ms.prod: sql-linux
ms.technology: database-engine
ms.assetid: 64da74cc-14bf-4636-a55e-8cc1fce2aaff
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 834bba08c90262fd72881ab2890abaaf7b8f7678
ms.openlocfilehash: 45f88572804d236c209ab86884fc0fcbc432bc62
ms.contentlocale: es-es
ms.lasthandoff: 10/02/2017

---
# <a name="security-limitations-for-sql-server-on-linux"></a>Limitaciones de seguridad de SQL Server en Linux

[!INCLUDE[tsql-appliesto-sslinux-only](../includes/tsql-appliesto-sslinux-only.md)]

SQL Server en Linux actualmente tiene las siguientes limitaciones:

* Se proporciona una directiva de contraseña estándar. MUST_CHANGE es la única opción que puede configurar.  
* No se admite la administración extensible de claves. 
* No se admite el uso de las claves almacenadas en el almacén de claves de Azure.
* SQL Server genera su propio certificado autofirmado para cifrado de las conexiones. En la actualidad, SQL Server no puede configurarse para usar un usuario proporcionado el certificado para SSL o TLS. 

Para obtener más información acerca de las características de seguridad disponibles en SQL Server, consulte el [centro de seguridad para el motor de base de datos de SQL Server y base de datos de SQL Azure](../relational-databases/security/security-center-for-sql-server-database-engine-and-azure-sql-database.md).

## <a name="next-steps"></a>Pasos siguientes

Para las tareas comunes de seguridad, consulte [empezar a trabajar con características de seguridad de SQL Server en Linux](sql-server-linux-security-get-started.md).   
Para que una secuencia de comandos cambiar el TCP número de puerto, los directorios de SQL Server y configurar el seguimiento o la intercalación, consulte [configurar SQL Server en Linux con mssql-conf](sql-server-linux-configure-mssql-conf.md).

