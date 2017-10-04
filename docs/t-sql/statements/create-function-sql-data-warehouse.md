---
title: "CREATE (función) (almacenamiento de datos SQL) | Documentos de Microsoft"
ms.custom: 
ms.date: 08/10/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: 8cad1b2c-5ea0-4001-9060-2f6832ccd057
caps.latest.revision: 14
author: barbkess
ms.author: barbkess
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 55f1b7e612a1c7d120e06078b0fdba45d6409d36
ms.contentlocale: es-es
ms.lasthandoff: 09/01/2017

---
# <a name="create-function-sql-data-warehouse"></a>CREATE (función) (almacenamiento de datos SQL)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-pdw_md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md.md)]

  Crea una función definida por el usuario en [!INCLUDE[ssSDW](../../includes/sssdw-md.md)]. Una función definida por el usuario es un [!INCLUDE[tsql](../../includes/tsql-md.md)] rutina que acepta parámetros, realiza una acción, como un cálculo complejo y devuelve el resultado de esa acción como un valor. El valor devuelto debe ser un valor escalar (único). Utilice esta instrucción para crear una rutina reutilizable que se pueda utilizar de estas formas:  
  
-   En instrucciones [!INCLUDE[tsql](../../includes/tsql-md.md)] como SELECT  
  
-   En las aplicaciones que llaman a la función  
  
-   En la definición de otra función definida por el usuario  
  
-   Para definir una restricción CHECK en una columna  
  
-   Para reemplazar un procedimiento almacenado  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
--Transact-SQL Scalar Function Syntax  
CREATE FUNCTION [ schema_name. ] function_name   
( [ { @parameter_name [ AS ] parameter_data_type   
    [ = default ] }   
    [ ,...n ]  
  ]  
)  
RETURNS return_data_type  
    [ WITH <function_option> [ ,...n ] ]  
    [ AS ]  
    BEGIN   
        function_body   
        RETURN scalar_expression  
    END  
[ ; ]  
  
<function_option>::=   
{  
    [ SCHEMABINDING ]  
  | [ RETURNS NULL ON NULL INPUT | CALLED ON NULL INPUT ]  
}  
  
