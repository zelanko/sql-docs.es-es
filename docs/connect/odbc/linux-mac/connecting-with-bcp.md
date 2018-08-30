---
title: Conexión con bcp | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- bcp
ms.assetid: 3eca5717-e50f-40db-be16-a1cebbdfee70
caps.latest.revision: 33
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 626f2144d29ba15d162e35c40ebc9b5b9317fded
ms.sourcegitcommit: 603d2e588ac7b36060fa0cc9c8621ff2a6c0fcc7
ms.translationtype: MTE75
ms.contentlocale: es-ES
ms.lasthandoff: 08/14/2018
ms.locfileid: "42785387"
---
# <a name="connecting-with-bcp"></a>Conexión con bcp
[!INCLUDE[Driver_ODBC_Download](../../../includes/driver_odbc_download.md)]

La utilidad [bcp](http://go.microsoft.com/fwlink/?LinkID=190626) está disponible en [!INCLUDE[msCoName](../../../includes/msconame_md.md)] ODBC Driver for [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] en Linux y MacOS. Esta página documenta las diferencias con respecto a la versión de Windows de `bcp`.
  
- El terminador de campo es una tabulación ("\t").  
  
- El terminador de línea es una nueva línea ("\n").  
  
- El modo de carácter es el formato preferido de los archivos de formato `bcp` y de datos que no contienen caracteres extendidos.  
  
> [!NOTE]  
> Las barras diagonales inversas "\\" de los argumentos de línea de comandos deben entrecomillarse o contener caracteres de escape. Por ejemplo, para especificar una nueva línea como terminador de fila personalizado debe utilizar uno de los siguientes mecanismos:  
>   
> -   -r\\\n  
> -   -r"\n"  
> -   -r'\n'  
  
A continuación, se muestra una invocación de ejemplo de un comando de `bcp` para copiar filas de la tabla en un archivo de texto:  
  
```  
bcp AdventureWorks2008R2.Person.Address out test.dat -Usa -Pxxxx -Sxxx.xxx.xxx.xxx  
```  
  
## <a name="available-options"></a>Opciones disponibles
En la versión actual, se encuentran disponibles las siguientes opciones y sintaxis:  

[*database***.**]* schema ***.*** table* **in** *data_file* | **out** *data_file*

- -a *packet_size*  
Especifica el número de bytes por paquete de red enviados y recibidos por el servidor.  
  
- -b *batch_size*  
Especifica el número de filas por lote de datos importados.  
  
- -c  
Utiliza un tipo de datos de caracteres.  
  
- -d *database_name*  
Especifica la base de datos a la que conectarse.  
  
- -d  
Hace que el valor transmitido a la opción `bcp` -S se interprete como un nombre de origen de datos (DSN). Para obtener más información, vea la sección "Compatibilidad con DSN en sqlcmd y bcp" de [Connecting with sqlcmd](../../../connect/odbc/linux-mac/connecting-with-sqlcmd.md).  
  
- -e *error_file* especifica la ruta completa de un archivo de error que se usa para almacenar las filas que la utilidad `bcp` no puede transferir del archivo a la base de datos.  
  
- -E  
Utiliza el valor o los valores de identidad del archivo de datos importado en la columna de identidad.  
  
- -f *format_file*  
Especifica la ruta de acceso completa de un archivo de formato.  
  
- -F *first_row*  
Especifica el número de la primera fila que se exportará desde una tabla o que se importará desde un archivo de datos.  
  
- -k  
Especifica que las columnas vacías deben conservar un valor NULL durante la operación, en vez de tener valores predeterminados para las columnas insertadas.  
  
- -l  
Especifica un tiempo de espera de inicio de sesión. La opción –l especifica el número de segundos que tienen que transcurrir antes de que un inicio de sesión en [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] agote el tiempo de espera cuando se trate de conectar a un servidor. El tiempo de espera de inicio de sesión predeterminado es 15 segundos. El período de tiempo de espera de inicio de sesión debe ser un número comprendido entre 0 y 65534. Si el valor proporcionado no es numérico o no está dentro de este intervalo, `bcp` genera un mensaje de error. Un valor de 0 especifica un tiempo de espera infinito.
  
- -L *last_row*  
Especifica el número de la última fila que se exportará desde una tabla o que se importará desde un archivo de datos.  
  
- -m *max_errors*  
Especifica el número máximo de errores de sintaxis que pueden producirse antes de que se cancele la operación de `bcp`.  
  
- -n  
Utiliza los tipos de datos nativos (de la base de datos) de los datos para realizar la operación de copia masiva.  
  
- -P *password*  
Especifica la contraseña para el identificador de inicio de sesión.  
  
- -Q  
Ejecuta la instrucción SET QUOTED_IDENTIFIERS ON en la conexión entre la utilidad `bcp` y una instancia de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
- -r *row_terminator*  
Especifica el terminador de la fila.  
  
- -r  
Especifica que se realice la copia masiva de datos de moneda, fecha y hora en [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] con el formato regional definido para la configuración regional del equipo cliente.  
  
- -S *server*  
Especifica el nombre de la [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] instancia para conectarse a, o si es -D utiliza, un DSN.  
  
- -t *field_terminator*  
Especifica el terminador del campo.  
  
- -T  
Especifica que la utilidad `bcp` se conecte a [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] con una conexión de confianza (seguridad integrada).  
  
- -U *login_id*  
Especifica el identificador de inicio de sesión para conectar con [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
- -V  
Facilita información acerca del número de versión y de los derechos de autor de la utilidad `bcp`.  
  
- -w  
Utiliza caracteres Unicode para realizar la operación de copia masiva.  
  
En esta versión, se admiten los caracteres Latin-1 y UTF-16.  
  
## <a name="unavailable-options"></a>Opciones no disponibles
En la versión actual, no se encuentran disponibles las siguientes opciones y sintaxis:  

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
Utiliza los tipos de datos de una versión anterior de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
- -X  
Si se usa con las opciones format y -f format_file, genera un archivo de formato basado en XML en lugar del archivo de formato predeterminado que no es XML.  
  
## <a name="see-also"></a>Ver también

[Conexión con **sqlcmd**](../../../connect/odbc/linux-mac/connecting-with-sqlcmd.md)  
