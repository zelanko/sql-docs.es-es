---
title: Configuración (conversión) (SybaseToSQL) del proyecto | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: eeb80fa5-f530-4f21-beee-25f5a4b8ace6
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.openlocfilehash: 4d7f290459e1da736605acad941602399ec3ea53
ms.sourcegitcommit: 6443f9a281904af93f0f5b78760b1c68901b7b8d
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/11/2018
ms.locfileid: "53215302"
---
# <a name="project-settings-conversion-sybasetosql"></a>Configuración del proyecto (conversión) (SybaseToSQL)
La página de conversión de la **configuración del proyecto** cuadro de diálogo contiene la configuración que permiten personalizar cómo SSMA convierte la sintaxis de Sybase Adaptive Server Enterprise (ASE) para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o sintaxis de SQL Azure.  
  
El panel de conversión está disponible en el **configuración del proyecto** y **configuración de proyecto predeterminada** cuadros de diálogo:  
  
-   Si desea especificar la configuración para todos los proyectos SSMA, en el **herramientas** menú, seleccione **la configuración predeterminada del proyecto**, haga clic en **General** en la parte inferior del panel izquierdo y, a continuación, haga clic en **Conversión**.  
  
-   Para especificar la configuración para el proyecto actual, en el **herramientas** menú, seleccione **configuración del proyecto**, haga clic en **General** en la parte inferior del panel izquierdo y, a continuación, haga clic en **Conversión**.  
  
## <a name="miscellaneous-options"></a>Otras opciones  
**@@ERROR**  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]/ SQL Azure y ASE usan distintos códigos de error.  
  
Use esta opción para especificar el tipo de mensaje (advertencia o Error) que SSMA se muestra en el panel de salida o la lista de errores cuando encuentra una referencia a **@@ERROR**  en el código de ASE.  
  
-   Si selecciona **convertir y marcar con advertencia**, SSMA convertirá las instrucciones y márquelos con comentarios de advertencia.  
  
-   Si selecciona **marca con el error**, SSMA omitirá la conversión y marcar las instrucciones con comentarios de error.  
  
Al seleccionar un modo de conversión en el **modo** cuadro, SSMA aplica la siguiente configuración:  
  
**Modo predeterminado/optimista:** Convertir y marcar con advertencia  
  
**Modo completo:** Marcar con error  
  
**Conversión de operador LIKE**  
Especifica si se deben convertir como operandos para coincidir con el comportamiento de Sybase ASE. El punto es que recorta los espacios en blanco en un patrón like de Sybase. La solución consiste en realizar una conversión de expresión de la derecha en un tipo de datos de longitud fija con una precisión máxima.  
  
-   Seleccione **conversión Simple** para convertir las expresiones sin ninguna corrección.  
  
-   Para usar el comportamiento, seleccione el ASE **convertir a una longitud fija.**  
  
Cuando se selecciona un modo de conversión en el cuadro modo, SSMA aplica la siguiente configuración:  
  
**Modo predeterminado/optimista**: Conversión simple  
  
**Modo completo**: Convertir a una longitud fija  
  
**CONVERTIR O CONVERTIR LAS CADENAS VACÍAS PARA LOS TIPOS NUMÉRICOS**  
Especifica cómo tratar las cadenas en blanco o vacías dentro de las expresiones de CONVERT o CAST con un tipo numérico como argumento de tipo de datos. Las siguientes opciones están disponibles para esta configuración:  
  
-   Seleccione **conversión Simple** para convertir las expresiones sin ninguna corrección.  
  
-   Si **cadena vacía como cero numérico** está seleccionada, el parámetro de cadena {s} se reemplazará con mayúsculas ltrim(rtrim({s})) cuando "", a continuación, 0 else {s} expresión final  
  
Cuando se selecciona un modo de conversión en el cuadro modo, SSMA aplica la siguiente configuración:  
  
**Modo predeterminado/optimista**: Conversión simple  
  
**Modo completo**: Cadena vacía como cero numérico  
  
**Concatenación de NULL**  
Esta configuración especifica cómo convertir la concatenación de cadenas con NULL. Para esta configuración concreta, se pueden establecer las siguientes opciones:  
  
-   **Ajustar con la función ISNULL:** Si se establece esta opción, se ajustará cada 'string_expression' en la concatenación no constante con ISNULL(string_expression) y se reemplazará los valores NULL con una cadena vacía.  
  
