---
description: SQLSetScrollOptions (controlador ODBC de Visual FoxPro)
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
ms.openlocfilehash: c0e7cecfb0ce7640575cb69f1e84e805a884b57b
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/17/2020
ms.locfileid: "88421639"
---
# <a name="sqlsetscrolloptions-visual-foxpro-odbc-driver"></a>SQLSetScrollOptions (controlador ODBC de Visual FoxPro)
> [!NOTE]  
>  Este tema contiene información específica del controlador ODBC de Visual FoxPro. Para obtener información general sobre esta función, vea el tema correspondiente en referencia de la [API de ODBC](../../odbc/reference/syntax/odbc-api-reference.md).  
  
 Compatibilidad: parcial  
  
 Conformidad con la API de ODBC: nivel 2  
  
 Establece las opciones que controlan el comportamiento de los cursores asociados a un identificador de instrucción, *hstmt*.  
  
 El controlador ODBC de Visual FoxPro solo admite SQL_CONCUR_READ_ONLY; no admite el valor *fConcurrency* SQL_CONCUR_ROWVER. El controlador convierte SQL_KEYSET_SIZE, SQL_CURSOR_DYNAMIC y SQL_CURSOR_KEYSET_DRIVEN en SQL_SCROLL_STATIC con ODBC_01S02 de advertencia.  
  
 Para obtener más información, vea [SQLSetScrollOptions](../../odbc/reference/syntax/sqlsetscrolloptions-function.md) en la *Referencia del programador de ODBC*.
