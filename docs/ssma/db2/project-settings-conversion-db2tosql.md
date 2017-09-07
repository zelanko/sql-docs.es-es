---
title: "Configuración (conversión) (DB2ToSQL) del proyecto | Documentos de Microsoft"
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
ms.assetid: 538c93cf-c5bb-43d5-b758-186d9fb00c19
caps.latest.revision: 8
author: sabotta
ms.author: carlasab
manager: lonnyb
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 98ebb756d8d228de70c1c1969dba36ee89f8e076
ms.contentlocale: es-es
ms.lasthandoff: 08/02/2017

---
# <a name="project-settings-conversion-db2tosql"></a>Configuración del proyecto (conversión) (DB2ToSQL)
La página de conversión de la **configuración del proyecto** cuadro de diálogo contiene la configuración que permiten personalizar cómo SSMA convierte la sintaxis de DB2 a [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] sintaxis.  
  
El panel de conversión está disponible en la **configuración del proyecto** y **configuración de proyecto predeterminada** cuadros de diálogo:  
  
-   Para especificar la configuración para todos los proyectos SSMA, en la **herramientas** menú haga clic en **la configuración predeterminada del proyecto**, seleccione el tipo de proyecto de migración para el que se requiere para puede ver o cambiar de configuración **versión de destino de migración** de lista desplegable, haga clic en **General** en la parte inferior del panel izquierdo y, a continuación, haga clic en **conversión**.  
  
-   Para especificar la configuración para el proyecto actual, en la **herramientas** menú haga clic en **configuración del proyecto**, a continuación, haga clic en **General** en la parte inferior del panel izquierdo y, a continuación, haga clic en **conversión**.  
  
## <a name="conversion-messages"></a>Mensajes de conversión  
  
### <a name="generate-messages-about-issues-applied"></a>Generar mensajes acerca de los problemas que se aplica  
Especifica si SSMA genera mensajes informativos durante la conversión, mostrarlos en el panel de resultados y agrega al código convertido.  
  
Al seleccionar un modo de conversión en el **modo** cuadro, SSMA aplica la siguiente configuración:  
  
**Modo predeterminado/optimista:** n  
  
**Modo completo:** n  
  
## <a name="miscellaneous-options"></a>Otras opciones  
  
### <a name="cast-rownum-expressions-as-integers"></a>Expresiones de conversión ROWNUM como enteros  
Cuando SSMA convierte expresiones ROWNUM, convierte la expresión en una cláusula TOP, seguida por la expresión. En el ejemplo siguiente se muestra ROWNUM en una instrucción DELETE de DB2:  
  
`DELETE FROM Table1`  
  
`WHERE ROWNUM < expression and Field1 >= 2`  
  
En el ejemplo siguiente se muestra los resultantes [!INCLUDE[tsql](../../includes/tsql_md.md)]:  
  
`DELETE TOP (expression-1)`  
  
`FROM Table1`  
  
`WHERE Field1>=2`  
  
La parte superior, se requiere que la expresión de cláusulas principales se evalúa como un número entero. Si el entero es negativo, la instrucción producirá un error.  
  
-   Si selecciona **Sí**, SSMA convierte la expresión como un número entero.  
  
-   Si selecciona **n**, SSMA marcará todas las expresiones de tipo no entero como un error en el código convertido.  
  
Al seleccionar un modo de conversión en el **modo** cuadro, SSMA aplica la siguiente configuración:  
  
**El modo predeterminado/completo:** n  
  
**El modo optimista:** sí  
  
### <a name="default-schema-mapping"></a>Asignación del esquema predeterminado  
Esta configuración especifica cómo se asignan los esquemas de DB2 a esquemas de SQL Server. Dos opciones están disponibles en esta configuración:  
  
1.  **Esquema de la base de datos:** en este modo DB2 esquema 'sch1' se asignará al esquema de SQL Server 'dbo' en la base de datos de SQL Server 'sch1' de forma predeterminada.  
  
2.  **Esquema al esquema:**en este modo DB2 esquema 'sch1' se asignará al esquema de SQL Server 'sch1' en la base de datos de SQL Server predeterminado proporcionado en el cuadro de diálogo de conexión de forma predeterminada.  
  
