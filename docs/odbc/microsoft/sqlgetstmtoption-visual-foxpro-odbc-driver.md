---
title: SQLGetStmtOption (controlador ODBC de Visual FoxPro) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLGetStmtOption function [ODBC], Visual FoxPro ODBC Driver
ms.assetid: 984a8b1d-f12c-420c-8be4-f555114c764b
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 2624783f7bd55903f5741c62190626e455a9096d
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/27/2020
ms.locfileid: "81295145"
---
# <a name="sqlgetstmtoption-visual-foxpro-odbc-driver"></a>SQLGetStmtOption (controlador ODBC de Visual FoxPro)
> [!NOTE]  
>  Este tema contiene información específica del controlador ODBC de Visual FoxPro. Para obtener información general sobre esta función, vea el tema correspondiente en referencia de la [API de ODBC](../../odbc/reference/syntax/odbc-api-reference.md).  
  
 Compatibilidad: completa  
  
 Conformidad con la API de ODBC: nivel uno  
  
 Devuelve el valor actual de una opción de instrucción.  
  
|*FOption*|Devuelve|  
|---------------|-------------|  
|SQL_GET_BOOKMARK|valor entero de 32 bits que es el marcador para el número de registro actual.|  
|SQL_ROW_NUMBER|entero de 32 bits que especifica la posición de la fila actual dentro del conjunto de resultados|  
|SQL_TRANSLATE_DLL|Error: "controlador no compatible"|  
  
 El controlador ODBC de Visual FoxPro no tiene ninguna dll de traducción.  
  
 Para obtener más información, vea [SQLGetStmtOption](../../odbc/reference/syntax/sqlgetstmtoption-function.md) en la *Referencia del programador de ODBC*.
