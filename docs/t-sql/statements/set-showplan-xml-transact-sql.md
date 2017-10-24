---
title: SET SHOWPLAN_XML (Transact-SQL) | Documentos de Microsoft
ms.custom: 
ms.date: 06/10/2016
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- SET SHOWPLAN_XML
- SET_SHOWPLAN_XML_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- statements [SQL Server], estimates
- SET SHOWPLAN_XML statement
- execution information and estimates [SQL Server]
- statements [SQL Server], information without processing
- XML [SQL Server], statement execution information
- SHOWPLAN_XML option
- estimated execution information [SQL Server]
ms.assetid: a467a1b3-10a5-43c4-9085-13d8aed549c9
caps.latest.revision: 48
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 3414096227310460a0a1b58a34cb0fbc4e528649
ms.contentlocale: es-es
ms.lasthandoff: 09/01/2017

---
# <a name="set-showplanxml-transact-sql"></a>SET SHOWPLAN_XML (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Hace que [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] no ejecute instrucciones [!INCLUDE[tsql](../../includes/tsql-md.md)]. En su lugar, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] devuelve información detallada de cómo se van a ejecutar las instrucciones con el formato de un documento XML bien definido.  
 
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
SET SHOWPLAN_XML { ON | OFF }  
```  
  
## <a name="remarks"></a>Comentarios  
 La opción SET SHOWPLAN_XML se establece en tiempo de ejecución, no en tiempo de análisis.  
  
 Cuando SET SHOWPLAN_XML es ON, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] devuelve información del plan de ejecución para cada instrucción sin ejecutarla y [!INCLUDE[tsql](../../includes/tsql-md.md)] no se ejecutan las instrucciones. Cuando esta opción está establecida en ON, se devuelve información acerca del plan de ejecución de todas las instrucciones [!INCLUDE[tsql](../../includes/tsql-md.md)] siguientes hasta que se vuelve a establecer en OFF. Por ejemplo, si se ejecuta una instrucción CREATE TABLE cuando SET SHOWPLAN_XML es ON y después se ejecuta una instrucción SELECT en la que se especifica la tabla creada, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] devuelve un mensaje de error, ya que la tabla no existe. Por ello, las referencias posteriores que se hagan a la tabla generarán un error. Cuando SET SHOWPLAN_XML está establecida en OFF, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ejecuta las instrucciones sin generar ningún informe.  
  
 SET SHOWPLAN_XML está diseñada para devolver datos **nvarchar (max)** para aplicaciones como el **sqlcmd** utilidad, donde la salida XML se utiliza otras herramientas para mostrar y procesar la consulta información del plan.  
  
> [!NOTE]  
>  La vista de administración dinámica **sys.dm_exec_query_plan**, devuelve la misma información que SET SHOWPLAN XML en el **xml** tipo de datos. Esta información se devuelve desde el **query_plan** columna de **sys.dm_exec_query_plan**. Para obtener más información, consulte [sys.dm_exec_query_plan &#40; Transact-SQL &#41; ](../../relational-databases/system-dynamic-management-views/sys-dm-exec-query-plan-transact-sql.md).  
  
 SET SHOWPLAN_XML no se puede especificar en un procedimiento almacenado. Debe ser la única instrucción en un lote.  
  
 SET SHOWPLAN_XML devuelve información como un conjunto de documentos XML. Cada lote después de la instrucción SET SHOWPLAN_XML ON se refleja en la salida con un único documento. Cada documento contiene el texto de las instrucciones del lote, seguido de los detalles de los pasos de ejecución. El documento muestra los costos estimados, el número de filas, los índices a los que se ha obtenido acceso y los tipos de operadores utilizados, el orden de combinación y más información acerca de los planes de ejecución.  
  
 El documento que contiene el esquema XML de la salida XML de SET SHOWPLAN_XML se copia durante la instalación en un directorio local del equipo en el que se instala Microsoft [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Se encuentra en la unidad que contiene los archivos de instalación de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], en:  
  
 \Microsoft SQL Server\130\Tools\Binn\schemas\sqlserver\2004\07\showplan\showplanxml.xsd  
  
 También puede encontrarse en el esquema del plan de presentación [este sitio Web](http://go.microsoft.com/fwlink/?linkid=43100&clcid=0x409).  
  
> [!NOTE]  
>  Si **incluir Plan de ejecución real** está seleccionado en [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], esta opción SET no produce resultado del plan de presentación XML. Desactive el **incluir Plan de ejecución real** botón antes de utilizarla opción SET..  
  
## <a name="permissions"></a>Permissions  
 Para utilizar SET SHOWPLAN_XML, debe disponer de permisos suficientes para ejecutar las instrucciones en las que se ejecuta SET SHOWPLAN_XML, y debe tener el permiso SHOWPLAN para todas las bases de datos que contengan objetos a los que se hace referencia.  
  
 Para SELECT, INSERT, UPDATE, DELETE, EXEC *stored_procedure*y EXEC *user_defined_function* instrucciones para generar un plan de presentación que el usuario debe:  
  
-   Tener los permisos correspondientes para ejecutar las instrucciones [!INCLUDE[tsql](../../includes/tsql-md.md)].  
  
-   Tener el permiso SHOWPLAN en todas las bases de datos que contengan objetos a los que hacen referencia las instrucciones [!INCLUDE[tsql](../../includes/tsql-md.md)], como tablas, vistas, etc.  
  
 Para todas las demás instrucciones, como DDL, USE *database_name*, conjunto, DECLARE, SQL dinámica y así sucesivamente, solo los permisos adecuados para ejecutar el [!INCLUDE[tsql](../../includes/tsql-md.md)] son necesarias las instrucciones.  
  
## <a name="examples"></a>Ejemplos  
 Las dos instrucciones siguientes utilizan la opción SET SHOWPLAN_XML para mostrar la forma en que [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] analiza y optimiza el uso de índices en las consultas.  
  
 La primera consulta utiliza el operador de comparación es igual a (=) en la cláusula WHERE de una columna indizada. La segunda consulta utiliza el operador LIKE en la cláusula WHERE. De este modo, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] debe utilizar un recorrido de índice clúster para encontrar los datos que cumplen la condición de la cláusula WHERE. Los valores de la **EstimateRows** y **EstimatedTotalSubtreeCost** atributos son inferiores en la primera consulta indizada, lo que indica que se procesa mucho más rápidamente y consume menos recursos que el consultas no indizadas.  
  
```  
USE AdventureWorks2012;  
GO  
SET SHOWPLAN_XML ON;  
GO  
-- First query.  
SELECT BusinessEntityID   
FROM HumanResources.Employee  
WHERE NationalIDNumber = '509647174';  
GO  
-- Second query.  
SELECT BusinessEntityID, JobTitle  
FROM HumanResources.Employee  
WHERE JobTitle LIKE 'Production%';  
GO  
SET SHOWPLAN_XML OFF;  
```  
  
## <a name="see-also"></a>Vea también  
 [Instrucciones SET &#40;Transact-SQL&#41;](../../t-sql/statements/set-statements-transact-sql.md)  
  
  