-   **Mantener la sintaxis actual**  
  
Al seleccionar un modo de conversión en el **modo** cuadro, SSMA aplica la siguiente configuración:  
  
**Modo predeterminado/optimista:** Mantener la sintaxis actual  
  
**Modo completo:** Ajustar con la función ISNULL  
  
**Conversión de cadenas vacías**  
Esta configuración especifica cómo convertir las cadenas vacías. Para esta configuración concreta, se pueden establecer las siguientes opciones:  
  
-   **Reemplace todas las expresiones de cadena con espacio**  
  
-   **Reemplace las constantes de cadena vacío con espacio**  
  
-   Para usar el [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]o comportamiento de SQL Azure, seleccione **mantener sintaxis actual**.  
  
Al seleccionar un modo de conversión en el **modo** cuadro, SSMA aplica la siguiente configuración:  
  
**Modo predeterminado/optimista:** Mantener la sintaxis actual  
  
**Modo completo:** Reemplace todas las expresiones de cadena con espacio  
  
**Conversión de cadena binaria de conversión y conversión**  
La conversión de valores binarios en números puede devolver valores diferentes en distintas plataformas. Por ejemplo, en x86 procesadores, CONVERT (entero, 0 x 00000100) devuelve 65536 en ASE y 256 en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. ASE también devuelve diferentes valores según el orden de bytes.  
  
Use esta opción para controlar cómo convertir convierte SSMA y las expresiones CASE que contienen valores binarios:  
  
-   Seleccione **conversión Simple** para convertir las expresiones sin ninguna advertencia o corrección. Use esta opción si sabe que el servidor de ASE tiene un orden de bytes que no se requiere ningún cambio del valor binario.  
  
-   Seleccione **convertir y corregir** tener SSMA convertir y corregir las expresiones para su uso en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Se invertirá el orden de bytes en constantes literales. Todos los demás valores binarios (como binarias variables y columnas) se marcará con errores. Use este valor si sabe que el servidor de ASE tiene un orden de bytes que requiere cambios en los valores binarios.  
  
-   Seleccione **convertir y marcar con advertencia** tener SSMA convertir y corregir las expresiones y marque todas convertir expresiones con comentarios de advertencia.  
  
Al seleccionar un modo de conversión en el **modo** cuadro, SSMA aplica la siguiente configuración:  
  
**Modo predeterminado:** Convertir y marcar con advertencia  
  
**Modo optimista:** Conversión simple  
  
**Modo completo:** Convertir y corregir  
  
**SQL dinámico**  
Use esta opción para especificar el tipo de mensaje (advertencia o Error) que SSMA se muestra en el panel de salida o la lista de errores cuando encuentra SQL dinámico en el código de ASE.  
  
-   Si selecciona **convertir y marcar con advertencia**, SSMA convertirá el SQL dinámico y marcar las instrucciones con comentarios de advertencia.  
  
-   Si selecciona **marca con el error**, SSMA omitirá la conversión y marcar las instrucciones con comentarios de error.  
  
Al seleccionar un modo de conversión en el **modo** cuadro, SSMA aplica la siguiente configuración:  
  
**Modo predeterminado/optimista:** Convertir y marcar con advertencia  
  
**Modo completo:** Marcar con error  
  
**Conversión de comprobación de igualdad**  
En [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]/ SQL Azure, si el valor de ANSI_NULLS es on, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]/ SQL Azure devuelve UNKNOWN cuando las comparaciones de igualdad contienen un valor null. Si ANSI_NULLS es off, las comparaciones de igualdad que contienen valores null devuelven Verdadero cuando la columna comparada y expresión o dos expresiones son null. Por igualdad de valor predeterminado (ANSINULL OFF) Sybase ASE las comparaciones se comportan como [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]/ SQL Azure con ANSI_NULLS OFF.  
  
-   Si selecciona **conversión Simple**, SSMA convertirá el código de ASE a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]o sintaxis de SQL Azure sin comprobaciones adicionales para los valores null. Use esta opción si ANSI_NULLS está desactivada en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]/ SQL Azure o si desea revisar las comparaciones de igualdad por caso.  
  
-   Si selecciona **valores NULL considere**, SSMA agregará las comprobaciones de valores null mediante el uso de las cláusulas IS NULL e IS NOT NULL.  
  
