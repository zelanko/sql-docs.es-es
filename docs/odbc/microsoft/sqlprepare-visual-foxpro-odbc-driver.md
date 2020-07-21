---
title: SQLPrepare (controlador ODBC de Visual FoxPro) | Microsoft Docs
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
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/27/2020
ms.locfileid: "81301561"
---
# <a name="sqlprepare-visual-foxpro-odbc-driver"></a>SQLPrepare (controlador ODBC de Visual FoxPro)
> [!NOTE]  
>  Este tema contiene información específica del controlador ODBC de Visual FoxPro. Para obtener información general sobre esta función, vea el tema correspondiente en referencia de la [API de ODBC](../../odbc/reference/syntax/odbc-api-reference.md).  
  
 Compatibilidad: completa  
  
 Conformidad con la API de ODBC: nivel básico  
  
 Prepara una instrucción SQL planeando cómo optimizar y ejecutar la instrucción. La instrucción SQL se compila para su ejecución mediante [SQLExecDirect](../../odbc/microsoft/sqlexecdirect-visual-foxpro-odbc-driver.md).  
  
 Si los nombres de tabla, vista o campo contienen espacios, incluya los nombres entre comillas dobles ('). Por ejemplo, si la base de datos contiene una tabla denominada My Table y el campo Field, incluya cada elemento del identificador de la manera siguiente:  
  
```  
SELECT * FROM `My Table`.`My Field`  
```  
  
 Para obtener más información, consulte [SQLPrepare](../../odbc/reference/syntax/sqlprepare-function.md) en la *Referencia del programador de ODBC*.
