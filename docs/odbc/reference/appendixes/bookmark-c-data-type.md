---
title: Tipo de datos C de marcador | Documentos de Microsoft
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- C data types [ODBC], bookmark C data type
- pseudo-type identifiers [ODBC], bookmark C data type
- data types [ODBC], pseudo-type identifiers
- bookmarks [ODBC]
- bookmark C data type [ODBC]
ms.assetid: add88e48-ada3-4c0c-a5ac-e78903d3ff41
caps.latest.revision: "5"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 698e450fbb816c5fb7e3caf3786f4b8d469af50c
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/20/2017
---
# <a name="bookmark-c-data-type"></a>Tipo de datos C de marcador
El tipo de datos C de marcador permite que una aplicación recuperar un marcador. Los tipos de marcador C sirven únicamente para recuperar los valores de marcador pueden ser variable de longitud; no se debe convertir en otros tipos de datos. Una aplicación recupera un marcador de columna 0 del resultado establecido con **SQLBulkOperations** (con una operación de SQL_ADD), **SQLFetch**, **SQLFetchScroll**, o **SQLGetData**. Para obtener más información, consulte [marcadores](../../../odbc/reference/develop-app/bookmarks-odbc.md).  
  
 En la tabla siguiente muestra el valor de *CType* para el tipo de datos C de marcador, escriba el tipo de datos C de ODBC que implementa el tipo de datos de marcador C y la definición de estos datos de SQL. H.  
  
> [!NOTE]  
>  El tipo de datos SQL_C_BOOKMARK está en desuso. ODBC 3*.x* aplicaciones no deben utilizar SQL_C_BOOKMARK. ODBC 3*.x* controladores necesitan admitir SQL_C_BOOKMARK solo si desean trabajar con ODBC 2. *x* las aplicaciones que lo usan. El Administrador de controladores asigna SQL_C_VARBOOKMARK a SQL_C_BOOKMARK cuando una aplicación trabaja con una API ODBC 2. *x* controlador.  
  
|Identificador de tipo de C|Definición de tipo C de ODBC|Tipo de C|  
|-----------------------|--------------------|------------|  
|SQL_C_BOOKMARK<br />(Desusado)|MARCADOR|int long sin signo|  
|SQL_C_VARBOOKMARK|SQLCHAR *|unsigned char *|
