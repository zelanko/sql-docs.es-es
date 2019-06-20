---
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
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: ccd783bdb7bf266bfdc83c3a02520345d707ceea
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "66702625"
---
# <a name="visual-c-extensions-for-ado"></a>Extensiones de Visual C++ para ADO
El método preferido de programación ADO con Visual C++ es usar el **#import** directiva, como se describe en [programación ADO en Microsoft Visual C++](../../../ado/guide/appendixes/visual-c-ado-programming.md). Sin embargo, las versiones anteriores de ADO se incluye con un método alternativo de la programación con Visual C++: las extensiones de Visual C++. Esta sección documentan esta característica para aquellos que se debe mantener el código de extensiones de Visual C++, pero se debe escribir el nuevo código de ADO con #**importar**.

 Uno de lo más tediosas trabajos Visual C++ se enfrentan los programadores al recuperar datos con ADO es convertir los datos devueltos como un tipo de datos VARIANT en un tipo de datos de C++ y, a continuación, almacenar los datos convertidos en una clase o estructura. Además de ser molesto, recuperar datos de C++ a través de un tipo de datos VARIANT disminuye el rendimiento.

 ADO proporciona una interfaz que admite la recuperación de datos en tipos de datos nativos de C o C++ sin pasar por una variante y también proporciona macros de preprocesador que simplifican el uso de la interfaz. El resultado es una herramienta flexible que es más fácil de usar y tiene un rendimiento excelente.

 Un escenario común de cliente de C o C++ consiste en enlazar un registro en un [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) struct de C o C++ o una clase que contiene los tipos de C o C++ nativos. Al pasar a través de variantes, esto implica escribir código de conversión de tipo VARIANT a tipos nativos de C/C ++. Las extensiones de Visual C++ para ADO se destinan a la hora de este escenario mucho más fácil para los programadores de Visual C++.

 Vea los temas siguientes para obtener más información sobre las extensiones de Visual C++ para ADO.

-   [Uso de extensiones de Visual C++ para ADO](../../../ado/guide/appendixes/using-visual-c-extensions.md)

-   [Encabezado de extensiones de Visual C++](../../../ado/guide/appendixes/visual-c-extensions-header.md)

-   [ADO con el ejemplo de extensiones de Visual C++](../../../ado/guide/appendixes/visual-c-extensions-example.md)

## <a name="see-also"></a>Vea también
 [Índice de sintaxis de Visual C++ para COM ADO para](../../../ado/reference/ado-api/ado-for-visual-c-syntax-index-for-com.md) [ejemplo de extensiones de Visual C++](../../../ado/guide/appendixes/visual-c-extensions-example.md) [mediante extensiones de Visual C++](../../../ado/guide/appendixes/using-visual-c-extensions.md) [encabezado de extensiones de Visual C++](../../../ado/guide/appendixes/visual-c-extensions-header.md)
