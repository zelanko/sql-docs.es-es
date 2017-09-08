---
title: "Las características de acceso incompatible (AccessToSQL) | Documentos de Microsoft"
ms.prod: sql-non-specified
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: 
ms.technology:
- sql-ssma
ms.tgt_pltfrm: 
ms.topic: article
applies_to:
- Azure SQL Database
- SQL Server
helpviewer_keywords:
- Access databases
- Access databases, features incompatible with SQL Azure
- Access databases, features incompatible with SQL Server
- dates
- default expressions
- foreign keys
- hyperlink columns
- incompatible Access features
- indexes
- indexes, length of
- keywords
- primary keys
- reference, incompatible features
- replication columns
- special characters
- unique indexes
- validation rules
ms.assetid: 99d45b9c-e3b9-4d56-8c25-b594b887ace1
caps.latest.revision: 18
author: Shamikg
ms.author: Shamikg
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: b60bab1d71142a74c8558ce05a6ca96451e7cfc9
ms.contentlocale: es-es
ms.lasthandoff: 08/02/2017

---
# <a name="incompatible-access-features-accesstosql"></a>Características de acceso incompatible (AccessToSQL)
No todas las características de base de datos de Access son compatibles con [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]. Por ejemplo, [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] y acceso tienen distintos conjuntos de palabras clave reservadas. Problemas como éstos pueden provocar que una migración correcta a [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]. Utilice la tabla siguiente para obtener información acerca de problemas de migración posible y lo que puede hacer con ellos.  
  
## <a name="database-settings-or-features-that-might-affect-migration"></a>Configuración de base de datos o las características que podrían afectar a la migración  
  
