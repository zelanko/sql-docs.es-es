---
title: 'Paso 2: Iniciar la aplicación | Documentos de Microsoft'
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- initializing applications [ODBC]
- application process [ODBC], initializing applications
ms.assetid: 23a7a230-ae2c-4a5e-9760-d2e17f92c389
caps.latest.revision: 8
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 85dff871a4b81551c699acc934aedb14c4f1725f
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="step-2-initialize-the-application"></a>Paso 2: Iniciar la aplicación
El segundo paso es iniciar la aplicación, tal como se muestra en la siguiente ilustración. Exactamente lo que se realiza aquí varía en función de la aplicación.  
  
 ![Muestra la inicialización de una aplicación ODBC](../../../odbc/reference/develop-app/media/pr12.gif "pr12")  
  
 En este punto, es habitual usar **SQLGetInfo** para detectar las capacidades del controlador. Para obtener más información, consulte [características de base de datos teniendo en cuenta que se utilizan](../../../odbc/reference/develop-app/considering-database-features-to-use.md).  
  
 Todas las aplicaciones necesitan asignar un identificador de instrucción con **SQLAllocHandle**, y muchas aplicaciones establecen atributos de instrucción, como el tipo de cursor con **SQLSetStmtAttr**. Para obtener más información, consulte [asignar un identificador de instrucciones](../../../odbc/reference/develop-app/allocating-a-statement-handle-odbc.md) y [atributos de instrucción](../../../odbc/reference/develop-app/statement-attributes.md).
