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
manager: craigg
ms.openlocfilehash: c9a3d63f0bf1923905c5281655aff2af294b8284
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "63241323"
---
# <a name="data-type-support"></a>Compatibilidad con tipos de datos
Controladores ODBC deben admitir al menos uno de SQL_VARCHAR y SQL_CHAR. Compatibilidad con otros tipos de datos viene determinada por el nivel de conformidad con del controlador u origen de datos SQL-92. Una aplicación debe llamar a **SQLGetTypeInfo** para determinar los tipos de datos compatibles con el controlador.  
  
 Para obtener más información sobre los tipos de datos, vea [apéndice D: Tipos de datos](../../../odbc/reference/appendixes/appendix-d-data-types.md).
