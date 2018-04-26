---
title: Limitaciones de seguridad de SQL Server en Linux | Documentos de Microsoft
description: Este artículo describe SQL Server en las restricciones de Linux.
author: rothja
ms.author: jroth
manager: craigg
ms.date: 01/30/2018
ms.topic: article
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: ''
ms.suite: sql
ms.custom: sql-linux
ms.technology: database-engine
ms.assetid: 64da74cc-14bf-4636-a55e-8cc1fce2aaff
ms.workload: Inactive
ms.openlocfilehash: dbf964ea466522b5735c8ccac85821ca1e1426c4
ms.sourcegitcommit: a85a46312acf8b5a59a8a900310cf088369c4150
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/26/2018
---
# <a name="security-limitations-for-sql-server-on-linux"></a>Limitaciones de seguridad de SQL Server en Linux

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

SQL Server en Linux actualmente tiene las siguientes limitaciones:

* Se proporciona una directiva de contraseña estándar. MUST_CHANGE es la única opción que puede configurar.  
* No se admite la administración extensible de claves. 
* No se admite el uso de las claves almacenadas en el almacén de claves de Azure.
* SQL Server genera su propio certificado autofirmado para cifrado de las conexiones. SQL Server puede configurarse para usar un usuario proporcionado el certificado para TLS. 

Para obtener más información acerca de las características de seguridad disponibles en SQL Server, consulte el [centro de seguridad para el motor de base de datos de SQL Server y base de datos de SQL Azure](../relational-databases/security/security-center-for-sql-server-database-engine-and-azure-sql-database.md).

## <a name="next-steps"></a>Pasos siguientes

Para las tareas comunes de seguridad, consulte [empezar a trabajar con características de seguridad de SQL Server en Linux](sql-server-linux-security-get-started.md). Para que una secuencia de comandos cambiar el TCP número de puerto, los directorios de SQL Server y configurar el seguimiento o la intercalación, consulte [configurar SQL Server en Linux con mssql-conf](sql-server-linux-configure-mssql-conf.md).
