---
title: Formato de archivo de texto (controlador de archivo de texto) | Documentos de Microsoft
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- delimited text lines
- fixed-width text files
- text format [ODBC]
- text file driver [ODBC], text format
ms.assetid: f53cd4b5-0721-4562-a90f-4c55e6030cb9
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: eb3505a7750bf2b538078139cf84b9e88a7e23bd
ms.contentlocale: es-es
ms.lasthandoff: 09/09/2017

---
# <a name="text-file-format-text-file-driver"></a>Formato de archivo de texto (controlador de archivo de texto)
El controlador de texto de ODBC admite tanto archivos de texto de ancho fijo y delimitado. Un archivo de texto está formada por una línea de encabezado opcional y cero o más líneas de texto.  
  
 Aunque en la línea de encabezado utiliza el mismo formato que las demás líneas del archivo de texto, el controlador de ODBC texto interpreta las entradas de la línea de encabezado como nombres de columna, no datos.  
  
 Una línea de texto delimitado contiene uno o más valores de datos separados por delimitadores: comas, tabulaciones o un delimitador personalizado. En el archivo se debe utilizar el mismo delimitador. Valores de datos nulos se denotan mediante dos delimitadores en una fila sin datos entre ellos. Cadenas de caracteres en una línea de texto delimitados pueden incluirse entre comillas dobles (""). Espacios en blanco no pueden producir antes o después de valores delimitados.  
  
 Se especifica el ancho de cada entrada de datos en una línea de texto de ancho fijo en un esquema. Valores de datos nulos se denotan mediante espacios en blanco.  
  
 Las tablas están limitadas a un máximo de 255 campos. Nombres de campo están limitados a 64 caracteres, y se limita a 32.766 caracteres anchos de campo. Los registros están limitados a 65.000 bytes.  
  
 Solo para un solo usuario, se puede abrir un archivo de texto. No se admiten varios usuarios.  
  
 La gramática siguiente, escrita para los programadores, define el formato de un archivo de texto que puede leerse mediante el controlador ODBC de texto:  
  
|Formato|Representación|  
|------------|--------------------|  
|No cursiva|Caracteres que deben escribirse tal como se muestra|  
|*cursiva*|Argumentos que se definen en otro lugar en la gramática|  
|Corchetes ([])|Elementos opcionales|  
|llaves ({})|Una lista de opciones mutuamente excluyentes|  
|barras verticales (&#124;)|Opciones mutuamente excluyentes diferentes|  
|botón de puntos suspensivos (...)|Elementos que se pueden repetir una o varias veces|  
  
 El formato de un archivo de texto es:  
  
```  
text-file ::=  
   [delimited-header-line] [delimited-text-line]... end-of-file |  
   [fixed-width-header-line] [fixed-width-text-line]... end-of-file  
delimited-header-line ::= delimited-text-line  
delimited-text-line ::=  
   blank-line |  
   delimited-data [delimiter delimited-data]... end-of-line  
fixed-width-header-line ::= fixed-width-text-line  
fixed-width-text-line ::=  
   blank-line |  
   fixed-width-data [fixed-width-data]... end-of-line  
end-of-file ::= <EOF>  
blank-line ::= end-of-line  
delimited-data ::= delimited-string | number | date | delimited-null  
fixed-width-data ::= fixed-width-string | number | date | fixed-width-null  
```  
  
> [!NOTE]  
>  El ancho de cada columna en un archivo de texto de ancho fijo se especifica en el archivo Schema.ini.  
  
```  
  
      end-of-line ::= <CR> | <LF> | <CR><LF>  
delimited-string ::= unquoted-string | quoted-stringunquoted-string ::= [character | digit] [character | digit | quote-character]...  
quoted-string ::=  
   quote-character  
   [character | digit | delimiter | end-of-line | embedded-quoted-string]...  
   quote-characterembedded-quoted-string ::=   quote-characterquote-character  
   [character | digit | delimiter | end-of-line]  
   quote-characterquote-characterfixed-width-string ::= [character | digit | delimiter | quote-character] ...  
character ::= any character except:  
   delimiterdigitend-of-fileend-of-linequote-characterdigit ::= 0 | 1 | 2 | 3 | 4 | 5 | 6 | 7 | 8 | 9  
delimiter ::= , | <TAB> |   
custom-delimitercustom-delimiter ::= any character except:  
   end-of-fileend-of-linequote-character  
```  
  
> [!NOTE]  
>  El delimitador de un archivo de texto delimitado personalizado se especifica en el archivo Schema.ini.  
  
```  
quote-character ::= "  
number ::= exact-number | approximate-number  
exact-number ::= [+ | -] {unsigned-integer[.unsigned-integer] |  
   unsigned-integer. |  
   .unsigned-integer}  
approximate-number ::= exact-number{e | E}[+ | -]unsigned-integer  
unsigned-integer ::= {digit}...  
date ::=  
   mm date-separator dd date-separator yy |  
   mmm date-separator dd date-separator yy |  
   dd date-separator mmm date-separator yy |  
   yyyy date-separator mm date-separator dd |  
   yyyy date-separator mmm date-separator dd  
mm ::= digit [digit]  
dd ::= digit [digit]  
yy ::= digit digit  
yyyy ::= digit digit digit digit  
mmm ::= Jan | Feb | Mar | Apr | May | Jun | Jul | Aug | Sep | Oct | Nov | Dec  
date-separator ::= - | / | .  
delimited-null ::=  
```  
  
> [!NOTE]  
>  Para los archivos delimitados, un valor NULL se representa mediante ningún dato entre dos delimitadores.  
  
```  
fixed-width-null ::= <SPACE>...  
```  
  
> [!NOTE]  
>  Para los archivos de ancho fijo, un valor NULL se representa por espacios.

