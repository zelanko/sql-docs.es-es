---
title: GETUTCDATE (expresión de SSIS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- dates [Integration Services], GETUTCDATE
- current date
- UTC time
- GETUTCDATE function
ms.assetid: 2282339c-c24f-493e-8e66-181ea8af5ad0
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 946d728d57210149b84850ca640edb4cafa57195
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/26/2020
ms.locfileid: "62898070"
---
# <a name="getutcdate-ssis-expression"></a>GETUTCDATE (expresión de SSIS)
  Devuelve la fecha actual del sistema en hora UTC (horario universal coordinado u hora del meridiano de Greenwich) usando un formato DT_DBTIMESTAMP. La función GETUTCDATE no tiene argumentos.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
GETUTCDATE()  
```  
  
## <a name="arguments"></a>Argumentos  
 None  
  
## <a name="result-types"></a>Tipos de resultado  
 DT_DBTIMESTAMP  
  
## <a name="expression-examples"></a>Ejemplos de expresiones  
 Este ejemplo devuelve el año de la fecha actual en hora UTC.  
  
```  
DATEPART("year",GETUTCDATE())  
```  
  
 Este ejemplo devuelve el número de días entre una fecha de la columna **ModifiedDate** y la fecha UTC actual.  
  
```  
DATEDIFF("dd",ModifiedDate,GETUTCDATE())  
```  
  
 Este ejemplo agrega tres meses a la fecha UTC actual.  
  
```  
DATEADD("Month",3,GETUTCDATE())  
```  
  
## <a name="see-also"></a>Consulte también  
 [GETDATE &#40;expresión de SSIS&#41;](getdate-ssis-expression.md)   
 [Funciones &#40;expresión de SSIS&#41;](functions-ssis-expression.md)  
  
  
