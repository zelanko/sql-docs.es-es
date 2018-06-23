---
title: Admite construcciones en procedimientos almacenados compilados de forma nativa | Documentos de Microsoft
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine-imoltp
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 6b21f47e-bceb-4054-8b3c-9d39bb9583c0
caps.latest.revision: 7
author: stevestein
ms.author: sstein
manager: jhubbard
ms.openlocfilehash: c54f811f2257adcb5c08f1741018be3211c1e874
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36203938"
---
# <a name="supported-constructs-on-natively-compiled-stored-procedures"></a>Construcciones admitidas en procedimientos almacenados compilados de forma nativa
  En este tema se enumeran las construcciones admitidas en procedimientos almacenados compilados de forma nativa.  
  
 Para obtener información sobre las construcciones no compatibles, vea [Construcciones Transact-SQL no admitidas por OLTP en memoria](transact-sql-constructs-not-supported-by-in-memory-oltp.md).  
  
## <a name="procedure-ddl"></a>Procedimiento DDL  
 Se admite lo siguiente:  
  
-   CREATE PROCEDURE  
  
-   DROP PROCEDURE  
  
-   SCHEMABINDING (se requiere para los procedimientos almacenados compilados de forma nativa)  
  
-   NATIVE_COMPILATION  
  
-   Es posible declarar los parámetros como NOT NULL.  
  
-   Parámetros con valores de tabla.  
  
## <a name="security"></a>Seguridad  
 Se admite lo siguiente:  
  
-   Para procedimientos: EXECUTE AS OWNER, SELF y usuario.  
  
-   GRANT (conceda) y DENY (deniegue) permisos a las tablas y los procedimientos.  
  
## <a name="see-also"></a>Vea también  
 [Procedimientos almacenados compilados de forma nativa](natively-compiled-stored-procedures.md)  
  
  