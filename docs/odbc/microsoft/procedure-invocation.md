---
title: "Invocación del procedimiento | Documentos de Microsoft"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- SQL grammar [ODBC], procedure invocation
- procedure invocation [ODBC]
ms.assetid: b9ff2c3a-2003-4832-adbe-08dd0f5ad948
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: fd42836285c29e36e6bb64ebe594df570876ff6e
ms.contentlocale: es-es
ms.lasthandoff: 09/09/2017

---
# <a name="procedure-invocation"></a>Invocación del procedimiento
Cuando se utiliza el controlador de Microsoft Access, los procedimientos se pueden invocar desde el controlador mediante el uso de la **SQLExecDirect** o **SQLPrepare** función con la sintaxis siguiente: {llamar *nombre del procedimiento * [(*parámetro*[,*parámetro*]...)]}. Tenga en cuenta que no se admiten expresiones como parámetros a un procedimiento llamado.  
  
 Si un nombre de procedimiento incluye un guión, el nombre debe estar delimitado con comillas atrás (').  
  
 Una consulta con parámetros se puede llamar mediante la instrucción anterior.
