---
title: Construcciones admitidas en procedimientos almacenados compilados de forma nativa | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: in-memory-oltp
ms.topic: conceptual
ms.assetid: 6b21f47e-bceb-4054-8b3c-9d39bb9583c0
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 0c439a424c409522eee696d0161c94251e82fb35
ms.sourcegitcommit: b72c9fc9436c44c6a21fd96223c73bf94706c06b
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/01/2020
ms.locfileid: "82718818"
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
  
  
