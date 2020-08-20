---
description: Transiciones de descriptor
title: Transiciones de descriptor | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- state transitions [ODBC], descriptor
- transitioning states [ODBC], descriptor
- descriptor transitions [ODBC]
ms.assetid: 0cf24fe6-5e3c-45fa-81b8-4f52ddf8501d
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 168df441e2e7e785f7dfc89894ec7aa9caf8207c
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/17/2020
ms.locfileid: "88456601"
---
# <a name="descriptor-transitions"></a>Transiciones de descriptor
Los descriptores ODBC tienen los tres Estados siguientes.  
  
|State|Descripción|  
|-----------|-----------------|  
|D0|Descriptor sin asignar|  
|D1i|Descriptor asignado implícitamente|  
|D1e|Descriptor asignado explícitamente|  
  
 En las tablas siguientes se muestra cómo afecta cada función ODBC al estado del descriptor.  
  
## <a name="sqlallochandle"></a>SQLAllocHandle  
  
|D0<br /><br /> Sin asignar|D1i<br /><br /> Implícita|D1e<br /><br /> Explícita|  
|------------------------|----------------------|----------------------|  
|D1i [1]|--|--|  
|D1e [2]|--|--|  
  
 [1] esta fila muestra las transiciones cuando se SQL_HANDLE_STMT *HandleType* .  
  
 [2] esta fila muestra las transiciones cuando se SQL_HANDLE_DESC *HandleType* .  
  
## <a name="sqlcopydesc"></a>SQLCopyDesc  
  
|D0<br /><br /> Sin asignar|D1i<br /><br /> Implícita|D1e<br /><br /> Explícita|  
|------------------------|----------------------|----------------------|  
|ADMITIR|--|--|  
  
## <a name="sqlfreehandle"></a>SQLFreeHandle  
  
|D0<br /><br /> Sin asignar|D1i<br /><br /> Implícita|D1e<br /><br /> Explícita|  
|------------------------|----------------------|----------------------|  
|--[1]|D0|--|  
|ADMITIR dos|(HY017)|D0|  
  
 [1] esta fila muestra las transiciones cuando se SQL_HANDLE_STMT *HandleType* .  
  
 [2] esta fila muestra las transiciones cuando se SQL_HANDLE_DESC *HandleType* .  
  
## <a name="sqlgetdescfield-and-sqlgetdescrec"></a>SQLGetDescField y SQLGetDescRec  
  
|D0<br /><br /> Sin asignar|D1i<br /><br /> Implícita|D1e<br /><br /> Explícita|  
|------------------------|----------------------|----------------------|  
|ADMITIR|--|--|  
  
## <a name="sqlsetdescfield-and-sqlsetdescrec"></a>SQLSetDescField y SQLSetDescRec  
  
|D0<br /><br /> Sin asignar|D1i<br /><br /> Implícita|D1e<br /><br /> Explícita|  
|------------------------|----------------------|----------------------|  
|ADMITIR dimensional|--|--|  
  
 [1] esta fila muestra las transiciones cuando *DescriptorHandle* era el identificador de ARD, APD o IPD, o (para **SQLSetDescField**) cuando *DescriptorHandle* era el identificador de un IRD y *FieldIdentifier* se SQL_DESC_ARRAY_STATUS_PTR o SQL_DESC_ROWS_PROCESSED_PTR.  
  
## <a name="all-other-odbc-functions"></a>Todas las demás funciones ODBC  
  
|D0<br /><br /> Sin asignar|D1i<br /><br /> Implícita|D1e<br /><br /> Explícita|  
|------------------------|----------------------|----------------------|  
|--|--|--|
