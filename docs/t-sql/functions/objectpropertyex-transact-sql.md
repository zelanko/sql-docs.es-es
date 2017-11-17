---
title: OBJECTPROPERTYEX (Transact-SQL) | Documentos de Microsoft
ms.custom: 
ms.date: 03/15/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: t-sql|functions
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- OBJECTPROPERTYEX
- OBJECTPROPERTYEX_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- displaying schema-scoped object information
- viewing schema-scoped object information
- OBJECTPROPERTYEX function
- schema-scoped objects [SQL Server]
- objects [SQL Server], schema-scoped
ms.assetid: be36b3e3-3309-4332-bfb5-c7e9cf8dc8bd
caps.latest.revision: 76
author: edmacauley
ms.author: edmaca
manager: cguyer
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 73e4cbb26ea46753a79b9089acaaab7fe5d50e65
ms.contentlocale: es-es
ms.lasthandoff: 09/01/2017

---
# <a name="objectpropertyex-transact-sql"></a>OBJECTPROPERTYEX (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Devuelve información acerca de los objetos de ámbito de esquema de la base de datos actual. Para obtener una lista de estos objetos, consulte [sys.objects &#40; Transact-SQL &#41; ](../../relational-databases/system-catalog-views/sys-objects-transact-sql.md). OBJECTPROPERTYEX no se puede utilizar con los objetos que no pertenecen al ámbito de esquema, como los desencadenadores de lenguaje de definición de datos (DDL) y las notificaciones de eventos.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
OBJECTPROPERTYEX ( id , property )  
```  
  
## <a name="arguments"></a>Argumentos  
 *id*  
 Es una expresión que representa el identificador del objeto en la base de datos actual. *Id. de* es **int** y se supone que es un objeto de ámbito de esquema en el contexto de base de datos actual.  
  
 *propiedad*  
 Es una expresión que contiene la información sobre el objeto especificado por el identificador que se va a devolver. El tipo de valor devuelto es **sql_variant**. En la siguiente tabla se muestra el tipo de datos base de cada valor de propiedad.  
  
> [!NOTE]  
>  A menos que se indique lo contrario, se devuelve NULL si *propiedad* no es un nombre de propiedad válido, *identificador* no es un identificador de objeto válido, *identificador* es un tipo de objeto no compatible para el elemento especificado *propiedad*, o el autor de llamada no tiene permiso para ver los metadatos del objeto.  
  
|Nombre de la propiedad|Tipo de objeto|Descripción y valores devueltos|  
|-------------------|-----------------|-------------------------------------|  
|BaseType|Cualquier objeto en el ámbito de esquema|Identifica el tipo base del objeto. Cuando el objeto especificado es un sinónimo, se devuelve el tipo base del objeto subyacente.<br /><br /> NonNULL = Tipo de objeto<br /><br /> Tipo de datos base: **char(2)**|  
|CnstIsClustKey|Restricción|Restricción PRIMARY KEY con un índice clúster.<br /><br /> 1 = True<br /><br /> 0 = False<br /><br /> Tipo de datos base: **int**|  
|CnstIsColumn|Restricción|Restricción CHECK, DEFAULT o FOREIGN KEY en una única columna.<br /><br /> 1 = True<br /><br /> 0 = False<br /><br /> Tipo de datos base: **int**|  
|CnstIsDeleteCascade|Restricción|Restricción FOREIGN KEY con la opción ON DELETE CASCADE.<br /><br /> 1 = True<br /><br /> 0 = False<br /><br /> Tipo de datos base: **int**|  
|CnstIsDisabled|Restricción|Restricción deshabilitada.<br /><br /> 1 = True<br /><br /> 0 = False<br /><br /> Tipo de datos base: **int**|  
|CnstIsNonclustKey|Restricción|Restricción PRIMARY KEY con un índice no clúster.<br /><br /> 1 = True<br /><br /> 0 = False<br /><br /> Tipo de datos base: **int**|  
|CnstIsNotRepl|Restricción|La restricción se define utilizando las palabras clave NOT FOR REPLICATION.<br /><br /> 1 = True<br /><br /> 0 = False<br /><br /> Tipo de datos base: **int**|  
|CnstIsNotTrusted|Restricción|La restricción se ha habilitado sin comprobar las filas existentes. Por lo tanto, es posible que no pueda mantenerse para todas las filas.<br /><br /> 1 = True<br /><br /> 0 = False<br /><br /> Tipo de datos base: **int**|  
|CnstIsUpdateCascade|Restricción|Restricción FOREIGN KEY con la opción ON UPDATE CASCADE.<br /><br /> 1 = True<br /><br /> 0 = False<br /><br /> Tipo de datos base: **int**|  
|ExecIsAfterTrigger|Desencadenador|Desencadenador AFTER.<br /><br /> 1 = True<br /><br /> 0 = False<br /><br /> Tipo de datos base: **int**|  
|ExecIsAnsiNullsOn|Función de [!INCLUDE[tsql](../../includes/tsql-md.md)], procedimiento de [!INCLUDE[tsql](../../includes/tsql-md.md)], desencadenador de [!INCLUDE[tsql](../../includes/tsql-md.md)], vista|El valor de ANSI_NULLS en el momento de su creación.<br /><br /> 1 = True<br /><br /> 0 = False<br /><br /> Tipo de datos base: **int**|  
|ExecIsDeleteTrigger|Desencadenador|Desencadenador DELETE.<br /><br /> 1 = True<br /><br /> 0 = False<br /><br /> Tipo de datos base: **int**|  
|ExecIsFirstDeleteTrigger|Desencadenador|El primer desencadenador que se activa cuando se ejecuta DELETE en la tabla.<br /><br /> 1 = True<br /><br /> 0 = False<br /><br /> Tipo de datos base: **int**|  
|ExecIsFirstInsertTrigger|Desencadenador|El primer desencadenador que se activa cuando se ejecuta INSERT en la tabla.<br /><br /> 1 = True<br /><br /> 0 = False<br /><br /> Tipo de datos base: **int**|  
|ExecIsFirstUpdateTrigger|Desencadenador|El primer desencadenador que se activa cuando se ejecuta UPDATE en la tabla.<br /><br /> 1 = True<br /><br /> 0 = False<br /><br /> Tipo de datos base: **int**|  
|ExecIsInsertTrigger|Desencadenador|Desencadenador INSERT.<br /><br /> 1 = True<br /><br /> 0 = False<br /><br /> Tipo de datos base: **int**|  
|ExecIsInsteadOfTrigger|Desencadenador|Desencadenador INSTEAD OF.<br /><br /> 1 = True<br /><br /> 0 = False<br /><br /> Tipo de datos base: **int**|  
|ExecIsLastDeleteTrigger|Desencadenador|Último desencadenador que se activa cuando se ejecuta DELETE en la tabla.<br /><br /> 1 = True<br /><br /> 0 = False<br /><br /> Tipo de datos base: **int**|  
|ExecIsLastInsertTrigger|Desencadenador|Último desencadenador que se activa cuando se ejecuta INSERT en la tabla.<br /><br /> 1 = True<br /><br /> 0 = False<br /><br /> Tipo de datos base: **int**|  
|ExecIsLastUpdateTrigger|Desencadenador|Último desencadenador que se activa cuando se ejecuta UPDATE en la tabla.<br /><br /> 1 = True<br /><br /> 0 = False<br /><br /> Tipo de datos base: **int**|  
|ExecIsQuotedIdentOn|Función de [!INCLUDE[tsql](../../includes/tsql-md.md)], procedimiento de [!INCLUDE[tsql](../../includes/tsql-md.md)], desencadenador de [!INCLUDE[tsql](../../includes/tsql-md.md)], vista|Valor de QUOTED_IDENTIFIER en el momento de su creación.<br /><br /> 1 = True<br /><br /> 0 = False<br /><br /> Tipo de datos base: **int**|  
|ExecIsStartup|Procedimiento|Procedimiento de inicio.<br /><br /> 1 = True<br /><br /> 0 = False<br /><br /> Tipo de datos base: **int**|  
|ExecIsTriggerDisabled|Desencadenador|Desencadenador deshabilitado.<br /><br /> 1 = True<br /><br /> 0 = False<br /><br /> Tipo de datos base: **int**|  
|ExecIsTriggerNotForRepl|Desencadenador|Desencadenador definido como NOT FOR REPLICATION.<br /><br /> 1 = True<br /><br /> 0 = False<br /><br /> Tipo de datos base: **int**|  
|ExecIsUpdateTrigger|Desencadenador|Desencadenador UPDATE.<br /><br /> 1 = True<br /><br /> 0 = False<br /><br /> Tipo de datos base: **int**|  
|ExecIsWithNativeCompilation|Procedimiento de [!INCLUDE[tsql](../../includes/tsql-md.md)]|**Se aplica a**: desde [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].<br /><br /> El procedimiento se compila de forma nativa.<br /><br /> 1 = True<br /><br /> 0 = False<br /><br /> Tipo de datos base: **int**|  
|HasAfterTrigger|Tabla, vista|La tabla o la vista tiene un desencadenador AFTER.<br /><br /> 1 = True<br /><br /> 0 = False<br /><br /> Tipo de datos base: **int**|  
|HasDeleteTrigger|Tabla, vista|La tabla o la vista tiene un desencadenador DELETE.<br /><br /> 1 = True<br /><br /> 0 = False<br /><br /> Tipo de datos base: **int**|  
|HasInsertTrigger|Tabla, vista|La tabla o la vista tiene un desencadenador INSERT.<br /><br /> 1 = True<br /><br /> 0 = False<br /><br /> Tipo de datos base: **int**|  
|HasInsteadOfTrigger|Tabla, vista|La tabla o la vista tiene un desencadenador INSTEAD OF.<br /><br /> 1 = True<br /><br /> 0 = False<br /><br /> Tipo de datos base: **int**|  
|HasUpdateTrigger|Tabla, vista|La tabla o la vista tiene un desencadenador UPDATE.<br /><br /> 1 = True<br /><br /> 0 = False<br /><br /> Tipo de datos base: **int**|  
|IsAnsiNullsOn|Función de [!INCLUDE[tsql](../../includes/tsql-md.md)], procedimiento de [!INCLUDE[tsql](../../includes/tsql-md.md)], tabla, desencadenador de [!INCLUDE[tsql](../../includes/tsql-md.md)], vista|Especifica que el valor de la opción ANSI NULLS para la tabla es ON, lo que significa que todas las comparaciones con un valor NULL se evalúan como UNKNOWN. Este valor se aplica a todas las expresiones de la definición de tabla, incluidas las columnas calculadas y las restricciones, mientras la tabla exista.<br /><br /> 1 = True<br /><br /> 0 = False<br /><br /> Tipo de datos base: **int**|  
|IsCheckCnst|Cualquier objeto en el ámbito de esquema|Restricción CHECK.<br /><br /> 1 = True<br /><br /> 0 = False<br /><br /> Tipo de datos base: **int**|  
|IsConstraint|Cualquier objeto en el ámbito de esquema|Restricción.<br /><br /> 1 = True<br /><br /> 0 = False<br /><br /> Tipo de datos base: **int**|  
|IsDefault|Cualquier objeto en el ámbito de esquema|**Se aplica a**: desde [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].<br /><br /> Valor predeterminado enlazado.<br /><br /> 1 = True<br /><br /> 0 = False<br /><br /> Tipo de datos base: **int**|  
|IsDefaultCnst|Cualquier objeto en el ámbito de esquema|Restricción DEFAULT.<br /><br /> 1 = True<br /><br /> 0 = False<br /><br /> Tipo de datos base: **int**|  
|IsDeterministic|Funciones escalares y con valores de tabla, vista|Propiedad de determinismo de la función o vista.<br /><br /> 1 = Determinista<br /><br /> 0 = No determinista<br /><br /> Tipo de datos base: **int**|  
|IsEncrypted|Función de [!INCLUDE[tsql](../../includes/tsql-md.md)], procedimiento de [!INCLUDE[tsql](../../includes/tsql-md.md)], tabla, desencadenador de [!INCLUDE[tsql](../../includes/tsql-md.md)], vista|Indica que el texto original de la instrucción del módulo se ha convertido a un formato confuso. La salida de la protección no es directamente visible en ninguna de las vistas de catálogo de [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]. Los usuarios sin acceso a las tablas del sistema o archivos de base de datos no pueden recuperar el texto confuso. Sin embargo, el texto está disponible para los usuarios que pueden tener acceso a las tablas del sistema sobre el [puerto DAC](../../database-engine/configure-windows/diagnostic-connection-for-database-administrators.md) o directamente a los archivos de base de datos. Además, los usuarios que pueden adjuntar un depurador al proceso del servidor pueden recuperar el procedimiento original de la memoria en tiempo de ejecución.<br /><br /> 1 = Cifrada<br /><br /> 0 = No cifrado<br /><br /> Tipo de datos base: **int**|  
|IsExecuted|Cualquier objeto en el ámbito de esquema|Especifica que el objeto se puede ejecutar (vista, procedimiento, función o desencadenador).<br /><br /> 1 = True<br /><br /> 0 = False<br /><br /> Tipo de datos base: **int**|  
|IsExtendedProc|Cualquier objeto en el ámbito de esquema|Procedimiento extendido.<br /><br /> 1 = True<br /><br /> 0 = False<br /><br /> Tipo de datos base: **int**|  
|IsForeignKey|Cualquier objeto en el ámbito de esquema|Restricción FOREIGN KEY.<br /><br /> 1 = True<br /><br /> 0 = False<br /><br /> Tipo de datos base: **int**|  
|IsIndexed|Tabla, vista|Una tabla o vista con un índice.<br /><br /> 1 = True<br /><br /> 0 = False<br /><br /> Tipo de datos base: **int**|  
|IsIndexable|Tabla, vista|Una tabla o una vista en la que es posible crear un índice.<br /><br /> 1 = True<br /><br /> 0 = False<br /><br /> Tipo de datos base: **int**|  
|IsInlineFunction|Función|Función insertada.<br /><br /> 1 = Función insertada<br /><br /> 0 = Función no insertada<br /><br /> Tipo de datos base: **int**|  
|IsMSShipped|Cualquier objeto en el ámbito de esquema|Un objeto creado durante la instalación de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].<br /><br /> 1 = True<br /><br /> 0 = False<br /><br /> Tipo de datos base: **int**|  
|IsPrecise|Columna calculada, función, tipo definido por el usuario, vista|Indica si el objeto contiene un cálculo impreciso, como una operación de punto flotante.<br /><br /> 1 = Preciso<br /><br /> 0 = Impreciso<br /><br /> Tipo de datos base: **int**|  
|IsPrimaryKey|Cualquier objeto en el ámbito de esquema|Restricción PRIMARY KEY.<br /><br /> 1 = True<br /><br /> 0 = False<br /><br /> Tipo de datos base: **int**|  
|IsProcedure|Cualquier objeto en el ámbito de esquema|Procedimiento.<br /><br /> 1 = True<br /><br /> 0 = False<br /><br /> Tipo de datos base: **int**|  
|IsQuotedIdentOn|Restricción CHECK, definición DEFAULT, función de [!INCLUDE[tsql](../../includes/tsql-md.md)], procedimiento de [!INCLUDE[tsql](../../includes/tsql-md.md)], tabla, desencadenador de [!INCLUDE[tsql](../../includes/tsql-md.md)], vista|Especifica que el valor del identificador entrecomillado para el objeto es ON, lo que significa que las comillas dobles delimitan los identificadores en todas las expresiones de la definición de objeto.<br /><br /> 1 = True<br /><br /> 0 = False<br /><br /> Tipo de datos base: **int**|  
|IsQueue|Cualquier objeto en el ámbito de esquema|Cola de Service Broker<br /><br /> 1 = True<br /><br /> 0 = False<br /><br /> Tipo de datos base: **int**|  
|IsReplProc|Cualquier objeto en el ámbito de esquema|Procedimiento de replicación.<br /><br /> 1 = True<br /><br /> 0 = False<br /><br /> Tipo de datos base: **int**|  
|IsRule|Cualquier objeto en el ámbito de esquema|Regla enlazada.<br /><br /> 1 = True<br /><br /> 0 = False<br /><br /> Tipo de datos base: **int**|  
|IsScalarFunction|Función|Función con valores escalares.<br /><br /> 1 = Función escalar<br /><br /> 0 = Función no escalar<br /><br /> Tipo de datos base: **int**|  
|IsSchemaBound|Función, procedimiento y vista|Función o vista enlazada al esquema creada mediante SCHEMABINDING.<br /><br /> 1 = Enlazada al esquema<br /><br /> 0 = No enlazada al esquema<br /><br /> Tipo de datos base: **int**|  
|IsSystemTable|Tabla|Tabla del sistema.<br /><br /> 1 = True<br /><br /> 0 = False<br /><br /> Tipo de datos base: **int**|  
|IsSystemVerified|Columna calculada, función, tipo definido por el usuario, vista|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] puede comprobar las propiedades de precisión y determinismo del objeto.<br /><br /> 1 = True<br /><br /> 0 = False<br /><br /> Tipo de datos base: **int**|  
|IsTable|Tabla|Tabla.<br /><br /> 1 = True<br /><br /> 0 = False<br /><br /> Tipo de datos base: **int**|  
|IsTableFunction|Función|Función con valores de tabla.<br /><br /> 1 = Función con valores de tabla<br /><br /> 0 = Función con valores no de tabla.<br /><br /> Tipo de datos base: **int**|  
|IsTrigger|Cualquier objeto en el ámbito de esquema|Desencadenador.<br /><br /> 1 = True<br /><br /> 0 = False<br /><br /> Tipo de datos base: **int**|  
|IsUniqueCnst|Cualquier objeto en el ámbito de esquema|Restricción UNIQUE.<br /><br /> 1 = True<br /><br /> 0 = False<br /><br /> Tipo de datos base: **int**|  
|IsUserTable|Tabla|Tabla definida por el usuario.<br /><br /> 1 = True<br /><br /> 0 = False<br /><br /> Tipo de datos base: **int**|  
|IsView|Ver|Vista.<br /><br /> 1 = True<br /><br /> 0 = False<br /><br /> Tipo de datos base: **int**|  
|OwnerId|Cualquier objeto en el ámbito de esquema|Propietario del objeto.<br /><br /> **Nota:** el propietario del esquema no es necesariamente el propietario del objeto. Por ejemplo, los objetos secundarios (aquellos en los que *parent_object_id* es diferente de null) siempre devolverá el mismo identificador de propietario que el elemento primario.<br /><br /> NonNULL = Id. de usuario de la base de datos del propietario del objeto.<br /><br /> NULL = Tipo de objeto no compatible o identificador de objeto no válido.<br /><br /> Tipo de datos base: **int**|  
|SchemaId|Cualquier objeto en el ámbito de esquema|Identificador de esquema asociado al objeto.<br /><br /> NonNULL = Identificador de esquema del objeto.<br /><br /> Tipo de datos base: **int**|  
|SystemDataAccess|Función, vista|El objeto obtiene acceso a los datos del sistema, los catálogos del sistema o las tablas virtuales del sistema en la instancia local de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].<br /><br /> 0 = Ninguno<br /><br /> 1 = Lectura<br /><br /> Tipo de datos base: **int**|  
|TableDeleteTrigger|Tabla|La tabla tiene un desencadenador DELETE.<br /><br /> > 1 = identificador del primer desencadenador con el tipo especificado.<br /><br /> Tipo de datos base: **int**|  
|TableDeleteTriggerCount|Tabla|La tabla tiene el número especificado de desencadenadores DELETE.<br /><br /> NonNULL = Número de desencadenadores DELETE<br /><br /> Tipo de datos base: **int**|  
|TableFullTextMergeStatus|Tabla|**Se aplica a**: desde [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].<br /><br /> Indica si una tabla que tiene un índice de texto completo se está combinando actualmente.<br /><br /> 0 = La tabla no tiene un índice de texto completo o el índice de texto completo no se está combinando.<br /><br /> 1 = El índice de texto completo se está combinando.|  
|TableFullTextBackgroundUpdateIndexOn|Tabla|**Se aplica a**: desde [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].<br /><br /> La tabla tiene habilitado el índice de actualización de texto completo en segundo plano (seguimiento de cambios automáticos).<br /><br /> 1 = TRUE<br /><br /> 0 = False<br /><br /> Tipo de datos base: **int**|  
|TableFulltextCatalogId|Tabla|**Se aplica a**: desde [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].<br /><br /> Identificador del catálogo de texto completo en el que residen los datos de índice de texto completo para la tabla.<br /><br /> Distinto de cero = Identificador del catálogo de texto completo, asociado al índice único que identifica las filas en una tabla indizada de texto completo.<br /><br /> 0 = La tabla no tiene un índice de texto completo.<br /><br /> Tipo de datos base: **int**|  
|TableFullTextChangeTrackingOn|Tabla|**Se aplica a**: desde [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].<br /><br /> La tabla tiene habilitado el seguimiento de cambios de texto completo.<br /><br /> 1 = TRUE<br /><br /> 0 = False<br /><br /> Tipo de datos base: **int**|  
|TableFulltextDocsProcessed|Tabla|**Se aplica a**: desde [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].<br /><br /> Número de filas procesadas desde el comienzo de la indización de texto completo. En una tabla que se indiza para búsquedas en texto completo, todas las columnas de una fila se consideran como parte de un documento que se va a indizar.<br /><br /> 0 = No se ha completado ningún rastreo activo ni ninguna indización de texto completo.<br /><br /> > 0 = uno de los siguientes (A o B): A) el número de documentos procesados por insert o las operaciones de actualización desde el inicio de completo, incremental o rellenado; de seguimiento de cambios manual B) el número de filas procesadas por insert o las operaciones de actualización desde que se habilitó el seguimiento de cambios con rellenado del índice de actualización de fondo, el esquema de índice de texto completo cambia, la regeneración del catálogo de texto completo o la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] reinicien y así sucesivamente.<br /><br /> NULL = La tabla no tiene un índice de texto completo.<br /><br /> Tipo de datos base: **int**<br /><br /> **Tenga en cuenta** esta propiedad no supervisa ni cuenta las filas eliminadas.|  
|TableFulltextFailCount|Tabla|**Se aplica a**: desde [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].<br /><br /> Número de filas que no ha indizado la búsqueda de texto completo.<br /><br /> 0 = El rellenado se ha completado.<br /><br /> > 0 = uno de los siguientes (A o B): A) el número de documentos no indizados desde el inicio del rellenado; de seguimiento de cambios completo, Incremental o actualización Manual B) para seguimiento de cambios con fondo actualización de índices, el número de filas que no indizados desde el principio de la población o el reinicio de la población. Esto podría ser debido a un cambio de esquema, una regeneración del catálogo, un reinicio del servidor, etc.<br /><br /> NULL = La tabla no tiene un índice de texto completo.<br /><br /> Tipo de datos base: **int**|  
|TableFulltextItemCount|Tabla|**Se aplica a**: desde [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].<br /><br /> NonNULL = El número de filas que se han indizado por texto completo correctamente.<br /><br /> NULL = La tabla no tiene un índice de texto completo.<br /><br /> Tipo de datos base: **int**|  
|TableFulltextKeyColumn|Tabla|**Se aplica a**: desde [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].<br /><br /> Identificador de la columna asociada al índice único de una sola columna que forma parte de la definición de un índice de texto completo y un índice semántico.<br /><br /> 0 = La tabla no tiene un índice de texto completo.<br /><br /> Tipo de datos base: **int**|  
|TableFulltextPendingChanges|Tabla|**Se aplica a**: desde [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].<br /><br /> Número de entradas de seguimiento de cambios pendientes de procesamiento.<br /><br /> 0 = El seguimiento de cambios no está habilitado.<br /><br /> NULL = La tabla no tiene un índice de texto completo.<br /><br /> Tipo de datos base: **int**|  
|TableFulltextPopulateStatus|Tabla|**Se aplica a**: desde [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].<br /><br /> 0 = Inactiva<br /><br /> 1 = Rellenado completo en curso.<br /><br /> 2 = Rellenado incremental en curso.<br /><br /> 3 = Propagación de cambios de seguimiento en curso.<br /><br /> 4 = el índice de actualización está en curso, como el seguimiento de cambios automáticos de fondo.<br /><br /> 5 = Indización de texto completo acelerada o pausada.<br /><br /> 6 = se ha producido un error. Examine el registro de rastreo para obtener más información. Para obtener más información, consulte el **solución de problemas de errores en un rellenado de texto completo (rastreo)** sección de [rellenar índices de texto completo](../../relational-databases/search/populate-full-text-indexes.md).<br /><br /> Tipo de datos base: **int**|  
|TableFullTextSemanticExtraction|Tabla|**Se aplica a**: desde [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].<br /><br /> La tabla está habilitada para la indización semántica.<br /><br /> 1 = True<br /><br /> 0 = False<br /><br /> Tipo de datos base: **int**|  
|TableHasActiveFulltextIndex|Tabla|**Se aplica a**: desde [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].<br /><br /> La tabla tiene un índice de texto completo activo.<br /><br /> 1 = True<br /><br /> 0 = False<br /><br /> Tipo de datos base: **int**|  
|TableHasCheckCnst|Tabla|La tabla tiene una restricción CHECK.<br /><br /> 1 = True<br /><br /> 0 = False<br /><br /> Tipo de datos base: **int**|  
|TableHasClustIndex|Tabla|La tabla tiene un índice clúster.<br /><br /> 1 = True<br /><br /> 0 = False<br /><br /> Tipo de datos base: **int**|  
|TableHasDefaultCnst|Tabla|La tabla tiene una restricción DEFAULT.<br /><br /> 1 = True<br /><br /> 0 = False<br /><br /> Tipo de datos base: **int**|  
|TableHasDeleteTrigger|Tabla|La tabla tiene un desencadenador DELETE.<br /><br /> 1 = True<br /><br /> 0 = False<br /><br /> Tipo de datos base: **int**|  
|TableHasForeignKey|Tabla|La tabla tiene una restricción FOREIGN KEY.<br /><br /> 1 = True<br /><br /> 0 = False<br /><br /> Tipo de datos base: **int**|  
|TableHasForeignRef|Tabla|Una restricción FOREIGN KEY hace referencia a la tabla.<br /><br /> 1 = True<br /><br /> 0 = False<br /><br /> Tipo de datos base: **int**|  
|TableHasIdentity|Tabla|La tabla tiene una columna de identidad.<br /><br /> 1 = True<br /><br /> 0 = False<br /><br /> Tipo de datos base: **int**|  
|TableHasIndex|Tabla|La tabla tiene un índice de cualquier tipo.<br /><br /> 1 = True<br /><br /> 0 = False<br /><br /> Tipo de datos base: **int**|  
|TableHasInsertTrigger|Tabla|El objeto tiene un desencadenador INSERT.<br /><br /> 1 = True<br /><br /> 0 = False<br /><br /> Tipo de datos base: **int**|  
|TableHasNonclustIndex|Tabla|La tabla tiene un índice no agrupado.<br /><br /> 1 = True<br /><br /> 0 = False<br /><br /> Tipo de datos base: **int**|  
|TableHasPrimaryKey|Tabla|La tabla tiene una clave principal.<br /><br /> 1 = True<br /><br /> 0 = False<br /><br /> Tipo de datos base: **int**|  
|TableHasRowGuidCol|Tabla|La tabla tiene un ROWGUIDCOL para una **uniqueidentifier** columna.<br /><br /> 1 = True<br /><br /> 0 = False<br /><br /> Tipo de datos base: **int**|  
|TableHasTextImage|Tabla|La tabla tiene un **texto**, **ntext**, o **imagen** columna.<br /><br /> 1 = True<br /><br /> 0 = False<br /><br /> Tipo de datos base: **int**|  
|TableHasTimestamp|Tabla|La tabla tiene un **timestamp** columna.<br /><br /> 1 = True<br /><br /> 0 = False<br /><br /> Tipo de datos base: **int**|  
|TableHasUniqueCnst|Tabla|La tabla tiene una restricción UNIQUE.<br /><br /> 1 = True<br /><br /> 0 = False<br /><br /> Tipo de datos base: **int**|  
|TableHasUpdateTrigger|Tabla|El objeto tiene un desencadenador UPDATE.<br /><br /> 1 = True<br /><br /> 0 = False<br /><br /> Tipo de datos base: **int**|  
|TableHasVarDecimalStorageFormat|Tabla|Tabla está habilitada para **vardecimal** el formato de almacenamiento.<br /><br /> 1 = True<br /><br /> 0 = False|  
|TableInsertTrigger|Tabla|La tabla tiene un desencadenador INSERT.<br /><br /> > 1 = identificador del primer desencadenador con el tipo especificado.<br /><br /> Tipo de datos base: **int**|  
|TableInsertTriggerCount|Tabla|La tabla tiene el número especificado de desencadenadores INSERT.<br /><br /> >0 = Número de desencadenadores INSERT.<br /><br /> Tipo de datos base: **int**|  
|TableIsFake|Tabla|La tabla no es real. [!INCLUDE[ssDE](../../includes/ssde-md.md)] la materializa internamente a petición.<br /><br /> 1 = True<br /><br /> 0 = False<br /><br /> Tipo de datos base: **int**|  
|TableIsLockedOnBulkLoad|Tabla|Tabla está bloqueada porque una **bcp** o BULK INSERT.<br /><br /> 1 = True<br /><br /> 0 = False<br /><br /> Tipo de datos base: **int**|  
|TableIsMemoryOptimized|Tabla|**Se aplica a**: desde [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].<br /><br /> La tabla tiene optimización para memoria<br /><br /> 1 = True<br /><br /> 0 = False<br /><br /> Tipo de datos base: **int**<br /><br /> Para obtener más información, vea [OLTP en memoria &#40;optimización en memoria&#41;](../../relational-databases/in-memory-oltp/in-memory-oltp-in-memory-optimization.md).|  
|TableIsPinned|Tabla|La tabla se ancla para que se mantenga en la memoria caché de datos.<br /><br /> 0 = False<br /><br /> Esta característica no es compatible con [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] y versiones posteriores.|  
|TableTextInRowLimit|Tabla|La tabla tiene establecida la opción text in row.<br /><br /> > 0 = Número máximo de bytes permitido para text in row.<br /><br /> 0 = La opción text in row no está establecida.<br /><br /> Tipo de datos base: **int**|  
|TableUpdateTrigger|Tabla|La tabla tiene un desencadenador UPDATE.<br /><br /> > 1 = Identificador del primer desencadenador con el tipo especificado.<br /><br /> Tipo de datos base: **int**|  
|TableUpdateTriggerCount|Tabla|Tabla tiene el número especificado de desencadenadores UPDATE.<br /><br /> > 0 = Número de desencadenadores UPDATE.<br /><br /> Tipo de datos base: **int**|  
|UserDataAccess|Función, vista|Indica que el objeto obtiene acceso a datos y tablas de usuario en la instancia local de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].<br /><br /> 1 = Lectura<br /><br /> 0 = Ninguno<br /><br /> Tipo de datos base: **int**|  
|TableHasColumnSet|Tabla|La tabla tiene un conjunto de columnas.<br /><br /> 0 = False<br /><br /> 1 = True<br /><br /> Para obtener más información, vea [Usar conjuntos de columnas](../../relational-databases/tables/use-column-sets.md).|  
|Cardinalidad|Tabla (del sistema o definida por el usuario), vista o índice|**Se aplica a**: desde [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].<br /><br /> El número de filas del objeto especificado.|  
|TableTemporalType|Tabla|**Se aplica a**: desde [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].<br /><br /> Especifica el tipo de tabla.<br /><br /> 0 = la tabla no temporal<br /><br /> 1 = la tabla de historial para la tabla con control de versiones<br /><br /> 2 = tabla temporal con versión del sistema|  
  
## <a name="return-types"></a>Tipos devueltos  
 **sql_variant**  
  
## <a name="exceptions"></a>Excepciones  
 Devuelve NULL si se produce un error o si el autor de la llamada no tiene permiso para ver el objeto.  
  
 Un usuario solo puede ver los metadatos de elementos protegibles que posea o para los que se le haya concedido permiso. Esto significa que las funciones integradas de emisión de metadatos, como OBJECTPROPERTYEX, pueden devolver NULL si el usuario no tiene ningún permiso para el objeto. Para obtener más información, consulte [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md).  
  
## <a name="remarks"></a>Comentarios  
 El [!INCLUDE[ssDE](../../includes/ssde-md.md)] se da por supuesto que *object_id* está en el contexto de base de datos actual. Una consulta que hace referencia a un *object_id* en otra base de datos devolverá NULL o resultados incorrectos. Por ejemplo, en la siguiente consulta el contexto de base de datos actual es la base de datos maestra. El [!INCLUDE[ssDE](../../includes/ssde-md.md)] intentará devolver el valor de propiedad para el elemento especificado *object_id* en esa base de datos en lugar de la base de datos que se especifica en la consulta. La consulta devuelve resultados incorrectos porque la vista `vEmployee` no está en la base de datos maestra.  
  
```  
USE master;  
GO  
SELECT OBJECTPROPERTYEX(OBJECT_ID(N'AdventureWorks2012.HumanResources.vEmployee'), 'IsView');  
GO  
```  
  
 OBJECTPROPERTYEX (*view_i*d., 'IsIndexable') puede consumir importantes recursos del equipo porque la evaluación de la propiedad IsIndexable requiere el análisis de la definición de la vista, la normalización y optimización parcial. Aunque la propiedad IsIndexable identifica tablas o vistas que se pueden indizar, es posible que se produzca un error en la creación real del índice si no se cumplen ciertos requisitos de clave de índice. Para obtener más información, vea [CREATE INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/create-index-transact-sql.md).  
  
 OBJECTPROPERTYEX (*table_id*, 'TableHasActiveFulltextIndex') devolverá un valor de 1 (true) cuando se agrega al menos una columna de una tabla para la indización. El índice de texto completo se activa para su llenado en el momento en que se agrega la primera columna para la indización.  
  
 Se aplican restricciones sobre la visibilidad de los metadatos al conjunto de resultados. Para obtener más información, consulte [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md).  
  
## <a name="examples"></a>Ejemplos  
  
### <a name="a-finding-the-base-type-of-an-object"></a>A. Buscar el tipo base de un objeto  
 En el siguiente ejemplo se crea un sinónimo `MyEmployeeTable` para la tabla `Employee` de la base de datos [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] y, a continuación, se devuelve el tipo base del sinónimo.  
  
```  
USE AdventureWorks2012;  
GO  
CREATE SYNONYM MyEmployeeTable FOR HumanResources.Employee;  
GO  
SELECT OBJECTPROPERTYEX ( object_id(N'MyEmployeeTable'), N'BaseType')AS [Base Type];  
GO  
```  
  
 El conjunto de resultados muestra que el tipo base del objeto subyacente, la tabla `Employee`, es una tabla de usuario.  
  
 ```
