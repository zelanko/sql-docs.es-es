---
title: Configuración (conversión) (DB2ToSQL) del proyecto | Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: 538c93cf-c5bb-43d5-b758-186d9fb00c19
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.openlocfilehash: a446fd4ce116ee19aa8b38d1ae6d8213e35c16e1
ms.sourcegitcommit: 1ab115a906117966c07d89cc2becb1bf690e8c78
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/27/2018
ms.locfileid: "52392479"
---
# <a name="project-settings-conversion-db2tosql"></a>Configuración del proyecto (conversión) (DB2ToSQL)
La página de conversión de la **configuración del proyecto** cuadro de diálogo contiene la configuración que permiten personalizar cómo SSMA convierte la sintaxis de DB2 a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] sintaxis.  
  
El panel de conversión está disponible en el **configuración del proyecto** y **configuración de proyecto predeterminada** cuadros de diálogo:  
  
-   Para especificar la configuración para todos los proyectos SSMA, en el **herramientas** menú haga clic en **la configuración predeterminada del proyecto**, seleccione el tipo de proyecto de migración para los que es necesaria para ver o cambiar de configuración  **Versión de destino de migración** lista desplegable y, después, haga clic en **General** en la parte inferior del panel izquierdo y, a continuación, haga clic en **conversión**.  
  
-   Para especificar la configuración para el proyecto actual, en el **herramientas** menú haga clic en **configuración del proyecto**, a continuación, haga clic en **General** en la parte inferior del panel izquierdo y, a continuación, haga clic en **Conversión**.  
  
## <a name="conversion-messages"></a>Mensajes de conversión  
  
### <a name="generate-messages-about-issues-applied"></a>Generar mensajes acerca de los problemas que se aplica  
Especifica si SSMA genera mensajes informativos durante la conversión, mostrarlos en el panel de resultados y agregarlos al código convertido.  
  
Al seleccionar un modo de conversión en el **modo** cuadro, SSMA aplica la siguiente configuración:  
  
**Modo predeterminado/optimista:** No  
  
**Modo completo:** No  
  
## <a name="miscellaneous-options"></a>Otras opciones  
  
### <a name="cast-rownum-expressions-as-integers"></a>Expresiones de conversión ROWNUM como enteros  
Cuando SSMA convierte expresiones ROWNUM, convierte la expresión en una cláusula TOP, seguida por la expresión. El ejemplo siguiente muestra ROWNUM en una instrucción DELETE de DB2:  
  
`DELETE FROM Table1`  
  
`WHERE ROWNUM < expression and Field1 >= 2`  
  
El ejemplo siguiente muestra el resultado [!INCLUDE[tsql](../../includes/tsql-md.md)]:  
  
`DELETE TOP (expression-1)`  
  
`FROM Table1`  
  
`WHERE Field1>=2`  
  
La parte superior, se requiere que la expresión de cláusulas principales se evalúa como un entero. Si el entero es negativo, la instrucción producirá un error.  
  
-   Si selecciona **Sí**, SSMA convierte la expresión como un número entero.  
  
-   Si selecciona **No**, SSMA marcará todas las expresiones de tipo no entero como un error en el código convertido.  
  
Al seleccionar un modo de conversión en el **modo** cuadro, SSMA aplica la siguiente configuración:  
  
**Modo completo o de forma predeterminada:** No  
  
**Modo optimista:** Sí  
  
### <a name="default-schema-mapping"></a>Asignación de esquema predeterminada  
Esta configuración especifica cómo se asignan los esquemas de DB2 a esquemas de SQL Server. Dos opciones están disponibles en esta configuración:  
  
1.  **Esquema de base de datos:** En este esquema de DB2 de modo 'sch1' se asignará al esquema de SQL Server 'dbo' en la base de datos de SQL Server 'sch1' de forma predeterminada.  
  
2.  **Esquema al esquema:** en este modo DB2 el esquema 'sch1' se asignará al esquema de SQL Server 'sch1' en la base de datos de SQL Server predeterminado proporcionado en el cuadro de diálogo de conexión de forma predeterminada.  
  
