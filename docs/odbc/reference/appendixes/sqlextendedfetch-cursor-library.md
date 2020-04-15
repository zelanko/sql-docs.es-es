---
title: SQLExtendedFetch (Biblioteca de cursores) Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLExtendedFetch function [ODBC], Cursor Library
ms.assetid: 06fbf06f-127b-475c-b636-7b784918475d
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: fe39b2d2cbbaf72ce3844c35187040589d1dac58
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/14/2020
ms.locfileid: "81302066"
---
# <a name="sqlextendedfetch-cursor-library"></a>SQLExtendedFetch (biblioteca de cursores)
> [!IMPORTANT]  
>  Esta característica se eliminará en una versión futura de Windows. Evite usar esta característica en el nuevo trabajo de desarrollo y planee modificar las aplicaciones que actualmente utilizan esta característica. Microsoft recomienda usar la funcionalidad del cursor del controlador.  
  
 En este tema se describe el uso de la función **SQLExtendedFetch** en la biblioteca de cursores. Para obtener información general acerca de **SQLExtendedFetch**, vea [SQLExtendedFetch (Función).](../../../odbc/reference/syntax/sqlextendedfetch-function.md)  
  
 La biblioteca de cursores implementa **SQLExtendedFetch** llamando repetidamente a **SQLFetch** en el controlador.  
  
 La biblioteca de cursores admite la llamada a **SQLExtendedFetch** con un *FetchOrientation* de SQL_FETCH_BOOKMARK.  
  
 Cuando se utiliza la biblioteca de cursores, las llamadas a **SQLExtendedFetch** no se pueden mezclar con llamadas a **SQLFetchScroll** o **SQLFetch**.
