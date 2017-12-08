---
title: "Características modificadas (base de datos independiente) | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: databases
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords: contained database, modifications to DBs
ms.assetid: a2942509-39a2-4903-b504-ae80a300a9de
caps.latest.revision: "27"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 6b44e142fba4e81b90ab7de843bcd8d97ab4ea0c
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 11/17/2017
---
# <a name="modified-features-contained-database"></a>Características modificadas (base de datos contenida)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)] Las siguientes características se han modificado de forma que las bases de datos parcialmente independientes las admitan. Normalmente, las características se modifican de modo que no crucen el límite de la base de datos.  
  
 Para más información, consulte [Contained Databases](../../relational-databases/databases/contained-databases.md).  
  
## <a name="alter-database"></a>ALTER DATABASE  
  
### <a name="application-level"></a>Nivel de aplicación  
 Al utilizar la instrucción ALTER DATABASE desde dentro de una base de datos contenida, la sintaxis difiere de la que se usa para una base de datos dependiente. Esta diferencia incluye restricciones de los elementos de la instrucción que se extienden más allá de la base de datos y llegan a la instancia. Para obtener más información, vea [ALTER DATABASE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql.md).  
  
### <a name="instance-level"></a>Nivel de instancia  
 La sintaxis de ALTER DATABASE cuando se utiliza fuera de una base de datos contenida difiere de la que se usa para bases de datos dependientes. Estos cambios impiden cruzar el límite de la base de datos. Para obtener más información, vea [ALTER DATABASE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql.md).  
  
## <a name="create-database"></a>CREATE DATABASE  
 La sintaxis de CREATE DATABASE para una base de datos contenida difiere de que se usa para una base de datos dependiente. Vea [CREATE DATABASE &#40;SQL Server Transact-SQL&#41;](../../t-sql/statements/create-database-sql-server-transact-sql.md) para obtener más información sobre los nuevos requisitos de sintaxis y valores permitidos.  
  
## <a name="temporary-tables"></a>Tablas temporales  
 Las tablas temporales locales se permiten en una base de datos independiente, pero su comportamiento difiere del de las tablas temporales locales en bases de datos dependientes. En las bases de datos dependientes, los datos de las tablas temporales se intercalan en la intercalación de **tempdb**. En una base de datos independiente, los datos de las tablas temporales se intercalan en la intercalación de la base de datos independiente.  
  
 Todos los metadatos asociados a tablas temporales (por ejemplo, los nombres, índices, etc. de tablas y columnas) estarán en la intercalación del catálogo.  
  
 En las tablas temporales no se pueden utilizar restricciones con nombre.  
  
 Las tablas temporales no pueden hacer referencia a tipos definidos por el usuario, colecciones de esquemas XML ni funciones definidas por el usuario.  
  
## <a name="collation"></a>Intercalación  
 En el modelo de base de datos dependiente, hay tres tipos distintos de intercalación: intercalación de base de datos, intercalación de instancia e intercalación de tempdb. Las bases de datos contenidas solo usan dos intercalaciones, la intercalación de base de datos y la nueva intercalación de catálogo. Vea [Contained Database Collations](../../relational-databases/databases/contained-database-collations.md) para obtener más información sobre la intercalación de base de datos contenida.  
  
## <a name="user-options"></a>Opciones de usuario  
 Al habilitar bases de datos independientes, la opción [user options](../../database-engine/configure-windows/configure-the-user-options-server-configuration-option.md) se debe establecer en 0 para la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
## <a name="see-also"></a>Vea también  
 [Contained Database Collations](../../relational-databases/databases/contained-database-collations.md)   
 [Contained Databases](../../relational-databases/databases/contained-databases.md)  
  
  