Al seleccionar un modo de conversión en el **modo** cuadro, SSMA aplica la siguiente configuración:  
  
**El modo predeterminado/Optimistic/completo:** esquema de la base de datos  
  
### <a name="conversion-ways-of-merge-statement"></a>Formas de conversión de la instrucción MERGE  
  
-   Si selecciona **usando INSERT, UPDATE, instrucción DELETE**, SSMA convierte la instrucción de combinación en INSERT, UPDATE, elimine las instrucciones.  
  
-   Si selecciona **instrucción utilizando MERGE**, SSMA convierte la instrucción de combinación en la instrucción MERGE en [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)].  
  
> [!WARNING]  
> Esta opción de configuración de proyecto solo está disponible en [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 2008, [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 2012, [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 2014.  
  
Al seleccionar un modo de conversión en el **modo** cuadro, SSMA aplica la siguiente configuración:  
  
**El modo predeterminado/Optimistic/completo:** mediante combinación instrucción  
  
### <a name="convert-calls-to-subprograms-that-use-default-arguments"></a>Convertir las llamadas a subprogramas que utilizan argumentos predeterminados  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]funciones no son compatibles con la omisión de los parámetros en la llamada de función. Asimismo, [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] funciones y procedimientos no admiten expresiones como valores de parámetros predeterminados.  
  
-   Si selecciona **Sí** y una llamada de función omite parámetros, SSMA, inserta la palabra clave **predeterminado** en la función y llamada en la posición correcta. A continuación, marcará la llamada con una advertencia.  
  
-   Si selecciona **n**, SSMA marcará las llamadas a funciones como errores.  
  
Al seleccionar un modo de conversión en el **modo** cuadro, SSMA aplica la siguiente configuración:  
  
**El modo predeterminado/optimista/completo:** sí  
  
### <a name="convert-count-function-to-countbig"></a>Convertir COUNT_BIG COUNT (función)  
Si las funciones de recuento están probables que devuelven valores mayores que 2.147.483.647, que es 2<sup>31</sup>-1, debe convertir las funciones en COUNT_BIG.  
  
-   Si selecciona **Sí**, SSMA convertirá todos los usos de recuento en COUNT_BIG.  
  
-   Si selecciona **n**, las funciones permanecerá como recuento. [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]se devolverá un error si la función devuelve un valor mayor que 2<sup>31</sup>-1.  
  
Al seleccionar un modo de conversión en el **modo** cuadro, SSMA aplica la siguiente configuración:  
  
**El modo predeterminado/completo:** sí  
  
**El modo optimista:** n  
  
### <a name="convert-forall-statement-to-while-statement"></a>Convertir instrucción FORALL a mientras se encuentra instrucción  
Define cómo tratará SSMA FORALL bucles en elementos de la colección de PL/SQL.  
  
-   Si selecciona **Sí**, SSMA crea un bucle WHILE, donde los elementos de la colección son recuperado uno por uno.  
  
-   Si selecciona **n**, SSMA genera un conjunto de filas de la colección utilizando el método de nodos () y se utiliza como una sola tabla. Esto es más eficaz, pero hace que el código de salida sea menos legible.  
  
Al seleccionar un modo de conversión en el **modo** cuadro, SSMA aplica la siguiente configuración:  
  
**Modo predeterminado/optimista:** n  
  
**Modo completo:** sí  
  
### <a name="convert-foreign-keys-with-set-null-referential-action-on-column-that-is-not-null"></a>Claves externas de Convert con la acción referencial SET NULL en la columna que es no NULL  
DB2 permite crear restricciones de clave externa, donde una acción SET NULL no se pudo posiblemente realizar porque no se permite valores NULL en la columna que se hace referencia. [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]no se permite esta configuración de clave externa.  
  
-   Si selecciona **Sí**, SSMA generará las acciones referenciales en DB2, pero deberá hacer cambios manuales antes de cargar la restricción [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]. Por ejemplo, puede elegir NO ACTION en lugar de SET NULL.  
  
-   Si selecciona **n**, la restricción se marcará como un error.  
  
Al seleccionar un modo de conversión en el **modo** cuadro, SSMA aplica la siguiente configuración:  
  
**El modo predeterminado/optimista/completo:** n  
  
### <a name="convert-function-calls-to-procedure-calls"></a>Convertir las llamadas de función a las llamadas a procedimiento  
Algunas funciones de DB2 se definen como transacciones autónomas o contienen instrucciones que no son válidas en [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]. En estos casos, SSMA crea un procedimiento y una función que es un contenedor para el procedimiento. La función convertida llama al procedimiento de implementación.  
  
SSMA puede convertir las llamadas a la función contenedora en llamadas al procedimiento. Esto crea un código más legible y puede mejorar el rendimiento. Sin embargo, el contexto no permitir siempre Por ejemplo, no puede reemplazar una llamada de función en la lista de selección con una llamada a procedimiento. SSMA tiene algunas opciones para cubrir los casos comunes:  
  
-   Si selecciona **siempre**, SSMA intenta convertir las llamadas de función de contenedor en llamadas a procedimiento. Si el contexto actual no permite esta conversión, se genera un mensaje de error. De esta manera, no hay llamadas de función se mantienen en el código generado.  
  
-   Si selecciona **siempre que sea posible**, SSMA realiza un movimiento en las llamadas a procedimiento únicamente si la función tiene parámetros de salida. Cuando el movimiento no es posible, se quita el atributo de salida del parámetro. En todos los demás casos SSMA deja las llamadas a funciones.  
  
-   Si selecciona **nunca**, SSMA dejará todas las llamadas de función como llamadas de función. A veces, esta opción puede ser inaceptable por motivos de rendimiento.  
  
Al seleccionar un modo de conversión en el **modo** cuadro, SSMA aplica la siguiente configuración:  
  
**El modo predeterminado/Optimistic/completo:** siempre que sea posible  
  
### <a name="convert-lock-table-statements"></a>Convertir las instrucciones de la tabla de bloqueo  
SSMA puede convertir muchas instrucciones de la tabla de bloqueo en las sugerencias de tabla. SSMA no puede convertir cualquier instrucción de bloqueo tabla que contiene la partición, SUBPARTITION, @dblinky las cláusulas NOWAIT y se marcarán dichas instrucciones con mensajes de error de conversión.  
  
-   Si selecciona **Sí**, SSMA convertirá las instrucciones de bloqueo tabla compatibles en las sugerencias de tabla.  
  
-   Si selecciona **n**, SSMA marcará todas las instrucciones de la tabla de bloqueo con mensajes de error de conversión.  
  
En la tabla siguiente se muestra cómo SSMA convierte los modos de bloqueo de DB2:  
  
|||  
|-|-|  
|DB2 Modo de bloqueo|Sugerencia de tabla SQL Server|  
|RECURSO COMPARTIDO DE FILA|ROWLOCK, HOLDLOCK|  
|EXCLUSIVO DE FILA|HOLDLOCK ROWLOCK, XLOCK,|  
|ACTUALIZACIÓN DE RECURSO COMPARTIDO = EL RECURSO COMPARTIDO DE FILA|ROWLOCK, HOLDLOCK|  
|COMPARTIR|TABLOCK, HOLDLOCK|  
|FILA DE RECURSO COMPARTIDO EXCLUSIVO|TABLOCK, XLOCK, HOLDLOCK|  
|EXCLUSIVO|TABLOCKX, HOLDLOCK|  
  
Al seleccionar un modo de conversión en el **modo** cuadro, SSMA aplica la siguiente configuración:  
  
**El modo predeterminado/optimista/completo:** sí  
  
### <a name="convert-open-for-statements-for-ref-cursor-out-parameters"></a>Convertir las instrucciones para abrir para los parámetros REF CURSOR OUT  
De DB2, la instrucción FOR OPEN puede utilizarse para devolver un conjunto de resultados a un parámetro de tipo REF CURSOR de salida del subprograma. En [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)], procedimientos almacenados directamente devuelvan los resultados de las instrucciones SELECT.  
  
SSMA puede convertir muchas instrucciones FOR OPEN en instrucciones SELECT.  
  
-   Si selecciona **Sí**, SSMA convierte la instrucción FOR abierto en una instrucción SELECT, que devuelve el conjunto de resultados para el cliente.  
  
-   Si selecciona **n**, SSMA generará un mensaje de error en el código convertido y en el panel de resultados.  
  
Al seleccionar un modo de conversión en el **modo** cuadro, SSMA aplica la siguiente configuración:  
  
**El modo predeterminado/optimista/completo:** sí  
  
### <a name="convert-record-as-a-list-of-separates-variables"></a>Convertir el registro como una lista de variables de separa  
SSMA puede convertir registros de DB2 de separa variables y variables XML con estructura específica.  
  
-   Si selecciona **Sí**, SSMA convierte el registro en una lista de variables de separa siempre que sea posible.  
  
-   Si selecciona **n**, SSMA convierte el registro en variables XML con estructura específica.  
  
Al seleccionar un modo de conversión en el **modo** cuadro, SSMA aplica la siguiente configuración:  
  
**El modo predeterminado/optimista/completo:** sí  
  
### <a name="convert-substr-function-calls-to-substring-function-calls"></a>Convertir las llamadas de función SUBSTR SUBCADENA para llamadas a funciones  
SSMA puede convertir las llamadas de función SUBSTR de DB2 en [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] **subcadena** llamadas a funciones, dependiendo del número de parámetros. Si SSMA no puede convertir una llamada de función SUBSTR o no se admite el número de parámetros, SSMA convertirá la llamada de función SUBSTR en una llamada de función SSMA personalizada.  
  
-   Si selecciona **Sí**, SSMA convertirá llamadas a función SUBSTR que usan tres parámetros en [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] **subcadena**. Otras funciones SUBSTR se convertirán para llamar a la función SSMA personalizada.  
  
-   Si selecciona **n**, SSMA convertirá la llamada de función SUBSTR en una llamada de función SSMA personalizada.  
  
Al seleccionar un modo de conversión en el **modo** cuadro, SSMA aplica la siguiente configuración:  
  
**Modo predeterminado/optimista:** sí  
  
**Modo completo:** n  
  
### <a name="convert-subtypes"></a>Convertir subtipos  
SSMA puede convertir a subtipos de PL/SQL de dos maneras:  
  
-   Si selecciona **Sí**, creará SSMA [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] definido por el usuario escriba desde un subtipo y usarla para cada variable de este subtipo.  
  
-   Si selecciona **n**, SSMA se sustituya todas las declaraciones de origen del subtipo de con el tipo subyacente y convierta el resultado como de costumbre. En este caso, no hay tipos adicionales se crean en[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]  
  
Al seleccionar un modo de conversión en el **modo** cuadro, SSMA aplica la siguiente configuración:  
  
**El modo predeterminado/optimista/completo:** n  
  
### <a name="convert-synonyms"></a>Convertir sinónimos  
Sinónimos para los siguientes objetos de DB2 pueden migrarse a [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]:  
  
-   Tablas y las tablas de objeto  
  
-   Vistas y vistas de objetos  
  
-   Funciones y procedimientos almacenados  
  
-   Vistas materializadas  
  
Sinónimos para los siguientes objetos de DB2 pueden reemplazarse por referencias directas a los objetos:  
  
-   Secuencias  
  
-   .  
  
-   Objetos de esquema de clase de Java  
  
-   Tipos de objetos definidos por el usuario  
  
No se puede migrar otros sinónimos. SSMA generarán mensajes de error para el sinónimo y todas las referencias que usar el sinónimo.  
  
-   Si selecciona **Sí**, creará SSMA [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] sinónimos y referencias de objeto directo según las listas anteriores.  
  
-   Si selecciona **n**, SSMA creará referencias a objetos directa para todos los sinónimos que se enumeran aquí.  
  
Al seleccionar un modo de conversión en el **modo** cuadro, SSMA aplica la siguiente configuración:  
  
**El modo predeterminado/optimista/completo:** sí  
  
### <a name="convert-tochardate-format"></a>Convertir TO_CHAR (fecha, formato)  
SSMA puede convertir DB2 TO_CHAR(date, format) en los procedimientos de base de datos de sysdb.  
  
-   Si selecciona **función TO_CHAR_DATE utilizando**, SSMA convierte el TO_CHAR (fecha, formato) en la función TO_CHAR_DATE mediante de idioma inglés para la conversión.  
  
-   Si selecciona **función usando TO_CHAR_DATE_LS (NLS cuidado)**, SSMA convierte el TO_CHAR (fecha, formato) en la función TO_CHAR_DATE_LS mediante de idioma de la sesión para la conversión  
  
Al seleccionar un modo de conversión en el **modo** cuadro, SSMA aplica la siguiente configuración:  
  
**El modo predeterminado/Optimistic:** Using TO_CHAR_DATE (función)  
  
**Modo completo:** Using TO_CHAR_DATE_LS función (NLS cuidado)  
  
### <a name="convert-transaction-processing-statements"></a>Convertir las instrucciones de procesamiento de transacciones  
SSMA puede convertir las instrucciones de procesamiento de transacciones de DB2:  
  
-   Si selecciona **Sí**, SSMA convierte instrucciones de procesamiento de transacciones de DB2 a [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] instrucciones.  
  
-   Si selecciona **n**, SSMA marca la transacción que se procesan instrucciones como errores de conversión.  
  
> [!NOTE]  
> DB2 abre implícitamente las transacciones. Para emular este comportamiento en [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)], debe agregar instrucciones BEGIN TRANSACTION manualmente en la que desea que las transacciones para iniciar. Como alternativa, puede ejecutar el comando SET IMPLICIT_TRANSACTIONS ON al principio de la sesión. SSMA agrega SET IMPLICIT_TRANSACTIONS ON de forma automática al convertir subrutinas con transacciones autónomas.  
  
Al seleccionar un modo de conversión en el **modo** cuadro, SSMA aplica la siguiente configuración:  
  
**El modo predeterminado/optimista/completo:** sí  
  
### <a name="emulate-db2-null-behavior-in-order-by-clauses"></a>Emular el comportamiento de null de DB2 en cláusulas ORDER BY  
Valores NULL se ordenan de forma distinta en [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] y DB2:  
  
-   En [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)], NULL los valores son los valores más bajos en una lista ordenada. En una lista ascendente, aparecerá primeros valores NULL.  
  