Base Type 
--------  
U
```  
  
### <a name="b-returning-a-property-value"></a>B. Devolver un valor de propiedad  
 En el siguiente ejemplo se devuelve el número de desencadenadores UPDATE de la tabla especificada.  
  
```  
USE AdventureWorks2012;  
GO  
SELECT OBJECTPROPERTYEX(OBJECT_ID(N'HumanResources.Employee'), N'TABLEUPDATETRIGGERCOUNT');  
GO  
  
```  
  
### <a name="c-finding-tables-that-have-a-foreign-key-constraint"></a>C. Buscar tablas que tengan una restricción FOREIGN KEY  
 En el ejemplo siguiente se utiliza la propiedad `TableHasForeignKey` para devolver todas las tablas que tengan una restricción FOREIGN KEY.  
  
```  
USE AdventureWorks2012;  
GO  
SELECT name, object_id, schema_id, type_desc  
FROM sys.objects   
WHERE OBJECTPROPERTYEX(object_id, N'TableHasForeignKey') = 1  
ORDER BY name;  
GO  
  
```  
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>Ejemplos: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] y[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
### <a name="d-finding-the-base-type-of-an-object"></a>D: buscar el tipo base de un objeto  
 En el ejemplo siguiente se devuelve el tipo base del `dbo.DimReseller` objeto.  
  
```  
-- Uses AdventureWorks  
  
