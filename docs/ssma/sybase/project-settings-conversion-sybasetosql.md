---
title: Configuración (conversión) (SybaseToSQL) del proyecto | Documentos de Microsoft
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.service: ''
ms.component: ssma-sybase
ms.reviewer: ''
ms.suite: sql
ms.technology:
- sql-ssma
ms.tgt_pltfrm: ''
ms.topic: article
applies_to:
- Azure SQL Database
- SQL Server
ms.assetid: eeb80fa5-f530-4f21-beee-25f5a4b8ace6
caps.latest.revision: 8
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: ffffc3badb8d65d5809e293e0c1ffb526409e4a9
ms.sourcegitcommit: a85a46312acf8b5a59a8a900310cf088369c4150
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/26/2018
---
# <a name="project-settings-conversion-sybasetosql"></a>Configuración del proyecto (conversión) (SybaseToSQL)
La página de conversión de la **configuración del proyecto** cuadro de diálogo contiene la configuración que permiten personalizar cómo SSMA convierte la sintaxis de Sybase Adaptive Server Enterprise (ASE) a [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] o la sintaxis de SQL Azure.  
  
El panel de conversión está disponible en la **configuración del proyecto** y **configuración de proyecto predeterminada** cuadros de diálogo:  
  
-   Si desea especificar la configuración para todos los proyectos SSMA, en la **herramientas** menú, seleccione **la configuración predeterminada del proyecto**, haga clic en **General** en la parte inferior del panel izquierdo y, a continuación, haga clic en **conversión**.  
  
-   Para especificar la configuración para el proyecto actual, en la **herramientas** menú, seleccione **configuración del proyecto**, haga clic en **General** en la parte inferior del panel izquierdo y, a continuación, haga clic en **conversión**.  
  
## <a name="miscellaneous-options"></a>Otras opciones  
**@@ERROR**  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]O SQL Azure y ASE usan códigos de error diferentes.  
  
Utilice esta opción para especificar el tipo de mensaje (advertencia o Error) que SSMA se muestra en el panel de resultados o la lista de errores cuando encuentra una referencia a **@@ERROR**  en el código de ASE.  
  
-   Si selecciona **convertir y marcar con una advertencia**, SSMA convertirá las instrucciones y márquelos con comentarios de advertencia.  
  
-   Si selecciona **marca con el error**, SSMA omitirá la conversión y marcar las instrucciones con comentarios de error.  
  
Al seleccionar un modo de conversión en el **modo** cuadro, SSMA aplica la siguiente configuración:  
  
**El modo predeterminado/Optimistic:** convertir y marcar con advertencia  
  
**Modo completo:** marca con error  
  
**Conversión de operador LIKE**  
Especifica si se deben convertir como operandos para emular el comportamiento de Sybase ASE. El punto es que Sybase recorta los espacios en blanco en un patrón de like. La solución consiste en realizar una conversión de expresión de la derecha en un tipo de datos de longitud fija con una precisión máxima.  
  
-   Seleccione **conversión Simple** para convertir las expresiones sin ninguna corrección.  
  
-   Para utilizar la instrucción select de comportamiento de ASE **convierte con longitud fija.**  
  
Cuando se selecciona un modo de conversión en el cuadro modo, SSMA aplica la siguiente configuración:  
  
**El modo predeterminado/Optimistic**: conversión Simple  
  
**Modo completo**: convierte con longitud fija  
  
**CONVERTIR O CONVERTIR LAS CADENAS VACÍAS PARA LOS TIPOS NUMÉRICOS**  
Especifica cómo controlar las cadenas en blanco o vacías dentro de las expresiones de CONVERT o CAST con un tipo numérico como argumento de tipo de datos. Las siguientes opciones están disponibles para esta configuración:  
  
-   Seleccione **conversión Simple** para convertir las expresiones sin ninguna corrección.  
  
-   Si **cadena vacía como cero numérico** se selecciona, el parámetro de cadena {s} se sustituirán por ltrim(rtrim({s})) mayúsculas cuando "", a continuación, 0 else {s} expresión de extremo  
  
Cuando se selecciona un modo de conversión en el cuadro modo, SSMA aplica la siguiente configuración:  
  
**El modo predeterminado/Optimistic**: conversión Simple  
  
**Modo completo**: cadena vacía como cero numérico  
  
**Concatenación es null**  
Esta configuración especifica cómo convertir la concatenación de cadenas con valor NULL. Las siguientes opciones se pueden establecer para esta configuración concreta:  
  
