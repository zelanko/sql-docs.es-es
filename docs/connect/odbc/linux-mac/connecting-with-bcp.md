---
title: "Conexión con bcp | Documentos de Microsoft"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: odbc
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords: bcp
ms.assetid: 3eca5717-e50f-40db-be16-a1cebbdfee70
caps.latest.revision: "33"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: f7e9db6a1ea636975a3f5719d9a1b3e9d5721eb6
ms.sourcegitcommit: 2713f8e7b504101f9298a0706bacd84bf2eaa174
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/18/2017
---
# <a name="connecting-with-bcp"></a>Conexión con bcp
[!INCLUDE[Driver_ODBC_Download](../../../includes/driver_odbc_download.md)]

El [bcp](http://go.microsoft.com/fwlink/?LinkID=190626) utilidad está disponible en la [!INCLUDE[msCoName](../../../includes/msconame_md.md)] ODBC Driver for [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] en Linux y macOS. Esta página documenta las diferencias con respecto a la versión de Windows `bcp`.
  
- El terminador de campo es una tabulación ("\t").  
  
- El terminador de línea es una nueva línea ("\n").  
  
- Modo de carácter es el formato preferido para `bcp` dar formato a los archivos y archivos de datos que no contienen caracteres extendidos.  
  
> [!NOTE]  
> Una barra diagonal inversa '\\' en un argumento de línea de comandos debe entrecomillarse o caracteres de escape. Por ejemplo, para especificar una nueva línea como terminador de fila personalizado, debe utilizar uno de los siguientes mecanismos:  
>   
> -   -r\\\n  
> -   -r"\n"  
> -   -r'\n'  
  
La siguiente es una invocación de comando de ejemplo de `bcp` para copiar filas de la tabla en un archivo de texto:  
  
```  
bcp AdventureWorks2008R2.Person.Address out test.dat -Usa -Pxxxx -Sxxx.xxx.xxx.xxx  
```  
  
## <a name="available-options"></a>Opciones disponibles
En la versión actual, la sintaxis y las opciones siguientes están disponibles:  

[*database***.**]*schema***.***table* **in** *data_file* | **out** *data_file*

- -a *packet_size*  
Especifica el número de bytes por paquete de red enviados y recibidos por el servidor.  
  
- -b *batch_size*  
Especifica el número de filas por lote de datos importados.  
  
- -c  
Utiliza un tipo de datos de caracteres.  
  
- -d *database_name*  
Especifica la base de datos a la que conectarse.  
  
- -d  
Hace que el valor pasado a la `bcp` opción -S se interprete como un nombre de origen de datos (DSN). Para obtener más información, vea "Compatibilidad con DSN en sqlcmd y bcp" en [conectar con sqlcmd](../../../connect/odbc/linux-mac/connecting-with-sqlcmd.md).  
  
- -e *error_file* especifica la ruta de acceso completa de un archivo de error que se usa para almacenarlas filas que la `bcp` utilidad no puede transferir del archivo a la base de datos.  
  
- -e  
Utiliza el valor o los valores de identidad del archivo de datos importado en la columna de identidad.  
  
- -f *format_file*  
Especifica la ruta de acceso completa de un archivo de formato.  
  
- -F *first_row*  
Especifica el número de la primera fila que se exportará desde una tabla o que se importará desde un archivo de datos.  
  
- -k  
Especifica que las columnas vacías deben conservar un valor NULL durante la operación, en vez de tener valores predeterminados para las columnas insertadas.  
  
- -l  
Especifica un tiempo de espera de inicio de sesión. La opción – l Especifica el número de segundos antes de que un inicio de sesión a [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] tiempos de espera al intentar conectarse a un servidor. El tiempo de espera de inicio de sesión predeterminado es 15 segundos. El tiempo de espera de inicio de sesión debe ser un número comprendido entre 0 y 65534. Si el valor proporcionado no es numérico o no está dentro de este intervalo, `bcp` genera un mensaje de error. Un valor de 0 especifica un tiempo de espera infinito.
  
- -L *last_row*  
Especifica el número de la última fila que se exportará desde una tabla o que se importará desde un archivo de datos.  
  
- -m *max_errors*  
Especifica el número máximo de errores de sintaxis que se pueden producir antes el `bcp` se cancela la operación.  
  
- -n  
Utiliza los tipos de datos nativos (de la base de datos) de los datos para realizar la operación de copia masiva.  
  
- -P *password*  
Especifica la contraseña para el identificador de inicio de sesión.  
  
- -Q  
Ejecuta la instrucción SET QUOTED_IDENTIFIERS ON en la conexión entre la utilidad `bcp` y una instancia de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)].  
  
- -r *row_terminator*  
Especifica el terminador de la fila.  
  
- -r  
Especifica que se realice la copia masiva de datos de moneda, fecha y hora en [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] con el formato regional definido para la configuración regional del equipo cliente.  
  
- -S *server*  
Especifica el nombre de la [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] instancia para conectarse a, o si es -D utiliza, un DSN.  
  
- -t *field_terminator*  
Especifica el terminador del campo.  
  
- -T  
Especifica que la `bcp` utilidad conectará a [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] con una conexión de confianza (seguridad integrada).  
  
- -U *login_id*  
Especifica el identificador de inicio de sesión para conectar con [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)].  
  
- -v  
Facilita información acerca del número de versión y de los derechos de autor de la utilidad `bcp`.  
  
- -w  
Utiliza caracteres Unicode para realizar la operación de copia masiva.  
  
En esta versión, se admiten los caracteres Latin-1 y UTF-16.  
  
## <a name="unavailable-options"></a>Opciones no disponibles
En la versión actual, la sintaxis y las opciones siguientes no están disponibles:  

- -c  
Especifica la página de códigos de los datos incluidos en el archivo de datos.  
  
- -h *hint*  
Especifica las sugerencias que deben usarse durante una importación de datos masiva en una tabla o vista.  
  
- -i *input_file*  
Especifica el nombre de un archivo de respuesta.  
  
- -n  
Utiliza los tipos de datos nativos (de la base de datos) para datos que no sean de caracteres, así como datos Unicode para los datos de caracteres.  
  
- -o *output_file*  
Especifica el nombre de un archivo que recibe la salida redirigida desde el símbolo del sistema.  
  
- -V (80 | 90 | 100)  
Utiliza los tipos de datos de una versión anterior de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)].  
  
- -x  
Si se usa con las opciones format y -f format_file, genera un archivo de formato basado en XML en lugar del archivo de formato predeterminado que no es XML.  
  
## <a name="see-also"></a>Vea también

[Conectar con **sqlcmd**](../../../connect/odbc/linux-mac/connecting-with-sqlcmd.md)  
