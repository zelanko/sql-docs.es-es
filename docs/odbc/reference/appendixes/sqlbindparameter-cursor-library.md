---
title: SQLBindParameter (Biblioteca de cursores) Microsoft Docs
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
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/14/2020
ms.locfileid: "81305433"
---
# <a name="sqlbindparameter-cursor-library"></a>SQLBindParameter (biblioteca de cursores)
> [!IMPORTANT]  
>  Esta característica se eliminará en una versión futura de Windows. Evite usar esta característica en el nuevo trabajo de desarrollo y planee modificar las aplicaciones que actualmente utilizan esta característica. Microsoft recomienda usar la funcionalidad del cursor del controlador.  
  
 En este tema se describe el uso de la función **SQLBindParameter** en la biblioteca de cursores. Para obtener información general acerca de **SQLBindParameter**, vea [SQLBindParameter (Función)](../../../odbc/reference/syntax/sqlbindparameter-function.md).  
  
 Una aplicación puede llamar a **SQLBindParameter** para volver a enlazar parámetros, siempre que el tipo de datos de C, el tamaño de columna y los dígitos decimales de la columna enlazada sigan siendo los mismos.  
  
 La biblioteca de cursores admite la configuración del atributo SQL_ATTR_ROW_BIND_OFFSET_PTR instrucción para utilizar desplazamientos de enlace. (**SQLBindParameter** no tiene que llamarse para que se produzca este reenlace.)  
  
 La biblioteca de cursores admite parámetros de enlace de datos en ejecución.