-   **Ajustar a la función ISNULL:** si se establece esta opción, se ajustará cada 'string_expression' en la concatenación no sea constante con ISNULL(string_expression) y valores NULL se sustituirán por una cadena vacía.  
  
-   **Mantener la sintaxis actual**  
  
Al seleccionar un modo de conversión en el **modo** cuadro, SSMA aplica la siguiente configuración:  
  
**El modo predeterminado/Optimistic:** mantener la sintaxis actual  
  
**Modo completo:** encapsulan con ISNULL, función  
  
**Conversión de cadenas vacías**  
Esta configuración especifica cómo convertir las cadenas vacías. Las siguientes opciones se pueden establecer para esta configuración concreta:  
  
-   **Reemplace todas las expresiones de cadena con espacio**  
  
-   **Reemplace las constantes de cadena vacía con espacio**  
  
-   Para usar el [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]/ comportamiento de SQL Azure, seleccione **mantener la sintaxis actual**.  
  
Al seleccionar un modo de conversión en el **modo** cuadro, SSMA aplica la siguiente configuración:  
  
**El modo predeterminado/Optimistic:** mantener la sintaxis actual  
  
**Modo completo:** reemplace todas las expresiones de cadena con espacio  
  
**Conversión de cadena binaria de conversión y conversión de tipos**  
La conversión de valores binarios en números puede devolver valores diferentes en distintas plataformas. Por ejemplo, en x86 procesadores, CONVERT (entero, 0 x 00000100) devuelve 65536 en ASE y 256 en [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]. ASE también devuelve valores diferentes según el orden de bytes.  
  
Use esta opción para controlar cómo convertir SSMA convierte y expresiones CASE que contienen valores binarios:  
  
-   Seleccione **conversión Simple** para convertir las expresiones sin advertencias ni corrección. Use esta opción si sabe que el servidor de ASE tiene un orden de bytes que no se requiere ningún cambio del valor binario.  
  
-   Seleccione **convertir y corregir** tener SSMA convertir y corregir las expresiones para su uso en [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]. Se invertirá el orden de bytes en constantes literales. Todos los demás valores binarios (como binarias variables y columnas) se marcarán con errores. Use este valor si sabe que el servidor de ASE tiene un orden de bytes que requiere cambios en los valores binarios.  
  
-   Seleccione **convertir y marcar con una advertencia** tener SSMA convertir y corrija las expresiones y marque todo convierten expresiones con comentarios de advertencia.  
  
Al seleccionar un modo de conversión en el **modo** cuadro, SSMA aplica la siguiente configuración:  
  
**Modo predeterminado:** convertir y marcar con advertencia  
  
**El modo optimista:** conversión Simple  
  
**Modo completo:** convertir y corregir  
  
**SQL dinámico**  
Utilice esta opción para especificar el tipo de mensaje (advertencia o Error) que SSMA se muestra en el panel de resultados o la lista de errores cuando encuentra SQL dinámico en el código de ASE.  
  
-   Si selecciona **convertir y marcar con una advertencia**, SSMA convertirá el SQL dinámico y marcar las instrucciones con comentarios de advertencia.  
  
-   Si selecciona **marca con el error**, SSMA omitirá la conversión y marcar las instrucciones con comentarios de error.  
  
Al seleccionar un modo de conversión en el **modo** cuadro, SSMA aplica la siguiente configuración:  
  
**El modo predeterminado/Optimistic:** convertir y marcar con advertencia  
  
**Modo completo:** marca con error  
  
**Conversión de comprobación de igualdad**  
En [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]/ SQL Azure, si el valor de ANSI_NULLS es on, [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]/ SQL Azure devuelve UNKNOWN cuando las comparaciones de igualdad contienen un valor null. Si ANSI_NULLS es off, las comparaciones de igualdad que contienen valores null devuelven true cuando la columna comparada y expresión o dos expresiones son null. Por igualdad de valor predeterminado (ANSINULL OFF) Sybase ASE las comparaciones se comportan como [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]/ SQL Azure con ANSI_NULLS OFF.  
  
-   Si selecciona **conversión Simple**, SSMA convertirá el código ASE a [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]/ la sintaxis de SQL Azure sin comprobaciones adicionales para los valores null. Utilice esta opción si ANSI_NULLS está desactivada en [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]/ SQL Azure o si desea revisar las comparaciones de igualdad por caso.  
  
