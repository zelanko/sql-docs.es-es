---
title: Enlazar columnas | Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 035e525116622a3c55e50547958b86fc2ee9bdb6
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/01/2018
ms.locfileid: "47678363"
---
# <a name="binding-columns"></a>Enlazar columnas
Datos capturados desde el origen de datos se devuelven a la aplicación en las variables que ha asignado la aplicación para este propósito. Antes de ello, debe asociar la aplicación, o *enlazar*, establecen estas variables a las columnas del resultado; conceptualmente, este proceso es el mismo que el enlace de variables de aplicación para los parámetros de la instrucción. Cuando la aplicación enlaza una variable a un conjunto de resultados columna, describe esa variable, dirección, tipo de datos y así sucesivamente, al controlador. El controlador almacena esta información en la estructura se mantiene para esa instrucción y usa la información para devolver el valor de la columna cuando se captura la fila.  
  
 Esta sección contiene los temas siguientes.  
  
-   [Columnas del conjunto de resultados de enlace](../../../odbc/reference/develop-app/binding-result-set-columns.md)  
  
-   [Uso de SQLBindCol](../../../odbc/reference/develop-app/using-sqlbindcol.md)
