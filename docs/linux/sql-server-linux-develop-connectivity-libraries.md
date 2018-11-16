---
title: Las bibliotecas de conectividad y marcos | Microsoft Docs
description: Enumera los controladores de conectividad que las aplicaciones cliente pueden utilizar desde diversos lenguajes para conectarse a Microsoft SQL Server que se ejecutan en local o en la nube, en Docker, Windows o Linux y también a Azure SQL Database y Azure SQL Data Warehouse.
author: rothja
ms.author: jroth
manager: craigg
ms.date: 03/17/2017
ms.topic: conceptual
ms.prod: sql
ms.custom: sql-linux
ms.technology: linux
ms.assetid: 80efe5ff-09ba-48a0-ac93-a91d62cff47c
ms.openlocfilehash: cbbd10ce9bc41ef7149f319077030e982ae6fcc0
ms.sourcegitcommit: 9c6a37175296144464ffea815f371c024fce7032
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/15/2018
ms.locfileid: "51664604"
---
# <a name="connectivity-libraries-and-frameworks-for-microsoft-sql-server"></a>Las bibliotecas de conectividad y marcos de trabajo para Microsoft SQL Server

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

Consulte la [tutoriales de introducción](https://aka.ms/sqldev) rápidamente empezar a trabajar con lenguajes de programación como C#, Java, Node.js, PHP y Python y compilar una aplicación mediante SQL Server en Linux o Windows o Docker en macOS.

En la tabla siguiente se enumera las bibliotecas de conectividad o *controladores* que las aplicaciones cliente pueden utilizar desde una variedad de lenguajes para conectarse a y usar Microsoft SQL Server que se ejecutan en local o en la nube, en Docker, Windows o Linux y también a Azure SQL Database y Azure SQL Data Warehouse. 

| Idioma | Plataforma | Recursos adicionales | Descargar | Introducción |
| :-- | :-- | :-- | :-- | :-- |
| C# | Windows, Linux, macOS | [Microsoft ADO.NET para SQL Server](https://msdn.microsoft.com/library/mt657768.aspx) | [Descargar](https://msdn.microsoft.com/vstudio/aa496123.aspx) | [Introducción](https://www.microsoft.com/sql-server/developer-get-started/csharp/ubuntu)
| Java | Windows, Linux, macOS | [Microsoft JDBC Driver para SQL Server](https://msdn.microsoft.com/library/mt484311.aspx) | [Descargar](https://go.microsoft.com/fwlink/?LinkId=245496) |  [Introducción](https://www.microsoft.com/sql-server/developer-get-started/java/ubuntu)
| PHP | Windows, Linux, macOS| [Controlador SQL para PHP para SQL Server](../connect/php/microsoft-php-driver-for-sql-server.md) | Sistema operativo: <br/> \* [Windows](https://www.microsoft.com/download/details.aspx?id=20098) <br/> \* [Linux](https://github.com/Microsoft/msphpsql/tree/dev#install-unix) <br/> \* [macOS](https://github.com/Microsoft/msphpsql/tree/dev#install-unix) |  [Introducción](https://www.microsoft.com/sql-server/developer-get-started/php/ubuntu)
| Node.js | Windows, Linux, macOS | [Controlador Node.js de SQL Server](../connect/node-js/node-js-driver-for-sql-server.md) |  [Introducción](https://www.microsoft.com/sql-server/developer-get-started/node/ubuntu)
| Python | Windows, Linux, macOS | [Controlador Python para SQL](../connect/python/python-driver-for-sql-server.md) <br/> \* [pyodbc](https://msdn.microsoft.com/library/mt763257.aspx) |  [Introducción](https://www.microsoft.com/sql-server/developer-get-started/python/ubuntu)
| Ruby | Windows, Linux, macOS | [Controlador Ruby para SQL Server](../connect/ruby/ruby-driver-for-sql-server.md) | [Introducción](https://www.microsoft.com/sql-server/developer-get-started/ruby/ubuntu)
| C++ | Windows, Linux, macOS | [Controlador ODBC de Microsoft para SQL Server](https://msdn.microsoft.com/library/mt654048(v=sql.1).aspx) | [Descargar](https://msdn.microsoft.com/library/mt654048(v=sql.1).aspx) |  

En la tabla siguiente se enumera algunos ejemplos de marcos de asignación relacional de objetos (ORM) y los marcos web que las aplicaciones cliente pueden utilizar con Microsoft SQL Server que se ejecutan en local o en la nube, en Docker, Windows o Linux y también a Azure SQL Database y Azure SQL Data Warehouse. 

| Idioma | Plataforma | ORM(s) |
| :-- | :-- | :-- |
| C# | Windows, Linux, macOS | [Entity Framework](https://docs.microsoft.com/ef)<br>[Entity Framework Core](https://docs.microsoft.com/ef/core/index) |
| Java | Windows, Linux, macOS |[Hibernar ORM](https://hibernate.org/orm)|
| PHP | Windows, Linux | [Laravel (elocuente)](https://laravel.com/docs/5.0/eloquent) |
| Node.js | Windows, Linux, macOS | [Sequelize ORM](https://docs.sequelizejs.com) |
| Python | Windows, Linux, macOS |[Django](https://www.djangoproject.com/) |
| Ruby | Windows, Linux, macOS | [Ruby on Rails](https://rubyonrails.org/) |

## <a name="related-links"></a>Vínculos relacionados
- [Controladores de SQL Server](https://msdn.microsoft.com/library/mt654049.aspx) para conectarse desde aplicaciones cliente
