---
description: Cuadro de diálogo Edición avanzada (condición)
title: Cuadro de diálogo Edición avanzada (condición) | Microsoft Docs
ms.custom: ''
ms.date: 08/12/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: security
ms.topic: conceptual
f1_keywords:
- sql13.swb.dmf.condition.advancededit.f1
ms.assetid: a0bbe501-78c5-45ad-9087-965d04855663
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: f22553f6fe5685600727ec5d382664e0f7878fac
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/17/2020
ms.locfileid: "88470368"
---
# <a name="advanced-edit-condition-dialog-box"></a>Cuadro de diálogo Edición avanzada (condición)
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
   Use el cuadro de diálogo **Edición avanzada** para crear expresiones complejas para las condiciones de administración basada en directivas.  
  
## <a name="options"></a>Opciones  
 **Valor de celda**  
 Muestra la función o expresión que se utilizará para el valor de celda al crearlo. Al hacer clic en **Aceptar**, el valor de celda aparecerá en la celda **Campo** o **Valor** en el cuadro de expresión de condición del cuadro de diálogo **Crear nueva condición** o **Abrir condición** en la página **General** .  
  
 **Funciones y propiedades**  
 Muestra las funciones y propiedades disponibles.  
  
 **Detalles**  
 Muestra la información sobre las funciones y propiedades, con el formato: firma de la función, descripción de la función, valor devuelto y ejemplo.  
  
## <a name="syntax"></a>Sintaxis  
 Las expresiones válidas deben estar en el formato siguiente:  
  
 `{property | function | constant}`  
  
 `{operator}`  
  
 `{property | function | constant}`  
  
## <a name="examples"></a>Ejemplos  
 A continuación se muestran algunos ejemplos de expresiones válidas:  
  
-   *Property1*> 5  
  
-   *Property1*=*Property2*  
  
-   Add(5, Multiply(.2,*Property1*))<*Property2*  
  
-   *Sometext* EN *Property1*  
  
-   *Property1*< Fn(*Property2*)  
  
-   BitwiseAnd(*Property1*,*Property2*)= 0  
  
## <a name="additional-function-information"></a>Información adicional de funciones  
 En las secciones siguientes se proporciona información adicional sobre las funciones que puede utilizar con el fin de crear expresiones complejas para las condiciones de administración basada en directivas.  
  
> **IMPORTANTE:** Las funciones que puede utilizar para crear condiciones de administración basada en directivas no siempre utilizan la sintaxis [!INCLUDE[tsql](../../includes/tsql-md.md)] . Asegúrese de seguir la sintaxis del ejemplo. Por ejemplo, al utilizar las funciones **DateAdd** o **DatePart** , debe incluir el argumento *datepart* entre comillas simples.  
  
