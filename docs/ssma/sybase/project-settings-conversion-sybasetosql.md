---
title: Configuración del proyecto (conversión) (SybaseToSQL) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: eeb80fa5-f530-4f21-beee-25f5a4b8ace6
author: Shamikg
ms.author: Shamikg
ms.openlocfilehash: 5d4936638fc9e283caafffc2f2a7cfdbed396920
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/27/2020
ms.locfileid: "68028763"
---
# <a name="project-settings-conversion-sybasetosql"></a>Configuración del proyecto (conversión) (SybaseToSQL)
La página conversión del cuadro de diálogo **configuración del proyecto** contiene opciones que personalizan el modo en que SSMA convierte la sintaxis de Sybase Adaptive [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Server Enterprise (ASE) en o SQL Azure sintaxis.  
  
El panel conversión está disponible en los cuadros de diálogo Configuración del **proyecto** y **configuración predeterminada del proyecto** :  
  
-   Si desea especificar la configuración de todos los proyectos de SSMA, en el menú **herramientas** , seleccione **configuración predeterminada del proyecto**, haga clic en **General** en la parte inferior del panel izquierdo y, a continuación, haga clic en **conversión**.  
  
-   Para especificar la configuración del proyecto actual, en el menú **herramientas** , seleccione **configuración del proyecto**, haga clic en **General** en la parte inferior del panel izquierdo y, a continuación, haga clic en **conversión**.  
  
## <a name="miscellaneous-options"></a>Otras opciones  
**@@ERROR**  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]/SQL Azure y ASE usan códigos de error diferentes.  
  
Use esta opción para especificar el tipo de mensaje (ADVERTENCIA o error) que SSMA muestra en el panel de salida o lista de errores cuando encuentra una referencia a **@@ERROR ** en el código ase.  
  
-   Si selecciona **convertir y marcar con ADVERTENCIA**, SSMA convertirá las instrucciones y las marcará con comentarios de advertencia.  
  
-   Si selecciona **Mark with error**, SSMA omitirá la conversión y marcará las instrucciones con comentarios de error.  
  
Al seleccionar un modo de conversión en el cuadro **modo** , SSMA aplica la siguiente configuración:  
  
**Modo predeterminado/optimista:** Convertir y marcar con ADVERTENCIA  
  
**Modo completo:** Marcar con error  
  
**Conversión de operador LIKE**  
Especifica si se deben convertir los operandos LIKE para que coincidan con el comportamiento de Sybase ASE. El punto es que Sybase recorta los espacios en blanco finales en un patrón like. La solución consiste en convertir una conversión de expresión derecha en un tipo de datos de longitud fija con una precisión máxima.  
  
-   Seleccione **conversión simple** para convertir las expresiones sin ninguna corrección.  
  
-   Para usar el comportamiento de ASE, seleccione **conversión a longitud fija.**  
  
Al seleccionar un modo de conversión en el cuadro modo, SSMA aplica la siguiente configuración:  
  
**Modo predeterminado/optimista**: conversión simple  
  
**Modo completo**: conversión a longitud fija  
  
**CONVERTIR O CONVERTIR CADENAS VACÍAS EN TIPOS NUMÉRICOS**  
Especifica cómo administrar cadenas vacías o vacías dentro de expresiones CONVERT o CAST con el tipo numérico como argumento DataType. Las siguientes opciones están disponibles para esta configuración:  
  
-   Seleccione **conversión simple** para convertir las expresiones sin ninguna corrección.  
  
-   Si se selecciona una **cadena vacía como cero numérico** , el parámetro de cadena {s} se reemplazará por Case LTrim (rtrim ({s})) cuando "", y 0 else {s} expresión end  
  
Al seleccionar un modo de conversión en el cuadro modo, SSMA aplica la siguiente configuración:  
  
**Modo predeterminado/optimista**: conversión simple  
  
**Modo completo**: cadena vacía como cero numérico  
  
