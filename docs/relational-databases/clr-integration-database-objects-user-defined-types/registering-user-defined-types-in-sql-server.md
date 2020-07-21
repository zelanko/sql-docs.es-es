---
title: Registrando tipos definidos por el usuario en SQL Server | Microsoft Docs
description: Debe registrar un UDT antes de instalarlo en SQL Server. Debe registrar el ensamblado y crear el tipo en la base de datos donde desea usarlo.
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: clr
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
author: rothja
ms.author: jroth
ms.openlocfilehash: 8918b20e02eb0d7045ad7e6603ed1f6cf4db40b8
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/01/2020
ms.locfileid: "85727776"
---
# <a name="registering-user-defined-types-in-sql-server"></a>Registrar tipos definidos por el usuario en SQL Server
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  Para poder usar un tipo definido por el usuario (UDT) en [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , debe registrarlo. El registro de un UDT implica el registro del ensamblado y la creación del tipo en la base de datos en la que desea usarlo. El ámbito de los UDT es una sola base de datos, por lo que no pueden usarse en varias bases de datos a menos que se registren un ensamblado y UDT idénticos en cada base de datos. Una vez que haya registrado el ensamblado UDT y que haya creado el tipo, podrá usar el UDT en [!INCLUDE[tsql](../../includes/tsql-md.md)] y en el código del cliente. Para obtener más información, vea [Tipos definidos por el usuario de CLR](../../relational-databases/clr-integration-database-objects-user-defined-types/clr-user-defined-types.md).  
  
## <a name="using-visual-studio-to-deploy-udts"></a>Usar Visual Studio para implementar tipos UDT  
 La forma más fácil de implementar un UDT consiste en usar [!INCLUDE[msCoName](../../includes/msconame-md.md)] Visual Studio. Sin embargo, en escenarios de implementación más complejos y para obtener la máxima flexibilidad, es preferible que use [!INCLUDE[tsql](../../includes/tsql-md.md)] tal y como se describe más adelante en este tema.  
  
 Siga estos pasos para crear e implementar un UDT mediante Visual Studio:  
  
1.  Cree un nuevo proyecto de **base de datos** en los nodos del lenguaje **Visual Basic** o **Visual C#** .  
  
2.  Agregue una referencia a la base de datos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que contenga el UDT.  
  
3.  Agregue una clase de **tipo definido por el usuario** .  
  
4.  Escriba código para implementar el UDT.  
  
5.  En el menú **compilar** , seleccione **implementar**. De este modo, se registrará el ensamblado y se creará el tipo en la base de datos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  

## <a name="using-transact-sql-to-deploy-udts"></a>Usar Transact-SQL para implementar tipos UDT  
 La sintaxis de la instrucción CREATE ASSEMBLY de [!INCLUDE[tsql](../../includes/tsql-md.md)] se usa para registrar el ensamblado en la base de datos en la que se desea usar el UDT. Se almacena internamente en las tablas del sistema de la base de datos, no externamente en el sistema de archivos. Si el UDT depende de ensamblados externos, éstos también deben cargarse en la base de datos. La instrucción CREATE TYPE se usa para crear el UDT en la base de datos en la que va a utilizarse. Para obtener más información, vea [Create assembly &#40;Transact-sql&#41;](../../t-sql/statements/create-assembly-transact-sql.md) y [Create Type &#40;transact-SQL&#41;](../../t-sql/statements/create-type-transact-sql.md).  
  
### <a name="using-create-assembly"></a>Usar CREATE ASSEMBLY  
 La sintaxis de la instrucción CREATE ASSEMBLY registra el ensamblado en la base de datos en la que se desea usar el UDT. Cuando se registra el ensamblado, no tiene ninguna dependencia.  
  
 No está permitido crear varias versiones del mismo ensamblado en una base de datos determinada. Sin embargo, es posible crear varias versiones del mismo ensamblado basadas en la referencia cultural en una base de datos determinada. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] distingue varias versiones de referencia cultural de un ensamblado mediante los distintos nombres registrados en la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Para obtener más información, vea el tema sobre la forma de crear y utilizar ensamblados con nombres seguros en .NET Framework SDK.  
  
 Al ejecutar CREATE ASSEMBLY con los conjuntos de permisos SAFE o EXTERNAL_ACCESS, se comprueba el ensamblado para garantizar que sea comprobable y presente seguridad de tipos. Si no se especifica ningún conjunto de permisos, se usa el conjunto de permisos SAFE. El código con el conjunto de permisos UNSAFE no se comprueba. Para obtener más información sobre los conjuntos de permisos de ensamblado, vea [Diseño de ensamblados](../../relational-databases/clr-integration/assemblies-designing.md).  
  
#### <a name="example"></a>Ejemplo  
 La [!INCLUDE[tsql](../../includes/tsql-md.md)] instrucción siguiente registra el ensamblado de punto en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] en la base de datos **AdventureWorks** , con el conjunto de permisos Safe. Si se omite la cláusula PERMISSION_SET, el ensamblado se registra con el conjunto de permisos SAFE.  
  
