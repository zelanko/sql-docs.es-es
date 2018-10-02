---
title: Always Encrypted (desarrollo de clientes) | Microsoft Docs
ms.custom: ''
ms.date: 08/21/2018
ms.prod: sql
ms.reviewer: vanto
ms.technology: security
ms.topic: conceptual
dev_langs:
- CSharp
ms.assetid: 9595eb66-284c-4474-828f-8961a05ce989
author: VanMSFT
ms.author: vanto
manager: craigg
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 728df586867f137b05d7bbb54efa420f0f35ceba
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 10/01/2018
ms.locfileid: "47604117"
---
# <a name="always-encrypted-client-development"></a>Always Encrypted (desarrollo de clientes)
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]

[Always Encrypted](../../../relational-databases/security/encryption/always-encrypted-database-engine.md) es una tecnología de cifrado de cliente que garantiza que nunca se va a revelar información confidencial (ni ninguna de las claves de cifrado relacionadas) a SQL Server o a Base de datos SQL de Azure. Con Always Encrypted, un controlador cliente cifra la información confidencial de forma transparente antes de pasar los datos al motor de base de datos y, de igual modo, descifra de forma transparente los datos recuperados de las columnas de la base de datos cifrada.

Para obtener más información sobre cómo desarrollar aplicaciones que usan bases de datos protegidas con Always Encrypted, así como qué controladores cliente y qué versiones de controlador admiten Always Encrypted, vea:

- [Uso de Always Encrypted con el proveedor de datos .NET Framework para SQL Server](../../../relational-databases/security/encryption/develop-using-always-encrypted-with-net-framework-data-provider.md)
- [Usar Always Encrypted con el controlador JDBC](../../../connect/jdbc/using-always-encrypted-with-the-jdbc-driver.md)
- [Uso de Always Encrypted con el controlador ODBC](../../../connect/odbc/using-always-encrypted-with-the-odbc-driver.md)
- [Uso de Always Encrypted con los controladores PHP](../../../connect/php/using-always-encrypted-php-drivers.md)

> [!NOTE]
> En la actualidad, en [.NET CORE](https://docs.microsoft.com/dotnet/core/) no se admite Always Encrypted.

## <a name="see-also"></a>Ver también

[Always Encrypted (motor de base de datos)](../../../relational-databases/security/encryption/always-encrypted-database-engine.md)

