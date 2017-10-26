---
title: "GETDATE (expresión de SSIS) | Documentos de Microsoft"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- current date
- GETDATE function
- dates [Integration Services], GETDATE
ms.assetid: 6d20ec93-3244-4d63-baf6-70eff7bd598c
caps.latest.revision: 35
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: e792dc04b4bb115dc3e9dff840da1690395862e9
ms.contentlocale: es-es
ms.lasthandoff: 08/03/2017

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
  
## <a name="see-also"></a>Vea también  
 [GETUTCDATE &#40; Expresión de SSIS &#41;](../../integration-services/expressions/getutcdate-ssis-expression.md)   
 [Funciones &#40; Expresión de SSIS &#41;](../../integration-services/expressions/functions-ssis-expression.md)  
  
  

