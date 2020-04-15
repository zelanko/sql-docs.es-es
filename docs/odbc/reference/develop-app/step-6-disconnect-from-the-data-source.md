---
title: 'Paso 6: Desconectarse de la fuente de datos ? Microsoft Docs'
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: df8cd94435d74bf813b0b64be0753a0beb44d354
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/14/2020
ms.locfileid: "81302796"
---
# <a name="step-6-disconnect-from-the-data-source"></a>Paso 6: Desconexión del origen de datos
El último paso es desconectarse del origen de datos, como se muestra en la siguiente ilustración. En primer lugar, la aplicación libera cualquier identificador de instrucción mediante una llamada a **SQLFreeHandle**. Para obtener más información, consulte [Liberación de un identificador](../../../odbc/reference/develop-app/freeing-a-statement-handle-odbc.md)de instrucción .  
  
 ![Muestra la desconexión de un origen de datos](../../../odbc/reference/develop-app/media/pr17.gif "pr17")  
  
 A continuación, la aplicación se desconecta del origen de datos con **SQLDisconnect** y libera el identificador de conexión con **SQLFreeHandle**. Para obtener más información, consulte [Desconectarse de un origen](../../../odbc/reference/develop-app/disconnecting-from-a-data-source-or-driver.md)de datos o controlador .  
  
 Por último, la aplicación libera el identificador de entorno con **SQLFreeHandle** y descarga el Administrador de controladores. Para obtener más información, consulte [Asignación del controlador](../../../odbc/reference/develop-app/allocating-the-environment-handle.md)de entorno .
