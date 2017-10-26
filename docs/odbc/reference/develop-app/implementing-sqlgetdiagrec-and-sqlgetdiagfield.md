---
title: Implementar SQLGetDiagRec y SQLGetDiagField | Documentos de Microsoft
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- diagnostic information [ODBC], SqlGetDiagField
- SQLGetDiagField function [ODBC], and SQLGetDiagRec
- SQLGetDiagRec function [ODBC], and SQLGetDiagField
- diagnostic information [ODBC], SqlGetDiagRec
- retrieving diagnostic information [ODBC]
ms.assetid: 11ba1857-b533-4517-8131-a2a8a0154a0a
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 463ddfe552c94a9e90ceb2a24f8061674955979d
ms.contentlocale: es-es
ms.lasthandoff: 09/09/2017

---
# <a name="implementing-sqlgetdiagrec-and-sqlgetdiagfield"></a>Implementar SQLGetDiagRec y SQLGetDiagField
**SQLGetDiagRec** y **SQLGetDiagField** se implementan mediante el Administrador de controladores y cada controlador. El Administrador de controladores y cada controlador mantienen registros de diagnóstico para cada entorno, la conexión, la instrucción y el identificador de descriptor y liberan esos registros sólo cuando se llama a otra función con que identificador o el identificador se libera.  
  
 Aunque el Administrador de controladores y cada controlador deben determinar el primer registro de estado según los criterios de clasificación en [secuencia de registros de estado](../../../odbc/reference/develop-app/sequence-of-status-records.md), el Administrador de controladores determina la secuencia final de registros.  
  
 **SQLGetDiagRec** y **SQLGetDiagField** no registrar registros de diagnóstico sobre sí mismos.  
  
 Esta sección contiene los temas siguientes.  
  
-   [Reglas de control de diagnóstico](../../../odbc/reference/develop-app/diagnostic-handling-rules.md)  
  
-   [Rol del Administrador de controladores](../../../odbc/reference/develop-app/role-of-the-driver-manager.md)  
  
-   [Rol del controlador](../../../odbc/reference/develop-app/role-of-the-driver.md)

