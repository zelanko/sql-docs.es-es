---
description: Extensiones de Visual C++ para ADO
title: Extensiones de Visual C++ para ADO | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 11/08/2018
ms.reviewer: ''
ms.topic: conceptual
dev_langs:
- C++
helpviewer_keywords:
- ADO, Visual C++
- Visual C++ [ADO], VC++ extensions for ADO
ms.assetid: 2952ece0-7217-4448-bb09-f6b64f43b7e2
author: rothja
ms.author: jroth
ms.openlocfilehash: f9fa962d4710811cf376634dcc299707f6b0e654
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/17/2020
ms.locfileid: "88453937"
---
# <a name="visual-c-extensions-for-ado"></a>Extensiones de Visual C++ para ADO
El método preferido para programar ADO con Visual C++ es usar la directiva **#import** , como se describe en [Microsoft Visual C++ programación de ADO](../../../ado/guide/appendixes/visual-c-ado-programming.md). Sin embargo, las versiones anteriores de ADO se incluían con un método alternativo de programación mediante Visual C++: las extensiones de Visual C++. En esta sección se documenta esta característica para los usuarios que deben mantener Visual C++ código de extensiones, pero se debe escribir el código de ADO nuevo mediante #**Import**.

 Uno de los trabajos más tediosos Visual C++ los programadores a la hora de recuperar datos con ADO es convertir los datos devueltos como un tipo de datos VARIANT en un tipo de datos de C++ y, a continuación, almacenar los datos convertidos en una clase o estructura. Además de ser engorroso, la recuperación de datos de C++ a través de un tipo de datos VARIANT disminuye el rendimiento.

 ADO proporciona una interfaz que admite la recuperación de datos en tipos de datos nativos de C/C++ sin pasar por una variante y también proporciona macros de preprocesador que simplifican el uso de la interfaz. El resultado es una herramienta flexible que es más fácil de usar y tiene un gran rendimiento.

 Un escenario de cliente de C/C++ común es enlazar un registro de un [conjunto de registros](../../../ado/reference/ado-api/recordset-object-ado.md) a una estructura o clase de c/c++ que contiene tipos nativos de c/c++. Al pasar por las variantes, esto implica la escritura de código de conversión de los tipos nativos de C/C++. Las extensiones de Visual C++ para ADO están destinadas a hacer que este escenario sea mucho más fácil para el programador de Visual C++.

 Vea los temas siguientes para obtener más información acerca de las extensiones de Visual C++ para ADO.

-   [Usar extensiones de Visual C++ para ADO](../../../ado/guide/appendixes/using-visual-c-extensions.md)

-   [Encabezado de extensiones de Visual C++](../../../ado/guide/appendixes/visual-c-extensions-header.md)

-   [Ejemplo de ADO con Visual C++ Extensions](../../../ado/guide/appendixes/visual-c-extensions-example.md)

## <a name="see-also"></a>Consulte también
 [Ado para Visual C++ Índice de sintaxis para](../../../ado/reference/ado-api/ado-for-visual-c-syntax-index-for-com.md) [las extensiones de Visual C++](../../../ado/guide/appendixes/visual-c-extensions-example.md) de com ejemplo que [usa extensiones de Visual C++](../../../ado/guide/appendixes/using-visual-c-extensions.md) [Visual C++ encabezado Extensions](../../../ado/guide/appendixes/visual-c-extensions-header.md)
