---
title: SQLNativeSql | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
topic_type:
- apiref
helpviewer_keywords:
- SQLNativeSql function
ms.assetid: 2d999fec-9e22-4514-ad5f-22a64b82f95b
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 8329eac48b395467c8c9c7354f28649d44149248
ms.sourcegitcommit: b72c9fc9436c44c6a21fd96223c73bf94706c06b
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/01/2020
ms.locfileid: "82705967"
---
# <a name="sqlnativesql"></a>SQLNativeSql
  El controlador ODBC de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client satisface las solicitudes de **SQLNativeSql** sin pasar por el servidor. La función prueba eficazmente la sintaxis de instrucciones SQL. La comprobación de la sintaxis no determina si los identificadores o los resultados de expresiones en las instrucciones SQL son válidos, además [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] SQLNativeSql **devuelve un** SQL nativo que puede causar un error al ejecutarse.  
  
## <a name="see-also"></a>Consulte también  
 [SQLNativeSql función)](https://go.microsoft.com/fwlink/?LinkID=59358)   
 [ODBC API Implementation Details](odbc-api-implementation-details.md)  
  
  
