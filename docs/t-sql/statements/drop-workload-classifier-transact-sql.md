---
title: DROP WORKLOAD CLASSIFIER (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/13/2019
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
ms.assetid: ''
author: ronortloff
ms.author: rortloff
manager: craigg
monikerRange: =azure-sqldw-latest||=sqlallproducts-allversions
ms.openlocfilehash: a9ef53323d77f1439df5daf0fedc669fe380cb3f
ms.sourcegitcommit: 46a2c0ffd0a6d996a3afd19a58d2a8f4b55f93de
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/15/2019
ms.locfileid: "59581519"
---
# <a name="drop-workload-classifier-transact-sql-preview"></a>DROP WORKLOAD CLASSIFIER (Transact-SQL) (versión preliminar)

> [!Note]
> La clasificación de la carga de trabajo está disponible para versión preliminar en SQL Data Warehouse Gen2. La versión preliminar de clasificación e importancia de la administración de la carga de trabajo es para las compilaciones con una fecha de lanzamiento del 9 de abril de 2019 o posterior.  Los usuarios deben evitar usar compilaciones anteriores a esta fecha para pruebas de administración de la carga de trabajo.  Para determinar si la compilación es compatible con la administración de la carga de trabajo, ejecute @@version cuando se conecte a la instancia de SQL Data Warehouse.

[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-xxx-md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-xxx-md.md)]

Coloca un clasificador de administración de cargas de trabajo definido por el usuario existente.  
  
![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md).  
  
## <a name="syntax"></a>Sintaxis  

```
DROP WORKLOAD CLASSIFIER classifier_name;
```

## <a name="arguments"></a>Argumentos

*classifier_name*  
Especifica el nombre por el que se identifica el clasificador de carga de trabajo.  "classifier_name" es un elemento "sysname".  Puede tener hasta 128 caracteres y debe ser único en la instancia.
  
## <a name="remarks"></a>Notas

La instrucción DROP WORKLOAD CLASSIFIER no se permite en clasificadores de cargas de trabajo del sistema.

Si las solicitudes se ejecutan o están en la cola de solicitudes en estado suspendido, mantendrán su clasificación y el clasificador se podrá colocar inmediatamente.  El hecho de colocar y volver a crear el clasificador con una importancia distinta no afectará a una solicitud ya clasificada.

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