Al seleccionar un modo de conversión en el **modo** cuadro, SSMA aplica la siguiente configuración:  
  
**Modo predeterminado/optimista/completo:** Esquema de base de datos  
  
### <a name="conversion-ways-of-merge-statement"></a>Formas de conversión de la instrucción MERGE  
  
-   Si selecciona **mediante INSERT, UPDATE, instrucción DELETE**, SSMA convierte la instrucción de fusión en INSERCIÓN, actualización y eliminación de instrucciones.  
  
-   Si selecciona **instrucción utilizando MERGE**, SSMA convierte la instrucción de combinación en la instrucción MERGE en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
> [!WARNING]  
> Esta opción de configuración de proyecto sólo está disponible en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2008, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2012, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2014.  
  
Al seleccionar un modo de conversión en el **modo** cuadro, SSMA aplica la siguiente configuración:  
  
**Modo predeterminado/optimista/completo:** Instrucción MERGE  
  
### <a name="convert-calls-to-subprograms-that-use-default-arguments"></a>Convertir las llamadas a subprogramas que utilizan argumentos predeterminados  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] funciones no admiten la omisión de los parámetros en la llamada de función. Además, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] funciones y procedimientos no admiten expresiones como valores de parámetro predeterminados.  
  
-   Si selecciona **Sí** y una llamada de función omite los parámetros, SSMA insertará la palabra clave **predeterminado** en la función y llamada en la posición correcta. A continuación, marcará la llamada con una advertencia.  
  
-   Si selecciona **No**, SSMA marcará las llamadas de función como errores.  
  
Al seleccionar un modo de conversión en el **modo** cuadro, SSMA aplica la siguiente configuración:  
  
**Modo predeterminado/optimista/completo:** Sí  
  
### <a name="convert-count-function-to-countbig"></a>Convertir función COUNT para COUNT_BIG  
Si las funciones de recuento están probables que devuelven valores mayores que 2.147.483.647, que es 2<sup>31</sup>-1, debe convertir las funciones a COUNT_BIG.  
  
-   Si selecciona **Sí**, SSMA convertirá todos los usos de recuento en COUNT_BIG.  
  
-   Si selecciona **No**, las funciones permanecerá como recuento. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] se devolverá un error si la función devuelve un valor mayor que 2<sup>31</sup>-1.  
  
Al seleccionar un modo de conversión en el **modo** cuadro, SSMA aplica la siguiente configuración:  
  
**Modo completo o de forma predeterminada:** Sí  
  
**Modo optimista:** No  
  
### <a name="convert-forall-statement-to-while-statement"></a>Convertir instrucción FORALL en WHILE instrucción  
Define cómo tratará SSMA FORALL bucles en elementos de la colección de PL/SQL.  
  
-   Si selecciona **Sí**, SSMA crea un bucle WHILE, donde los elementos de la colección son recuperados uno por uno.  
  
-   Si selecciona **No**, SSMA genera un conjunto de filas de la colección utilizando el método de nodos () y lo usa como una sola tabla. Esto es más eficaz, pero hace que el código de salida sea menos legible.  
  
Al seleccionar un modo de conversión en el **modo** cuadro, SSMA aplica la siguiente configuración:  
  
**Modo predeterminado/optimista:** No  
  
**Modo completo:** Sí  
  
### <a name="convert-foreign-keys-with-set-null-referential-action-on-column-that-is-not-null"></a>Las claves externas de Convert con la acción referencial SET NULL en la columna que es no NULL  
DB2 permite crear restricciones de clave externa, donde una acción SET NULL podría no posiblemente se puede realizar porque no se permiten valores NULL en la columna que se hace referencia. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] no se permite esta configuración de clave externa.  
  