**Concatenación de NULL**  
Esta configuración especifica cómo convertir la concatenación de cadenas con NULL. Se pueden establecer las siguientes opciones para esta configuración determinada:  
  
-   **Wrap con la función ISNULL:** Si se establece esta opción, cada ' string_expression ' que no sea constante en la concatenación se ajustará con ISNULL (string_expression) y los valores NULL se reemplazarán por una cadena vacía.  
  
-   **Mantener la sintaxis actual**  
  
Al seleccionar un modo de conversión en el cuadro **modo** , SSMA aplica la siguiente configuración:  
  
**Modo predeterminado/optimista:** Mantener la sintaxis actual  
  
**Modo completo:** Wrap con la función ISNULL  
  
**Conversión de cadenas vacías**  
Esta configuración especifica cómo se convierten las cadenas vacías. Se pueden establecer las siguientes opciones para esta configuración determinada:  
  
-   **Reemplazar todas las expresiones de cadena por espacio**  
  
-   **Reemplazar constantes de cadena vacías por espacio**  
  
-   Para usar el [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]comportamiento de SQL Azure, seleccione **mantener la sintaxis actual**.  
  
Al seleccionar un modo de conversión en el cuadro **modo** , SSMA aplica la siguiente configuración:  
  
**Modo predeterminado/optimista:** Mantener la sintaxis actual  
  
**Modo completo:** Reemplazar todas las expresiones de cadena por espacio  
  
**CONVERTIR y convertir la conversión de cadena binaria**  
La conversión de valores binarios en números puede devolver valores diferentes en distintas plataformas. Por ejemplo, en procesadores x86, CONVERT (integer, 0x00000100) devuelve 65536 en ASE y 256 en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. ASE también devuelve valores distintos según el orden de los bytes.  
  
Utilice esta opción para controlar cómo SSMA convierte las expresiones de conversión de mayúsculas y minúsculas que contienen valores binarios:  
  
-   Seleccione **conversión simple** para convertir las expresiones sin ninguna advertencia o corrección. Utilice esta opción si sabe que el servidor ASE tiene un orden de bytes que no requiere ningún cambio del valor binario.  
  
-   Seleccione **convertir y corregir** para que SSMA convierta y corrija las expresiones que se [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]van a usar en. Se revertirá el orden de bytes en las constantes literales. Todos los demás valores binarios (como las variables y columnas binarias) se marcarán con errores. Use este valor si sabe que el servidor ASE tiene un orden de bytes que requiere cambios en los valores binarios.  
  
-   Seleccione **convertir y marcar con ADVERTENCIA** para que SSMA convierta y corrija las expresiones y marque todas las expresiones convertidas con comentarios de advertencia.  
  
Al seleccionar un modo de conversión en el cuadro **modo** , SSMA aplica la siguiente configuración:  
  
**Modo predeterminado:** Convertir y marcar con ADVERTENCIA  
  
**Modo optimista:** Conversión simple  
  
**Modo completo:** Convertir y corregir  
  
**SQL dinámico**  
Use esta opción para especificar el tipo de mensaje (ADVERTENCIA o error) que SSMA muestra en el panel de salida o Lista de errores cuando encuentra SQL dinámico en el código de ASE.  
  
-   Si selecciona **convertir y marcar con ADVERTENCIA**, SSMA convertirá el SQL dinámico y marcará las instrucciones con comentarios de advertencia.  
  
-   Si selecciona **Mark with error**, SSMA omitirá la conversión y marcará las instrucciones con comentarios de error.  
  
Al seleccionar un modo de conversión en el cuadro **modo** , SSMA aplica la siguiente configuración:  
  
**Modo predeterminado/optimista:** Convertir y marcar con ADVERTENCIA  
  
**Modo completo:** Marcar con error  
  
