---
title: Implementar SQLGetDiagRec y SQLGetDiagField | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- diagnostic information [ODBC], SqlGetDiagField
- SQLGetDiagField function [ODBC], and SQLGetDiagRec
- SQLGetDiagRec function [ODBC], and SQLGetDiagField
- diagnostic information [ODBC], SqlGetDiagRec
- retrieving diagnostic information [ODBC]
ms.assetid: 11ba1857-b533-4517-8131-a2a8a0154a0a
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: ab1f808b005afaa91ed93bf8f8ec7a8385c9c945
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "62447289"
---
# <a name="implementing-sqlgetdiagrec-and-sqlgetdiagfield"></a>Implementar SQLGetDiagRec y SQLGetDiagField
**SQLGetDiagRec** y **SQLGetDiagField** se implementan mediante el Administrador de controladores y cada controlador. El Administrador de controladores y cada controlador mantienen registros de diagnóstico para cada entorno, la conexión, la instrucción y el identificador de descriptor y liberan los registros solo cuando se llama a otra función con que se libera el identificador o el identificador.  
  
 Aunque el Administrador de controladores y cada controlador deben determinar el primer registro de estado según las clasificaciones en [secuencia de registros de estado](../../../odbc/reference/develop-app/sequence-of-status-records.md), el Administrador de controladores determina la secuencia final de registros.  
  
 **SQLGetDiagRec** y **SQLGetDiagField** no registra los registros de diagnóstico sobre sí mismos.  
  
 Esta sección contiene los temas siguientes.  
  
-   [Reglas de control de diagnóstico](../../../odbc/reference/develop-app/diagnostic-handling-rules.md)  
  
-   [Rol del Administrador de controladores](../../../odbc/reference/develop-app/role-of-the-driver-manager.md)  
  
-   [Rol del controlador](../../../odbc/reference/develop-app/role-of-the-driver.md)
