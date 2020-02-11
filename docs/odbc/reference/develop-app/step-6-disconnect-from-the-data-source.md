---
title: 'Paso 6: desconexión del origen de datos | Microsoft Docs'
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- application process [ODBC], disconnecting from data source
- data sources [ODBC], disconnecting
- disconnecting from data source [ODBC]
ms.assetid: 6ad759ba-4721-4d8f-9b26-de976d4fc1a0
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 65cc2ae8d2c2248a733e6efa9537fd3b40bb8fd1
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "68114123"
---
# <a name="step-6-disconnect-from-the-data-source"></a>Paso 6: Desconectar del origen de datos
El paso final consiste en desconectarse del origen de datos, tal y como se muestra en la siguiente ilustración. En primer lugar, la aplicación libera los identificadores de instrucción llamando a **SQLFreeHandle**. Para obtener más información, vea [liberar un identificador de instrucción](../../../odbc/reference/develop-app/freeing-a-statement-handle-odbc.md).  
  
 ![Muestra la desconexión de un origen de datos](../../../odbc/reference/develop-app/media/pr17.gif "pr17")  
  
 A continuación, la aplicación se desconecta del origen de datos con **SQLDisconnect** y libera el identificador de conexión con **SQLFreeHandle**. Para obtener más información, consulte [desconectar de un origen de datos o un controlador](../../../odbc/reference/develop-app/disconnecting-from-a-data-source-or-driver.md).  
  
 Por último, la aplicación libera el identificador del entorno con **SQLFreeHandle** y descarga el administrador de controladores. Para obtener más información, consulte [asignar el identificador de entorno](../../../odbc/reference/develop-app/allocating-the-environment-handle.md).
