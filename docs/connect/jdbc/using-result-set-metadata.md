---
title: Metadatos del conjunto de resultado de usar | Documentos de Microsoft
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 5e37529a-30db-48c8-b90a-ae9657d0f6b0
caps.latest.revision: 13
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 4ea7ce7da7d5327c12204d60ec5c97ec58793403
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
ms.locfileid: "32853170"
---
# <a name="using-result-set-metadata"></a>Usar metadatos del conjunto de resultados
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  Para consultar un conjunto de resultados para obtener información acerca de las columnas que contiene, el [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] implementa la [SQLServerResultSetMetaData](../../connect/jdbc/reference/sqlserverresultsetmetadata-class.md) clase. Esta clase contiene varios métodos que devuelven información como un solo valor.  
  
 Para crear un objeto SQLServerResultSetMetaData, puede usar el [getMetaData](../../connect/jdbc/reference/getmetadata-method-sqlserverresultset.md) método de la [SQLServerResultSet](../../connect/jdbc/reference/sqlserverresultset-class.md) clase.  
  
 En el ejemplo siguiente, una conexión abierta a la [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal_md.md)] base de datos de ejemplo se pasa a la función, se usa el método getMetaData de la clase SQLServerResultSet para devolver un objeto SQLServerResultSetMetaData y, a continuación, varios métodos de la Objeto SQLServerResultSetMetaData se usan para mostrar información sobre el nombre y tipo de datos de las columnas contenidas en el conjunto de resultados.  
  
 [!code[JDBC#UsingResultSetMetaData1](../../connect/jdbc/codesnippet/Java/using-result-set-metadata_1.java)]  
  
## <a name="see-also"></a>Vea también  
 [Controlar metadatos con el controlador JDBC](../../connect/jdbc/handling-metadata-with-the-jdbc-driver.md)  
  
  
