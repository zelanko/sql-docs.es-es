---
title: SQLFreeHandle | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology: native-client
ms.tgt_pltfrm: ''
ms.topic: reference
topic_type:
- apiref
helpviewer_keywords:
- SQLFreeHandle function
ms.assetid: d374e5c8-ed35-43bf-8dd6-c37e38d9b5f1
caps.latest.revision: 28
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 7ba100363f3570364d9a114e8406d2b0b4c8f21f
ms.sourcegitcommit: f8ce92a2f935616339965d140e00298b1f8355d7
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/03/2018
ms.locfileid: "37411764"
---
# <a name="sqlfreehandle"></a>SQLFreeHandle
  En el modo de confirmación manual, al llamar a **SQLFreeHandle** en un identificador de instrucción con una transacción abierta se produce una operación de reversión de cambios pendientes a la base de datos. Al llamando a **SQLFreeHandle** en un identificador de instrucción siempre se cierra cualquier cursor abierto y se descartan los resultados pendientes, liberando todos los recursos asociados con el identificador de instrucción.  
  
## <a name="see-also"></a>Vea también  
 [Función SQLFreeHandle](http://go.microsoft.com/fwlink/?LinkId=59345)   
 [Detalles de implementación de la API de ODBC](odbc-api-implementation-details.md)  
  
  
