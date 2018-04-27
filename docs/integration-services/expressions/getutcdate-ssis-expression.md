---
title: GETUTCDATE (expresión de SSIS) | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.service: ''
ms.component: expressions
ms.reviewer: ''
ms.suite: sql
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- dates [Integration Services], GETUTCDATE
- current date
- UTC time
- GETUTCDATE function
ms.assetid: 2282339c-c24f-493e-8e66-181ea8af5ad0
caps.latest.revision: 32
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 0067e1204c8445077d7b07e529292e462fd3488a
ms.sourcegitcommit: a85a46312acf8b5a59a8a900310cf088369c4150
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/26/2018
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
  
## <a name="see-also"></a>Ver también  
 [GETDATE &#40;expresión de SSIS&#41;](../../integration-services/expressions/getdate-ssis-expression.md)   
 [Funciones &#40;expresión de SSIS&#41;](../../integration-services/expressions/functions-ssis-expression.md)  
  
  
