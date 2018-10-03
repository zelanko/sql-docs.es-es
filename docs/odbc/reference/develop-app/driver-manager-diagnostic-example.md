---
title: Ejemplo de diagnóstico del Administrador de controladores | Microsoft Docs
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
manager: craigg
ms.openlocfilehash: 6ad253c2d0603846d6d1f795f6115e7bb727b3da
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/01/2018
ms.locfileid: "47778595"
---
# <a name="driver-manager-diagnostic-example"></a>Ejemplo de diagnóstico del Administrador de controladores
El Administrador de controladores puede generar también mensajes de diagnóstico. Por ejemplo, si una aplicación pasa de una opción de dirección no válida para **SQLDataSources**, el Administrador de controladores podría dar formato y devolver los valores siguientes de **SQLGetDiagRec**:  
  
```  
SQLSTATE:         "HY103"  
Native Error:      0  
Diagnostic Msg:   "[Microsoft][ODBC Driver Manager]Direction option out of range"  
```  
  
 Debido al error en el Administrador de controladores, agregar prefijos para el mensaje de diagnóstico para su proveedor ([Microsoft]) y su identificador ([ODBC Driver Manager]).
