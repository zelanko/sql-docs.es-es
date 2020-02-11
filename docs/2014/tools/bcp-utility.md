---
title: bcp (Utilidad) | Microsoft Docs
ms.custom: ''
ms.date: 10/27/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: tools-other
ms.topic: conceptual
helpviewer_keywords:
- bcp utility [SQL Server]
- exporting data
- row exporting [SQL Server]
- copying data [SQL Server], bcp utility
- command prompt utilities [SQL Server], bcp
- tables [SQL Server], importing data
- column importing [SQL Server]
- bcp utility [SQL Server], command options
- file exporting [SQL Server]
- bulk copy [SQL Server]
- bcp utility [SQL Server], about bcp utility
- tables [SQL Server], exporting data
- row importing [SQL Server]
- importing data, bcp utility
- file importing [SQL Server]
- column exporting [SQL Server]
ms.assetid: c0af54f5-ca4a-4995-a3a4-0ce39c30ec38
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 24367bfec4b0e25fec60eb49c77a74e1ccd54f46
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "68187138"
---
# <a name="bcp-utility"></a>bcp (utilidad)
  La utilidad **BCP** copia datos de forma masiva entre una [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] instancia de y un archivo de datos en un formato especificado por el usuario. La utilidad **bcp** se puede usar para importar un número elevado de filas nuevas en tablas de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] o para exportar datos de tablas a archivos de datos. Excepto cuando se usa con la opción **queryout** , la utilidad no requiere ningún conocimiento de [!INCLUDE[tsql](../includes/tsql-md.md)]. Para importar datos en una tabla, debe usar un archivo de formato creado para esa tabla o comprender la estructura de la tabla y los tipos de datos que son válidos para sus columnas.  
  
 ![Icono de vínculo de tema](../../2014/database-engine/media/topic-link.gif "Icono de vínculo de tema") Para obtener las convenciones de sintaxis que se usan para la sintaxis de **BCP** , vea [convenciones de sintaxis de transact-SQL &#40;&#41;de Transact-SQL ](/sql/t-sql/language-elements/transact-sql-syntax-conventions-transact-sql).  
  
> [!NOTE]  
>  Si usa **bcp** para hacer una copia de seguridad de los datos, cree un archivo de formato para registrar el formato de datos. los archivos de datos **BCP** no incluyen ningún esquema ni información de formato, por lo que si se quita una tabla o una vista y no tiene un archivo de formato, es posible que no pueda importar los datos.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
   bcp [database_name.] schema.{table_name | view_name | "query" {indata_file | outdata_file | queryoutdata_file | format nul}  
  
[-apacket_size]  
[-bbatch_size]  
[-c]  
[-C { ACP | OEM | RAW | code_page } ]  
[-ddatabase_name]  
[-eerr_file]  
[-E]  
[-fformat_file]  
[-Ffirst_row]  
[-h"hint [,...n]"]   
[-iinput_file]  
[-k]  
[-Kapplication_intent]  
[-Llast_row]  
[-mmax_errors]  
[-n]  
[-N]  
[-ooutput_file]  
[-Ppassword]  
[-q]  
[-rrow_term]  
[-R]  
[-S [server_name[\instance_name]]  
[-tfield_term]  
[-T]  
[-Ulogin_id]  
[-v]  
[-V (80 | 90 | 100 | 110)]  
[-w]  
[-x]  
/?  
```  
  
## <a name="arguments"></a>Argumentos  
 *data_file*  
 Es la ruta completa del archivo de datos. Cuando se importan datos de forma masiva a [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)], el archivo de datos contiene los datos que se van a copiar en la tabla o vista especificada. Cuando se realiza una exportación de datos de forma masiva desde [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)], el archivo de datos contiene los datos copiados desde la tabla o desde la vista. La ruta de acceso puede contener de 1 a 255 caracteres. El archivo de datos puede contener un máximo de 2<sup>63</sup> -1 filas.  
  
 *database_name*  
 Es el nombre de la base de datos en la que reside la tabla o vista especificada. Si no se especifica, es la base de datos predeterminada para el usuario.  
  
 También puede especificar explícitamente el nombre de la base de datos con `d-`.  
  
 **en** _data_file_ | **out**__ data_file | **QUERYOUT**__ data_file | **formato NUL**  
 Especifica la dirección de la copia masiva, de la siguiente manera:  
  
-   **in** copia desde un archivo en la vista o tabla de base de datos.  
  
-   **out** copia desde la tabla o vista de la base de datos a un archivo. Si se especifica un archivo ya existente, este se sobrescribe. Al extraer datos, tenga en cuenta que la utilidad **bcp** representa una cadena vacía como nula y una cadena nula como vacía.  
  
-   **QUERYOUT** copia desde una consulta y debe especificarse solo cuando se copian datos de forma masiva desde una consulta.  
  
-   **Format** crea un archivo de formato basado en la opción especificada (**-n** `-c`, `-w`, o **-n**) y en los delimitadores de la vista o de la tabla. Cuando se copian datos en bloque, el comando **bcp** puede hacer referencia a un archivo de formato, lo que evita tener que especificar de nuevo la información de formato interactivamente. La opción **format** necesita la opción **-f**; la creación de un archivo de formato XML también requiere la opción **-x**. Para obtener más información, vea [Crear un archivo de formato &#40;SQL Server&#41;](../relational-databases/import-export/create-a-format-file-sql-server.md). Hay que especificar **nul**como el valor (**format nul**).  
  
 *propietario*  
 Es el nombre del propietario de la tabla o vista. *Owner* es opcional si el usuario que realiza la operación es propietario de la tabla o vista especificada. Si *owner* no se especifica y el usuario que realiza la acción no es el propietario de la tabla o la vista especificada, [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] devuelve un mensaje de error y se cancela la operación.  
  
 **"** _consulta_ **"**  
 Es una consulta [!INCLUDE[tsql](../includes/tsql-md.md)] que devuelve un conjunto de resultados. Si la consulta devuelve múltiples conjuntos de resultados, solo se copiará el primero en el archivo de datos; los conjuntos de resultados siguientes se omitirán. Utilice comillas dobles para la consulta y comillas simples en los elementos que incruste en la consulta. **QUERYOUT** también se debe especificar cuando se copian datos de forma masiva desde una consulta.  
  
 La consulta puede hacer referencia a un procedimiento almacenado siempre que todas las tablas a las que se haga referencia dentro del procedimiento almacenado existan antes de ejecutar la instrucción bcp. Por ejemplo, si el procedimiento almacenado genera una tabla temporal, se produce un error en la instrucción **bcp** porque la tabla temporal solamente está disponible en tiempo de ejecución y no cuando se ejecuta la instrucción. En este caso, considere la posibilidad de insertar los resultados del procedimiento almacenado en una tabla y, después, usar **bcp** para copiar los datos de la tabla en un archivo de datos.  
  
 *table_name*  
 Es el nombre de la tabla de destino cuando se importan datos a [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] (**in**) y la tabla de origen cuando se exportan datos de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] (**out**).  
  
 *view_name*  
 Es el nombre de la vista de destino cuando se copian datos en [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] (**in**) y la vista de origen cuando se copian datos de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] (**out**). Solamente pueden usarse como vistas de destino aquellas vistas en las que todas las columnas hacen referencia a la misma tabla. Para obtener más información sobre las restricciones para copiar datos en vistas, vea [INSERT &#40;Transact-SQL&#41;](/sql/t-sql/statements/insert-transact-sql).  
  
 **-un** _packet_size_  
 Especifica el número de bytes por paquete de red enviados y recibidos por el servidor. Se puede establecer una opción de configuración de servidor con [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] (o el procedimiento almacenado del sistema **sp_configure**). No obstante, la opción de configuración de servidor puede sustituirse individualmente mediante esta opción. *packet_size* puede ser de 4096 a 65535 bytes; el valor predeterminado es 4096.  
  
 Un tamaño mayor de los paquetes puede mejorar el rendimiento de las operaciones de copia masiva. Si se pide un tamaño de paquete mayor, pero no puede concederse, se usa el valor predeterminado. Las estadísticas de rendimiento generadas por la utilidad **bcp** muestran el tamaño del paquete usado.  
  
 **-b** _batch_size_  
 Especifica el número de filas por lote de datos importados. Cada lote se importa y registra como una transacción aparte que importa el lote entero antes de confirmarse. De forma predeterminada, todas las filas del archivo de datos se importan en un solo lote. Para distribuir las filas en varios lotes, especifique un valor de *batch_size* inferior al número de filas del archivo de datos. Si se produce un error en la transacción de un lote, solamente se revierten las inserciones del lote actual. Los lotes importados por transacciones confirmadas no se ven afectados por los errores posteriores.  
  
 No use esta opción junto con la opción **-h "** ROWS_PER_BATCH ** = *`bb`*"** .  
  
 `-c`  
 Realiza la operación con un tipo de datos de caracteres. Esta opción no realiza una petición para cada campo; usa `char` como tipo de almacenamiento, sin prefijos y con **\t** (carácter de tabulación) como separador de campos y **\r\n** (carácter de nueva línea) como terminador de fila. 
  `-c` no es compatible con `-w`.  
  
 Para obtener más información, vea [Usar el formato de caracteres para importar o exportar datos &#40;SQL Server&#41;](../relational-databases/import-export/use-character-format-to-import-or-export-data-sql-server.md).  
  
 **-C** { **ACP** | **OEM** | **raw** | *code_page* }  
 Especifica la página de códigos de los datos incluidos en el archivo de datos. *code_page* solo es pertinente si los datos contienen `char`columnas `varchar`, o `text` con valores de caracteres mayores que 127 o menores que 32.  
  
> [!NOTE]  
>  Se recomienda especificar un nombre de intercalación para cada columna de un archivo de formato.  
  
|Valor de página de códigos|Descripción|  
|---------------------|-----------------|  
|ACP|
  [!INCLUDE[vcpransi](../includes/vcpransi-md.md)]/Microsoft Windows (ISO 1252).|  
|OEM|Página de códigos predeterminada, utilizada por el cliente. Esta es la página de códigos que se usa de forma predeterminada si no se especifica **-C** .|  
|RAW|No se realiza ninguna conversión entre páginas de códigos. Se trata de la opción más rápida porque no se producen conversiones.|  
|*code_page*|Número específico de una página de códigos, por ejemplo, 850.<br /><br /> **&#42;&#42; importante &#42;&#42;** [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] no admite la página de códigos 65001 (codificación UTF-8).|  
  
 `-d` *database_name*  
 Especifica la base de datos a la que conectarse. De forma predeterminada, bcp.exe se conecta a la base de datos predeterminada del usuario. Si `-d`se especifica *database_name* y un nombre de tres partes (*database_name. Schema. Table*, que se pasa como primer parámetro a BCP. exe), se producirá un error porque no se puede especificar dos veces el nombre de la base de datos. Si *database_name* comienza con un guión (-) o una barra diagonal (/), no agregue un espacio entre `-d` y el nombre de la base de datos.  
  
 **-e** _err_file_  
 Especifica la ruta de acceso completa de un archivo de error que se usa para almacenar las filas que la utilidad **bcp** no puede transferir del archivo a la base de datos. Los mensajes de error del comando **bcp** van a la estación de trabajo del usuario. Si no se usa esta opción, no se creará el archivo de errores.  
  
 Si *err_file* comienza con un guión (-) o una barra diagonal (/), no incluya un espacio entre **-e** y el valor de *err_file*.  
  
 **-E**  
 Especifica que se usará el valor o valores de identidad del archivo de datos importado para la columna de identidad. Si no se especifica **-E**, se omiten los valores de identidad de esta columna en el archivo de datos que se importa y [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] asigna automáticamente valores únicos basados en los valores de inicialización y de incremento especificados durante la creación de la tabla.  
  
 Si el archivo de datos no contiene valores para la columna de identidad de la tabla o la vista, use un archivo de formato para especificar que se debe omitir la columna de identidad de la tabla o la vista al importar los datos; [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] asigna automáticamente valores únicos para la columna. Para obtener más información, vea [DBCC CHECKIDENT &#40;Transact-SQL&#41;](/sql/t-sql/database-console-commands/dbcc-checkident-transact-sql).  
  
 La opción **-E** tiene un requisito de permisos especial. Para obtener más información, vea "Comentarios" más adelante en este tema.  
  
 **-f** _format_file_  
 Especifica la ruta de acceso completa de un archivo de formato. El significado de esta opción depende del entorno en el que se utiliza, como se indica a continuación:  
  
-   Si se usa **-f** con la opción **format** , se crea el archivo *format_file* especificado para la tabla o la vista especificada. Para crear un archivo de formato XML, especifique también la opción **-x**. Para obtener más información, vea [Crear un archivo de formato &#40;SQL Server&#41;](../relational-databases/import-export/create-a-format-file-sql-server.md).  
  
-   Si se usa con las opciones **in** u **out**, **-f** requiere un archivo de formato existente.  
  
    > [!NOTE]  
    >  El uso de un archivo de formato con la opción **in** o **out** es opcional. En ausencia de la opción **-f** , si no se especifica **-n**, `-c`, `-w`o **-n** , el comando solicita información de formato y permite guardar las respuestas en un archivo de formato (cuyo nombre de archivo predeterminado es BCP. FMT).  
  
 Si *format_file* comienza por un guión (-) o una barra diagonal (/), no incluya un espacio entre **-f** y el valor de *format_file*.  
  
 **-F** _first_row_  
 Especifica el número de la primera fila que se exportará desde una tabla o que se importará desde un archivo de datos. Este parámetro requiere un valor mayor que (>) 0 pero menor que (\<) o igual que (=) el número total de filas. En ausencia de este parámetro, el valor predeterminado es la primera fila del archivo.  
  
 *first_row* puede ser un entero positivo con un valor de hasta 2 ^ 63-1. **-F**_first_row_ se basa en 1.  
  
 **-h "** _sugerencia_[ **,**... *n*] **"**  
 Especifica las sugerencias que deben usarse durante una importación de datos masiva en una tabla o en una vista.  
  
 Order **(**_columna_[ASC | DESC] [**,**... *n*] **)**  
 Indica el criterio de ordenación de los datos en el archivo de datos. El rendimiento de la importación masiva mejora si los datos importados se ordenan según el índice clúster de la tabla, si lo hay. Si el archivo de datos se ordena siguiendo otro criterio que no sea el orden de una clave de índice clúster, o si no hay ningún índice clúster en la tabla, la cláusula ORDER se pasa por alto. Los nombres de columna facilitados deben ser nombres válidos en la tabla de destino. De forma predeterminada, **bcp** supone que el archivo de datos no está ordenado. En las importaciones masivas optimizadas, [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] también valida que los datos importados estén ordenados.  
  
 ROWS_PER_BATCH **=** _BB_  
 Número de filas de datos por lote (como *bb*). Se usa cuando no se especifica **-b** , por lo que el archivo de datos completo se envía al servidor en una sola transacción. El servidor optimiza la carga masiva según el valor *bb*. De forma predeterminada, el valor de ROWS_PER_BATCH es desconocido.  
  
 KILOBYTES_PER_BATCH **=** _CC_  
 Número aproximado de kilobytes (KB) de datos por lote (igual que *cc*). De forma predeterminada, el valor de KILOBYTES_PER_BATCH es desconocido.  
  
 TABLOCK  
 Especifica que se adquiera un bloqueo de tabla de actualización masiva para la duración de la operación de carga masiva; de lo contrario, se adquiere un bloqueo de fila. Esta sugerencia mejora notablemente el rendimiento, dado que, al mantenerse el bloqueo durante la operación de copia masiva, se reduce la contención en la tabla por bloqueo. Varios clientes pueden cargar una tabla simultáneamente si la tabla no tiene índices y se especifica **TABLOCK** . De forma predeterminada, el comportamiento del bloqueo viene determinado por la opción de tabla **table lock on bulk load**.  
  
 CHECK_CONSTRAINTS  
 Especifica que deben comprobarse todas las restricciones de la tabla o vista de destino durante la operación de importación masiva. Sin la sugerencia CHECK_CONSTRAINTS, se omiten las restricciones CHECK y FOREIGN KEY y, después de la operación, la restricción sobre la tabla se marca como de no confianza.  
  
> [!NOTE]  
>  Las restricciones UNIQUE, PRIMARY KEY y NOT NULL se aplican siempre.  
  
 En algún momento deberá comprobar las restricciones de toda la tabla. Si la tabla no estaba vacía antes de la operación de importación masiva, el costo de revalidar la restricción puede exceder el costo de aplicar restricciones CHECK a los datos incrementales. Por lo tanto, se recomienda que se habilite normalmente la comprobación de restricciones durante una importación incremental masiva.  
  
 Una situación en la que quizá desee que las restricciones estén deshabilitadas (comportamiento predeterminado) es si los datos de entrada contienen filas que infringen las restricciones. Con las restricciones CHECK deshabilitadas, puede importar los datos y después usar instrucciones de [!INCLUDE[tsql](../includes/tsql-md.md)] para quitar los datos que no son válidos.  
  
> [!NOTE]  
>  **BCP** ahora aplica la validación de datos y las comprobaciones de datos que podrían provocar errores en los scripts si se ejecutan en datos no válidos en un archivo de datos.  
  
> [!NOTE]  
>  El modificador **-m** _max_errors_ no es válido en la comprobación de restricciones.  
  
 FIRE_TRIGGERS  
 Cuando se especifica con el argumento **in**, se ejecutarán todos los desencadenadores de inserción definidos en la tabla de destino durante la operación de copia masiva. Si no se especifica FIRE_TRIGGERS, no se ejecutará ningún desencadenador. FIRE_TRIGGERS se ignora para los argumentos **out**, **queryout** y **format**.  
  
 **-i** _input_file_  
 Especifica el nombre de un archivo de respuesta, que contiene las respuestas a las preguntas del símbolo del sistema para cada campo de datos cuando se realiza una copia masiva con el modo `-c`interactivo `-w`(no se especifica **-n**,, o **-n** ).  
  
 Si *input_file* comienza por un guión (-) o una barra diagonal (/), no incluya un espacio entre **-i** y el valor de *input_file*.  
  
 **-k**  
 Especifica que las columnas vacías deben conservar un valor NULL durante la operación, en vez de tener valores predeterminados para las columnas insertadas. Para obtener más información, vea [Mantener valores NULL o usar valores predeterminados durante la importación en bloque &#40;SQL Server&#41;](../relational-databases/import-export/keep-nulls-or-use-default-values-during-bulk-import-sql-server.md).  
  
 **-K** _application_intent_  
 Declara el tipo de carga de trabajo de la aplicación al conectarse a un servidor. El único valor que es posible es **ReadOnly**. Si no se especifica **-K**, la utilidad bcp no admitirá la conectividad con una réplica secundaria en el grupo de disponibilidad AlwaysOn. Para obtener más información, vea secundarias [activas: réplicas secundarias legibles (grupos de disponibilidad AlwaysOn)](../database-engine/availability-groups/windows/active-secondaries-readable-secondary-replicas-always-on-availability-groups.md).  
  
 **-L** _last_row_  
 Especifica el número de la última fila que se exportará desde una tabla o que se importará desde un archivo de datos. Este parámetro requiere un valor mayor que (>) 0 pero menor que (\<) o igual que (=) el número de la última fila. En ausencia de este parámetro, el valor predeterminado es la última fila del archivo.  
  
 *last_row* puede ser un entero positivo con un valor de hasta 2 ^ 63-1.  
  
 **-m** _max_errors_  
 Especifica el número máximo de errores de sintaxis que pueden producirse antes de que se cancele la operación de **bcp**. Un error de sintaxis implica un error de conversión de datos en el tipo de datos de destino. El total de *max_errors* excluye cualquier error que pueda detectarse solamente en el servidor, como las infracciones de restricciones.  
  
 Una fila que no puede copiarse con la utilidad **bcp** se omite y se cuenta como un error. Si no se incluye esta opción, el valor predeterminado es 10.  
  
> [!NOTE]  
>  La opción **-m** tampoco se aplica a la conversión de `money` los `bigint` tipos de datos o.  
  
 **-n**  
 Realiza la operación de copia masiva con los tipos de datos nativos (base de datos) de los datos. Esta opción no efectúa una petición para cada campo, sino que usa los valores nativos.  
  
 Para obtener más información, vea [Usar el formato nativo para importar o exportar datos &#40;SQL Server&#41;](../relational-databases/import-export/use-native-format-to-import-or-export-data-sql-server.md).  
  
 **-N**  
 Realiza la operación de copia masiva con los tipos de datos nativos (de la base de datos) para datos que no sean de caracteres y con datos Unicode para los datos de caracteres. Esta opción es una alternativa de mayor rendimiento que la opción `-w` y tiene como objeto la transferencia de datos de una instancia de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] a otra mediante un archivo de datos. No realiza una petición para cada campo. Utilice esta opción cuando vaya a transferir datos que contengan caracteres extendidos ANSI y desee aprovechar el rendimiento del modo nativo.  
  
 Para obtener más información, vea [Usar el formato nativo Unicode para importar o exportar datos &#40;SQL Server&#41;](../relational-databases/import-export/use-unicode-native-format-to-import-or-export-data-sql-server.md).  
  
 Si exporta y, a continuación, importa datos al mismo esquema de tabla mediante BCP. exe con **-N**, es posible que vea una advertencia de truncamiento si hay una columna de caracteres no Unicode de longitud fija (por ejemplo `char(10)`,).  
  
 La advertencia puede omitirse. Una manera de resolver esta advertencia es usar **-n** en lugar de **-N**.  
  
 **-o** _output_file_  
 Especifica el nombre de un archivo que recibe la salida redirigida desde el símbolo del sistema.  
  
 Si *output_file* comienza por un guión (-) o una barra diagonal (/), no incluya un espacio entre **-o** y el valor de *output_file*.  
  
 **-P** _contraseña_  
 Especifica la contraseña para el identificador de inicio de sesión. Si no se usa esta opción, el comando **bcp** solicitará una contraseña. Si se usa esta opción al final del símbolo del sistema sin especificar ninguna contraseña, **bcp** usa la contraseña predeterminada (NULL).  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteStrongPass](../includes/ssnotestrongpass-md.md)]  
  
 Para enmascarar la contraseña, no especifique la opción **-P** junto con la opción **-U** . En su lugar, después de especificar **bcp** junto con la opción **-U** y otros modificadores (sin especificar **-P**), pulse ENTRAR y el comando le solicitará una contraseña. Este método garantiza que la contraseña se enmascare al especificarla.  
  
 Si *password* comienza por un guión (-) o una barra diagonal (/), no incluya un espacio entre **-P** y el valor de *password*.  
  
 `-q`  
 Ejecuta la instrucción SET QUOTED_IDENTIFIERS ON en la conexión entre la utilidad **bcp** y una instancia de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]. Use esta opción para especificar una base de datos, un propietario, una tabla o un nombre de vista que contenga un espacio o una comilla simple. Englobe la totalidad del nombre de tres partes de la vista o tabla entre comillas (" ").  
  
 Para especificar un nombre de base de datos que contenga un espacio o una comilla simple, debe usar la opción **-q**.  
  
 
  `-q` no se aplica a los valores que se pasan a `-d`.  
  
 Para obtener más información, vea Comentarios, más adelante en este tema.  
  
 **-r** _row_term_  
 Especifica el terminador de la fila. El valor predeterminado es **\n** (carácter de nueva línea). Use este parámetro para sustituir el terminador de fila predeterminado. Para obtener más información, vea [Especificar terminadores de campo y de fila &#40;SQL Server&#41;](../relational-databases/import-export/specify-field-and-row-terminators-sql-server.md).  
  
 Si especifica el terminador de fila en notación hexadecimal en un comando bcp.exe, el valor se truncará en 0x00. Por ejemplo, si especifica 0x410041, se usará 0x41.  
  
 Si *row_term* comienza por un guión (-) o una barra diagonal (/), no incluya un espacio entre **-r** y el valor de *row_term*.  
  
 **-R**  
 Especifica que se realice la copia masiva de datos de moneda, fecha y hora en [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] con el formato regional definido para la configuración regional del equipo cliente. De forma predeterminada, la configuración regional se omite.  
  
 **-S** _SERVER_NAME_[ **\\** _instance_name_]  
 Especifica la instancia de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] a la que hay que conectarse. Si no se especifica ningún servidor, la utilidad **bcp** se conecta a la instancia predeterminada de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] en el equipo local. Esta opción es necesaria cuando se ejecuta un comando **bcp** desde un equipo remoto de la red o desde una instancia local con nombre. Para establecer una conexión con la instancia predeterminada de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] en un servidor, especifique únicamente *server_name*. Para conectarse a una instancia con nombre [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]de, *Especifique**_\\_** SERVER_NAME instance_name*.  
  
 `-t`*field_term*  
 Especifica el terminador del campo. El valor predeterminado es **\t** (carácter de tabulación). Use este parámetro para invalidar el terminador de campo predeterminado. Para obtener más información, vea [Especificar terminadores de campo y de fila &#40;SQL Server&#41;](../relational-databases/import-export/specify-field-and-row-terminators-sql-server.md).  
  
 Si especifica el terminador de campo en notación hexadecimal en un comando bcp.exe, el valor se truncará en 0x00. Por ejemplo, si especifica 0x410041, se usará 0x41.  
  
 Si *field_term* comienza con un guión (-) o una barra diagonal (/), no incluya un espacio entre `-t` y el valor de *field_term* .  
  
 **-T**  
 Especifica que la utilidad **bcp** se conecta a [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] con una conexión de confianza utilizando la seguridad integrada. No es necesario usar las credenciales de seguridad del usuario de la red, *login_id*y *password* . Si no se especifica **-T** , es necesario especificar **-U** y **-P** para iniciar sesión correctamente.  
  
 **-U** _login_id_  
 Especifica el identificador de inicio de sesión para conectar con [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)].  
  
> [!IMPORTANT]  
>  Si la utilidad **bcp** se conecta a [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] mediante una conexión de confianza que usa seguridad integrada, use la opción **-T** (conexión de confianza) en lugar de la combinación *user name* y *password*.  
  
 **-v**  
 Informa del número de versión y los derechos de autor de la utilidad **bcp**.  
  
 **-V** (**80** | **90** | **100**| **110**)  
 Realiza la operación de copia masiva con tipos de datos de versiones anteriores de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]. Esta opción no realiza una petición para cada campo, sino que utiliza los valores predeterminados.  
  
 **80** = [!INCLUDE[ssVersion2000](../includes/ssversion2000-md.md)]  
  
 **90** = [!INCLUDE[ssVersion2005](../includes/ssversion2005-md.md)]  
  
 **** =  100[!INCLUDE[ssKatmai](../includes/sskatmai-md.md)] y[!INCLUDE[ssKilimanjaro](../includes/sskilimanjaro-md.md)]  
  
 **110 =[!INCLUDE[ssSQL11](../includes/sssql11-md.md)]**  
  
 Por ejemplo, para generar datos de tipos no compatibles con [!INCLUDE[ssVersion2000](../includes/ssversion2000-md.md)], pero que se introdujeron en versiones posteriores de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)], use la opción -V80.  
  
 Para obtener más información, vea [Importar datos con formato nativo y de caracteres de versiones anteriores de SQL Server](../relational-databases/import-export/import-native-and-character-format-data-from-earlier-versions-of-sql-server.md).  
  
 `-w`  
 Realiza la operación de copia masiva con caracteres Unicode. Esta opción no realiza una petición para cada campo; usa `nchar` como tipo de almacenamiento, sin prefijos, **\t** (carácter de tabulación) como separador de campos y **\n** (carácter de nueva línea) como terminador de fila. 
  `-w` no es compatible con `-c`.  
  
 Para obtener más información, vea [Usar el formato de caracteres Unicode para importar o exportar datos &#40;SQL Server&#41;](../relational-databases/import-export/use-unicode-character-format-to-import-or-export-data-sql-server.md).  
  
 **-x**  
 Si se usa con las opciones **format** y **-f**_format_file_, se genera un archivo de formato basado en XML en lugar del archivo de formato predeterminado que no es XML. 
  **-x** no funciona cuando se importan o exportan datos. Genera un error si se usa sin **format** ni **-f**_format_file_.  
  
## <a name="remarks"></a>Observaciones  
 El cliente **BCP** 12,0 se instala al instalar [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] las herramientas de. Si se instalan herramientas para [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] y para una versión anterior de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)], según el valor de la variable de entorno PATH, es posible usar el cliente **bcp** anterior en lugar del cliente **bcp** 12.0. Esta variable de entorno define el conjunto de directorios que Windows usa para buscar archivos ejecutables. Para saber qué versión está usando, ejecute el comando **bcp /v** en el símbolo del sistema de Windows. Para obtener información acerca del establecimiento de la ruta de comandos en la variable de entorno PATH, vea la Ayuda de Windows.  
  
 Los archivos con formato XML solamente se admiten cuando se instalan herramientas de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] con [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Native Client.  
  
 Para obtener más información sobre dónde encontrar o cómo ejecutar la utilidad **bcp** y sobre las convenciones de sintaxis de las utilidades del símbolo del sistema, vea [Referencia de la utilidad del símbolo del sistema &#40;motor de base de datos&#41;](../tools/command-prompt-utility-reference-database-engine.md).  
  
 Para obtener más información sobre cómo preparar datos para operaciones de importación y exportación en bloque, vea [Preparar los datos para exportar o importar en bloque &#40;SQL Server&#41;](../relational-databases/import-export/prepare-data-for-bulk-export-or-import-sql-server.md).  
  
 Para obtener más información sobre cuándo se incluyen en el registro de transacciones las operaciones de inserción de filas que se efectúan durante una importación en bloque, vea [Requisitos previos para el registro mínimo durante la importación en bloque](../relational-databases/import-export/prerequisites-for-minimal-logging-in-bulk-import.md).  
  
## <a name="native-data-file-support"></a>Compatibilidad de los archivos de datos nativos  
 En [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)], la **utilidad BCP** admite archivos de datos nativos compatibles [!INCLUDE[ssVersion2000](../includes/ssversion2000-md.md)]con [!INCLUDE[ssVersion2005](../includes/ssversion2005-md.md)], [!INCLUDE[ssKatmai](../includes/sskatmai-md.md)], [!INCLUDE[ssKilimanjaro](../includes/sskilimanjaro-md.md)], y [!INCLUDE[ssSQL11](../includes/sssql11-md.md)].  
  
## <a name="computed-columns-and-timestamp-columns"></a>Columnas calculadas y columnas de marca de tiempo  
 Los valores del archivo de datos que se importa para las columnas calculadas o `timestamp` se omiten y [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] asigna valores automáticamente. Si el archivo de datos no contiene valores para las columnas calculadas o `timestamp` de la tabla, utilice un archivo de formato para especificar que deben pasarse por alto las columnas calculadas o `timestamp` de la tabla al importar datos; [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] asigna valores para la columna de forma automática.  
  
 Las columnas calculadas y `timestamp` se copian de forma masiva desde [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] en un archivo de datos de la forma habitual.  
  
## <a name="specifying-identifiers-that-contain-spaces-or-quotation-marks"></a>Especificar identificadores que incluyen espacios o comillas  
 
  [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] pueden incluir caracteres tales como espacios insertados y comillas. Tales identificadores deben tratarse de la siguiente manera:  
  
-   Cuando especifique un identificador o nombre de archivo que incluya un espacio o comillas en el símbolo del sistema, coloque el identificador entre comillas dobles (" ").  
  
     Por ejemplo, el siguiente comando `bcp out` crea un archivo de datos denominado `Currency Types.dat`:  
  
    ```  
    bcp AdventureWorks2012.Sales.Currency out "Currency Types.dat" -T -c  
    ```  
  
-   Para especificar un nombre de base de datos que contenga un espacio o comillas, debe usar la opción `-q`.  
  
-   Para los nombres de vista, tabla o propietario que contienen espacios insertados o comillas, puede hacer lo siguiente:  
  
    -   Especificar la opción `-q`, o bien  
  
    -   Incluir el nombre de vista, tabla o propietario entre corchetes ([]) dentro de las comillas.  
  
## <a name="data-validation"></a>Validación de datos  
 **BCP** ahora aplica la validación de datos y las comprobaciones de datos que podrían provocar errores en los scripts si se ejecutan en datos no válidos en un archivo de datos. Por ejemplo, **bcp** ahora comprueba que:  
  
-   La representación nativa de los tipos de datos `float` o `real` es válida.  
  
-   Los datos Unicode tienen una longitud de bytes uniforme.  
  
 Es posible que los formularios de datos no válidos que podían importarse de forma masiva en versiones anteriores de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] no se carguen ahora, mientras que, en anteriores versiones, el error no se producía hasta que un cliente intentaba tener acceso a datos no válidos. La validación agregada evita sorpresas cuando se consultan los datos después de una carga masiva.  
  
## <a name="bulk-exporting-or-importing-sqlxml-documents"></a>Exportación o importación masiva de documentos SQLXML  
 Para importar o exportar de forma masiva datos SQLXML, utilice uno de los tipos de datos siguientes en el archivo de formato.  
  
|Tipo de datos|Efecto|  
|---------------|------------|  
|SQLCHAR o SQLVARYCHAR|Los datos se envían a la página de códigos del cliente o a la página de códigos implícita por la intercalación. Tiene el mismo efecto que especificar el modificador `-c` sin indicar un archivo de formato.|  
|SQLNCHAR o SQLNVARCHAR|Los datos se envían como datos Unicode. Tiene el mismo efecto que especificar el modificador `-w` sin indicar un archivo de formato.|  
|SQLBINARY o SQLVARYBIN|Los datos se envían sin realizar ninguna conversión.|  
  
## <a name="permissions"></a>Permisos  
 Una operación **bcpout** requiere permisos SELECT en la tabla de origen.  
  
 Una operación **bcpin**requiere como mínimo permisos SELECT/INSERT en la tabla de destino. Además, se requiere el permiso ALTER TABLE si cualquiera de las siguientes afirmaciones es verdadera:  
  
-   Existen restricciones y la sugerencia CHECK_CONSTRAINTS no se ha especificado.  
  
    > [!NOTE]  
    >  La deshabilitación de restricciones es el comportamiento predeterminado. Para habilitar las restricciones de forma explícita, use la opción **-h** con la sugerencia CHECK_CONSTRAINTS.  
  
-   Existen desencadenadores y la sugerencia FIRE_TRIGGER no se ha especificado.  
  
    > [!NOTE]  
    >  De forma predeterminada, los desencadenadores no se activan. Para activarlos de forma explícita, use la opción **-h** con la sugerencia FIRE_TRIGGERS.  
  
-   La opción **-E** se usa para importar valores de identidad de un archivo de datos.  
  
> [!NOTE]  
>  El requisito del permiso ALTER TABLE en la tabla de destino era nuevo en [!INCLUDE[ssVersion2005](../includes/ssversion2005-md.md)]. Este nuevo requisito podría hacer que los scripts de **bcp** que no exigen las comprobaciones de restricciones y desencadenadores devuelvan un error si la cuenta de usuario no tiene los permisos de tabla ALTER para la tabla de destino.  
  
## <a name="character-mode--c-and-native-mode--n-best-practices"></a>Prácticas recomendadas para el modo de carácter (-c) y el modo nativo (-n)  
 Esta sección contiene recomendaciones para el modo de carácter (-c) y el modo nativo (-n).  
  
-   (Administrador o usuario) Cuando sea posible, utilice el formato nativo (-n) para evitar problemas de separador. Utilice el formato nativo para exportar e importar utilizando [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]. Exporte datos de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] utilizando la opción -c o -w si los datos se van a importar a una base de datos que no es de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)].  
  
-   (Administrador) Compruebe los datos al utilizar BCP OUT. Por ejemplo, cuando se utiliza BCP OUT, BCP IN y luego BCP OUT, compruebe que los datos se han exportado correctamente y que los valores de terminador no se utilizan como parte de algún valor de datos. Considere la posibilidad de reemplazar los terminadores predeterminados (utilizando las opciones -t y -r) por valores hexadecimales aleatorios para evitar conflictos entre los valores de terminador y los valores de datos.  
  
-   (Usuario) Utilice un terminador largo y único (cualquier secuencia de bytes o caracteres) para minimizar la posibilidad de conflicto con el valor de cadena real. Esto se puede realizar utilizando las opciones -t y -r.  
  
## <a name="examples"></a>Ejemplos  
 En esta sección se incluyen los ejemplos siguientes:  
  
-   A. Copiar filas de tablas en un archivo de datos (con una conexión de confianza)  
  
-   B. Copiar filas de tablas en un archivo de datos (con autenticación de modo mixto)  
  
-   C. Copiar datos de un archivo en una tabla  
  
-   D. Copiar una columna específica en un archivo de datos  
  
-   E. Copiar una fila específica en un archivo de datos  
  
-   F. Copiar datos de una consulta en un archivo de datos  
  
-   G. Crear un archivo de formato no XML  
  
-   H. Crear un archivo de formato XML  
  
-   I. Usar un archivo de formato para importar de forma masiva con **bcp**  
  
### <a name="a-copying-table-rows-into-a-data-file-with-a-trusted-connection"></a>A. Copiar filas de tablas en un archivo de datos (con una conexión de confianza)  
 En el siguiente ejemplo se ilustra la opción **out** de la tabla `AdventureWorks2012.Sales.Currency` . En este ejemplo se crea un archivo de datos con el nombre `Currency.dat` y se usa el formato de caracteres para copiar los datos de la tabla en ese archivo. En el ejemplo se supone que usa la autenticación de Windows y que existe una conexión de confianza con la instancia del servidor en la que se ejecuta el comando **bcp** .  
  
 En el símbolo del sistema, escriba el siguiente comando:  
  
```  
bcp AdventureWorks2012.Sales.Currency out Currency.dat -T -c  
```  
  
### <a name="b-copying-table-rows-into-a-data-file-with-mixed-mode-authentication"></a>B. Copiar filas de tablas en un archivo de datos (con autenticación de modo mixto)  
 En el siguiente ejemplo se ilustra la opción **out** de la tabla `AdventureWorks2012.Sales.Currency` . En este ejemplo se crea un archivo de datos con el nombre `Currency.dat` y se usa el formato de caracteres para copiar los datos de la tabla en ese archivo.  
  
 En el ejemplo se da por hecho que usa la autenticación de modo mixto; hay que usar el modificador **-U** para especificar su identificador de inicio de sesión. Además, a menos que se esté conectando a la instancia predeterminada de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] en el equipo local, use el modificador **-S** para especificar el nombre del sistema y, opcionalmente, un nombre de instancia.  
  
```  
bcp AdventureWorks2012.Sales.Currency out Currency.dat -c -U<login_id> -S<server_name\instance_name>  
```  
  
 El sistema le solicitará la contraseña.  
  
### <a name="c-copying-data-from-a-file-to-a-table"></a>C. Copiar datos de un archivo en una tabla  
 En el siguiente ejemplo se ilustra la opción **in** y se usa el archivo creado en el ejemplo anterior (`Currency.dat`). No obstante, en primer lugar, este ejemplo crea una copia vacía de la tabla de `AdventureWorks2012 Sales.Currency`, `Sales.Currency2`, en la que se copian los datos. En el ejemplo se supone que usa la autenticación de Windows y que existe una conexión de confianza con la instancia del servidor en la que se ejecuta el comando **bcp** .  
  
 Para crear la tabla vacía, en el Editor de consultas, escriba el siguiente comando:  
  
```  
USE AdventureWorks2012;  
GO  
SELECT * INTO AdventureWorks2012.Sales.Currency2   
FROM AdventureWorks2012.Sales.Currency WHERE 1=2;  
```  
  
 Para realizar una copia masiva de los datos de caracteres en la nueva tabla, es decir, para importar los datos, escriba el siguiente comando en un símbolo del sistema:  
  
```  
bcp AdventureWorks2012.Sales.Currency2 in Currency.dat -T -c  
```  
  
 Para comprobar que el comando se ha ejecutado correctamente, muestre el contenido en el Editor de consultas y escriba:  
  
```  
USE AdventureWorks2012;  
GO  
SELECT * FROM Sales.Currency2  
```  
  
### <a name="d-copying-a-specific-column-into-a-data-file"></a>D. Copiar una columna específica en un archivo de datos  
 Para copiar una columna específica, puede usar la opción **queryout** . El siguiente ejemplo copia únicamente la columna `Name` de la tabla `Sales.Currency` en un archivo de datos. En el ejemplo se supone que usa la autenticación de Windows y que existe una conexión de confianza con la instancia del servidor en la que se ejecuta el comando **bcp** .  
  
 En el símbolo del sistema de Windows, escriba:  
  
```  
bcp "SELECT Name FROM AdventureWorks.Sales.Currency" queryout Currency.Name.dat -T -c  
```  
  
### <a name="e-copying-a-specific-row-into-a-data-file"></a>E. Copiar una fila específica en un archivo de datos  
 Para copiar una fila específica, puede usar la opción **queryout** . En el siguiente ejemplo se copia únicamente la fila relativa al contacto denominado `Jarrod Rana` desde la tabla `AdventureWorks2012.Person.Person` en un archivo de datos (`Jarrod Rana.dat`). En el ejemplo se da por hecho que usa la autenticación de Windows y que existe una conexión de confianza con la instancia de servidor en la que se ejecuta el comando **bcp**.  
  
 En el símbolo del sistema de Windows, escriba:  
  
```  
bcp "SELECT * FROM AdventureWorks2012.Person.Person WHERE FirstName='Jarrod' AND LastName='Rana' "  queryout "Jarrod Rana.dat" -T -c  
```  
  
### <a name="f-copying-data-from-a-query-to-a-data-file"></a>F. Copiar datos de una consulta en un archivo de datos  
 Para copiar el conjunto de resultados de una instrucción [!INCLUDE[tsql](../includes/tsql-md.md)] en un archivo de datos, use la opción **queryout** . El siguiente ejemplo copia los nombres de la tabla de `AdventureWorks2012.Person.Person` , ordenados por el apellido y después por el nombre, en el archivo de datos `Contacts.txt` . En el ejemplo se supone que usa la autenticación de Windows y que existe una conexión de confianza con la instancia del servidor en la que se ejecuta el comando **bcp** .  
  
 En el símbolo del sistema de Windows, escriba:  
  
```  
bcp "SELECT FirstName, LastName FROM AdventureWorks2012.Person.Person ORDER BY LastName, Firstname" queryout Contacts.txt -c -T  
```  
  
### <a name="g-creating-a-non-xml-format-file"></a>G. Crear un archivo de formato no XML  
 En el siguiente ejemplo se crea un archivo de formato no XML, `Currency.fmt`, para la tabla `Sales.Currency` de la base de datos [!INCLUDE[ssSampleDBobject](../includes/sssampledbobject-md.md)]. En el ejemplo se supone que usa la autenticación de Windows y que existe una conexión de confianza con la instancia del servidor en la que se ejecuta el comando **bcp** .  
  
 En el símbolo del sistema de Windows, escriba:  
  
```  
bcp AdventureWorks2012.Sales.Currency format nul -T -c  -f Currency.fmt  
```  
  
 Para obtener más información, vea [Archivos de formato no XML &#40;SQL Server&#41;](../relational-databases/import-export/xml-format-files-sql-server.md).  
  
### <a name="h-creating-an-xml-format-file"></a>H. Crear un archivo de formato XML  
 El siguiente ejemplo crea un archivo de formato XML con el nombre `Currency.xml` para la tabla `Sales.Currency` de la base de datos [!INCLUDE[ssSampleDBobject](../includes/sssampledbobject-md.md)] . En el ejemplo se supone que usa la autenticación de Windows y que existe una conexión de confianza con la instancia del servidor en la que se ejecuta el comando **bcp** .  
  
 En el símbolo del sistema de Windows, escriba:  
  
```  
bcp AdventureWorks2012.Sales.Currency format nul -T -c -x -f Currency.xml  
```  
  
> [!NOTE]  
>  Para usar el modificador **-x**, debe contar con un cliente **bcp** 9.0. Para obtener información acerca de cómo usar el cliente **bcp** 9.0, consulte la sección "Comentarios".  
  
 Para obtener más información, vea [XML, archivos de formato &#40;SQL Server&#41;](../relational-databases/import-export/xml-format-files-sql-server.md).  
  
### <a name="i-using-a-format-file-to-bulk-import-with-bcp"></a>I. Usar un archivo de formato para importar de forma masiva con bcp  
 Para usar un archivo de formato creado anteriormente al importar datos a una instancia de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)], use el modificador **-f** con la opción **in**. Por ejemplo, el siguiente comando copia de forma masiva el contenido de un archivo de datos, `Currency.dat`, en una copia de la tabla `Sales.Currency` (`Sales.Currency2`) mediante el archivo de formato creado anteriormente (`Currency.xml`). En el ejemplo se supone que usa la autenticación de Windows y que existe una conexión de confianza con la instancia del servidor en la que se ejecuta el comando **bcp** .  
  
 En el símbolo del sistema de Windows, escriba:  
  
```  
bcp AdventureWorks2012.Sales.Currency2 in Currency.dat -T -f Currency.xml  
```  
  
> [!NOTE]  
>  Los archivos de formato son útiles cuando los campos del archivo de datos son diferentes a los de las columnas de la tabla; por ejemplo, en su numeración, orden o tipos de datos. Para obtener más información, vea [Archivos de formato para importar o exportar datos &#40;SQL Server&#41;](../relational-databases/import-export/format-files-for-importing-or-exporting-data-sql-server.md).  
  
## <a name="additional-examples"></a>Otros ejemplos  
 Los siguientes temas incluyen ejemplos de uso de **bcp**:  
  
-   [Crear un archivo de formato &#40;SQL Server&#41;](../relational-databases/import-export/create-a-format-file-sql-server.md)  
  
-   [Ejemplos de importación y exportación en bloque de documentos XML &#40;SQL Server&#41;](../relational-databases/import-export/examples-of-bulk-import-and-export-of-xml-documents-sql-server.md)  
  
-   [Mantener los valores de identidad al importar datos de forma masiva &#40;SQL Server&#41;](../relational-databases/import-export/keep-identity-values-when-bulk-importing-data-sql-server.md)  
  
-   [Mantener valores NULL o usar valores predeterminados durante la importación en bloque &#40;SQL Server&#41;](../relational-databases/import-export/keep-nulls-or-use-default-values-during-bulk-import-sql-server.md)  
  
-   [Especificar terminadores de campo y de fila &#40;SQL Server&#41;](../relational-databases/import-export/specify-field-and-row-terminators-sql-server.md)  
  
-   [Usar un archivo de formato para importar datos en bloque &#40;SQL Server&#41;](../relational-databases/import-export/use-a-format-file-to-bulk-import-data-sql-server.md)  
  
-   [Usar el formato de caracteres para importar o exportar datos &#40;SQL Server&#41;](../relational-databases/import-export/use-character-format-to-import-or-export-data-sql-server.md)  
  
-   [Usar el formato nativo para importar o exportar datos &#40;SQL Server&#41;](../relational-databases/import-export/use-native-format-to-import-or-export-data-sql-server.md)  
  
-   [Usar el formato de caracteres Unicode para importar o exportar datos &#40;SQL Server&#41;](../relational-databases/import-export/use-unicode-character-format-to-import-or-export-data-sql-server.md)  
  
-   [Usar el formato nativo Unicode para importar o exportar datos &#40;SQL Server&#41;](../relational-databases/import-export/use-unicode-native-format-to-import-or-export-data-sql-server.md)  
  
## <a name="see-also"></a>Consulte también  
 [Preparar los datos para exportar o &#40;importar de forma masiva SQL Server&#41;](../relational-databases/import-export/prepare-data-for-bulk-export-or-import-sql-server.md)   
 [BULK INSERT &#40;Transact-SQL&#41;](/sql/t-sql/statements/bulk-insert-transact-sql)   
 [OPENROWSET &#40;Transact-SQL&#41;](/sql/t-sql/functions/openrowset-transact-sql)   
 [ESTABLECER QUOTED_IDENTIFIER &#40;&#41;de Transact-SQL](/sql/t-sql/statements/set-quoted-identifier-transact-sql)   
 [sp_configure &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-configure-transact-sql)   
 [sp_tableoption &#40;&#41;de Transact-SQL](/sql/relational-databases/system-stored-procedures/sp-tableoption-transact-sql)   
 [Archivos de formato para importar o exportar datos &#40;SQL Server&#41;](../relational-databases/import-export/format-files-for-importing-or-exporting-data-sql-server.md)  
  
  
