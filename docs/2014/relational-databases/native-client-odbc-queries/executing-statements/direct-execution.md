---
title: La ejecución directa | Documentos de Microsoft
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- ODBC applications, statements
- direct execution [ODBC]
- SQLExecDirect function
- statements [ODBC], direct execution
ms.assetid: fa36e1af-ed98-4abc-97c1-c4cc5d227b29
caps.latest.revision: 37
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: 4f594c8c7bb54faf62ce803cfb7af3bf12073f21
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36114024"
---
# <a name="direct-execution"></a>Ejecución directa
  La ejecución directa es la manera más sencilla de ejecutar una instrucción. Una aplicación compila una cadena de caracteres que contiene un [!INCLUDE[tsql](../../../includes/tsql-md.md)] instrucción y se envía para su ejecución con el **SQLExecDirect** función. Cuando la instrucción llega al servidor, [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] la compila en un plan de ejecución y ejecuta inmediatamente el plan de ejecución.  
  
 La ejecución directa se utiliza habitualmente en las aplicaciones que generan y ejecutan instrucciones en tiempo de ejecución y es el método más eficaz para las instrucciones que se van a ejecutar una sola vez. El inconveniente cuando se utiliza la ejecución directa con muchas bases de datos es que la instrucción SQL se debe analizar y compilar cada vez que se ejecuta, lo que supone una sobrecarga si la instrucción se ejecuta varias veces.  
  
 En [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] se ha mejorado considerablemente el rendimiento de la ejecución directa en instrucciones ejecutadas habitualmente en entornos multiusuario, y el uso de SQLExecDirect con marcadores de parámetros para las instrucciones SQL ejecutadas habitualmente es prácticamente tan eficaz como el de la ejecución preparada.  
  
 Cuando se conecta a una instancia de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] controlador ODBC de Native Client utiliza [sp_executesql](/sql/relational-databases/system-stored-procedures/sp-executesql-transact-sql) para transmitir la instrucción SQL o el lote especificado en **SQLExecDirect**. [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] tiene una lógica para determinar rápidamente si una instrucción SQL o el lote se ejecuta con **sp_executesql** coincide con la instrucción o lote que generó un plan de ejecución que ya existe en la memoria. Si se encuentra una coincidencia, [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] simplemente reutiliza el plan existente en lugar de compilar un nuevo plan. Esto significa que normalmente ejecuta instrucciones SQL ejecutadas con **SQLExecDirect** en un sistema con muchos usuarios se beneficiarán de muchas de las ventajas de reutilización de planes que sólo estaban disponibles para los procedimientos almacenados en las versiones anteriores de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
 Esta ventaja de reutilización de los planes de ejecución solo funciona cuando varios usuarios ejecutan la misma instrucción o lote de instrucciones SQL. Siga estas convenciones de codificación para aumentar la probabilidad de que las instrucciones SQL ejecutadas por clientes diferentes sean lo suficientemente similares para poder reutilizar planes de ejecución:  
  
-   No incluya constantes de datos en las instrucciones SQL; utilice en su lugar marcadores de parámetros enlazados a variables del programa. Para obtener más información, consulte [Using Statement Parameters](../using-statement-parameters.md).  
  
-   Utilice nombres de objeto completos. Los planes de ejecución no se reutilizan si los nombres de objeto no son completos.  
  
-   Haga que las conexiones de la aplicación utilicen siempre que sea posible un conjunto común de opciones de conexión e instrucción. Los planes de ejecución generados para una conexión con un conjunto de opciones (como ANSI_NULLS) no se reutilizan para una conexión que tiene otro conjunto de opciones. El proveedor ODBC de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client y el proveedor OLE DB de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client proporcionan la misma configuración predeterminada para estas opciones.  
  
 Si todas las instrucciones ejecutadas con **SQLExecDirect** se codifican mediante estas convenciones, [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] puede volver a utilizar planes de ejecución cuando surja la oportunidad.  
  
## <a name="see-also"></a>Vea también  
 [Ejecutar instrucciones &#40;ODBC&#41;](executing-statements-odbc.md)  
  
  
