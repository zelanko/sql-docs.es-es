---
title: 'Paso 2: Iniciar la aplicación | Microsoft Docs'
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- initializing applications [ODBC]
- application process [ODBC], initializing applications
ms.assetid: 23a7a230-ae2c-4a5e-9760-d2e17f92c389
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: b0d25173dc8dc14aa1ed41a4a88496ef654e2ff0
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/01/2018
ms.locfileid: "47850934"
---
# <a name="step-2-initialize-the-application"></a>Paso 2: Iniciar la aplicación
El segundo paso es inicializar la aplicación, tal como se muestra en la siguiente ilustración. Exactamente lo que se realiza aquí varía en función de la aplicación.  
  
 ![Muestra la inicialización de una aplicación ODBC](../../../odbc/reference/develop-app/media/pr12.gif "pr12")  
  
 En este momento, es habitual usar **SQLGetInfo** para detectar las capacidades del controlador. Para obtener más información, consulte [teniendo en cuenta las características de base de datos que se usarán](../../../odbc/reference/develop-app/considering-database-features-to-use.md).  
  
 Todas las aplicaciones que necesitan asignar un identificador de instrucción con **SQLAllocHandle**, y muchas aplicaciones establecen atributos de instrucción, como el tipo de cursor con **SQLSetStmtAttr**. Para obtener más información, consulte [asignar un identificador de instrucciones](../../../odbc/reference/develop-app/allocating-a-statement-handle-odbc.md) y [atributos de instrucción](../../../odbc/reference/develop-app/statement-attributes.md).
