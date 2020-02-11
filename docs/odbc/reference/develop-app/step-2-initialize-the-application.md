---
title: 'Paso 2: inicializar la aplicación | Microsoft Docs'
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
ms.openlocfilehash: 41030015645bda11242a703a163f26104e66dba0
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "68114249"
---
# <a name="step-2-initialize-the-application"></a>Paso 2: Iniciar la aplicación
El segundo paso consiste en inicializar la aplicación, tal como se muestra en la siguiente ilustración. Exactamente lo que se hace aquí varía en función de la aplicación.  
  
 ![Muestra cómo inicializar una aplicación ODBC](../../../odbc/reference/develop-app/media/pr12.gif "pr12")  
  
 En este punto, es habitual usar **SQLGetInfo** para detectar las capacidades del controlador. Para obtener más información, vea [considerar la posibilidad de usar las características de base de datos](../../../odbc/reference/develop-app/considering-database-features-to-use.md).  
  
 Todas las aplicaciones deben asignar un identificador de instrucción con **SQLAllocHandle**y muchas aplicaciones establecen atributos de instrucción, como el tipo de cursor, con **SQLSetStmtAttr**. Para obtener más información, vea [asignar un identificador de instrucción](../../../odbc/reference/develop-app/allocating-a-statement-handle-odbc.md) y [atributos de instrucción](../../../odbc/reference/develop-app/statement-attributes.md).