-   En DB2, valores NULL son los valores más altos en una lista ordenada. De forma predeterminada, los valores NULL aparecen en último lugar en una lista en orden ascendente.  
  
-   DB2 tiene cláusulas de valores NULL primero y último de valores NULL, lo que permite cambiar cómo DB2 ordena los valores NULL.  
  
SSMA puede emular el comportamiento de DB2 ORDER BY activando la casilla de verificación para los valores NULL. A continuación, en primer lugar ordena los valores NULL en el orden especificado y, a continuación, los pedidos por otros valores.  
  
-   Si selecciona **Sí**, SSMA convertirá la instrucción de DB2 de forma que emula el comportamiento de DB2 ORDER BY.  
  
-   Si selecciona **n**, SSMA omitirá las reglas de DB2 y generar un mensaje de error cuando encuentra las cláusulas de valores NULL primero y último de valores NULL.  
  
Al seleccionar un modo de conversión en el **modo** cuadro, SSMA aplica la siguiente configuración:  
  
**Modo predeterminado/optimista:** n  
  
**Modo completo:** sí  
  
### <a name="emulate-row-count-exceptions-in-select"></a>Emular las excepciones de recuento de filas en, seleccione  
Si una instrucción SELECT con una cláusula INTO no devuelve ninguna fila, DB2 provoca una excepción NO_DATA_FOUND. Si la instrucción devuelve dos o más filas, se produce la excepción TOO_MANY_ROWS. La instrucción convertida en [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] no genera ninguna excepción si el recuento de filas es diferente de uno.  
  
