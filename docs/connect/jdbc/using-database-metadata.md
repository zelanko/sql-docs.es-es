---
title: Uso de los metadatos de base de datos | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 8b048371-e912-4ed1-afd7-436978f48888
caps.latest.revision: 13
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: b2f3e0a4e19b30eeb494f89281a01195cf98b7d9
ms.sourcegitcommit: e77197ec6935e15e2260a7a44587e8054745d5c2
ms.translationtype: MTE75
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2018
ms.locfileid: "37982117"
---
# <a name="using-database-metadata"></a>Usar metadatos de una base de datos
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  Para consultar en una base de datos información sobre compatibilidad, [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] implementa la clase [SQLServerDatabaseMetaData](../../connect/jdbc/reference/sqlserverdatabasemetadata-class.md). Esta clase contiene numerosos métodos que devuelven información en forma de un solo valor o de conjunto de resultados.  
  
 Para crear un objeto SQLServerDatabaseMetaData, puede usar el método [getMetaData](../../connect/jdbc/reference/getmetadata-method-sqlserverconnection.md) de la clase [SQLServerConnection](../../connect/jdbc/reference/sqlserverconnection-class.md) para obtener información sobre la base de datos a la que está conectado.  
  
 En el ejemplo siguiente, una conexión abierta a la [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal_md.md)] base de datos de ejemplo se pasa a la función, se usa el método getMetaData de la clase SQLServerConnection para devolver un objeto SQLServerDatabaseMetadata y, a continuación, varios métodos de la Objeto SQLServerDatabaseMetaData se usan para mostrar información sobre el controlador, versión del controlador, el nombre de base de datos y versión de la base de datos.  
  
 [!code[JDBC#UsingDBMetaData1](../../connect/jdbc/codesnippet/Java/using-database-metadata_1.java)]  
  
## <a name="see-also"></a>Ver también  
 [Controlar metadatos con el controlador JDBC](../../connect/jdbc/handling-metadata-with-the-jdbc-driver.md)  
  
  
