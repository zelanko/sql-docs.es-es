---
title: CREATE WORKLOAD CLASSIFIER (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 05/01/2019
ms.prod: sql
ms.prod_service: sql-data-warehouse
ms.reviewer: jrasnick
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- WORKLOAD CLASSIFIER
- WORKLOAD_CLASSIFIER_TSQL
- CREATE WORKLOAD CLASSIFIER
- CREATE_WORKLOAD_CLASSIFIER_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- CREATE WORKLOAD CLASSIFIER statement
ms.assetid: ''
author: ronortloff
ms.author: rortloff
manager: craigg
monikerRange: =azure-sqldw-latest||=sqlallproducts-allversions
ms.openlocfilehash: 64235b77ea2e1cf2f2c4c8d8240f34ad2e8eab8b
ms.sourcegitcommit: bb5484b08f2aed3319a7c9f6b32d26cff5591dae
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/06/2019
ms.locfileid: "65090042"
---
# <a name="create-workload-classifier-transact-sql"></a>CREATE WORKLOAD CLASSIFIER (Transact-SQL)

[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-xxx-md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-xxx-md.md)]

Crea un clasificador de administración de cargas de trabajo.  El clasificador asigna las solicitudes entrantes a un grupo de cargas de trabajo y asigna una importancia según los parámetros especificados en la definición de la instrucción del clasificador.  Los clasificadores se evalúan con cada solicitud enviada.  Si una solicitud no coincide con un clasificador, se asigna al grupo de cargas de trabajo predeterminado.  El grupo de cargas de trabajo predeterminado es la clase de recurso smallrc.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md).  
  
## <a name="syntax"></a>Sintaxis

```
CREATE WORKLOAD CLASSIFIER classifier_name  
WITH  
    ( WORKLOAD_GROUP = 'name'  
     ,MEMBERNAME = 'security_account'
 [ [ , ] IMPORTANCE = { LOW | BELOW_NORMAL | NORMAL (default) | ABOVE_NORMAL | HIGH }])
[;]
```

## <a name="arguments"></a>Argumentos

 *classifier_name*  
 Especifica el nombre por el que se identifica el clasificador de carga de trabajo.  "classifier_name" es un elemento "sysname".  Puede tener hasta 128 caracteres y debe ser único en la instancia.

WORKLOAD_GROUP = *"name"*: si se cumplen las condiciones en las reglas de clasificador, "name" asigna la solicitud a un grupo de cargas de trabajo.  "name" es un elemento "sysname".  Puede tener hasta 128 caracteres y debe ser un nombre de grupo de cargas de trabajo válido en el momento de crear el clasificador.

WORKLOAD_GROUP debe asignarse a una clase de recursos existente:

|Clases de recursos estáticos|Clases de recursos dinámicos|
|------------------------|-----------------------|
|staticrc10|smallrc|
|staticrc20|mediumrc|
|staticrc30|largerc|
|staticrc40|xlargerc|
|staticrc50||
|staticrc60||
|staticrc70||
|staticrc80||

MEMBERNAME = *"security_account"*: se trata de la cuenta de seguridad que se va a agregar al rol.  "Security_account" es un elemento "sysname" y no tiene ningún valor predeterminado. "Security_account" puede ser un usuario o un rol de base de datos, el inicio de sesión de Azure Active Directory o un grupo de Azure Active Directory.

IMPORTANCE = { LOW | BELOW_NORMAL | NORMAL | ABOVE_NORMAL | HIGH } especifica la importancia relativa de una solicitud.  IMPORTANCE puede ser es uno de los siguientes valores:

- LOW
- BELOW_NORMAL
- NORMAL (valor predeterminado)
- ABOVE_NORMAL
- HIGH  

"Importance" influye en el orden en el que se programan las solicitudes, lo que da el primer acceso a los recursos y bloqueos.

Si un usuario es miembro de varios roles con diferentes clases de recursos asignados o coincidentes en varios clasificadores, el usuario tiene la asignación de clase de recursos más alta. Para obtener más información, vea la [clasificación de las cargas de trabajo](/azure/sql-data-warehouse/sql-data-warehouse-workload-classification#classification-precedence)

## <a name="permissions"></a>Permisos

 Requiere el permiso CONTROL DATABASE.  
  
## <a name="examples"></a>Ejemplos

 En el ejemplo siguiente se muestra cómo crear un clasificador de cargas de trabajo denominado `wgcELTRole`. Usa el grupo de cargas de trabajo staticrc20, el usuario `ELTRole` y establece la importancia en `above_normal`.

```sql
CREATE WORKLOAD CLASSIFIER wgcELTRole
  WITH (WORKLOAD_GROUP = 'staticrc20'
       ,MEMBERNAME = 'ELTRole'
      ,IMPORTANCE = above_normal);
```

## <a name="see-also"></a>Consulte también

[DROP WORKLOAD CLASSIFIER (Transact-SQL)](../../t-sql/statements/drop-workload-classifier-transact-sql.md)</br>
Vista de catálogo [sys.workload_management_workload_classifier_details](../../relational-databases/system-catalog-views/sys-workload-management-workload-classifier-details-transact-sql.md)</br>
Vista de catálogo [sys.workload_management_workload_classifiers](../../relational-databases/system-catalog-views/sys-workload-management-workload-classifiers-transact-sql.md)
[Clasificación de SQL Data Warehouse](/azure/sql-data-warehouse/classification)
