---
title: Usar instrucciones con procedimientos almacenados | Microsoft Docs
ms.custom: ''
ms.date: 08/12/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 0041f9e1-09b6-4487-b052-afd636c8e89a
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 7fe07352ff1bcda9dd3ff3e77a6b879e592235a6
ms.sourcegitcommit: 9348f79efbff8a6e88209bb5720bd016b2806346
ms.translationtype: MTE75
ms.contentlocale: es-ES
ms.lasthandoff: 08/14/2019
ms.locfileid: "69025863"
---
# <a name="using-statements-with-stored-procedures"></a>Empleo de instrucciones con procedimientos almacenados

[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

Un procedimiento almacenado es un procedimiento de base de datos, similar a un procedimiento en otros lenguajes de programación, que está contenido en la misma base de datos. En [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], se pueden crear procedimientos almacenados mediante [!INCLUDE[tsql](../../includes/tsql-md.md)] o mediante Common Language Runtime (CLR) y uno de los lenguajes de programación de Visual Studio, como Visual Basic o C#. Por lo general, los procedimientos almacenados de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] pueden hacer lo siguiente:  
  
- Aceptar parámetros de entrada y devolver varios valores en forma de parámetros de salida al lote o al procedimiento que realiza la llamada.  
  
- Contener instrucciones de programación que realicen operaciones en la base de datos, incluidas las llamadas a otros procedimientos.  
  
- Devolver un valor de estado a un lote o a un procedimiento que realice una llamada para indicar si la operación se ha realizado correctamente o se han producido errores, y el motivo de estos.  
  
> [!NOTE]  
> Para obtener más información sobre los procedimientos almacenados de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], vea "Procedimientos almacenados" en Libros en pantalla de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
Para trabajar con datos de una base de datos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] mediante un procedimiento almacenado, [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] proporciona las clases [SQLServerStatement](../../connect/jdbc/reference/sqlserverstatement-class.md), [SQLServerPreparedStatement](../../connect/jdbc/reference/sqlserverpreparedstatement-class.md) y [SQLServerCallableStatement](../../connect/jdbc/reference/sqlservercallablestatement-class.md). La clase usada depende de si el procedimiento almacenado requiere los parámetros IN (entrada) u OUT (salida). Si el procedimiento almacenado no requiere parámetros IN ni OUT, puede usar la clase SQLServerStatement; si se llama al procedimiento almacenado varias veces o este requiere solo parámetros IN, puede usar la clase SQLServerPreparedStatement. Si el procedimiento almacenado requiere parámetros IN y OUT, debe usar la clase SQLServerCallableStatement. Solo si el procedimiento almacenado requiere parámetros OUT, necesita usar la clase SQLServerCallableStatement.  
  
> [!NOTE]  
> Los procedimientos almacenados también pueden devolver recuentos de actualización y varios conjuntos de resultados. Para obtener más información, vea [usar un procedimiento almacenado con un recuento de actualizaciones](../../connect/jdbc/using-a-stored-procedure-with-an-update-count.md) y [usar varios conjuntos de resultados](../../connect/jdbc/using-multiple-result-sets.md).  
  
Si usa el controlador JDBC para llamar a un procedimiento almacenado con parámetros, debe usar la secuencia de escape de SQL `call` junto con el método [prepareCall](../../connect/jdbc/reference/preparecall-method-sqlserverconnection.md) de la clase [SQLServerConnection](../../connect/jdbc/reference/sqlserverconnection-class.md). La sintaxis completa de la secuencia de escape `call` es la siguiente:  
  
 `{[?=]call procedure-name[([parameter][,[parameter]]...)]}`  
  
> [!NOTE]  
> Para obtener más información sobre `call` y otras secuencias de escape de SQL, vea [usar secuencias de escape de SQL](../../connect/jdbc/using-sql-escape-sequences.md).  
  
En los temas de esta sección se describen las formas en las que puede llamar a los procedimientos almacenados de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] con el controlador JDBC y la secuencia de escape de SQL `call`.  
  
## <a name="in-this-section"></a>En esta sección  
  
|Tema|Descripción|  
|-----------|-----------------|  
|[Empleo de un procedimiento almacenado sin parámetros](../../connect/jdbc/using-a-stored-procedure-with-no-parameters.md)|Describe cómo usar el controlador JDBC para ejecutar procedimientos almacenados que no contengan parámetros de entrada o de salida.|  
|[Empleo de un procedimiento almacenado con parámetros de entrada](../../connect/jdbc/using-a-stored-procedure-with-input-parameters.md)|Describe cómo usar el controlador JDBC para ejecutar procedimientos almacenados que contengan parámetros de entrada.|  
|[Empleo de un procedimiento almacenado con parámetros de salida](../../connect/jdbc/using-a-stored-procedure-with-output-parameters.md)|Describe cómo usar el controlador JDBC para ejecutar procedimientos almacenados que contengan parámetros de salida.|  
|[Empleo de un procedimiento almacenado con un estado de retorno](../../connect/jdbc/using-a-stored-procedure-with-a-return-status.md)|Describe cómo usar el controlador JDBC para ejecutar procedimientos almacenados que contengan valores de estado de devolución.|  
|[Empleo de un procedimiento almacenado con un recuento de actualización](../../connect/jdbc/using-a-stored-procedure-with-an-update-count.md)|Describe cómo usar el controlador JDBC para ejecutar procedimientos almacenados que devuelvan recuentos de actualizaciones.|  
  
## <a name="see-also"></a>Vea también

[Empleo de instrucciones con el controlador JDBC](../../connect/jdbc/using-statements-with-the-jdbc-driver.md)  