-   Si selecciona **Sí**, SSMA generará las acciones referenciales en DB2, pero necesita realizar cambios manuales antes de cargar la restricción [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Por ejemplo, puede elegir NO ACTION en lugar de establecer como NULL.  
  
-   Si selecciona **No**, la restricción se marcará como un error.  
  
Al seleccionar un modo de conversión en el **modo** cuadro, SSMA aplica la siguiente configuración:  
  
**Modo predeterminado/optimista/completo:** No  
  
### <a name="convert-function-calls-to-procedure-calls"></a>Convertir las llamadas de función a las llamadas a procedimientos  
Algunas funciones de DB2 se definen como transacciones autónomas o contener instrucciones que no sería válidas en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. En estos casos, SSMA crea un procedimiento y una función que es un contenedor para el procedimiento. La función convertida llama al procedimiento de implementación.  
  
SSMA puede convertir las llamadas a la función contenedora en llamadas al procedimiento. Esto crea código más legible y puede mejorar el rendimiento. Sin embargo, el contexto no siempre lo permite; Por ejemplo, no se puede reemplazar una llamada de función en la lista de selección con una llamada a procedimiento. SSMA tiene unas cuantas opciones para cubrir los casos más comunes:  
  
-   Si selecciona **siempre**, SSMA intenta convertir las llamadas de función de contenedor en las llamadas a procedimiento. Si el contexto actual no admite esta conversión, se genera un mensaje de error. De este modo, no hay llamadas de función se dejan en el código generado.  
  
-   Si selecciona **cuando sea posible**, SSMA realiza un movimiento en las llamadas a procedimiento únicamente si la función tiene parámetros de salida. Cuando el movimiento no es posible, se quita el atributo de salida del parámetro. En todos los demás casos SSMA deja las llamadas de función.  
  
-   Si selecciona **nunca**, SSMA dejará de todas las llamadas de función como llamadas de función. A veces, esta opción puede ser inaceptable debido a motivos de rendimiento.  
  
Al seleccionar un modo de conversión en el **modo** cuadro, SSMA aplica la siguiente configuración:  
  
**Modo predeterminado/optimista/completo:** Cuando sea posible  
  
### <a name="convert-lock-table-statements"></a>Convertir las instrucciones de la tabla de bloqueo  
SSMA puede convertir muchas instrucciones de la tabla de BLOQUEOS en las sugerencias de tabla. SSMA no puede convertir cualquier instrucción de bloqueo tabla que contiene la partición, SUBPARTITION, @dblinky las cláusulas NOWAIT y se marcará estas instrucciones con mensajes de error de conversión.  
  
-   Si selecciona **Sí**, SSMA convertirá las instrucciones de bloqueo tabla admitidas en las sugerencias de tabla.  
  
-   Si selecciona **No**, SSMA marcará todas las instrucciones de la tabla de bloqueo con mensajes de error de conversión.  
  
En la tabla siguiente se muestra cómo SSMA convierte los modos de bloqueo de DB2:  
  
|||  
|-|-|  
|DB2 Modo de bloqueo|Sugerencia de tabla SQL Server|  
|RECURSO COMPARTIDO DE FILA|ROWLOCK, HOLDLOCK|  
|EXCLUSIVO DE FILA|HOLDLOCK ROWLOCK, XLOCK,|  
|ACTUALIZACIÓN DE RECURSO COMPARTIDO = EL RECURSO COMPARTIDO DE FILA|ROWLOCK, HOLDLOCK|  
|COMPARTIR|TABLOCK, HOLDLOCK|  
|EXCLUSIVO DE FILA DE RECURSO COMPARTIDO|TABLOCK, XLOCK, HOLDLOCK|  
|EXCLUSIVO|TABLOCKX, HOLDLOCK|  
  
Al seleccionar un modo de conversión en el **modo** cuadro, SSMA aplica la siguiente configuración:  
  
**Modo predeterminado/optimista/completo:** Sí  
  
### <a name="convert-open-for-statements-for-ref-cursor-out-parameters"></a>Convertir instrucciones OPEN FOR para los parámetros REF CURSOR OUT  
En DB2, la instrucción OPEN FOR puede usarse para devolver un conjunto de resultados a un parámetro de tipo REF CURSOR de salida del subprograma. En [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], procedimientos almacenados devuelven directamente los resultados de las instrucciones SELECT.  
  
SSMA puede convertir muchas instrucciones OPEN FOR en instrucciones SELECT.  
  
-   Si selecciona **Sí**, SSMA convierte la instrucción OPEN FOR en una instrucción SELECT, que devuelve el conjunto de resultados para el cliente.  
  
-   Si selecciona **No**, SSMA generará un mensaje de error en el código convertido y en el panel de salida.  
  
Al seleccionar un modo de conversión en el **modo** cuadro, SSMA aplica la siguiente configuración:  
  
**Modo predeterminado/optimista/completo:** Sí  
  
### <a name="convert-record-as-a-list-of-separates-variables"></a>Convertir el registro como una lista de variables separa  
SSMA puede convertir los registros de DB2 en variables separa en variables XML con estructura específica.  
  
-   Si selecciona **Sí**, SSMA convierte el registro en una lista de variables de separa cuando sea posible.  
  
-   Si selecciona **No**, SSMA convierte el registro en variables XML con estructura específica.  
  
Al seleccionar un modo de conversión en el **modo** cuadro, SSMA aplica la siguiente configuración:  
  
**Modo predeterminado/optimista/completo:** Sí  
  
### <a name="convert-substr-function-calls-to-substring-function-calls"></a>Convertir las llamadas de función SUBSTR para llamadas de función SUBSTRING  
SSMA puede convertir las llamadas de función SUBSTR DB2 en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **subcadena** llamadas a funciones, dependiendo del número de parámetros. Si SSMA no puede convertir una llamada de función SUBSTR o no se admite el número de parámetros, SSMA convertirá la llamada de función SUBSTR en una llamada de función SSMA personalizada.  
  
-   Si selecciona **Sí**, SSMA convertirá las llamadas de función SUBSTR que usan tres parámetros en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **subcadena**. Otras funciones SUBSTR se convertirán para llamar a la función personalizada de SSMA.  
  
-   Si selecciona **No**, SSMA convertirá la llamada de función SUBSTR en una llamada de función SSMA personalizada.  
  
Al seleccionar un modo de conversión en el **modo** cuadro, SSMA aplica la siguiente configuración:  
  
**Modo predeterminado/optimista:** Sí  
  
**Modo completo:** No  
  
### <a name="convert-subtypes"></a>Convertir a subtipos  
SSMA puede convertir a subtipos de PL/SQL de dos maneras:  
  
-   Si selecciona **Sí**, creará SSMA [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] definido por el usuario escriba desde un subtipo y usarlo para cada variable de este subtipo.  
  
-   Si selecciona **No**, SSMA se sustituya todas las declaraciones de origen del subtipo de con el tipo subyacente y convertir el resultado como de costumbre. En este caso, no hay tipos adicionales se crean en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]  
  
