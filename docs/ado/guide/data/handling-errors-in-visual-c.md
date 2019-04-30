---
title: Control de errores en Visual C++ | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
dev_langs:
- C++
helpviewer_keywords:
- errors [ADO], Visual C++
- Visual C++ error handling [ADO]
ms.assetid: b7576f07-020a-45f7-9e79-b5756f33f7ab
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: e33d28201e1a2e4f7df8ac330ac89b3f00194b14
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "63161622"
---
# <a name="handling-errors-in-visual-c"></a>Control de errores en Visual C++
En COM, la mayoría de las operaciones devuelve un código de retorno HRESULT que indica si una función se completó correctamente. La directiva #import genera código de contenedor en torno a cada método de "raw" o una propiedad y comprueba el HRESULT devuelto. Si el valor HRESULT indica un error, el código de contenedor genera un error de COM que realiza la llamada _com_issue_errorex () con el código de retorno HRESULT como argumento. Objetos de error COM se pueden capturar en un **try-catch** bloque. (Para una mayor eficacia, detecte una referencia a un objeto _com_error).  
  
 Recuerde, éstas son errores de ADO: son el resultado de la operación de ADO. Los errores devueltos por el proveedor subyacente aparecen como **Error** objetos en el **conexión** del objeto **errores** colección.  
  
 La directiva #import sólo crea rutinas de control de errores para los métodos y propiedades declaradas en la DLL de ADO. Sin embargo, se puede aprovechar este mismo mecanismo de control de errores al escribir su propia función alineado o macro comprobación de errores. Vea el tema de las extensiones de Visual C++® para ver ejemplos.
