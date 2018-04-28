---
title: Control de errores | Documentos de Microsoft
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: jdbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 8fd5b5ef-d939-4b78-b900-5b7b6ddb3eb9
caps.latest.revision: 14
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 4a5a30d85dedb8de9d5cbfcff1714731c04fcd66
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/16/2018
---
# <a name="handling-errors"></a>Control de errores
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  Cuando se usa el [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)], todas las condiciones de error de base de datos se devuelven a la aplicación Java como excepciones mediante la [SQLServerException](../../connect/jdbc/reference/sqlserverexception-class.md) clase. Los siguientes métodos de la clase SQLServerException están heredados de java.sql.SQLException y java.lang.Throwable y puede usarse para devolver información específica sobre la [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] error que se ha producido:  
  
-   getSQLState devuelve el estándar X / Open o SQL99 de código de estado de la excepción.  
  
-   getErrorCode devuelve el número de error específico de la base de datos.  
  
-   getMessage devuelve el texto completo de la excepción. El texto del mensaje de error describe el problema y, con frecuencia, incluye marcadores de posición de información tales como nombres de objetos, que se incluyen en el mensaje de error cuando se muestra.  
  
-   getNextException devuelve el siguiente objeto SQLServerException o null si no hay ningún objeto de excepción más para devolver.  
  
 En el ejemplo siguiente, una conexión abierta a la [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal_md.md)] base de datos de ejemplo se pasa a la función y se construye una instrucción SQL incorrecta que no tiene una cláusula FROM. A continuación, se ejecuta la instrucción de SQL y se procesa una excepción de SQL.  
  
 [!code[JDBC#HandlingErrors1](../../connect/jdbc/codesnippet/Java/handling-errors_1.java)]  
  
## <a name="see-also"></a>Vea también  
 [Diagnosticar problemas del controlador JDBC](../../connect/jdbc/diagnosing-problems-with-the-jdbc-driver.md)  
  
  
