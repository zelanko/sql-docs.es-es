---
title: sp_help (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 10/24/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_help
- sp_help_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_help
ms.assetid: 913cd5d4-39a3-4a4b-a926-75ed32878884
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 39a1e699b52b29db74209aa5288bb5dc01896a3b
ms.sourcegitcommit: cff8dd63959d7a45c5446cadf1f5d15ae08406d8
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/05/2019
ms.locfileid: "67586244"
---
# <a name="sphelp-transact-sql"></a>sp_help (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Proporciona información acerca de un objeto de base de datos (todos los objetos enumerados en la **sys.sysobjects** vista de compatibilidad), un tipo de datos definido por el usuario o un tipo de datos.  
  
 
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
sp_help [ [ @objname = ] 'name' ]  
```  
  
## <a name="arguments"></a>Argumentos  
`[ @objname = ] 'name'` Es el nombre de cualquier objeto, en **sysobjects** o cualquier dato definido por el usuario escriba en el **systypes** tabla. *nombre* es **nvarchar (** 776 **)** , su valor predeterminado es null. No se aceptan nombres de bases de datos.  Se deben delimitar dos o tres nombres de partes, como "Person.AddressType" o [Person.AddressType].   
   
  
## <a name="return-code-values"></a>Valores de código de retorno  
 0 (correcto) o 1 (error)  
  
## <a name="result-sets"></a>Conjuntos de resultados  
 Los conjuntos de resultados devueltos dependen de si *nombre* está especificado, cuando se especifica y es el objeto de base de datos.  
  
1.  Si **sp_help** se ejecuta sin argumentos, se devuelve información de resumen de los objetos de todos los tipos que existen en la base de datos actual.  
  
    |Nombre de columna|Tipo de datos|Descripción|  
    |-----------------|---------------|-----------------|  
    |**Name**|**nvarchar(** 128 **)**|Nombre del objeto|  
    |**Propietario**|**nvarchar(** 128 **)**|Propietario del objeto (esta es la entidad de seguridad de base de datos que posee el objeto. De forma predeterminada, es el propietario del esquema que contiene el objeto).|  
    |**Object_type**|**nvarchar(** 31 **)**|Tipo de objeto|  
  
2.  Si *nombre* es un [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tipo de datos o tipo de datos definido por el usuario, **sp_help** devuelve este conjunto de resultados.  
  
    |Nombre de columna|Tipo de datos|Descripción|  
    |-----------------|---------------|-----------------|  
    |**Type_name**|**nvarchar(** 128 **)**|Nombre del tipo de datos.|  
    |**Storage_type**|**nvarchar(** 128 **)**|Nombre del tipo de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
    |**Longitud**|**smallint**|Longitud física del tipo de datos (en bytes).|  
    |**Prec**|**int**|Precisión (número total de dígitos).|  
    |**Escala**|**int**|Número de dígitos a la derecha del separador decimal.|  
    |**Admisión de valores NULL**|**varchar(** 35 **)**|Indica si se permiten valores NULL: Sí o no.|  
    |**Default_name**|**nvarchar(** 128 **)**|Nombre de un valor predeterminado enlazado a este tipo.<br /><br /> NULL = No hay un valor predeterminado enlazado.|  
    |**Rule_name**|**nvarchar(** 128 **)**|Nombre de una regla enlazada a este tipo.<br /><br /> NULL = No hay un valor predeterminado enlazado.|  
    |**Intercalación**|**sysname**|Intercalación del tipo de datos. NULL para tipos de datos que no sean de caracteres.|  
  
3.  Si *nombre* es cualquier objeto de base de datos que no sea un tipo de datos, **sp_help** devuelve este resultado conjuntos de resultados establecido y también adicionales, según el tipo del objeto especificado.  

[!INCLUDE[freshInclude](../../includes/paragraph-content/fresh-note-steps-feedback.md)]

    |Nombre de columna|Tipo de datos|Descripción|  
    |-----------------|---------------|-----------------|  
    |**Name**|**nvarchar(** 128 **)**|Nombre de la tabla|  
    |**Propietario**|**nvarchar(** 128 **)**|Propietario de la tabla.|  
    |**Tipo**|**nvarchar(** 31 **)**|Tipo de tabla.|  
    |**Created_datetime**|**datetime**|Tabla de fechas creado|  
  
     Depending on the database object specified, **sp_help** returns additional result sets.  
  
     If *name* is a system table, user table, or view, **sp_help** returns the following result sets. However, the result set that describes where the data file is located on a file group is not returned for a view.  
  
    -   Conjunto de resultados adicional devuelto en los objetos de columna:  
  
        |Nombre de columna|Tipo de datos|Descripción|  
        |-----------------|---------------|-----------------|  
        |**Column_name**|**nvarchar(** 128 **)**|Nombre de columna.|  
        |**Tipo**|**nvarchar(** 128 **)**|Tipo de datos de la columna.|  
        |**Calculado**|**varchar(** 35 **)**|Indica si se calculan los valores de la columna: Sí o no.|  
        |**Longitud**|**int**|Longitud de la columna en bytes.<br /><br /> Nota: Si el tipo de datos de columna es un tipo de valor grande (**varchar (max)** , **nvarchar (max)** , **varbinary (max)** , o **xml**), el valor será se mostrará como -1.|  
        |**Prec**|**char(** 5 **)**|Precisión de columna.|  
        |**Escala**|**char(** 5 **)**|Escala de la columna.|  
        |**Admisión de valores NULL**|**varchar(** 35 **)**|Indica si se permiten valores NULL en la columna: Sí o no.|  
        |**TrimTrailingBlanks**|**varchar(** 35 **)**|Recorta los espacios en blanco finales. Devuelve Yes o No.|  
        |**FixedLenNullInSource**|**varchar(** 35 **)**|Se conserva únicamente por compatibilidad con versiones anteriores.|  
        |**Intercalación**|**sysname**|Intercalación de la columna. NULL para los tipos de datos que no son caracteres.|  
  
    -   Conjunto de resultados adicional devuelto en las columnas de identidad:  
  
        |Nombre de columna|Tipo de datos|Descripción|  
        |-----------------|---------------|-----------------|  
        |**Identidad**|**nvarchar(** 128 **)**|Nombre de la columna cuyo tipo de datos se declara como identidad.|  
        |**Valor de inicialización**|**numeric**|Valor inicial de la columna de identidad.|  
        |**Incremento**|**numeric**|Incremento que se va a utilizar en los valores de esta columna.|  
        |**No disponible para replicación**|**int**|Propiedad IDENTITY no se aplica cuando un inicio de sesión de replicación, como **sqlrepl**, inserta datos en la tabla:<br /><br /> 1 = True<br /><br /> 0 = False|  
  
    -   Conjunto de resultados adicional devuelto en las columnas:  
  
        |Nombre de columna|Tipo de datos|Descripción|  
        |-----------------|---------------|-----------------|  
        |**RowGuidCol**|**sysname**|Nombre de la columna de identificador único global.|  
  
    -   Conjunto de resultados adicional devuelto en los grupos de archivos:  
  
        |Nombre de columna|Tipo de datos|Descripción|  
        |-----------------|---------------|-----------------|  
        |**Data_located_on_filegroup**|**nvarchar(** 128 **)**|En el que se encuentran los datos del grupo de archivos: Principal, secundario o registro de transacciones.|  
  
    -   Conjunto de resultados adicional devuelto en los índices:  
  
        |Nombre de columna|Tipo de datos|Descripción|  
        |-----------------|---------------|-----------------|  
        |**index_name**|**sysname**|Nombre del índice.|  
        |**Index_description**|**varchar(** 210 **)**|Descripción del índice.|  
        |**index_keys**|**nvarchar(** 2078 **)**|Nombres de las columnas en las que se ha generado el índice. Devuelve NULL para los índices de almacén de columnas optimizados de memoria xVelocity.|  
  
    -   Conjunto de resultados adicional devuelto en las restricciones:  
  
        |Nombre de columna|Tipo de datos|Descripción|  
        |-----------------|---------------|-----------------|  
        |**constraint_type**|**nvarchar(** 146 **)**|Tipo de restricción.|  
        |**constraint_name**|**nvarchar(** 128 **)**|Nombre de la restricción.|  
        |**delete_action**|**nvarchar(** 9 **)**|Indica si la acción DELETE es: NO_ACTION, CASCADE, SET_NULL, SET_DEFAULT o N/A.<br /><br /> Solo se aplica a las restricciones FOREIGN KEY.|  
        |**update_action**|**nvarchar(** 9 **)**|Indica si la acción UPDATE es: NO_ACTION, CASCADE, SET_NULL, SET_DEFAULT o N/A.<br /><br /> Solo se aplica a las restricciones FOREIGN KEY.|  
        |**status_enabled**|**varchar(** 8 **)**|Indica si la restricción está habilitada: Habilitado, Disabled o N/A.<br /><br /> Solo se aplica a las restricciones CHECK y FOREIGN KEY.|  
        |**status_for_replication**|**varchar(** 19 **)**|Indica si la restricción es para replicación.<br /><br /> Solo se aplica a las restricciones CHECK y FOREIGN KEY.|  
        |**constraint_keys**|**nvarchar(** 2078 **)**|Nombres de las columnas que componen la restricción o, en el caso de valores predeterminados y reglas, el texto que define el valor predeterminado o la regla.|  
  
    -   Conjunto de resultados adicional devuelto en los objetos de referencia:  
  
        |Nombre de columna|Tipo de datos|Descripción|  
        |-----------------|---------------|-----------------|  
        |**Tabla hace referencia**|**nvarchar(** 516 **)**|Identifica otros objetos de base de datos que hacen referencia a la tabla.|  
  
    -   Conjunto de resultados adicional devuelto en los procedimientos almacenados, las funciones o los procedimientos almacenados extendidos.  
  
        |Nombre de columna|Tipo de datos|Descripción|  
        |-----------------|---------------|-----------------|  
        |**Nombre de parámetro**|**nvarchar(** 128 **)**|Nombre del parámetro del procedimiento almacenado.|  
        |**Tipo**|**nvarchar(** 128 **)**|Tipo de datos del parámetro del procedimiento almacenado.|  
        |**Longitud**|**smallint**|Longitud máxima de almacenamiento físico en bytes.|  
        |**Prec**|**int**|Precisión o número total de dígitos.|  
        |**Escala**|**int**|Número de dígitos a la derecha del separador decimal.|  
        |**Param_order**|**smallint**|Orden del parámetro.|  
  
## <a name="remarks"></a>Comentarios  
 El **sp_help** procedimiento busca un objeto solo la base de datos actual.  
  
 Cuando *nombre* no se especifica, **sp_help** listas objeto nombres, propietarios y tipos de objeto para todos los objetos de la base de datos actual. **sp_helptrigger** proporciona información acerca de los desencadenadores.  
  
 **sp_help** expone solo las columnas de índice ordenable; por lo tanto, no expone información sobre los índices XML o índices espaciales.  
  
## <a name="permissions"></a>Permisos  
 Debe pertenecer al rol **public** . El usuario debe tener al menos un permiso *objname*. Para ver claves de restricción de columna, valores predeterminados o reglas, debe tener el permiso VIEW DEFINITION en la tabla.  
  
## <a name="examples"></a>Ejemplos  
  
### <a name="a-returning-information-about-all-objects"></a>A. Devolver información acerca de todos los objetos  
 En el siguiente ejemplo se presenta información acerca de cada objeto de la base de datos `master`.  
  
```  
USE master;  
GO  
EXEC sp_help;  
GO  
```  
  
### <a name="b-returning-information-about-a-single-object"></a>b. Devolver información acerca de un solo objeto  
 En el siguiente ejemplo se presenta información acerca de la tabla `Person`.  
  
```  
USE AdventureWorks2012;  
GO  
EXEC sp_help 'Person.Person';  
GO  
```  
  
## <a name="see-also"></a>Vea también  
 [Procedimientos almacenados del motor de base de datos &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/database-engine-stored-procedures-transact-sql.md)   
 [sp_helpindex &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helpindex-transact-sql.md)   
 [sp_helprotect &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helprotect-transact-sql.md)   
 [sp_helpserver &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helpserver-transact-sql.md)   
 [sp_helptrigger &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helptrigger-transact-sql.md)   
 [sp_helpuser &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helpuser-transact-sql.md)   
 [Procedimientos almacenados del sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [sys.sysobjects &#40;Transact-SQL&#41;](../../relational-databases/system-compatibility-views/sys-sysobjects-transact-sql.md)  
  
  
