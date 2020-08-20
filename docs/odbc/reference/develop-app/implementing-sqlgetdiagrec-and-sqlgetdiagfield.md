---
description: Implementar SQLGetDiagRec y SQLGetDiagField
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 91e43252aea4ebf12dedcb14bb1b7fb34f75df6f
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/17/2020
ms.locfileid: "88461437"
---
# <a name="implementing-sqlgetdiagrec-and-sqlgetdiagfield"></a>Implementar SQLGetDiagRec y SQLGetDiagField
**SQLGetDiagRec** y **SQLGetDiagField** se implementan mediante el administrador de controladores y cada controlador. El administrador de controladores y cada controlador mantienen registros de diagnóstico para cada entorno, conexión, instrucción y identificador de descriptor, y liberan esos registros solo cuando se llama a otra función con ese identificador o se libera el identificador.  
  
 Aunque el administrador de controladores y cada controlador deben determinar el primer registro de estado según las clasificaciones en [secuencia de registros de estado](../../../odbc/reference/develop-app/sequence-of-status-records.md), el administrador de controladores determina la secuencia final de los registros.  
  
 **SQLGetDiagRec** y **SQLGetDiagField** no publican registros de diagnóstico sobre sí mismos.  
  
 Esta sección contiene los temas siguientes.  
  
-   [Reglas de control de diagnóstico](../../../odbc/reference/develop-app/diagnostic-handling-rules.md)  
  
-   [Rol del Administrador de controladores](../../../odbc/reference/develop-app/role-of-the-driver-manager.md)  
  
-   [Rol del controlador](../../../odbc/reference/develop-app/role-of-the-driver.md)