-   Si selecciona **valores NULL considere la posibilidad de**, SSMA agregará comprueba si hay valores null mediante el uso de las cláusulas IS NULL e IS NOT NULL.  
  
Al seleccionar un modo de conversión en el **modo** cuadro, SSMA aplica la siguiente configuración:  
  
**El modo predeterminado/Optimistic:** conversión Simple  
  
**Modo completo:** considere la posibilidad de NULL valores  
  
**Cadenas de formato**  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]O SQL Azure ya no admite la *format_string* argumento en las instrucciones PRINT y RAISERROR. El *format_string* variable admite colocar parámetros reemplazables directamente en la cadena y, a continuación, reemplazando los parámetros en tiempo de ejecución. En su lugar, [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] requiere que la cadena completa con un literal de cadena o una cadena que se compila mediante una variable. Para obtener más información, consulte la "impresión ([!INCLUDE[tsql](../../includes/tsql_md.md)])" tema en [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] libros en pantalla.  
  
Cuando se encuentra SSMA un *format_string* argumento, puede generar una cadena literal usando las variables o crear una nueva variable y generar una cadena mediante el uso de esa variable.  
  
-   Para utilizar un literal de cadena para las funciones de impresión y RAISERROR, seleccione **crear nueva cadena**.  
  
    En este modo, si una instrucción PRINT o RAISERROR no usa marcadores de posición y las variables locales, no se modifica la instrucción. Caracteres dobles de porcentaje (%) se cambian a un único carácter de porcentaje % en literales de cadena de impresión.  
  
    Si una instrucción PRINT o RAISERROR usa marcadores de posición y uno o más variables locales, como se muestra en el ejemplo siguiente:  
  
    ```  
    PRINT 'Total: %1!%%', @percent  
    ```  
    SSMA lo convertirá a la siguiente sintaxis:  
  
    ```  
    PRINT 'Total: '+ CAST(@percent AS varchar(max)) + '%'  
    ```  
    Si *format_string* es una variable, como en la siguiente instrucción:  
  
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
    Cuando usa **crear nueva cadena** modo, SSMA se da por supuesto que el [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] opción CONCAT_NULL_YIELDS_NULL es OFF. Por lo tanto, SSMA no comprueba si hay argumentos null.  
  
-   Para crear una nueva variable para cada instrucción PRINT y RAISERROR y, a continuación, usar esa variable para el valor de cadena SSMA, seleccione **crear nueva variable**.  
  
    En este modo, si una instrucción PRINT o RAISERROR no usa marcadores de posición y las variables locales, SSMA reemplaza todos los caracteres de porcentaje dobles (%) con caracteres de porcentaje individuales para cumplir con [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]/ sintaxis de SQL Azure.  
  
    Si una instrucción PRINT o RAISERROR usa marcadores de posición y uno o más variables locales, como se muestra en el ejemplo siguiente:  
  
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
    Si *format_string* es una variable, como en la siguiente instrucción:  
  
    ```  
    PRINT @fmt, @arg1, @arg2  
    ```  
    SSMA crea una nueva variable como sigue, comprobación de valores null en cada argumento:  
  
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
  
Al seleccionar un modo de conversión en el **modo** cuadro, SSMA aplica la siguiente configuración:  
  
**El modo predeterminado/Optimistic:** crear nueva cadena  
  
**Modo completo:** crear nueva variable  
  
**Insertar un valor explícito en una columna de marca de tiempo**  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]O SQL Azure no admite insertar valores explícitos en una columna de marca de tiempo.  
  
-   Para excluir columnas de marca de tiempo de las instrucciones INSERT, seleccione **columna excluir**.  
  
-   Para imprimir un mensaje de error cada vez que una columna de marca de tiempo se encuentra en una instrucción INSERT, seleccione **marca con el error**. En este modo, las instrucciones INSERT no se convertirán y se marcarán con comentarios de error.  
  
Al seleccionar un modo de conversión en el **modo** cuadro, SSMA aplica la siguiente configuración:  
  
**El modo predeterminado/Optimistic:** columna excluir  
  
**Modo completo:** marca con error  
  
**Almacenar objetos temporales definidos en los procedimientos**  
Esta configuración especifica si las definiciones de objetos temporales que aparecen en los procedimientos se deben almacenar en los metadatos de origen durante la conversión.  
  
-   Seleccione **Sí** para almacenar en los metadatos.  
  
