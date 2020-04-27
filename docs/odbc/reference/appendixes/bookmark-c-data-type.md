---
title: Tipo de datos de marcador C | Microsoft Docs
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
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/27/2020
ms.locfileid: "81292295"
---
# <a name="bookmark-c-data-type"></a>Tipo de datos C de marcador
El tipo de datos de marcador C permite que una aplicación recupere un marcador. Los tipos de marcador C solo se usan para recuperar valores de marcador que pueden tener una longitud variable. no se deben convertir en otros tipos de datos. Una aplicación recupera un marcador de la columna 0 del conjunto de resultados con **SQLBulkOperations** (con una operación de SQL_ADD), **SQLFetch**, **SQLFetchScroll**o **SQLGetData**. Para obtener más información, vea [marcadores](../../../odbc/reference/develop-app/bookmarks-odbc.md).  
  
 En la tabla siguiente se muestra el valor de *CType* para el tipo de datos de marcador c, el tipo de datos c de ODBC que implementa el tipo de datos de marcador c y la definición de este tipo de datos a partir de SQL. C.  
  
> [!NOTE]
>  El tipo de datos SQL_C_BOOKMARK ha quedado en desuso. Las aplicaciones ODBC *3. x* no deben utilizar SQL_C_BOOKMARK. Los controladores ODBC *3. x* solo deben admitir SQL_C_BOOKMARK si desean trabajar con aplicaciones ODBC *2. x* que lo utilizan. El administrador de controladores asigna SQL_C_VARBOOKMARK a SQL_C_BOOKMARK cuando una aplicación trabaja con un controlador ODBC *2. x* .  
  
|Identificador de tipo de C|Definición de tipo C de ODBC|Tipo de C|  
|-----------------------|--------------------|------------|  
|SQL_C_BOOKMARK<br />(Desusado)|Marcador|unsigned long int|  
|SQL_C_VARBOOKMARK|SQLCHAR|unsigned char *|
