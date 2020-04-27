---
title: GETDATE (expresión de SSIS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- current date
- GETDATE function
- dates [Integration Services], GETDATE
ms.assetid: 6d20ec93-3244-4d63-baf6-70eff7bd598c
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 83d8d4126ff7dbcd6e0d5b114626cd8acb1b8d20
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/26/2020
ms.locfileid: "62769037"
---
# <a name="getdate-ssis-expression"></a>GETDATE (expresión de SSIS)
  Devuelve la fecha actual del sistema con formato DT_DBTIMESTAMP. La función GETDATE no tiene argumentos.  
  
> [!NOTE]  
>  El resultado devuelto de la función GETDATE tiene una longitud de 29 caracteres.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
GETDATE()  
```  
  
## <a name="arguments"></a>Argumentos  
 None  
  
## <a name="result-types"></a>Tipos de resultado  
 DT_DBTIMESTAMP  
  
## <a name="expression-examples"></a>Ejemplos de expresiones  
 Este ejemplo devuelve el año de la fecha actual.  
  
```  
DATEPART("year",GETDATE())  
```  
  
 Este ejemplo devuelve el número de días entre una fecha de la columna **ModifiedDate** y la fecha actual.  
  
```  
DATEDIFF("dd",ModifiedDate,GETDATE())  
```  
  
 Este ejemplo agrega tres meses a la fecha actual.  
  
```  
DATEADD("Month",3,GETDATE())  
```  
  
## <a name="see-also"></a>Consulte también  
 [GETUTCDATE &#40;expresión de SSIS&#41;](getutcdate-ssis-expression.md)   
 [Funciones &#40;expresión de SSIS&#41;](functions-ssis-expression.md)  
  
  
