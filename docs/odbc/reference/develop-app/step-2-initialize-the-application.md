---
description: 'Paso 2: Inicialización de la aplicación'
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 26d20a5b10ee7b414b9285a388359b3a93029f16
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/17/2020
ms.locfileid: "88482888"
---
# <a name="step-2-initialize-the-application"></a>Paso 2: Inicialización de la aplicación
El segundo paso consiste en inicializar la aplicación, tal como se muestra en la siguiente ilustración. Exactamente lo que se hace aquí varía en función de la aplicación.  
  
 ![Muestra cómo inicializar una aplicación ODBC](../../../odbc/reference/develop-app/media/pr12.gif "pr12")  
  
 En este punto, es habitual usar **SQLGetInfo** para detectar las capacidades del controlador. Para obtener más información, vea [considerar la posibilidad de usar las características de base de datos](../../../odbc/reference/develop-app/considering-database-features-to-use.md).  
  
 Todas las aplicaciones deben asignar un identificador de instrucción con **SQLAllocHandle**y muchas aplicaciones establecen atributos de instrucción, como el tipo de cursor, con **SQLSetStmtAttr**. Para obtener más información, vea [asignar un identificador de instrucción](../../../odbc/reference/develop-app/allocating-a-statement-handle-odbc.md) y [atributos de instrucción](../../../odbc/reference/develop-app/statement-attributes.md).
