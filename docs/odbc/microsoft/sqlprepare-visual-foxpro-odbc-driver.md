---
title: SQLPrepare (controlador ODBC de Visual FoxPro) | Documentos de Microsoft
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: microsoft
ms.reviewer: 
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- SQLPrepare function [ODBC], Visual FoxPro ODBC Driver
ms.assetid: 0c4cb5a4-9729-4b2e-a0c6-52027b92e8fc
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 9ef6287177be3b52b80e0a2439d7d0686da180da
ms.contentlocale: es-es
ms.lasthandoff: 09/09/2017

---
# <a name="sqlprepare-visual-foxpro-odbc-driver"></a>SQLPrepare (controlador ODBC de Visual FoxPro)
> [!NOTE]  
>  Este tema contiene información específica del controlador ODBC de Visual FoxPro. Para obtener información general acerca de esta función, vea el tema correspondiente en [referencia de la API de ODBC](../../odbc/reference/syntax/odbc-api-reference.md).  
  
 Soporte técnico: completo  
  
 Conformidad de la API de ODBC: Nivel de núcleo  
  
 Prepara una instrucción SQL mediante la planeación de optimizar y ejecute la instrucción. Se compila la instrucción SQL para la ejecución mediante [SQLExecDirect](../../odbc/microsoft/sqlexecdirect-visual-foxpro-odbc-driver.md).  
  
 Si la tabla, vista o nombres de campo contienen espacios, encierre los nombres en la parte posterior oferta marcas ('). Por ejemplo, si la base de datos contiene una tabla denominada Mi tabla y el campo mi campo, incluya cada elemento del identificador como sigue:  
  
```  
SELECT * FROM `My Table`.`My Field`  
```  
  
 Para obtener más información, consulte [SQLPrepare](../../odbc/reference/syntax/sqlprepare-function.md) en el *referencia del programador de ODBC*.