-   Seleccione **n** si no es necesario almacenar los objetos.  
  
**Modo predeterminado/optimista:** sí  
  
**Modo completo:** n  
  
**Conversión de la tabla de proxy**  
Especifica si las tablas de proxy de ASE se convierten en [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]/ no convertir tablas de SQL Azure, o se y el código está marcado con comentarios de error.  
  
-   Seleccione **convertir** para convertir tablas de proxy en las tablas normales.  
  
-   Seleccione **marca con el error** simplemente marcar el código de la tabla de proxy con comentarios de error.  
  
Al seleccionar un modo de conversión en el **modo** cuadro, SSMA aplica la siguiente configuración:  
  
**El modo predeterminado/Optimistic/completo:** marca con error  
  
**Número de mensajes de base de RAISERROR**  
Mensajes de usuario de ASE se almacenan en cada base de datos. [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] mensajes de usuario centralmente se almacenan y están disponibles a través de la **sys.messages** vista de catálogo. Además se inician los mensajes de usuario ASE al 20000, pero [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] mensajes de error de inician en 50001.  
  
Esta configuración especifica el número para agregar el número de mensajes de usuario ASE para convertirlo en un [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] mensaje de usuario. Si su [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] tiene mensajes de usuario en el **sys.messages** vista de catálogo, es posible que deba cambiar este número a un valor superior. Esto es por lo que los números de mensaje convertido no entren en conflicto con los números de mensajes existente.  
  
Observe lo siguiente:  
  
-   Mensajes ASE en el intervalo 17000 a 19999 provienen de la tabla del sistema sysmessages y no se convierten.  
  
-   Si el número de mensajes que se hace referencia en la instrucción RAISERROR es una constante, SSMA agregará el número de mensajes de base a la constante para determinar el número de mensajes de usuario nuevo.  
  
-   Si el número de mensajes que se hace referencia es una variable o expresión, SSMA creará una variable local intermedia.  
  
-   En el modo optimista, SSMA da por supuesto que el [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] opción CONCAT_NULL_YIELDS_NULL está desactivada y no se realiza ninguna comprobación para argumentos que son null.  
  
-   En el modo completo, SSMA comprueba si hay argumentos null.  
  
-   RAISERROR con ERRORDATA *lista* no se convierte.  
  
Al seleccionar un modo de conversión en el **modo** cuadro, SSMA aplica la siguiente configuración:  
  
**El modo predeterminado/optimista/completo:** 30001  
  
**Objetos del sistema**  
Utilice esta opción para especificar el tipo de mensaje (advertencia o Error) que SSMA se muestra en el panel de resultados o la lista de errores cuando encuentra el uso de objetos del sistema ASE.  
  
-   Si selecciona **convertir y marcar con una advertencia**, SSMA convertirá las referencias a objetos del sistema y se marcarán instrucciones con comentarios de advertencia.  
  
-   Si selecciona **marca con el error**, SSMA no convertirá las referencias a objetos de sistemas y marcará instrucciones con comentarios de error.  
  
Al seleccionar un modo de conversión en el **modo** cuadro, SSMA aplica la siguiente configuración:  
  
**El modo predeterminado/Optimistic:** convertir y marcar con advertencia  
  
**Modo completo:** marca con error  
  
**Identificadores sin resolver**  
Utilice esta opción para especificar el tipo de mensaje (advertencia o Error) que SSMA se muestra en el panel de resultados o la lista de errores cuando no puede resolver un identificador.  
  
-   Si selecciona **convertir y marcar con una advertencia**, SSMA intentará convertir las referencias a identificadores sin resolver y marcará instrucciones con comentarios de advertencia.  
  
-   Si selecciona **marca con el error**, SSMA no convertirá las referencias a identificadores sin resolver y marcará instrucciones con comentarios de error.  
  
Al seleccionar un modo de conversión en el **modo** cuadro, SSMA aplica la siguiente configuración:  
  
**El modo predeterminado/Optimistic:** convertir y marcar con advertencia  
  
**Modo completo:** marca con error  
  
## <a name="system-function-options"></a>Opciones de función del sistema  
**CHARINDEX, función**  
En ASE, CHARINDEX devuelve NULL solo si todas las expresiones de entrada son NULL. [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]O SQL Azure devolverá NULL si cualquier expresión de entrada es NULL.  
  
