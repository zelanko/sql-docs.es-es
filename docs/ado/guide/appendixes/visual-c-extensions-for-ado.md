---
title: Las extensiones de Visual C++ para ADO | Documentos de Microsoft
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: ado
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
dev_langs:
- C++
helpviewer_keywords:
- ADO, Visual C++
- Visual C++ [ADO], VC++ extensions for ADO
ms.assetid: 2952ece0-7217-4448-bb09-f6b64f43b7e2
caps.latest.revision: 
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: d2c48eff858219640bf58bcd9abd9b222e48619b
ms.sourcegitcommit: acab4bcab1385d645fafe2925130f102e114f122
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/09/2018
---
# <a name="visual-c-extensions"></a>Extensiones de Visual C++
El método preferido de programación ADO con Visual C++ utiliza el **#import** directiva, como se describe en [programación ADO en Microsoft Visual C++](../../../ado/guide/appendixes/visual-c-ado-programming.md). Sin embargo, se incluyen las versiones anteriores de ADO con un método alternativo de la programación con Visual C++: extensiones de Visual C++. Esta sección documenta esa característica para aquéllos que deben mantener código de extensiones de Visual C++, pero debería escribir el nuevo código de ADO con #**importar**.

 Uno de lo más tediosas trabajos Visual C++ se enfrentan los programadores al recuperar datos con ADO es convertir los datos devueltos como un tipo de datos VARIANT en un tipo de datos de C++ y, a continuación, almacenar los datos convertidos en una clase o estructura. Además de ser molesto, recuperar datos de C++ a través de un tipo de datos VARIANT disminuye el rendimiento.

 ADO proporciona una interfaz que admite la recuperación de datos en tipos de datos de C o C++ nativo sin pasar por una variante y también proporciona macros de preprocesador que simplifican el uso de la interfaz. El resultado es una herramienta flexible que es más fácil de usar y tiene un gran rendimiento.

 Un escenario común de cliente de C o C++ consiste en enlazar un registro en un [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) a un struct de C o C++ o una clase que contiene los tipos de C o C++ nativo. Cuando vaya a través de variantes, esto implica escribir código de conversión de tipo VARIANT a tipos nativos de C o C++. Extensiones de Visual C++ para ADO se dirigen a lo que este escenario mucho más fácil para los programadores de Visual C++.

 Vea los temas siguientes para obtener más información sobre las extensiones de Visual C++ para ADO.

-   [Utilizar extensiones de Visual C++ para ADO](../../../ado/guide/appendixes/using-visual-c-extensions.md)

-   [Encabezado de extensiones de Visual C++](../../../ado/guide/appendixes/visual-c-extensions-header.md)

-   [ADO con el ejemplo de extensiones de Visual C++](../../../ado/guide/appendixes/visual-c-extensions-example.md)

## <a name="see-also"></a>Vea también
 [ADO para el índice de sintaxis de Visual C++ para COM](../../../ado/reference/ado-api/ado-for-visual-c-syntax-index-for-com.md) [ejemplo de extensiones de Visual C++](../../../ado/guide/appendixes/visual-c-extensions-example.md) [mediante extensiones de Visual C++](../../../ado/guide/appendixes/using-visual-c-extensions.md) [encabezado de extensiones de Visual C++](../../../ado/guide/appendixes/visual-c-extensions-header.md)
