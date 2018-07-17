---
title: Registrar tipos definidos por el usuario en SQL Server | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology: clr
ms.tgt_pltfrm: ''
ms.topic: reference
dev_langs:
- TSQL
helpviewer_keywords:
- UDTs [CLR integration], maintaining
- user-defined types [CLR integration], maintaining
- dependencies [CLR integration]
- deploying user-defined types [CLR integration]
- CurrencyConversion function
- user-defined types [CLR integration], deploying
- Transact-SQL deploying UDTs
- assemblies [CLR integration], user-defined types
- cross-database UDT support
- CREATE ASSEMBLY statement
- DROP TYPE statement
- Currency UDT
- CREATE TYPE statement
- registering user-defined types
- UDTs [CLR integration], deploying
- removing user-defined types
- user-defined types [CLR integration], registering
- ALTER ASSEMBLY statement
- UDTs [CLR integration], registering
- ADD FILE clause
ms.assetid: f7da3e92-e407-4f0b-b3a3-f214e442b37d
caps.latest.revision: 25
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 1307f5b351ab77e9fb61160f4a0ad73a5eb06eb6
ms.sourcegitcommit: 022d67cfbc4fdadaa65b499aa7a6a8a942bc502d
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/03/2018
ms.locfileid: "37351537"
---
# <a name="registering-user-defined-types-in-sql-server"></a>Registrar tipos definidos por el usuario en SQL Server
  Para poder usar un tipo definido por el usuario (UDT) en [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], debe registrarlo. El registro de un UDT implica el registro del ensamblado y la creación del tipo en la base de datos en la que desea usarlo. El ámbito de los UDT es una sola base de datos, por lo que no pueden usarse en varias bases de datos a menos que se registren un ensamblado y UDT idénticos en cada base de datos. Una vez que haya registrado el ensamblado UDT y que haya creado el tipo, podrá usar el UDT en [!INCLUDE[tsql](../../includes/tsql-md.md)] y en el código del cliente. Para obtener más información, vea [Tipos definidos por el usuario de CLR](clr-user-defined-types.md).  
  
## <a name="using-visual-studio-to-deploy-udts"></a>Usar Visual Studio para implementar tipos UDT  
 La forma más fácil de implementar un UDT consiste en usar [!INCLUDE[msCoName](../../includes/msconame-md.md)] Visual Studio. Sin embargo, en escenarios de implementación más complejos y para obtener la máxima flexibilidad, es preferible que use [!INCLUDE[tsql](../../includes/tsql-md.md)] tal y como se describe más adelante en este tema.  
  
 Siga estos pasos para crear e implementar un UDT mediante Visual Studio:  
  
1.  Cree un nuevo **base de datos** del proyecto en el **Visual Basic** o **Visual C#** nodos de lenguaje.  
  
2.  Agregue una referencia a la base de datos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que contenga el UDT.  
  
3.  Agregar un **User-Defined Type** clase.  
  
4.  Escriba código para implementar el UDT.  
  
5.  Desde el **compilar** menú, seleccione **implementar**. De este modo, se registrará el ensamblado y se creará el tipo en la base de datos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
## <a name="using-transact-sql-to-deploy-udts"></a>Usar Transact-SQL para implementar tipos UDT  
 La sintaxis de la instrucción CREATE ASSEMBLY de [!INCLUDE[tsql](../../includes/tsql-md.md)] se usa para registrar el ensamblado en la base de datos en la que se desea usar el UDT. Se almacena internamente en las tablas del sistema de la base de datos, no externamente en el sistema de archivos. Si el UDT depende de ensamblados externos, éstos también deben cargarse en la base de datos. La instrucción CREATE TYPE se usa para crear el UDT en la base de datos en la que va a utilizarse. Para obtener más información, consulte [CREATE ASSEMBLY &#40;Transact-SQL&#41; ](/sql/t-sql/statements/create-assembly-transact-sql) y [CREATE TYPE &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-type-transact-sql).  
  
### <a name="using-create-assembly"></a>Usar CREATE ASSEMBLY  
 La sintaxis de la instrucción CREATE ASSEMBLY registra el ensamblado en la base de datos en la que se desea usar el UDT. Cuando se registra el ensamblado, no tiene ninguna dependencia.  
  
 No está permitido crear varias versiones del mismo ensamblado en una base de datos determinada. Sin embargo, es posible crear varias versiones del mismo ensamblado basadas en la referencia cultural en una base de datos determinada. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] distingue varias versiones de referencia cultural de un ensamblado mediante los distintos nombres registrados en la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Para obtener más información, vea el tema sobre la forma de crear y utilizar ensamblados con nombres seguros en .NET Framework SDK.  
  
 Al ejecutar CREATE ASSEMBLY con los conjuntos de permisos SAFE o EXTERNAL_ACCESS, se comprueba el ensamblado para garantizar que sea comprobable y presente seguridad de tipos. Si no se especifica ningún conjunto de permisos, se usa el conjunto de permisos SAFE. El código con el conjunto de permisos UNSAFE no se comprueba. Para obtener más información sobre los conjuntos de permisos de ensamblado, vea [Diseño de ensamblados](../../relational-databases/clr-integration/assemblies-designing.md).  
  
