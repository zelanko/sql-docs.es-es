---
description: Enlazar columnas para su uso con cursores de bloque
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: a58e6359bd7b0ad5d44f75a3d844ef2e9872f2a8
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/17/2020
ms.locfileid: "88429447"
---
# <a name="binding-columns-for-use-with-block-cursors"></a>Enlazar columnas para su uso con cursores de bloque
Dado que los cursores de bloque devuelven varias filas, las aplicaciones que las usan deben enlazar una matriz de variables a cada columna en lugar de a una sola variable. Estas matrices se conocen colectivamente como *búferes de conjunto de filas*. A continuación se muestran los dos estilos de enlace:  
  
-   Enlazar una matriz a cada columna. Esto se denomina *enlace de modo de columna* porque cada estructura de datos (matriz) contiene datos de una sola columna.  
  
-   Defina una estructura que contenga los datos de una fila completa y enlace una matriz de estas estructuras. Esto se denomina *enlace de modo de fila* porque cada estructura de datos contiene los datos de una sola fila.  
  
 Como cuando la aplicación enlaza variables únicas a columnas, llama a **SQLBindCol** para enlazar matrices a columnas. La única diferencia es que las direcciones que se pasan son direcciones de matriz, no direcciones de una sola variable. La aplicación establece el atributo de instrucción SQL_BIND_BY_COLUMN para especificar si utiliza el enlace de modo de columna o de modo de fila. El uso de un enlace de modo de columna o de modo de fila es, en gran medida, una cuestión de preferencia de la aplicación. El enlace de modo de fila podría corresponder más estrechamente con el diseño de datos de la aplicación, en cuyo caso proporcionaría un mejor rendimiento.  
  
 Esta sección contiene los temas siguientes.  
  
-   [El enlace](../../../odbc/reference/develop-app/column-wise-binding.md)  
  
-   [El enlace](../../../odbc/reference/develop-app/row-wise-binding.md)