**Conversión de comprobación de igualdad**  
En [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]/SQL Azure, si la opción ANSI_NULLS está activada, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]/SQL Azure devuelve Unknown cuando cualquier comparación de igualdad contiene un valor null. Si ANSI_NULLS está desactivado, las comparaciones de igualdad que contienen valores NULL devuelven TRUE cuando la columna comparada y la expresión o dos expresiones son NULL. De forma predeterminada (ANSINULL), las comparaciones de igualdad [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]de Sybase ase se comportan como/SQL Azure con ANSI_NULLS OFF.  
  
-   Si selecciona **conversión simple**, SSMA convertirá el código ase en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]la sintaxis/SQL Azure sin comprobaciones adicionales para los valores NULL. Utilice esta opción si ANSI_NULLS está desactivada en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]/SQL Azure o si desea revisar las comparaciones de igualdad en cada caso.  
  
-   Si selecciona **considerar valores NULL**, SSMA agregará comprobaciones de valores NULL mediante las cláusulas is null e is not null.  
  
Al seleccionar un modo de conversión en el cuadro **modo** , SSMA aplica la siguiente configuración:  
  
**Modo predeterminado/optimista:** Conversión simple  
  
**Modo completo:** Considerar valores NULL  
  
**Cadenas de formato**  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]/SQL Azure ya no admite el argumento *Format_String* en las instrucciones Print y RAISERROR. La variable *Format_String* admite la colocación directa de parámetros reemplazables en la cadena y, a continuación, la sustitución de los parámetros en tiempo de ejecución. En su lugar [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , requiere la cadena completa mediante un literal de cadena o una cadena generada mediante una variable. Para obtener más información, vea el tema " [!INCLUDE[tsql](../../includes/tsql-md.md)]Print ()" [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] en los libros en pantalla de.  
  
Cuando SSMA encuentra un argumento *Format_String* , puede generar un literal de cadena mediante las variables o crear una nueva variable y compilar una cadena utilizando esa variable.  
  
-   Para usar un literal de cadena para las funciones de impresión y RAISERROR, seleccione **crear nueva cadena**.  
  
    En este modo, si una instrucción PRINT o RAISERROR no usa marcadores de posición y variables locales, la instrucción no cambia. Porcentaje de caracteres dobles (%%) se cambian a un solo carácter de porcentaje en literales de cadena de impresión.  
  
    Si una instrucción PRINT o RAISERROR usa marcadores de posición y una o varias variables locales, como en el ejemplo siguiente:  
  
    ```  
    PRINT 'Total: %1!%%', @percent  
    ```  
    SSMA lo convertirá a la siguiente sintaxis:  
  
    ```  
    PRINT 'Total: '+ CAST(@percent AS varchar(max)) + '%'  
    ```  
    Si *Format_String* es una variable, como en la siguiente instrucción:  
  
    ```  
    PRINT @fmt, @arg1, @arg2  
    ```  
    SSMA no puede realizar una conversión de cadena simple y debe crear una nueva variable:  
  
    ```  
    DECLARE @print_format_1 varchar(max)  
    SET @print_format_1  =   
        REPLACE (@fmt, '%%', '%')  
    SET @print_format_1  =   
        REPLACE (@print_format_1, '%1!',   
        CAST (@arg1 AS varchar(max)))  
    SET @print_format_1  =   
        REPLACE (@print_format_1, '%2!',   
        CAST (@arg2 AS varchar(max)))  
    PRINT @print_format_1  
    ```  
    Cuando se usa **crear nuevo** modo de cadena, SSMA supone que [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] la opción CONCAT_NULL_YIELDS_NULL está desactivada. Por lo tanto, SSMA no comprueba los argumentos null.  
  
-   Para que SSMA cree una nueva variable para cada instrucción PRINT y RAISERROR y, a continuación, use esa variable para el valor de cadena, seleccione **crear nueva variable**.  
  
    En este modo, si una instrucción PRINT o RAISERROR no usa marcadores de posición y variables locales, SSMA reemplaza todos los caracteres de porcentaje doble (%%). con un solo carácter de porcentaje para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]cumplir con la sintaxis/SQL Azure.  
  
    Si una instrucción PRINT o RAISERROR usa marcadores de posición y una o varias variables locales, como en el ejemplo siguiente:  
  
    ```  
    PRINT 'Total: %1!%%', @percent  
    ```  
    SSMA lo convertirá a la siguiente sintaxis:  
  
    ```  
    DECLARE @print_format_1 varchar(max)  
    SET @print_format_1 = 'Total: %1!%'  
    SET @print_format_1  =   
        REPLACE (@print_format_1, '%1!',   
        ISNULL(CAST (@percent AS VARCHAR(max)), ''))  
    PRINT @print_format_1  
    ```  
    Si *Format_String* es una variable, como en la siguiente instrucción:  
  
    ```  
    PRINT @fmt, @arg1, @arg2  
    ```  
    SSMA crea una nueva variable como se indica a continuación, comprobando si hay valores NULL en cada argumento:  
  
    ```  
    DECLARE @print_format_1 varchar(max)  
    SET @print_format_1  =   
        REPLACE (@fmt, '%%', '%')  
    SET @print_format_1  =   
        REPLACE (@print_format_1, '%1!',   
        ISNULL(CAST (@arg1 AS varchar(max)),''))  
    SET @print_format_1  =   
        REPLACE (@print_format_1, '%2!',   
        ISNULL(CAST (@arg2 AS varchar(max)),''))  
    PRINT @print_format_1  
    ```  
  
