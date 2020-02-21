---
title: Empleo de metadatos de la base de datos | Microsoft Docs
ms.custom: ''
ms.date: 08/12/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 8b048371-e912-4ed1-afd7-436978f48888
author: MightyPen
ms.author: genemi
ms.openlocfilehash: fce2bf9d72136b303ee3bc974f3aede313233a82
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 01/31/2020
ms.locfileid: "69026417"
---
# <a name="using-database-metadata"></a>Empleo de metadatos de la base de datos

[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

Para consultar en una base de datos información sobre compatibilidad, [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] implementa la clase [SQLServerDatabaseMetaData](../../connect/jdbc/reference/sqlserverdatabasemetadata-class.md). Esta clase contiene numerosos métodos que devuelven información en forma de un solo valor o de conjunto de resultados.

Para crear un objeto SQLServerDatabaseMetaData, puede usar el método [getMetaData](../../connect/jdbc/reference/getmetadata-method-sqlserverconnection.md) de la clase [SQLServerConnection](../../connect/jdbc/reference/sqlserverconnection-class.md) para obtener información sobre la base de datos a la que está conectado.

En el ejemplo siguiente, se pasa a la función una conexión abierta a la base de datos de ejemplo de [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal_md.md)], el método getMetaData de la clase SQLServerConnection se usa para devolver un objeto SQLServerDatabaseMetadata y, a continuación, se usan los diversos métodos del objeto SQLServerDatabaseMetaData para mostrar información sobre el controlador, su versión y el nombre y la versión de la base de datos.

[!code[JDBC#UsingDBMetaData1](../../connect/jdbc/codesnippet/Java/using-database-metadata_1.java)]

## <a name="see-also"></a>Consulte también

[Control de metadatos con el controlador JDBC](../../connect/jdbc/handling-metadata-with-the-jdbc-driver.md)
