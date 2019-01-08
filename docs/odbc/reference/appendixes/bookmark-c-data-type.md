---
title: Tipo de datos C de marcador | Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: b81acf6c60bd11e03a598e349e145dbf72e174b4
ms.sourcegitcommit: 6443f9a281904af93f0f5b78760b1c68901b7b8d
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/11/2018
ms.locfileid: "53205294"
---
# <a name="bookmark-c-data-type"></a>Tipo de datos C de marcador
El tipo de datos C de marcador permite que una aplicación recuperar un marcador. Los tipos de marcador C sirven únicamente para recuperar los valores de marcador pueden ser variable de longitud; no se debe convertir en otros tipos de datos. Una aplicación recupera un marcador desde la columna 0 del resultado se establece con **SQLBulkOperations** (con una operación de SQL_ADD), **SQLFetch**, **SQLFetchScroll**, o **SQLGetData**. Para obtener más información, consulte [marcadores](../../../odbc/reference/develop-app/bookmarks-odbc.md).  
  
 La tabla siguiente muestra el valor de *CType* para el tipo de datos C de marcador, el tipo de datos C de ODBC que implementa el tipo de datos C de marcador y la definición de datos de este tipo de SQL. H.  
  
> [!NOTE]
>  El tipo de datos SQL_C_BOOKMARK ha quedado obsoleto. ODBC 3 *.x* las aplicaciones no deben usar SQL_C_BOOKMARK. ODBC 3 *.x* controladores deben admitir SQL_C_BOOKMARK solo si desean trabajar con ODBC 2. *x* las aplicaciones que lo usan. El Administrador de controladores asigna SQL_C_VARBOOKMARK a SQL_C_BOOKMARK cuando una aplicación trabaja con un ODBC 2. *x* controlador.  
  
|Identificador de tipo de C|Definición de tipo C de ODBC|Tipo de C|  
|-----------------------|--------------------|------------|  
|SQL_C_BOOKMARK<br />(Desusado)|MARCADOR|int long sin signo|  
|SQL_C_VARBOOKMARK|SQLCHAR *|unsigned char *|
