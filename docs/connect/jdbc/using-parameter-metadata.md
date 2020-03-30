---
title: Empleo de matadatos del parámetro | Microsoft Docs
ms.custom: ''
ms.date: 08/12/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: db2c1957-91c6-4989-a07b-9f8be6d2033a
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 80ff8cebcc4141e8363c25f83821cb4924e6c46a
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 03/29/2020
ms.locfileid: "69026076"
---
# <a name="using-parameter-metadata"></a>Empleo de metadatos del parámetro

[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

Para consultar un objeto [SQLServerPreparedStatement](../../connect/jdbc/reference/sqlserverpreparedstatement-class.md) o [SQLServerCallableStatement](../../connect/jdbc/reference/sqlservercallablestatement-class.md) sobre los parámetros que contiene, [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] implementa la clase [SQLServerParameterMetaData](../../connect/jdbc/reference/sqlserverparametermetadata-class.md). Esta clase contiene numerosos campos y métodos que devuelven información en forma de un solo valor.

Para crear un objeto SQLServerParameterMetaData, puede usar los métodos [getParameterMetaData](../../connect/jdbc/reference/getparametermetadata-method-sqlserverpreparedstatement.md) de las clases SQLServerPreparedStatement y SQLServerCallableStatement.

En el siguiente ejemplo, una conexión abierta a la base de datos de ejemplo [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal_md.md)] se pasa a la función, el método getParameterMetaData de la clase SQLServerCallableStatement se usa para devolver un objeto SQLServerParameterMetaData y luego se usan distintos métodos del objeto SQLServerParameterMetaData para mostrar información sobre el tipo y modo de los parámetros que se incluyen en el procedimiento almacenado HumanResources.uspUpdateEmployeeHireInfo.

[!code[JDBC#UsingParamMetaData1](../../connect/jdbc/codesnippet/Java/using-parameter-metadata_1.java)]  

> [!NOTE]  
> Hay varias limitaciones a la hora de usar la clase SQLServerParameterMetaData con instrucciones preparadas.
>
> **Con Microsoft JDBC Driver 6.0 (o superior) para SQL Server**: al usar SQL Server 2008 o 2008 R2, el controlador JDBC admite las instrucciones SELECT, DELETE, INSERT y UPDATE siempre y cuando estas no contengan subconsultas ni combinaciones.

Las consultas MERGE tampoco se admiten para la clase SQLServerParameterMetaData al usar SQL Server 2008 o 2008 R2. Para SQL Server 2012 y versiones superiores, se admiten metadatos de parámetros con consultas complejas.

No se admite la recuperación de metadatos de parámetros para columnas cifradas. **Con Microsoft JDBC Driver 4.1 o 4.2 para SQL Server**: el controlador JDBC admite las instrucciones SELECT, DELETE, INSERT y UPDATE siempre y cuando estas no contengan subconsultas ni combinaciones. Las consultas MERGE tampoco se admiten para la clase SQLServerParameterMetaData.
