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
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 0544fe096d75f4dfe64f4501b62948193abaf25a
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 10/01/2018
ms.locfileid: "47626853"
---
# <a name="transaction-isolation-levels"></a>Niveles de aislamiento de transacción
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

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
  
|Nivel de aislamiento|Admitida|Respetado|  
|---------------------|---------------|-------------|  
|READ UNCOMMITTED|no|Sin garantizar|  
|READ COMMITTED|Sí|Sí|  
|REPEATABLE READ|no|no|  
|SNAPSHOT ISOLATION|no|no|  
|SERIALIZABLE|no|no|  
  
  