Al seleccionar un modo de conversión en el **modo** cuadro, SSMA aplica la siguiente configuración:  
  
**Modo predeterminado/optimista/completo:** No  
  
### <a name="convert-synonyms"></a>Convertir sinónimos  
Sinónimos de los siguientes objetos de DB2 pueden migrarse a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]:  
  
-   Las tablas y objetos  
  
-   Vistas y objetos  
  
-   Funciones y procedimientos almacenados  
  
-   Vistas materializadas  
  
Sinónimos de los siguientes objetos de DB2 pueden reemplazarse por referencias directas a los objetos:  
  
-   Secuencias  
  
-   .  
  
-   Objetos de esquema de clase de Java  
  
-   Tipos de objeto definido por el usuario  
  
No se puede migrar otros sinónimos. SSMA generará mensajes de error para el sinónimo y todas las referencias que usar el sinónimo.  
  
-   Si selecciona **Sí**, creará SSMA [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] sinónimos y referencias a objetos directos según las listas anteriores.  
  
-   Si selecciona **No**, SSMA creará las referencias de objeto directo para todos los sinónimos que se muestran aquí.  
  
Al seleccionar un modo de conversión en el **modo** cuadro, SSMA aplica la siguiente configuración:  
  
**Modo predeterminado/optimista/completo:** Sí  
  
### <a name="convert-tochardate-format"></a>Convertir TO_CHAR (fecha, formato)  
SSMA puede convertir TO_CHAR(date, format) DB2 en los procedimientos de la base de datos sysdb.  
  
