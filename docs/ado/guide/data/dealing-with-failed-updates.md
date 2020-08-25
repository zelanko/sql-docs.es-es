---
description: Tratar actualizaciones con errores
title: Tratamiento de las actualizaciones con error | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- updates [ADO], dealing with failed updates
ms.assetid: 299c37bd-19ff-4261-8571-b9665687e075
author: rothja
ms.author: jroth
ms.openlocfilehash: 508508da57fc7a0b1ab899acf3f77b1a49a7fa9b
ms.sourcegitcommit: 33e774fbf48a432485c601541840905c21f613a0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/25/2020
ms.locfileid: "88806927"
---
# <a name="dealing-with-failed-updates"></a>Tratar actualizaciones con errores
Cuando una actualización finaliza con errores, la forma de resolver los errores depende de la naturaleza y la gravedad de los errores y de la lógica de la aplicación. Sin embargo, si la base de datos se comparte con otros usuarios, un error típico es que otra persona modifica el campo antes de hacerlo. Este tipo de error se denomina conflicto. ADO detecta esta situación e informa de un error.  
  
## <a name="remarks"></a>Observaciones  
 Si hay errores de actualización, se capturarán en una rutina de control de errores. Filtre el conjunto de registros con la constante adFilterConflictingRecords de modo que solo estén visibles las filas en conflicto. En este ejemplo, la estrategia de resolución de errores es simplemente imprimir el nombre y los apellidos del autor (au_fname y au_lname).  
  
 El código para avisar al usuario del conflicto de actualización tiene el siguiente aspecto:  
  
```  
objRs.Filter = adFilterConflictingRecords  
objRs.MoveFirst  
Do While Not objRst.EOF  
   Debug.Print "Conflict: Name =  "; objRs!au_fname; " "; objRs!au_lname  
   objRs.MoveNext  
Loop  
```  
  
## <a name="see-also"></a>Consulte también  
 [Batch Mode](./batch-mode.md)