Al seleccionar un modo de conversión en el cuadro **modo** , SSMA aplica la siguiente configuración:  
  
**Modo predeterminado/optimista:** Crear nueva cadena  
  
**Modo completo:** Crear nueva variable  
  
**Insertar un valor explícito en una columna de marca de tiempo**  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]/SQL Azure no admite la inserción de valores explícitos en una columna de marca de tiempo.  
  
-   Para excluir columnas de marca de tiempo de las instrucciones INSERT, seleccione **excluir columna**.  
  
-   Para imprimir un mensaje de error cada vez que una columna TIMESTAMP esté en una instrucción INSERT, seleccione **marcar con error**. En este modo, las instrucciones INSERT no se convertirán y se marcarán con comentarios de error.  
  
Al seleccionar un modo de conversión en el cuadro **modo** , SSMA aplica la siguiente configuración:  
  
**Modo predeterminado/optimista:** Excluir columna  
  
**Modo completo:** Marcar con error  
  
**Almacenar objetos temporales definidos en procedimientos**  
Esta configuración especifica si las definiciones de los objetos temporales que aparecen en los procedimientos deben almacenarse en los metadatos de origen durante la conversión.  
  
-   Seleccione **sí** para almacenar en los metadatos.  
  
-   Seleccione **no** si no es necesario almacenar los objetos.  
  
**Modo predeterminado/optimista:** ?  
  
**Modo completo:** No  
  
**Conversión de tabla de proxy**  
Especifica si las tablas de proxy de ASE [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]se convierten en tablas de o SQL Azure, o no se convierten y el código se marca con comentarios de error.  
  
-   Seleccione **convertir** para convertir las tablas de proxy en tablas normales.  
  
-   Seleccione **marcar con error** para marcar simplemente el código de la tabla de proxy con los comentarios de error.  
  
Al seleccionar un modo de conversión en el cuadro **modo** , SSMA aplica la siguiente configuración:  
  
**Modo predeterminado/optimista/completo:** Marcar con error  
  
**Número de mensaje base de RAISERROR**  
Los mensajes de usuario de ASE se almacenan en cada base de datos. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]los mensajes de usuario se almacenan de forma centralizada y se ponen a disposición a través de la vista de catálogo **Sys. Messages** . Además, los mensajes de usuario de ASE empiezan en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 20000, pero los mensajes de error se inician en 50001.  
  