```  
USE AdventureWorks;  
CREATE ASSEMBLY Point  
FROM '\\ShareName\Projects\Point\bin\Point.dll'   
WITH PERMISSION_SET = SAFE;  
```  
  
 La [!INCLUDE[tsql](../../includes/tsql-md.md)] instrucción siguiente registra el ensamblado mediante *<assembly_bits argumento>* en la cláusula FROM. Este valor **varbinary** representa el archivo como un flujo de bytes.  
  
```  
USE AdventureWorks;  
CREATE ASSEMBLY Point  
FROM 0xfeac4 ... 21ac78  
```  
  
### <a name="using-create-type"></a>Usar CREATE TYPE  
 Una vez que haya cargado el ensamblado en la base de datos, podrá crear el tipo mediante la instrucción CREATE TYPE de [!INCLUDE[tsql](../../includes/tsql-md.md)]. De esta forma, el tipo se agregará a la lista de tipos disponibles para esa base de datos. El tipo tiene como ámbito la base de datos y solamente puede usarse en la base de datos en la que se creó. Si el UDT ya existe en la base de datos, la instrucción CREATE TYPE generará un error.  
  
> [!NOTE]  
>  La sintaxis de CREATE TYPE también se usa para crear [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tipos de datos de alias nativos y está pensado para reemplazar **sp_addtype** como un medio para crear tipos de datos de alias. Algunos de los argumentos opcionales de la sintaxis de CREATE TYPE hacen referencia a la creación de UDTs y no sirven para crear tipos de datos de alias (como el tipo base).  
  
 Para obtener más información, vea [Create TYPE &#40;Transact-SQL&#41;](../../t-sql/statements/create-type-transact-sql.md).  
  
#### <a name="example"></a>Ejemplo  
 La [!INCLUDE[tsql](../../includes/tsql-md.md)] instrucción siguiente crea el tipo de **punto** . El nombre externo se especifica mediante la sintaxis de nomenclatura de dos partes de *AssemblyName*. *Nombreudt*.  
  
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
 La siguiente consulta [!INCLUDE[tsql](../../includes/tsql-md.md)] debe ejecutarse en el orden que se indica. En primer lugar, se debe quitar la tabla que hace referencia al UDT **Point** , el tipo y, por último, el ensamblado.  
  
```  
DROP TABLE dbo.Points;  
DROP TYPE dbo.Point;  
DROP ASSEMBLY Point;  
```  
  
### <a name="finding-udt-dependencies"></a>Buscar dependencias UDT  
 Si hay objetos dependientes, como tablas con definiciones de columna UDT, se produce un error en la instrucción DROP TYPE. También produce un error si hay funciones, procedimientos almacenados o desencadenadores creados en la base de datos con la cláusula WITH SCHEMABINDING, cuando estas rutinas utilizan variables o parámetros del tipo definido por el usuario. Debe quitar primero todos los objetos dependientes y, a continuación, ejecutar la instrucción DROP TYPE.  
  
 La siguiente [!INCLUDE[tsql](../../includes/tsql-md.md)] consulta busca todas las columnas y parámetros que usan un UDT en la base de datos **AdventureWorks** .  
  
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
 La instrucción ALTER ASSEMBLY se usa después de haber realizado cambios en el código fuente del ensamblado UDT y después de haberlo compilado de nuevo. Esta instrucción copia el archivo .dll en el servidor y lo enlaza al nuevo ensamblado. Para obtener la sintaxis completa, vea [ALTER assembly &#40;Transact-SQL&#41;](../../t-sql/statements/alter-assembly-transact-sql.md).  
  
 La siguiente instrucción ALTER ASSEMBLY de [!INCLUDE[tsql](../../includes/tsql-md.md)] vuelve a cargar el ensamblado Point.dll desde la ubicación del disco especificada.  
  
```  
ALTER ASSEMBLY Point  
FROM '\\Projects\Point\bin\Point.dll'  
```  
  
### <a name="using-alter-assembly-to-add-source-code"></a>Usar ALTER ASSEMBLY para agregar código fuente  
 La cláusula ADD FILE de la sintaxis ALTER ASSEMBLY no está presente en CREATE ASSEMBLY. Puede usarla para agregar código fuente o cualquier otro archivo asociado a un ensamblado. Los archivos se copian desde sus ubicaciones originales y se almacenan en tablas del sistema en la base de datos. De esta forma, se garantiza que el código fuente u otros archivos estén disponibles siempre que sea necesario volver a crear o documentar la versión actual del UDT.  
  
 La siguiente [!INCLUDE[tsql](../../includes/tsql-md.md)] instrucción ALTER ASSEMBLY agrega el código fuente de la clase Point.CS para el UDT **Point** . De esta forma, el texto incluido en el archivo Point.cs se copia y se almacena en la base de datos con el nombre "PointSource".  
  
```  
ALTER ASSEMBLY Point  
ADD FILE FROM '\\Projects\Point\Point.cs' AS PointSource;  
```  
  
 La información de ensamblado se almacena en la tabla **Sys. assembly_files** en la base de datos donde se ha instalado el ensamblado. La tabla **Sys. assembly_files** contiene las columnas siguientes.  
  
 **assembly_id**  
 Identificador definido para el ensamblado. Este número se asigna a todos los objetos relacionados con el mismo ensamblado.  
  
 **name**  
 Nombre del objeto.  
  
 **file_id**  
 Número que identifica cada objeto, con el primer objeto asociado a una **assembly_id** determinada a la que se proporciona el valor 1. Si hay varios objetos asociados al mismo **assembly_id**, cada valor de **file_id** subsiguiente se incrementa en 1.  
  
 **content**  
 Representación hexadecimal del ensamblado o archivo.  
  
 Puede utilizar la función CAST o CONVERT para convertir el contenido de la columna **Content** en texto legible. La consulta siguiente convierte el contenido del archivo Point.cs en texto legible, utilizando el nombre de la cláusula WHERE para restringir el conjunto de resultados a una única fila.  
  
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
 El UDT **Currency** de la base de datos de ejemplo **AdventureWorks** proporciona un ejemplo útil de la manera recomendada de estructurar un UDT y sus funciones asociadas. El UDT **Currency** se utiliza para controlar el dinero según el sistema monetario de una referencia cultural determinada y permite el almacenamiento de distintos tipos de moneda, como dólares, euros, etc. La clase UDT expone un nombre de referencia cultural como una cadena y una cantidad de dinero como un tipo de datos **decimal** . Todos los métodos de serialización necesarios están incluidos en el ensamblado que define la clase. La función que implementa la conversión de moneda de una referencia cultural a otra se implementa como una función externa denominada **ConvertCurrency**y esta función se encuentra en un ensamblado independiente. La función **ConvertCurrency** realiza su trabajo mediante la recuperación de la tasa de conversión de una tabla en la base de datos **AdventureWorks** . Si el origen de las tasas de conversión debe cambiar alguna vez, o si debe haber otros cambios en el código existente, el ensamblado se puede modificar fácilmente sin que afecte al UDT de **moneda** .  
  
 La lista de código de las funciones UDT de **moneda** y **ConvertCurrency** se puede encontrar instalando los ejemplos de Common Language Runtime (CLR).  
  
### <a name="using-udts-across-databases"></a>Usar tipos UDT en varias bases de datos  
 El ámbito de los UDT es, por definición, una sola base de datos. Por lo tanto, un UDT definido en una base de datos no puede usarse en una definición de columna de otra base de datos. Para usar los UDT en varias bases de datos, debe ejecutar las instrucciones CREATE ASSEMBLY y CREATE TYPE en cada base de datos en ensamblados idénticos. Los ensamblados se consideran idénticos si tienen el mismo nombre, nombre seguro, referencia cultural, versión, conjunto de permisos y contenido binario.  
  
 Cuando el UDT se haya registrado y esté accesible en ambas bases de datos, podrá convertir un valor UDT de una base de datos para utilizarlo en la otra. Pueden usarse UDT idénticos en varias bases de datos en los escenarios siguientes:  
  
-   Al llamar a un procedimiento almacenado definido en bases de datos diferentes.  
  
-   Al consultar tablas definidas en bases de datos diferentes.  
  
-   Al seleccionar datos UDT de una columna UDT de una tabla de base de datos e insertarlos en una segunda base de datos con una columna UDT idéntica.  
  
 En estas situaciones, todas las conversiones que requiere el servidor se realizan automáticamente. No puede realizar las conversiones de forma explícita utilizando las funciones CAST o CONVERT de [!INCLUDE[tsql](../../includes/tsql-md.md)].  
  
 Tenga en cuenta que no es necesario realizar ninguna acción para usar UDT cuando [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] crea tablas de trabajo en la base de datos del sistema **tempdb** . Esto incluye el control de cursores, variables de tabla y funciones con valores de tabla definidas por el usuario que incluyen UDT y que usan de forma transparente **tempdb**. Sin embargo, si crea explícitamente una tabla temporal en **tempdb** que define una columna UDT, el UDT debe registrarse en **tempdb** del mismo modo que para una base de datos de usuario.  
  
## <a name="see-also"></a>Consulte también  
 [Tipos CLR definidos por el usuario](../../relational-databases/clr-integration-database-objects-user-defined-types/clr-user-defined-types.md)  
  
  
