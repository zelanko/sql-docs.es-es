---
title: SQLSetScrollOptions (controlador ODBC de Visual FoxPro) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLSetScrollOptions function [ODBC], Visual FoxPro ODBC Driver
ms.assetid: 693e6e28-a845-41b1-9622-5058b0d87229
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 19051fc83466bc40d72c029089cfe6ec45c20a08
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/27/2020
ms.locfileid: "81299425"
---
# <a name="sqlsetscrolloptions-visual-foxpro-odbc-driver"></a>SQLSetScrollOptions (controlador ODBC de Visual FoxPro)
> [!NOTE]  
>  Este tema contiene información específica del controlador ODBC de Visual FoxPro. Para obtener información general sobre esta función, vea el tema correspondiente en referencia de la [API de ODBC](../../odbc/reference/syntax/odbc-api-reference.md).  
  
 Compatibilidad: parcial  
  
 Conformidad con la API de ODBC: nivel 2  
  
 Establece las opciones que controlan el comportamiento de los cursores asociados a un identificador de instrucción, *hstmt*.  
  
 El controlador ODBC de Visual FoxPro solo admite SQL_CONCUR_READ_ONLY; no admite el valor *fConcurrency* SQL_CONCUR_ROWVER. El controlador convierte SQL_KEYSET_SIZE, SQL_CURSOR_DYNAMIC y SQL_CURSOR_KEYSET_DRIVEN en SQL_SCROLL_STATIC con ODBC_01S02 de advertencia.  
  
 Para obtener más información, vea [SQLSetScrollOptions](../../odbc/reference/syntax/sqlsetscrolloptions-function.md) en la *Referencia del programador de ODBC*.
