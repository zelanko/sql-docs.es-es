---
title: SQLGetData y cursores de bloque | Microsoft Docs
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
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/27/2020
ms.locfileid: "81299755"
---
# <a name="sqlgetdata-and-block-cursors"></a>SQLGetData y cursores de bloque
**SQLGetData** funciona en una sola columna de una sola fila y no puede capturar una matriz que contenga datos de varias filas. Esto se debe a que el uso principal de **SQLGetData** es capturar datos de gran tamaño en partes y hay poca o ninguna razón para hacerlo para más de una fila a la vez.  
  
 Para usar **SQLGetData** con un cursor de bloque, una aplicación llama primero a **SQLSetPos** para colocar el cursor en una sola fila. A continuación, llama a **SQLGetData** para una columna de esa fila. Sin embargo, este comportamiento es opcional. Para determinar si un controlador admite el uso de **SQLGetData** con cursores de bloque, una aplicación llama a **SQLGetInfo** con la opción SQL_GETDATA_EXTENSIONS.
