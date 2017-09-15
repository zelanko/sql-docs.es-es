---
title: Revocar y conceder derechos al usar procedimientos almacenados | Documentos de Microsoft
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
- stored procedures [ODBC], ODBC driver for Oracle
- ODBC driver for Oracle [ODBC], stored procedures
ms.assetid: 24070039-03ab-4623-a681-6308802eb399
caps.latest.revision: 8
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 67bad57e201d10c5eb29aafb19fa9f513c43b172
ms.contentlocale: es-es
ms.lasthandoff: 09/09/2017

---
# <a name="revoking-and-granting-rights-when-using-stored-procedures"></a>Revocación y conceder derechos al usar procedimientos almacenados
> [!IMPORTANT]  
>  Esta característica se quitará en una versión futura de Windows. Evite utilizar esta característica en nuevos trabajos de desarrollo y tenga previsto modificar las aplicaciones que actualmente la utilizan. En su lugar, utilice el controlador ODBC proporcionado por Oracle.  
  
 El controlador ODBC de Microsoft para Oracle devuelve el siguiente mensaje de error cuando se concede derechos de usuario y se revocar, a continuación, en una tabla que tiene acceso a un procedimiento almacenado:  
  
 SQL_ERROR =-1  
  
 szErrorMsg = "[Microsoft] [controlador ODBC para Oracle] número de parámetros incorrecto"  
  
 szErrorMsg = "[Microsoft] [controlador ODBC para Oracle] sintaxis o infracción de acceso"  
  
 La llamada a la función de Oracle OCI Odessp() se produce un error en este escenario, pero es necesaria para implementar los parámetros predeterminados. Después de modificaron los permisos de la tabla subyacente, se debe volver a compilar el procedimiento almacenado antes de ejecutar de nuevo.
