---
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 44e9d92c7371451d6bfdd2e1513c3f8fdac8447b
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "68130001"
---
# <a name="descriptor-transitions"></a>Transiciones de descriptor
Los descriptores de ODBC tienen los tres estados siguientes.  
  
|Estado|Descripción|  
|-----------|-----------------|  
|D0|Descriptor sin asignar|  
|D1i|Descriptores implícitamente asignados|  
|D1e|Descriptores asignados explícitamente|  
  
 Las tablas siguientes muestran cómo cada función ODBC afecta al estado de descriptor.  
  
## <a name="sqlallochandle"></a>SQLAllocHandle  
  
|D0<br /><br /> Sin asignar|D1i<br /><br /> Implícitas|D1e<br /><br /> Explícito|  
|------------------------|----------------------|----------------------|  
|D1i[1]|--|--|  
|D1e[2]|--|--|  
  
 [1] esta fila muestra las transiciones cuando *HandleType* era SQL_HANDLE_STMT.  
  
 [2] esta fila muestra las transiciones cuando *HandleType* era SQL_HANDLE_DESC.  
  
## <a name="sqlcopydesc"></a>SQLCopyDesc  
  
|D0<br /><br /> Sin asignar|D1i<br /><br /> Implícitas|D1e<br /><br /> Explícito|  
|------------------------|----------------------|----------------------|  
|(IH)|--|--|  
  
## <a name="sqlfreehandle"></a>SQLFreeHandle  
  
|D0<br /><br /> Sin asignar|D1i<br /><br /> Implícitas|D1e<br /><br /> Explícito|  
|------------------------|----------------------|----------------------|  
|--[1]|D0|--|  
|(IH)[2]|(HY017)|D0|  
  
 [1] esta fila muestra las transiciones cuando *HandleType* era SQL_HANDLE_STMT.  
  
 [2] esta fila muestra las transiciones cuando *HandleType* era SQL_HANDLE_DESC.  
  
## <a name="sqlgetdescfield-and-sqlgetdescrec"></a>SQLGetDescField y SQLGetDescRec  
  
|D0<br /><br /> Sin asignar|D1i<br /><br /> Implícitas|D1e<br /><br /> Explícito|  
|------------------------|----------------------|----------------------|  
|(IH)|--|--|  
  
## <a name="sqlsetdescfield-and-sqlsetdescrec"></a>SQLSetDescField y SQLSetDescRec  
  
|D0<br /><br /> Sin asignar|D1i<br /><br /> Implícitas|D1e<br /><br /> Explícito|  
|------------------------|----------------------|----------------------|  
|(IH) [1]|--|--|  
  
 [1] esta fila muestra las transiciones cuando *DescriptorHandle* era el controlador de descartar, APD o IPD, o (para **SQLSetDescField**) cuando *DescriptorHandle* era el controlador de un IRD y *FieldIdentifier* era SQL_DESC_ARRAY_STATUS_PTR o SQL_DESC_ROWS_PROCESSED_PTR.  
  
## <a name="all-other-odbc-functions"></a>Todas las demás funciones ODBC  
  
|D0<br /><br /> Sin asignar|D1i<br /><br /> Implícitas|D1e<br /><br /> Explícito|  
|------------------------|----------------------|----------------------|  
|--|--|--|
