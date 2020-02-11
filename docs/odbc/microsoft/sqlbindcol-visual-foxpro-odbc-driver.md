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
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "68098299"
---
# <a name="sqlbindcol-visual-foxpro-odbc-driver"></a>SQLBindCol (controlador ODBC de Visual FoxPro)
> [!NOTE]  
>  Este tema contiene información específica del controlador ODBC de Visual FoxPro. Para obtener información general sobre esta función, vea el tema correspondiente en referencia de la [API de ODBC](../../odbc/reference/syntax/odbc-api-reference.md).  
  
 Compatibilidad: completa  
  
 Conformidad con la API de ODBC: nivel básico  
  
 Asigna espacio de almacenamiento para una columna de resultados y especifica el tipo del resultado. Cuando se llama a [SQLFetch](../../odbc/microsoft/sqlfetch-visual-foxpro-odbc-driver.md) o [SQLExtendedFetch](../../odbc/microsoft/sqlextendedfetch-visual-foxpro-odbc-driver.md) , el controlador coloca los datos de todas las columnas enlazadas en las ubicaciones asignadas. Vea [SQLGetTypeInfo](../../odbc/microsoft/sqlgettypeinfo-visual-foxpro-odbc-driver.md) para obtener información sobre la asignación entre los tipos de datos de ODBC y Visual FoxPro.  
  
 Para obtener más información, vea [SQLBindCol](../../odbc/reference/syntax/sqlbindcol-function.md) en la *Referencia del programador de ODBC*.