|Obtener acceso a la opción de base de datos o característica|Problema de migración|  
|--------------------------------------|-------------------|  
|Acceso a tablas no tienen índices únicos.|Si una tabla que no tiene un índice único se migra a [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)], no se puede modificar la tabla después de la migración. Esto puede provocar problemas de compatibilidad de aplicaciones.<br /><br />Cuando se convierte los objetos de base de datos de Access, la ventana de resultados mostrará cualquier acceso a tablas que no tienen índices únicos.<br /><br />Puede configurar el acceso para agregar una clave principal en la [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] tabla durante la conversión. Para obtener más información, consulte [configuración del proyecto (conversión)](http://msdn.microsoft.com/en-us/bcebc635-c638-4ddb-924c-b9ccfef86388).|  
|Acceso a tablas tienen columnas de replicación.|Si una tabla de Access que incluye las columnas del sistema de replicación se migra a [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)], se interrumpirá la funcionalidad de replicación de Jet después de la migración.<br /><br />Tras la migración, considere el uso de [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] replicación para mantener sincronizadas copias de las bases de datos.|  
|Acceso a tablas que tienen índices únicos contengan varios valores null.|Acceso a tablas que tienen índices únicos con varios valores null no se puede transferir a [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)], porque en [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)], índices únicos no permitir varios valores nulos. Se producirá un error de migración de estas tablas.<br /><br />SSMA marcará este problema en los informes de evaluación. Para crear un informe de evaluación, consulte [evaluar objetos de base de datos de acceso para la conversión](http://msdn.microsoft.com/en-us/8b9e23d6-da62-437a-8c05-8ad2628b9441).<br /><br />Si se produce este problema, debe asegurarse de que la clave principal no tiene los valores nulos duplicados. O bien, debe quitar la clave principal o índices únicos que contienen varios valores null.|  
|Acceso a tablas contienen valores de fecha que están fuera de la [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] intervalo.|El [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] **datetime** tipo acepta fechas en el intervalo de 1 de enero de 1753 a 31 de diciembre de 9999 solo. Acceso acepta fechas en el intervalo de 1 de enero de 100 al 31 de diciembre de 9999.<br /><br />SSMA marcará este problema en los informes de evaluación. Para crear un informe de evaluación, consulte [evaluar objetos de base de datos de acceso para la conversión](http://msdn.microsoft.com/en-us/8b9e23d6-da62-437a-8c05-8ad2628b9441).<br /><br />Puede configurar cómo SSMA resuelve las fechas que están fuera de la [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] intervalo. Para obtener más información, consulte [configuración del proyecto (migración)](http://msdn.microsoft.com/en-us/4caebc9c-8680-4b99-a8fa-89c43161c95d).|  
|Longitudes de índice en Access superan los 900 bytes.|[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]los índices tienen un límite de 900 bytes para el tamaño total de columnas de clave de índice. Si las tablas de Access utilizan índices más grandes, SSMA mostrará una advertencia.<br /><br />Si continúa con la migración de datos, se puede producir un error en la migración.|  
|Nombres de objeto de acceso [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] palabras clave, o contener caracteres especiales.|Acceso y [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] tienen distintos conjuntos de palabras clave reservadas y caracteres especiales. [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]acepte objetos cuyos nombran mediante el uso de [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] palabras clave o que contienen caracteres especiales si se utilizan identificadores entre corchetes o entre comillas, como "select" o [Active] .p. Para obtener más información, vea "Identificadores delimitados (motor de base de datos)" en [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] libros en pantalla.<br /><br />**Nota:** para usar comillas para delimitar identificadores, SET QUOTED_IDENTIFIER debe ser ON.<br /><br />Por ejemplo, `CREATE TABLE [schema](c1 [FOR])` es una instrucción válida, aunque **esquema** y **para** son palabras clave reservadas. Además, `CREATE TABLE [xxx*yyy](c1 x&y)` es una instrucción válida, aunque el nombre de tabla y columna contenga los caracteres especiales  **\&#42;** y  **&amp;** .<br /><br />Todas las consultas que hacen referencia a esos objetos también deben utilizar los nombres con corchetes o comillas. Por ejemplo, la consulta `SELECT * FROM schema` se producirá un error. La consulta correcta es: `SELECT * FROM [schema]`.<br /><br />Cuando se convierte los objetos de base de datos de Access, el panel de resultados mostrará cualquier acceso a tablas que usan palabras clave o caracteres especiales. Puede modificar las tablas de Access y, a continuación, quitar y agregar la base de datos de nuevo; o bien, puede modificar las consultas que hacen referencia a esos objetos para que las consultas utilizan corchetes o comillas para delimitar identificadores. Si no modifica las consultas, las aplicaciones de Access pueden devolver errores o tener otros problemas.|  
|Tamaño de los campos difiere en las relaciones de clave principales/clave externa.|[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]no se admite la funcionalidad de Jet sobre la vinculación de las columnas que tienen tipos de datos diferentes o tamaños con restricciones foreign key.<br /><br />Al convertir objetos de base de datos de Access, la ventana de salida mostrará una lista cualquier principales/claves restricciones de clave externa que no se convertirán a [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]. Puede modificar los tipos de datos y tamaños de las columnas de acceso para que puedan coinciden y, a continuación, quitarán y volver a agregar la base de datos de Access. O bien, puede migrar datos aunque estas restricciones no se creará en [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)].|  
|Las tablas que se hace referencia en las relaciones de acceso tienen una clave principal ni un índice único.|Acceso acepta la relación entre las tablas donde la tabla que se hace referencia no tiene una clave principal o un índice único. Sin embargo, esto no es compatible con [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)].<br /><br />Cuando se convierte los objetos de base de datos de Access, la ventana de resultados mostrará todas las tablas que no tienen relaciones pero ninguna clave principal o un índice único. Puede modificar las tablas para agregar las claves principales o índices únicos y, a continuación, quitar y volver a agregar la base de datos de Access. O bien, puede migrar datos aunque la relación entre las tablas se interrumpirá.|  
|Acceso a tablas tienen columnas de hipervínculo.|[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]no admite **hipervínculo** columnas. En su lugar, las columnas se tratan como columnas de memorando de acceso. De forma predeterminada, estas columnas se convertirá en **nvarchar (max)** columnas en [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]. Puede personalizar la asignación. Para obtener más información, consulte [tipos de datos de destino y origen de asignación](http://msdn.microsoft.com/en-us/b362a075-16e7-423f-b63f-e1e9f02844a9).|  
|Valor predeterminado o la validación de expresiones de reglas contienen funciones de acceso que no se puede convertir a [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] o SQL Azure.|Expresiones de acceso predeterminadas o las reglas de validación podrían incluir funciones del sistema de acceso o funciones definidas por el usuario que no se asignan a [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] o SQL Azure. Uso de funciones que no se asignan a [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] o SQL Azure no podrá cargar las expresiones predeterminadas o las reglas de validación en [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] o SQL Azure.|  
  
## <a name="see-also"></a>Vea también  
[Preparar las bases de datos de acceso para la migración](http://msdn.microsoft.com/en-us/9b80a9e0-08e7-4b4d-b5ec-cc998d3f5114)  
[Migrar bases de datos de Access a SQL Server](http://msdn.microsoft.com/en-us/76a3abcf-2998-4712-9490-fe8d872c89ca)  
  

