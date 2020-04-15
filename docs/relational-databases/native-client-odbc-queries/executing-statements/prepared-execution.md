---
title: Ejecución Preparada ? Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- deferred statement preparation
- prepared execution [ODBC]
- SQLPrepare function
- ODBC applications, statements
- SQLExecute function
- statements [ODBC], prepared execution
ms.assetid: f3a9d32b-6cd7-4f0c-b38d-c8ccc4ee40c3
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 8265ed80028d5d8ac9696853a29474552f401f3e
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/14/2020
ms.locfileid: "81297925"
---
# <a name="prepared-execution"></a>Ejecución preparada
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  La API de ODBC define la ejecución preparada como una manera de reducir la sobrecarga de análisis y compilación asociada a la ejecución reiterativa de una instrucción [!INCLUDE[tsql](../../../includes/tsql-md.md)]. La aplicación genera una cadena de caracteres que contiene una instrucción SQL y, a continuación, la ejecuta en dos fases. Llama a [SQLPrepare Function](https://go.microsoft.com/fwlink/?LinkId=59360) una vez para que el [!INCLUDE[ssDE](../../../includes/ssde-md.md)]archivo . A continuación, llama a **SQLExecute** para cada ejecución del plan de ejecución preparado. De esta forma, se guarda la sobrecarga de análisis y compilación en cada ejecución. Las aplicaciones suelen usar la ejecución preparada para ejecutar repetidamente una misma instrucción SQL parametrizada.  
  
 Para la mayoría de las bases de datos, la ejecución preparada es más rápida que la ejecución directa de instrucciones que se ejecutan más de tres o cuatro veces, principalmente porque la instrucción se compila solo una vez, mientras que las instrucciones ejecutadas directamente se compilan cada vez que se ejecutan. La ejecución preparada también puede proporcionar una reducción del tráfico de red porque el controlador puede enviar un identificador de plan de ejecución y los valores de los parámetros, en lugar de una instrucción SQL completa, al origen de datos cada vez que se ejecuta la instrucción.  
  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]reduce la diferencia de rendimiento entre la ejecución directa y preparada a través de algoritmos mejorados para detectar y reutilizar planes de ejecución de **SQLExecDirect**. Estos algoritmos permiten disfrutar en las instrucciones que se ejecutan directamente de algunas de las ventajas de rendimiento de la ejecución preparada. Para obtener más información, consulte [Ejecución directa](../../../relational-databases/native-client-odbc-queries/executing-statements/direct-execution.md).  
  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] proporciona también compatibilidad nativa con la ejecución preparada. Un plan de ejecución se basa en **SQLPrepare** y se ejecuta más adelante cuando **SQLExecute** se llama. Dado [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] que no es necesario crear procedimientos almacenados temporales en **SQLPrepare**, no hay ninguna sobrecarga adicional en las tablas del sistema en **tempdb**.  
  
 Por motivos de rendimiento, la preparación de la instrucción se aplaza hasta que se llama a **SQLExecute** o se realiza una operación de metapropiedad (como [SQLDescribeCol](../../../relational-databases/native-client-odbc-api/sqldescribecol.md) o [SQLDescribeParam](../../../relational-databases/native-client-odbc-api/sqldescribeparam.md) en ODBC). Este es el comportamiento predeterminado. Cualquier error que se produzca en la instrucción que se está preparando no se dará a conocer hasta que la instrucción se ejecute o hasta que se realice una operación de metapropiedad. Si desea desactivar este comportamiento predeterminado, establezca el atributo de instrucción específico del controlador ODBC de Native Client de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] SQL_SOPT_SS_DEFER_PREPARE en SQL_DP_OFF.  
  
 En caso de preparación diferida, llamar a **SQLDescribeCol** o **SQLDescribeParam** antes de llamar a **SQLExecute** genera un ida y vuelta adicional al servidor. En **SQLDescribeCol**, el controlador quita la cláusula WHERE de la consulta y la envía al servidor con SET FMTONLY ON para obtener la descripción de las columnas del primer conjunto de resultados devuelto por la consulta. En **SQLDescribeParam**, el controlador llama al servidor para obtener una descripción de las expresiones o columnas a las que hace referencia los marcadores de parámetro de la consulta. Este método tiene también algunas restricciones, como la imposibilidad de resolver parámetros en subconsultas.  
  
 El uso excesivo de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] **SQLPrepare** con el controlador ODBC de Native Client degrada el rendimiento, especialmente cuando se conecta a versiones anteriores de SQL Server. La ejecución preparada no se debe utilizar para las instrucciones que se ejecutan una sola vez. La ejecución preparada es más lenta que la ejecución directa para una ejecución única de una instrucción porque requiere un ciclo de ida y vuelta de red adicional del cliente al servidor. En las versiones anteriores de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] genera además un procedimiento almacenado temporal.  
  
 Las instrucciones preparadas no se pueden utilizar para crear objetos temporales en [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
 Algunas aplicaciones ODBC tempranas usaban **SQLPrepare** cada vez que se usaba [SQLBindParameter.](../../../relational-databases/native-client-odbc-api/sqlbindparameter.md) **SQLBindParameter** no requiere el uso de **SQLPrepare**, se puede utilizar con **SQLExecDirect**. Por ejemplo, utilice **SQLExecDirect** con **SQLBindParameter** para recuperar el código de retorno o los parámetros de salida de un procedimiento almacenado que solo se ejecuta una vez. No utilice **SQLPrepare** con **SQLBindParameter** a menos que la misma instrucción se ejecute varias veces.  
  
## <a name="see-also"></a>Consulte también  
 [Ejecución de instrucciones &#40;&#41;ODBC](../../../relational-databases/native-client-odbc-queries/executing-statements/executing-statements-odbc.md)  
  
  
