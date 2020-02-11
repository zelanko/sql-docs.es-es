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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 7943987d52554e0f5cd7723e8c9ae8a0e3afddd2
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "68093028"
---
# <a name="sqlbindparameter-cursor-library"></a>SQLBindParameter (biblioteca de cursores)
> [!IMPORTANT]  
>  Esta característica se quitará en una versión futura de Windows. Evite usar esta característica en los nuevos trabajos de desarrollo y planee modificar las aplicaciones que actualmente la utilizan. Microsoft recomienda el uso de la funcionalidad de cursor del controlador.  
  
 En este tema se describe el uso de la función **SQLBindParameter** en la biblioteca de cursores. Para obtener información general acerca de **SQLBindParameter**, consulte [SQLBindParameter (función](../../../odbc/reference/syntax/sqlbindparameter-function.md)).  
  
 Una aplicación puede llamar a **SQLBindParameter** para volver a enlazar parámetros, siempre que el tipo de datos de C, el tamaño de la columna y los dígitos decimales de la columna enlazada sigan siendo los mismos.  
  
 La biblioteca de cursores admite el establecimiento del atributo de instrucción SQL_ATTR_ROW_BIND_OFFSET_PTR para usar desplazamientos de enlace. No es necesario llamar a**SQLBindParameter** para que se produzca este reenlace.  
  
 La biblioteca de cursores permite enlazar parámetros de datos en ejecución.
