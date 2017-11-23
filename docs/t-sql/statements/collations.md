---
title: Intercalaciones | Documentos de Microsoft
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: t-sql|statements
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- COLLATE
- COLLATE_TSQL
dev_langs: TSQL
helpviewer_keywords:
- collations [SQL Server], COLLATE clause
- COLLATE clause
ms.assetid: 76763ac8-3e0d-4bbb-aa53-f5e7da021daa
caps.latest.revision: "25"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Active
ms.openlocfilehash: 4192928157e3f6e534b8fb50c34e349dac3f5b8c
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/21/2017
---
# <a name="collations"></a>Intercalaciones
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Es una cláusula que se puede aplicar a una definición de base de datos o a una definición de columna para definir la intercalación, o a una expresión de cadena de caracteres para aplicar una conversión de intercalación.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
COLLATE { <collation_name> | database_default }  
<collation_name> :: =   
     { Windows_collation_name } | { SQL_collation_name }  
```  
  
## <a name="arguments"></a>Argumentos  
 *collation_name*  
 Es el nombre de la intercalación que se va a aplicar a la expresión, definición de columna o definición de base de datos. *collation_name* puede ser solo un determinado *Windows_collation_name* o un *SQL_collation_name*. *collation_name* debe ser un valor literal. *collation_name* no se puede representar mediante una variable o expresión.  
  
 *Windows_collation_name* es el nombre de intercalación para un [nombre de intercalación de Windows](../../t-sql/statements/windows-collation-name-transact-sql.md).  
  
 *SQL_collation_name* es el nombre de intercalación para un [nombre de intercalación de SQL Server](../../t-sql/statements/sql-server-collation-name-transact-sql.md).  
  
 Al aplicar una intercalación en el nivel de definición de base de datos, las intercalaciones solo Unicode de Windows no se pueden utilizar con la cláusula COLLATE.  
  
 **database_default**  
 Hace que la cláusula COLLATE herede la intercalación de la base de datos actual.  
  
## <a name="remarks"></a>Comentarios  
 La cláusula COLLATE se puede especificar en varios niveles. Entre ellas, figuran:  
  
1.  Crear o modificar una base de datos.  
  
     Puede utilizar la cláusula COLLATE de la instrucción CREATE DATABASE o ALTER DATABASE para especificar la intercalación predeterminada de la base de datos. También puede especificar una intercalación al crear una base de datos utilizando [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]. Si no especifica ninguna intercalación, se asigna a la base de datos la intercalación predeterminada de la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
    > [!NOTE]  
    >  Intercalaciones exclusivas de Unicode de Windows sólo puede utilizarse con la cláusula COLLATE para aplicar intercalaciones a los **nchar**, **nvarchar**, y **ntext** tipos de datos en el nivel de columna y datos de nivel de expresión; no puede utilizarse con la cláusula COLLATE para cambiar la intercalación de una instancia del servidor o base de datos.  
  
2.  Crear o modificar una columna de una tabla.  
  
     Puede especificar intercalaciones para cada columna de cadena de caracteres mediante la cláusula COLLATE de la instrucción CREATE TABLE o ALTER TABLE. También puede especificar una intercalación al crear una tabla utilizando [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]. Si no especifica ninguna intercalación, se asigna a la columna la intercalación predeterminada de la base de datos.  
  
     También puede usar el `database_default` opción en la cláusula COLLATE para especificar que una columna en una tabla temporal utiliza la intercalación predeterminada de la base de datos de usuario actual para la conexión en lugar de **tempdb**.  
  
3.  Convertir la intercalación de una expresión.  
  
     Puede utilizar la cláusula COLLATE para aplicar una expresión de caracteres a una intercalación concreta. La intercalación predeterminada de la base de datos actual se asigna a los literales y las variables de carácter. La intercalación de definición de la columna se asigna a las referencias de columna.  
  
 La intercalación de un identificador depende del nivel en que está definido. Se asigna a los identificadores de objetos de instancia, como los inicios de sesión y los nombres de base de datos, la intercalación predeterminada de la instancia. Se asigna a los identificadores de objetos de una base de datos, como nombres de tablas, vistas y columnas, la intercalación predeterminada de la base de datos. Por ejemplo, es posible crear dos tablas con nombres que solo se diferencian en las mayúsculas en una base de datos con intercalación que distinga entre mayúsculas y minúsculas, pero no se pueden crear en una base de datos con una intercalación que no distinga entre mayúsculas y minúsculas. Para obtener más información, vea [Database Identifiers](../../relational-databases/databases/database-identifiers.md).  
  
 Las variables, etiquetas GOTO, procedimientos almacenados temporales y tablas temporales pueden crearse cuando se asocia el contexto de conexión a una base de datos y, a continuación, se les hace referencia cuando se ha cambiado el contexto a otra base de datos. Los identificadores para variables, etiquetas GOTO, procedimientos almacenados temporales y tablas temporales se encuentran en la intercalación predeterminada de la instancia de servidor.  
  
 La cláusula COLLATE se puede aplicar únicamente para la **char**, **varchar**, **texto**, **nchar**, **nvarchar** , y **ntext** tipos de datos.  
  
 COLLATE utiliza *collate_name* para hacer referencia al nombre de la intercalación de SQL Server o la intercalación de Windows que se aplicará a la expresión, la definición de columna o la definición de la base de datos. *collation_name* puede ser solo un determinado *Windows_collation_name* o un *SQL_collation_name* y el parámetro debe contener un valor literal. *collation_name* no se puede representar mediante una variable o expresión.  
  
 Las intercalaciones se suelen identificar mediante un nombre de intercalación, excepto en el programa de instalación. En el programa de instalación, se especifica en su lugar el designador de intercalación raíz (configuración regional de la intercalación) para las intercalaciones de Windows y, a continuación, se especifican las opciones de ordenación que distinguen o no las mayúsculas de minúsculas, o acentos.  
  
 Puede ejecutar la función de sistema [fn_helpcollations](../../relational-databases/system-functions/sys-fn-helpcollations-transact-sql.md) para recuperar una lista de todos los nombres de intercalación válidos para intercalaciones de Windows e intercalaciones de SQL Server:  
  
```  
SELECT name, description  
FROM fn_helpcollations();  
```  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] solo admite páginas de códigos compatibles con el sistema operativo subyacente. Cuando ejecuta una acción que depende de intercalaciones, la intercalación de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] utilizada por el objeto de referencia debe usar una página de códigos compatible con el sistema operativo del equipo. Entre estas acciones pueden incluirse las siguientes:  
  
-   Especificar una intercalación predeterminada para una base de datos durante su creación o modificación.  
  
-   Especificar una intercalación para una columna durante la creación o la modificación de una tabla.  
  
-   Al restaurar o adjuntar una base de datos, la intercalación predeterminada de la base de datos y la intercalación de cualquier **char**, **varchar**, y **texto** columnas o parámetros en la base de datos deben ser compatibles con el sistema operativo.  
  
     Traducción de página de códigos se admite para **char** y **varchar** tipos de datos, pero no para **texto** tipo de datos. La pérdida de datos durante la traducción de páginas de códigos no se notifica.  
  
 Si la intercalación especificada o la intercalación utilizada por el objeto que se hace referencia utiliza una página de códigos no admitida por Windows, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] muestra un error.  
  
## <a name="examples"></a>Ejemplos  
  
### <a name="a-specifying-collation-during-a-select"></a>A. Especificar la intercalación durante una selección  
 En el ejemplo siguiente se crea la tabla simple y se insertan 4 filas. A continuación, el ejemplo aplica dos intercalaciones al seleccionar datos de la tabla, mostrando cómo `Chiapas` se ordena de manera diferente.  
  
```tsql  
CREATE TABLE Locations  
(Place varchar(15) NOT NULL);  
GO  
INSERT Locations(Place) VALUES ('Chiapas'),('Colima')  
                             , ('Cinco Rios'), ('California');  
