---
title: SQLPrepare (Controlador ODBC de Visual FoxPro) Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLPrepare function [ODBC], Visual FoxPro ODBC Driver
ms.assetid: 0c4cb5a4-9729-4b2e-a0c6-52027b92e8fc
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 14c9358d04e539eb2c77a00e195e8216cd0f5496
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/14/2020
ms.locfileid: "81301561"
---
# <a name="sqlprepare-visual-foxpro-odbc-driver"></a>SQLPrepare (controlador ODBC de Visual FoxPro)
> [!NOTE]  
>  Este tema contiene información específica del controlador ODBC de Visual FoxPro. Para obtener información general sobre esta función, consulte el tema adecuado en Referencia de [la API ODBC](../../odbc/reference/syntax/odbc-api-reference.md).  
  
 Soporte: Completo  
  
 Conformidad de la API ODBC: nivel principal  
  
 Prepara una instrucción SQL planeando cómo optimizar y ejecutar la instrucción. [SQLExecDirect](../../odbc/microsoft/sqlexecdirect-visual-foxpro-odbc-driver.md)compila la instrucción SQL para su ejecución.  
  
 Si los nombres de tabla, vista o campo contienen espacios, incluya los nombres en las marcas de comillas atrás ('). Por ejemplo, si la base de datos contiene una tabla denominada Mi tabla y el campo Mi campo, incluya cada elemento del identificador de la siguiente manera:  
  
```  
SELECT * FROM `My Table`.`My Field`  
```  
  
 Para obtener más información, vea [SQLPrepare](../../odbc/reference/syntax/sqlprepare-function.md) en la *referencia del programador ODBC*.