-   Si selecciona **función TO_CHAR_DATE utilizando**, SSMA convierte la TO_CHAR (fecha, formato) en función TO_CHAR_DATE mediante del idioma inglés para la conversión.  
  
-   Si selecciona **función utilizando TO_CHAR_DATE_LS (NLS atención)**, SSMA convierte la TO_CHAR (fecha, formato) en función TO_CHAR_DATE_LS mediante de idioma de la sesión para la conversión  
  
Al seleccionar un modo de conversión en el **modo** cuadro, SSMA aplica la siguiente configuración:  
  
**Modo predeterminado/optimista:** Uso de la función TO_CHAR_DATE  
  
**Modo completo:** Usar función TO_CHAR_DATE_LS (NLS atención)  
  
### <a name="convert-transaction-processing-statements"></a>Convertir las instrucciones de procesamiento de transacciones  
SSMA puede convertir las instrucciones de procesamiento de transacciones de DB2:  
  
-   Si selecciona **Sí**, SSMA convierte DB2 las instrucciones de procesamiento de transacciones a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] instrucciones.  
  
-   Si selecciona **No**, SSMA marca la transacción como errores de conversión de instrucciones de procesamiento.  
  
> [!NOTE]  
> DB2 abre implícitamente las transacciones. Para emular este comportamiento en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], debe agregar instrucciones BEGIN TRANSACTION manualmente en la que desea que las transacciones para iniciar. Como alternativa, puede ejecutar el comando SET IMPLICIT_TRANSACTIONS ON al principio de la sesión. SSMA agrega SET IMPLICIT_TRANSACTIONS ON de forma automática al convertir las subrutinas con transacciones autónomas.  
  
Al seleccionar un modo de conversión en el **modo** cuadro, SSMA aplica la siguiente configuración:  
  
**Modo predeterminado/optimista/completo:** Sí  
  
### <a name="emulate-db2-null-behavior-in-order-by-clauses"></a>Emular el comportamiento de null de DB2 en las cláusulas ORDER BY  
Los valores NULL están ordenados de manera diferente en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] y DB2:  
  
-   En [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], NULL los valores son los valores más bajos en una lista ordenada. En una lista en orden ascendente, aparecerán primeros los valores NULL.  
  
-   En DB2, los valores NULL son los valores más altos en una lista ordenada. De forma predeterminada, los valores NULL aparecen en último lugar en una lista en orden ascendente.  
  
-   DB2 tiene las cláusulas de los valores NULL primero y último de los valores NULL, lo que permite cambiar cómo DB2 ordena los valores NULL.  
  
SSMA puede emular el comportamiento DB2 ORDER BY activando la casilla de verificación para los valores NULL. , A continuación, en primer lugar ordena los valores NULL en el orden especificado y, a continuación, los pedidos por otros valores.  
  
-   Si selecciona **Sí**, SSMA convertirá la instrucción de DB2 de forma que emula el comportamiento de DB2 ORDER BY.  
  
-   Si selecciona **No**, SSMA omitirá las reglas de DB2 y generar un mensaje de error cuando encuentra las cláusulas de los valores NULL primero y último de los valores NULL.  
  
Al seleccionar un modo de conversión en el **modo** cuadro, SSMA aplica la siguiente configuración:  
  
**Modo predeterminado/optimista:** No  
  
**Modo completo:** Sí  
  
### <a name="emulate-row-count-exceptions-in-select"></a>Emular las excepciones de recuento de filas en SELECT  
Si una instrucción SELECT con una cláusula INTO no devuelve ninguna fila, DB2 genera una excepción NO_DATA_FOUND. Si la instrucción devuelve dos o más filas, se produce la excepción TOO_MANY_ROWS. La instrucción convertida en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] no genera ninguna excepción si el recuento de filas es diferente de uno.  
  