Al seleccionar un modo de conversión en el **modo** cuadro, SSMA aplica la siguiente configuración:  
  
**Modo predeterminado/optimista:** Conversión simple  
  
**Modo completo:** Considere la posibilidad de valores NULL  
  
**Cadenas de formato**  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Y SQL Azure ya no admite la *format_string* argumento en las instrucciones PRINT y RAISERROR. El *format_string* variable admite poner parámetros reemplazables directamente en la cadena y, a continuación, reemplazando los parámetros en tiempo de ejecución. En su lugar, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] requiere la cadena completa mediante el uso de un literal de cadena o una cadena creada con una variable. Para obtener más información, consulte la "PRINT ( [!INCLUDE[tsql](../../includes/tsql-md.md)])" tema en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] libros en pantalla.  
  
Cuando encuentra SSMA un *format_string* argumento, puede generar una cadena literal con las variables o crear una nueva variable y generar una cadena mediante el uso de esa variable.  
  
-   Para utilizar un literal de cadena para las funciones PRINT y RAISERROR, seleccione **crear nueva cadena**.  
  
    En este modo, si una instrucción PRINT o RAISERROR no usa marcadores de posición y las variables locales, no se modifica la instrucción. Caracteres dobles de porcentaje (%) se cambian a un único carácter de porcentaje % en los literales de cadena de impresión.  
  
    Si una instrucción PRINT o RAISERROR usa marcadores de posición y uno o más variables locales, como se muestra en el ejemplo siguiente:  
  
    ```  
    PRINT 'Total: %1!%%', @percent  
    ```  
    SSMA convertirá en la siguiente sintaxis:  
  
    ```  
    PRINT 'Total: '+ CAST(@percent AS varchar(max)) + '%'  
    ```  
    Si *format_string* es una variable, como en la siguiente instrucción:  
  
    ```  
    PRINT @fmt, @arg1, @arg2  
    ```  
    No puede realizar una conversión de cadena simple SSMA y debe crear una nueva variable:  
  
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
    Cuando usa **crear nueva cadena** modo, SSMA se da por supuesto que el [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] opción CONCAT_NULL_YIELDS_NULL es OFF. Por lo tanto, no comprueba si hay argumentos null SSMA.  
  
-   Para crear una nueva variable para cada instrucción RAISERROR y PRINT y, a continuación, usar esa variable para el valor de cadena SSMA, seleccione **crear nueva variable**.  
  
    En este modo, si una instrucción PRINT o RAISERROR no usa marcadores de posición y las variables locales, SSMA reemplaza todos los caracteres de porcentaje doble (%) por caracteres de porcentaje individuales para cumplir con [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]o sintaxis de SQL Azure.  
  
    Si una instrucción PRINT o RAISERROR usa marcadores de posición y uno o más variables locales, como se muestra en el ejemplo siguiente:  
  
    ```  
    PRINT 'Total: %1!%%', @percent  
    ```  
    SSMA convertirá en la siguiente sintaxis:  
  
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
  
**Modo predeterminado/optimista:** Crear nueva cadena  
  
**Modo completo:** Crear nueva variable  
  
**Insertar un valor explícito en una columna de marca de tiempo**  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]O no admite SQL Azure insertar valores explícitos en una columna de marca de tiempo.  
  
-   Para excluir las columnas de marca de tiempo de las instrucciones INSERT, seleccione **columna excluir**.  
  
-   Para imprimir un mensaje de error cada vez que se encuentra una columna de marca de tiempo en una instrucción INSERT, seleccione **marca con el error**. En este modo, las instrucciones INSERT no se convertirán y se marcará con comentarios de error.  
  
Al seleccionar un modo de conversión en el **modo** cuadro, SSMA aplica la siguiente configuración:  
  
**Modo predeterminado/optimista:** Excluir la columna  
  
**Modo completo:** Marcar con error  
  
**Objetos temporales que se definen en los procedimientos de Store**  
Esta configuración especifica si las definiciones de objetos temporales que aparecen en los procedimientos se deben almacenar en los metadatos de origen durante la conversión.  
  
-   Seleccione **Sí** para almacenar en los metadatos.  
  
-   Seleccione **n** si no es necesario almacenar los objetos.  
  
**Modo predeterminado/optimista:** Sí  
  
**Modo completo:** No  
  
