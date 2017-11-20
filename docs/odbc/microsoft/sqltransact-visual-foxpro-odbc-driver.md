---
title: SQLTransact (controlador ODBC de Visual FoxPro) | Documentos de Microsoft
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: microsoft
ms.reviewer: 
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- SQLTransact function [ODBC], Visual FoxPro ODBC Driver
ms.assetid: 92cf86c0-f7a8-44d7-b59f-a1342677440b
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 9b12fa480f4aef8b669bdd57c4322f8d9f736be6
ms.contentlocale: es-es
ms.lasthandoff: 09/09/2017

---
# <a name="sqltransact-visual-foxpro-odbc-driver"></a>SQLTransact (controlador ODBC de Visual FoxPro)
> [!NOTE]  
>  Este tema contiene información específica del controlador ODBC de Visual FoxPro. Para obtener información general acerca de esta función, vea el tema correspondiente en [referencia de la API de ODBC](../../odbc/reference/syntax/odbc-api-reference.md).  
  
 Soporte técnico: completo  
  
 Conformidad de la API de ODBC: Nivel de núcleo  
  
 Solicita una operación de confirmación o reversión para todas las operaciones activas en todos los identificadores de instrucción (*hstmt*s) asociado con una conexión o para todas las conexiones asociadas con el identificador de entorno, *henv*. **SQLTransact** solo funciona para los orígenes de datos que son [bases de datos](../../odbc/microsoft/visual-foxpro-terminology.md).  
  
 Si se produce un error en una confirmación en el modo manual, la transacción permanece activa; puede revertir la transacción o vuelva a intentar la operación de confirmación. Si se produce un error en una operación de confirmación cuando está en modo de transacción automática, la transacción se revierte automáticamente; la transacción no puede estar inactiva.  
  
 Para obtener más información, consulte [SQLTransact](../../odbc/reference/syntax/sqltransact-function.md) en el *referencia del programador de ODBC*.

