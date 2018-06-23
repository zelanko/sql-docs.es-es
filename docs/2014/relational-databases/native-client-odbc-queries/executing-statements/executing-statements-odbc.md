---
title: Ejecución de instrucciones (ODBC) | Documentos de Microsoft
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
- SQL Server Native Client ODBC driver, statements
- statements [ODBC]
- ODBC applications, statements
- statements [ODBC], executing
ms.assetid: 063fc40d-ff81-490d-9c9b-2faefb729f37
caps.latest.revision: 32
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: ff5f9dcc3d8087418e3003dedc7f57e56840cba0
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36197918"
---
# <a name="executing-statements-odbc"></a>Ejecutar instrucciones (ODBC)
  El [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] controlador ODBC Native Client ofrece varios modos para ejecutar instrucciones SQL en un [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] base de datos:  
  
-   Ejecución directa  
  
-   Ejecución preparada  
  
 La ejecución directa implica crear una cadena de caracteres que contiene un [!INCLUDE[tsql](../../../includes/tsql-md.md)] instrucción y enviarlo para su ejecución con el **SQLExecDirect** función. La ejecución preparada implica la creación de una cadena de caracteres que contiene una instrucción [!INCLUDE[tsql](../../../includes/tsql-md.md)] y su posterior ejecución en dos fases. La primera fase se utiliza la [SQLPrepare Function](http://go.microsoft.com/fwlink/?LinkId=59360) función para analizar y compilar el plan de ejecución de la instrucción en el [!INCLUDE[ssDE](../../../includes/ssde-md.md)]. La segunda fase se utiliza la **SQLExecute** función que se ejecuta el plan de ejecución preparada previamente. De esta forma, se guarda la sobrecarga de análisis y compilación en cada ejecución. Las aplicaciones suelen usar la ejecución preparada para ejecutar repetidamente una misma instrucción SQL parametrizada.  
  
 Tanto en la ejecución directa como en la ejecución preparada puede ejecutarse una única instrucción de [!INCLUDE[tsql](../../../includes/tsql-md.md)] o un lote de instrucciones de SQL, o puede llamarse a un procedimiento almacenado.  
  
## <a name="in-this-section"></a>En esta sección  
  
-   [Ejecución directa](direct-execution.md)  
  
-   [Ejecución preparada](prepared-execution.md)  
  
-   [Procedimientos](procedures.md)  
  
-   [Lotes de instrucciones](batches-of-statements.md)  
  
-   [Efectos de las opciones ISO](effects-of-iso-options.md)  
  
## <a name="see-also"></a>Vea también  
 [Ejecutar consultas &#40;ODBC&#41;](../executing-queries-odbc.md)  
  
  