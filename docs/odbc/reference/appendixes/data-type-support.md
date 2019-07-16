---
title: Compatibilidad con tipos de datos | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- minimum SQL syntax supported [ODBC]
- ODBC drivers [ODBC], minimum SQL syntax supported
- data types [ODBC], ODBC drivers
- ODBC drivers [ODBC], data types
ms.assetid: 782b4490-372b-4366-aad7-a486fb8a07c8
author: MightyPen
ms.author: genemi
ms.openlocfilehash: b5fe4081d0786ace40dd027606a830982798075e
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "68044951"
---
# <a name="data-type-support"></a>Compatibilidad con tipos de datos
Controladores ODBC deben admitir al menos uno de SQL_VARCHAR y SQL_CHAR. Compatibilidad con otros tipos de datos viene determinada por el nivel de conformidad con del controlador u origen de datos SQL-92. Una aplicación debe llamar a **SQLGetTypeInfo** para determinar los tipos de datos compatibles con el controlador.  
  
 Para obtener más información sobre los tipos de datos, vea [apéndice D: Tipos de datos](../../../odbc/reference/appendixes/appendix-d-data-types.md).
