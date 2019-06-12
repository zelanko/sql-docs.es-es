---
title: Administrar conjuntos de resultados con el controlador JDBC | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 9ed5ad41-22e0-4e4a-8a79-10512db60d50
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: b78c12158cdebebd5619cdb4f18065d213245fed
ms.sourcegitcommit: ad2e98972a0e739c0fd2038ef4a030265f0ee788
ms.translationtype: MTE75
ms.contentlocale: es-ES
ms.lasthandoff: 06/07/2019
ms.locfileid: "66781486"
---
# <a name="managing-result-sets-with-the-jdbc-driver"></a>Administrar conjuntos de resultados con el controlador JDBC
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  Un conjunto de resultados es un objeto que representa un grupo de datos que ha devuelto un origen de datos, normalmente como resultado de una consulta. Los conjuntos de resultados contienen filas y columnas que alojan los elementos de datos solicitados. Además, se puede navegar por ellos con un cursor. Los conjuntos de resultados pueden ser actualizables, lo que significa que se pueden modificar e incluir esas modificaciones en el origen de datos. Los conjuntos de resultados también pueden tener varios niveles de sensibilidad a los cambios en el origen de datos subyacente.  
  
 El tipo de conjunto de resultados se determina cuando se crea una instrucción, que es cuando se hace una llamada al método [createStatement](../../connect/jdbc/reference/createstatement-method-sqlserverconnection.md) de la clase [SQLServerConnection](../../connect/jdbc/reference/sqlserverconnection-class.md). El papel fundamental de los conjuntos de resultados es proporcionar a las aplicaciones Java una representación utilizable de los datos de la base de datos. Esto normalmente se realiza con los métodos de tipo de establecimiento y obtención en los elementos de los datos del conjunto de resultados.  
  
 En el siguiente ejemplo, que está basado en la base de datos de ejemplo de [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal_md.md)], se crea un conjunto de resultados llamando al método [executeQuery](../../connect/jdbc/reference/executequery-method-sqlserverstatement.md) de la clase [SQLServerStatement](../../connect/jdbc/reference/sqlserverstatement-class.md). A continuación, los datos del conjunto de resultados se muestran mediante el método [getString](../../connect/jdbc/reference/getstring-method-sqlserverresultset.md) de la clase [SQLServerResultSet](../../connect/jdbc/reference/sqlserverresultset-class.md).  
  
 [!code[JDBC#ManagingResultSets1](../../connect/jdbc/codesnippet/Java/managing-result-sets-with-t_1.java)]  
  
 Los temas de esta sección describen diferentes aspectos del uso de los conjuntos de resultados, incluyendo los tipos de cursor, la simultaneidad y el bloqueo de filas.  
  
## <a name="in-this-section"></a>En esta sección  
  
|Tema|Descripción|  
|-----------|-----------------|  
|[Descripción de los tipos de cursor](../../connect/jdbc/understanding-cursor-types.md)|Describe los diferentes tipos de cursor que el [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] admite.|  
|[Descripción del control de simultaneidad](../../connect/jdbc/understanding-concurrency-control.md)|Describe la compatibilidad del controlador JDBC con el control de simultaneidad.|  
|[Descripción del bloqueo de filas](../../connect/jdbc/understanding-row-locking.md)|Describe la compatibilidad del controlador JDBC con el bloqueo de filas.|  
  
## <a name="see-also"></a>Consulte también  
 [Introducción al controlador JDBC](../../connect/jdbc/overview-of-the-jdbc-driver.md)  
  
  
