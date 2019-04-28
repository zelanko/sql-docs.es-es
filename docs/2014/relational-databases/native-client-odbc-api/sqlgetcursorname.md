---
title: SQLGetCursorName | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
topic_type:
- apiref
helpviewer_keywords:
- SQLGetCursorName function
ms.assetid: 3a427a23-28ef-49aa-b9ec-6cab0914bdf3
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 603a2b5be4ca75495f094aa838d0373a9689a523
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "62657784"
---
# <a name="sqlgetcursorname"></a>SQLGetCursorName
  Si la aplicación no especifica un nombre de cursor, el controlador ODBC de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client genera uno para la aplicación en la generación del cursor. La aplicación puede utilizar **SQLGetCursorName** para recuperar el nombre del cursor definido por controlador para las instrucciones UPDATE y DELETE posicionadas. La aplicación no necesita llamar a **SQLSetCursorName** para sacar provecho de las instrucciones de manipulación de datos posicionadas.  
  
## <a name="see-also"></a>Vea también  
 [Función SQLGetCursorName](https://go.microsoft.com/fwlink/?LinkId=59349)   
 [Detalles de implementación de la API de ODBC](odbc-api-implementation-details.md)  
  
  