-   Si selecciona **Sí**, SSMA agrega la llamada a sysdb procedimiento db_error_exact_one_row_check después de cada instrucción SELECT. Este procedimiento emula las excepciones NO_DATA_FOUND y TOO_MANY_ROWS. Este es el valor predeterminado y permite reproducir el comportamiento de DB2, lo más cerca como sea posible. Siempre debe elegir **Sí** si el código fuente tiene controladores de excepciones que procesan estos errores. Tenga en cuenta que si se produce la instrucción SELECT dentro de una función definida por el usuario, este módulo se convertirá en un procedimiento almacenado, porque la ejecución de procedimientos almacenados y generar excepciones no es compatible con [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] contexto de la función.  
  
-   Si selecciona **No**, no se generará ninguna excepción. Esto puede ser útil cuando SSMA convierte una función definida por el usuario y desea que permanezca en una función de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]  
  
Al seleccionar un modo de conversión en el **modo** cuadro, SSMA aplica la siguiente configuración:  
  
**Modo predeterminado/optimista/completo:** Sí  
  
### <a name="generate-error-for-dbmssqlparse"></a>Genera el error para DBMS_SQL. ANALIZAR  
  
-   Si selecciona **Error**, SSMA generar error en la conversión DBMS_SQL. ANALIZAR.  
  
-   Si selecciona **advertencia**, SSMA generar advertencia en la conversión DBMS_SQL. ANALIZAR.  
  
Al seleccionar un modo de conversión en el **modo** cuadro, SSMA aplica la siguiente configuración:  
  
**Modo predeterminado/optimista/completo:** Error  
  
### <a name="generate-rowid-column"></a>Generar columna ROWID  
Cuando crea tablas en SSMA [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], puede crear una columna ROWID. Cuando se migran los datos, cada fila Obtiene un nuevo valor UNIQUEIDENTIFIER generado por la función newid().  
  
-   Si selecciona **Sí**, se crea la columna ROWID en todas las tablas y [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] GUID se genera como insertar valores. Elija siempre **Sí** si va a usar la herramienta de comprobación de SSMA.  
  
-   Si selecciona **No**, no se agregan columnas ROWID a las tablas.  
  
-   **Agregar columna ROWID para tablas con desencadenadores** agregar ROWID para las tablas que contienen desencadenadores.  
  
> [!WARNING]  
> Es el valor predeterminado en el caso de SQL Server 2005, SQL Server 2008 y SQL Server 2012 y 2014 **columna ROWID agregar las tablas con desencadenadores**.  
  
Al seleccionar un modo de conversión en el **modo** cuadro, SSMA aplica la siguiente configuración:  
  
**Modo predeterminado/optimista:** Agregar columna ROWID para tablas con desencadenadores  
  
**Modo completo:** Sí  
  
### <a name="generate-unique-index-on-rowid-column"></a>Generar un índice único en la columna ROWID  
Especifica si SSMA genera la columna de índice único en la columna ROWID generado o no. Si la opción está establecida en "Sí", se genera el índice único y si se establece en "NO", no se genera un índice único en la columna ROWID.  
  
Al seleccionar un modo de conversión en el **modo** cuadro, SSMA aplica la siguiente configuración:  
  
**Modo predeterminado/optimista/completo:** Sí  
  
### <a name="local-modules-conversion"></a>Conversión de módulos locales  
Define el tipo de conversión de DB2 anidados subprograma (declarado en el procedimiento independiente almacenado o función).  
  
-   Si selecciona **Inline**, las llamadas anidadas subprograma se reemplazará por su cuerpo.  
  
-   Si selecciona **procedimientos almacenados**subprograma anidada se convertirá en un procedimiento almacenado de SQL Server y sus llamadas se reemplazará en esta llamada a procedimiento.  
  
Al seleccionar un modo de conversión en el **modo** cuadro, SSMA aplica la siguiente configuración:  
  
**Modo predeterminado/optimista/completo:** En línea  
  
### <a name="use-isnull-in-string-concatenation"></a>Usar ISNULL de concatenación de cadenas  
DB2 y [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] devolver resultados diferentes cuando concatenaciones de cadenas incluyen valores NULL. DB2 trata el valor NULL como un juego de caracteres vacía. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Devuelve NULL.  
  
