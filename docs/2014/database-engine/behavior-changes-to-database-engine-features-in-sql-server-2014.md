---
title: Características de SQL Server 2014 del motor de base de datos de los cambios de comportamiento | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- behavior changes [SQL Server]
- Database Engine [SQL Server], what's new
- Transact-SQL behavior changes
ms.assetid: 65eaafa1-9e06-4264-b547-cbee8013c995
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 6e7b629b93e0c79a003019a2e024388d54b12b76
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "66065211"
---
# <a name="behavior-changes-to-database-engine-features-in-sql-server-2014"></a>Cambios de comportamiento en las características del Motor de base de datos en SQL Server 2014
  En este tema se describen los cambios de comportamiento en [!INCLUDE[ssDE](../includes/ssde-md.md)]. Los cambios de comportamiento afectan al modo en que las características de [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] funcionan o interactúan en comparación con las versiones anteriores de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)].  
  
## <a name="behavior-changes-in-includesssql14includessssql14-mdmd"></a>Cambios de comportamiento en [!INCLUDE[ssSQL14](../includes/sssql14-md.md)]  
 En las versiones anteriores de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)], las consultas en un documento XML que contiene cadenas por encima de una determinada longitud (más de 4020 caracteres) pueden producir resultados incorrectos. En [!INCLUDE[ssSQL14](../includes/sssql14-md.md)], estas consultas devuelven resultados correctos.  
  
## <a name="behavior-changes-in-includesssql11includessssql11-mdmd"></a>Cambios de comportamiento en [!INCLUDE[ssSQL11](../includes/sssql11-md.md)]  
  
### <a name="metadata-discovery"></a>Detección de metadatos  
 Mejoras en el [!INCLUDE[ssDE](../includes/ssde-md.md)] partir [!INCLUDE[ssSQL11](../includes/sssql11-md.md)] permitir SQLDescribeCol obtener descripciones más precisas de los resultados esperados que los devueltos por SQLDescribeCol en versiones anteriores de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]. Para obtener más información, vea [Detección de metadatos](../relational-databases/native-client/features/metadata-discovery.md).  
  
 El [SET FMTONLY](/sql/t-sql/statements/set-fmtonly-transact-sql) opción para determinar el formato de una respuesta sin ejecutar realmente la consulta se reemplaza por [sp_describe_first_result_set &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-describe-first-result-set-transact-sql), [sp_describe_undeclared_parameters &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-describe-undeclared-parameters-transact-sql), [sys.dm_exec_describe_first_result_set &#40;Transact-SQL&#41;](/sql/relational-databases/system-dynamic-management-views/sys-dm-exec-describe-first-result-set-transact-sql), y [sys.dm_ exec_describe_first_result_set_for_object &#40;Transact-SQL&#41;](/sql/relational-databases/system-dynamic-management-views/sys-dm-exec-describe-first-result-set-for-object-transact-sql).  
  
### <a name="changes-to-behavior-in-scripting-a-sql-server-agent-task"></a>Cambios de comportamiento de scripting en una tarea del Agente SQL Server  
 En [!INCLUDE[ssSQL11](../includes/sssql11-md.md)], si crea un nuevo trabajo copiando el script desde un trabajo existente, el nuevo trabajo puede afectar inadvertidamente al trabajo existente. Para crear un nuevo trabajo con la secuencia de comandos desde un trabajo existente, elimine manualmente el parámetro *@schedule_uid* que normalmente es el último parámetro de la sección que crea la programación de trabajo en el trabajo existente. De esta forma se crea una nueva programación independiente del nuevo trabajo sin que se vean afectados los trabajos existentes.  
  
### <a name="constant-folding-for-clr-user-defined-functions-and-methods"></a>Doblado constante para las funciones y métodos CLR definidos por el usuario  
 En [!INCLUDE[ssSQL11](../includes/sssql11-md.md)], los objetos definidos por el usuario para CLR pueden doblarse ahora:  
  
-   Funciones CLR definidas por el usuario con valores escalares deterministas.  
  
-   Métodos deterministas de tipos CLR definidos por el usuario.  
  
 Esta mejora trata de aumentar el rendimiento cuando estas funciones o métodos se llaman más de una vez con los mismos argumentos. Sin embargo, este cambio puede producir resultados inesperados cuando las funciones o métodos no deterministas se han marcado como deterministas por error. El determinismo de una función o método CLR viene indicado por el valor de la propiedad `IsDeterministic` de `SqlFunctionAttribute` o `SqlMethodAttribute`.  
  
### <a name="behavior-of-stenvelope-method-has-changed-with-empty-spatial-types"></a>El comportamiento del método STEnvelope() ha cambiado con tipos espaciales vacíos  
 El comportamiento del método `STEnvelope` con objetos vacíos es ahora coherente con el comportamiento de otros métodos espaciales de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] .  
  
 En [!INCLUDE[ssKatmai](../includes/sskatmai-md.md)], el método `STEnvelope` devuelve los siguientes resultados cuando se llama con objetos vacíos:  
  
