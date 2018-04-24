---
title: dwloader cargador de línea de comandos - almacenamiento de datos paralelos | Documentos de Microsoft
description: dwloader es una herramienta de línea de comandos de almacenamiento de datos paralelo (PDW) que carga filas de la tabla de forma masiva en una tabla existente.
author: mzaman1
manager: craigg
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.openlocfilehash: d5d8ead82525266148729f9773e47b933def349e
ms.sourcegitcommit: 056ce753c2d6b85cd78be4fc6a29c2b4daaaf26c
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/19/2018
---
# <a name="dwloader-command-line-loader-for-parallel-data-warehouse"></a>Cargador de la línea de comandos para el almacenamiento de datos paralelo de dwloader
**dwloader** es una herramienta de línea de comandos de almacenamiento de datos paralelo (PDW) que carga filas de la tabla de forma masiva en una tabla existente. Cuando se cargan filas, puede agregar todas las filas al final de la tabla (*modo append* o *fastappend modo*), anexar filas nuevas y actualizar filas existentes (*upsert modo*), o todos los elimine existente filas antes de la carga y, a continuación, insertar todas las filas en una tabla vacía (*recargar modo*).  
  
**Proceso para cargar datos**  
  
1.  Preparar los datos de origen.  
  
    Utilice su propio proceso ETL para crear el origen de datos que se va a cargar. Los datos de origen deben estar formateados para que coincida con el esquema de la tabla de destino. Almacenar los datos de origen en uno o varios archivos de texto y copie los archivos de texto en el mismo directorio en el servidor de carga. Para obtener información sobre el servidor de carga, consulte [adquirir y configurar un servidor de carga](acquire-and-configure-loading-server.md)  
  
2.  Preparar las opciones de carga.  
  
    Decidir qué opciones de carga que se va a usar. Almacenar las opciones de carga en un archivo de configuración. Copie el archivo de configuración en una ubicación local en el servidor de carga. El **dwloader** opciones de configuración se describen en este tema.  
  
3.  Preparar la carga de las opciones de error.  
  
    Decida cómo desea **dwloader** controle las filas que no se pudo cargar. Para realizar la carga, **dwloader** carga por primera vez los datos en una tabla de ensayo y, a continuación, transfiere los datos a la tabla de destino. Como el cargador carga datos en la tabla de ensayo, realiza un seguimiento del número de filas que no se pudo cargar. Por ejemplo, se producirá un error de filas que no tengan el formato correcto cargar. Filas con errores se copian en un archivo de rechazo. De forma predeterminada, la carga se anula después del primer rechazo a menos que especifique un umbral de rechazo diferentes.  
  
4.  Instalar **dwloader**.  
  
    Instale dwloader en el servidor de carga si no está ya instalado. 