**Conversión de la tabla de proxy**  
Especifica si las tablas de proxy de ASE se convierten en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]/ no convertir las tablas de SQL Azure, o son y el código está marcado con comentarios de error.  
  
-   Seleccione **convertir** para convertir las tablas de proxy para las tablas normales.  
  
-   Seleccione **marca con el error** para marcar simplemente el código de la tabla de proxy con comentarios de error.  
  
Al seleccionar un modo de conversión en el **modo** cuadro, SSMA aplica la siguiente configuración:  
  
**Modo predeterminado/optimista/completo:** Marcar con error  
  
**Número de mensajes de base de RAISERROR**  
Mensajes de usuario de ASE se almacenan en cada base de datos. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] mensajes de usuario centralmente están almacenados y están disponibles a través de la **sys.messages** vista de catálogo. Además los mensajes de usuario de ASE a partir de 20000, pero [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 50001 a partir de los mensajes de error.  
  
Esta configuración especifica el número que se agregará al número de mensajes de usuario de ASE para convertirlo en un [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] mensaje de usuario. Si su [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tiene mensajes de usuario en el **sys.messages** vista de catálogo, es posible que deba cambiar este número en un valor superior. Esto es por lo que los números de mensaje convertido no entren en conflicto con los números de mensajes existente.  
  
Tenga en cuenta lo siguiente:  
  
-   Mensajes de ASE en el intervalo 17000 a 19999 proceden de la tabla del sistema sysmessages y no se convierten.  
  
-   Si el número de mensajes que se hace referencia en la instrucción RAISERROR es una constante, SSMA agregarán el número de mensajes de base a la constante para determinar el número de mensajes de usuario nuevo.  
  
-   Si el número de mensajes que se hace referencia es una variable o expresión, SSMA creará una variable local con intermedia.  
  
-   En el modo optimista, SSMA supone que el [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] opción CONCAT_NULL_YIELDS_NULL es off y no realiza ninguna comprobación para los argumentos null.  
  
-   En el modo completo, SSMA comprueba si hay argumentos null.  
  
-   RAISERROR con DATOSERROR *lista* no se convierte.  
  
Al seleccionar un modo de conversión en el **modo** cuadro, SSMA aplica la siguiente configuración:  
  
**Modo predeterminado/optimista/completo:** 30001  
  
**Objetos del sistema**  
Use esta opción para especificar el tipo de mensaje (advertencia o Error) que SSMA se muestra en el panel de salida o la lista de errores cuando encuentra el uso de objetos del sistema ASE.  
  
-   Si selecciona **convertir y marcar con advertencia**, SSMA convertirá las referencias a objetos del sistema y marcará las instrucciones con comentarios de advertencia.  
  
-   Si selecciona **marca con el error**, SSMA no convertirá las referencias a objetos de sistemas y marcará las instrucciones con comentarios de error.  
  
Al seleccionar un modo de conversión en el **modo** cuadro, SSMA aplica la siguiente configuración:  
  
**Modo predeterminado/optimista:** Convertir y marcar con advertencia  
  
**Modo completo:** Marcar con error  
  
**Identificadores sin resolver**  
Use esta opción para especificar el tipo de mensaje (advertencia o Error) que SSMA se muestra en el panel de salida o la lista de errores cuando no puede resolver un identificador.  
  
-   Si selecciona **convertir y marcar con advertencia**, intentará convertir referencias a identificadores sin resolver de SSMA y marcará las instrucciones con comentarios de advertencia.  
  
-   Si selecciona **marca con el error**, SSMA no convertirá las referencias a identificadores sin resolver y marcará las instrucciones con comentarios de error.  
  
Al seleccionar un modo de conversión en el **modo** cuadro, SSMA aplica la siguiente configuración:  
  
**Modo predeterminado/optimista:** Convertir y marcar con advertencia  
  
**Modo completo:** Marcar con error  
  
## <a name="system-function-options"></a>Opciones de función del sistema  
**CHARINDEX, función**  
En el ASE, CHARINDEX devuelve NULL solo si todas las expresiones de entrada son NULL. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Y SQL Azure devolverá NULL si cualquier expresión de entrada es NULL.  
  
-   Para usar el comportamiento de ASE, seleccione **reemplazar la función**. Todas las llamadas a función CHARINDEX se sustituye por una llamada a CHARINDEX_VARCHAR o CHARINDEX_NVARCHAR una función definida por el usuario según el tipo de parámetros pasados (creado en la base de datos de usuario en el nombre de esquema 's2ss') para emular el comportamiento de Sybase ASE.  
  
-   Para usar el [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]o comportamiento de SQL Azure, seleccione **mantener sintaxis actual**.  
  
Al seleccionar un modo de conversión en el **modo** cuadro, SSMA aplica la siguiente configuración:  
  
**Modo predeterminado/optimista:** Mantener la sintaxis actual  
  
**Modo completo:** Reemplace la función  
  
**Función DATALENGTH**  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] / SQL Azure y ASE difieren en el valor devuelto por la función DATALENGTH cuando el valor es un único espacio. En este caso, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]/ SQL Azure devuelve 0 y ASE devuelve 1.  
  
