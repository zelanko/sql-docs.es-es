---
title: GETUTCDATE (expresión de SSIS) | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- dates [Integration Services], GETUTCDATE
- current date
- UTC time
- GETUTCDATE function
ms.assetid: 2282339c-c24f-493e-8e66-181ea8af5ad0
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 4afe3909387669e1bfcc230744ff7cf5dbd7ae20
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 10/01/2018
ms.locfileid: "47648183"
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
  
  