-   Si selecciona **Sí**, SSMA reemplaza el carácter de concatenación de DB2 (|) con el [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] carácter de concatenación (+). SSMA también comprueba las expresiones en ambos lados de la concatenación de valores NULL.  
  
-   Si selecciona **No**, SSMA reemplaza los caracteres de la concatenación, pero no comprueba los valores NULL.  
  
Al seleccionar un modo de conversión en el **modo** cuadro, SSMA aplica la siguiente configuración:  
  
### <a name="use-isnull-in-replace-function-calls"></a>Usar ISNULL en llamadas a funciones de reemplazo  
Instrucción ISNULL se utiliza en llamadas a funciones de reemplazo para emular el comportamiento de DB2. Las siguientes opciones están disponibles para esta configuración:  
  
-   SÍ  
  
-   No  
  
Al seleccionar un modo de conversión en el **modo** cuadro, SSMA aplica la siguiente configuración:  
  
**Modo predeterminado/optimista:** No  
  
**Modo completo:** Sí  
  
### <a name="use-isnull-in-concat-function-calls"></a>Usar ISNULL en llamadas a función CONCAT  
Instrucción ISNULL se utiliza en llamadas a función CONCAT para emular el comportamiento de DB2. Las siguientes opciones están disponibles para esta configuración:  
  
-   SÍ  
  
-   No  
  
Al seleccionar un modo de conversión en el **modo** cuadro, SSMA aplica la siguiente configuración:  
  
**Modo predeterminado/optimista:** No  
  
**Modo completo:** Sí  
  
### <a name="use-native-convert-function-when-possible"></a>Utilice convert nativo función cuando sea posible  
  
-   Si selecciona **Sí**, SSMA convierte la TO_CHAR (fecha, formato) en función de convert nativo cuando sea posible.  
  
-   Si selecciona **No**, SSMA convierte la TO_CHAR (fecha, formato) en TO_CHAR_DATE o TO_CHAR_DATE_LS (se define mediante las opciones "Convertir TO_CHAR(date, format)").  
  
Al seleccionar un modo de conversión en el **modo** cuadro, SSMA aplica la siguiente configuración:  
  
**Modo predeterminado/optimista:** Sí  
  
**Modo completo:** No  
  
### <a name="use-selectfor-xml-when-converting-selectinto-for-record-variable"></a>Usar SELECT... FOR XML al convertir seleccionar... INTO para la variable de registro  
Especifica si se debe generar un resultado XML que se establece cuando se selecciona en una variable de registro.  
  
-   Si selecciona **Sí**, la instrucción SELECT devuelve XML.  
  
-   Si selecciona **No**, la instrucción SELECT devuelve un conjunto de resultados.  
  
Al seleccionar un modo de conversión en el **modo** cuadro, SSMA aplica la siguiente configuración:  
  
**Modo predeterminado/optimista/completo:** No  
  
## <a name="returning-clause-conversion"></a>DEVOLVER la conversión de cláusula  
  
### <a name="convert-returning-clause-in-delete-statement-to-output"></a>Convertir cláusula RETURNING en la instrucción DELETE en la salida  
DB2 proporciona una cláusula RETURNING como una manera de obtener inmediatamente los valores eliminados. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] proporciona esa funcionalidad con la cláusula OUTPUT.  
  
-   Si selecciona **Sí**, SSMA convertirá RETURNING cláusulas en instrucciones DELETE en las cláusulas de salida. Dado que los desencadenadores en una tabla pueden cambiar los valores, el valor devuelto podría ser diferente en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] de lo que era en DB2.  
  
-   Si selecciona **No**, SSMA generará una instrucción SELECT antes de las instrucciones DELETE para recuperar los valores devueltos.  
  
Al seleccionar un modo de conversión en el **modo** cuadro, SSMA aplica la siguiente configuración:  
  
**Modo predeterminado/optimista/completo:** Sí  
  
### <a name="convert-returning-clause-in-insert-statement-to-output"></a>Convertir cláusula RETURNING en instrucción INSERT en la salida  
DB2 proporciona una cláusula RETURNING como una manera de obtener inmediatamente los valores insertados. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] proporciona esa funcionalidad con la cláusula OUTPUT.  
  
