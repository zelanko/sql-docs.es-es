---
title: Ejecutar instrucciones (ODBC) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- SQL Server Native Client ODBC driver, statements
- statements [ODBC]
- ODBC applications, statements
- statements [ODBC], executing
ms.assetid: 063fc40d-ff81-490d-9c9b-2faefb729f37
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: a367d5ee7def19ffdfd40e24860ebf95f642fae9
ms.sourcegitcommit: b72c9fc9436c44c6a21fd96223c73bf94706c06b
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/01/2020
ms.locfileid: "82700427"
---
# <a name="executing-statements-odbc"></a>Ejecutar instrucciones (ODBC)
  El [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] controlador ODBC de Native Client ofrece varias maneras de ejecutar instrucciones SQL en una [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] base de datos:  
  
-   Ejecución directa  
  
-   Ejecución preparada  
  
 La ejecución directa implica la creación de una cadena de caracteres que contiene una [!INCLUDE[tsql](../../../includes/tsql-md.md)] instrucción y su envío para su ejecución mediante la función **SQLExecDirect** . La ejecución preparada implica la creación de una cadena de caracteres que contiene una instrucción [!INCLUDE[tsql](../../../includes/tsql-md.md)] y su posterior ejecución en dos fases. En la primera fase se usa la función de [función SQLPrepare](https://go.microsoft.com/fwlink/?LinkId=59360) para analizar y compilar el plan de ejecución de la instrucción en [!INCLUDE[ssDE](../../../includes/ssde-md.md)] . En la segunda fase se usa la función **SQLExecute** para ejecutar el plan de ejecución previamente preparado. De esta forma, se guarda la sobrecarga de análisis y compilación en cada ejecución. Las aplicaciones suelen usar la ejecución preparada para ejecutar repetidamente una misma instrucción SQL parametrizada.  
  
 Tanto en la ejecución directa como en la ejecución preparada puede ejecutarse una única instrucción de [!INCLUDE[tsql](../../../includes/tsql-md.md)] o un lote de instrucciones de SQL, o puede llamarse a un procedimiento almacenado.  
  
## <a name="in-this-section"></a>En esta sección  
  
-   [Ejecución directa](direct-execution.md)  
  
-   [Ejecución preparada](prepared-execution.md)  
  
-   [Procedimientos](procedures.md)  
  
-   [Lotes de instrucciones](batches-of-statements.md)  
  
-   [Efectos de las opciones ISO](effects-of-iso-options.md)  
  
## <a name="see-also"></a>Consulte también  
 [Ejecutar consultas &#40;&#41;ODBC](../executing-queries-odbc.md)  
  
  
