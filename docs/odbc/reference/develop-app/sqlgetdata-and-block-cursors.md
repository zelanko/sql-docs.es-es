---
title: SQLGetData y cursores de bloque | Documentos de Microsoft
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: odbc
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- cursors [ODBC], block
- SQLGetData function [ODBC], block cursors
- block cursors [ODBC]
- result sets [ODBC], block cursors
ms.assetid: 12599cdc-7725-4faf-bcae-e163ea0f5851
caps.latest.revision: "5"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 12b3c2dc5693f141f24b9209a12923b18a9859e5
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/21/2017
---
# <a name="sqlgetdata-and-block-cursors"></a>SQLGetData y cursores de bloque
**SQLGetData** funciona en una sola columna de una sola fila y no se puede encontrar una matriz que contiene los datos de varias filas. Esto es porque el uso principal de **SQLGetData** consiste en capturar datos largos en partes, y hay poca o ninguna razón para hacerlo para más de una fila a la vez.  
  
 Usar **SQLGetData** con un cursor de bloque, una aplicación llama primero **SQLSetPos** para colocar el cursor en una sola fila. A continuación, se llama **SQLGetData** para una columna de esa fila. Sin embargo, este comportamiento es opcional. Para determinar si un controlador es compatible con el uso de **SQLGetData** con cursores de bloque, llama a una aplicación **SQLGetInfo** con la opción SQL_GETDATA_EXTENSIONS.