GO  
--Apply an typical collation  
SELECT Place FROM Locations  
ORDER BY Place  
COLLATE Latin1_General_CS_AS_KS_WS ASC;  
GO  
-- Apply a Spanish collation  
SELECT Place FROM Locations  
ORDER BY Place  
COLLATE Traditional_Spanish_ci_ai ASC;  
GO  
```  

 Estos son los resultados de la primera consulta.  
  
 ```
 Place 
 ------------- 
 California 
 Chiapas 
 Cinco Rios 
 Colima
 ```  
  
 Estos son los resultados de la segunda consulta.  
  
 ```
 Place 
 ------------- 
 California 
 Cinco Rios 
 Colima 
 Chiapas
 ```  
  
### <a name="b-additional-examples"></a>B. Ejemplos adicionales  
 Para obtener ejemplos adicionales que usan **COLLATE**, consulte [CREATE DATABASE &#40; Transact-SQL de SQL Server &#41; ](../../t-sql/statements/create-database-sql-server-transact-sql.md) ejemplo **g. crear una base de datos y especificar un nombre de intercalación y sus opciones**, y [ALTER TABLE &#40; Transact-SQL &#41; ](../../t-sql/statements/alter-table-transact-sql.md) ejemplo **V. cambiar la intercalación de columnas**.  
  
## <a name="see-also"></a>Vea también  
 [ALTER TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-table-transact-sql.md)   
 [Compatibilidad con la intercalación y Unicode](../../relational-databases/collations/collation-and-unicode-support.md)   
 [Prioridad de intercalación &#40;Transact-SQL&#41;](../../t-sql/statements/collation-precedence-transact-sql.md)   
 [Constantes &#40; Transact-SQL &#41;](../../t-sql/data-types/constants-transact-sql.md)   
 [CREATE DATABASE &#40;Transact-SQL de SQL Server&#41;](../../t-sql/statements/create-database-sql-server-transact-sql.md)   
 [CREATE TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/create-table-transact-sql.md)   
 [DECLARE @local_variable &#40;Transact-SQL&#41;](../../t-sql/language-elements/declare-local-variable-transact-sql.md)   
 [tabla &#40; Transact-SQL &#41;](../../t-sql/data-types/table-transact-sql.md)  
  
  