```  
select geometry::Parse('POINT EMPTY').STEnvelope().ToString()  
-- returns POINT EMPTY  
select geometry::Parse('LINESTRING EMPTY').STEnvelope().ToString()  
-- returns LINESTRING EMPTY  
select geometry::Parse('POLYGON EMPTY').STEnvelope().ToString()  
-- returns POLYGON EMPTY  
```  
  
 En [!INCLUDE[ssSQL11](../includes/sssql11-md.md)], el método `STEnvelope` devuelve ahora los siguientes resultados cuando se llama con objetos vacíos:  
  
```  
select geometry::Parse('POINT EMPTY').STEnvelope().ToString()  
-- returns GEOMETRYCOLLECTION EMPTY  
select geometry::Parse('LINESTRING EMPTY').STEnvelope().ToString()  
-- returns GEOMETRYCOLLECTION EMPTY  
select geometry::Parse('POLYGON EMPTY').STEnvelope().ToString()  
-- returns GEOMETRYCOLLECTION EMPTY  
```  
  
 Para determinar si un objeto espacial está vacío, llame a la [STIsEmpty &#40;tipo de datos geometry&#41; ](/sql/t-sql/spatial-geometry/stisempty-geometry-data-type) método.  
  
### <a name="log-function-has-new-optional-parameter"></a>La función LOG tiene un nuevo parámetro opcional  
 El `LOG` función ahora tiene un elemento opcional *base* parámetro. Para obtener más información, consulte [registro &#40;Transact-SQL&#41;](/sql/t-sql/functions/log-transact-sql).  
  
### <a name="statistics-computation-during-partitioned-index-operations-has-changed"></a>El cálculo de estadísticas durante las operaciones de índice con particiones ha cambiado  
 En [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)], las estadísticas no se crean mediante el examen de todas las filas de la tabla cuando se crea o se vuelve a compilar un índice con particiones. En su lugar, el optimizador de consultas usa el algoritmo de muestreo predeterminado para generar estadísticas. Después de actualizar una base de datos con índices con particiones, puede observar una diferencia en los datos del histograma para estos índices. Este cambio de comportamiento puede no afectar al rendimiento de las consultas. Para obtener estadísticas sobre índices con particiones examinando todas las filas de la tabla, use CREATE STATISTICS o UPDATE STATISTICS con la cláusula FULLSCAN.  
  
### <a name="data-type-conversion-by-the-xml-value-method-has-changed"></a>La conversión de tipo de datos del método value de XML ha cambiado  
 El comportamiento interno del método `value` del tipo de datos `xml` ha cambiado. Este método realiza una consulta XQuery en XML y devuelve un valor escalar del tipo de datos especificado de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] . El tipo xs se tiene que convertir al tipo de datos de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]. Anteriormente, el método `value` convertía internamente el valor de origen una xs:string y, a continuación, convertía la xs:string al tipo de datos de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]. En [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)], la conversión a xs:string se omite en los casos siguientes:  
  
