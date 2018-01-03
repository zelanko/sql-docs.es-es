---
title: "Paso 2: Iniciar la aplicación | Documentos de Microsoft"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: odbc
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- initializing applications [ODBC]
- application process [ODBC], initializing applications
ms.assetid: 23a7a230-ae2c-4a5e-9760-d2e17f92c389
caps.latest.revision: "8"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 64ef3dea2a8403af43cc03a3deeee47ff16dd2b6
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/21/2017
---
# <a name="step-2-initialize-the-application"></a>Paso 2: Iniciar la aplicación
El segundo paso es iniciar la aplicación, tal como se muestra en la siguiente ilustración. Exactamente lo que se realiza aquí varía en función de la aplicación.  
  
 ![Muestra la inicialización de una aplicación ODBC](../../../odbc/reference/develop-app/media/pr12.gif "pr12")  
  
 En este punto, es habitual usar **SQLGetInfo** para detectar las capacidades del controlador. Para obtener más información, consulte [características de base de datos teniendo en cuenta que se utilizan](../../../odbc/reference/develop-app/considering-database-features-to-use.md).  
  
 Todas las aplicaciones necesitan asignar un identificador de instrucción con **SQLAllocHandle**, y muchas aplicaciones establecen atributos de instrucción, como el tipo de cursor con **SQLSetStmtAttr**. Para obtener más información, consulte [asignar un identificador de instrucciones](../../../odbc/reference/develop-app/allocating-a-statement-handle-odbc.md) y [atributos de instrucción](../../../odbc/reference/develop-app/statement-attributes.md).
