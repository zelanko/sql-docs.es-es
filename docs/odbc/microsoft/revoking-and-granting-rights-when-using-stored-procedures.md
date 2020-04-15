---
title: Revocar y conceder derechos al usar procedimientos almacenados Microsoft Docs
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 469e6f0fdc6794e3bd163844e43821798aa4a617
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/14/2020
ms.locfileid: "81303991"
---
# <a name="revoking-and-granting-rights-when-using-stored-procedures"></a>Revocación y conceder derechos al usar procedimientos almacenados
> [!IMPORTANT]  
>  Esta característica se eliminará en una versión futura de Windows. Evite utilizar esta característica en nuevos trabajos de desarrollo y tenga previsto modificar las aplicaciones que actualmente la utilizan. En su lugar, utilice el controlador ODBC proporcionado por Oracle.  
  
 El controlador ODBC de Microsoft para Oracle devuelve el siguiente mensaje de error cuando se conceden derechos de usuario y, a continuación, se revocan en una tabla a la que tiene acceso un procedimiento almacenado:  
  
 SQL_ERROR-1  
  
 szErrorMsg"[Microsoft][Controlador ODBC para Oracle]Número incorrecto de parámetros"  
  
 szErrorMsg"[Microsoft][Controlador ODBC para Oracle]Error de sintaxis o violación de acceso"  
  
 La llamada a la función Odessp() de Oracle OCI falla en este escenario, pero es necesaria para implementar los parámetros predeterminados. Después de modificar los permisos de la tabla subyacente, el procedimiento almacenado debe volver a compilarse antes de volver a ejecutarlo.
