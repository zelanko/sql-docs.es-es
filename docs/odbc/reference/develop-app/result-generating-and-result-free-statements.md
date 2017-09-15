---
title: Las instrucciones generan resultados y liberar resultado | Documentos de Microsoft
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- result-generating statements [ODBC]
- batches [ODBC], result-generating statements
- batches [ODBC], result-free statements
- SQL statements [ODBC], batches
- result-free statements [ODBC]
ms.assetid: 2f3475d1-3999-4dd8-aba2-a6e1299c95f8
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: a99ea01cbd5a00ea4aa12e4b1461ca7f1ce9afa5
ms.contentlocale: es-es
ms.lasthandoff: 09/09/2017

---
# <a name="result-generating-and-result-free-statements"></a>Instrucciones generan resultados y libre de resultado
Instrucciones SQL pueden dividirse flexible en las cinco categorías siguientes:  
  
-   **Como resultado la generación de conjunto de instrucciones** se trata de instrucciones SQL que generan un conjunto de resultados. Por ejemplo, un **seleccione** instrucción.  
  
-   **Instrucciones de generación de recuento de filas** se trata de instrucciones SQL que generan un recuento de filas afectadas. Por ejemplo, un **actualización** o **eliminar** instrucción.  
  
-   **Las instrucciones de lenguaje de definición (DDL) de datos** se trata de instrucciones SQL que modifican la estructura de la base de datos. Por ejemplo, **CREATE TABLE** o **DROP INDEX**.  
  
-   **Instrucciones de cambio de contexto** se trata de instrucciones SQL que cambian el contexto de una base de datos. Por ejemplo, el **USE** y **establecer** las instrucciones de SQL Server.  
  
-   **Instrucciones administrativas** se trata de instrucciones SQL usadas para fines administrativos en una base de datos. Por ejemplo, **GRANT** y **REVOCAR**.  
  
 Instrucciones SQL en las primeras dos categorías se conocen colectivamente como *instrucciones generan resultados*. Instrucciones SQL en las tres últimas categorías se conocen colectivamente como *libre de resultado instrucciones*. ODBC define la semántica de lotes que incluyen instrucciones sólo genera resultados. Estas semánticas varían en gran medida y, por tanto, son específicos del origen de datos. Por ejemplo, el controlador de SQL Server no admite la eliminación de un objeto y, a continuación, hacer referencia a o volver a crear el mismo objeto en el mismo lote. Por lo tanto, el término *lote* tal y como se usan en este manual se refiere sólo a los lotes de la generación de resultados las instrucciones.