-   Si selecciona **Sí**, SSMA agrega la llamada a sysdb procedimiento db_error_exact_one_row_check después de cada instrucción SELECT. Este procedimiento emula las excepciones NO_DATA_FOUND y TOO_MANY_ROWS. Este es el valor predeterminado y permite reproducir el comportamiento de DB2 lo más cerca posible. Siempre debe elegir **Sí** si el código de origen tiene controladores de excepciones que procesan estos errores. Tenga en cuenta que si la instrucción SELECT se produce dentro de una función definida por el usuario, este módulo se convertirá en un procedimiento almacenado, puesto que ejecuta los procedimientos almacenados y generar excepciones no es compatible con [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] contexto de la función.  
  
-   Si selecciona **No**, no se generará ninguna excepción. Que puede ser útil cuando SSMA convierte una función definida por el usuario y desea que siguen siendo una función en[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]  
  
Al seleccionar un modo de conversión en el **modo** cuadro, SSMA aplica la siguiente configuración:  
  
**El modo predeterminado/optimista/completo:** sí  
  
### <a name="generate-error-for-dbmssqlparse"></a>Generar error para DBMS_SQL. ANÁLISIS  
  
-   Si selecciona **Error**, SSMA generará error en la conversión DBMS_SQL. ANÁLISIS.  
  
