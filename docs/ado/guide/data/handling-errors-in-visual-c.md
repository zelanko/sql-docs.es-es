---
description: Control de errores en Visual C++
title: Control de errores en Visual C++ | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
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
author: rothja
ms.author: jroth
ms.openlocfilehash: 3f61f6b9f27011543545932f9ce7d9e5d434bbf9
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/27/2020
ms.locfileid: "88980626"
---
# <a name="handling-errors-in-visual-c"></a>Control de errores en Visual C++
En COM, la mayoría de las operaciones devuelven un código de retorno HRESULT que indica si una función se ha completado correctamente. La Directiva #import genera código de contenedor alrededor de cada método o propiedad "RAW" y comprueba el HRESULT devuelto. Si el valor HRESULT indica un error, el código de contenedor produce un error COM llamando a _com_issue_errorex () con el código de retorno HRESULT como argumento. Los objetos de error COM se pueden detectar en un bloque **try-catch** . (Por motivos de eficacia, Capture una referencia a un objeto _com_error).  
  
 Recuerde que se trata de errores de ADO: son el resultado de un error en la operación de ADO. Los errores devueltos por el proveedor subyacente aparecen como objetos de **error** en la colección de **errores** del objeto de **conexión** .  
  
 La Directiva #import solo crea rutinas de control de errores para métodos y propiedades declaradas en el archivo. dll de ADO. Sin embargo, puede aprovechar este mismo mecanismo de control de errores escribiendo su propia macro o función insertada. Vea el tema Visual C++ extensiones de® para obtener ejemplos.
