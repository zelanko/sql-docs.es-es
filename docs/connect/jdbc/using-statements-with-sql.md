---
title: Empleo de instrucciones con SQL
description: Obtenga información general sobre el uso de diferentes tipos de instrucciones SQL con el controlador JDBC de Microsoft para SQL Server.
ms.custom: ''
ms.date: 08/12/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: fe28f48a-e1bc-48ff-a5e7-c24cd6e5ecc7
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 49ab0f6367353847bdf3a9e0a7aff13975b4d711
ms.sourcegitcommit: 129f8574eba201eb6ade1f1620c6b80dfe63b331
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/30/2020
ms.locfileid: "87435283"
---
# <a name="using-statements-with-sql"></a>Empleo de instrucciones con SQL

[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

Cuando se trabaja con datos de una base de datos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] mediante [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] e instrucciones SQL insertadas, se pueden usar varias clases. La clase usada depende del tipo de instrucción SQL que desee ejecutar.  
  
Si la instrucción SQL no contiene parámetros IN, use la clase [SQLServerStatement](../../connect/jdbc/reference/sqlserverstatement-class.md), pero si contiene parámetros IN, use la clase [SQLServerPreparedStatement](../../connect/jdbc/reference/sqlserverpreparedstatement-class.md).  
  
> [!NOTE]  
> Si necesita usar instrucciones SQL que contengan parámetros IN y OUT, debe implementarlas como procedimientos almacenados y llamarlas mediante la clase [SQLServerCallableStatement](../../connect/jdbc/reference/sqlservercallablestatement-class.md). Para obtener más información acerca de cómo usar los procedimientos almacenados, consulte [Usar instrucciones con procedimientos almacenados](../../connect/jdbc/using-statements-with-stored-procedures.md).  
  
En las siguientes secciones se describen las diferentes situaciones de trabajo con datos de una base de datos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] mediante instrucciones SQL.  

## <a name="in-this-section"></a>En esta sección  

| Tema                                                                                                                        | Descripción                                                       |
| ---------------------------------------------------------------------------------------------------------------------------- | ----------------------------------------------------------------- |
| [Empleo de una instrucción SQL sin parámetros](../../connect/jdbc/using-an-sql-statement-with-no-parameters.md)                 | Describe cómo usar instrucciones SQL que no contienen parámetros.   |
| [Empleo de una instrucción SQL con parámetros](../../connect/jdbc/using-an-sql-statement-with-parameters.md)                       | Describe cómo usar instrucciones SQL que contienen parámetros.      |
| [Empleo de una instrucción SQL para modificar objetos de base de datos](../../connect/jdbc/using-an-sql-statement-to-modify-database-objects.md) | Describe cómo usar instrucciones SQL para modificar objetos de la base de datos.   |
| [Empleo de una instrucción SQL para modificar datos](../../connect/jdbc/using-an-sql-statement-to-modify-data.md)                         | Describe cómo usar instrucciones SQL para modificar datos de una base de datos. |
  
## <a name="see-also"></a>Consulte también

[Empleo de instrucciones con el controlador JDBC](../../connect/jdbc/using-statements-with-the-jdbc-driver.md)  
