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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 1581cb7ecc694dc9adcbb03d83cf73a6ba41dbed
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "63270042"
---
# <a name="sqltransact-visual-foxpro-odbc-driver"></a>SQLTransact (controlador ODBC de Visual FoxPro)
> [!NOTE]  
>  Este tema contiene información específica del controlador ODBC de Visual FoxPro. Para obtener información general acerca de esta función, vea el tema correspondiente en [referencia de la API de ODBC](../../odbc/reference/syntax/odbc-api-reference.md).  
  
 Soporte técnico: Completo  
  
 Conformidad de la API de ODBC: Nivel básico  
  
 Solicita una operación de confirmación o reversión para todas las operaciones activas en todos los identificadores de instrucciones (*hstmt*s) asociado con una conexión o para todas las conexiones asociadas con el identificador del entorno, *henv*. **SQLTransact** solo funciona para los orígenes de datos que son [bases de datos](../../odbc/microsoft/visual-foxpro-terminology.md).  
  
 Si se produce un error en una confirmación en el modo manual, la transacción permanece activa; puede revertir la transacción o volver a intentar la operación de confirmación. Si se produce un error en una operación de confirmación cuando está en modo de transacción automática, la transacción se revierte automáticamente; la transacción no puede estar inactiva.  
  
 Para obtener más información, consulte [SQLTransact](../../odbc/reference/syntax/sqltransact-function.md) en el *referencia del programador de ODBC*.