|Tipo de datos XS de origen|Tipo de datos de SQL Server de destino|  
|-------------------------|--------------------------------------|  
|byte<br /><br /> short<br /><br /> INT<br /><br /> integer<br /><br /> long<br /><br /> unsignedByte<br /><br /> unsignedShort<br /><br /> unsignedInt<br /><br /> unsignedLong<br /><br /> positiveInteger<br /><br /> nonPositiveInteger<br /><br /> negativeInteger<br /><br /> nonNegativeInteger|TINYINT<br /><br /> SMALLINT<br /><br /> INT<br /><br /> BIGINT<br /><br /> Decimal<br /><br /> NUMERIC|  
|Decimal|Decimal<br /><br /> NUMERIC|  
|FLOAT|REAL|  
|double|FLOAT|  
  
 El nuevo comportamiento mejora el rendimiento cuando la conversión intermedia puede omitirse. Sin embargo, cuando se producen errores en las conversiones de tipo de datos, aparecerán mensajes de error distintos de los que se generaban al convertir del valor xs:string intermedio. Por ejemplo, si el método value no podía convertir el valor `int` 100000 a `smallint`, el mensaje de error anterior era:  
  
 `The conversion of the nvarchar value '100000' overflowed an INT2 column. Use a larger integer column.`  
  
 En [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)], sin la conversión intermedia a xs:string, el mensaje de error es:  
  
 `Arithmetic overflow error converting expression to data type smallint.`  
  
### <a name="sqlcmdexe-behavior-change-in-xml-mode"></a>Cambio de comportamiento de sqlcmd.exe en modo XML  
 Hay cambios de comportamiento si usa sqlcmd.exe con el modo XML (: comando XML ON) al ejecutar una instrucción SELECT * desde T FOR XML...  
  
### <a name="dbcc-checkident-revised-message"></a>Mensaje revisado de CHECKIDENT DBCC  
 En [!INCLUDE[ssSQL11](../includes/sssql11-md.md)], ha cambiado el mensaje devuelto por el comando DBCC CHECKIDENT solo cuando se usa con RESEED *new_reseed_value* para cambiar el valor de identidad actual. El nuevo mensaje es "comprobación de información de identidad: valor de identidad actual '\<valor de identidad actual >'. Ejecución de DBCC completada. Si DBCC imprime algún mensaje de error, póngase en contacto con su administrador del sistema."  
  
 En versiones anteriores, el mensaje es "comprobación de información de identidad: valor de identidad actual '\<valor de identidad actual >', valor de columna actual '\<valor de columna actual >'. Ejecución de DBCC completada. Si DBCC imprime algún mensaje de error, póngase en contacto con su administrador del sistema." El mensaje no se modifica cuando DBCC CHECKIDENT se especifica con NORESEED, sin un segundo parámetro o sin un valor de reinicialización. Para obtener más información, vea [DBCC CHECKIDENT &#40;Transact-SQL&#41;](/sql/t-sql/database-console-commands/dbcc-checkident-transact-sql).  
  
### <a name="behavior-of-exist-function-on-xml-datatype-has-changed"></a>El comportamiento de la función exist() del tipo de datos XML ha cambiado  
 El comportamiento de la **exist()** función ha cambiado al comparar un tipo de datos XML con un valor null en 0 (cero). Considere el ejemplo siguiente:  
  
```xml  
DECLARE @test XML;  
SET @test = null;  
SELECT COUNT(1) WHERE @test.exist('/dogs') = 0;  
```  
  
 En versiones anteriores, esta comparación devolvía 1 (true); ahora, esta comparación devuelve 0 (cero, false).  
  
 Las comparaciones siguientes no han cambiado:  
  
```xml  
DECLARE @test XML;  
SET @test = null;  
SELECT COUNT(1) WHERE @test.exist('/dogs') = 1; -- 0 expected, 0 returned  
SELECT COUNT(1) WHERE @test.exist('/dogs') IS NULL; -- 1 expected, 1 returned  
```  
  
## <a name="see-also"></a>Vea también  
 [Cambios substanciales en las características del motor de base de datos en SQL Server 2014](breaking-changes-to-database-engine-features-in-sql-server-2016.md)   
 [Características del motor de base de datos en desuso en SQL Server 2014](deprecated-database-engine-features-in-sql-server-2016.md)   
 [Funcionalidad del motor de base de datos no incluida en SQL Server 2014](discontinued-database-engine-functionality-in-sql-server-2016.md)   
 [Nivel de compatibilidad de ALTER DATABASE &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-database-transact-sql-compatibility-level)  
  
  
