---
title: SQLBindParameter (biblioteca de cursores) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLBindParameter function [ODBC], Cursor Library
ms.assetid: 04c53e4c-cd1d-40b2-9997-684ebe43499f
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 55708cc5192fb40149d6db7710f6ee638c4880d2
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/27/2020
ms.locfileid: "81305433"
---
# <a name="sqlbindparameter-cursor-library"></a>SQLBindParameter (biblioteca de cursores)
> [!IMPORTANT]  
>  Esta característica se quitará en una versión futura de Windows. Evite usar esta característica en los nuevos trabajos de desarrollo y planee modificar las aplicaciones que actualmente la utilizan. Microsoft recomienda el uso de la funcionalidad de cursor del controlador.  
  
 En este tema se describe el uso de la función **SQLBindParameter** en la biblioteca de cursores. Para obtener información general acerca de **SQLBindParameter**, consulte [SQLBindParameter (función](../../../odbc/reference/syntax/sqlbindparameter-function.md)).  
  
 Una aplicación puede llamar a **SQLBindParameter** para volver a enlazar parámetros, siempre que el tipo de datos de C, el tamaño de la columna y los dígitos decimales de la columna enlazada sigan siendo los mismos.  
  
 La biblioteca de cursores admite el establecimiento del atributo de instrucción SQL_ATTR_ROW_BIND_OFFSET_PTR para usar desplazamientos de enlace. No es necesario llamar a**SQLBindParameter** para que se produzca este reenlace.  
  
 La biblioteca de cursores permite enlazar parámetros de datos en ejecución.
