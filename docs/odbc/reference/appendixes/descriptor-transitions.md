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
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "68130001"
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
  
|D0<br /><br /> Sin asignar|D1i<br /><br /> Implícita|D1e<br /><br /> Explícito|  
|------------------------|----------------------|----------------------|  
|D1i [1]|--|--|  
|D1e [2]|--|--|  
  
 [1] esta fila muestra las transiciones cuando se SQL_HANDLE_STMT *HandleType* .  
  
 [2] esta fila muestra las transiciones cuando se SQL_HANDLE_DESC *HandleType* .  
  
## <a name="sqlcopydesc"></a>SQLCopyDesc  
  
|D0<br /><br /> Sin asignar|D1i<br /><br /> Implícita|D1e<br /><br /> Explícito|  
|------------------------|----------------------|----------------------|  
|ADMITIR|--|--|  
  
## <a name="sqlfreehandle"></a>SQLFreeHandle  
  
|D0<br /><br /> Sin asignar|D1i<br /><br /> Implícita|D1e<br /><br /> Explícito|  
|------------------------|----------------------|----------------------|  
|--[1]|D0|--|  
|ADMITIR dos|(HY017)|D0|  
  
 [1] esta fila muestra las transiciones cuando se SQL_HANDLE_STMT *HandleType* .  
  
 [2] esta fila muestra las transiciones cuando se SQL_HANDLE_DESC *HandleType* .  
  
## <a name="sqlgetdescfield-and-sqlgetdescrec"></a>SQLGetDescField y SQLGetDescRec  
  
|D0<br /><br /> Sin asignar|D1i<br /><br /> Implícita|D1e<br /><br /> Explícito|  
|------------------------|----------------------|----------------------|  
|ADMITIR|--|--|  
  
## <a name="sqlsetdescfield-and-sqlsetdescrec"></a>SQLSetDescField y SQLSetDescRec  
  
|D0<br /><br /> Sin asignar|D1i<br /><br /> Implícita|D1e<br /><br /> Explícito|  
|------------------------|----------------------|----------------------|  
|ADMITIR dimensional|--|--|  
  
 [1] esta fila muestra las transiciones cuando *DescriptorHandle* era el identificador de ARD, APD o IPD, o (para **SQLSetDescField**) cuando *DescriptorHandle* era el identificador de un IRD y *FieldIdentifier* se SQL_DESC_ARRAY_STATUS_PTR o SQL_DESC_ROWS_PROCESSED_PTR.  
  
## <a name="all-other-odbc-functions"></a>Todas las demás funciones ODBC  
  
|D0<br /><br /> Sin asignar|D1i<br /><br /> Implícita|D1e<br /><br /> Explícito|  
|------------------------|----------------------|----------------------|  
|--|--|--|
