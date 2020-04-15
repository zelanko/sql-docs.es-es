---
title: Columnas de encuadernación ? Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- result sets [ODBC], binding columns
- binding columns [ODBC]
ms.assetid: c4407694-c8e1-4b0b-a39d-b007e6c3b54d
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: fca4cfb1455c91ca57f7b1769266e2040d6a3511
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/14/2020
ms.locfileid: "81301826"
---
# <a name="binding-columns"></a>Enlazar columnas
Los datos obtenidos del origen de datos se devuelven a la aplicación en variables que la aplicación ha asignado para este fin. Antes de que esto se pueda hacer, la aplicación debe asociar o *enlazar*, estas variables a las columnas del conjunto de resultados; conceptualmente, este proceso es el mismo que enlazar variables de aplicación a parámetros de instrucción. Cuando la aplicación enlaza una variable a una columna de conjunto de resultados, describe esa variable (dirección, tipo de datos, etc.) al controlador. El controlador almacena esta información en la estructura que mantiene para esa instrucción y utiliza la información para devolver el valor de la columna cuando se captura la fila.  
  
 Esta sección contiene los temas siguientes.  
  
-   [Columnas del conjunto de resultados de enlace](../../../odbc/reference/develop-app/binding-result-set-columns.md)  
  
-   [Uso de SQLBindCol](../../../odbc/reference/develop-app/using-sqlbindcol.md)
