---
title: Función SQLTransact | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLTransact
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLTransact
helpviewer_keywords:
- SQLTransact function [ODBC]
ms.assetid: 496249e0-8eff-4c60-8358-5543bc3ead9c
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 6c96c903b68dee2d1d215804d318d47b4c39a7a5
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "68039498"
---
# <a name="sqltransact-function"></a>Función SQLTransact
**Conformidad**  
 Versión de introducción: Cumplimiento de estándares 1.0 de ODBC: En desuso  
  
 **Resumen**  
 En ODBC *3.x*, ODBC *2.x* función **SQLTransact** ha sido reemplazado por **SQLEndTran**. Para obtener más información, consulte [SQLEndTran](../../../odbc/reference/syntax/sqlendtran-function.md).  
  
> [!NOTE]  
>  El atributo SQL_ASYNC_DBC_FUNCTION_ENABLE, que se introdujo en ODBC 3.8, no es compatible con **SQLTransact**. Mediante una operación asincrónica en un identificador de conexión de las aplicaciones deben usar **SQLEndTran**.  
  
## <a name="see-also"></a>Vea también  
 [Referencia de la API de ODBC](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [Archivos de encabezado de ODBC](../../../odbc/reference/install/odbc-header-files.md)
