---
title: Always Encrypted (desarrollo de clientes) | Microsoft Docs
ms.custom:
- SQL2016_New_Updated
ms.date: 07/29/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
dev_langs:
- CSharp
ms.assetid: 9595eb66-284c-4474-828f-8961a05ce989
caps.latest.revision: 33
author: stevestein
manager: jhubbard
translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 091625c7e502ac131bd045546ca4c587b754e366
ms.lasthandoff: 04/11/2017

---
# <a name="always-encrypted-client-development"></a>Always Encrypted (desarrollo de clientes)
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx_md](../../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

[Always Encrypted](../../../relational-databases/security/encryption/always-encrypted-database-engine.md) es una tecnología de cifrado de cliente que garantiza que nunca se va a revelar información confidencial (ni ninguna de las claves de cifrado relacionadas) a SQL Server o a Base de datos SQL de Azure. Con Always Encrypted, un controlador cliente cifra la información confidencial de forma transparente antes de pasar los datos al motor de base de datos y, de igual modo, descifra de forma transparente los datos recuperados de las columnas de la base de datos cifrada.

Para obtener más información sobre cómo desarrollar aplicaciones que usan bases de datos protegidas con Always Encrypted, así como qué controladores cliente y qué versiones de controlador admiten Always Encrypted, vea:

- [Uso de Always Encrypted con el proveedor de datos .NET Framework para SQL Server](../../../relational-databases/security/encryption/develop-using-always-encrypted-with-net-framework-data-provider.md)
- [Usar Always Encrypted con el controlador JDBC](https://msdn.microsoft.com/library/mt591987.aspx)
- [Uso de Always Encrypted con el controlador ODBC de Windows](https://msdn.microsoft.com/library/mt637351.aspx)



## <a name="see-also"></a>Vea también

[Always Encrypted (motor de base de datos)](../../../relational-databases/security/encryption/always-encrypted-database-engine.md)