#### <a name="example"></a>Ejemplo  
 La siguiente [!INCLUDE[tsql](../../includes/tsql-md.md)] instrucción registra el ensamblado Point de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] en el **AdventureWorks** base de datos, con el conjunto de permisos SAFE. Si se omite la cláusula PERMISSION_SET, el ensamblado se registra con el conjunto de permisos SAFE.  
  
```  
USE AdventureWorks;  
CREATE ASSEMBLY Point  
FROM '\\ShareName\Projects\Point\bin\Point.dll'   
WITH PERMISSION_SET = SAFE;  
```  
  
 La siguiente [!INCLUDE[tsql](../../includes/tsql-md.md)] instrucción registra el ensamblado utilizando *< assembly_bits >* argumento en la cláusula FROM. Este valor `varbinary` representa el archivo como un flujo de bytes.  
  
```  
USE AdventureWorks;  
CREATE ASSEMBLY Point  
FROM 0xfeac4 … 21ac78  
```  
  
### <a name="using-create-type"></a>Usar CREATE TYPE  
 Una vez que haya cargado el ensamblado en la base de datos, podrá crear el tipo mediante la instrucción CREATE TYPE de [!INCLUDE[tsql](../../includes/tsql-md.md)]. De esta forma, el tipo se agregará a la lista de tipos disponibles para esa base de datos. El tipo tiene como ámbito la base de datos y solamente puede usarse en la base de datos en la que se creó. Si el UDT ya existe en la base de datos, la instrucción CREATE TYPE generará un error.  
  
> [!NOTE]  
>  La sintaxis de la instrucción CREATE TYPE también se usa para crear tipos de datos de alias nativos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] y sirve para reemplazar `sp_addtype` como un medio de creación de tipos de datos de alias. Algunos de los argumentos opcionales de la sintaxis de CREATE TYPE hacen referencia a la creación de UDTs y no sirven para crear tipos de datos de alias (como el tipo base).  
  
 Para obtener más información, consulte [CREATE TYPE &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-type-transact-sql).  
  
#### <a name="example"></a>Ejemplo  
 La siguiente instrucción [!INCLUDE[tsql](../../includes/tsql-md.md)] crea el tipo `Point`. EXTERNAL NAME se especifica mediante la sintaxis de nomenclatura de dos partes de *AssemblyName*. *Nombreudt*.  
  
```  
CREATE TYPE dbo.Point   
EXTERNAL NAME Point.[Point];  
```  
  
## <a name="removing-a-udt-from-the-database"></a>Quitar un UDT de la base de datos  
 La instrucción DROP TYPE quita un UDT de la base de datos actual. Una vez quitado un UDT, puede utilizar la instrucción DROP ASSEMBLY para quitar el ensamblado de la base de datos.  
  
 La instrucción DROP TYPE no se ejecuta en las situaciones siguientes:  
  
-   Tablas de la base de datos que contienen columnas definidas mediante el UDT.  
  
-   Funciones, procedimientos almacenados o desencadenadores que usan variables o parámetros del UDT creados en la base de datos con la cláusula WITH SCHEMABINDING.  
  
### <a name="example"></a>Ejemplo  
 La siguiente consulta [!INCLUDE[tsql](../../includes/tsql-md.md)] debe ejecutarse en el orden que se indica. En primer lugar, debe quitarse la tabla que hace referencia al UDT `Point`, después, el tipo y, por último, el ensamblado.  
  
```  
DROP TABLE dbo.Points;  
DROP TYPE dbo.Point;  
DROP ASSEMBLY Point;  
```  
  
### <a name="finding-udt-dependencies"></a>Buscar dependencias UDT  
 Si hay objetos dependientes, como tablas con definiciones de columna UDT, se produce un error en la instrucción DROP TYPE. También produce un error si hay funciones, procedimientos almacenados o desencadenadores creados en la base de datos con la cláusula WITH SCHEMABINDING, cuando estas rutinas utilizan variables o parámetros del tipo definido por el usuario. Debe quitar primero todos los objetos dependientes y, a continuación, ejecutar la instrucción DROP TYPE.  
  
 La siguiente [!INCLUDE[tsql](../../includes/tsql-md.md)] consulta busca todas las columnas y parámetros que usan un UDT en el **AdventureWorks** base de datos.  
  
