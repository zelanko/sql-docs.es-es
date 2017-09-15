---
title: Usar instrucciones con procedimientos almacenados | Documentos de Microsoft
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 0041f9e1-09b6-4487-b052-afd636c8e89a
caps.latest.revision: 20
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: f617fdf969c0bdd238b07cb0def1b0a948a4d328
ms.contentlocale: es-es
ms.lasthandoff: 09/09/2017

---
# <a name="using-statements-with-stored-procedures"></a>Usar instrucciones con procedimientos almacenados
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  Un procedimiento almacenado es un procedimiento de base de datos, similar a un procedimiento en otros lenguajes de programación, que está contenido en la misma base de datos. En [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)], se pueden crear procedimientos almacenados mediante el uso de [!INCLUDE[tsql](../../includes/tsql_md.md)], o mediante common language runtime (CLR) y uno de Visual Studio de lenguajes como Visual Basic o C# de programación. Por lo general, [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] los procedimientos almacenados pueden hacer lo siguiente:  
  
-   Aceptar parámetros de entrada y devolver varios valores en forma de parámetros de salida al lote o al procedimiento que realiza la llamada.  
  
-   Contener instrucciones de programación que realicen operaciones en la base de datos, incluidas las llamadas a otros procedimientos.  
  
-   Devolver un valor de estado a un lote o a un procedimiento que realice una llamada para indicar si la operación se ha realizado correctamente o se han producido errores, y el motivo de estos.  
  
> [!NOTE]  
>  Para obtener más información acerca de [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] los procedimientos almacenados, vea "Procedimientos almacenados" en [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] libros en pantalla.  
  
 Para trabajar con datos en un [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] base de datos mediante un procedimiento almacenado, el [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] proporciona el [SQLServerStatement](../../connect/jdbc/reference/sqlserverstatement-class.md), [SQLServerPreparedStatement](../../connect/jdbc/reference/sqlserverpreparedstatement-class.md), y [ SQLServerCallableStatement](../../connect/jdbc/reference/sqlservercallablestatement-class.md) clases. La clase usada depende de si el procedimiento almacenado requiere los parámetros IN (entrada) u OUT (salida). Si no hay ninguna en requiere que el procedimiento almacenado o los parámetros de salida, puede usar la clase SQLServerStatement; Si el procedimiento almacenado se llamará varias veces, o requiere solo parámetros IN, puede usar la clase SQLServerPreparedStatement. Si el procedimiento almacenado requiere IN y los parámetros OUT, debe usar la clase SQLServerCallableStatement. Es solo si el procedimiento almacenado requiere parámetros OUT que necesitará la sobrecarga resultante de usar la clase SQLServerCallableStatement.  
  
> [!NOTE]  
>  Los procedimientos almacenados también pueden conteos de actualizaciones devueltos y varios conjuntos de resultados. Para obtener más información, consulte [mediante un procedimiento almacenado con un recuento de actualizaciones](../../connect/jdbc/using-a-stored-procedure-with-an-update-count.md) y [utilizando varios conjuntos de resultados](../../connect/jdbc/using-multiple-result-sets.md).  
  
 Al usar el controlador JDBC para llamar a un procedimiento almacenado con parámetros, debe usar el `call` secuencia de escape SQL junto con la [prepareCall](../../connect/jdbc/reference/preparecall-method-sqlserverconnection.md) método de la [SQLServerConnection](../../connect/jdbc/reference/sqlserverconnection-class.md) clase. La sintaxis completa de la `call` secuencia de escape es como sigue:  
  
 `{[?=]call procedure-name[([parameter][,[parameter]]...)]}`  
  
> [!NOTE]  
>  Para obtener más información sobre la `call` y otro SQL secuencias de escape, vea [usar secuencias de Escape de SQL](../../connect/jdbc/using-sql-escape-sequences.md).  
  
 Los temas de esta sección describen las maneras en que se pueden llamar a [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] procedimientos almacenados con el controlador JDBC y `call` secuencia de escape SQL.  
  
## <a name="in-this-section"></a>En esta sección  
  
|Tema|Description|  
|-----------|-----------------|  
|[Usar un procedimiento almacenado sin parámetros](../../connect/jdbc/using-a-stored-procedure-with-no-parameters.md)|Describe cómo usar el controlador JDBC para ejecutar procedimientos almacenados que no contengan parámetros de entrada o de salida.|  
|[Uso de un procedimiento almacenado con parámetros de entrada](../../connect/jdbc/using-a-stored-procedure-with-input-parameters.md)|Describe cómo usar el controlador JDBC para ejecutar procedimientos almacenados que contengan parámetros de entrada.|  
|[Uso de un procedimiento almacenado con parámetros de salida](../../connect/jdbc/using-a-stored-procedure-with-output-parameters.md)|Describe cómo usar el controlador JDBC para ejecutar procedimientos almacenados que contengan parámetros de salida.|  
|[Uso de un procedimiento almacenado con un estado de retorno](../../connect/jdbc/using-a-stored-procedure-with-a-return-status.md)|Describe cómo usar el controlador JDBC para ejecutar procedimientos almacenados que contengan valores de estado de devolución.|  
|[Uso de un procedimiento almacenado con un recuento de actualizaciones](../../connect/jdbc/using-a-stored-procedure-with-an-update-count.md)|Describe cómo usar el controlador JDBC para ejecutar procedimientos almacenados que devuelvan recuentos de actualizaciones.|  
  
## <a name="see-also"></a>Vea también  
 [Usar instrucciones con el controlador JDBC](../../connect/jdbc/using-statements-with-the-jdbc-driver.md)  
  
  