-   Para utilizar el comportamiento de ASE, seleccione **Replace, función**. Todas las llamadas a función CHARINDEX se sustituye por una llamada a CHARINDEX_VARCHAR o CHARINDEX_NVARCHAR una función definida por el usuario según el tipo de parámetros pasados (creado en la base de datos de usuario en el nombre de esquema 's2ss') para emular el comportamiento de Sybase ASE.  
  
-   Para usar el [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]/ comportamiento de SQL Azure, seleccione **mantener la sintaxis actual**.  
  
Al seleccionar un modo de conversión en el **modo** cuadro, SSMA aplica la siguiente configuración:  
  
**El modo predeterminado/Optimistic:** mantener la sintaxis actual  
  
**Modo completo:** Replace, función  
  
**Función DATALENGTH**  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] O SQL Azure y ASE difieren en el valor devuelto por la función DATALENGTH cuando el valor es un único espacio. En este caso, [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]/ SQL Azure devuelve 0 y ASE devuelve 1.  
  
-   Para utilizar el comportamiento de ASE, seleccione **Replace, función**. Todas las llamadas a función DATALENGTH se sustituirán por la expresión CASE para emular el comportamiento de Sybase ASE.  
  
-   Use el valor predeterminado [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] / comportamiento de SQL Azure, seleccione **mantener la sintaxis actual**.  
  
Al seleccionar un modo de conversión en el **modo** cuadro, SSMA aplica la siguiente configuración:  
  
**El modo predeterminado/Optimistic:** mantener la sintaxis actual  
  
**Modo completo:** Replace, función  
  
**Index_col, función**  
Admite una función opcional ASE *user_id* argumento pasado a la función INDEX_COL; sin embargo, [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]o SQL Azure no admite este argumento. Si usas el *user_id* argumento, esta función no se puede convertir a [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]/ sintaxis de SQL Azure.  
  
-   Para utilizar el comportamiento de ASE, seleccione **Convert, función**. Si el código contiene la *user_id* argumento, SSMA mostrará un error.  
  
-   Para mostrar un mensaje de error cada vez que se encuentre ese INDEX_COL, seleccione **marca con el error**. SSMA no convertirá referencias a la función y marcará la instrucción con comentarios de error.  
  
**El modo predeterminado/Optimistic/completo:** marca con error  
  
**Función INDEX_COLORDER**  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]O SQL Azure no tiene una función de sistema INDEX_COLORDER.  
  
-   Para utilizar el comportamiento de ASE, seleccione **Convert, función**. Todas las llamadas a función INDEX_COLORDER se sustituye con una llamada a una función definida por el usuario con el mismo nombre INDEX_COLORDER (creado en la base de datos de usuario en el nombre de esquema 's2ss') que emula el comportamiento de Sybase ASE.  
  
-   Para imprimir un mensaje de error cada vez que se encuentre ese INDEX_COLORDER, seleccione **marca con el error**. SSMA no convertirá referencias a la función y marcará la instrucción con comentarios de error.  
  
Al seleccionar un modo de conversión en el **modo** cuadro, SSMA aplica la siguiente configuración:  
  
**El modo predeterminado/Optimistic/completo:** marca con error  
  
**Las funciones LEFT y RIGHT**  
Izquierda y derecha funciones en Sybase comportan de forma diferente para el parámetro de longitud negativa.  
  
-   Para utilizar el comportamiento de ASE, seleccione **función Replace**. El parámetro de longitud, a continuación, se sustituye por la expresión CASE que devolvería null para el valor negativo.  
  
-   Para utilizar el comportamiento de SQL Server, seleccione **mantener la sintaxis actual**  
  
Al seleccionar un modo de conversión en el **modo** cuadro, SSMA aplica la siguiente configuración:  
  
**El modo predeterminado/Optimistic:** mantener la sintaxis actual  
  
**Modo completo:** Replace, función  
  
> [!NOTE]  
> Si el parámetro de longitud es un valor literal y no una expresión compleja, el valor de longitud siempre se reemplaza con el valor null con independencia de la configuración del proyecto.  
  
**Función NEXT_IDENTITY**  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]O SQL Azure no tiene una función de sistema NEXT_IDENTITY.  
  
