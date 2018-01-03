---
title: Control de errores en Visual C++ | Documentos de Microsoft
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: ado
ms.technology: drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
dev_langs: C++
helpviewer_keywords:
- errors [ADO], Visual C++
- Visual C++ error handling [ADO]
ms.assetid: b7576f07-020a-45f7-9e79-b5756f33f7ab
caps.latest.revision: "5"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 8c7ea661c0254246c3288396d0c5ee6495ca41a7
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/21/2017
---
# <a name="handling-errors-in-visual-c"></a>Control de errores en Visual C++
En COM, la mayoría de las operaciones devuelve un código de retorno HRESULT que indica si una función se ha completado correctamente. La directiva #import genera código que envuelve cada método "sin formato" o una propiedad y comprueba el HRESULT devuelto. Si el valor HRESULT indica error, el código de contenedor produce un error de COM llamada _com_issue_errorex () con el código de retorno HRESULT como argumento. Objetos de error COM se pueden capturar en una **try-catch** bloque. (Para una mayor eficacia, detecte una referencia a un objeto _com_error).  
  
 Recuerde que éstos son los errores de ADO: son el resultado de la operación de ADO. Los errores devueltos por el proveedor subyacente aparecen como **Error** objetos en el **conexión** del objeto **errores** colección.  
  
 La directiva #import sólo crea rutinas de control de errores para los métodos y propiedades declarados en la DLL de ADO. Sin embargo, puede sacar partido de este mismo mecanismo de control de errores escribiendo su propia comprobación de errores de macro o una función insertada. Vea el tema de las extensiones de Visual C++® para obtener ejemplos.
