---
title: sp_help (Transact-SQL) | Documentos de Microsoft
ms.custom: 
ms.date: 10/24/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: system-stored-procedures
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sp_help
- sp_help_TSQL
dev_langs: TSQL
helpviewer_keywords: sp_help
ms.assetid: 913cd5d4-39a3-4a4b-a926-75ed32878884
caps.latest.revision: "60"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Active
ms.openlocfilehash: 4df2325ef2da29b60ca4f1e7109dd73ff9530ea2
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/21/2017
---
# <a name="sphelp-transact-sql"></a>sp_help (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Ofrece información acerca de un objeto de base de datos (todos los objetos enumerados en la **sys.sysobjects** vista de compatibilidad), un tipo de datos definido por el usuario o un tipo de datos.  
  
 
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
sp_help [ [ @objname = ] 'name' ]  
```  
  
## <a name="arguments"></a>Argumentos  
 [  **@objname=**] **'***nombre***'**  
 Es el nombre de cualquier objeto en **sysobjects** o tipo de los datos definidos por el usuario en el **systypes** tabla. *nombre* es **nvarchar (**776**)**, su valor predeterminado es null. No se aceptan nombres de bases de datos.  Nombres de partes de dos o tres deben delimitarse, como 'Person.AddressType' o [Person.AddressType].   
   
  
## <a name="return-code-values"></a>Valores de código de retorno  
 0 (correcto) o 1 (error)  
  
## <a name="result-sets"></a>Conjuntos de resultados  
 Los conjuntos de resultados devueltos dependen de si *nombre* está especificada, cuando se especifica, y qué objeto de base de datos es.  
  
1.  Si **sp_help** se ejecuta sin argumentos, se devuelve información de resumen de los objetos de todos los tipos que existen en la base de datos actual.  
  
    |Nombre de columna|Tipo de datos|Description|  
    |-----------------|---------------|-----------------|  
    |**Nombre**|**nvarchar (**128**)**|Nombre del objeto|  
    |**Propietario**|**nvarchar (**128**)**|Propietario del objeto (esta es la entidad de seguridad de base de datos que posee el objeto. De forma predeterminada, es el propietario del esquema que contiene el objeto).|  
    |**Object_type**|**nvarchar (**31**)**|Tipo de objeto|  
  
2.  Si *nombre* es un [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tipo de datos o tipo de datos definido por el usuario, **sp_help** devuelve este conjunto de resultados.  
  
    |Nombre de columna|Tipo de datos|Description|  
    |-----------------|---------------|-----------------|  
    |**Type_name**|**nvarchar (**128**)**|Nombre del tipo de datos.|  
    |**Storage_type**|**nvarchar (**128**)**|Nombre del tipo de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
    |**Longitud**|**smallint**|Longitud física del tipo de datos (en bytes).|  
    |**Prec**|**int**|Precisión (número total de dígitos).|  
    |**Escala**|**int**|Número de dígitos a la derecha del separador decimal.|  
    |**Admisión de valores NULL**|**varchar (**35**)**|Indica si se permiten valores NULL: Yes o No.|  
    |**Default_name**|**nvarchar (**128**)**|Nombre de un valor predeterminado enlazado a este tipo.<br /><br /> NULL = No hay un valor predeterminado enlazado.|  
    |**Rule_name**|**nvarchar (**128**)**|Nombre de una regla enlazada a este tipo.<br /><br /> NULL = No hay un valor predeterminado enlazado.|  
    |**Intercalación**|**sysname**|Intercalación del tipo de datos. NULL para tipos de datos que no sean de caracteres.|  
  
3.  Si *nombre* es cualquier objeto de base de datos que no sea un tipo de datos, **sp_help** devuelve este resultado conjuntos de resultados de conjunto y también adicional, según el tipo de objeto especificado.  
  
    |Nombre de columna|Tipo de datos|Description|  
    |-----------------|---------------|-----------------|  
    |**Nombre**|**nvarchar (**128**)**|Nombre de la tabla|  
    |**Propietario**|**nvarchar (**128**)**|Propietario de la tabla.|  
    |**Tipo**|**nvarchar (**31**)**|Tipo de tabla.|  
    |**Created_datetime**|**datetime**|Tabla de fecha creada|  
  
     Según el objeto de base de datos especificado, **sp_help** devuelve conjuntos de resultados adicionales.  
  
     Si *nombre* es una tabla del sistema, la tabla de usuario o la vista, **sp_help** devuelve los siguientes conjuntos de resultados. No obstante, el conjunto de resultados que describe la ubicación del archivo de datos en un grupo de archivos no se devuelve para una vista.  
  
    -   Conjunto de resultados adicional devuelto en los objetos de columna:  
  
        |Nombre de columna|Tipo de datos|Description|  
        |-----------------|---------------|-----------------|  
        |**Column_name**|**nvarchar (**128**)**|Nombre de columna.|  
        |**Tipo**|**nvarchar (**128**)**|Tipo de datos de la columna.|  
        |**Calculado**|**varchar (**35**)**|Indica si los valores de la columna son calculados: Yes o No.|  
        |**Longitud**|**int**|Longitud de la columna en bytes.<br /><br /> Nota: Si el tipo de datos de columna es un tipo de valor grande (**varchar (max)**, **nvarchar (max)**, **varbinary (max)**, o **xml**), el valor será se mostrará como -1.|  
        |**Prec**|**Char (**5**)**|Precisión de la columna.|  
        |**Escala**|**Char (**5**)**|Escala de la columna.|  
        |**Admisión de valores NULL**|**varchar (**35**)**|Indica si se permiten valores NULL en la columna: Yes o No.|  
        |**TrimTrailingBlanks**|**varchar (**35**)**|Recorta los espacios en blanco finales. Devuelve Yes o No.|  
        |**FixedLenNullInSource**|**varchar (**35**)**|Se conserva únicamente por compatibilidad con versiones anteriores.|  
        |**Intercalación**|**sysname**|Intercalación de la columna. NULL para los tipos de datos.|  
  
    -   Conjunto de resultados adicional devuelto en las columnas de identidad:  
  
        |Nombre de columna|Tipo de datos|Description|  
        |-----------------|---------------|-----------------|  
        |**Identidad**|**nvarchar (**128**)**|Nombre de la columna cuyo tipo de datos se declara como identidad.|  
        |**Valor de inicialización**|**numeric**|Valor inicial de la columna de identidad.|  
        |**Incremento**|**numeric**|Incremento que se va a utilizar en los valores de esta columna.|  
        |**No disponible para replicación**|**int**|Propiedad IDENTITY no se aplica cuando un inicio de sesión de replicación, como **sqlrepl**, inserta datos en la tabla:<br /><br /> 1 = True<br /><br /> 0 = False|  
  
    -   Conjunto de resultados adicional devuelto en las columnas:  
  
        |Nombre de columna|Tipo de datos|Description|  
        |-----------------|---------------|-----------------|  
        |**RowGuidCol**|**sysname**|Nombre de la columna de identificador único global.|  
  
    -   Conjunto de resultados adicional devuelto en los grupos de archivos:  
  
        |Nombre de columna|Tipo de datos|Description|  
        |-----------------|---------------|-----------------|  
        |**Data_located_on_filegroup**|**nvarchar (**128**)**|Grupo de archivos en el que se encuentran los datos: Principal, Secundario o Registro de transacciones.|  
  
    -   Conjunto de resultados adicional devuelto en los índices:  
  
        |Nombre de columna|Tipo de datos|Description|  
        |-----------------|---------------|-----------------|  
        |**index_name**|**sysname**|Nombre del índice.|  
        |**Index_description**|**varchar (**210**)**|Descripción del índice.|  
        |**index_keys**|**nvarchar (**2078**)**|Nombres de las columnas en las que se ha generado el índice. Devuelve NULL para los índices de almacén de columnas optimizados de memoria xVelocity.|  
  
    -   Conjunto de resultados adicional devuelto en las restricciones:  
  
        |Nombre de columna|Tipo de datos|Description|  
        |-----------------|---------------|-----------------|  
        |**constraint_type**|**nvarchar (**146**)**|Tipo de restricción.|  
        |**constraint_name**|**nvarchar (**128**)**|Nombre de la restricción.|  
        |**delete_action**|**nvarchar (**9**)**|Indica si la acción DELETE es: NO_ACTION, CASCADE, SET_NULL, SET_DEFAULT o N/A.<br /><br /> Solo se aplica a las restricciones FOREIGN KEY.|  
        |**update_action**|**nvarchar (**9**)**|Indica si la acción UPDATE es: NO_ACTION, CASCADE, SET_NULL, SET_DEFAULT o N/A.<br /><br /> Solo se aplica a las restricciones FOREIGN KEY.|  
        |**status_enabled**|**varchar (**8**)**|Indica si la restricción está habilitada: Habilitada, Deshabilitada o N/A.<br /><br /> Solo se aplica a las restricciones CHECK y FOREIGN KEY.|  
        |**status_for_replication**|**varchar (**19**)**|Indica si la restricción es para replicación.<br /><br /> Solo se aplica a las restricciones CHECK y FOREIGN KEY.|  
        |**constraint_keys**|**nvarchar (**2078**)**|Nombres de las columnas que componen la restricción o, en el caso de valores predeterminados y reglas, el texto que define el valor predeterminado o la regla.|  
  
    -   Conjunto de resultados adicional devuelto en los objetos de referencia:  
  
        |Nombre de columna|Tipo de datos|Description|  
        |-----------------|---------------|-----------------|  
        |**Tabla hace referencia**|**nvarchar (**516**)**|Identifica otros objetos de base de datos que hacen referencia a la tabla.|  
  
    -   Conjunto de resultados adicional devuelto en los procedimientos almacenados, las funciones o los procedimientos almacenados extendidos.  
  
        |Nombre de columna|Tipo de datos|Description|  
        |-----------------|---------------|-----------------|  
        |**Parameter_name**|**nvarchar (**128**)**|Nombre del parámetro del procedimiento almacenado.|  
        |**Tipo**|**nvarchar (**128**)**|Tipo de datos del parámetro del procedimiento almacenado.|  
        |**Longitud**|**smallint**|Longitud máxima de almacenamiento físico en bytes.|  
        |**Prec**|**int**|Precisión o número total de dígitos.|  
        |**Escala**|**int**|Número de dígitos a la derecha del separador decimal.|  
        |**Param_order**|**smallint**|Orden del parámetro.|  
  
## <a name="remarks"></a>Comentarios  
 El **sp_help** procedimiento busca un objeto en la base de datos actual.  
  
 Cuando *nombre* no se especifica, **sp_help** listas objeto nombres, propietarios y tipos de objeto para todos los objetos de la base de datos actual. **sp_helptrigger** proporciona información acerca de los desencadenadores.  
  
 **sp_help** expone solo las columnas de índice ordenable; por lo tanto, no expone información acerca de los índices XML o espaciales.  
  
## <a name="permissions"></a>Permissions  
 Debe pertenecer al rol **public** . El usuario debe tener al menos un permiso en *objname*. Para ver claves de restricción de columna, valores predeterminados o reglas, debe tener el permiso VIEW DEFINITION en la tabla.  
  
## <a name="examples"></a>Ejemplos  
  
### <a name="a-returning-information-about-all-objects"></a>A. Devolver información acerca de todos los objetos  
 En el siguiente ejemplo se presenta información acerca de cada objeto de la base de datos `master`.  
  
```  
USE master;  
GO  
EXEC sp_help;  
GO  
```  
  
### <a name="b-returning-information-about-a-single-object"></a>B. Devolver información acerca de un solo objeto  
 En el siguiente ejemplo se presenta información acerca de la tabla `Person`.  
  
```  
USE AdventureWorks2012;  
GO  
EXEC sp_help 'Person.Person';  
GO  
```  
  
## <a name="see-also"></a>Vea también  
 [Motor de base de datos almacenados procedimientos &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/database-engine-stored-procedures-transact-sql.md)   
 [sp_helpindex &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sp-helpindex-transact-sql.md)   
 [sp_helprotect &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sp-helprotect-transact-sql.md)   
 [sp_helpserver &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helpserver-transact-sql.md)   
 [sp_helptrigger &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helptrigger-transact-sql.md)   
 [sp_helpuser &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sp-helpuser-transact-sql.md)   
 [Procedimientos almacenados del sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [Sys.sysobjects &#40; Transact-SQL &#41;](../../relational-databases/system-compatibility-views/sys-sysobjects-transact-sql.md)  
  
  
