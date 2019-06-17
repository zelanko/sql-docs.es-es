---
title: Revocación y conceder derechos al usar procedimientos almacenan | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- stored procedures [ODBC], ODBC driver for Oracle
- ODBC driver for Oracle [ODBC], stored procedures
ms.assetid: 24070039-03ab-4623-a681-6308802eb399
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: e881201e4653a168faff2fa438be19c1ca37e9b1
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "63127967"
---
# <a name="revoking-and-granting-rights-when-using-stored-procedures"></a>Revocación y conceder derechos al usar procedimientos almacenados
> [!IMPORTANT]  
>  Esta característica se quitará en una versión futura de Windows. Evite utilizar esta característica en nuevos trabajos de desarrollo y tenga previsto modificar las aplicaciones que actualmente la utilizan. En su lugar, use el controlador ODBC proporcionado por Oracle.  
  
 El controlador ODBC de Microsoft para Oracle devuelve el siguiente mensaje de error cuando se conceden derechos de usuario y se revocar, a continuación, en una tabla que tiene acceso a un procedimiento almacenado:  
  
 SQL_ERROR=-1  
  
 szErrorMsg = "[Microsoft] [controlador ODBC para Oracle] número de parámetros incorrecto"  
  
 szErrorMsg = "[Microsoft] [controlador ODBC para Oracle] sintaxis o infracción de acceso"  
  
 La llamada a la función de Oracle OCI Odessp() se produce un error en este escenario, pero es necesaria para implementar los parámetros predeterminados. Después de modificaron los permisos de la tabla subyacente, se debe volver a compilar el procedimiento almacenado antes de ejecutarlo de nuevo.
