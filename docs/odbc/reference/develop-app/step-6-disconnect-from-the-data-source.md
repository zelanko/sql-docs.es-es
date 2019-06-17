---
title: 'Paso 6: Desconectarse del origen de datos | Microsoft Docs'
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
manager: craigg
ms.openlocfilehash: a42465e763f8f6d520ed9c1dac42612aa1b28575
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "63149234"
---
# <a name="step-6-disconnect-from-the-data-source"></a>Paso 6: Desconexión del origen de datos
El último paso es desconectarse del origen de datos, como se muestra en la siguiente ilustración. En primer lugar, la aplicación libera los identificadores de instrucciones mediante una llamada a **SQLFreeHandle**. Para obtener más información, consulte [liberar un identificador de instrucciones](../../../odbc/reference/develop-app/freeing-a-statement-handle-odbc.md).  
  
 ![Muestra la desconexión de un origen de datos](../../../odbc/reference/develop-app/media/pr17.gif "pr17")  
  
 A continuación, la aplicación se desconecta del origen de datos con **SQLDisconnect** y libera el identificador de conexión con **SQLFreeHandle**. Para obtener más información, consulte [desconectarse de un origen de datos o un controlador](../../../odbc/reference/develop-app/disconnecting-from-a-data-source-or-driver.md).  
  
 Por último, la aplicación libera el identificador del entorno con **SQLFreeHandle** y descarga el Administrador de controladores. Para obtener más información, consulte [asignar el entorno de controlar](../../../odbc/reference/develop-app/allocating-the-environment-handle.md).
