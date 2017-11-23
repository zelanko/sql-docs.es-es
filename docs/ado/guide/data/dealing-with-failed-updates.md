---
title: Tratar actualizaciones con errores | Documentos de Microsoft
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: guide
ms.technology: drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords: updates [ADO], dealing with failed updates
ms.assetid: 299c37bd-19ff-4261-8571-b9665687e075
caps.latest.revision: "3"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: e2be023b954040c1c539063c1e1a3d1cf67931ba
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/17/2017
---
# <a name="dealing-with-failed-updates"></a>Tratar actualizaciones con errores
Cuando una actualización concluye con errores, cómo resolver los errores depende de la naturaleza y la gravedad de los errores y la lógica de la aplicación. Sin embargo, si la base de datos se comparte con otros usuarios, un error habitual es que otro usuario modifica el campo antes de seguir. Este tipo de error se denomina un conflicto. ADO detecta esta situación y notifica un error.  
  
## <a name="remarks"></a>Comentarios  
 Si hay errores de actualización, se capturarán en una rutina de control de errores. Filtre el conjunto de registros con la constante adFilterConflictingRecords para que estén visibles solo las filas en conflicto. En este ejemplo, la estrategia de resolución de errores consiste simplemente en imprimir el autor nombres y apellidos (au_fname y au_lname).  
  
 El código para avisar al usuario para el conflicto de actualización tiene el siguiente aspecto:  
  
```  
objRs.Filter = adFilterConflictingRecords  
objRs.MoveFirst  
Do While Not objRst.EOF  
   Debug.Print "Conflict: Name =  "; objRs!au_fname; " "; objRs!au_lname  
   objRs.MoveNext  
Loop  
```  
  
## <a name="see-also"></a>Vea también  
 [Modo por lotes](../../../ado/guide/data/batch-mode.md)
