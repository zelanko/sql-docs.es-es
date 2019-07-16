---
title: SQLBindCol (controlador ODBC de Visual FoxPro) | Microsoft Docs
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 706677b71d1243baac0ca576bb3087d50abb6796
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "68098299"
---
# <a name="sqlbindcol-visual-foxpro-odbc-driver"></a>SQLBindCol (controlador ODBC de Visual FoxPro)
> [!NOTE]  
>  Este tema contiene información específica del controlador ODBC de Visual FoxPro. Para obtener información general acerca de esta función, vea el tema correspondiente en [referencia de la API de ODBC](../../odbc/reference/syntax/odbc-api-reference.md).  
  
 Soporte técnico: Completo  
  
 Conformidad de la API de ODBC: Nivel básico  
  
 Se asigna espacio de almacenamiento para una columna de resultados y especifica el tipo del resultado. Cuando [SQLFetch](../../odbc/microsoft/sqlfetch-visual-foxpro-odbc-driver.md) o [SQLExtendedFetch](../../odbc/microsoft/sqlextendedfetch-visual-foxpro-odbc-driver.md) es llama, el controlador coloca los datos para todas las columnas enlazadas en las ubicaciones asignadas. Consulte [SQLGetTypeInfo](../../odbc/microsoft/sqlgettypeinfo-visual-foxpro-odbc-driver.md) para la asignación entre tipos de datos ODBC y Visual FoxPro.  
  
 Para obtener más información, consulte [SQLBindCol](../../odbc/reference/syntax/sqlbindcol-function.md) en el *referencia del programador de ODBC*.