-   Si selecciona **advertencia**, SSMA generar advertencia en la conversión DBMS_SQL. ANÁLISIS.  
  
Al seleccionar un modo de conversión en el **modo** cuadro, SSMA aplica la siguiente configuración:  
  
**El modo predeterminado/optimista/completo:** Error  
  
### <a name="generate-rowid-column"></a>Generar columna ROWID  
Cuando SSMA crea tablas en [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)], puede crear una columna ROWID. Cuando se migran los datos, cada fila Obtiene un nuevo valor UNIQUEIDENTIFIER generado por la función newid().  
  
-   Si selecciona **Sí**, se crea la columna ROWID en todas las tablas y [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] GUID se genera como se insertan valores. Siempre elija **Sí** si va a usar la herramienta de comprobación de SSMA.  
  
-   Si selecciona **n**, ROWID columnas no se agregan a las tablas.  
  
-   **Agregar columna ROWID para tablas con desencadenadores** agregar ROWID para las tablas que contienen desencadenadores.  
  
> [!WARNING]  
> Valor predeterminado en el caso de SQL Server 2005, SQL Server 2008 y SQL Server 2012 y 2014 es **columna Agregar ROWID para tablas con desencadenadores**.  
  
Al seleccionar un modo de conversión en el **modo** cuadro, SSMA aplica la siguiente configuración:  
  
