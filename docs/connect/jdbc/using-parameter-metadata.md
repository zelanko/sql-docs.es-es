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
manager: jroth
ms.openlocfilehash: e2c0e9f7589f58a1ef3c1cc5ee4026dd9eea5076
ms.sourcegitcommit: ad2e98972a0e739c0fd2038ef4a030265f0ee788
ms.translationtype: MTE75
ms.contentlocale: es-ES
ms.lasthandoff: 06/07/2019
ms.locfileid: "66798567"
---
# <a name="using-parameter-metadata"></a>Usar metadatos de parámetros

[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

Para consultar un objeto [SQLServerPreparedStatement](../../connect/jdbc/reference/sqlserverpreparedstatement-class.md) o [SQLServerCallableStatement](../../connect/jdbc/reference/sqlservercallablestatement-class.md) sobre los parámetros que contiene, [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] implementa la clase [SQLServerParameterMetaData](../../connect/jdbc/reference/sqlserverparametermetadata-class.md). Esta clase contiene numerosos campos y métodos que devuelven información en forma de un solo valor.

Para crear un objeto SQLServerParameterMetaData, puede usar el [getParameterMetaData](../../connect/jdbc/reference/getparametermetadata-method-sqlserverpreparedstatement.md) métodos de las clases SQLServerPreparedStatement y SQLServerCallableStatement.

En el ejemplo siguiente, una conexión abierta a la [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal_md.md)] base de datos de ejemplo se pasa a la función, se usa el método getParameterMetaData de la clase SQLServerCallableStatement para devolver un objeto SQLServerParameterMetaData y, a continuación, varios métodos del objeto SQLServerParameterMetaData se usan para mostrar información sobre el tipo y el modo de los parámetros que están dentro del procedimiento almacenado HumanResources.uspUpdateEmployeeHireInfo.

[!code[JDBC#UsingParamMetaData1](../../connect/jdbc/codesnippet/Java/using-parameter-metadata_1.java)]  

> [!NOTE]  
> Existen algunas limitaciones cuando se usa la clase SQLServerParameterMetaData con instrucciones preparadas.
>
> **Con Microsoft JDBC Driver 6.0 (o superior) para SQL Server**: al usar SQL Server 2008 o 2008 R2, el controlador JDBC admite las instrucciones SELECT, DELETE, INSERT y UPDATE siempre y cuando estas no contengan subconsultas ni combinaciones.

Las consultas MERGE tampoco se admiten para la clase SQLServerParameterMetaData al usar SQL Server 2008 o 2008 R2. Para SQL Server 2012 y versiones superiores, se admiten metadatos de parámetros con consultas complejas.

No se admite la recuperación de metadatos de parámetros para las columnas cifradas. **Con Microsoft JDBC Driver 4.1 o 4.2 para SQL Server**: el controlador JDBC admite las instrucciones SELECT, DELETE, INSERT y UPDATE siempre y cuando estas no contengan subconsultas ni combinaciones. También, las consultas de combinación no se admiten para la clase SQLServerParameterMetaData.
