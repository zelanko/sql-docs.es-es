---
title: Invocación del procedimiento | Documentos de Microsoft
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: odbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- SQL grammar [ODBC], procedure invocation
- procedure invocation [ODBC]
ms.assetid: b9ff2c3a-2003-4832-adbe-08dd0f5ad948
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 6d01859ee1b44f29c1109e976cc4a59302306444
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="procedure-invocation"></a>Invocación del procedimiento
Cuando se utiliza el controlador de Microsoft Access, los procedimientos se pueden invocar desde el controlador mediante el uso de la **SQLExecDirect** o **SQLPrepare** función con la sintaxis siguiente: {llamar *nombre del procedimiento*  [(*parámetro*[,*parámetro*]...)]}. Tenga en cuenta que no se admiten expresiones como parámetros a un procedimiento llamado.  
  
 Si un nombre de procedimiento incluye un guión, el nombre debe estar delimitado con comillas atrás (').  
  
 Una consulta con parámetros se puede llamar mediante la instrucción anterior.