**El modo predeterminado/Optimistic:** Agregar columna ROWID para tablas con desencadenadores  
  
**Modo completo:** sí  
  
### <a name="generate-unique-index-on-rowid-column"></a>Generar un índice único en la columna ROWID  
Especifica si SSMA genera un columna de índice único en la columna ROWID generado o no. Si la opción está establecida en "Sí", se genera el índice único y si se establece en "NO", no se genera un índice único en la columna ROWID.  
  
Al seleccionar un modo de conversión en el **modo** cuadro, SSMA aplica la siguiente configuración:  
  
**El modo predeterminado/optimista/completo:** sí  
  
### <a name="local-modules-conversion"></a>Conversión de módulos locales  
Define el tipo de conversión de DB2 anidados subprograma (declarado en la función o un procedimiento independiente almacenado).  
  
-   Si selecciona **en línea**, las llamadas anidadas subprograma se reemplazará por su cuerpo.  
  
-   Si selecciona **procedimientos almacenados**, subprograma anidada se convertirá en un procedimiento almacenado de SQL Server y sus llamadas se reemplazará en la llamada a procedimiento.  
  
Al seleccionar un modo de conversión en el **modo** cuadro, SSMA aplica la siguiente configuración:  
  
**El modo predeterminado/optimista/completo:** en línea  
  
### <a name="use-isnull-in-string-concatenation"></a>Use ISNULL de concatenación de cadenas  
DB2 y [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] devolver resultados diferentes cuando concatenaciones de cadenas incluyen valores NULL. DB2 trata el valor NULL como un conjunto de caracteres vacía. [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]Devuelve NULL.  
  
