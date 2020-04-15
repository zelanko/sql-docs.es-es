---
title: SQLExecDirect (Controlador ODBC de Visual FoxPro) Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLExecDirect function [ODBC], Visual FoxPro ODBC Driver
ms.assetid: 5004060f-8510-4018-87a4-d41789e69d3e
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 40c0a3404a3e7a9a67b6f71d197343eddb417955
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/14/2020
ms.locfileid: "81298675"
---
# <a name="sqlexecdirect-visual-foxpro-odbc-driver"></a>SQLExecDirect (controlador ODBC de Visual FoxPro)
> [!NOTE]  
>  Este tema contiene información específica del controlador ODBC de Visual FoxPro. Para obtener información general sobre esta función, consulte el tema adecuado en Referencia de [la API ODBC](../../odbc/reference/syntax/odbc-api-reference.md).  
  
 Soporte: Completo  
  
 Conformidad de la API ODBC: nivel principal  
  
 Ejecuta una nueva [instrucción SQL preparable.](../../odbc/microsoft/visual-foxpro-terminology.md) El controlador ODBC de Visual FoxPro utiliza los valores actuales de las variables de marcador de parámetro si existen parámetros en la instrucción.  
  
 Para crear un comando por lotes para enviar más de una instrucción SQL a la vez, utilice un punto y coma (;) separar cada instrucción SQL del lote.  
  
 Si los nombres de tabla, vista o campo contienen espacios, incluya los nombres entre comillas. Por ejemplo, si la base de datos contiene una tabla denominada Mi tabla y el campo Mi campo, incluya cada elemento del identificador de la siguiente manera:  
  
```  
SELECT `My Table`.`Field1`, `My Table`.`Field2` FROM `My Table`  
```  
  
 Para obtener más información, vea [SQLExecDirect](../../odbc/reference/syntax/sqlexecdirect-function.md) en la *referencia del programador ODBC*.
