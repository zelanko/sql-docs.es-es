---
title: SQLTransact (controlador ODBC de Visual FoxPro) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLTransact function [ODBC], Visual FoxPro ODBC Driver
ms.assetid: 92cf86c0-f7a8-44d7-b59f-a1342677440b
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 3910f24578bcbc409a84573e994c0680ed5949b2
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/27/2020
ms.locfileid: "81299225"
---
# <a name="sqltransact-visual-foxpro-odbc-driver"></a>SQLTransact (controlador ODBC de Visual FoxPro)
> [!NOTE]  
>  Este tema contiene información específica del controlador ODBC de Visual FoxPro. Para obtener información general sobre esta función, vea el tema correspondiente en referencia de la [API de ODBC](../../odbc/reference/syntax/odbc-api-reference.md).  
  
 Compatibilidad: completa  
  
 Conformidad con la API de ODBC: nivel básico  
  
 Solicita una operación de confirmación o reversión para todas las operaciones activas en todos los identificadores de instrucciones (*hstmt*s) asociados a una conexión o para todas las conexiones asociadas al identificador de entorno, *HENV*. **SQLTransact** solo funciona con orígenes de datos que son [bases](../../odbc/microsoft/visual-foxpro-terminology.md)de datos de.  
  
 Si se produce un error en una confirmación en el modo manual, la transacción permanece activa; puede optar por revertir la transacción o volver a intentar la operación de confirmación. Si se produce un error en una operación de confirmación en el modo de transacción automática, la transacción se revierte automáticamente. la transacción no puede estar inactiva.  
  
 Para obtener más información, vea [SQLTransact](../../odbc/reference/syntax/sqltransact-function.md) en la *Referencia del programador de ODBC*.
