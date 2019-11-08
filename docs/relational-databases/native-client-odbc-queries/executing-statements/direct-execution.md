---
title: Ejecución directa | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- ODBC applications, statements
- direct execution [ODBC]
- SQLExecDirect function
- statements [ODBC], direct execution
ms.assetid: fa36e1af-ed98-4abc-97c1-c4cc5d227b29
author: MightyPen
ms.author: genemi
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 292b0f787819a52eb5759ead41bde80fc3a72acf
ms.sourcegitcommit: 856e42f7d5125d094fa84390bc43048808276b57
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/07/2019
ms.locfileid: "73779760"
---
# <a name="direct-execution"></a>Ejecución directa
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  La ejecución directa es la manera más sencilla de ejecutar una instrucción. Una aplicación genera una cadena de caracteres que contiene una instrucción [!INCLUDE[tsql](../../../includes/tsql-md.md)] y la envía para su ejecución mediante la función **SQLExecDirect** . Cuando la instrucción llega al servidor, [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] la compila en un plan de ejecución y ejecuta inmediatamente el plan de ejecución.  
  
 La ejecución directa se utiliza habitualmente en las aplicaciones que generan y ejecutan instrucciones en tiempo de ejecución y es el método más eficaz para las instrucciones que se van a ejecutar una sola vez. El inconveniente cuando se utiliza la ejecución directa con muchas bases de datos es que la instrucción SQL se debe analizar y compilar cada vez que se ejecuta, lo que supone una sobrecarga si la instrucción se ejecuta varias veces.  
  
 En [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] se ha mejorado considerablemente el rendimiento de la ejecución directa en instrucciones ejecutadas habitualmente en entornos multiusuario, y el uso de SQLExecDirect con marcadores de parámetros para las instrucciones SQL ejecutadas habitualmente es prácticamente tan eficaz como el de la ejecución preparada.  
  
 Cuando se conecta a una instancia de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], el controlador ODBC de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client utiliza [sp_executesql](../../../relational-databases/system-stored-procedures/sp-executesql-transact-sql.md) para transmitir la instrucción SQL o el lote especificado en **SQLExecDirect**. [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] tiene lógica para determinar rápidamente si una instrucción SQL o un lote ejecutado con **sp_executesql** coincide con la instrucción o lote que generó un plan de ejecución que ya existe en la memoria. Si se encuentra una coincidencia, [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] simplemente reutiliza el plan existente en lugar de compilar un nuevo plan. Esto significa que las instrucciones SQL ejecutadas habitualmente con **SQLExecDirect** en un sistema con muchos usuarios se beneficiarán de muchas de las ventajas de la reutilización de planes que solo estaban disponibles para los procedimientos almacenados en versiones anteriores de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
 Esta ventaja de reutilización de los planes de ejecución solo funciona cuando varios usuarios ejecutan la misma instrucción o lote de instrucciones SQL. Siga estas convenciones de codificación para aumentar la probabilidad de que las instrucciones SQL ejecutadas por clientes diferentes sean lo suficientemente similares para poder reutilizar planes de ejecución:  
  
-   No incluya constantes de datos en las instrucciones SQL; utilice en su lugar marcadores de parámetros enlazados a variables del programa. Para obtener más información, vea [using Statement Parameters](../../../relational-databases/native-client-odbc-queries/using-statement-parameters.md).  
  
-   Utilice nombres de objeto completos. Los planes de ejecución no se reutilizan si los nombres de objeto no son completos.  
  
-   Haga que las conexiones de la aplicación utilicen siempre que sea posible un conjunto común de opciones de conexión e instrucción. Los planes de ejecución generados para una conexión con un conjunto de opciones (como ANSI_NULLS) no se reutilizan para una conexión que tiene otro conjunto de opciones. El proveedor ODBC de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client y el proveedor OLE DB de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client proporcionan la misma configuración predeterminada para estas opciones.  
  
 Si todas las instrucciones ejecutadas con **SQLExecDirect** se codifican utilizando estas convenciones, [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] pueden reutilizar los planes de ejecución cuando surja la oportunidad.  
  
## <a name="see-also"></a>Vea también  
 [Ejecutar instrucciones &#40;ODBC&#41;](../../../relational-databases/native-client-odbc-queries/executing-statements/executing-statements-odbc.md)  
  
  
