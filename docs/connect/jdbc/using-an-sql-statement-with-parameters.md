---
title: "Usar una instrucción SQL con parámetros | Documentos de Microsoft"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 3202b88f-ce13-44dd-982c-c6a3b0260378
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 8475ea4917ffcc0d9226933b29e81b99f89345c2
ms.contentlocale: es-es
ms.lasthandoff: 09/09/2017

---
# <a name="using-an-sql-statement-with-parameters"></a>Usar una instrucción SQL con parámetros
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  Para trabajar con datos en un [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] base de datos mediante una instrucción SQL que contiene parámetros IN, se puede utilizar el [executeQuery](../../connect/jdbc/reference/executequery-method-sqlserverpreparedstatement.md) método de la [SQLServerPreparedStatement](../../connect/jdbc/reference/sqlserverpreparedstatement-class.md) clase para devolver un [ SQLServerResultSet](../../connect/jdbc/reference/sqlserverresultset-class.md) que contendrá los datos solicitados. Para ello, primero debe crear un objeto SQLServerPreparedStatement mediante el uso de la [prepareStatement](../../connect/jdbc/reference/preparestatement-method-sqlserverconnection.md) método de la [SQLServerConnection](../../connect/jdbc/reference/sqlserverconnection-class.md) clase.  
  
 Al generar la instrucción SQL, los parámetros IN se especifican mediante el carácter ? (signo de interrogación), que actúa como un marcador de posición para los valores de parámetros que se van a pasar a la instrucción SQL. Para especificar un valor para un parámetro, puede usar uno de los métodos de establecedor de la clase SQLServerPreparedStatement. El método de establecedor usado se determina mediante el tipo de datos del valor que desea pasar a la instrucción SQL.  
  
 Al pasar un valor al método de establecedor, debe especificar no sólo el valor real que se va a usar en la instrucción SQL, sino también la posición ordinal del parámetro en la instrucción SQL. Por ejemplo, si la instrucción SQL contiene un único parámetro, su valor ordinal será 1. Si la instrucción contiene dos parámetros, el primer valor ordinal será 1, mientras que el segundo valor ordinal será 2.  
  
 En el ejemplo siguiente, una conexión abierta a la [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal_md.md)] base de datos de ejemplo se pasa a la función, se genera una instrucción SQL preparada y se ejecuta con un valor de parámetro de cadena único y, a continuación, se leen los resultados del conjunto de resultados.  
  
 [!code[JDBC#UsingSQLWithParams1](../../connect/jdbc/codesnippet/Java/using-an-sql-statement-w_1_1.java)]  
  
## <a name="see-also"></a>Vea también  
 [Usar instrucciones con SQL](../../connect/jdbc/using-statements-with-sql.md)  
  
  

