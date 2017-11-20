---
title: Compatibilidad con tipos de datos | Documentos de Microsoft
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.reviewer: 
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- minimum SQL syntax supported [ODBC]
- ODBC drivers [ODBC], minimum SQL syntax supported
- data types [ODBC], ODBC drivers
- ODBC drivers [ODBC], data types
ms.assetid: 782b4490-372b-4366-aad7-a486fb8a07c8
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 147e940dcd37b452e1fe05b3a39f6b184c810397
ms.contentlocale: es-es
ms.lasthandoff: 09/09/2017

---
# <a name="data-type-support"></a>Compatibilidad con tipos de datos
Controladores ODBC deben admitir al menos uno de SQL_CHAR y SQL_VARCHAR. Compatibilidad con otros tipos de datos se determina por el nivel de conformidad de del controlador u origen de datos SQL-92. Una aplicación debe llamar a **SQLGetTypeInfo** para determinar los tipos de datos admitidos por el controlador.  
  
 Para obtener más información sobre los tipos de datos, vea [tipos de datos de apéndice D:](../../../odbc/reference/appendixes/appendix-d-data-types.md).

