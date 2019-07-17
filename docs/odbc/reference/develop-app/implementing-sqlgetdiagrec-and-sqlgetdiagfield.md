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
ms.openlocfilehash: a4b602d5ff4a94d2888395e6a62f03553fb50f98
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "68216373"
---
# <a name="implementing-sqlgetdiagrec-and-sqlgetdiagfield"></a>Implementar SQLGetDiagRec y SQLGetDiagField
**SQLGetDiagRec** y **SQLGetDiagField** se implementan mediante el Administrador de controladores y cada controlador. El Administrador de controladores y cada controlador mantienen registros de diagnóstico para cada entorno, la conexión, la instrucción y el identificador de descriptor y liberan los registros solo cuando se llama a otra función con que se libera el identificador o el identificador.  
  
 Aunque el Administrador de controladores y cada controlador deben determinar el primer registro de estado según las clasificaciones en [secuencia de registros de estado](../../../odbc/reference/develop-app/sequence-of-status-records.md), el Administrador de controladores determina la secuencia final de registros.  
  
 **SQLGetDiagRec** y **SQLGetDiagField** no registra los registros de diagnóstico sobre sí mismos.  
  
 Esta sección contiene los temas siguientes.  
  
-   [Reglas de control de diagnóstico](../../../odbc/reference/develop-app/diagnostic-handling-rules.md)  
  
-   [Rol del Administrador de controladores](../../../odbc/reference/develop-app/role-of-the-driver-manager.md)  
  
-   [Rol del controlador](../../../odbc/reference/develop-app/role-of-the-driver.md)
