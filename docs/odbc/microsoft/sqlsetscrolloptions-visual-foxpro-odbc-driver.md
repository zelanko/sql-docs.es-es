---
title: SQLSetScrollOptions (controlador ODBC de Visual FoxPro) | Documentos de Microsoft
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- SQLSetScrollOptions function [ODBC], Visual FoxPro ODBC Driver
ms.assetid: 693e6e28-a845-41b1-9622-5058b0d87229
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 81542e2e2187872725bd4db5f5922dbbefb2f944
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
ms.locfileid: "32901880"
---
# <a name="sqlsetscrolloptions-visual-foxpro-odbc-driver"></a>SQLSetScrollOptions (controlador ODBC de Visual FoxPro)
> [!NOTE]  
>  Este tema contiene información específica del controlador ODBC de Visual FoxPro. Para obtener información general acerca de esta función, vea el tema correspondiente en [referencia de la API de ODBC](../../odbc/reference/syntax/odbc-api-reference.md).  
  
 Soporte técnico: parcial  
  
 Conformidad de la API de ODBC: 2 de nivel  
  
 Establece las opciones que controlan el comportamiento de los cursores asociado con un identificador de instrucción, *hstmt*.  
  
 El controlador ODBC de Visual FoxPro admite solo SQL_CONCUR_READ_ONLY; no admite la *fConcurrency* SQL_CONCUR_ROWVER de valor. El controlador convierte SQL_KEYSET_SIZE, SQL_CURSOR_DYNAMIC y SQL_CURSOR_KEYSET_DRIVEN a SQL_SCROLL_STATIC advertencia ODBC_01S02.  
  
 Para obtener más información, consulte [SQLSetScrollOptions](../../odbc/reference/syntax/sqlsetscrolloptions-function.md) en el *referencia del programador de ODBC*.
