---
title: SQLSetScrollOptions (controlador ODBC de Visual FoxPro) | Documentos de Microsoft
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: odbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- SQLSetScrollOptions function [ODBC], Visual FoxPro ODBC Driver
ms.assetid: 693e6e28-a845-41b1-9622-5058b0d87229
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 22b92ffb804ee7f325367c46a7d78b17c8604d94
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="sqlsetscrolloptions-visual-foxpro-odbc-driver"></a>SQLSetScrollOptions (controlador ODBC de Visual FoxPro)
> [!NOTE]  
>  Este tema contiene información específica del controlador ODBC de Visual FoxPro. Para obtener información general acerca de esta función, vea el tema correspondiente en [referencia de la API de ODBC](../../odbc/reference/syntax/odbc-api-reference.md).  
  
 Soporte técnico: parcial  
  
 Conformidad de la API de ODBC: 2 de nivel  
  
 Establece las opciones que controlan el comportamiento de los cursores asociado con un identificador de instrucción, *hstmt*.  
  
 El controlador ODBC de Visual FoxPro admite solo SQL_CONCUR_READ_ONLY; no admite la *fConcurrency* SQL_CONCUR_ROWVER de valor. El controlador convierte SQL_KEYSET_SIZE, SQL_CURSOR_DYNAMIC y SQL_CURSOR_KEYSET_DRIVEN a SQL_SCROLL_STATIC advertencia ODBC_01S02.  
  
 Para obtener más información, consulte [SQLSetScrollOptions](../../odbc/reference/syntax/sqlsetscrolloptions-function.md) en el *referencia del programador de ODBC*.
