---
description: Tratar actualizaciones con errores
title: Tratamiento de las actualizaciones con error | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- updates [ADO], dealing with failed updates
ms.assetid: 299c37bd-19ff-4261-8571-b9665687e075
author: rothja
ms.author: jroth
ms.openlocfilehash: ca4c5a094e263ca0c44c58a9d9118d4e2ce01538
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/27/2020
ms.locfileid: "88991416"
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