<!-- MISSING LINK
    See [Install dwloader Command-Line Loader &#40;SQL Server PDW&#41;](install-dwloader-command-line-loader-sql-server-pdw.md). 
--> 
  
5.  Ejecutar **dwloader**.  
  
    Inicie sesión en el servidor de carga y ejecuta el archivo ejecutable **dwloader.exe** con las opciones de línea de comandos adecuadas.  
  
6.  Comprobar los resultados.  
  
    Puede comprobar el error filas archivo (especificado con -R) para ver si todas las filas no se pudieron cargar. Si este archivo está vacío, todas las filas se cargan correctamente. **dwloader** es transaccional, por lo que si cualquier paso produce un error (que no sea rechazadas filas), todos los pasos se revertirá a su estado inicial.  
  
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
}  
```  
  
## <a name="arguments"></a>Argumentos  
**-h**  
Muestra información de ayuda simple acerca de cómo utilizar el cargador. Ayuda muestra solo si no se especifica ningún otro parámetro de línea de comandos.  
  
**-U** *login_name*  
Inicio de sesión autenticación de SQL Server válido con los permisos adecuados para realizar la carga.  
  
**-P** *password*  
La contraseña de autenticación de SQL Server *login_name*.  
  
**-W**  
Usa la autenticación de Windows. (No *login_name* o *contraseña* necesaria.) 

<!-- MISSING LINK
For information about configuring Windows Authentication, see [Security - Configure Domain Trusts](security-configure-domain-trusts.md).  
-->
  
**-f** *parameter_file_name*  
Usar un archivo de parámetros, *parameter_file_name*, en lugar de parámetros de línea de comandos. *parameter_file_name* puede contener cualquier parámetro de línea de comandos excepto *nombre_usuario* y *contraseña*. Si se especifica un parámetro en la línea de comandos y en el archivo de parámetros, la línea de comandos reemplaza el parámetro del archivo.  
  
El archivo de parámetros contiene un parámetro, sin la **-** prefijo por línea.  
  
Ejemplos:  
  
`rt=percentage`  
  
`rv=25`  
  
**-S***target_appliance*  
Especifica el dispositivo PDW de SQL Server que recibirá los datos cargados.  
  
*Para las conexiones Infiniband*, *target_appliance* se especifica como < nombre del dispositivo >-SQLCTL01. Para configurar esto con el nombre de conexión, consulte [configurar adaptadores de red InfiniBand](configure-infiniband-network-adapters.md).  
  
Para las conexiones Ethernet, *target_appliance* es la dirección IP para el clúster de nodo de Control.  
  
Si se omite, el valor predeterminado de dwloader es el valor que se especificó cuando se instaló dwloader. 

<!-- MISSING LINK
For more information about this install option, see [Install dwloader Command-Line Loader](install-dwloader.md).  
-->
  
**-T** *target_database_name.*[*schema*].*table_name*  
El nombre de tres partes de la tabla de destino.  
  
**-I***source_data_location*  
La ubicación de uno o varios archivos de origen para cargar. Cada archivo de origen debe ser un archivo de texto o un archivo de texto que se ha comprimido con gzip. Solo un archivo de origen se puede comprimir en cada archivo gzip.  
  
Para dar formato a un archivo de origen:  
  
-   El archivo de origen debe estar formateado con arreglo a las opciones de carga.  
  
-   Cada línea en un archivo de origen contiene los datos de una fila de tabla. Los datos de origen deben coincidir con el esquema de la tabla de destino. También deben coincidir con los tipos de datos y orden de columna. Cada campo de la fila representa una columna en la tabla de destino.  
  
-   De forma predeterminada, los campos son de longitud variable y separan por un delimitador. Para especificar el tipo de delimitador, utilice las opciones de línea de comandos de < variable_length_column_options >. Para especificar los campos de longitud fija, utilice las opciones de línea de comandos de < fixed_width_column_options >.  
  
Para especificar la ubicación de origen de datos:  
  
-   La ubicación de datos de origen puede ser una ruta de acceso de red o una ruta de acceso local a un directorio en el servidor de carga.  
  
-   Para especificar todos los archivos en un directorio, escriba la ruta de acceso de directorio seguido por el * carácter comodín.  El cargador no carga los archivos de los subdirectorios que se encuentran en la ubicación de origen de datos... Los errores de cargador cuando existe un directorio en un archivo gzip.  
  
-   Para especificar algunos de los archivos en un directorio, use una combinación de caracteres y el * comodín.  
  
Para cargar varios archivos con un solo comando:  
  
-   Todos los archivos deben encontrarse en el mismo directorio.  
  
-   Los archivos deben ser todos los archivos de texto, todos los archivos gzip o una combinación de archivos de texto e gzip.  
  
-   Ninguno de los archivos pueden contener información de encabezado.  
  
-   Todos los archivos deben usar el mismo tipo de codificación de caracteres. Vea la opción-e.  
  
-   Todos los archivos deben cargarse en la misma tabla.  
  
-   Todos los archivos se concatenarán y se cargan como si son un archivo y las filas rechazadas irá a un archivo único de rechazo.  
  
Ejemplos:  
  
-   -i \\\loadserver\loads\daily\\*.gz  
  
-   -i \\\loadserver\loads\daily\\*.txt  
  
-   -i \\\loadserver\loads\daily\monday.*  
  
-   -i \\\loadserver\loads\daily\monday.txt  
  
-   -i \\\loadserver\loads\daily\\*  
  
**-R** *load_failure_file_name*  
Si hay errores de carga, **dwloader** almacena la fila que no se pudo cargar y la descripción del error la información del error en un archivo denominado *load_failure_file_name*. Si el archivo ya existe, dwloader sobrescribirá el archivo existente. *load_failure_file_name* se crea cuando se produce el primer error. Si todas las filas se cargan correctamente, *load_failure_file_name* no se crea.  
  
**-fh** *number_header_rows*  
El número de líneas (filas) para pasar por alto al principio de *source_data_file_name*. El valor predeterminado es 0.  
  
<variable_length_column_options>  
Las opciones para un *source_data_file_name* que tiene columnas de longitud variable delimitada por un carácter. De forma predeterminada, *source_data_file_name* contiene caracteres ASCII en columnas de longitud variable.  
  
Para los archivos de ASCII, valores NULL se representa mediante la colocación de forma consecutiva delimitadores. Por ejemplo, en un archivo delimitado por barra vertical ("|"), un valor NULL viene indicado por "||". En un archivo delimitado por comas, un valor NULL viene indicado por ",,". Además, el **-E** (--emptyStringAsNull) debe especificar la opción. Para obtener más información sobre -E, consulte a continuación.  
  
**-e** *character_encoding*  
Especifica un tipo de codificación de caracteres para los datos que va a cargarse desde el archivo de datos. Opciones son ASCII (valor predeterminado), UTF8, UTF16 o UTF16BE, donde UTF16 es poco endian y UTF16BE es big endian. Estas opciones distinguen mayúsculas de minúsculas.  
  
**-t** *delimitadordecampo*  
El delimitador para cada campo (columna) en la fila. El delimitador de campo es uno o varios de estos caracteres de escape de ASCII o valores hexadecimales de ASCII...  
  
|Nombre|Carácter de escape|Carácter hexadecimal|  
|--------|--------------------|-----------------|  
|Pestaña|\t|0 x 09|  
|Retorno de carro (CR)|\r|0x0D|  
|Salto de línea (LF)|\n|0x0A|  
|CRLF|\r\n|0x0d0x0a|  
|Coma|','|0x2c|  
|Comilla doble|\\"|0x22|  
|Comilla simple|\\'|0x27|  
  
Para especificar el carácter de barra vertical en la línea de comandos, escríbalo entre comillas dobles, "|". Esto evitará una interpretación incorrecta por el analizador de línea de comandos. Otros caracteres se incluyen entre comillas sencillas.  
  
Ejemplos:  
  
-t "|"  
  
-t ' '  
  
-t 0x0a  
  
\t -t  
  
-t ' ~ | ~'  
  
**-r** *delimitadordefilas*  
El delimitador para cada fila del archivo de datos de origen. El delimitador de fila es uno o más valores ASCII.  
  
Para especificar un retorno de carro (CR), avance de línea (LF) o carácter de tabulación como delimitador, puede usar los caracteres de escape (\r, \n, \t) ni sus valores hexadecimales (0 x, 0D, 09). Para especificar caracteres especiales como delimitadores, utilice su valor hexadecimal.  
  
Ejemplos de CR + LF:  
  
-r \r\n  
  
-r 0x0d0x0a  
  
Ejemplos de CR:  
  
-r \r  
  
-r 0x0d  
  
Ejemplos de LF:  
  
-r \n  
  
-r 0x0a  
  
Un LF es necesaria para Unix. Un CR es necesario para Windows.  
  
**-s** *string_delimiter*  
El delimitador para datos de cadena tipo de campo de un archivo de entrada de texto delimitado. El delimitador de cadenas es uno o más valores ASCII.  Se puede especificar como un carácter (p. ej., -s *) o como un valor hexadecimal (p. ej., -s 0 x 22 para una comilla doble).  
  
Ejemplos:  
  
-s *  
  
-s 0 x 22  
  
< fixed_width_column_options>  
Las opciones para un archivo de datos de origen que tiene columnas de longitud fija. De forma predeterminada, *source_data_file_name* contiene caracteres ASCII en columnas de longitud variable.  
  
No se admiten columnas de ancho fijo cuando – e es UTF8.  
  
**-w** *fixed_width_config_file*  
Ruta de acceso y nombre del archivo de configuración que especifica el número de caracteres en cada columna. Se deben especificar todos los campos.  
  
Este archivo debe residir en el servidor de carga. La ruta de acceso puede ser una ruta de acceso UNC absoluta o relativa. Cada línea en *fixed_width_config_file* contiene el nombre de una columna y el número de caracteres para esa columna. Hay una línea por cada columna, como se indica a continuación y el orden en el archivo debe coincidir con el orden en la tabla de destino:  
  
*column_name*=*num_chars*  
  
*column_name*=*num_chars*  
  
En el ejemplo se ha corregido el archivo de configuración de ancho:  
  
SalesCode = 3  
  
SalesID = 10  
  
Ejemplo líneas *source_data_file_name*:  
  
230Shirts0056  
  
320Towels1356  
  
En el ejemplo anterior, la primera fila cargada tendrá SalesCode = '230' y SalesID = 'Shirts0056'. La fila cargada en segundo lugar tendrá SalesCode = '320' y SaleID = 'Towels1356'.  
  
Para obtener información sobre cómo administrar iniciales y finales de conversión de tipos de datos o espacios en el modo de ancho fijo, vea [de dwloader las reglas de conversión de tipo de datos](dwloader-data-type-conversion-rules.md).  
  
**-e** *character_encoding*  
Especifica un tipo de codificación de caracteres para los datos que va a cargarse desde el archivo de datos. Opciones son ASCII (valor predeterminado), UTF8, UTF16 o UTF16BE, donde UTF16 es poco endian y UTF16BE es big endian. Estas opciones distinguen mayúsculas de minúsculas.  
  
No se admiten columnas de ancho fijo cuando – e es UTF8.  
  
**-r** *delimitadordefilas*  
El delimitador para cada fila del archivo de datos de origen. El delimitador de fila es uno o más valores ASCII.  
  
Para especificar un retorno de carro (CR), avance de línea (LF) o carácter de tabulación como delimitador, puede usar los caracteres de escape (\r, \n, \t) ni sus valores hexadecimales (0 x, 0D, 09). Para especificar caracteres especiales como delimitadores, utilice su valor hexadecimal.  
  
Ejemplos de CR + LF:  
  
-r \r\n  
  
-r 0x0d0x0a  
  
Ejemplos de CR:  
  
-r \r  
  
-r 0x0d  
  
Ejemplos de LF:  
  
-r \n  
  
-r 0x0a  
  
Un LF es necesaria para Unix. Un CR es necesario para Windows.  
  
**-D** { **AMD** | adm | mdy | MAD |  DMA | DAM | *custom_date_format* }  
Especifica el orden del mes (m), día (d) y año (y) para todos los campos de fecha y hora en el archivo de entrada. El orden predeterminado es AMD. Para especificar varios formatos de orden para el mismo archivo de origen, use la opción – dt.  
  
AMD | DMA  
ADM y DMA permiten a los mismos formatos de entrada. Ambos permiten el año como al principio o al final de la fecha. Por ejemplo, para ambos **adm** y **DMA** formatos, de fecha podría tener 2013-02-03 o 02-03-2013 en el archivo de entrada.  
  
ADM  
Solo puede cargar la entrada con el formato año-día-mes en columnas de tipo de datos datetime y smalldatetime. No se puede cargar adm valores en una columna del datetime2, fecha o tipo de datos datetimeoffset.  
  
mdy  
MDA permite <month> <space> <day> <comma> <year>.  
  
Ejemplos de datos de entrada de MDA para el 1 de enero de 1975:  
  
-   1 de enero de 1975  
  
-   01 de enero de 75  
  
-   Ene/1/75  
  
-   01011975  
  
mad  
Ejemplos de archivos de entrada para marzo 04,2010: 2010-03-04, 3/4/2010  
  
dam  
Ejemplos de archivos de entrada para 04 de marzo de 2010: 2010-04-03, 4/3/2010  
  
*custom_date_format*  
*custom_date_format* es un formato de fecha personalizado (p. ej., MM/dd/aaaa) y se incluye por compatibilidad con versiones anteriores solo. dwloader no no enfoce el formato de fecha personalizado. En su lugar, cuando se especifica un formato de fecha personalizado, **dwloader** convertirá en el valor correspondiente de AMD, ADM, mdy, MAD, DAM o DMA.  
  
Por ejemplo, si se especifica – D MM/dd/aaaa, dwloader espera que todas las fecha de entrada para poder ordenarse con el mes en primer lugar, a continuación, día y año (MDA). No aplica 2 meses de carácter, 2 días de dígitos y 4 años dígitos tal y como especifica el formato de fecha personalizado. Estos son algunos ejemplos de cómo se pueden aplicar formato a fechas en el archivo de entrada cuando el formato de fecha es – D MM/dd/aaaa: 01/02/2013, Jan.02.2013, 1/2/2013  
  
Para obtener información más completa de formato, vea [de dwloader las reglas de conversión de tipo de datos](dwloader-data-type-conversion-rules.md).  
  
**-dt** *datetime_format_file*  
Cada formato de fecha y hora se especifica en un archivo denominado *datetime_format_file*. A diferencia de los parámetros de línea de comandos, parámetros de archivo que contienen espacios no deben incluirse entre comillas dobles. No se puede modificar el formato de fecha y hora como cargar datos. El archivo de datos de origen y su columna correspondiente en la tabla de destino deben tener el mismo formato.  
  
Cada línea contiene el nombre de una columna en la tabla de destino y su formato de fecha y hora.  
  
Ejemplos:  
  
`LastReceiptDate=ymd`  
  
`ModifiedDate=dym`  
  
**-d** *staging_database_name*  
El nombre de base de datos que contendrá la tabla de ensayo. El valor predeterminado es la base de datos especificada con la opción -T, que es la base de datos para la tabla de destino. Para obtener más información sobre el uso de una base de datos de almacenamiento provisional, consulte [crear la base de datos de almacenamiento provisional](staging-database.md).  
  
**-M** *load_mode_option*  
Especifica si se debe anexar upsert, o volver a cargar datos. El modo predeterminado es anexar.  
  
Anexar  
El cargador inserta filas al final de las filas existentes en la tabla de destino.  
  
fastappend  
El cargador inserta filas directamente, sin usar una tabla temporal, al final de las filas existentes en la tabla de destino. fastappend requiere la transacción múltiple (– m) opción. No se puede especificar una base de datos de almacenamiento provisional al usar fastappend. No hay ninguna reversión con fastappend, lo que significa que la recuperación a partir de una carga anulada o con error deberá controlarse mediante su propio proceso de carga.  
  
Upsert **-K***merge_column* [,...*n* ]    
El cargador usa la instrucción Merge de SQL Server para actualizar filas existentes e insertar nuevas filas.  
  
La opción -K especifica la columna o columnas que se basa la combinación. Estas columnas forman una clave de combinación, que debe representar una única fila. Si la clave de combinación existe en la tabla de destino, se actualiza la fila. Si no existe la clave de combinación en la tabla de destino, se anexa la fila.  
  
Para las tablas hash distribuida, la clave de combinación debe ser o incluir la columna de distribución.  
  
Para las tablas replicadas, la clave de combinación es la combinación de una o varias columnas. Estas columnas se especifican según las necesidades de la aplicación.  
  
Varias columnas deben ser separados por comas sin espacios, o separados por comas con los espacios e incluidas entre comillas simples.  
  
Si dos filas en la tabla de origen tienen valores de clave coincidentes de mezcla, sus filas correspondientes deben ser idénticos.  
  
Volver a cargar  
El cargador trunca la tabla de destino antes de insertar los datos de origen.  
  
**-b** *batchsize*  
Se recomienda únicamente para su uso por Microsoft Support, *batchsize* es el tamaño de lote de SQL Server para la copia masiva que DMS realiza en instancias de SQL Server en los nodos de proceso.  Cuando *batchsize* se especifica, SQL Server PDW invalidará el tamaño de carga por lotes que se calcula dinámicamente para cada carga.  
  
A partir de SQL Server 2012 PDW, el nodo de Control calcula dinámicamente un tamaño de lote para cada carga de forma predeterminada. Este cálculo automático se basa en varios parámetros, como el tamaño de la memoria, tipo de tabla de destino, esquema de la tabla de destino, tipo de carga, el tamaño de archivo y clase de recurso del usuario.  
  
Por ejemplo, si el modo de carga es FASTAPPEND y la tabla tiene un índice de almacén de columnas agrupado, SQL Server PDW le intento predeterminada que puedan usar un tamaño de lote de 1.048.576 rowgroups pasará a cerrado y carga directamente en el almacén de columnas sin pasar por el almacén delta. Si la memoria no permite el tamaño del lote de 1.048.576, dwloader elegirá un tamaño más pequeño.  
  
Si el tipo de carga es FASTAPPEND, el *batchsize* se aplica a la carga de datos en la tabla, en caso contrario, *batchsize* se aplica a la carga de datos en la tabla de ensayo.  
  
<reject_options>  
Especifica opciones para determinar el número de errores de carga que permitirá que el cargador. Si los errores de carga superan el umbral, el cargador se detendrá y no se confirmar todas las filas.  
  
**-rt** { **valor** | porcentaje}  
Especifica si la -*reject_value* en el **-rv** *reject_value* opción es un número de filas (valor) literal o una tasa de error (porcentaje). El valor predeterminado es.  
  
La opción de porcentaje es un cálculo en tiempo real que se produce a intervalos de acuerdo con la opción - rs.  
  
Por ejemplo, si se producirá un error en los intentos de cargador para cargar 100 filas y 25 y 75 sea correcta, la tasa de error es 25%.  
  
**-rv** *reject_value*  
Especifica el número o porcentaje de rechazos de fila que se permiten antes de detener la carga. El **-rt** opción determina si *reject_value* hace referencia al número de filas o el porcentaje de filas.  
  
El valor predeterminado *reject_value* es 0.  
  
Cuando se usa con el valor de -rt, el cargador detiene la carga cuando el recuento de filas rechazados supera reject_value.  
  
Cuando se usa con porcentaje -rt, el cargador calcula el porcentaje a intervalos (-opción de rs). Por lo tanto, puede superar el porcentaje de filas con errores *reject_value*.  
  
**rs -** *reject_sample_size*  
Usar con el `-rt percentage` opción para especificar las comprobaciones de porcentaje incremental. Por ejemplo, si reject_sample_size es 1000, el cargador de calcular el porcentaje de filas con errores después de que ha intentado cargar 1000 filas. Vuelve a calcular el porcentaje de filas con errores después de intentar cargar cada 1000 filas adicionales.  
  
**-c**  
Quita los caracteres de espacio en blanco de la izquierda y derecha de char, nchar, varchar y nvarchar campos. Convierte cada campo que contiene solo caracteres de espacio en blanco en la cadena vacía.  
  
Ejemplos:  
  
' ' se trunca a ''.  
  
se trunca 'abc' a 'abc'  
  
Cuando se utiliza – c con -E, la operación – E se produce en primer lugar. Los campos que contienen únicamente caracteres de espacio en blanco se convierten en la cadena vacía y no NULL.  
  
**-E**  
Convertir cadenas vacías en NULL. El valor predeterminado es no realizar estas conversiones.  
  
**-m**  
Utilice el modo de varias transacciones para la segunda fase de carga; al cargar datos de la tabla de ensayo en una tabla distribuida.  
  
Con **– m**, PDW de SQL Server realiza y confirma cargas en paralelo. Esto lleva a cabo mucho más rápido que el modo de carga predeterminado, pero no es seguro para la transacción.  
  
Sin **– m**, PDW de SQL Server realiza y confirma cargas en serie a través de las distribuciones dentro de cada nodo de proceso y de forma simultánea a través de los nodos de proceso. Este método es más lento que el modo de varias transacciones, pero es seguro para la transacción.  
  
**-m** es opcional para *anexar*, *recargar*, y *upsert*.  
  
**-m** es necesario para fastappend.  
  
**-m** no se puede usar con las tablas replicadas.  
  
**-m** solo se aplica a la segunda fase de carga. No se aplica a la primera fase de carga; para cargar datos en la tabla de ensayo.  
  
No hay ninguna reversión con el modo de transacción múltiple, lo que significa que la recuperación a partir de una carga anulada o con error deberá controlarse mediante su propio proceso de carga.  
  
Se recomienda usar **– m** solo cuando se carga en una tabla vacía, por lo que se pueda recuperar sin pérdida de datos. Para recuperarse de un error de carga: elimine la tabla de destino, resuelva el problema de carga, volver a crear la tabla de destino y vuelva a ejecutar la carga.  
  
**-N**  
Compruebe que el dispositivo de destino tiene un certificado válido de SQL Server PDW de una autoridad de confianza. Use esta opción para ayudar a garantizar que los datos no se está secuestradas por un atacante y se envía a una ubicación no autorizada. El certificado ya debe instalarse en el dispositivo. La única manera admitida para instalar el certificado es para que el administrador del equipo instalar mediante la herramienta Administrador de configuración. Pida al administrador de dispositivo si no está seguro de si el dispositivo tiene instalado un certificado de confianza.  
  
**-se**  
Omitir la carga de archivos vacíos. Esto también omite descomprimir archivos gzip vacía.  
  
## <a name="return-code-values"></a>Valores de código de retorno  
0 (correcto) o en otro valor entero (error)  
  
En un archivo de lote o la ventana de comandos, use `errorlevel` para mostrar el código de retorno. Por ejemplo:  
  
```  
dwloader  
echo ReturnCode=%errorlevel%  
if not %errorlevel%==0 echo Fail  
if %errorlevel%==0 echo Success  
```  
  
Cuando se usa PowerShell, use `$LastExitCode`.  
  
## <a name="permissions"></a>Permissions  
Requiere el permiso de carga y permisos aplicables (INSERT, UPDATE, DELETE) en la tabla de destino. Requiere permiso de creación (para crear una tabla temporal) en la base de datos de almacenamiento provisional. Si no se utiliza una base de datos de almacenamiento provisional, se requiere el permiso de crear en la base de datos de destino. 

<!-- MISSING LINK
For more information, see [Grant permissions to load data](grant-permissions-to-load-data.md).  
-->
  
## <a name="general-remarks"></a>Notas generales  
Para obtener información sobre las conversiones de tipo de datos cuando se carga con dwloader, consulte [de dwloader las reglas de conversión de tipo de datos](dwloader-data-type-conversion-rules.md).  
  
Si un parámetro incluye uno o varios espacios, incluya el parámetro entre comillas dobles.  
  
Debe ejecutar el cargador desde su ubicación de instalación. El ejecutable dwloader preinstalado con el dispositivo y se encuentra en el directorio C:\Program Files\Microsoft SQL Server datos Warehouse\DWLoader.  
  
Puede invalidar un parámetro que se especifica en el archivo de parámetros (-f (opción)), especifíquelo como un parámetro de línea de comandos.  
  
Puede ejecutar simultáneamente varias instancias del cargador. El número máximo de instancias de cargador está preconfigurado y no se puede cambiar. 

<!-- MISSING LINK
For the maximum number of loads per appliance, see [Minimum and Maximum Values](minimum-maximum-values.md)  
-->
  
Datos cargados pueden requerir más o menos espacio en el dispositivo que en la ubicación de origen. Puede realizar importaciones de prueba con subconjuntos de datos para calcular el consumo de disco.  
  
Aunque **dwloader** es un proceso de transacción y se revertirá correctamente en caso de error, no se puede revertir una vez se ha completado correctamente la carga masiva. Para cancelar un activo **dwloader** procesar, presione CTRL+C.  
  
## <a name="limitations-and-restrictions"></a>Limitaciones y restricciones  
El tamaño total de todas las cargas que se producen al mismo tiempo debe ser menor que LOG_SIZE para la base de datos, y se recomienda el tamaño total de todas las cargas simultáneas es inferior al 50% de la LOG_SIZE. Para lograr esta limitación de tamaño, puede dividir cargas de gran tamaño en varios lotes. Para obtener más información sobre LOG_SIZE, consulte [crear base de datos](../t-sql/statements/create-database-parallel-data-warehouse.md)  
  
Al cargar varios archivos con la carga de un comando, todas las filas rechazadas se escriben en el mismo archivo de rechazo. El archivo de rechazo no muestra el archivo de entrada que contiene cada fila rechazado.  
  
La cadena vacía no debe usarse como un delimitador. Cuando se utiliza una cadena vacía como un delimitador de filas, se producirá un error en la carga. Cuando se usa como delimitador de columna, la carga se pasa por alto el delimitador y continúa usando el valor predeterminado "|" como el delimitador de columna. Cuando se usa como delimitador de cadenas, la cadena vacía se omite y se aplica el comportamiento predeterminado.  
  
## <a name="locking-behavior"></a>Comportamiento del bloqueo  
**dwloader** varía según el comportamiento del bloqueo del *load_mode_option*.  
  
-   **anexar** : parámetro Append es la opción más común y la recomendada. Anexar carga datos en una tabla de ensayo. El bloqueo se describe en detalle a continuación.  
  
-   **Anexar rápido** : anexar Fast carga directamente en la tabla final que se haga cargo de un bloqueo de tabla ExclusiveUpdate y es el único modo que no se utiliza una tabla de ensayo.  
  
-   **volver a cargar** : volver a cargar carga datos en una tabla de ensayo y requiere un bloqueo exclusivo en la tabla de ensayo y la tabla final. No se recomienda volver a cargar para las operaciones simultáneas.  
  
-   **Upsert** – Upsert carga datos en una tabla de ensayo y, a continuación, realiza una operación de combinación de la tabla de ensayo a la tabla final. Upsert no requiere un bloqueo exclusivo en la tabla final. El rendimiento puede variar cuando se utiliza upsert. Probar el comportamiento en su entorno.  
  
### <a name="locking-behavior"></a>Comportamiento del bloqueo  
**Un bloqueo de modo append**  
  
Anexar se puede ejecutar en modo multi-transaccional (mediante el argumento – m) pero no es seguro para la ejecución de la transacción. Anexar, por tanto, debe usarse como una operación transaccional (sin usar el argumento – m). Desafortunadamente, durante la operación INSERT SELECT final, el modo transaccional es actualmente aproximadamente seis veces más lento que el modo de varias transaccional.  
  
El modo append carga datos en dos fases. La primera fase carga los datos del archivo de origen en una tabla de ensayo simultáneamente (fragmentación puede producir). Segunda fase carga datos de la tabla de ensayo para la tabla final. La segunda fase se realiza un **INSERT INTO... Seleccione WITH (TABLOCK)** operación. En la tabla siguiente se muestra el comportamiento de bloqueo en la tabla final y comportamiento del registro cuando se usa de modo append:  
  
|Tipo de tabla|Varias transacciones<br />Modo (-m)|Tabla está vacía|Simultaneidad compatibles|Registro|  
|--------------|-----------------------------------|------------------|-------------------------|-----------|  
|Montón|Sí|Sí|Sí|mínimo|  
|Montón|Sí|No|Sí|mínimo|  
|Montón|no|Sí|no|mínimo|  
|Montón|no|No|no|mínimo|  
|CL|Sí|Sí|no|mínimo|  
|CL|Sí|No|Sí|Completa|  
|CL|no|Sí|no|mínimo|  
|CL|no|No|Sí|Completa|  
  
Se muestra en la tabla anterior **dwloader** utilizando el modo de anexar cargar en un montón o una tabla de índice agrupado (CI), con o sin la marca múltiples transaccional y cargar en una tabla vacía o una tabla no vacía. Comportamiento de cada combinación de este tipo de carga de registro y el bloqueo se muestra en la tabla. Por ejemplo, cargar fase (2) con el modo append en un índice clúster sin modo multi-transaccional y en vacío tabla tendrá PDW cree un bloqueo exclusivo en la tabla y el registro es mínimo. Esto significa que un cliente no pueda cargar (2) fase y consultas simultáneamente en una tabla vacía. Sin embargo, cuando se carga con la misma configuración en una tabla no está vacía, PDW no emitirá un bloqueo exclusivo en la tabla y la simultaneidad es posible. Por desgracia, se produce un registro completo, ralentizan el proceso.  
  
## <a name="examples"></a>Ejemplos  
  
### <a name="a-simple-dwloader-example"></a>A. Ejemplo simple dwloader  
En el ejemplo siguiente se muestra el inicio de la **cargador** con las opciones necesarias seleccionadas. Otras opciones se realizan desde el archivo de configuración global, *loadparamfile.txt*.  
  
Ejemplo de cómo utilizar la autenticación de SQL Server.  
  
```  
--Load over Ethernet  
dwloader.exe -S 10.192.63.148 -U mylogin -P 123jkl -f /configfiles/loadparamfile.txt  
  