-   Si selecciona **Sí**, SSMA reemplaza el carácter de concatenación de DB2 (|) con el [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] caracteres de concatenación (+). SSMA también comprueba las expresiones en ambos lados de la concatenación de valores NULL.  
  
-   Si selecciona **n**, SSMA reemplaza los caracteres de la concatenación, pero no se buscan valores NULL.  
  
Al seleccionar un modo de conversión en el **modo** cuadro, SSMA aplica la siguiente configuración:  
  
### <a name="use-isnull-in-replace-function-calls"></a>Use ISNULL en llamadas a funciones REPLACE  
Instrucción ISNULL se utiliza en llamadas a funciones REPLACE para emular el comportamiento de DB2. Las siguientes opciones están disponibles para esta configuración:  
  
-   SÍ  
  
-   No  
  
Al seleccionar un modo de conversión en el **modo** cuadro, SSMA aplica la siguiente configuración:  
  
**Modo predeterminado/optimista:** n  
  
**Modo completo:** sí  
  
### <a name="use-isnull-in-concat-function-calls"></a>Use ISNULL en llamadas a función CONCAT  
Instrucción ISNULL se utiliza en llamadas a función CONCAT para emular el comportamiento de DB2. Las siguientes opciones están disponibles para esta configuración:  
  
-   SÍ  
  
-   No  
  
Al seleccionar un modo de conversión en el **modo** cuadro, SSMA aplica la siguiente configuración:  
  
**Modo predeterminado/optimista:** n  
  
**Modo completo:** sí  
  
### <a name="use-native-convert-function-when-possible"></a>Utilice convert nativo función siempre que sea posible  
  
-   Si selecciona **Sí**, SSMA convierte el TO_CHAR (fecha, formato) en función de convert nativo siempre que sea posible.  
  
-   Si selecciona **n**, SSMA convierte el TO_CHAR (fecha, formato) en TO_CHAR_DATE o TO_CHAR_DATE_LS (se define en las opciones de "Convertir TO_CHAR(date, format)").  
  
Al seleccionar un modo de conversión en el **modo** cuadro, SSMA aplica la siguiente configuración:  
  
**Modo predeterminado/optimista:** sí  
  
**Modo completo:** n  
  
### <a name="use-selectfor-xml-when-converting-selectinto-for-record-variable"></a>Utilizar instrucciones SELECT... FOR XML al convertir seleccionar... INTO para la variable de registro  
Especifica si se debe generar un resultado XML que se establece cuando se selecciona en una variable de registro.  
  
-   Si selecciona **Sí**, la instrucción SELECT devuelve XML.  
  
-   Si selecciona **n**, la instrucción SELECT devuelve un conjunto de resultados.  
  
Al seleccionar un modo de conversión en el **modo** cuadro, SSMA aplica la siguiente configuración:  
  
**El modo predeterminado/optimista/completo:** n  
  
## <a name="returning-clause-conversion"></a>Conversión de la cláusula de devolución  
  
### <a name="convert-returning-clause-in-delete-statement-to-output"></a>Convertir cláusula RETURNING en la instrucción DELETE en la salida  
DB2 proporciona una cláusula RETURNING como una manera de obtener inmediatamente los valores eliminados. [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]proporciona esa funcionalidad con la cláusula OUTPUT.  
  
-   Si selecciona **Sí**, SSMA convertirá RETURNING cláusulas en las instrucciones DELETE en las cláusulas de salida. Dado que los desencadenadores en una tabla pueden cambiar valores, el valor devuelto puede variar en [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] de lo que era en DB2.  
  
-   Si selecciona **n**, SSMA generará una instrucción SELECT antes de las instrucciones DELETE para recuperar los valores devueltos.  
  
Al seleccionar un modo de conversión en el **modo** cuadro, SSMA aplica la siguiente configuración:  
  
**El modo predeterminado/optimista/completo:** sí  
  
