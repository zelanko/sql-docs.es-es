---
title: ORIGINAL_DB_NAME (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- ORIGINAL_DB_NAME
- ORIGINAL_DB_NAME_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- ORIGINAL_DB_NAME function
ms.assetid: 7dadc40a-1287-4f31-8487-434ee477144d
author: VanMSFT
ms.author: vanto
manager: craigg
ms.openlocfilehash: ff466a1bd10035ba1dad5bc95a3e67252a1e771e
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "65944777"
---
# <a name="originaldbname-transact-sql"></a>ORIGINAL_DB_NAME (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Devuelve el nombre de la base de datos especificada por el usuario en la cadena de conexión de la base de datos. Esta base de datos se especifica mediante la opción **sqlcmd-d** (USE *database*). También puede especificarse con la expresión de origen de datos Open Database Connectivity (ODBC) (initial catalog =*databasename*).  
  
 Esta base de datos no es la misma que la base de datos de usuario predeterminada.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
ORIGINAL_DB_NAME ()  
```  
  
## <a name="remarks"></a>Notas  
 Si no se especifica la base de datos inicial, la función devuelve una cadena vacía.  
  
## <a name="see-also"></a>Consulte también  
 [sqlcmd (utilidad)](../../tools/sqlcmd-utility.md)   
 [osql Utility](../../tools/osql-utility.md)  (Utilidad osql)  
 [SQL Server Native Client (ODBC)](../../relational-databases/native-client/odbc/sql-server-native-client-odbc.md)  
  
  
