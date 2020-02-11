---
title: Invocación de procedimiento | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQL grammar [ODBC], procedure invocation
- procedure invocation [ODBC]
ms.assetid: b9ff2c3a-2003-4832-adbe-08dd0f5ad948
author: MightyPen
ms.author: genemi
ms.openlocfilehash: bc37ef6d268dba71f8270909ea9c5b938ef3ee75
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "68070493"
---
# <a name="procedure-invocation"></a>Invocación del procedimiento
Cuando se usa el controlador de Microsoft Access, los procedimientos se pueden invocar desde el controlador mediante la función **SQLExecDirect** o **SQLPrepare** con la sintaxis siguiente: {Call *procedure-Name* [(*parámetro*[,*parámetro*]...)]}. Tenga en cuenta que las expresiones no se admiten como parámetros de un procedimiento llamado.  
  
 Si un nombre de procedimiento incluye un guión, el nombre debe delimitarse con comillas dobles (').  
  
 Se puede llamar a una consulta con parámetros mediante la instrucción anterior.
