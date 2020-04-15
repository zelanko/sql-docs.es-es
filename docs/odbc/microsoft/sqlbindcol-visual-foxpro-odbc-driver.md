---
title: SQLBindCol (Controlador ODBC de Visual FoxPro) Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLBindCol function [ODBC], Visual FoxPro ODBC Driver
ms.assetid: 984d6605-39ba-4d33-ac94-22625bfa6107
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 1e5eda58c6dec31206de9ddb10e73bdf90272d0a
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/14/2020
ms.locfileid: "81300645"
---
# <a name="sqlbindcol-visual-foxpro-odbc-driver"></a>SQLBindCol (controlador ODBC de Visual FoxPro)
> [!NOTE]  
>  Este tema contiene información específica del controlador ODBC de Visual FoxPro. Para obtener información general sobre esta función, consulte el tema adecuado en Referencia de [la API ODBC](../../odbc/reference/syntax/odbc-api-reference.md).  
  
 Soporte: Completo  
  
 Conformidad de la API ODBC: nivel principal  
  
 Asigna espacio de almacenamiento para una columna de resultados y especifica el tipo del resultado. Cuando [SQLFetch](../../odbc/microsoft/sqlfetch-visual-foxpro-odbc-driver.md) o [SQLExtendedFetch](../../odbc/microsoft/sqlextendedfetch-visual-foxpro-odbc-driver.md) se llama, el controlador coloca los datos para todas las columnas enlazadas en las ubicaciones asignadas. Consulte [SQLGetTypeInfo](../../odbc/microsoft/sqlgettypeinfo-visual-foxpro-odbc-driver.md) para obtener la asignación entre los tipos de datos ODBC y Visual FoxPro.  
  
 Para obtener más información, vea [SQLBindCol](../../odbc/reference/syntax/sqlbindcol-function.md) en la *referencia del programador ODBC*.
