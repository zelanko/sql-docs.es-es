---
title: Cargador de línea de comandos de dwloader
description: dwloader es una herramienta de línea de comandos de almacenamiento de datos paralelos (PDW) que carga masivamente filas de tabla en una tabla existente.
author: mzaman1
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.custom: seo-dt-2019
ms.openlocfilehash: 7dd0ccf960b53b3cd1b474f61c60a58ff9b0a2c6
ms.sourcegitcommit: 7345e4f05d6c06e1bcd73747a4a47873b3f3251f
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/24/2020
ms.locfileid: "88767054"
---
# <a name="dwloader-command-line-loader-for-parallel-data-warehouse"></a>Cargador de línea de comandos de dwloader para almacenamiento de datos paralelos
**dwloader** es una herramienta de línea de comandos de almacenamiento de datos paralelos (PDW) que carga masivamente filas de tabla en una tabla existente. Al cargar filas, puede agregar todas las filas al final de la tabla (modo*Append* o *modo fastappend*), anexar nuevas filas y actualizar las filas existentes (*modo Upsert*) o eliminar todas las filas existentes antes de cargarlas y, a continuación, insertar todas las filas en una tabla vacía (*modo de recarga*).  
  
**Proceso de carga de datos**  
  
1.  Prepare los datos de origen.  
  
    Use su propio proceso ETL para crear los datos de origen que desea cargar. Se debe dar formato a los datos de origen para que coincidan con el esquema de la tabla de destino. Almacene los datos de origen en uno o varios archivos de texto y copie los archivos de texto en el mismo directorio del servidor de carga. Para obtener información sobre el servidor de carga, consulte [adquisición y configuración de un servidor de carga](acquire-and-configure-loading-server.md) .  
  
2.  Preparar las opciones de carga.  
  
    Decida qué opciones de carga usará. Almacene las opciones de carga en un archivo de configuración. Copie el archivo de configuración en una ubicación local en el servidor de carga. En este tema se describen las opciones de configuración de **dwloader** .  
  
3.  Preparar las opciones de error de carga.  
  
    Decida cómo desea que **dwloader** controle las filas que no se cargan. Para realizar la carga, **dwloader** primero carga los datos en una tabla de ensayo y, a continuación, transfiere los datos a la tabla de destino. A medida que el cargador carga los datos en la tabla de ensayo, realiza un seguimiento del número de filas que no se cargan. Por ejemplo, las filas que no tengan el formato correcto no se cargarán. Las filas con errores se copian en un archivo de rechazo. De forma predeterminada, la carga se anula después del primer rechazo a menos que especifique un umbral de rechazo diferente.  
  
4.  Instale **dwloader**.  
  
    Instale dwloader en el servidor de carga si aún no está instalado. 

