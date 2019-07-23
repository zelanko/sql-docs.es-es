---
title: Usar instrucciones con SQL | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: fe28f48a-e1bc-48ff-a5e7-c24cd6e5ecc7
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 082671d3acf2873bb822e6b836599c00f42d6323
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "67916159"
---
# <a name="using-statements-with-sql"></a>Usar instrucciones con SQL

[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

Cuando se trabaja con datos de una base de datos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] mediante [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] e instrucciones SQL insertadas, se pueden usar varias clases. La clase usada depende del tipo de instrucción SQL que desee ejecutar.  
  
Si la instrucción SQL no contiene parámetros IN, use la clase [SQLServerStatement](../../connect/jdbc/reference/sqlserverstatement-class.md), pero si contiene parámetros IN, use la clase [SQLServerPreparedStatement](../../connect/jdbc/reference/sqlserverpreparedstatement-class.md).  
  
> [!NOTE]  
> Si necesita usar instrucciones SQL que contengan parámetros IN y OUT, debe implementarlas como procedimientos almacenados y llamarlas mediante la clase [SQLServerCallableStatement](../../connect/jdbc/reference/sqlservercallablestatement-class.md). Para obtener más información sobre el uso de procedimientos almacenados, vea [usar instrucciones con procedimientos almacenados](../../connect/jdbc/using-statements-with-stored-procedures.md).  
  
En las siguientes secciones se describen las diferentes situaciones de trabajo con datos de una base de datos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] mediante instrucciones SQL.  

## <a name="in-this-section"></a>En esta sección  

| Tema                                                                                                                        | Descripción                                                       |
| ---------------------------------------------------------------------------------------------------------------------------- | ----------------------------------------------------------------- |
| [Usar una instrucción SQL sin parámetros](../../connect/jdbc/using-an-sql-statement-with-no-parameters.md)                 | Describe cómo usar instrucciones SQL que no contienen parámetros.   |
| [Usar una instrucción SQL con parámetros](../../connect/jdbc/using-an-sql-statement-with-parameters.md)                       | Describe cómo usar instrucciones SQL que contienen parámetros.      |
| [Usar una instrucción SQL para modificar objetos de la base de datos](../../connect/jdbc/using-an-sql-statement-to-modify-database-objects.md) | Describe cómo usar instrucciones SQL para modificar objetos de la base de datos.   |
| [Usar una instrucción SQL para modificar datos](../../connect/jdbc/using-an-sql-statement-to-modify-data.md)                         | Describe cómo usar instrucciones SQL para modificar datos de una base de datos. |
  
## <a name="see-also"></a>Consulte también

[Usar instrucciones con el controlador JDBC](../../connect/jdbc/using-statements-with-the-jdbc-driver.md)  
