---
title: SQLGetCursorName | Microsoft Docs
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
- SQLGetCursorName function
ms.assetid: 3a427a23-28ef-49aa-b9ec-6cab0914bdf3
caps.latest.revision: 30
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: f8840a494cbf5d4b0cdf8c304da0a0f063fcebed
ms.sourcegitcommit: f8ce92a2f935616339965d140e00298b1f8355d7
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/03/2018
ms.locfileid: "37427834"
---
# <a name="sqlgetcursorname"></a>SQLGetCursorName
  Si la aplicación no especifica un nombre de cursor, el controlador ODBC de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client genera uno para la aplicación en la generación del cursor. La aplicación puede utilizar **SQLGetCursorName** para recuperar el nombre del cursor definido por controlador para las instrucciones UPDATE y DELETE posicionadas. La aplicación no necesita llamar a **SQLSetCursorName** para sacar provecho de las instrucciones de manipulación de datos posicionadas.  
  
## <a name="see-also"></a>Vea también  
 [Función SQLGetCursorName](http://go.microsoft.com/fwlink/?LinkId=59349)   
 [Detalles de implementación de la API de ODBC](odbc-api-implementation-details.md)  
  
  