Esta configuración especifica el número que se va a agregar al número de mensaje de usuario de ASE [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para convertirlo en un mensaje de usuario. Si su [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tiene mensajes de usuario en la vista de catálogo **Sys. Messages** , es posible que tenga que cambiar este número a un valor superior. Esto es así para que los números de mensaje convertidos no entren en conflicto con los números de mensaje existentes.  
  
Tenga en cuenta lo siguiente:  
  
-   Los mensajes ASE en el intervalo 17000-19999 son de la tabla del sistema sysmessages y no se convierten.  
  
-   Si el número de mensaje al que se hace referencia en la instrucción RAISERROR es una constante, SSMA agregará el número de mensaje base a la constante para determinar el nuevo número de mensaje de usuario.  
  
-   Si el número de mensaje al que se hace referencia es una variable o una expresión, SSMA creará una variable local intermedia.  
  
-   En el modo optimista, SSMA supone que [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] la opción CONCAT_NULL_YIELDS_NULL está desactivada y no realiza ninguna comprobación para los argumentos nulos.  
  
-   En el modo completo, SSMA comprueba los argumentos null.  
  
-   No se convierte RAISERROR con la *lista* datoserror.  
  
Al seleccionar un modo de conversión en el cuadro **modo** , SSMA aplica la siguiente configuración:  
  
**Modo predeterminado/optimista/completo:** 30001  
  
**Objetos del sistema**  
Use esta opción para especificar el tipo de mensaje (ADVERTENCIA o error) que SSMA muestra en el panel de salida o Lista de errores cuando encuentra el uso de objetos del sistema ASE.  
  
-   Si selecciona **convertir y marcar con ADVERTENCIA**, SSMA convertirá las referencias a los objetos del sistema y marcará las instrucciones con comentarios de advertencia.  
  
-   Si selecciona **Mark with error**, SSMA no convertirá las referencias a objetos de sistema y marcará las instrucciones con comentarios de error.  
  
Al seleccionar un modo de conversión en el cuadro **modo** , SSMA aplica la siguiente configuración:  
  
**Modo predeterminado/optimista:** Convertir y marcar con ADVERTENCIA  
  
**Modo completo:** Marcar con error  
  
**Identificadores sin resolver**  
Use esta opción para especificar el tipo de mensaje (ADVERTENCIA o error) que SSMA muestra en el panel de salida o Lista de errores cuando no puede resolver un identificador.  
  
-   Si selecciona **convertir y marcar con ADVERTENCIA**, SSMA intentará convertir las referencias a identificadores sin resolver y marcará las instrucciones con comentarios de advertencia.  
  
-   Si selecciona **Mark with error**, SSMA no convertirá las referencias a identificadores sin resolver y marcará las instrucciones con comentarios de error.  
  
Al seleccionar un modo de conversión en el cuadro **modo** , SSMA aplica la siguiente configuración:  
  
**Modo predeterminado/optimista:** Convertir y marcar con ADVERTENCIA  
  
**Modo completo:** Marcar con error  
  
## <a name="system-function-options"></a>Opciones de función del sistema  
**CHARINDEX, función**  
En ASE, CHARINDEX devuelve NULL solo si todas las expresiones de entrada son NULL. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]/SQL Azure devolverá NULL si alguna expresión de entrada es NULL.  
  
-   Para usar el comportamiento de ASE, seleccione **reemplazar función**. Todas las llamadas a la función CHARINDEX se sustituyen por una llamada a CHARINDEX_VARCHAR o CHARINDEX_NVARCHAR función definida por el usuario según el tipo de parámetros pasados (creados en la base de datos de usuario en el 2SS del nombre de esquema) para emular el comportamiento de Sybase ASE.  
  
-   Para usar el [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]comportamiento de SQL Azure, seleccione **mantener la sintaxis actual**.  
  
Al seleccionar un modo de conversión en el cuadro **modo** , SSMA aplica la siguiente configuración:  
  
**Modo predeterminado/optimista:** Mantener la sintaxis actual  
  
**Modo completo:** Replace (función)  
  
**DATALENGTH, función**  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]/SQL Azure y ASE difieren en el valor devuelto por la función DATALENGTH cuando el valor es un espacio único. En este caso, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]/SQL Azure devuelve 0 y ase devuelve 1.  
  
