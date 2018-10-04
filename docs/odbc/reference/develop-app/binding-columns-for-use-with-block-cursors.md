---
title: Enlazar columnas para su uso con cursores de bloque | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: c0ed819643e7ea818fc17c0fa317473afc8f5ca3
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/01/2018
ms.locfileid: "47706383"
---
# <a name="binding-columns-for-use-with-block-cursors"></a>Enlazar columnas para su uso con cursores de bloque
Dado que los cursores de bloque devuelven varias filas, las aplicaciones que usan deben enlazar una matriz de variables a cada columna en lugar de una sola variable. Estas matrices se conocen colectivamente como la *búferes de conjunto de filas*. Estos son los dos estilos de enlace:  
  
-   Enlazar una matriz para cada columna. Esto se denomina *el enlace* porque cada estructura de datos (matriz) contiene datos para una sola columna.  
  
-   Definir una estructura que contenga los datos de una fila completa y enlazar una matriz de estas estructuras. Esto se denomina *el enlace* porque cada estructura de datos contiene los datos de una sola fila.  
  
 Cuando cuando la aplicación enlaza variables de solo a las columnas, se llama a **SQLBindCol** para enlazar las matrices a las columnas. La única diferencia es que las direcciones pasadas son direcciones de matriz, no sola direcciones de variable. La aplicación establece el atributo de instrucción SQL_BIND_BY_COLUMN para especificar si está utilizando enlace de columna o de modo de fila. Si se debe utilizar el enlace de columna o de modo de fila es principalmente una cuestión de preferencia de la aplicación. El enlace podría corresponden más al diseño de la aplicación de datos, en cuyo caso proporcionaría un mejor rendimiento.  
  
 Esta sección contiene los temas siguientes.  
  
-   [El enlace](../../../odbc/reference/develop-app/column-wise-binding.md)  
  
-   [El enlace](../../../odbc/reference/develop-app/row-wise-binding.md)
