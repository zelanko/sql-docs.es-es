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
manager: craigg
ms.openlocfilehash: a14c98f045fd974b404209cc998496dc5fa7193e
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "63149069"
---
# <a name="sqlgetdata-and-block-cursors"></a>SQLGetData y cursores de bloque
**SQLGetData** opera en una sola columna de una sola fila y no se puede capturar una matriz que contiene los datos de varias filas. Esto es porque el uso principal de **SQLGetData** consiste en capturar datos largos en partes, y hay poca o ninguna razón para hacer esto más de una fila a la vez.  
  
 Para usar **SQLGetData** con un cursor de bloque, una aplicación llama primero **SQLSetPos** para colocar el cursor en una sola fila. A continuación, llama **SQLGetData** para una columna de esa fila. Sin embargo, este comportamiento es opcional. Para determinar si un controlador admite el uso de **SQLGetData** con cursores de bloque, una aplicación llama a **SQLGetInfo** con la opción SQL_GETDATA_EXTENSIONS.