--Load over InfiniBand to appliance named MyPDW  
dwloader.exe -S MyPDW-SQLCTL01 -U mylogin -P 123jkl -f /configfiles/loadparamfile.txt  
```  
  
El mismo ejemplo mediante la autenticación de Windows.  
  
```  
--Load over Ethernet  
dwloader.exe -S 10.192.63.148 -W -f /configfiles/loadparamfile.txt  
  
--Load over InfiniBand to appliance named MyPDW  
dwloader.exe -S MyPDW-SQLCTL01 -W -f /configfiles/loadparamfile.txt  
```  
  
Ejemplo utilizando los argumentos para un archivo de código fuente y el archivo de error.  
  
```  
--Load over Ethernet  
dwloader.exe -U mylogin -P 123jkl -S 10.192.63.148  -i C:\SQLData\AWDimEmployees.csv -T AdventureWorksPDW2012.dbo.DimEmployees -R C:\SQLData\LoadErrors  
```  
  
### <a name="b-load-data-into-an-adventureworks-table"></a>B. Cargar datos en una tabla de AdventureWorks  
El siguiente ejemplo es parte de un script por lotes que carga datos en **AdventureWorksPDW2012**.  Para ver el script completo, abra el archivo aw_create.bat que se suministra con la **AdventureWorksPDW2012** paquete de instalación. 

<!-- Missing link
For more information, see [Install AdventureWorksPDW2012](install-adventureworkspdw2012.md).  
-->

El siguiente fragmento de script utiliza dwloader para cargar datos en las tablas DimAccount y DimCurrency. Este script está usando una dirección Ethernet. Si se estaba usando InfiniBand, servidor sería *< nombre_dispositivo >*`-SQLCTL01`.  
  
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
  
A continuación se muestra el archivo DDL para la tabla DimAccount.  
  
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
  
El siguiente es un ejemplo del archivo de datos, DimAccount.txt, que contiene datos que se va a cargar en la tabla DimAccount.  
  
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
La secuencia de comandos del ejemplo B puede reemplazarse especificando todos los parámetros en la línea de comandos, tal como se muestra en el ejemplo siguiente.  
  
```  
C:\Program Files\Microsoft SQL Server Parallel Data Warehouse\100\dwloader.exe –S <Control node IP> -E –M reload –e UTF16 -i .\DimAccount.txt –T AdventureWorksPDW2012.dbo.DimAccount –R DimAccount.bad –t "|" –r \r\n –U <login> -P <password>  
```  
  
Descripción de los parámetros de línea de comandos:  
  
-   *C:\Program Files\Microsoft SQL Server Parallel datos Warehouse\100\dwloader.exe* es la ubicación de la instalación de dwloader.exe.  
  
-   *-S* va seguido de la dirección IP del nodo de Control.  
  
-   *-E* especifica para cargar las cadenas vacías como NULL.  
  
-   *Volver a cargar -M* especifica para truncar la tabla de destino antes de insertar los datos de origen.  
  
-   *-e UTF16* indica el archivo de origen usa el tipo de codificación de caracteres endian poco.  
  
-   *-i.\DimAccount.txt* especifica los datos están en un archivo denominado DimAccount.txt que se encuentra en el directorio actual.  
  
-   *-T AdventureWorksPDW2012.dbo.DimAccount* especifica el nombre de parte 3 de la tabla para recibir los datos.  
  
-   *-R DimAccount.bad* especifica las filas que no se pudo cargar se escribirán en un archivo denominado DimAccount.bad.  
  
-   *– t "|"*  indica los campos en el archivo de entrada, DimAccount.txt, se separan con el carácter de barra vertical.  
  
-   *-r \r\n* especifica cada fila de DimAccount.txt termina con un retorno de carro y un salto de línea.  
  
-   *-U < login_name > -P <password>*  especifica el inicio de sesión y la contraseña para el inicio de sesión que tenga permisos para realizar la carga.  
  

<!-- MISSING LINK

## See Also  
[Common Metadata Query Examples](metadata-query-examples.md)  

-->
  
