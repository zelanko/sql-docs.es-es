---
title: Resultado de usar metadatos del conjunto | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 5e37529a-30db-48c8-b90a-ae9657d0f6b0
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 60b854cc260f0488f56e77fb10a34025c80d7620
ms.sourcegitcommit: ad2e98972a0e739c0fd2038ef4a030265f0ee788
ms.translationtype: MTE75
ms.contentlocale: es-ES
ms.lasthandoff: 06/07/2019
ms.locfileid: "66798638"
---
# <a name="using-result-set-metadata"></a>Usar metadatos del conjunto de resultados

[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

Para consultar información sobre las columnas que contiene un conjunto de resultados, [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] implementa la clase [SQLServerResultSetMetaData](../../connect/jdbc/reference/sqlserverresultsetmetadata-class.md). Esta clase contiene varios métodos que devuelven información como un solo valor.

Para crear un objeto SQLServerResultSetMetaData, puede usar el [getMetaData](../../connect/jdbc/reference/getmetadata-method-sqlserverresultset.md) método de la [SQLServerResultSet](../../connect/jdbc/reference/sqlserverresultset-class.md) clase.

En el ejemplo siguiente, una conexión abierta a la [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal_md.md)] base de datos de ejemplo se pasa a la función, se usa el método getMetaData de la clase SQLServerResultSet para devolver un objeto SQLServerResultSetMetaData y, a continuación, varios métodos de la Objeto SQLServerResultSetMetaData se usan para mostrar información sobre el tipo de datos y el nombre de las columnas contenidas en el conjunto de resultados.

[!code[JDBC#UsingResultSetMetaData1](../../connect/jdbc/codesnippet/Java/using-result-set-metadata_1.java)]

## <a name="see-also"></a>Consulte también

[Controlar metadatos con el controlador JDBC](../../connect/jdbc/handling-metadata-with-the-jdbc-driver.md)
