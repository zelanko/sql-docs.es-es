---
title: Ejemplo de diagnóstico del Administrador de controladores | Documentos de Microsoft
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- driver manager [ODBC], diagnostic messages
- diagnostic information [ODBC], examples
- error messages [ODBC], diagnostic messages
ms.assetid: af8f2d35-d1bf-495c-af25-630654542b7d
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 8c383dda247d3309ed38744609afb5ca12e3c38f
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="driver-manager-diagnostic-example"></a>Ejemplo de diagnóstico del Administrador de controladores
El Administrador de controladores también puede generar mensajes de diagnóstico. Por ejemplo, si una aplicación pasa una opción de dirección no válida para **SQLDataSources**, el Administrador de controladores podría dar formato y devolver los valores siguientes de **SQLGetDiagRec**:  
  
```  
SQLSTATE:         "HY103"  
Native Error:      0  
Diagnostic Msg:   "[Microsoft][ODBC Driver Manager]Direction option out of range"  
```  
  
 Debido al error en el Administrador de controladores, agregar los prefijos para el mensaje de diagnóstico para su proveedor ([Microsoft]) y su identificador ([Administrador de controladores ODBC]).
