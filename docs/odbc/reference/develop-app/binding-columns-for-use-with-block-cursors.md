---
title: Enlazar columnas para su uso con cursores de bloque | Documentos de Microsoft
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- column-wise binding [ODBC]
- row-wise binding [ODBC]
- result sets [ODBC], binding columns
- cursors [ODBC], block
- binding columns [ODBC]
- block cursors [ODBC]
- result sets [ODBC], block cursors
ms.assetid: 231beede-cdfa-4e28-8b10-2760b983250f
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: f9bee14abc4bbdbad17360666d40a7d59af5480d
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="binding-columns-for-use-with-block-cursors"></a>Enlazar columnas para su uso con cursores de bloque
Dado que los cursores de bloque devuelven varias filas, las aplicaciones que usan deben enlazar una matriz de variables a cada columna en lugar de una única variable. Estas matrices se conocen colectivamente como la *búferes de conjunto de filas*. Estos son los dos estilos de enlace:  
  
-   Enlazar una matriz para cada columna. Esto se denomina *el enlace* porque cada estructura de datos (matriz) contiene datos de una sola columna.  
  
-   Define una estructura para contener los datos para una fila completa y una matriz de estas estructuras de enlace. Esto se denomina *el enlace* porque cada estructura de datos contiene los datos de una sola fila.  
  
 Tal y como cuando la aplicación enlaza las variables solo a las columnas, se llama a **SQLBindCol** para enlazar las matrices a las columnas. La única diferencia es que las direcciones que se pasan son direcciones de matriz, no sola direcciones de variable. La aplicación establece el atributo de instrucción de SQL_BIND_BY_COLUMN para especificar si está utilizando enlace de modo de columna o de modo de fila. Si desea utilizar el enlace de modo de columna o de modo de fila es mayormente una cuestión de preferencia de la aplicación. El enlace puede corresponden más al diseño de la aplicación de los datos, en cuyo caso podría proporcionar un mejor rendimiento.  
  
 Esta sección contiene los temas siguientes.  
  
-   [El enlace](../../../odbc/reference/develop-app/column-wise-binding.md)  
  
-   [El enlace](../../../odbc/reference/develop-app/row-wise-binding.md)