-   Para usar el comportamiento de ASE, seleccione **reemplazar la función**. Todas las llamadas a la función DATALENGTH se sustituirán por la expresión CASE para emular el comportamiento de Sybase ASE.  
  
-   Use el valor predeterminado [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o comportamiento de SQL Azure, seleccione **mantener sintaxis actual**.  
  
Al seleccionar un modo de conversión en el **modo** cuadro, SSMA aplica la siguiente configuración:  
  
**Modo predeterminado/optimista:** Mantener la sintaxis actual  
  
**Modo completo:** Reemplace la función  
  
**Index_col, función**  
ASE admite opcional *user_id* argumento a la función INDEX_COL; sin embargo, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]o SQL Azure no admite este argumento. Si usas el *user_id* argumento, esta función no puede convertirse en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]o sintaxis de SQL Azure.  
  
-   Para usar el comportamiento de ASE, seleccione **convertir función**. Si el código contiene la *user_id* argumento, SSMA mostrará un error.  
  
-   Para mostrar un mensaje de error cada vez que se encuentra esa INDEX_COL, seleccione **marca con el error**. SSMA no convertirá las referencias a la función y marcará la instrucción con comentarios de error.  
  
**Modo predeterminado/optimista/completo:** Marcar con error  
  
**Función INDEX_COLORDER**  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]O SQL Azure no tiene una función de sistema INDEX_COLORDER.  
  
-   Para usar el comportamiento de ASE, seleccione **convertir función**. Todas las llamadas a función INDEX_COLORDER se sustituye por una llamada a una función definida por el usuario con el mismo nombre INDEX_COLORDER (creada en la base de datos de usuario en el nombre de esquema 's2ss'), que emula el comportamiento de Sybase ASE.  
  
-   Para imprimir un mensaje de error cada vez que se encuentra esa INDEX_COLORDER, seleccione **marca con el error**. SSMA no convertirá las referencias a la función y marcará la instrucción con comentarios de error.  
  
Al seleccionar un modo de conversión en el **modo** cuadro, SSMA aplica la siguiente configuración:  
  
**Modo predeterminado/optimista/completo:** Marcar con error  
  
**Las funciones LEFT y RIGHT**  
Izquierda y derecha funciones en Sybase comportan de manera diferente para el parámetro de longitud negativa.  
  
-   Para usar el comportamiento de ASE, seleccione **función Replace**. El parámetro de longitud, a continuación, se reemplaza por la expresión CASE que devolvería null para un valor negativo.  
  
-   Para usar el comportamiento de SQL Server, seleccione **mantener sintaxis actual**  
  
Al seleccionar un modo de conversión en el **modo** cuadro, SSMA aplica la siguiente configuración:  
  
**Modo predeterminado/optimista:** Mantener la sintaxis actual  
  
**Modo completo:** Reemplace la función  
  
> [!NOTE]  
> Si el parámetro de longitud es un valor literal y no una expresión compleja, el valor de longitud siempre se reemplaza con el valor null con independencia de la configuración del proyecto.  
  
**Función NEXT_IDENTITY**  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]O SQL Azure no tiene una función de sistema NEXT_IDENTITY.  
  
