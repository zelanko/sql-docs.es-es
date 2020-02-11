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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 4841d8d923ff73d187569df3d7f9e29daf0f4e48
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "68107398"
---
# <a name="sqlgetdata-and-block-cursors"></a>SQLGetData y cursores de bloque
**SQLGetData** funciona en una sola columna de una sola fila y no puede capturar una matriz que contenga datos de varias filas. Esto se debe a que el uso principal de **SQLGetData** es capturar datos de gran tamaño en partes y hay poca o ninguna razón para hacerlo para más de una fila a la vez.  
  
 Para usar **SQLGetData** con un cursor de bloque, una aplicación llama primero a **SQLSetPos** para colocar el cursor en una sola fila. A continuación, llama a **SQLGetData** para una columna de esa fila. Sin embargo, este comportamiento es opcional. Para determinar si un controlador admite el uso de **SQLGetData** con cursores de bloque, una aplicación llama a **SQLGetInfo** con la opción SQL_GETDATA_EXTENSIONS.
