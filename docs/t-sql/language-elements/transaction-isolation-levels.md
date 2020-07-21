---
title: Niveles de aislamiento de transacción | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- locking [SQL Server], hints
- isolation levels [SQL Server], metadata access
- hints [SQL Server], locking
ms.assetid: 02bb71fa-1e92-4782-a9cf-6e256cc1f3ea
author: rothja
ms.author: jroth
ms.openlocfilehash: f1532197e46e0ad6ea314ec83acb46b841ed7b72
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/01/2020
ms.locfileid: "85731378"
---
# <a name="transaction-isolation-levels"></a>Niveles de aislamiento de transacción
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] no garantiza que se respeten las sugerencias de bloqueo en consultas que tengan acceso a metadatos por medio de vistas de catálogo, vistas de compatibilidad, vistas del esquema de información y funciones integradas de emisión de metadatos.  
  
 Internamente, [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] solo respeta el nivel de aislamiento READ COMMITTED para el acceso a metadatos. Si una transacción tiene un nivel de aislamiento que es, por ejemplo, SERIALIZABLE, y en la transacción se intenta obtener acceso a metadatos mediante vistas de catálogo o funciones integradas de emisión de metadatos, dichas consultas se ejecutan hasta que finalizan como READ COMMITTED. Sin embargo, en el aislamiento de instantánea, puede que el acceso a metadatos genere un error debido a operaciones DDL simultáneas. Esto se debe a que los metadatos no admiten versiones. Por tanto, puede que en el aislamiento de instantánea se genere un error al obtener acceso a:  
  
-   Vistas de catálogo  
  
-   Vistas de compatibilidad  
  
-   Vistas de esquema de información  
  
-   Funciones integradas de emisión de metadatos  
  
-   Grupo de procedimientos almacenados **sp_help**  
  
-   Procedimientos de catálogo de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client  
  
-   Funciones y vistas de administración dinámica  
  
 Para más información sobre los niveles de aislamiento, vea [SET TRANSACTION ISOLATION LEVEL &#40;Transact-SQL&#41;](../../t-sql/statements/set-transaction-isolation-level-transact-sql.md).  
  
 En la siguiente tabla se proporciona un resumen de acceso a metadatos en distintos niveles de aislamiento.  
  
|Nivel de aislamiento|Compatible|Respetado|  
|---------------------|---------------|-------------|  
|READ UNCOMMITTED|No|Sin garantizar|  
|READ COMMITTED|Sí|Sí|  
|REPEATABLE READ|No|No|  
|SNAPSHOT ISOLATION|No|No|  
|SERIALIZABLE|No|No|  
  
  