-   Para usar el comportamiento de ASE, seleccione **convertir función**. Todas las llamadas a función NEXT_IDENTITY se sustituye por la expresión (IDENT_CURRENT(parameter Value) + IDENT_INCR(parameter Value) que emula el comportamiento de Sybase ASE.  
  
-   Para imprimir un mensaje de error cada vez que se encuentra esa NEXT_IDENTITY, seleccione **marca con el error**. SSMA no convertirá las referencias a la función y marcará la instrucción con comentarios de error.  
  
Al seleccionar un modo de conversión en el **modo** cuadro, SSMA aplica la siguiente configuración:  
  
**Modo predeterminado/optimista/completo:** Marcar con error  
  
**Función PATINDEX**  
Especifica si se debe convertir la función PATINDEX para emular el comportamiento de Sybase ASE. El punto es que recorta los espacios en blanco en un patrón de búsqueda de Sybase. La solución consiste en realizar una conversión de expresión de valor a un tipo con una precisión máxima de datos y aplican la función rtrim para buscar el patrón de longitud fija.  
  
-   Para usar el comportamiento, seleccione el ASE **usar**.  
  
-   Use el valor predeterminado [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]o comportamiento de SQL Azure, seleccione **no use**.  
  
Al seleccionar un modo de conversión en el **modo** cuadro, SSMA aplica la siguiente configuración:  
  
**Modo predeterminado/optimista:** No debe usarse  
  
**Modo completo:** Usar  
  
**Función REPLICATE**  
La función REPLICATE repite una cadena el número de veces especificado. En el ASE, si se especifica para repetir la cadena de cero veces, el resultado es null. En [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]/ SQL Azure, el resultado es una cadena vacía.  
  
-   Para usar el comportamiento de ASE, seleccione **reemplazar la función**. Todas las llamadas a función REPLICATE se sustituye por una llamada a REPLICATE_VARCHAR o REPLICATE_NVARCHAR una función definida por el usuario según el tipo de parámetros pasados (creado en la base de datos de usuario en el nombre de esquema 's2ss') para emular el comportamiento de Sybase ASE.  
  
-   Use el valor predeterminado [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]o comportamiento de SQL Azure, seleccione **función Replace**.  
  
Al seleccionar un modo de conversión en el **modo** cuadro, SSMA aplica la siguiente configuración:  
  
**Modo completo y el modo predeterminado/optimista:** Reemplace la función  
  
**Función TRIM (LTRIM, RTRIM)**  
Esta configuración especifica si va a mantener la sintaxis actual o reemplazar las llamadas a funciones Trim (LTRIM, RTRIM) con las funciones de sintaxis de Sybase ASE equivalentes. Las siguientes opciones están disponibles para esta configuración concreta:  
  
-   **Reemplace la función**  
  
-   **Mantener la sintaxis actual**  
  
Al seleccionar un modo de conversión en el **modo** cuadro, SSMA aplica la siguiente configuración:  
  
**Modo completo y el modo predeterminado/optimista:** Reemplace la función  
  
**Función SUBSTRING**  
En el ASE, la función `SUBSTRING(expression, start, length)` devuelve NULL si no se especifica un valor de inicio mayor que el número de caracteres de expresión, o si la longitud es igual a cero. En [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]/ SQL Azure, la expresión equivalente devuelve una cadena vacía.  
  
-   Para usar el comportamiento de ASE, seleccione **reemplazar la función**. Todas las llamadas a función SUBSTRING se sustituye por una llamada a SUBSTRING_VARCHAR o SUBSTRING_NVARCHAR o SUBSTRING_VARBINARY una función definida por el usuario según el tipo de parámetros pasados (creada en la base de datos de usuario bajo el nombre de esquema 's2ss') para emular el Comportamiento de Sybase ASE.  
  
-   Para usar el [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o comportamiento de SQL Azure, seleccione **mantener sintaxis actual**.  
  
Al seleccionar un modo de conversión en el **modo** cuadro, SSMA aplica la siguiente configuración:  
  
**Modo predeterminado/optimista:** Mantener la sintaxis actual  
  
**Modo completo:** Reemplace la función  
  
## <a name="tables"></a>TABLES  
**Agregar la clave principal**  
Crea una nueva clave principal en la [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o una tabla de SQL Azure, si una tabla de Access no tiene ninguna clave principal o índice único.  
  
-   **Modo predeterminado**: False  
  
-   **Modo optimista**: False  
  
-   **Modo completo**: True  
  
> [!NOTE]  
> Cuando se conecta a SQL Azure, es True de forma predeterminada.  
  
## <a name="see-also"></a>Vea también  
[Referencia de la interfaz de usuario &#40;SybaseToSQL&#41;](../../ssma/sybase/user-interface-reference-sybasetosql.md)  
  
