---
title: Usar metadatos de parámetros | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2018
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: db2c1957-91c6-4989-a07b-9f8be6d2033a
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 168a153ecf12acda5adfbae22d13618669c6c2a4
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "67916214"
---
# <a name="using-parameter-metadata"></a>Usar metadatos de parámetros

[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

Para consultar un objeto [SQLServerPreparedStatement](../../connect/jdbc/reference/sqlserverpreparedstatement-class.md) o [SQLServerCallableStatement](../../connect/jdbc/reference/sqlservercallablestatement-class.md) sobre los parámetros que contiene, [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] implementa la clase [SQLServerParameterMetaData](../../connect/jdbc/reference/sqlserverparametermetadata-class.md). Esta clase contiene numerosos campos y métodos que devuelven información en forma de un solo valor.

Para crear un objeto SQLServerParameterMetaData, puede utilizar los métodos [getParameterMetaData](../../connect/jdbc/reference/getparametermetadata-method-sqlserverpreparedstatement.md) de las clases SQLServerPreparedStatement y SQLServerCallableStatement.

En el ejemplo siguiente, se pasa una conexión abierta [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal_md.md)] a la base de datos de ejemplo a la función, el método getParameterMetaData de la clase SQLServerCallableStatement se usa para devolver un objeto SQLServerParameterMetaData y, a continuación, varios los métodos del objeto SQLServerParameterMetaData se usan para mostrar información sobre el tipo y el modo de los parámetros incluidos en el procedimiento almacenado HumanResources. uspUpdateEmployeeHireInfo.

[!code[JDBC#UsingParamMetaData1](../../connect/jdbc/codesnippet/Java/using-parameter-metadata_1.java)]  

> [!NOTE]  
> Hay algunas limitaciones cuando se usa la clase SQLServerParameterMetaData con instrucciones preparadas.
>
> **Con Microsoft JDBC Driver 6.0 (o superior) para SQL Server**: al usar SQL Server 2008 o 2008 R2, el controlador JDBC admite las instrucciones SELECT, DELETE, INSERT y UPDATE siempre y cuando estas no contengan subconsultas ni combinaciones.

Las consultas MERGE tampoco se admiten para la clase SQLServerParameterMetaData al usar SQL Server 2008 o 2008 R2. Para SQL Server 2012 y versiones superiores, se admiten metadatos de parámetros con consultas complejas.

No se admite la recuperación de metadatos de parámetros para columnas cifradas. **Con Microsoft JDBC Driver 4.1 o 4.2 para SQL Server**: el controlador JDBC admite las instrucciones SELECT, DELETE, INSERT y UPDATE siempre y cuando estas no contengan subconsultas ni combinaciones. Las consultas de combinación tampoco se admiten para la clase SQLServerParameterMetaData.
