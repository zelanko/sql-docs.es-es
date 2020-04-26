---
title: Construcciones admitidas en procedimientos almacenados compilados de forma nativa | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: in-memory-oltp
ms.topic: conceptual
ms.assetid: 6b21f47e-bceb-4054-8b3c-9d39bb9583c0
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: cc064eb8a4c6b206d3b690a4c4e7ca196c7475dc
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/25/2020
ms.locfileid: "62467879"
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
  
## <a name="see-also"></a>Consulte también  
 [procedimientos almacenados compilados de forma nativa](natively-compiled-stored-procedures.md)  
  
  
