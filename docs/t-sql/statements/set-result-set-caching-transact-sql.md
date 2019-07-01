---
title: SET RESULT SET CACHING (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 05/03/2019
ms.prod: sql
ms.prod_service: sql-data-warehouse
ms.reviewer: jrasnick
ms.technology: t-sql
ms.topic: language-reference
f1_keywords: ''
dev_langs:
- TSQL
helpviewer_keywords: ''
author: XiaoyuL-Preview
ms.author: xiaoyul
manager: craigg
monikerRange: =azure-sqldw-latest || = sqlallproducts-allversions
ms.openlocfilehash: f9750cdc2dea7049bde77d31c275789691abf1b0
ms.sourcegitcommit: 3f2936e727cf8e63f38e5f77b33442993ee99890
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 06/21/2019
ms.locfileid: "67313814"
---
# <a name="set-result-set-caching-transact-sql"></a>SET RESULT SET CACHING (Transact-SQL) 

[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-xxx-md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-xxx-md.md)]

Controla el comportamiento de almacenamiento en caché para la sesión de cliente actual del conjunto de resultados.  

Se aplica a Azure SQL Data Warehouse, versión preliminar 
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis

```
SET RESULT_SET_CACHING { ON | OFF };
```  
  
## <a name="remarks"></a>Notas  

**ON**   
Habilita el almacenamiento en caché del conjunto de resultados para la sesión de cliente actual.  El almacenamiento en caché del conjunto de resultados no se puede activar en una sesión si está desactivado en el nivel de base de datos.

**OFF**   
Deshabilita el almacenamiento en caché del conjunto de resultados para la sesión de cliente actual.

## <a name="permissions"></a>Permisos

Debe pertenecer al rol público.

## <a name="see-also"></a>Vea también

[Instrucciones SET &#40;Transact-SQL&#41;](../../t-sql/statements/set-statements-transact-sql.md)</br>
[ALTER DATABASE &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-database-transact-sql?view=azure-sqldw-latest)