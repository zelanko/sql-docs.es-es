---
title: 'Paso 2: Inicializar la aplicación ? Microsoft Docs'
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 843155ba6b641ea26717e63af55c8774f963a800
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/14/2020
ms.locfileid: "81288271"
---
# <a name="step-2-initialize-the-application"></a>Paso 2: Inicialización de la aplicación
El segundo paso es inicializar la aplicación, como se muestra en la siguiente ilustración. Exactamente lo que se hace aquí varía con la aplicación.  
  
 ![Muestra cómo inicializar una aplicación ODBC](../../../odbc/reference/develop-app/media/pr12.gif "pr12")  
  
 En este punto, es común usar **SQLGetInfo** para detectar las capacidades del controlador. Para obtener más información, consulte [Consideración de](../../../odbc/reference/develop-app/considering-database-features-to-use.md)las características de base de datos que se usan .  
  
 Todas las aplicaciones deben asignar un identificador de instrucción con **SQLAllocHandle**y muchas aplicaciones establecen atributos de instrucción, como el tipo de cursor, con **SQLSetStmtAttr**. Para obtener más información, vea Asignación de un identificador de [instrucción](../../../odbc/reference/develop-app/allocating-a-statement-handle-odbc.md) y atributos de [instrucción](../../../odbc/reference/develop-app/statement-attributes.md).
