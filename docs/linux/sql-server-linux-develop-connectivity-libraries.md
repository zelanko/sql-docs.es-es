---
title: Bibliotecas de conectividad y marcos
description: En este artículo se enumeran los controladores de conectividad que las aplicaciones cliente pueden usar desde distintos lenguajes para conectarse a la instancia de Microsoft SQL Server que se ejecuta de forma local o en la nube, en Linux, en Windows o en Docker, y también en Azure SQL Database y Azure SQL Data Warehouse.
author: VanMSFT
ms.author: vanto
ms.date: 03/17/2017
ms.topic: conceptual
ms.prod: sql
ms.technology: linux
ms.assetid: 80efe5ff-09ba-48a0-ac93-a91d62cff47c
ms.openlocfilehash: a4ed76cde2cd8ff8b9d862b981dcbed2361c6ae8
ms.sourcegitcommit: 4fb6bc7c81a692a2df706df063d36afad42816af
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 10/29/2019
ms.locfileid: "73049737"
---
# <a name="connectivity-libraries-and-frameworks-for-microsoft-sql-server"></a>Bibliotecas de conectividad y marcos para Microsoft SQL Server

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

Consulte los [tutoriales de introducción](https://aka.ms/sqldev) para empezar a trabajar rápidamente con lenguajes de programación como C#, Java, Node.js, PHP y Python y compilar una aplicación con SQL Server en Linux o Windows, o bien en Docker en macOS.

En la tabla siguiente se enumeran las bibliotecas o *controladores* de conectividad que las aplicaciones cliente pueden usar desde distintos lenguajes para la conexión y el uso de la instancia de Microsoft SQL Server que se ejecuta de forma local o en la nube, en Linux, en Windows o en Docker, y también en Azure SQL Database y Azure SQL Data Warehouse. 

| Idioma | Plataforma | Recursos adicionales | Descargar | Introducción |
| :-- | :-- | :-- | :-- | :-- |
| C# | Windows, Linux, macOS | [Microsoft ADO.NET para SQL Server](/sql/connect/ado-net/microsoft-ado-net-sql-server) | [Descargar](https://msdn.microsoft.com/vstudio/aa496123.aspx) | [Primeros pasos](https://www.microsoft.com/sql-server/developer-get-started/csharp/ubuntu)
| Java | Windows, Linux, macOS | [Microsoft JDBC Driver para SQL Server](https://msdn.microsoft.com/library/mt484311.aspx) | [Descargar](https://go.microsoft.com/fwlink/?LinkId=245496) |  [Primeros pasos](https://www.microsoft.com/sql-server/developer-get-started/java/ubuntu)
| PHP | Windows, Linux, macOS| [Controlador de SQL para PHP para SQL Server](../connect/php/microsoft-php-driver-for-sql-server.md) | Sistema operativo: <br/> \* [Windows](https://www.microsoft.com/download/details.aspx?id=20098) <br/> \* [Linux](https://github.com/Microsoft/msphpsql/tree/dev#install-unix) <br/> \* [macOS](https://github.com/Microsoft/msphpsql/tree/dev#install-unix) |  [Primeros pasos](https://www.microsoft.com/sql-server/developer-get-started/php/ubuntu)
| Node.js | Windows, Linux, macOS | [Controlador Node.js de SQL Server](../connect/node-js/node-js-driver-for-sql-server.md) |  [Primeros pasos](https://www.microsoft.com/sql-server/developer-get-started/node/ubuntu)
| Python | Windows, Linux, macOS | [Controlador de SQL para Python](../connect/python/python-driver-for-sql-server.md) <br/> \* [pyodbc](https://msdn.microsoft.com/library/mt763257.aspx) |  [Primeros pasos](https://www.microsoft.com/sql-server/developer-get-started/python/ubuntu)
| Ruby | Windows, Linux, macOS | [Controlador Ruby para SQL Server](../connect/ruby/ruby-driver-for-sql-server.md) | [Primeros pasos](https://www.microsoft.com/sql-server/developer-get-started/ruby/ubuntu)
| C++ | Windows, Linux, macOS | [Controlador ODBC de Microsoft para SQL Server](https://msdn.microsoft.com/library/mt654048(v=sql.1).aspx) | [Descargar](https://msdn.microsoft.com/library/mt654048(v=sql.1).aspx) |  

En la tabla siguiente se enumeran algunos ejemplos de marcos de Asignación relacional de objetos (ORM) y marcos web que las aplicaciones cliente pueden usar con la instancia de Microsoft SQL Server que se ejecuta de forma local o en la nube, en Linux, en Windows o en Docker, y también en Azure SQL Database y Azure SQL Data Warehouse. 

| Idioma | Plataforma | ORM |
| :-- | :-- | :-- |
| C# | Windows, Linux, macOS | [Entity Framework](https://docs.microsoft.com/ef)<br>[Entity Framework Core](https://docs.microsoft.com/ef/core/index) |
| Java | Windows, Linux, macOS |[Hibernate ORM](https://hibernate.org/orm)|
| PHP | Windows, Linux | [Laravel (Eloquent)](https://laravel.com/docs/5.0/eloquent) |
| Node.js | Windows, Linux, macOS | [Sequelize ORM](https://docs.sequelizejs.com) |
| Python | Windows, Linux, macOS |[Django](https://www.djangoproject.com/) |
| Ruby | Windows, Linux, macOS | [Ruby on Rails](https://rubyonrails.org/) |

## <a name="related-links"></a>Vínculos relacionados
- [Controladores de SQL Server](https://msdn.microsoft.com/library/mt654049.aspx) para conectarse desde aplicaciones cliente
