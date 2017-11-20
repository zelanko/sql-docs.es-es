---
title: Marcos y bibliotecas de conectividad | Documentos de Microsoft
description: "Enumera los controladores de conectividad que las aplicaciones cliente pueden utilizar en varios idiomas para conectarse a Microsoft SQL Server que se ejecutan de forma local o en la nube, en Linux, Windows o Docker y también para base de datos de SQL Azure y almacenamiento de datos de SQL Azure."
author: sanagama
ms.author: sanagama
manager: jhubbard
ms.date: 03/17/2017
ms.topic: article
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: linux
ms.suite: sql
ms.custom: 
ms.technology: database-engine
ms.assetid: 80efe5ff-09ba-48a0-ac93-a91d62cff47c
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 96ec352784f060f444b8adcae6005dd454b3b460
ms.openlocfilehash: f692639531a133652787dfe818fe25847c0d910b
ms.contentlocale: es-es
ms.lasthandoff: 09/27/2017

---
# <a name="connectivity-libraries-and-frameworks-for-microsoft-sql-server"></a>Las bibliotecas de conectividad y marcos de trabajo para Microsoft SQL Server

[!INCLUDE[tsql-appliesto-sslinux-only](../includes/tsql-appliesto-sslinux-only.md)]

Visite nuestro [tutoriales de introducción](http://aka.ms/sqldev) para empezar a trabajar con lenguajes como C#, Java, Node.js, PHP y Python de programación y compilar una aplicación mediante SQL Server en Linux o Windows o Docker en macOS rápidamente.

La tabla siguiente enumera las bibliotecas de conectividad o *controladores* que las aplicaciones cliente pueden utilizar desde una variedad de lenguajes para conectarse a y usar Microsoft SQL Server que se ejecutan de forma local o en la nube, en Linux, Windows o Docker y también para base de datos de SQL Azure y almacenamiento de datos de SQL Azure. 

| Lenguaje | Plataforma | Recursos adicionales | Descargar | Introducción |
| :-- | :-- | :-- | :-- | :-- |
| C# | Windows, Linux, macOS | [Microsoft ADO.NET para SQL Server](http://msdn.microsoft.com/library/mt657768.aspx) | [Descargar](https://msdn.microsoft.com/vstudio/aa496123.aspx) | [Introducción](https://www.microsoft.com/en-us/sql-server/developer-get-started/csharp/ubuntu)
| Java | Windows, Linux, macOS | [Controlador JDBC de Microsoft para SQL Server](http://msdn.microsoft.com/library/mt484311.aspx) | [Descargar](http://go.microsoft.com/fwlink/?LinkId=245496) |  [Introducción](https://www.microsoft.com/en-us/sql-server/developer-get-started/java/ubuntu)
| PHP | Windows, Linux, macOS| [Controlador de SQL para PHP para SQL Server](http://msdn.microsoft.com/library/dn865013.aspx) | Sistema operativo: <br/> \*[Windows](https://www.microsoft.com/download/details.aspx?id=20098) <br/> \*[Linux](https://github.com/Microsoft/msphpsql/tree/dev#install-unix) <br/> \*[macOS](https://github.com/Microsoft/msphpsql/tree/dev#install-unix) |  [Introducción](https://www.microsoft.com/en-us/sql-server/developer-get-started/php/ubuntu)
| Node.js | Windows, Linux, macOS | [Controlador Node.js de SQL Server](../connect/node-js/node-js-driver-for-sql-server.md) |  [Introducción](https://www.microsoft.com/en-us/sql-server/developer-get-started/node/ubuntu)
| Python | Windows, Linux, macOS | [Controlador de Python para SQL Server](../connect/python/python-driver-for-sql-server.md) <br/> \*[pyodbc](http://msdn.microsoft.com/library/mt763257.aspx) |  [Introducción](https://www.microsoft.com/en-us/sql-server/developer-get-started/python/ubuntu)
| Ruby | Windows, Linux, macOS | [Controlador Ruby para SQL Server](../connect/ruby/ruby-driver-for-sql-server.md) | [Introducción](https://www.microsoft.com/en-us/sql-server/developer-get-started/ruby/ubuntu)
| C++ | Windows, Linux, macOS | [Controlador ODBC de Microsoft para SQL Server](https://msdn.microsoft.com/en-us/library/mt654048(v=sql.1).aspx) | [Descargar](https://msdn.microsoft.com/en-us/library/mt654048(v=sql.1).aspx) |  

En la tabla siguiente se enumera algunos ejemplos de marcos de trabajo de asignación relacional de objetos (ORM) y marcos de trabajo web que las aplicaciones cliente pueden utilizar con Microsoft SQL Server que se ejecutan de forma local o en la nube, en Linux, Windows o Docker y también para base de datos de SQL Azure y almacenamiento de datos de SQL Azure. 

| Lenguaje | Plataforma | ORM(s) |
| :-- | :-- | :-- |
| C# | Windows, Linux, macOS | [Entity Framework](https://docs.microsoft.com/en-us/ef)<br>[Entity Framework Core](https://docs.microsoft.com/en-us/ef/core/index) |
| Java | Windows, Linux, macOS |[Hibernación ORM](http://hibernate.org/orm)|
| PHP | Windows, Linux | [Laravel (elocuente)](https://laravel.com/docs/5.0/eloquent) |
| Node.js | Windows, Linux, macOS | [Sequelize ORM](http://docs.sequelizejs.com) |
| Python | Windows, Linux, macOS |[Django](https://www.djangoproject.com/) |
| Ruby | Windows, Linux, macOS | [Ruby sobre raíles](http://rubyonrails.org/) |

## <a name="related-links"></a>Vínculos relacionados
- [Controladores de SQL Server](http://msdn.microsoft.com/library/mt654049.aspx) para conectarse desde aplicaciones cliente