```  
USE Adventureworks;  
SELECT o.name AS major_name, o.type_desc AS major_type_desc  
     , c.name AS minor_name, c.type_desc AS minor_type_desc  
     , at.assembly_class  
  FROM (  
        SELECT object_id, name, user_type_id, 'SQL_COLUMN' AS type_desc  
          FROM sys.columns  
     UNION ALL  
        SELECT object_id, name, user_type_id, 'SQL_PROCEDURE_PARAMETER'  
          FROM sys.parameters  
     ) AS c  
  JOIN sys.objects AS o  
    ON o.object_id = c.object_id  
  JOIN sys.assembly_types AS at  
    ON at.user_type_id = c.user_type_id;  
```  
  
## <a name="maintaining-udts"></a>Mantener los UDT  
 No es posible modificar un UDT una vez creado en una base de datos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], pero puede modificar el ensamblado en el que se basa el tipo. En la mayoría de los casos, tendrá que quitar el UDT de la base de datos con la instrucción DROP TYPE de [!INCLUDE[tsql](../../includes/tsql-md.md)], efectuar cambios en el ensamblado subyacente y volver a cargarlo mediante la instrucción ALTER ASSEMBLY. A continuación, tendrá que volver a crear el UDT y todos los objetos dependientes.  
  
### <a name="example"></a>Ejemplo  
 La instrucción ALTER ASSEMBLY se usa después de haber realizado cambios en el código fuente del ensamblado UDT y después de haberlo compilado de nuevo. Esta instrucción copia el archivo .dll en el servidor y lo enlaza al nuevo ensamblado. Para ver la sintaxis completa, consulte [ALTER ASSEMBLY &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-assembly-transact-sql).  
  
 La siguiente instrucción ALTER ASSEMBLY de [!INCLUDE[tsql](../../includes/tsql-md.md)] vuelve a cargar el ensamblado Point.dll desde la ubicación del disco especificada.  
  
```  
ALTER ASSEMBLY Point  
FROM '\\Projects\Point\bin\Point.dll'  
```  
  
### <a name="using-alter-assembly-to-add-source-code"></a>Usar ALTER ASSEMBLY para agregar código fuente  
 La cláusula ADD FILE de la sintaxis ALTER ASSEMBLY no está presente en CREATE ASSEMBLY. Puede usarla para agregar código fuente o cualquier otro archivo asociado a un ensamblado. Los archivos se copian desde sus ubicaciones originales y se almacenan en tablas del sistema en la base de datos. De esta forma, se garantiza que el código fuente u otros archivos estén disponibles siempre que sea necesario volver a crear o documentar la versión actual del UDT.  
  
 La siguiente [!INCLUDE[tsql](../../includes/tsql-md.md)] instrucción ALTER ASSEMBLY agrega el código de origen de clase Point.cs para el `Point` UDT. De esta forma, el texto incluido en el archivo Point.cs se copia y se almacena en la base de datos con el nombre "PointSource".  
  
```  
ALTER ASSEMBLY Point  
ADD FILE FROM '\\Projects\Point\Point.cs' AS PointSource;  
```  
  
 Información de ensamblado se almacena en el **sys.assembly_files** tabla en la base de datos que se ha instalado el ensamblado. El **sys.assembly_files** tabla contiene las siguientes columnas.  
  
 **assembly_id**  
 Identificador definido para el ensamblado. Este número se asigna a todos los objetos relacionados con el mismo ensamblado.  
  
 **Nombre**  
 Nombre del objeto.  
  
 **file_id**  
 Número que identifica cada objeto, con el primer objeto asociado a un determinado **assembly_id** que se le asigna el valor de 1. Si hay varios objetos asociados con el mismo **assembly_id**, a continuación, cada **file_id** valor se incrementa en 1.  
  
 **contenido**  
 Representación hexadecimal del ensamblado o archivo.  
  
 Puede usar la función CAST o CONVERT para convertir el contenido de la **contenido** columna en texto legible. La consulta siguiente convierte el contenido del archivo Point.cs en texto legible, utilizando el nombre de la cláusula WHERE para restringir el conjunto de resultados a una única fila.  
  
```  
SELECT CAST(content AS varchar(8000))   
  FROM sys.assembly_files   
  WHERE name='PointSource';  
```  
  
 Si copia y pega los resultados en un editor de texto, verá que se han conservado los saltos de línea y los espacios originales.  
  