### <a name="convert-returning-clause-in-insert-statement-to-output"></a>Convertir la cláusula RETURNING en instrucción INSERT en la salida  
DB2 proporciona una cláusula RETURNING como una manera de obtener inmediatamente los valores insertados. [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]proporciona esa funcionalidad con la cláusula OUTPUT.  
  
-   Si selecciona **Sí**, SSMA convertirá una cláusula RETURNING en una instrucción INSERT en la salida. Dado que los desencadenadores en una tabla pueden cambiar valores, el valor devuelto puede variar en [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] de lo que era en DB2.  
  
-   Si selecciona **n**, SSMA emula la funcionalidad de DB2 insertando y, a continuación, seleccionando los valores en una tabla de referencia.  
  
Al seleccionar un modo de conversión en el **modo** cuadro, SSMA aplica la siguiente configuración:  
  
**El modo predeterminado/optimista/completo:** sí  
  
### <a name="convert-returning-clause-in-update-statement-to-output"></a>Convertir cláusula RETURNING en instrucción UPDATE en la salida  
DB2 proporciona una cláusula RETURNING como una manera de obtener inmediatamente los valores actualizados. [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]proporciona esa funcionalidad con la cláusula OUTPUT.  
  
-   Si selecciona **Sí**, SSMA convertirá RETURNING cláusulas en las instrucciones UPDATE en las cláusulas de salida. Dado que los desencadenadores en una tabla pueden cambiar valores, el valor devuelto puede variar en [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] de lo que era en DB2.  
  
-   Si selecciona **n**, SSMA generará las instrucciones SELECT después de las instrucciones UPDATE para recuperar valores de devolución.  
  
Al seleccionar un modo de conversión en el **modo** cuadro, SSMA aplica la siguiente configuración:  
  
**El modo predeterminado/optimista/completo:** sí  
  
## <a name="sequence-conversion"></a>Conversión de secuencia  
  
### <a name="convert-sequence-generator"></a>Convertir el generador de secuencias  
En DB2, puede usar una secuencia para generar identificadores únicos.  
  
SSMA puede convertir secuencias al siguiente.  
  
-   Usar el generador de secuencias de SQL Server (esta opción sólo está disponible cuando se convierte a SQL Server 2012 y SQL Server 2014).  
  
-   Usar el generador de secuencias SSMA.  
  
-   Uso de la identidad de columna.  
  
La opción predeterminada al convertir a SQL Server 2012 o SQL Server 2014 es usar el generador de secuencias de SQL Server. Sin embargo, SQL Server 2012 y SQL Server 2014 no admite la obtención de valor de secuencia actual (como el del método de DB2 secuencia currval). Hacer referencia al sitio de blog de equipo SSMA para obtener instrucciones sobre el método de currval migrar de la secuencia de DB2.  
  
SSMA también ofrece una opción para convertir la secuencia de DB2 al emulador de secuencia SSMA. Esta es la opción predeterminada cuando se convierte a SQL Server anteriores a 2012.  
  
Por último, también puede convertir la secuencia que se asigna a una columna de tabla con valores de identidad de SQL Server. Debe especificar la asignación entre las secuencias para una columna de identidad en DB2 **tabla** ficha  
  
### <a name="convert-currval-outside-triggers"></a>Convertir CURRVAL fuera de desencadenadores  
Sólo está visible cuando se establece el generador de secuencias convertir en **utilizando la identidad de la columna**. Puesto que las secuencias de DB2 son objetos independientes de las tablas, muchas de las tablas que utilizan secuencias de utilizan un desencadenador para generar e insertar un nuevo valor de secuencia. SSMA estas instrucciones en comentario o marca como errores cuando el comentario fuera generan errores.  
  
-   Si selecciona **Sí**, SSMA marcará todas las referencias para fuera de desencadenadores en convertido de secuencia CURRVAL con una advertencia.  
  
-   Si selecciona **n**, SSMA marcará todas las referencias para fuera de desencadenadores en convertido de secuencia CURRVAL con un error.  
  
## <a name="see-also"></a>Vea también  
[Referencia de la interfaz de usuario &#40; DB2ToSQL &#41;](../../ssma/db2/user-interface-reference-db2tosql.md)  
  