-   Para usar el comportamiento de ASE, seleccione **reemplazar función**. Todas las llamadas a la función DATALENGTH se sustituyen por la expresión CASE para emular el comportamiento de Sybase ASE.  
  
-   Para usar el comportamiento [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] predeterminado/SQL Azure, seleccione **mantener la sintaxis actual**.  
  
Al seleccionar un modo de conversión en el cuadro **modo** , SSMA aplica la siguiente configuración:  
  
**Modo predeterminado/optimista:** Mantener la sintaxis actual  
  
**Modo completo:** Replace (función)  
  
**INDEX_COL, función**  
ASE admite un argumento *USER_ID* opcional para la función INDEX_COL; sin embargo [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)],/SQL Azure no admite este argumento. Si usa el argumento *USER_ID* , esta función no se puede convertir en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]sintaxis/SQL Azure.  
  
-   Para usar el comportamiento de ASE, seleccione **convertir función**. Si el código contiene el argumento *USER_ID* , SSMA mostrará un error.  
  
-   Para mostrar un mensaje de error cada vez que se encuentra INDEX_COL, seleccione **marcar con error**. SSMA no convertirá las referencias a la función y marcará la instrucción con comentarios de error.  
  
**Modo predeterminado/optimista/completo:** Marcar con error  
  
**INDEX_COLORDER función)**  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]/SQL Azure no tiene una función del sistema INDEX_COLORDER.  
  
-   Para usar el comportamiento de ASE, seleccione **convertir función**. Todas las llamadas a la función INDEX_COLORDER se sustituyen por una llamada a una función definida por el usuario con el mismo nombre INDEX_COLORDER (creada en la base de datos de usuario con el nombre de esquema 2SS '), que emula el comportamiento de Sybase ASE.  
  
-   Para imprimir un mensaje de error cada vez que se encuentre INDEX_COLORDER, seleccione **marcar con error**. SSMA no convertirá las referencias a la función y marcará la instrucción con comentarios de error.  
  
Al seleccionar un modo de conversión en el cuadro **modo** , SSMA aplica la siguiente configuración:  
  
**Modo predeterminado/optimista/completo:** Marcar con error  
  
**Funciones izquierda y derecha**  
Las funciones izquierda y derecha de Sybase se comportan de manera diferente para el parámetro de longitud negativa.  
  
-   Para usar el comportamiento de ASE, seleccione **reemplazar función**. A continuación, el parámetro de longitud se reemplaza por una expresión CASE que devolvería null para un valor negativo.  
  
-   Para usar el comportamiento de SQL Server, seleccione **mantener la sintaxis actual** .  
  
Al seleccionar un modo de conversión en el cuadro **modo** , SSMA aplica la siguiente configuración:  
  
**Modo predeterminado/optimista:** Mantener la sintaxis actual  
  
**Modo completo:** Replace (función)  
  
> [!NOTE]  
> Si el parámetro de longitud es un valor literal y no una expresión compleja, el valor de longitud siempre se reemplaza por null independientemente de la configuración del proyecto.  
  
**NEXT_IDENTITY función)**  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]/SQL Azure no tiene una función del sistema NEXT_IDENTITY.  
  