<!-- MISSING LINK
    See [Install dwloader Command-Line Loader &#40;SQL Server PDW&#41;](install-dwloader-command-line-loader-sql-server-pdw.md). 
--> 
  
5.  Ejecute **dwloader**.  
  
    Inicie sesión en el servidor de carga y ejecute el **dwloader.exe** ejecutable con las opciones de línea de comandos adecuadas.  
  
6.  Compruebe los resultados.  
  
    Puede comprobar el archivo de filas con errores (especificado con-R) para ver si no se cargó ninguna fila. Si este archivo está vacío, se cargan todas las filas correctamente. **dwloader** es transaccional, por lo que si se produce un error en algún paso (excepto las filas rechazadas), todos los pasos se revertirán a su estado inicial.  
  
<!-- 
![Topic link icon](media/topic-link.gif "Topic_Link")[Syntax Conventions](syntax-conventions-sql-server-pdw.md)  
-->  


## <a name="syntax"></a>Sintaxis  
  
```  
dwloader.exe { -h }  
  
dwloader.exe   
    {  
        { -U login_name  -P password  }  
        | -W  
    }  
    [ -f parameter_file ]  
    [ -S target_appliance ]  
    { -T target_database_name . [ schema ] . table_name }   
    { -i source_data_location } [ <source_data_options> ]  
    { -R load_failure_file_name } [ <load_failure_options> ]  
    [ <loading_options> ]  
}  
  
<source_data_options> ::=  
{  
    [ -fh number_header_rows ]  
    [ < variable_length_column_options > | < fixed_width_column_options > ]  
    [ -D { mdy | myd | ymd | ydm | dmy | dym | custom_date_format } ]  
    [ -dt datetime_format_file ]  
}  
  
<variable_length_column_options> ::=  
{  
    [ -e character_encoding ]  
    -r row_delimiter   
    [ -s string_delimiter ]  
    -t field_delimiter   
}  
  
<fixed_width_column_options> ::=  
{  
    -w fixed_width_config_file   
    [ -e character_encoding ]   
    -r row_delimiter   
}  
  
<load_failure_options> ::=  
{  
    [ -rt { value | percentage } ]  
    [ -rv reject_value ]  
    [ -rs reject_sample_value ]  
}  
  
<loading_options> ::=  
{  
    [ -d staging_database_name ]  
    [ -M { append | fastappend | upsert -K merge_column [ ,...n ] | reload } ]  
    [ -b batchsize ]   
    [ -c ]  
    [ -E ]  
    [ -m ]  
    [ -N ]  
    [ -se ]
    [ -l ]   
}  
```  
  
## <a name="arguments"></a>Argumentos  
**-h**  
Muestra información de ayuda sencilla sobre el uso del cargador. La ayuda solo muestra si no se especifica ningún otro parámetro de línea de comandos.  
  
**-U** *login_name*  
Un inicio de sesión de autenticación de SQL Server válido con los permisos adecuados para realizar la carga.  
  
**-P** *password*  
La contraseña de un *login_name*de autenticación de SQL Server.  
  
**-W**  
Usa la autenticación de Windows. (No se requiere *login_name* ni la *contraseña* ). 

<!-- MISSING LINK
For information about configuring Windows Authentication, see [Security - Configure Domain Trusts](security-configure-domain-trusts.md).  
-->
  
**-f** *parameter_file_name*  
Use un archivo de parámetros, *parameter_file_name*, en lugar de los parámetros de línea de comandos. *parameter_file_name* puede contener cualquier parámetro de línea de comandos excepto *user_name* y *contraseña*. Si se especifica un parámetro en la línea de comandos y en el archivo de parámetros, la línea de comandos invalida el parámetro de archivo.  
  
El archivo de parámetros contiene un parámetro, sin el **-** prefijo, por línea.  
  
Ejemplo:  
  
`rt=percentage`  
  
`rv=25`  
  
**-S** *target_appliance*  
Especifica el dispositivo PDW de SQL Server que recibirá los datos cargados.  
  
*En el caso de las conexiones de InfiniBand*, *target_appliance* se especifica como <nombre del dispositivo>-SQLCTL01. Para configurar esta conexión con nombre, consulte [configuración de adaptadores de red InfiniBand](configure-infiniband-network-adapters.md).  
  
En el caso de las conexiones Ethernet, *target_appliance* es la dirección IP del clúster de nodo de control.  
  
Si se omite, dwloader toma como valor predeterminado el valor que se especificó al instalar dwloader. 

<!-- MISSING LINK
For more information about this install option, see [Install dwloader Command-Line Loader](install-dwloader.md).  
-->
  
**-T** *target_database_name.* [*esquema*]. *TABLE_NAME*  
Nombre de tres partes de la tabla de destino.  
  
**-I** *source_data_location*  
Ubicación de uno o más archivos de código fuente que se van a cargar. Cada archivo de código fuente debe ser un archivo de texto o un archivo de texto comprimido con gzip. Solo se puede comprimir un archivo de código fuente en cada archivo gzip.  
  
Para dar formato a un archivo de código fuente:  
  
-   El archivo de código fuente debe tener el formato de acuerdo con las opciones de carga.  
  
-   Cada línea de un archivo de código fuente contiene los datos de una fila de la tabla. Los datos de origen deben coincidir con el esquema de la tabla de destino. El orden de las columnas y los tipos de datos también deben coincidir. Cada campo de la fila representa una columna de la tabla de destino.  
  
-   De forma predeterminada, los campos son de longitud variable y están separados por un delimitador. Para especificar el tipo de delimitador, use las opciones de la línea de comandos> variable_length_column_options de <. Para especificar los campos de longitud fija, utilice las opciones de la línea de comandos> fixed_width_column_options de <.  
  
Para especificar la ubicación de los datos de origen:  
  
-   La ubicación de los datos de origen puede ser una ruta de acceso de red o una ruta de acceso local a un directorio en el servidor de carga.  
  
-   Para especificar todos los archivos de un directorio, escriba la ruta de acceso del directorio seguida del carácter comodín *.  El cargador no carga archivos de ningún subdirectorio que estén en la ubicación de los datos de origen. El cargador produce errores cuando un directorio existe en un archivo gzip.  
  
-   Para especificar algunos de los archivos de un directorio, use una combinación de caracteres y el carácter comodín *.  
  
Para cargar varios archivos con un comando:  
  
-   Todos los archivos deben existir en el mismo directorio.  
  
-   Los archivos deben estar en todos los archivos de texto, en todos los archivos gzip o en una combinación de archivos de texto y gzip.  
  
-   Ninguno de los archivos puede contener información de encabezado.  
  
-   Todos los archivos deben usar el mismo tipo de codificación de caracteres. Consulte la opción-e.  
  
-   Todos los archivos se deben cargar en la misma tabla.  
  
-   Todos los archivos se concatenarán y se cargarán como si fueran un archivo, y las filas rechazadas Irán a un solo archivo de rechazo.  
  
Ejemplo:  
  
-   -i \\ \loadserver\loads\daily \\ *. gz  
  
-   -i \\ \loadserver\loads\daily \\ *. txt  
  
-   -i \\ \loadserver\loads\daily\monday. *  
  
-   -i \\\loadserver\loads\daily\monday.txt  
  
-   -i \\ \loadserver\loads\daily\\*  
  
**-R** *load_failure_file_name*  
Si hay errores de carga, **dwloader** almacena la fila que no se pudo cargar y la descripción del error en un archivo denominado *load_failure_file_name*. Si este archivo ya existe, dwloader sobrescribirá el archivo existente. *load_failure_file_name* se crea cuando se produce el primer error. Si todas las filas se cargan correctamente, no se crea *load_failure_file_name* .  
  
**-fh** *number_header_rows*  
Número de líneas (filas) que se van a omitir al principio de *source_data_file_name*. El valor predeterminado es 0.  
  
<variable_length_column_options>  
Opciones de un *source_data_file_name* que tiene columnas de longitud variable delimitada por caracteres. De forma predeterminada, *source_data_file_name* contiene caracteres ASCII en columnas de longitud variable.  
  
En el caso de los archivos ASCII, los valores NULL se representan mediante la colocación consecutiva de los delimitadores. Por ejemplo, en un archivo delimitado por canalización ("|"), un valor NULL se indica mediante "| |". En un archivo delimitado por comas, un valor NULL se indica mediante ",,". Además, se debe especificar la opción **-E** (--emptyStringAsNull). Para obtener más información sobre-E, vea a continuación.  
  
**-e** *character_encoding*  
Especifica un tipo de codificación de caracteres para los datos que se van a cargar desde el archivo de datos. Las opciones son ASCII (predeterminado), UTF8, UTF16 o UTF16BE, donde UTF16 es little endian y UTF16BE es big endian. Estas opciones no distinguen mayúsculas de minúsculas.  
  
**-t** *field_delimiter*  
Delimitador para cada campo (columna) de la fila. El delimitador de campo es uno o varios de estos caracteres de escape ASCII o valores hexadecimales ASCII.  
  
|Nombre|Carácter de escape|Carácter Hex|  
|--------|--------------------|-----------------|  
|Pestaña|\t|0x09|  
|Retorno de carro (CR)|\r|0x0D|  
|Avance de línea (LF)|\n|STOP|  
|CRLF|\r\n|0x0d0x0a|  
|Coma|','|0x2c|  
|Comilla doble|\\"|0x22|  
|Comilla simple|\\'|0x27|  
  
Para especificar el carácter de barra vertical en la línea de comandos, escríbalo entre comillas dobles, "|". Esto evitará que el analizador de la línea de comandos interprete erróneamente. Otros caracteres se incluyen entre comillas simples.  
  
Ejemplo:  
  
-t "|"  
  
-t ' '  
  
-t 0x0A  
  
-t \t  
  
-t ' ~ | ~ '  
  
**-r** *row_delimiter*  
Delimitador de cada fila del archivo de datos de origen. El delimitador de filas es uno o más valores ASCII.  
  
Para especificar un carácter de retorno de carro (CR), avance de la letra (LF) o un carácter de tabulación como delimitador, puede usar los caracteres de escape (\r, \n, \t) o sus valores hexadecimales (0x, 0d, 09). Para especificar cualquier otro carácter especial como delimitadores, use su valor hexadecimal.  
  
Ejemplos de CR + LF:  
  
-r \r\n  
  
-r 0x0d0x0a  
  
Ejemplos de CR:  
  
-r \r  
  
-r 0x0D  
  
Ejemplos de LF:  
  
-r \n  
  
-r 0x0A  
  
Se requiere un LF para UNIX. Se requiere un CR para Windows.  
  
**-s** *string_delimiter*  
El delimitador para el campo de tipo de datos de cadena de un archivo de entrada delimitado por texto. El delimitador de cadena es uno o más valores ASCII.  Se puede especificar como un carácter (por ejemplo,-s *) o como un valor hexadecimal (por ejemplo,-s 0x22 para una comilla doble).  
  
Ejemplo:  
  
seg  
  
-s 0x22  
  
< fixed_width_column_options>  
Opciones de un archivo de datos de origen que tiene columnas de longitud fija. De forma predeterminada, *source_data_file_name* contiene caracteres ASCII en columnas de longitud variable.  
  
Las columnas de ancho fijo no se admiten cuando-e es UTF8.  
  
**-w** *fixed_width_config_file*  
Ruta de acceso y nombre del archivo de configuración que especifica el número de caracteres de cada columna. Se debe especificar cada campo.  
  
Este archivo debe residir en el servidor de carga. La ruta de acceso puede ser una ruta de acceso UNC, relativa o absoluta. Cada línea de *fixed_width_config_file* contiene el nombre de una columna y el número de caracteres de dicha columna. Hay una línea por columna, como se indica a continuación, y el orden del archivo debe coincidir con el orden de la tabla de destino:  
  
*column_name* = *num_chars*  
  
*column_name* = *num_chars*  
  
Ejemplo de archivo de configuración de ancho fijo:  
  
SalesCode = 3  
  
SalesID = 10  
  
Líneas de ejemplo en *source_data_file_name*:  
  
230Shirts0056  
  
320Towels1356  
  
En el ejemplo anterior, la primera fila cargada tendrá SalesCode = ' 230 ' y SalesID = ' Shirts0056 '. La segunda fila cargada tendrá SalesCode = ' 320 ' y SaleID = ' Towels1356 '.  
  
Para obtener información sobre cómo controlar los espacios iniciales y finales o la conversión de tipos de datos en el modo de ancho fijo, vea [reglas de conversión de tipos de datos para dwloader](dwloader-data-type-conversion-rules.md).  
  
**-e** *character_encoding*  
Especifica un tipo de codificación de caracteres para los datos que se van a cargar desde el archivo de datos. Las opciones son ASCII (predeterminado), UTF8, UTF16 o UTF16BE, donde UTF16 es little endian y UTF16BE es big endian. Estas opciones no distinguen mayúsculas de minúsculas.  
  
Las columnas de ancho fijo no se admiten cuando-e es UTF8.  
  
**-r** *row_delimiter*  
Delimitador de cada fila del archivo de datos de origen. El delimitador de filas es uno o más valores ASCII.  
  
Para especificar un carácter de retorno de carro (CR), avance de la letra (LF) o un carácter de tabulación como delimitador, puede usar los caracteres de escape (\r, \n, \t) o sus valores hexadecimales (0x, 0d, 09). Para especificar cualquier otro carácter especial como delimitadores, use su valor hexadecimal.  
  
Ejemplos de CR + LF:  
  
-r \r\n  
  
-r 0x0d0x0a  
  
Ejemplos de CR:  
  
-r \r  
  
-r 0x0D  
  
Ejemplos de LF:  
  
-r \n  
  
-r 0x0A  
  
Se requiere un LF para UNIX. Se requiere un CR para Windows.  
  
**-D** { **AMD** \| ydm \| MDA \| Mad \| DMY \| Dam \| *custom_date_format* }  
Especifica el orden de mes (m), día (d) y año (y) de todos los campos de fecha y hora del archivo de entrada. El orden predeterminado es AMD. Para especificar varios formatos de orden para el mismo archivo de código fuente, use la opción-DT.  
  
AMD \| DMY  
ydm y DMY permiten los mismos formatos de entrada. Ambos permiten que el año esté al principio o al final de la fecha. Por ejemplo, para los formatos de fecha **ydm** y **DMY** , podría tener 2013-02-03 o 02-03-2013 en el archivo de entrada.  
  
ydm  
Solo puede cargar entradas con formato de ydm en columnas de tipo de datos datetime y smalldatetime. No se pueden cargar valores de ydm en una columna de tipo de datos datetime2, Date o DateTimeOffset.  
  
mdy  
MDA permite \<month> \<space> \<day> \<comma> \<year> .  
  
Ejemplos de datos de entrada de MDA para el 1 de enero de 1975:  
  
-   1 de enero de 1975  
  
-   01 de enero de 75  
  
-   Jan/1/75  
  
-   01011975  
  
mad  
Ejemplos de archivos de entrada del 4 de marzo de 2010:03-2010-04, 3/2010/4  
  
dam  
Ejemplos de archivos de entrada de marzo de 2004, 2010:04-2010-03, 4/2010/3  
  
*custom_date_format*  
*custom_date_format* es un formato de fecha personalizado (por ejemplo, mm/dd/aaaa) y se incluye únicamente por razones de compatibilidad con versiones anteriores. dwloader no aplica el formato de fecha personalizado. En su lugar, cuando se especifica un formato de fecha personalizado, **dwloader** lo convertirá en la configuración correspondiente de AMD, ydm, MDA, Mad, Dam o DMY.  
  
Por ejemplo, si especifica-D MM/DD/AAAA, dwloader espera que todas las entradas de fecha se ordenen con el mes primero, después con el día y después con el año (MDA). No aplica los meses de 2 caracteres, los días de 2 dígitos y los años de 4 dígitos tal como se especifica en el formato de fecha personalizado. Estos son algunos ejemplos de formas en las que se puede dar formato a las fechas en el archivo de entrada cuando el formato de fecha es-D MM/DD/AAAA: 01/02/2013, Ene. 02.2013, 1/2/2013  
  
Para obtener información de formato más completa, vea [reglas de conversión de tipos de datos para dwloader](dwloader-data-type-conversion-rules.md).  
  
**-dt** *datetime_format_file*  
Cada formato de fecha y hora se especifica en un archivo denominado *datetime_format_file*. A diferencia de los parámetros de línea de comandos, los parámetros de archivo que incluyen espacios no deben incluirse entre comillas dobles. No se puede modificar el formato de fecha y hora mientras se cargan los datos. El archivo de datos de origen y su columna correspondiente en la tabla de destino deben tener el mismo formato.  
  
Cada línea contiene el nombre de una columna en la tabla de destino y su formato de fecha y hora.  
  
Ejemplo:  
  
`LastReceiptDate=ymd`  
  
`ModifiedDate=dym`  
  
**-d** *staging_database_name*  
Nombre de la base de datos que contendrá la tabla de ensayo. El valor predeterminado es la base de datos especificada con la opción-T, que es la base de datos de la tabla de destino. Para obtener más información sobre cómo usar una base de datos de almacenamiento provisional, vea [crear la base de datos de ensayo](staging-database.md).  
  
**-M** *load_mode_option*  
Especifica si se van a anexar, Upsert o volver a cargar los datos. El modo predeterminado es anexar.  
  
append  
El cargador inserta filas al final de las filas existentes en la tabla de destino.  
  
fastappend  
El cargador inserta filas directamente, sin usar una tabla temporal, al final de las filas existentes en la tabla de destino. fastappend requiere la opción de transacciones múltiples (-m). No se puede especificar una base de datos de ensayo cuando se usa fastappend. No hay reversión con fastappend, lo que significa que la recuperación de una carga errónea o anulada debe controlarse mediante su propio proceso de carga.  
  
Upsert **-K**  *merge_column* [,... *n* ]  
El cargador utiliza la instrucción SQL Server Merge para actualizar las filas existentes e insertar nuevas filas.  
  
La opción-K especifica las columnas en las que se basará la combinación. Estas columnas forman una clave de combinación, que debe representar una fila única. Si la clave de combinación existe en la tabla de destino, se actualiza la fila. Si la clave de fusión mediante combinación no existe en la tabla de destino, se anexará la fila.  
  
En el caso de las tablas distribuidas por hash, la clave de fusión mediante combinación debe ser o incluir la columna de distribución.  
  
En el caso de las tablas replicadas, la clave de combinación es la combinación de una o varias columnas. Estas columnas se especifican según las necesidades de la aplicación.  
  
Varias columnas deben estar separadas por comas sin espacios o separarse por comas con espacios y encerrados entre comillas simples.  
  
Si dos filas de la tabla de origen tienen valores de clave de combinación coincidentes, sus respectivas filas deben ser idénticas.  
  
volver a cargar  
El cargador trunca la tabla de destino antes de insertar los datos de origen.  
  
**-b** *BatchSize*  
Solo se recomienda para su uso por Soporte técnico de Microsoft, *BatchSize* es el tamaño de lote SQL Server para la copia masiva que DMS realiza en SQL Server instancias en los nodos de proceso.  Cuando se especifica *BatchSize* , PDW de SQL Server invalidará el tamaño de carga del lote que se calcula dinámicamente para cada carga.  
  
A partir de SQL Server PDW 2012, el nodo de control calcula dinámicamente un tamaño de lote para cada carga de forma predeterminada. Este cálculo automático se basa en varios parámetros, como el tamaño de la memoria, el tipo de tabla de destino, el esquema de tabla de destino, el tipo de carga, el tamaño de archivo y la clase de recurso del usuario.  
  
Por ejemplo, si el modo de carga es FASTAPPEND y la tabla tiene un índice de almacén de columnas agrupado, PDW de SQL Server intentará usar de forma predeterminada un tamaño de lote de 1.048.576 para que filas se cierre y se cargue directamente en el almacén de columnas sin pasar por el almacén Delta. Si la memoria no permite el tamaño de lote de 1.048.576, dwloader elegirá un BatchSize más pequeño.  
  
Si el tipo de carga es FASTAPPEND, *BatchSize* se aplica a la carga de datos en la tabla; de lo contrario, *BatchSize* se aplica a la carga de datos en la tabla de ensayo.  
  
<reject_options>  
Especifica las opciones para determinar el número de errores de carga que permitirá el cargador. Si los errores de carga superan el umbral, el cargador se detendrá y no confirmará ninguna fila.  
  
**-RT** { **Value** | Percentage}  
Especifica si el*reject_value* de la opción **-RV** *reject_value* es un número literal de filas (valor) o una tasa de error (porcentaje). El valor predeterminado es Value.  
  
La opción de porcentaje es un cálculo en tiempo real que se produce a intervalos según la opción-RS.  
  
Por ejemplo, si el cargador intenta cargar 100 filas y 25 producen un error y 75 se realiza correctamente, la tasa de error es del 25%.  
  
**-rv** *reject_value*  
Especifica el número o porcentaje de rechazos de filas que se van a permitir antes de detener la carga. La opción **-RT** determina si *reject_value* hace referencia al número de filas o al porcentaje de filas.  
  
El *reject_value* predeterminado es 0.  
  
Cuando se usa con el valor-RT, el cargador detiene la carga cuando el recuento de filas rechazados supera reject_value.  
  
Cuando se usa con el porcentaje de-RT, el cargador calcula el porcentaje a intervalos (opción-RS). Por lo tanto, el porcentaje de filas con errores puede superar *reject_value*.  
  
**-rs** *reject_sample_size*  
Se utiliza con la `-rt percentage` opción para especificar las comprobaciones de porcentaje incremental. Por ejemplo, si reject_sample_size es 1000, el cargador calculará el porcentaje de filas con errores después de intentar cargar 1000 filas. Vuelve a calcular el porcentaje de filas con errores después de intentar cargar cada 1000 filas adicionales.  
  
**-c**  
Quita los caracteres de espacio en blanco situados a la izquierda y a la derecha de los campos Char, nchar, VARCHAR y nvarchar. Convierte cada campo que solo contiene caracteres de espacio en blanco en la cadena vacía.  
  
Ejemplo:  
  
' ' se trunca en ' '  
  
' ABC ' se trunca a ' ABC '  
  
Cuando se usa-c con-E, la operación-E se produce primero. Los campos que contienen solo caracteres de espacio en blanco se convierten en una cadena vacía y no en NULL.  
  
**-E**  
Convertir cadenas vacías en NULL. El valor predeterminado es no realizar estas conversiones.  
  
**-m**  
Usar el modo de transacción múltiple para la segunda fase de carga; al cargar datos de la tabla de ensayo en una tabla distribuida.  
  
Con **-m**, PDW de SQL Server realiza y confirma cargas en paralelo. Esto funciona mucho más rápido que el modo de carga predeterminado, pero no es seguro para las transacciones.  
  
Sin **-m**, PDW de SQL Server realiza y confirma cargas en serie entre las distribuciones dentro de cada nodo de proceso y simultáneamente a través de los nodos de proceso. Este método es más lento que el modo de transacciones múltiples, pero es seguro para las transacciones.  
  
**-m** es opcional para *Append*, *Reload*y *Upsert*.  
  
**-m** es necesario para fastappend.  
  
**-m** no se puede usar con tablas replicadas.  
  
**-m** solo se aplica a la segunda fase de carga. No se aplica a la primera fase de carga; cargar datos en la tabla de ensayo.  
  
No hay ninguna reversión con el modo de transacciones múltiples, lo que significa que la recuperación de una carga errónea o anulada debe controlarse mediante su propio proceso de carga.  
  
Se recomienda usar **-m** solo al cargar en una tabla vacía, de modo que se pueda recuperar sin pérdida de datos. Para recuperarse de un error de carga: Quite la tabla de destino, resuelva el problema de carga, vuelva a crear la tabla de destino y vuelva a ejecutar la carga.  
  
**-N**  
Compruebe que el dispositivo de destino tiene un certificado de PDW de SQL Server válido de una entidad de confianza. Úsela para asegurarse de que un atacante no esté secuestrando los datos y se envíen a una ubicación no autorizada. El certificado ya debe estar instalado en el dispositivo. La única manera admitida de instalar el certificado es que el administrador del dispositivo lo instale mediante la herramienta Configuration Manager. Pregunte al administrador del dispositivo si no está seguro de si el dispositivo tiene instalado un certificado de confianza.  
  
**-se**  
Omitir la carga de archivos vacíos. Esto también omite la descompresión de archivos gzip vacíos.

**-l**  
Disponible con la actualización CU 7.4, especifica la longitud máxima de fila (en bytes) que se puede cargar. Los valores válidos son enteros entre 32768 y 33554432. Use solo cuando sea necesario para cargar grandes filas (más de 32 KB), ya que esto asignará más memoria en el cliente y en el servidor.
  
## <a name="return-code-values"></a>Valores de código de retorno  
0 (correcto) u otro valor entero (error)  
  
En una ventana de comandos o un archivo por lotes, use `errorlevel` para mostrar el código de retorno. Por ejemplo:  
  
```  
dwloader  
echo ReturnCode=%errorlevel%  
if not %errorlevel%==0 echo Fail  
if %errorlevel%==0 echo Success  
```  
  
Al usar PowerShell, use `$LastExitCode` .  
  
## <a name="permissions"></a>Permisos  
Requiere permiso LOAD y permisos aplicables (INSERT, UPDATE y DELETE) en la tabla de destino. Requiere el permiso CREATE (para crear una tabla temporal) en la base de datos de ensayo. Si no se utiliza una base de datos de ensayo, se requiere el permiso CREATE en la base de datos de destino. 

<!-- MISSING LINK
For more information, see [Grant permissions to load data](grant-permissions-to-load-data.md).  
-->
  
## <a name="general-remarks"></a>Notas generales  
Para obtener información sobre las conversiones de tipos de datos al cargar con dwloader, vea [reglas de conversión de tipos de datos para dwloader](dwloader-data-type-conversion-rules.md).  
  
Si un parámetro incluye uno o varios espacios, inclúyalo entre comillas dobles.  
  
Debe ejecutar el cargador desde su ubicación de instalación. El ejecutable dwloader se instala previamente con el dispositivo y se encuentra en el directorio C:\Archivos de Programa\microsoft SQL Server Data Warehouse\DWLoader  
  
Puede invalidar un parámetro especificado en el archivo de parámetros (opción-f) si lo especifica como un parámetro de línea de comandos.  
  
Puede ejecutar varias instancias del cargador simultáneamente. El número máximo de instancias del cargador se configura previamente y no se puede cambiar. 

<!-- MISSING LINK
For the maximum number of loads per appliance, see [Minimum and Maximum Values](minimum-maximum-values.md)  
-->
  
Los datos cargados pueden requerir más o menos espacio en el dispositivo que en la ubicación de origen. Puede realizar importaciones de prueba con subconjuntos de datos para calcular el consumo del disco.  
  
Aunque **dwloader** es un proceso de transacción y se revierte correctamente en caso de error, no se puede revertir una vez que la carga masiva se ha completado correctamente. Para cancelar un proceso de **dwloader** activo, escriba Ctrl + C.  
  
## <a name="limitations-and-restrictions"></a>Limitaciones y restricciones  
El tamaño total de todas las cargas que se producen simultáneamente debe ser menor que LOG_SIZE para la base de datos y se recomienda que el tamaño total de todas las cargas simultáneas sea inferior al 50% del LOG_SIZE. Para lograr este límite de tamaño, puede dividir las cargas grandes en varios lotes. Para obtener más información sobre LOG_SIZE, consulte [Create Database](../t-sql/statements/create-database-transact-sql.md?view=aps-pdw-2016) .  
  
Al cargar varios archivos con un comando LOAD, todas las filas rechazadas se escriben en el mismo archivo de rechazo. El archivo de rechazo no muestra el archivo de entrada que contiene cada fila rechazada.  
  
La cadena vacía no se debe usar como delimitador. Cuando se usa una cadena vacía como delimitador de filas, se producirá un error en la carga. Cuando se usa como delimitador de columna, la carga omite el delimitador y continúa usando el valor predeterminado "|" como delimitador de columna. Cuando se usa como delimitador de cadena, la cadena vacía se omite y se aplica el comportamiento predeterminado.  
  
## <a name="locking-behavior"></a>Comportamiento del bloqueo  
el comportamiento de bloqueo de **dwloader** varía en función del *load_mode_option*.  
  
-   **Append** -Append es la opción recomendada y la más común. Append carga los datos en una tabla de ensayo. El bloqueo se describe en detalle a continuación.  
  
-   **Fast Append** -Fast: anexar se carga directamente en la tabla final tomando un bloqueo de tabla ExclusiveUpdate y es el único modo que no utiliza una tabla de ensayo.  
  
-   **recarga** : recarga carga los datos en una tabla de ensayo y requiere un bloqueo exclusivo en la tabla de ensayo y en la tabla final. No se recomienda volver a cargar para las operaciones simultáneas.  
  
-   **Upsert** -Upsert carga los datos en una tabla de ensayo y, a continuación, realiza una operación de combinación de la tabla de ensayo a la tabla final. Upsert no requiere bloqueos exclusivos en la tabla final. El rendimiento puede variar al usar Upsert. Pruebe el comportamiento en su entorno.  
  
### <a name="locking-behavior"></a>Comportamiento del bloqueo  
**Bloqueo del modo Append**  
  
Append se puede ejecutar en modo multitransaccional (mediante el argumento-m), pero no es seguro para las transacciones. Por lo tanto, Append debe usarse como una operación transaccional (sin usar el argumento-m). Desafortunadamente, durante la operación de inserción y selección final, el modo transaccional es actualmente seis veces más lento que el modo de varias transacciones.  
  
El modo Append carga los datos en dos fases. La fase uno carga los datos del archivo de origen en una tabla de ensayo simultáneamente (se puede producir una fragmentación). La fase dos carga los datos de la tabla de ensayo en la tabla final. En la segunda fase se realiza una **inserción en... Seleccione WITH (TABLOCK)** Operation. En la tabla siguiente se muestra el comportamiento de bloqueo de la tabla final y el comportamiento de registro al usar el modo Append:  
  
|Tipo de tabla|Transacciones múltiples<br />Modo (-m)|La tabla está vacía|Compatibilidad con simultaneidad|Registro|  
|--------------|-----------------------------------|------------------|-------------------------|-----------|  
|Montón|Sí|Sí|Sí|mínimo|  
|Montón|Sí|No|Sí|mínimo|  
|Montón|No|Sí|No|mínimo|  
|Montón|No|No|No|mínimo|  
|Cl|Sí|Sí|No|mínimo|  
|Cl|Sí|No|Sí|Completo|  
|Cl|No|Sí|No|mínimo|  
|Cl|No|No|Sí|Completo|  
  
En la tabla anterior se muestra **dwloader** mediante la carga del modo Append en un montón o en una tabla de índice clúster (CI), con o sin la marca multitransaccional y la carga en una tabla vacía o en una tabla no vacía. El comportamiento de bloqueo y registro de cada combinación de carga se muestra en la tabla. Por ejemplo, la fase de carga (2ª) con el modo Append en un índice agrupado sin el modo de varias transacciones y en una tabla vacía hará que PDW cree un bloqueo exclusivo en la tabla y el registro sea mínimo. Esto significa que un cliente no podrá cargar (2ª) fase y consulta simultáneamente en una tabla vacía. Sin embargo, al cargar con la misma configuración en una tabla que no está vacía, PDW no emitirá un bloqueo exclusivo en la tabla y es posible la simultaneidad. Desafortunadamente, se produce el registro completo, lo que ralentiza el proceso.  
  
## <a name="examples"></a>Ejemplos  
  
### <a name="a-simple-dwloader-example"></a>A. Ejemplo de dwloader simple  
En el ejemplo siguiente se muestra la iniciación del **cargador** solo con las opciones requeridas seleccionadas. Otras opciones se toman del archivo de configuración global, *loadparamfile.txt*.  
  
Ejemplo de uso de la autenticación de SQL Server.  
  
```  
--Load over Ethernet  
dwloader.exe -S 10.192.63.148 -U mylogin -P 123jkl -f /configfiles/loadparamfile.txt  
  
--Load over InfiniBand to appliance named MyPDW  
dwloader.exe -S MyPDW-SQLCTL01 -U mylogin -P 123jkl -f /configfiles/loadparamfile.txt  
```  
  
En el mismo ejemplo se usa la autenticación de Windows.  
  
```  
--Load over Ethernet  
dwloader.exe -S 10.192.63.148 -W -f /configfiles/loadparamfile.txt  
  
--Load over InfiniBand to appliance named MyPDW  
dwloader.exe -S MyPDW-SQLCTL01 -W -f /configfiles/loadparamfile.txt  
```  
  
Ejemplo de uso de argumentos para un archivo de código fuente y un archivo de error.  
  
```  
--Load over Ethernet  
dwloader.exe -U mylogin -P 123jkl -S 10.192.63.148  -i C:\SQLData\AWDimEmployees.csv -T AdventureWorksPDW2012.dbo.DimEmployees -R C:\SQLData\LoadErrors  
```  
  
### <a name="b-load-data-into-an-adventureworks-table"></a>B. Cargar datos en una tabla de AdventureWorks  
El ejemplo siguiente forma parte de un script de Batch que carga datos en **AdventureWorksPDW2012**.  Para ver el script completo, abra el archivo aw_create.bat que se incluye con el paquete de instalación de **AdventureWorksPDW2012** . 

<!-- Missing link
For more information, see [Install AdventureWorksPDW2012](install-adventureworkspdw2012.md).  
-->

El siguiente fragmento de script usa dwloader para cargar datos en las tablas DimAccount y DimCurrency. Este script usa una dirección Ethernet. Si estaba usando InfiniBand, el servidor se *<appliance_name>* `-SQLCTL01` .  
  
```  
set server=10.193.63.134  
set user=<MyUser>  
set password=<MyPassword>  
  
set schema=AdventureWorksPDW2012.dbo  
set load="C:\Program Files\Microsoft SQL Server Parallel Data Warehouse\100\dwloader.exe"  
set mode=reload  
  
--Loads data into the AdventureWorksPDW2012.dbo.DimAccount table  
--Source data is stored in the file DimAccount.txt,   
--which is in the current directory.  
  
set t1=DimAccount  
%load% -S %server% -E -M %mode% -e Utf16 -i .\%t1%.txt -T %schema%.%t1% -R %t1%.bad -t "|" -r \r\n -U %user% -P %password%   
  
--Loads data from the DimCurrency.txt file into  
--AdventureWorksPDW2012.dbo.DimCurrency  
set t1=DimCurrency  
%load% -S %server% -E -M %mode% -e Utf16 -i .\%t1%.txt -T %schema%.%t1% -R %t1%.bad -t "|" -r \r\n -U %user% -P %password%  
```  
  
El siguiente es el DDL de la tabla DimAccount.  
  
```  
CREATE TABLE DimAccount(  
AccountKey int NOT NULL,  
ParentAccountKey int,  
AccountCodeAlternateKey int,  
ParentAccountCodeAlternateKey int,  
AccountDescription nvarchar(50),  
AccountType nvarchar(50),  
Operator nvarchar(50),  
CustomMembers nvarchar(300),  
ValueType nvarchar(50),  
CustomMemberOptions nvarchar(200))  
with (CLUSTERED INDEX(AccountKey),  
DISTRIBUTION = REPLICATE);  
```  
  
A continuación se muestra un ejemplo del archivo de datos, DimAccount.txt, que contiene los datos que se van a cargar en la tabla DimAccount.  
  
```  
--Sample of data in the DimAccount.txt load file.  
  
1||1||Balance Sheet||~||Currency|  
2|1|10|1|Assets|Assets|+||Currency|  
3|2|110|10|Current Assets|Assets|+||Currency|  
4|3|1110|110|Cash|Assets|+||Currency|  
5|3|1120|110|Receivables|Assets|+||Currency|  
6|5|1130|1120|Trade Receivables|Assets|+||Currency|  
7|5|1140|1120|Other Receivables|Assets|+||Currency|  
8|3|1150|110|Allowance for Bad Debt|Assets|+||Currency|  
9|3|1160|110|Inventory|Assets|+||Currency|  
10|9|1162|1160|Raw Materials|Assets|+||Currency|  
11|9|1164|1160|Work in Process|Assets|+||Currency|  
12|9|1166|1160|Finished Goods|Assets|+||Currency|  
13|3|1170|110|Deferred Taxes|Assets|+||Currency|  
```  
  
### <a name="c-load-data-from-the-command-line"></a>C. Cargar datos desde la línea de comandos  
El script del ejemplo B se puede reemplazar escribiendo todos los parámetros en la línea de comandos, tal y como se muestra en el ejemplo siguiente.  
  
```  
C:\Program Files\Microsoft SQL Server Parallel Data Warehouse\100\dwloader.exe -S <Control node IP> -E -M reload -e UTF16 -i .\DimAccount.txt -T AdventureWorksPDW2012.dbo.DimAccount -R DimAccount.bad -t "|" -r \r\n -U <login> -P <password>  
```  
  
Descripción de los parámetros de la línea de comandos:  
  
-   *C:\Archivos de programa\microsoft SQL Server Warehouse\100\dwloader.exede datos paralelos * es la ubicación instalada de dwloader.exe.  
  
-   *-S* va seguido de la dirección IP del nodo de control.  
  
-   *-E* especifica que se carguen cadenas vacías como null.  
  
-   *-M recargar* especifica que se trunque la tabla de destino antes de insertar los datos de origen.  
  
-   *-e UTF16* indica que el archivo de origen usa el tipo de codificación de caracteres Little Endian.  
  
-   *-i .\DimAccount.txt* especifica que los datos están en un archivo denominado DimAccount.txt que existe en el directorio actual.  
  
-   *-T AdventureWorksPDW2012. DBO. DimAccount* especifica el nombre de tres partes de la tabla que va a recibir los datos.  
  
-   *-R DimAccount. Bad* especifica que las filas que no se cargan se escribirán en un archivo denominado DimAccount. Bad.  
  
-   *-t "|"* indica que los campos del archivo de entrada, DimAccount.txt, se separan con el carácter de barra vertical.  
  
-   *-r \r\n* especifica que cada fila de DimAccount.txt finaliza con un retorno de carro y un carácter de avance de línea.  
  
-   *-U <login_name>-P <password> * especifica el inicio de sesión y la contraseña para el inicio de sesión que tiene permisos para realizar la carga.  
  

<!-- MISSING LINK

## See Also  
[Common Metadata Query Examples](metadata-query-examples.md)  

-->
