---
description: SQLExecDirect (controlador ODBC de Visual FoxPro)
title: SQLExecDirect (controlador ODBC de Visual FoxPro) | Microsoft Docs
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
ms.openlocfilehash: d12218097caf6d4a2c4a0375f1a8e9542b2ccf59
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/17/2020
ms.locfileid: "88449187"
---
# <a name="sqlexecdirect-visual-foxpro-odbc-driver"></a>SQLExecDirect (controlador ODBC de Visual FoxPro)
> [!NOTE]  
>  Este tema contiene información específica del controlador ODBC de Visual FoxPro. Para obtener información general sobre esta función, vea el tema correspondiente en referencia de la [API de ODBC](../../odbc/reference/syntax/odbc-api-reference.md).  
  
 Compatibilidad: completa  
  
 Conformidad con la API de ODBC: nivel básico  
  
 Ejecuta una nueva [instrucción SQL preparable.](../../odbc/microsoft/visual-foxpro-terminology.md). El controlador ODBC de Visual FoxPro usa los valores actuales de las variables de marcador de parámetro si existe algún parámetro en la instrucción.  
  
 Para crear un comando por lotes para enviar más de una instrucción SQL a la vez, use un punto y coma (;) para separar cada instrucción SQL en el lote.  
  
 Si los nombres de tabla, vista o campo contienen espacios, incluya los nombres entre comillas tipográficas. Por ejemplo, si la base de datos contiene una tabla denominada My Table y el campo Field, incluya cada elemento del identificador de la manera siguiente:  
  
```  
SELECT `My Table`.`Field1`, `My Table`.`Field2` FROM `My Table`  
```  
  
 Para obtener más información, vea [SQLExecDirect](../../odbc/reference/syntax/sqlexecdirect-function.md) en la *Referencia del programador de ODBC*.
