---
title: SQLEndTran | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
topic_type:
- apiref
helpviewer_keywords:
- SQLEndTran function
ms.assetid: 95cff841-c2d5-4e1e-a18d-f3d4696a5b85
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: f5425fdc189febd23e9fc61765f4ad56fe484111
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "63067606"
---
# <a name="sqlendtran"></a>SQLEndTran
  De forma predeterminada, el controlador ODBC de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client cierra el cursor asociado de una instrucción cuando **SQLEndTran** confirma o revierte una operación. Los cursores de servidor se cierran, a menos que sean estáticos. Cuando **SQLEndTran** confirma o revierte una operación, el valor del atributo de conexión ODBC específico del controlador SQL_COPT_SS_PRESERVE_CURSORS, establecido por [SQLSetConnectAttr](sqlsetconnectattr.md), determina el comportamiento del cursor asociado de una instrucción.  
  
## <a name="see-also"></a>Consulte también  
 [Detalles de implementación de la API de ODBC](odbc-api-implementation-details.md)   
 [Función SQLEndTran](https://go.microsoft.com/fwlink/?LinkId=59342)  
  
  
