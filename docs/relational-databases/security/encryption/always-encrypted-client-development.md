---
title: Always Encrypted (desarrollo de clientes) | Microsoft Docs
ms.custom: 
ms.date: 07/29/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: security
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
dev_langs:
- CSharp
ms.assetid: 9595eb66-284c-4474-828f-8961a05ce989
caps.latest.revision: 
author: stevestein
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: b342d2733ad9dfab013957c08edfee93a3c78859
ms.sourcegitcommit: 37f0b59e648251be673389fa486b0a984ce22c81
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 02/12/2018
---
# <a name="always-encrypted-client-development"></a>Always Encrypted (desarrollo de clientes)
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]

[Always Encrypted](../../../relational-databases/security/encryption/always-encrypted-database-engine.md) es una tecnología de cifrado de cliente que garantiza que nunca se va a revelar información confidencial (ni ninguna de las claves de cifrado relacionadas) a SQL Server o a Base de datos SQL de Azure. Con Always Encrypted, un controlador cliente cifra la información confidencial de forma transparente antes de pasar los datos al motor de base de datos y, de igual modo, descifra de forma transparente los datos recuperados de las columnas de la base de datos cifrada.

Para obtener más información sobre cómo desarrollar aplicaciones que usan bases de datos protegidas con Always Encrypted, así como qué controladores cliente y qué versiones de controlador admiten Always Encrypted, vea:

- [Uso de Always Encrypted con el proveedor de datos .NET Framework para SQL Server](../../../relational-databases/security/encryption/develop-using-always-encrypted-with-net-framework-data-provider.md)
- [Usar Always Encrypted con el controlador JDBC](../../../connect/jdbc/using-always-encrypted-with-the-jdbc-driver.md)
- [Uso de Always Encrypted con el controlador ODBC de Windows](../../../connect/odbc/using-always-encrypted-with-the-odbc-driver.md)



## <a name="see-also"></a>Ver también

[Always Encrypted (motor de base de datos)](../../../relational-databases/security/encryption/always-encrypted-database-engine.md)

