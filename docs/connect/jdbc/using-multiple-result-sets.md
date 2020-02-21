---
title: Empleo de varios conjuntos de resultados | Microsoft Docs
ms.custom: ''
ms.date: 08/12/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: ab6a3cfa-073b-44e9-afca-a8675cfe5fd1
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 802ade7a34eb5c5174efc35032587f801ef12179
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 01/31/2020
ms.locfileid: "69026276"
---
# <a name="using-multiple-result-sets"></a>Empleo de varios conjuntos de resultados

[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

Cuando se trabaja con SQL insertado o procedimientos almacenados de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que devuelven más de un conjunto de resultados, [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] proporciona el método [getResultSet](../../connect/jdbc/reference/getresultset-method-sqlserverstatement.md) de la clase [SQLServerStatement](../../connect/jdbc/reference/sqlserverstatement-class.md) para recuperar cada conjunto de datos devuelto. Además, si ejecuta una instrucción que devuelva más de un conjunto de resultados, puede usar el método [execute](../../connect/jdbc/reference/execute-method-sqlserverstatement.md) de la clase SQLServerStatement, ya que devuelve un valor **booleano** que indica si el valor devuelto es un conjunto de resultados o un recuento de actualización.

Si el método execute devuelve **true**, la instrucción que se ha ejecutado ha devuelto uno o más conjuntos de resultados. Puede acceder al primer conjunto de resultados si llama al método getResultSet. Para determinar si hay más conjuntos de resultados disponibles, puede llamar al método [getMoreResults](../../connect/jdbc/reference/getmoreresults-method-sqlserverstatement.md), que devuelve un valor **booleano** de **true** si hay más conjuntos de resultados disponibles. Si hay disponibles más conjuntos de resultados, puede volver a llamar al método getResultSet para acceder a ellos, continuando el proceso hasta que se hayan procesado todos los conjuntos de resultados. Si el método getMoreResults devuelve **false**, no hay más conjuntos de resultados que procesar.

Si el método execute devuelve **false**, la instrucción que se ha ejecutado ha devuelto un valor de recuento de actualización, que se puede recuperar al llamar al método [getUpdateCount](../../connect/jdbc/reference/getupdatecount-method-sqlserverstatement.md).

> [!NOTE]  
> Para obtener más información sobre los recuentos de actualizaciones, consulte [Empleo de un procedimiento almacenado con un recuento de actualización](../../connect/jdbc/using-a-stored-procedure-with-an-update-count.md).

En el siguiente ejemplo, se pasa a la función una conexión abierta a la base de datos de ejemplo [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal_md.md)] y se construye una instrucción SQL que, al ejecutarse, devuelve dos conjuntos de resultados:

[!code[JDBC#UsingMultipleResultSets1](../../connect/jdbc/codesnippet/Java/using-multiple-result-sets_1.java)]

En este caso, se sabe que el número de conjuntos de resultados que se devuelven es dos. No obstante, el código está escrito de forma que si se devolviera un número desconocido de conjuntos de resultados, como cuando se llama a un procedimiento almacenado, se procesarían todos. Para ver un ejemplo de llamada a un procedimiento almacenado que devuelve varios conjuntos de resultados junto con valores de actualización, vea [Control de instrucciones complejas](../../connect/jdbc/handling-complex-statements.md).

> [!NOTE]  
> Cuando hace la llamada al método getMoreResults de la clase SQLServerStatement, se cierra el conjunto de resultados que se había devuelto anteriormente.

## <a name="see-also"></a>Consulte también

[Empleo de instrucciones con el controlador JDBC](../../connect/jdbc/using-statements-with-the-jdbc-driver.md)
