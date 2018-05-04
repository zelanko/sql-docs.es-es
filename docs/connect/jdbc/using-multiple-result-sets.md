---
title: Utilizar varios conjuntos de resultados | Documentos de Microsoft
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
ms.topic: conceptual
ms.assetid: ab6a3cfa-073b-44e9-afca-a8675cfe5fd1
caps.latest.revision: 33
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: ba12e749d6fe8131b0e2a1183f20a9d9101d7e53
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="using-multiple-result-sets"></a>Usar múltiples conjuntos de resultados
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  Cuando se trabaja con SQL insertado o [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] procedimientos almacenados que devuelven más de un conjunto de resultados, el [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] proporciona el [getResultSet](../../connect/jdbc/reference/getresultset-method-sqlserverstatement.md) método en el [SQLServerStatement](../../connect/jdbc/reference/sqlserverstatement-class.md) clase recuperar todos los conjuntos de datos devueltos. Además, cuando se ejecuta una instrucción que devuelve más de un conjunto de resultados, puede usar el [ejecutar](../../connect/jdbc/reference/execute-method-sqlserverstatement.md) clase de método de SQLServerStatement, porque devolverá un **booleano** valor que indica si el valor devuelto es un conjunto de resultados o un recuento de actualización.  
  
 Si el método execute devuelve **true**, la instrucción que se ha ejecutado ha devuelto uno o varios conjuntos de resultados. Puede tener acceso el primer conjunto llamando al método getResultSet de resultados. Para determinar si hay más conjuntos de resultados, puede llamar a la [getMoreResults](../../connect/jdbc/reference/getmoreresults-method-sqlserverstatement.md) método, que devuelve un **booleano** valo **true** si hay disponibles más conjuntos de resultados. Si hay más conjuntos de resultados, puede llamar al método de getResultSet nuevo para tener acceso a ellos, continuando el proceso hasta han procesado todos los conjuntos de resultados. Si el método getMoreResults devuelve **false**, hay que no hay más conjuntos de resultados al proceso.  
  
 Si el método execute devuelve **false**, la instrucción que se ha ejecutado ha devuelto un valor de recuento de actualización, que puede recuperar mediante una llamada a la [getUpdateCount](../../connect/jdbc/reference/getupdatecount-method-sqlserverstatement.md) método.  
  
> [!NOTE]  
>  Para obtener más información sobre recuentos de actualizaciones, consulte [mediante un procedimiento almacenado con un recuento de actualización](../../connect/jdbc/using-a-stored-procedure-with-an-update-count.md).  
  
 En el ejemplo siguiente, una conexión abierta a la [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal_md.md)] base de datos de ejemplo se pasa a la función y se construye una instrucción SQL que, cuando se ejecuta, devuelve dos conjuntos de resultados:  
  
 [!code[JDBC#UsingMultipleResultSets1](../../connect/jdbc/codesnippet/Java/using-multiple-result-sets_1.java)]  
  
 En este caso, se sabe que el número de conjuntos de resultados que se devuelven es dos. No obstante, el código está escrito de forma que si se devolviera un número desconocido de conjuntos de resultados, como cuando se llama a un procedimiento almacenado, se procesarían todos. Para ver un ejemplo de una llamada a un procedimiento almacenado que devuelve varios conjuntos de resultados junto con los valores de actualización, vea [controlar instrucciones complejas](../../connect/jdbc/handling-complex-statements.md).  
  
> [!NOTE]  
>  Cuando realiza la llamada al método getMoreResults de la clase SQLServerStatement, implícitamente se cierra el conjunto de resultados devuelto anteriormente.  
  
## <a name="see-also"></a>Vea también  
 [Usar instrucciones con el controlador JDBC](../../connect/jdbc/using-statements-with-the-jdbc-driver.md)  
  
  