|Función|Firma|Descripción|Argumentos|Valor devuelto|Ejemplo|  
|--------------|---------------|-----------------|---------------|------------------|-------------|  
|**Add()**|Numeric Add (Numeric *expression1*, Numeric *expression2*)|Suma dos números.|*expression1* y *expression2* : es cualquier expresión válida de cualquiera de los tipos de datos de la categoría numeric, excepto el tipo de datos **bit** . Puede ser una constante, propiedad o función que devuelva un tipo numérico.|Devuelve el tipo de datos del argumento que tenga mayor prioridad.|`Add(Property1, 5)`|  
|**Array()**|Array Array (VarArgs *expression*)|Crea una matriz a partir de una lista de valores. Se puede utilizar con funciones de agregado como Sum() y Count().|*expression* : es una expresión que se convertirá en una matriz.|La matriz|`Array(2,3,4,5,6)`|  
|**Avg()**|Numeric Avg (*VarArgs*)|devuelve el promedio de valores de la lista de argumentos.|*VarArgs* : es una lista de expresiones Variant de la categoría de tipo de datos numérico exacto o numérico aproximado, excepto el tipo de datos **bit** .|El tipo de valor devuelto viene determinado por el tipo del resultado evaluado de la expresión.<br /><br /> Si el resultado de la expresión es de la categoría **integer**, **decimal**, **money** o **smallmoney**, o de la categoría **float** o **real** , los tipos devueltos son **int**, **decimal**, **money**y **float**; respectivamente.|`Avg(1.0, 2.0, 3.0, 4.0, 5.0)` devuelve `3.0` en este ejemplo.|  
|**BitwiseAnd()**|Numeric BitwiseAnd (Numeric *expression 1*, Numeric *expression2*)|Realiza una operación lógica AND bit a bit entre dos valores enteros.|*expression1* y *expression2* : es cualquier expresión válida de cualquiera de los tipos de datos de la categoría de tipo de datos entero.|Devuelve un valor de categoría con el tipo de datos integer.|`BitwiseAnd(Property1, Property2)`|  
|**BitwiseOr()**|Numeric BitwiseOr (Numeric *expression1*, Numeric *expression2*)|Realiza una operación lógica OR bit a bit entre dos valores enteros especificados.|*expression1* y *expression2* : es cualquier expresión válida de cualquiera de los tipos de datos de la categoría de tipo de datos entero.|Devuelve un valor de categoría con el tipo de datos integer.|`BitwiseOr(Property1, Property2)`|  
|**Concatenate()**|String Concatenate (String *string1*, String *string2*)|Concatena dos cadenas.|*string1* y *string2* : son las dos cadenas que se quiere concatenar. Puede ser cualquier cadena válida que no sea NULL.|La cadena concatenada, con *string1* seguida de *string2*.|`Concatenate("Hello", " World` `")` devuelve "`Hello World`".|  
|**Count()**|Numeric Count (*VarArgs*)|Devuelve el número de elementos en la lista de argumentos.|*VarArgs* : es una expresión de cualquier tipo excepto **text**, **image**y **ntext**.|Devuelve un valor de categoría con el tipo de datos integer.|`Count(1.0, 2.0, 3.0, 4.0, 5.0)` devuelve `5` en este ejemplo.|  
|**AgregarFecha()**|DateTime DateAdd (String *datepart*, Numeric *number*, DateTime *date*)|Devuelve un valor **datetime** nuevo que se basa en sumar un intervalo a la fecha especificada.|*datepart* : es el parámetro que especifica en qué parte de la fecha se devuelve un valor nuevo. Algunos de los tipos admitidos son year(yy, yyyy), month(mm, m) y dayofyear(dy, y). Para obtener más información, vea [DATEADD &#40;Transact-SQL&#41;](../../t-sql/functions/dateadd-transact-sql.md).<br /><br /> *number*: es el valor que se usa para incrementar *datepart*.<br /><br /> *date* es una expresión que devuelve un valor **datetime** o una cadena de caracteres en formato de fecha.|Es el valor **datetime** nuevo que se basa en sumar un intervalo a la fecha especificada.|**Ejemplo:** `DateAdd('day', 21, DateTime('2007-08-06 14:21:50'))` devuelve `'2007-08-27 14:21:50'` en este ejemplo.<br /><br /> Los siguientes son *dateparts* y abreviaturas que admite esta función:<br /><br /> **year**: yy, yyyy<br /><br /> **month**: mm, m<br /><br /> **dayofyear**: dy, y<br /><br /> **day**: dd, d<br /><br /> **week**: wk, ww<br /><br /> **weekday**: dw, w<br /><br /> **hour**: hh<br /><br /> **minute**: mi, n<br /><br /> **second**: ss, s<br /><br /> **millisecond**: ms|  
|**DatePart()**|Numeric DatePart (String *datepart*, DateTime *date*)|Devuelve un entero que representa el *datepart* especificado de la fecha especificada.|*datepart* : es el parámetro que especifica la parte de la fecha que se devolverá. Algunos de los tipos admitidos son year(yy, yyyy), month(mm, m) y dayofyear(dy, y). Para obtener más información, vea [DATEPART &#40;Transact-SQL&#41;](../../t-sql/functions/datepart-transact-sql.md).<br /><br /> *date* es una expresión que devuelve un valor **datetime** o una cadena de caracteres en formato de fecha.|Devuelve el valor de una categoría de tipo de datos entero que representa el parámetro *datepart* especificado de la fecha indicada.|`DatePart('month', DateTime('2007-08-06 14:21:50.620'))` devuelve `8` en este ejemplo.|  
|**DateTime()**|DateTime DateTime (String *dateString*)|Crea un valor datetime a partir de una cadena.|*dateString* : es el valor datetime como una cadena.|Devuelve un valor datetime creado a partir de la cadena de entrada.|`DateTime('3/12/2006')`|  
|**Dividir()**|Numeric Divide (Numeric *expression_dividend*, Numeric *expression_divisor*)|Divide un número por otro.|*expression_dividend* : es la expresión numérica entre la que se va a dividir. El dividendo puede ser cualquier expresión válida de cualquiera de los tipos de datos de la categoría de tipos de datos numéricos, excepto el tipo de datos **datetime** .<br /><br /> *expression_divisor* : es la expresión numérica entre la que se divide el dividendo. El divisor puede ser cualquier expresión válida de cualquiera de los tipos de datos de la categoría de tipos de datos numéricos, excepto el tipo de datos **datetime** .|Devuelve el tipo de datos del argumento que tenga mayor prioridad.|**Ejemplo:** `Divide(Property1, 2)`<br /><br /> Nota: será una operación de valores double. Para hacer una comparación de valores enteros, debe combinar los resultados con `Round()`. Por ejemplo: `Round(Divide(10, 3), 0) = 3`.|  
|**Enum()**|Numeric Enum (String *enumTypeName*, String *enumValueName*)|Crea un valor enum a partir de una cadena.|*enumTypeName* : es el nombre del tipo enum.<br /><br /> *enumValueName* : es el valor de la enumeración.|Devuelve el valor enum como un valor numérico.|`Enum('CompatibilityLevel','Version100')`|  
|**Escape()**|String Escape (String *replaceString*, String *stringToEscape*, String *escapeString*)|Antepone a una subcadena de la cadena de entrada una cadena de escape determinada.|*replaceString*: es la cadena de entrada.<br /><br /> *stringToEscape*: es una subcadena de *replaceString*. Se trata de la cadena a la que desea anteponer una cadena de escape.<br /><br /> *escapeString*: es la cadena de escape que quiere agregar delante de cada instancia de *stringToEscape*.|Devuelve una *replaceString* modificada en la que cada instancia de *stringToEscape* es precedida por *escapeString*.|`Escape("Hello", "l", "[")` devuelve "`He[l[lo`".|  
|**ExecuteSQL()**|Variant ExecuteSQL (String *returnType*, String *sqlQuery*)|Ejecuta la consulta de [!INCLUDE[tsql](../../includes/tsql-md.md)] con el servidor de destino.<br /><br /> Para obtener más información sobre ExecuteSql(), vea el tema sobre la [función ExecuteSql()](https://blogs.msdn.com/b/sqlpbm/archive/2008/07/03/executesql.aspx).|*returnType* : especifica el tipo de los datos devueltos por la instrucción de [!INCLUDE[tsql](../../includes/tsql-md.md)] . Los literales válidos para *returnType* son los siguientes: **Numeric**, **String**, **Bool**, **DateTime**, **Array**y **Guid**.<br /><br /> *sqlQuery* : es la cadena que contiene la consulta que se va a ejecutar.||`ExecuteSQL ('Numeric', 'SELECT COUNT(*) FROM msdb.dbo.sysjobs') <> 0`<br /><br /> Ejecuta una consulta de Transact-SQL con valores escalares en una instancia de destino de SQL Server. Solo se puede especificar una columna en una instrucción `SELECT` ; se omiten las columnas posteriores a la primera. La consulta resultante debe devolver solo una fila; se omiten las filas posteriores a la primera. Si la consulta devuelve un conjunto vacío, la expresión de condición creada en torno a `ExecuteSQL` se evaluará como FALSE. `ExecuteSql` admite los modos de evaluación **A petición** y **Al programar** .<br /><br /> -`@@ObjectName`:<br />                      Se corresponde con el campo de nombre en [sys.objects](../../relational-databases/system-catalog-views/sys-objects-transact-sql.md). La variable será reemplazada por el nombre del objeto actual.<br /><br /> -`@@SchemaName`: corresponde al campo de nombre en [sys.schemas](../../relational-databases/system-catalog-views/schemas-catalog-views-sys-schemas.md). La variable será reemplazada por el nombre del esquema para el objeto actual, si es aplicable.<br /><br /> Nota: para incluir una comilla simple en una instrucción ExecuteSQL, defina la comilla simple como carácter de escape mediante dos comillas simples. Por ejemplo, para incluir una referencia a un usuario cuyo nombre es O'Brian, escriba O"Brian.|  
|**ExecuteWQL()**|Variant ExecuteWQL (string *returnType* , string *namespace*, string *wql*)|Ejecuta el script WQL con el espacio de nombres que se proporciona. La instrucción Select puede contener solo una única columna de retorno. Si se proporciona más de una columna, se producirá un error.|*returnType* : especifica el tipo de datos devuelto por WQL. Los literales válidos son **Numeric**, **String**, **Bool**, **DateTime**, **Array**y **Guid**.<br /><br /> *namespace* : es el espacio de nombres de WMI con el que se realiza la ejecución.<br /><br /> *wql* : es la cadena que contiene el lenguaje WQL que se va a ejecutar.||`ExecuteWQL('Numeric', 'root\CIMV2', 'select NumberOfProcessors from win32_ComputerSystem') <> 0`|  
|**False()**|Bool False()|Devuelve el valor booleano FALSE.|None|Devuelve el valor booleano FALSE.|`IsDatabaseMailEnabled = False()`|  
|**GetDate()**|DateTime GetDate()|Devuelve la fecha del sistema.|None|Devuelve la fecha del sistema como DateTime.|`@DateLastModified = GetDate()`|  
|**Guid()**|Guid Guid(String *guidString*)|Devuelve un GUID a partir de una cadena.|*guidString* : es la representación de cadena del GUID que se va a crear.|Devuelve el GUID creado a partir de la cadena.|`Guid('12340000-0000-3455-0000-000000000454')`|  
|**IsNull()**|Variant IsNull (Variant *check_expression*, Variant *replacement_value*)|Se devuelve el valor de *check_expression* si no es NULL; en caso contrario, se devuelve *replacement_value* . Si los tipos son diferentes, *replacement_value* se convierte implícitamente en el tipo de *check_expression*.|*check_expression* : es la expresión que se va a comprobar si es NULL. *check_expression* : puede ser de cualquier tipo compatible de administración basada en directivas: Numeric, String, Bool, DateTime, Array y Guid.<br /><br /> *replacement_value* : es la expresión que se devuelve si *check_expression* es NULL. *replacement_value* debe ser de un tipo que se convierta implícitamente en el tipo de *check_expression*.|Se devuelve el tipo de *check_expression* si *check_expression* no es NULL; de lo contrario, se devuelve el tipo de *replacement_value* .||  
|**Len()**|Numeric Len (*string_expression*)|Devuelve el número de caracteres de la expresión de cadena dada, excluyendo los espacios en blanco del final.|*string_expression* : es la expresión de cadena que se va a evaluar.|Devuelve un valor de categoría con el tipo de datos integer.|`Len('Hello')` devuelve `5` en este ejemplo.|  
|**Lower()**|String Lower (String *_expression*)|Devuelve la cadena después de convertir todos los caracteres en mayúscula a minúscula.|*expression* : es la expresión de la cadena de origen.|Devuelve una cadena que representa la expresión de cadena de origen después de haber convertido todos los caracteres en mayúscula a minúscula.|`Len('HeLlO')` devuelve `'hello'` en este ejemplo.|  
|**Mod()**|Numeric Mod (Numeric *expression_dividend*, Numeric *expression_divisor*)|Proporciona el resto entero después de dividir la primera expresión numérica por la segunda expresión numérica.|*expression_dividend* : es la expresión numérica entre la que se va a dividir. *expression_dividend* debe ser una expresión válida de cualquiera de los tipos de datos de las categorías de tipos de datos enteros y numéricos.<br /><br /> *expression_divisor* : es la expresión numérica entre la que se divide el dividendo. *expression_divisor* debe ser una expresión válida de cualquiera de los tipos de datos de las categorías de tipos de datos enteros y numéricos.|Devuelve un valor de categoría con el tipo de datos integer.|`Mod(Property1, 3)`|  
|**Multiplicar()**|Numeric Multiply (Numeric *expression1*, Numeric *expression2*)|Multiplica dos expresiones.|*expression1* y *expression2* : es cualquier expresión válida de cualquiera de los tipos de datos de la categoría numeric, excepto el tipo de datos **datetime** .|Devuelve el tipo de datos del argumento que tenga mayor prioridad.|`Multiply(Property1, .20)`|  
|**Potencia()**|Numeric Power (Numeric *numeric_expression*, Numeric *expression_power*)|Devuelve el valor de la expresión especificada a la potencia especificada.|*numeric_expression* : es una expresión de la categoría de tipos de datos numérico exacto o numérico aproximado, excepto para el tipo de datos bit.<br /><br /> *expression_power* : es la potencia a la que se eleva *numeric_expression*. *expression_power* puede ser una expresión de la categoría de tipos de datos numérico exacto o numérico aproximado, excepto para el tipo de datos **bit** .|El tipo devuelto es el mismo de *numeric_expression*.|`Power(Property1, 3)`|  
|**Redondear()**|Numeric Round (Numeric *expression*, Numeric *expression_precision*)|Devuelve una expresión numérica, redondeada a la longitud o precisión especificada.|*expression* : es una expresión de la categoría de tipos de datos numérico exacto o numérico aproximado, excepto para el tipo de datos **bit** .<br /><br /> *expression_precision* : es la precisión con la que se redondea la expresión. Si *expression_precision* es un número positivo, *numeric_expression* se redondea al número de posiciones decimales especificado por la longitud. Si *expression_precision* es un número negativo, *numeric_expression* se redondea a la izquierda del separador decimal, según lo especificado por *expression_precision*.|Devuelve el mismo tipo que *numeric_expression*.|`Round(5.333, 0)`|  
|**String()**|String String (Variant *_expression*)|Convierte una variante en una cadena.|*expression* : es la expresión variant que se va a convertir en una cadena.|Devuelve el valor de cadena de la expresión variant.|`String(4)`|  
|**Sum()**|Numeric Sum (*VarArgs*)|Devuelve la suma de todos los valores de una lista de argumentos. La suma se puede utilizar con valores numéricos.|*VarArgs*: es una lista de expresiones Variant de la categoría de tipo de datos numérico exacto o numérico aproximado, excepto el tipo de datos **bit** .|Devuelve la suma de todos los valores de expresión en el tipo de datos de expresión más preciso.<br /><br /> Si el resultado de la expresión es de la categoría **integer**, **numeric**, **money** o **small money**, o de la categoría **float** o **real** , los tipos devueltos son **int**, **numeric**, **money**y **float**; respectivamente.|`Sum(1.0, 2.0, 3.0, 4.0, 5.0)` devuelve `15` en este ejemplo.|  
|**True()**|Bool TRUE()|Devuelve el valor booleano TRUE.||Devuelve el valor booleano TRUE.|`IsDatabaseMailEnabled = True()`|  
|**Upper()**|String Upper (String *_expression*)|Devuelve la cadena después de convertir todos los caracteres en minúscula a mayúscula.|*expression* : es la expresión de la cadena de origen.|Devuelve una cadena que representa la expresión de cadena de origen después de convertir todos los caracteres en minúscula a mayúscula.|`Upper('HeLlO')` devuelve `'HELLO'` en este ejemplo.|  
  
## <a name="see-also"></a>Consulte también  
 [Cuadro de diálogo Crear nueva condición o Abrir condición, página General](../../relational-databases/policy-based-management/create-new-condition-or-open-condition-dialog-box-general-page.md)   
 [Administrar servidores mediante administración basada en directivas](../../relational-databases/policy-based-management/administer-servers-by-using-policy-based-management.md)  
  
  