## <a name="managing-udts-and-assemblies"></a>Administrar UDT y ensamblados  
 A la hora de planear la implementación de los UDT, tenga en cuenta qué métodos se necesitan en el propio ensamblado UDT y qué métodos deberían crearse en ensamblados independientes e implementarse como funciones o procedimientos almacenados definidos por el usuario. Si separa los métodos en ensamblados distintos, podrá actualizar el código sin que esto afecte a los datos almacenados en una columna UDT de una tabla. Solo podrá modificar los ensamblados UDT sin quitar las columnas UDT y otros objetos dependientes cuando la nueva definición pueda leer los valores anteriores y la firma del tipo no cambie.  
  
 Puede simplificar considerablemente el mantenimiento separando el código de los procedimientos que pueden cambiar del código necesario para implementar el UDT. Si solamente incluye el código necesario para que el UDT funcione y crea las definiciones UDT de la forma más simple posible, se reducirá el riesgo de que el propio UDT tenga quitarse de la base de datos a la hora de revisar el código o corregir errores.  
  
### <a name="the-currency-udt-and-currency-conversion-function"></a>El UDT Currency y la función de conversión de monedas  
 El **moneda** UDT en el **AdventureWorks** base de datos de ejemplo proporciona un ejemplo útil del modo recomendado de estructurar un UDT y sus funciones asociadas. El **moneda** UDT se usa para administrar valores de moneda según el sistema monetario de una determinada referencia cultural y permite almacenar distintos tipos de moneda, como dólares, euros y así sucesivamente. La clase UDT expone un nombre de referencia cultural como una cadena y un importe monetario como un tipo de datos `decimal`. Todos los métodos de serialización necesarios están incluidos en el ensamblado que define la clase. La función que implementa la conversión de moneda de una referencia cultural a otra se implementa como una función externa denominada **ConvertCurrency**, y esta función se encuentra en un ensamblado independiente. El **ConvertCurrency** función realiza su trabajo mediante la recuperación de la tasa de conversión de una tabla en la **AdventureWorks** base de datos. Si alguna vez debe cambiar el origen de las tasas de conversión, o si debe haber otros cambios en el código existente, el ensamblado puede modificarse fácilmente sin que afecte a la **moneda** UDT.  
  
 La lista de código la **moneda** UDT y **ConvertCurrency** funciones pueden encontrarse al instalar los ejemplos de common language runtime (CLR).  
  
### <a name="using-udts-across-databases"></a>Usar tipos UDT en varias bases de datos  
 El ámbito de los UDT es, por definición, una sola base de datos. Por lo tanto, un UDT definido en una base de datos no puede usarse en una definición de columna de otra base de datos. Para usar los UDT en varias bases de datos, debe ejecutar las instrucciones CREATE ASSEMBLY y CREATE TYPE en cada base de datos en ensamblados idénticos. Los ensamblados se consideran idénticos si tienen el mismo nombre, nombre seguro, referencia cultural, versión, conjunto de permisos y contenido binario.  
  
 Cuando el UDT se haya registrado y esté accesible en ambas bases de datos, podrá convertir un valor UDT de una base de datos para utilizarlo en la otra. Pueden usarse UDT idénticos en varias bases de datos en los escenarios siguientes:  
  
-   Al llamar a un procedimiento almacenado definido en bases de datos diferentes.  
  
-   Al consultar tablas definidas en bases de datos diferentes.  
  
-   Al seleccionar datos UDT de una columna UDT de una tabla de base de datos e insertarlos en una segunda base de datos con una columna UDT idéntica.  
  
 En estas situaciones, todas las conversiones que requiere el servidor se realizan automáticamente. No puede realizar las conversiones de forma explícita utilizando las funciones CAST o CONVERT de [!INCLUDE[tsql](../../includes/tsql-md.md)].  
  
 Tenga en cuenta que no es necesario realizar ninguna acción para utilizar los UDT cuando [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] crea las tablas de trabajo en el **tempdb** base de datos del sistema. Esto incluye la administración de los cursores, variables de tabla, y funciones definidas por el usuario de con valores de tabla que se incluyen de forma transparente los UDT y que hace uso de **tempdb**. Sin embargo, si crea explícitamente una tabla temporal en **tempdb** que define una columna UDT, a continuación, el UDT debe estar registrado en **tempdb** la misma manera que una base de datos de usuario.  
  
## <a name="see-also"></a>Vea también  
 [Tipos definidos por el usuario de CLR](clr-user-defined-types.md)  
  
  
