---
title: Ejecución de instrucciones (ODBC) | Documentos de Microsoft
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.component: native-client-odbc-queries
ms.reviewer: ''
ms.suite: sql
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- SQL Server Native Client ODBC driver, statements
- statements [ODBC]
- ODBC applications, statements
- statements [ODBC], executing
ms.assetid: 063fc40d-ff81-490d-9c9b-2faefb729f37
caps.latest.revision: 33
author: MightyPen
ms.author: genemi
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 7521f18d4ac934bd05b6922f8e48bcb18d31a4c8
ms.sourcegitcommit: 2d93cd115f52bf3eff3069f28ea866232b4f9f9e
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/01/2018
ms.locfileid: "34707823"
---
# <a name="executing-statements-odbc"></a>Ejecutar instrucciones (ODBC)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../../includes/snac-deprecated.md)]

  El [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] controlador ODBC Native Client ofrece varios modos para ejecutar instrucciones SQL en un [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] base de datos:  
  
-   Ejecución directa  
  
-   Ejecución preparada  
  
 La ejecución directa implica crear una cadena de caracteres que contiene un [!INCLUDE[tsql](../../../includes/tsql-md.md)] instrucción y enviarlo para su ejecución con el **SQLExecDirect** función. La ejecución preparada implica la creación de una cadena de caracteres que contiene una instrucción [!INCLUDE[tsql](../../../includes/tsql-md.md)] y su posterior ejecución en dos fases. La primera fase se utiliza la [SQLPrepare Function](http://go.microsoft.com/fwlink/?LinkId=59360) función para analizar y compilar el plan de ejecución de la instrucción en el [!INCLUDE[ssDE](../../../includes/ssde-md.md)]. La segunda fase se utiliza la **SQLExecute** función que se ejecuta el plan de ejecución preparada previamente. De esta forma, se guarda la sobrecarga de análisis y compilación en cada ejecución. Las aplicaciones suelen usar la ejecución preparada para ejecutar repetidamente una misma instrucción SQL parametrizada.  
  
 Tanto en la ejecución directa como en la ejecución preparada puede ejecutarse una única instrucción de [!INCLUDE[tsql](../../../includes/tsql-md.md)] o un lote de instrucciones de SQL, o puede llamarse a un procedimiento almacenado.  
  
## <a name="in-this-section"></a>En esta sección  
  
-   [Ejecución directa](../../../relational-databases/native-client-odbc-queries/executing-statements/direct-execution.md)  
  
-   [Ejecución preparada](../../../relational-databases/native-client-odbc-queries/executing-statements/prepared-execution.md)  
  
-   [Procedimientos](../../../relational-databases/native-client-odbc-queries/executing-statements/procedures.md)  
  
-   [Lotes de instrucciones](../../../relational-databases/native-client-odbc-queries/executing-statements/batches-of-statements.md)  
  
-   [Efectos de las opciones ISO](../../../relational-databases/native-client-odbc-queries/executing-statements/effects-of-iso-options.md)  
  
## <a name="see-also"></a>Vea también  
 [Ejecutar consultas &#40;ODBC&#41;](../../../relational-databases/native-client-odbc-queries/executing-queries-odbc.md)  
  
  