-   Para usar el comportamiento de ASE, seleccione **convertir función**. Todas las llamadas a la función NEXT_IDENTITY se sustituyen por Expression (IDENT_CURRENT (valor de parámetro) + IDENT_INCR (valor de parámetro) que emula el comportamiento de Sybase ASE.  
  
-   Para imprimir un mensaje de error cada vez que se encuentre NEXT_IDENTITY, seleccione **marcar con error**. SSMA no convertirá las referencias a la función y marcará la instrucción con comentarios de error.  
  
Al seleccionar un modo de conversión en el cuadro **modo** , SSMA aplica la siguiente configuración:  
  
**Modo predeterminado/optimista/completo:** Marcar con error  
  
**PATINDEX, función**  
Especifica si se debe convertir la función PATINDEX para que coincida con el comportamiento de Sybase ASE. El punto es que Sybase recorta los espacios en blanco finales en un patrón de búsqueda. La solución consiste en convertir una conversión de expresión de valor en un tipo de datos de longitud fija con una precisión máxima y aplicar la función RTrim al patrón de búsqueda.  
  
-   Para usar el comportamiento de ASE, seleccione **usar**.  
  
-   Para usar el comportamiento [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]predeterminado/SQL Azure, seleccione **no usar**.  
  
Al seleccionar un modo de conversión en el cuadro **modo** , SSMA aplica la siguiente configuración:  
  
**Modo predeterminado/optimista:** No usar  
  
**Modo completo:** Realice  
  
**REPLICATE, función**  
La función REPLICAte repite una cadena el número especificado de veces. En ASE, si especifica que se repita la cadena cero veces, el resultado es NULL. En [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]/SQL Azure, el resultado es una cadena vacía.  
  
-   Para usar el comportamiento de ASE, seleccione **reemplazar función**. Todas las llamadas a la función REPLICAte se sustituyen por una llamada a REPLICATE_VARCHAR o REPLICATE_NVARCHAR función definida por el usuario según el tipo de parámetros pasados (creados en la base de datos de usuario en el 2SS del nombre de esquema) para emular el comportamiento de Sybase ASE.  
  
-   Para usar el comportamiento [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]predeterminado/SQL Azure, seleccione **reemplazar función**.  
  
Al seleccionar un modo de conversión en el cuadro **modo** , SSMA aplica la siguiente configuración:  
  
**Modo predeterminado/optimista/modo completo:** Replace (función)  
  
**TRIM (LTRIM, RTRIM) (función)**  
Esta configuración especifica si se deben reemplazar las llamadas a las funciones Trim (LTRIM, RTRIM) con las funciones de sintaxis equivalentes de Sybase ASE o para mantener la sintaxis actual. Las siguientes opciones están presentes para esta configuración determinada:  
  
-   **Replace (función)**  
  
-   **Mantener la sintaxis actual**  
  
Al seleccionar un modo de conversión en el cuadro **modo** , SSMA aplica la siguiente configuración:  
  
**Modo predeterminado/optimista/modo completo:** Replace (función)  
  
**SUBSTRING, función**  
En ASE, la función `SUBSTRING(expression, start, length)` devuelve NULL si se especifica un valor de inicio mayor que el número de caracteres de la expresión, o si la longitud es igual a cero. En [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]/SQL Azure, la expresión equivalente devuelve una cadena vacía.  
  
-   Para usar el comportamiento de ASE, seleccione **reemplazar función**. Todas las llamadas a la función Substring se sustituyen por una llamada a SUBSTRING_VARCHAR o SUBSTRING_NVARCHAR o SUBSTRING_VARBINARY función definida por el usuario según el tipo de parámetros pasados (creados en la base de datos de usuario en el nombre de esquema 2SS ') para emular el comportamiento de Sybase ASE.  
  
-   Para usar el [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] comportamiento de SQL Azure, seleccione **mantener la sintaxis actual**.  
  
Al seleccionar un modo de conversión en el cuadro **modo** , SSMA aplica la siguiente configuración:  
  
**Modo predeterminado/optimista:** Mantener la sintaxis actual  
  
**Modo completo:** Replace (función)  
  
## <a name="tables"></a>TABLES  
**Agregar clave principal**  
Crea una nueva clave principal en la [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tabla o SQL Azure si una tabla de Access no tiene una clave principal o un índice único.  
  
-   **Modo predeterminado**: false  
  
-   **Modo optimista**: false  
  
-   **Modo completo**: true  
  
> [!NOTE]  
> Cuando se conecta a SQL Azure, es true de forma predeterminada.  
  
## <a name="see-also"></a>Consulte también  
[Referencia de la interfaz de usuario &#40;SybaseToSQL&#41;](../../ssma/sybase/user-interface-reference-sybasetosql.md)  
  
