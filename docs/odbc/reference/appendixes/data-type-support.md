---
title: Compatibilidad con tipos de datos (Data Type Support) Microsoft Docs
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 3abfe85ee32fb9ff4a8499c9949c0685563fec70
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/14/2020
ms.locfileid: "81284432"
---
# <a name="data-type-support"></a>Compatibilidad con tipos de datos
Los controladores ODBC deben admitir al menos uno de SQL_CHAR y SQL_VARCHAR. La compatibilidad con otros tipos de datos viene determinada por el nivel de conformidad SQL-92 del controlador o del origen de datos. Una aplicación debe llamar a **SQLGetTypeInfo** para determinar los tipos de datos admitidos por el controlador.  
  
 Para obtener más información sobre los tipos de datos, vea [Apéndice D: Tipos](../../../odbc/reference/appendixes/appendix-d-data-types.md)de datos .
