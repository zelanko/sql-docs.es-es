---
title: SQLExecDirect (controlador ODBC de Visual FoxPro) | Documentos de Microsoft
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: microsoft
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords: SQLExecDirect function [ODBC], Visual FoxPro ODBC Driver
ms.assetid: 5004060f-8510-4018-87a4-d41789e69d3e
caps.latest.revision: "5"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 39c8f163940784cb135d39b5985f74f6f29bc997
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/20/2017
---
# <a name="sqlexecdirect-visual-foxpro-odbc-driver"></a>SQLExecDirect (controlador ODBC de Visual FoxPro)
> [!NOTE]  
>  Este tema contiene información específica del controlador ODBC de Visual FoxPro. Para obtener información general acerca de esta función, vea el tema correspondiente en [referencia de la API de ODBC](../../odbc/reference/syntax/odbc-api-reference.md).  
  
 Soporte técnico: completo  
  
 Conformidad de la API de ODBC: Nivel de núcleo  
  
 Ejecuta un nuevo [instrucción SQL puede](../../odbc/microsoft/visual-foxpro-terminology.md). El controlador ODBC de Visual FoxPro utiliza los valores actuales de las variables de marcador de parámetro, si existe algún parámetro en la instrucción.  
  
 Para crear un comando por lotes para enviar más de una instrucción SQL a la vez, use un punto y coma (;) para separar cada instrucción SQL del lote.  
  
 Si la tabla, vista o nombres de campo contienen espacios, encierre los nombres en la parte posterior oferta marcas. Por ejemplo, si la base de datos contiene una tabla denominada Mi tabla y el campo mi campo, incluya cada elemento del identificador como sigue:  
  
```  
SELECT `My Table`.`Field1`, `My Table`.`Field2` FROM `My Table`  
```  
  
 Para obtener más información, consulte [SQLExecDirect](../../odbc/reference/syntax/sqlexecdirect-function.md) en el *referencia del programador de ODBC*.
