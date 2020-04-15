---
title: SQLGetData y los cursores de bloques de sqlgetdata Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- cursors [ODBC], block
- SQLGetData function [ODBC], block cursors
- block cursors [ODBC]
- result sets [ODBC], block cursors
ms.assetid: 12599cdc-7725-4faf-bcae-e163ea0f5851
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: b60d7093552b8f1dbed87d9ad8840ddb5a9e0799
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/14/2020
ms.locfileid: "81299755"
---
# <a name="sqlgetdata-and-block-cursors"></a>SQLGetData y cursores de bloque
**SQLGetData** funciona en una sola columna de una sola fila y no puede capturar una matriz que contenga datos de varias filas. Esto se debe a que el uso principal de **SQLGetData** es capturar datos largos en partes y hay pocas o ninguna razón para hacerlo durante más de una fila a la vez.  
  
 Para usar **SQLGetData** con un cursor de bloque, una aplicación llama primero **SQLSetPos** para colocar el cursor en una sola fila. A continuación, llama a **SQLGetData** para una columna de esa fila. Sin embargo, este comportamiento es opcional. Para determinar si un controlador admite el uso de **SQLGetData** con cursores de bloque, una aplicación llama a **SQLGetInfo** con la opción SQL_GETDATA_EXTENSIONS.
