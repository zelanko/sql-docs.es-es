---
title: "La ejecución preparada | Documentos de Microsoft"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: native-client-odbc-queries
ms.reviewer: 
ms.suite: sql
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: reference
helpviewer_keywords:
- deferred statement preparation
- prepared execution [ODBC]
- SQLPrepare function
- ODBC applications, statements
- SQLExecute function
- statements [ODBC], prepared execution
ms.assetid: f3a9d32b-6cd7-4f0c-b38d-c8ccc4ee40c3
caps.latest.revision: 
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: cedfb3926904af0a9d7393a1ff896c3c2f08a61f
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 01/25/2018
---
# <a name="prepared-execution"></a>Ejecución preparada
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../../includes/snac-deprecated.md)]

  La API de ODBC define la ejecución preparada como una manera de reducir la sobrecarga de análisis y compilación asociada a la ejecución reiterativa de una instrucción [!INCLUDE[tsql](../../../includes/tsql-md.md)]. La aplicación genera una cadena de caracteres que contiene una instrucción SQL y, a continuación, la ejecuta en dos fases. Llama [SQLPrepare Function](http://go.microsoft.com/fwlink/?LinkId=59360) una vez que la instrucción analizará y compilará en un plan de ejecución el [!INCLUDE[ssDE](../../../includes/ssde-md.md)]. A continuación, se llama **SQLExecute** para cada ejecución del plan de ejecución preparada. De esta forma, se guarda la sobrecarga de análisis y compilación en cada ejecución. Las aplicaciones suelen usar la ejecución preparada para ejecutar repetidamente una misma instrucción SQL parametrizada.  
  
 Para la mayoría de las bases de datos, la ejecución preparada es más rápida que la ejecución directa de instrucciones que se ejecutan más de tres o cuatro veces, principalmente porque la instrucción se compila solo una vez, mientras que las instrucciones ejecutadas directamente se compilan cada vez que se ejecutan. La ejecución preparada también puede proporcionar una reducción del tráfico de red porque el controlador puede enviar un identificador de plan de ejecución y los valores de los parámetros, en lugar de una instrucción SQL completa, al origen de datos cada vez que se ejecuta la instrucción.  
  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]reduce la diferencia de rendimiento entre la ejecución directa y preparada a través de algoritmos mejorados para la detección y reutilización de planes de ejecución de **SQLExecDirect**. Estos algoritmos permiten disfrutar en las instrucciones que se ejecutan directamente de algunas de las ventajas de rendimiento de la ejecución preparada. Para obtener más información, consulte [la ejecución directa](../../../relational-databases/native-client-odbc-queries/executing-statements/direct-execution.md).  
  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] proporciona también compatibilidad nativa con la ejecución preparada. Un plan de ejecución se basa en **SQLPrepare** y después se ejecutan al **SQLExecute** se llama. Dado que [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] no es necesario generar procedimientos almacenados temporales **SQLPrepare**, no hay ninguna sobrecarga adicional en las tablas del sistema en **tempdb**.  
  
 Por motivos de rendimiento, la preparación de instrucciones se difiere hasta que **SQLExecute** se llama o una operación de metapropiedad (como [SQLDescribeCol](../../../relational-databases/native-client-odbc-api/sqldescribecol.md) o [SQLDescribeParam](../../../relational-databases/native-client-odbc-api/sqldescribeparam.md) en ODBC) se lleva a cabo. Éste es el comportamiento predeterminado. Cualquier error que se produzca en la instrucción que se está preparando no se dará a conocer hasta que la instrucción se ejecute o hasta que se realice una operación de metapropiedad. Si desea desactivar este comportamiento predeterminado, establezca el atributo de instrucción específico del controlador ODBC de Native Client de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] SQL_SOPT_SS_DEFER_PREPARE en SQL_DP_OFF.  
  
 En caso de diferidas preparar, una llamada a **SQLDescribeCol** o **SQLDescribeParam** antes de llamar a **SQLExecute** genera un adicional de ida y vuelta al servidor. En **SQLDescribeCol**, el controlador se quita la cláusula WHERE de la consulta y lo envía al servidor con SET FMTONLY ON para obtener la descripción de las columnas en el primer conjunto de resultados devuelto por la consulta. En **SQLDescribeParam**, el controlador llama al servidor para obtener una descripción de las expresiones o columnas de referencia por los marcadores de parámetros en la consulta. Este método tiene también algunas restricciones, como la imposibilidad de resolver parámetros en subconsultas.  
  
 El uso excesivo de **SQLPrepare** con el [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] controlador ODBC Native Client degrada el rendimiento, especialmente cuando se conecta a versiones anteriores de SQL Server. La ejecución preparada no se debe utilizar para las instrucciones que se ejecutan una sola vez. La ejecución preparada es más lenta que la ejecución directa para una ejecución única de una instrucción porque requiere un ciclo de ida y vuelta de red adicional del cliente al servidor. En las versiones anteriores de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] genera además un procedimiento almacenado temporal.  
  
 Las instrucciones preparadas no se pueden utilizar para crear objetos temporales en [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
 Algunas aplicaciones ODBC anteriores utilizados **SQLPrepare** cualquier momento [SQLBindParameter](../../../relational-databases/native-client-odbc-api/sqlbindparameter.md) se utilizó. **SQLBindParameter** no requiere el uso de **SQLPrepare**, se puede utilizar con **SQLExecDirect**. Por ejemplo, utilice **SQLExecDirect** con **SQLBindParameter** para recuperar el código de retorno o parámetros de salida de un procedimiento almacenado que se ejecuta solo una vez. No utilice **SQLPrepare** con **SQLBindParameter** a menos que la misma instrucción se ejecutará varias veces.  
  
## <a name="see-also"></a>Vea también  
 [Ejecutar instrucciones &#40; ODBC &#41;](../../../relational-databases/native-client-odbc-queries/executing-statements/executing-statements-odbc.md)  
  
  
