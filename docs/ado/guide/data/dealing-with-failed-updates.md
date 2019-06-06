---
title: Tratar actualizaciones con errores | Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 97a55923043d26c0eb672d7a698d5bf9224f1187
ms.sourcegitcommit: 074d44994b6e84fe4552ad4843d2ce0882b92871
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/05/2019
ms.locfileid: "66718738"
---
# <a name="dealing-with-failed-updates"></a>Tratar actualizaciones con errores
Cuando finaliza una actualización con errores, cómo se resuelven los errores depende de la naturaleza y la gravedad de los errores y la lógica de la aplicación. Sin embargo, si la base de datos se comparte con otros usuarios, un error habitual es que otra persona modifica el campo antes de realizar. Este tipo de error se denomina un conflicto. ADO detecta esta situación y notifica un error.  
  
## <a name="remarks"></a>Comentarios  
 Si hay errores de actualización, se capturarán en una rutina de control de errores. Filtrar el conjunto de registros con la constante adFilterConflictingRecords para que sean visibles solo las filas en conflicto. En este ejemplo, la estrategia de resolución de errores es simplemente imprimir el autor nombres y apellidos (au_fname y au_lname).  
  
 El código para avisar al usuario para el conflicto de actualización tiene este aspecto:  
  
```  
objRs.Filter = adFilterConflictingRecords  
objRs.MoveFirst  
Do While Not objRst.EOF  
   Debug.Print "Conflict: Name =  "; objRs!au_fname; " "; objRs!au_lname  
   objRs.MoveNext  
Loop  
```  
  
## <a name="see-also"></a>Vea también  
 [Modo por lotes](../../../ado/guide/data/batch-mode.md)