```  
  
## <a name="arguments"></a>Argumentos  
 *schema_name*  
 Nombre del esquema al que pertenece la función definida por el usuario.  
  
 *nombre_función*  
 Nombre de la función definida por el usuario. Nombres de función deben cumplir las reglas para identificadores y deben ser únicos dentro de la base de datos y a su esquema.  
  
> [!NOTE]  
>  Los paréntesis después del nombre de la función son necesarios, aunque no se especifique un parámetro.  
  
 @*parameter_name*  
 Es un parámetro de la función definida por el usuario. Es posible declarar uno o varios parámetros.  
  
 Una función puede tener un máximo de 2.100 parámetros. El usuario debe proporcionar el valor de cada parámetro declarado cuando se ejecuta la función, a menos que se defina un valor predeterminado para el parámetro.  
  
 Especifique un nombre de parámetro con una arroba (@) como primer carácter. El nombre del parámetro debe cumplir las mismas reglas que los identificadores. Los parámetros son locales para la función; los mismos nombres de parámetro se pueden utilizar en otras funciones. Los parámetros solamente pueden ocupar el lugar de constantes; no se pueden utilizar en lugar de nombres de tablas, nombres de columnas o nombres de otros objetos de base de datos.  
  
> [!NOTE]  
>  ANSI_WARNINGS no se respeta al pasar parámetros en un procedimiento almacenado o una función definida por el usuario, ni cuando se declaran y se establecen variables en una instrucción por lotes. Por ejemplo, si una variable se define como **char (3)**y, a continuación, establece en un valor mayor que tres caracteres, se truncan los datos para el tamaño definido y la INSERCIÓN o instrucción de actualización se realiza correctamente.  
  
 *parameter_data_type*  
 Es el tipo de datos de parámetro. Para [!INCLUDE[tsql](../../includes/tsql-md.md)] funciones, todos los tipos de datos escalares admitidos en [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] se permiten. El tipo de datos de marca de tiempo (rowversion) no es un tipo admitido.  
  
 [=*predeterminado* ]  
 Es un valor predeterminado para el parámetro. Si un *predeterminado* se define un valor, la función se puede ejecutar sin especificar un valor para ese parámetro.  
  
 Cuando un parámetro de la función tiene un valor predeterminado, se debe especificar la palabra clave DEFAULT al llamar a la función para recuperar el valor predeterminado. Este comportamiento es distinto del uso de parámetros con valores predeterminados en los procedimientos almacenados, donde la omisión del parámetro implica especificar el valor predeterminado.  
  
 *return_data_type*  
 Es el valor devuelto de una función escalar definida por el usuario. Para [!INCLUDE[tsql](../../includes/tsql-md.md)] funciones, todos los tipos de datos escalares admitidos en [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] se permiten. El tipo de datos de marca de tiempo (rowversion) no es un tipo admitido. No se permiten los tipos de datos no escalares de cursor y la tabla.  
  
 *function_body*  
 Serie de [!INCLUDE[tsql](../../includes/tsql-md.md)] instrucciones.  El function_body no puede contener una instrucción SELECT y no se puede hacer referencia a la base de datos.  El function_body no se puede hacer referencia a tablas o vistas. El cuerpo de la función puede llamar a otras funciones deterministas, pero no puede llamar a funciones no deterministas. 
  
 En las funciones escalares, *cuerpo_función* es una serie de [!INCLUDE[tsql](../../includes/tsql-md.md)] instrucciones que juntas se evalúan como un valor escalar.  
  
 *scalar_expression*  
 Especifica el valor escalar que devuelve la función escalar.  
  
 **\<function_option >:: =** 
  
 Especifica que la función tendrá una o más de las siguientes opciones.  
  
 SCHEMABINDING  
 Especifica que la función está enlazada a los objetos de base de datos a los que hace referencia. Cuando se especifica SCHEMABINDING, los objetos base no se pueden modificar de una forma que afecte a la definición de la función. En primer lugar, se debe modificar o quitar la propia definición de la función para quitar las dependencias en el objeto que se va a modificar.  
  
 El enlace de la función a los objetos a los que hace referencia solamente se quita cuando se ejecuta una de estas acciones:  
  
-   Se quita la función.  
  
-   La función se modifica con la instrucción ALTER sin especificar la opción SCHEMABINDING.  
  
 Una función se puede enlazar a esquema solamente si se cumplen las siguientes condiciones:  
  
-   Las funciones definidas por el usuario al que hace referencia la función también están enlazadas a los esquemas.  
  
-   Las funciones y otro UDF al que hace referencia la función se hace referencia mediante un nombre de uno o dos partes.  
  
-   Solo las funciones integradas y otra UDF en la misma base de datos puede hacer referencia en el cuerpo del UDF.  
  
-   El usuario que ejecutó la instrucción CREATE FUNCTION tiene permisos REFERENCES para los objetos de base de datos a los que hace referencia la función.  
  
 Para quitar SCHEMABINDING use ALTER  
  
 DEVUELVE NULL EN LA ENTRADA NULL | **LLAMA EN LA ENTRADA NULL**  
 Especifica la **OnNULLCall** atributo de una función con valores escalares. Si no se especifica, se utiliza CALLED ON NULL INPUT de manera predeterminada. Esto significa que el cuerpo de la función se ejecuta aunque se envíe NULL como argumento.  
  
## <a name="best-practices"></a>Procedimientos recomendados  
 Si una función definida por el usuario no se crea con la cláusula SCHEMABINDING, los cambios que se realicen en los objetos subyacentes pueden afectar a la definición de la función y generar resultados inesperados al invocarla. Recomendamos implementar uno de los siguientes métodos para garantizar que la función no queda sin actualizar como consecuencia de los cambios realizados en sus objetos subyacentes:  
  
-   Especifique la cláusula WITH SCHEMABINDING al crear la función. Así se asegura de que no se pueden modificar los objetos a los que se hace referencia en la definición de la función a menos que también se modifique la función.  
  
## <a name="interoperability"></a>Interoperabilidad  
 Las siguientes instrucciones son válidas en una función:  
  
-   Instrucciones de asignación.  
  
-   Instrucciones de control de flujo, excepto las instrucciones TRY...CATCH.  
  
-   Instrucciones DECLARE que definen variables de datos locales.  
  
## <a name="limitations-and-restrictions"></a>Limitaciones y restricciones  
 Las funciones definidas por el usuario no se pueden utilizar para realizar acciones que modifican el estado de la base de datos.  
  
 Las funciones definidas por el usuario se pueden anidar; es decir, una función definida por el usuario puede llamar a otra. El nivel de anidamiento aumenta cuando se empieza a ejecutar la función llamada y disminuye cuando se termina de ejecutar la función llamada. Las funciones definidas por el usuario se pueden anidar hasta un máximo de 32 niveles. Si se superan los niveles máximos de anidamiento, la cadena completa de funciones de llamada produce un error.   
  
## <a name="metadata"></a>Metadatos  
 Esta sección enumeran las vistas de catálogo del sistema que puede usar para devolver los metadatos acerca de las funciones definidas por el usuario.  
  
 [Sys.sql_modules](../../relational-databases/system-catalog-views/sys-sql-modules-transact-sql.md) : muestra la definición de [!INCLUDE[tsql](../../includes/tsql-md.md)] funciones definidas por el usuario. Por ejemplo:  
  
```  
SELECT definition, type   
FROM sys.sql_modules AS m  
JOIN sys.objects AS o   
    ON m.object_id = o.object_id   
    AND type = ('FN');  
GO  
  
```  
  
 [Sys.Parameters](../../relational-databases/system-catalog-views/sys-parameters-transact-sql.md) : muestra información acerca de los parámetros definidos en las funciones definidas por el usuario.  
  
 [Sys.sql_expression_dependencies](../../relational-databases/system-catalog-views/sys-sql-expression-dependencies-transact-sql.md) : muestra los objetos subyacentes que se hace referencia a una función.  
  
## <a name="permissions"></a>Permissions  
 Se requiere el permiso CREATE FUNCTION en la base de datos y el permiso ALTER en el esquema en el que se va a crear la función.  
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>Ejemplos: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] y[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
### <a name="a-using-a-scalar-valued-user-defined-function-to-change-a-data-type"></a>A. Usar una función escalar definida por el usuario para cambiar un tipo de datos  
 Esta función simple toma un **int** de tipo de datos como entrada y devuelve un **decimal (10,2)** tipo de datos como una salida.  
  
```  
CREATE FUNCTION dbo.ConvertInput (@MyValueIn int)  
RETURNS decimal(10,2)  
AS  
BEGIN  
    DECLARE @MyValueOut int;  
    SET @MyValueOut= CAST( @MyValueIn AS decimal(10,2));  
    RETURN(@MyValueOut);  
END;  
GO  
  
SELECT dbo.ConvertInput(15) AS 'ConvertedValue';  
```  
  
## <a name="see-also"></a>Vea también  
 [Modifique la función (SQL Server PDW)](http://msdn.microsoft.com/en-us/25ff3798-eb54-4516-9973-d8f707a13f6c)   
 [FUNCIÓN de destino (SQL Server PDW)](http://msdn.microsoft.com/en-us/1792a90d-0d06-4852-9dec-6de1b9cd229e)  
  
  