SELECT OBJECTPROPERTYEX ( object_id(N'dbo.DimReseller'), N'BaseType')AS BaseType;  
```  
  
 El conjunto de resultados muestra que el tipo base del objeto subyacente, la tabla `dbo.DimReseller`, es una tabla de usuario.  
  
```  
BaseType   
--------   
U   
```  
  
## <a name="see-also"></a>Vea también  
 [CREAR el sinónimo &#40; Transact-SQL &#41;](../../t-sql/statements/create-synonym-transact-sql.md)   
 [Funciones de metadatos &#40; Transact-SQL &#41;](../../t-sql/functions/metadata-functions-transact-sql.md)   
 [OBJECT_DEFINITION &#40;Transact-SQL&#41;](../../t-sql/functions/object-definition-transact-sql.md)   
 [Object_id &#40; Transact-SQL &#41;](../../t-sql/functions/object-id-transact-sql.md)   
 [Object_name &#40; Transact-SQL &#41;](../../t-sql/functions/object-name-transact-sql.md)   
 [Sys.Objects &#40; Transact-SQL &#41;](../../relational-databases/system-catalog-views/sys-objects-transact-sql.md)   
 [ALTER AUTHORIZATION &#40; Transact-SQL &#41;](../../t-sql/statements/alter-authorization-transact-sql.md)   
 [TYPEPROPERTY &#40; Transact-SQL &#41;](../../t-sql/functions/typeproperty-transact-sql.md)  
  
  


