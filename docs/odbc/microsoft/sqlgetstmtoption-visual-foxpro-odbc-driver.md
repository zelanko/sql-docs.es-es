---
title: SQLGetStmtOption (Controlador ODBC de Visual FoxPro) Microsoft Docs
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
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/14/2020
ms.locfileid: "81295145"
---
# <a name="sqlgetstmtoption-visual-foxpro-odbc-driver"></a>SQLGetStmtOption (controlador ODBC de Visual FoxPro)
> [!NOTE]  
>  Este tema contiene información específica del controlador ODBC de Visual FoxPro. Para obtener información general sobre esta función, consulte el tema adecuado en Referencia de [la API ODBC](../../odbc/reference/syntax/odbc-api-reference.md).  
  
 Soporte: Completo  
  
 Conformidad de la API ODBC: nivel uno  
  
 Devuelve la configuración actual de una opción de instrucción.  
  
|*FOption*|Devuelve|  
|---------------|-------------|  
|SQL_GET_BOOKMARK|Valor entero de 32 bits que es el marcador para el número de registro actual|  
|SQL_ROW_NUMBER|Entero de 32 bits que especifica la posición de la fila actual dentro del conjunto de resultados|  
|SQL_TRANSLATE_DLL|Error: "Driver not capable"|  
  
 El controlador ODBC de Visual FoxPro no tiene archivos DLL de traducción.  
  
 Para obtener más información, vea [SQLGetStmtOption](../../odbc/reference/syntax/sqlgetstmtoption-function.md) en la *referencia del programador ODBC*.