-   Si selecciona **Sí**, SSMA convertirá una cláusula RETURNING en una instrucción INSERT en la salida. Dado que los desencadenadores en una tabla pueden cambiar los valores, el valor devuelto podría ser diferente en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] de lo que era en DB2.  
  
-   Si selecciona **No**, SSMA emula la funcionalidad de DB2 insertando y, a continuación, seleccionando los valores en una tabla de referencia.  
  
Al seleccionar un modo de conversión en el **modo** cuadro, SSMA aplica la siguiente configuración:  
  
**Modo predeterminado/optimista/completo:** Sí  
  
### <a name="convert-returning-clause-in-update-statement-to-output"></a>Convertir cláusula RETURNING en instrucción UPDATE en la salida  
DB2 proporciona una cláusula RETURNING como una manera de obtener inmediatamente los valores actualizados. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] proporciona esa funcionalidad con la cláusula OUTPUT.  
  
-   Si selecciona **Sí**, SSMA convertirá RETURNING cláusulas en instrucciones UPDATE en las cláusulas de salida. Dado que los desencadenadores en una tabla pueden cambiar los valores, el valor devuelto podría ser diferente en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] de lo que era en DB2.  
  
-   Si selecciona **No**, SSMA generará las instrucciones SELECT después de las instrucciones UPDATE para recuperar valores de devolución.  
  
Al seleccionar un modo de conversión en el **modo** cuadro, SSMA aplica la siguiente configuración:  
  
**Modo predeterminado/optimista/completo:** Sí  
  
## <a name="sequence-conversion"></a>Conversión de secuencia  
  
### <a name="convert-sequence-generator"></a>Convertir el generador de secuencias  
En DB2, puede usar una secuencia para generar identificadores únicos.  
  
SSMA puede convertir las secuencias en el siguiente.  
  
-   Uso el generador de secuencias de SQL Server (esta opción solo está disponible cuando se convierte a SQL Server 2012 y SQL Server 2014).  
  
-   Uso el generador de secuencias SSMA.  
  
-   Mediante la identidad de la columna.  
  
La opción predeterminada cuando se convierte a SQL Server 2012 o SQL Server 2014 es usar el generador de secuencias de SQL Server. Sin embargo, SQL Server 2012 y SQL Server 2014 no admite la obtención de valor actual de la secuencia (por ejemplo, que el del método de DB2 secuencia currval). Hacer referencia al sitio de blog de equipo SSMA para obtener instrucciones sobre el método de migración DB2 secuencia currval.  
  
SSMA también proporciona una opción para convertir la secuencia de DB2 al emulador de secuencia SSMA. Esta es la opción predeterminada cuando se convierte a SQL Server anteriores a 2012.  
  
Por último, también puede convertir la secuencia que se asigna a una columna de tabla a valores de identidad de SQL Server. Debe especificar la asignación entre las secuencias de una columna de identidad en DB2 **tabla** ficha  
  
### <a name="convert-currval-outside-triggers"></a>Convertir CURRVAL fuera de los desencadenadores  
Sólo está visible cuando se establece el generador de secuencias de convertir en **utilizando la identidad de la columna**. Dado que las secuencias de DB2 son objetos independientes de las tablas, muchas de las tablas que utilizan secuencias de utilizan un desencadenador para generar e insertar un nuevo valor de secuencia. SSMA estas instrucciones en comentario o los marca como errores cuando el comentario fuera generan errores.  
  
-   Si selecciona **Sí**, SSMA marcará todas las referencias para fuera de los desencadenadores en convertido CURRVAL de secuencia con una advertencia.  
  
-   Si selecciona **No**, SSMA marcará todas las referencias para fuera de los desencadenadores en convertido CURRVAL de secuencia con un error.  
  
## <a name="see-also"></a>Vea también  
[Referencia de la interfaz de usuario &#40;DB2ToSQL&#41;](../../ssma/db2/user-interface-reference-db2tosql.md)  
  
