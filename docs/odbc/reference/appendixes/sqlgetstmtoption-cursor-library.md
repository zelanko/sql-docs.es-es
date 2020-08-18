---
description: SQLGetStmtOption (biblioteca de cursores)
title: SQLGetStmtOption (biblioteca de cursores) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLGetStmtOption function [ODBC], Cursor Library
ms.assetid: 986170b3-fba8-4323-9224-60b381c7effb
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 93a1e34648d1cef320ca7385eb24215701ed9dd3
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/17/2020
ms.locfileid: "88411111"
---
# <a name="sqlgetstmtoption-cursor-library"></a>SQLGetStmtOption (biblioteca de cursores)
> [!IMPORTANT]  
>  Esta característica se quitará en una versión futura de Windows. Evite usar esta característica en los nuevos trabajos de desarrollo y planee modificar las aplicaciones que actualmente la utilizan. Microsoft recomienda el uso de la funcionalidad de cursor del controlador.  
  
 En este tema se describe el uso de la función **SQLGetStmtOption** en la biblioteca de cursores. Para obtener información general sobre **SQLGetStmtOption**, consulte la [función SQLGetStmtOption](../../../odbc/reference/syntax/sqlgetstmtoption-function.md).  
  
 La biblioteca de cursores admite las siguientes opciones de instrucción con **SQLGetStmtOption**:  

:::row:::
    :::column:::
        SQL_BIND_TYPE  
        SQL_CONCURRENCY  
        SQL_CURSOR_TYPE  
        SQL_GET_BOOKMARK  
    :::column-end:::
    :::column:::
        SQL_ROW_NUMBER  
        SQL_ROWSET_SIZE  
        SQL_SIMULATE_CURSOR  
    :::column-end:::
:::row-end:::
