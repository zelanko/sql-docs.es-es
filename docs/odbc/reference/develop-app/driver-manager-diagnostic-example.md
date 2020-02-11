---
title: Ejemplo de diagnóstico del administrador de controladores | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- driver manager [ODBC], diagnostic messages
- diagnostic information [ODBC], examples
- error messages [ODBC], diagnostic messages
ms.assetid: af8f2d35-d1bf-495c-af25-630654542b7d
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 95392367b70af3eb820f0943af5dc668783a3fe5
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "68046961"
---
# <a name="driver-manager-diagnostic-example"></a>Ejemplo de diagnóstico del Administrador de controladores
El administrador de controladores también puede generar mensajes de diagnóstico. Por ejemplo, si una aplicación pasa una opción de dirección no válida a **SQLDataSources**, el administrador de controladores podría dar formato y devolver los valores siguientes de **SQLGetDiagRec**:  
  
```  
SQLSTATE:         "HY103"  
Native Error:      0  
Diagnostic Msg:   "[Microsoft][ODBC Driver Manager]Direction option out of range"  
```  
  
 Dado que el error se produjo en el administrador de controladores, agregó prefijos al mensaje de diagnóstico para su proveedor ([Microsoft]) y su identificador ([administrador de controladores ODBC]).
