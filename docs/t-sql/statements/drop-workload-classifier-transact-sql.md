---
title: DROP WORKLOAD CLASSIFIER (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 11/04/2019
ms.prod: sql
ms.prod_service: sql-data-warehouse
ms.reviewer: jrasnick
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- WORKLOAD CLASSIFIER
- WORKLOAD_CLASSIFIER_TSQL
- DROP_WORKLOAD_CLASSIFIER_TSQL
- DROP WORKLOAD GROUP
dev_langs:
- TSQL
helpviewer_keywords:
- DROP WORKLOAD CLASSIFIER statement
author: ronortloff
ms.author: rortloff
monikerRange: =azure-sqldw-latest||=sqlallproducts-allversions
ms.openlocfilehash: 5db3c50e4b0a21e2e1acf9512995870b62375dd8
ms.sourcegitcommit: 66dbc3b740f4174f3364ba6b68bc8df1e941050f
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 11/05/2019
ms.locfileid: "73632834"
---
# <a name="drop-workload-classifier-transact-sql"></a>DROP WORKLOAD CLASSIFIER (Transact-SQL)

[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-xxx-md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-xxx-md.md)]

Coloca un clasificador de administración de cargas de trabajo definido por el usuario existente.  Si las solicitudes se ejecutan o están en la cola de solicitudes en estado suspendido, mantendrán su clasificación y el clasificador se podrá colocar inmediatamente. El hecho de colocar y volver a crear el clasificador con una importancia distinta no afectará a una solicitud ya clasificada.
  
![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo a temas") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md).  
  
## <a name="syntax"></a>Sintaxis  

```
DROP WORKLOAD CLASSIFIER classifier_name;
```

## <a name="arguments"></a>Argumentos

*classifier_name*  
Especifica el nombre por el que se identifica el clasificador de carga de trabajo.
  
## <a name="permissions"></a>Permisos

Requiere el permiso CONTROL DATABASE.  
  
## <a name="examples"></a>Ejemplos

En el ejemplo siguiente se coloca el clasificador de cargas de trabajo denominado `wgcELTROLE`.  

```sql
DROP WORKLOAD CLASSIFIER wgcELTRole;
```

> [!NOTE]
> Una solicitud enviada sin un clasificador coincidente se clasificará en el grupo de cargas de trabajo predeterminado.  El grupo de cargas de trabajo predeterminado es la clase de recurso smallrc.
  
## <a name="see-also"></a>Consulte también

[CREATE WORKLOAD CLASSIFIER (Transact-SQL)](../../t-sql/statements/create-workload-classifier-transact-sql.md)</br>
[Clasificación de cargas de trabajo de SQL Data Warehouse](/azure/sql-data-warehouse/sql-data-warehouse-workload-classification)