-   Para utilizar el comportamiento de ASE, seleccione **función Convert para convertir**. Todas las llamadas a función NEXT_IDENTITY se sustituye por la expresión (IDENT_CURRENT(parameter Value) + IDENT_INCR(parameter Value) que emula el comportamiento de Sybase ASE.  
  
-   Para imprimir un mensaje de error cada vez que se encuentre ese NEXT_IDENTITY, seleccione **marca con el error**. SSMA no convertirá referencias a la función y marcará la instrucción con comentarios de error.  
  
Al seleccionar un modo de conversión en el **modo** cuadro, SSMA aplica la siguiente configuración:  
  
**El modo predeterminado/Optimistic/completo:** marca con error  
  
**Función PATINDEX**  
Especifica si se debe convertir la función PATINDEX para emular el comportamiento de Sybase ASE. El punto es que Sybase recorta los espacios en blanco en un patrón de búsqueda. La solución consiste en realizar una conversión de expresión de valor con una longitud fija de tipo con una precisión máxima de datos y aplican la función rtrim para buscar el patrón.  
  
-   Para utilizar la instrucción select de comportamiento de ASE **usar**.  
  
-   Use el valor predeterminado [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]/ comportamiento de SQL Azure, seleccione **no utilice**.  
  
Al seleccionar un modo de conversión en el **modo** cuadro, SSMA aplica la siguiente configuración:  
  
**El modo predeterminado/Optimistic:** no usar  
  
**Modo completo:** uso  
  
**REPLICATE, función**  
La función REPLICATE repite una cadena el número de veces especificado. En ASE, si se especifica para repetir la cadena de cero veces, el resultado es null. En [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]/ SQL Azure, el resultado es una cadena vacía.  
  
-   Para utilizar el comportamiento de ASE, seleccione **Replace, función**. Todas las llamadas a función REPLICATE se sustituye por una llamada a REPLICATE_VARCHAR o REPLICATE_NVARCHAR una función definida por el usuario según el tipo de parámetros pasados (creado en la base de datos de usuario en el nombre de esquema 's2ss') para emular el comportamiento de Sybase ASE.  
  
-   Use el valor predeterminado [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]/ comportamiento de SQL Azure, seleccione **función Replace**.  
  
Al seleccionar un modo de conversión en el **modo** cuadro, SSMA aplica la siguiente configuración:  
  
**Modo de modo/completo predeterminado/Optimistic:** Replace, función  
  
**Función TRIM (LTRIM, RTRIM)**  
Esta configuración especifica si se va a reemplazar las llamadas a funciones de recorte (LTRIM, RTRIM) con las funciones de sintaxis de Sybase ASE equivalentes o para mantener la sintaxis actual. Las siguientes opciones están disponibles para esta configuración concreta:  
  
-   **Replace, función**  
  
-   **Mantener la sintaxis actual**  
  
Al seleccionar un modo de conversión en el **modo** cuadro, SSMA aplica la siguiente configuración:  
  
**Modo de modo/completo predeterminado/Optimistic:** Replace, función  
  
**SUBSTRING, función**  
En ASE, la función `SUBSTRING(expression, start, length)` devuelve NULL si no se especifica un valor de inicio mayor que el número de caracteres en la expresión, o si la longitud es igual a cero. En [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]/ SQL Azure, la expresión equivalente devuelve una cadena vacía.  
  
-   Para utilizar el comportamiento de ASE, seleccione **Replace, función**. Todas las llamadas a función SUBSTRING se sustituye por una llamada a SUBSTRING_VARCHAR o SUBSTRING_NVARCHAR o SUBSTRING_VARBINARY una función definida por el usuario según el tipo de parámetros pasados (creado en la base de datos de usuario en el nombre de esquema 's2ss') para emular el comportamiento de Sybase ASE.  
  
-   Para usar el [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] / comportamiento de SQL Azure, seleccione **mantener la sintaxis actual**.  
  
Al seleccionar un modo de conversión en el **modo** cuadro, SSMA aplica la siguiente configuración:  
  
**El modo predeterminado/Optimistic:** mantener la sintaxis actual  
  
**Modo completo:** Replace, función  
  
## <a name="tables"></a>TABLES  
**Agregar la clave principal**  
Crea una nueva clave principal en la [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] o una tabla de SQL Azure, si una tabla de Access no tiene clave principal o índice único.  
  
-   **Modo predeterminado**: False  
  
-   **Modo optimista**: False  
  
-   **Modo completo**: True  
  
> [!NOTE]  
> Cuando se conecta a SQL Azure, es True de forma predeterminada.  
  
## <a name="see-also"></a>Vea también  
[Referencia de la interfaz de usuario &#40;SybaseToSQL&#41;](../../ssma/sybase/user-interface-reference-sybasetosql.md)  
  
