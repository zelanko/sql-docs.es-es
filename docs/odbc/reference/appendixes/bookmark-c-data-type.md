---
title: Tipo de datos del marcador C ( Bookmark C) Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- C data types [ODBC], bookmark C data type
- pseudo-type identifiers [ODBC], bookmark C data type
- data types [ODBC], pseudo-type identifiers
- bookmarks [ODBC]
- bookmark C data type [ODBC]
ms.assetid: add88e48-ada3-4c0c-a5ac-e78903d3ff41
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 566f1065d30a47b2db234ba1f11f877725189fb7
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/14/2020
ms.locfileid: "81292295"
---
# <a name="bookmark-c-data-type"></a>Tipo de datos C de marcador
El tipo de datos C del marcador permite a una aplicación recuperar un marcador. Los tipos C del marcador solo se utilizan para recuperar valores de marcador que pueden ser de longitud variable; no se deben convertir a otros tipos de datos. Una aplicación recupera un marcador de la columna 0 del conjunto de resultados con **SQLBulkOperations** (con una operación de SQL_ADD), **SQLFetch**, **SQLFetchScroll**o **SQLGetData**. Para obtener más información, consulte [Marcadores](../../../odbc/reference/develop-app/bookmarks-odbc.md).  
  
 En la tabla siguiente se muestra el valor de *CType* para el tipo de datos C marcador, el tipo de datos ODBC C que implementa el tipo de datos C marcador y la definición de este tipo de datos de SQL. H.  
  
> [!NOTE]
>  El tipo de datos SQL_C_BOOKMARK ha quedado en desuso. Las aplicaciones ODBC *3.x* no deben usar SQL_C_BOOKMARK. Los controladores ODBC *3.x* deben admitir SQL_C_BOOKMARK solo si desean trabajar con aplicaciones ODBC *2.x* que lo utilizan. El Administrador de controladores asigna SQL_C_VARBOOKMARK a SQL_C_BOOKMARK cuando una aplicación funciona con un controlador ODBC *2.x.*  
  
|Identificador de tipo C|ODBC C typedef|Tipo de C|  
|-----------------------|--------------------|------------|  
|SQL_C_BOOKMARK<br />(Desusado)|Marcador|unsigned long int|  
|SQL_C_VARBOOKMARK|SQLCHAR *|unsigned char *|
