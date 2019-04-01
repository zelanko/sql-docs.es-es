---
title: ADD SENSITIVITY CLASSIFICATION (Transact-SQL) | Microsoft Docs
ms.date: 03/25/2019
ms.reviewer: ''
ms.prod: sql
ms.technology: t-sql
ms.topic: language-reference
ms.custom: ''
ms.manager: craigg
ms.author: giladm
author: giladmit
f1_keywords:
- ADD SENSITIVITY CLASSIFICATION
- ADD_SENSITIVITY_CLASSIFICATION
dev_langs:
- TSQL
helpviewer_keywords:
- ADD SENSITIVITY CLASSIFICATION statement
- add labels
- adding labels
- adding labels
- classification [SQL]
- labels [SQL]
- information types
- data classification
monikerRange: = azuresqldb-current || = sqlallproducts-allversions
ms.openlocfilehash: 9e4fee7a2504255b0763cf9cfad708fd341d336d
ms.sourcegitcommit: 2db83830514d23691b914466a314dfeb49094b3c
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 03/27/2019
ms.locfileid: "58494067"
---
# <a name="add-sensitivity-classification-transact-sql"></a>ADD SENSITIVITY CLASSIFICATION (Transact-SQL)
[!INCLUDE[tsql-appliesto-xxxxxx-asdb-asdw-xxx-md](../../includes/tsql-appliesto-xxxxxx-asdb-asdw-xxx-md.md)]

Agrega metadatos sobre la clasificación de confidencialidad a una o varias columnas de base de datos. La clasificación puede incluir una etiqueta de confidencialidad y un tipo de información.  

La clasificación de datos confidenciales en su entorno de base de datos le ayuda a lograr mayor visibilidad y una mejor protección. Puede encontrar información adicional en [Clasificación y detección de datos de Azure SQL Database](https://aka.ms/sqlip).

## <a name="syntax"></a>Sintaxis  

```sql
ADD SENSITIVITY CLASSIFICATION TO
    <object_name> [, ...n ]
    WITH ( <sensitivity_label_option> [, ...n ] )     

<object_name> ::=
{
    [schema_name.]table_name.column_name
}

<sensitivity_label_option> ::=  
{   
    LABEL = string |
    LABEL_ID = guidOrString |
    INFORMATION_TYPE = string |
    INFORMATION_TYPE_ID = guidOrString  
}
```  

## <a name="arguments"></a>Argumentos  

*object_name* ([schema_name.]table_name.column_name)

Es el nombre de la columna de base de datos que se va a clasificar. Actualmente solo se admite la clasificación de columnas.
    - *schema_name* (opcional): es el nombre del esquema al que pertenece la columna clasificada.
    - *table_name*: es el nombre de la tabla a la que pertenece la columna clasificada.
    - *column_name*: es el nombre de la columna que se va a clasificar.

*LABEL*

Es el nombre legible de la etiqueta de confidencialidad. Las etiquetas de confidencialidad representan la confidencialidad de los datos almacenados en la columna de base de datos.

*LABEL_ID*

Es un identificador asociado a la etiqueta de confidencialidad. A menudo se usa con plataformas de protección de información centralizadas para identificar etiquetas de forma única en el sistema.

*INFORMATION_TYPE*

Es el nombre legible del tipo de información. Los tipos de información se utilizan para describir el tipo de datos que se almacenan en la columna de base de datos.

*INFORMATION_TYPE_ID*

Es un identificador asociado con el tipo de información. A menudo se usa con plataformas de protección de información centralizadas para identificar tipos de información de forma única en el sistema.


## <a name="remarks"></a>Notas  

- Solo se puede agregar una clasificación a un único objeto. La adición de una clasificación a un objeto que ya está clasificado sobrescribirá la clasificación existente.
- Se pueden clasificar varios objetos con una sola instrucción `ADD SENSITIVITY CLASSIFICATION`.
- La vista del sistema [sys.sensitivity_classifications](../../relational-databases/system-catalog-views/sys-sensitivity-classifications-transact-sql.md) puede usarse para recuperar la información de clasificación de confidencialidad para una base de datos.


## <a name="permissions"></a>Permisos

Requiere el permiso ALTER ANY SENSITIVITY CLASSIFICATION. ALTER ANY SENSITIVITY CLASSIFICATION está implícito en el permiso de base de datos ALTER, o en el permiso de servidor CONTROL SERVER.


## <a name="examples"></a>Ejemplos  

### <a name="a-classifying-two-columns"></a>A. Clasificación de dos columnas

El ejemplo siguiente se clasifican las columnas **dbo.sales.price** y **dbo.sales.discount** con la etiqueta de confidencialidad **Highly Confidential** y el tipo de información **Financial**.

```sql
ADD SENSITIVITY CLASSIFICATION TO
    dbo.sales.price, dbo.sales.discount
    WITH ( LABEL='Highly Confidential', INFORMATION_TYPE='Financial' )
```  

### <a name="b-classifying-only-a-label"></a>B. Clasificación de solo una etiqueta
En el ejemplo siguiente se clasifica la columna **dbo.customer.comments** con la etiqueta **Confidential** y el identificador de etiqueta **643f7acd-776a-438d-890c-79c3f2a520d6**. El tipo de información no está clasificado en esta columna.

```sql
ADD SENSITIVITY CLASSIFICATION TO
    dbo.customer.comments
    WITH ( LABEL='Confidential', LABEL_ID='643f7acd-776a-438d-890c-79c3f2a520d6' )
```  

## <a name="see-also"></a>Consulte también  

[DROP SENSITIVITY CLASSIFICATION (Transact-SQL)](../../t-sql/statements/drop-sensitivity-classification-transact-sql.md)

[sys.sensitivity_classifications (Transact-SQL)](../../relational-databases/system-catalog-views/sys-sensitivity-classifications-transact-sql.md)

[Permisos (motor de base de datos)](https://docs.microsoft.com/sql/relational-databases/security/permissions-database-engine)

[Clasificación y detección de datos de Azure SQL Database](https://aka.ms/sqlip)
