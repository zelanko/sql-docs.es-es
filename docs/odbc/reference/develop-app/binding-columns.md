---
description: Enlazar columnas
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 8f3f02ec6487b34a6ca2c973c3115c3940ca8fa9
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/17/2020
ms.locfileid: "88429437"
---
# <a name="binding-columns"></a>Enlazar columnas
Los datos capturados del origen de datos se devuelven a la aplicación en las variables asignadas por la aplicación para este fin. Antes de ello, la aplicación debe asociar, o *enlazar*, estas variables a las columnas del conjunto de resultados. conceptualmente, este proceso es el mismo que el enlace de variables de aplicación a parámetros de instrucción. Cuando la aplicación enlaza una variable a una columna de conjunto de resultados, describe la dirección de la variable, el tipo de datos, etc. del controlador. El controlador almacena esta información en la estructura que mantiene para esa instrucción y usa la información para devolver el valor de la columna cuando se captura la fila.  
  
 Esta sección contiene los temas siguientes.  
  
-   [Columnas del conjunto de resultados de enlace](../../../odbc/reference/develop-app/binding-result-set-columns.md)  
  
-   [Uso de SQLBindCol](../../../odbc/reference/develop-app/using-sqlbindcol.md)
