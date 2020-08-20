---
description: Ejecutar instrucciones (ODBC)
title: Ejecutar instrucciones (ODBC) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- SQL Server Native Client ODBC driver, statements
- statements [ODBC]
- ODBC applications, statements
- statements [ODBC], executing
ms.assetid: 063fc40d-ff81-490d-9c9b-2faefb729f37
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 45ac4b91f5aab26d1086bcc8e3b31c11821f75da
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/17/2020
ms.locfileid: "88486849"
---
# <a name="executing-statements-odbc"></a>Ejecutar instrucciones (ODBC)
[!INCLUDE [SQL Server](../../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

  El [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] controlador ODBC de Native Client ofrece varias maneras de ejecutar instrucciones SQL en una [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] base de datos:  
  
-   Ejecución directa  
  
-   Ejecución preparada  
  
 La ejecución directa implica la creación de una cadena de caracteres que contiene una [!INCLUDE[tsql](../../../includes/tsql-md.md)] instrucción y su envío para su ejecución mediante la función **SQLExecDirect** . La ejecución preparada implica la creación de una cadena de caracteres que contiene una instrucción [!INCLUDE[tsql](../../../includes/tsql-md.md)] y su posterior ejecución en dos fases. En la primera fase se usa la función de [función SQLPrepare](https://go.microsoft.com/fwlink/?LinkId=59360) para analizar y compilar el plan de ejecución de la instrucción en [!INCLUDE[ssDE](../../../includes/ssde-md.md)] . En la segunda fase se usa la función **SQLExecute** para ejecutar el plan de ejecución previamente preparado. De esta forma, se guarda la sobrecarga de análisis y compilación en cada ejecución. Las aplicaciones suelen usar la ejecución preparada para ejecutar repetidamente una misma instrucción SQL parametrizada.  
  
 Tanto en la ejecución directa como en la ejecución preparada puede ejecutarse una única instrucción de [!INCLUDE[tsql](../../../includes/tsql-md.md)] o un lote de instrucciones de SQL, o puede llamarse a un procedimiento almacenado.  
  
## <a name="in-this-section"></a>En esta sección  
  
-   [Ejecución directa](../../../relational-databases/native-client-odbc-queries/executing-statements/direct-execution.md)  
  
-   [Ejecución preparada](../../../relational-databases/native-client-odbc-queries/executing-statements/prepared-execution.md)  
  
-   [Procedimientos](../../../relational-databases/native-client-odbc-queries/executing-statements/procedures.md)  
  
-   [Lotes de instrucciones](../../../relational-databases/native-client-odbc-queries/executing-statements/batches-of-statements.md)  
  
-   [Efectos de las opciones ISO](../../../relational-databases/native-client-odbc-queries/executing-statements/effects-of-iso-options.md)  
  
## <a name="see-also"></a>Consulte también  
 [Ejecutar consultas &#40;&#41;ODBC ](../../../relational-databases/native-client-odbc-queries/executing-queries-odbc.md)  
  
  
