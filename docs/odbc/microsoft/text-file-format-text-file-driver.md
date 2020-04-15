---
title: Formato de archivo de texto (controlador de archivo de texto) Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- delimited text lines
- fixed-width text files
- text format [ODBC]
- text file driver [ODBC], text format
ms.assetid: f53cd4b5-0721-4562-a90f-4c55e6030cb9
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 5801433e0180bb07cb2d09a59db2bb74be012cdf
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/14/2020
ms.locfileid: "81303096"
---
# <a name="text-file-format-text-file-driver"></a>Formato de archivo de texto (controlador de archivo de texto)
El controlador de texto ODBC admite archivos de texto delimitados y de ancho fijo. Un archivo de texto consta de una línea de encabezado opcional y cero o más líneas de texto.  
  
 Aunque la línea de encabezado utiliza el mismo formato que las otras líneas del archivo de texto, el controlador de texto ODBC interpreta las entradas de línea de encabezado como nombres de columna, no como datos.  
  
 Una línea de texto delimitada contiene uno o varios valores de datos separados por delimitadores: comas, tabulaciones o un delimitador personalizado. El mismo delimitador debe utilizarse en todo el archivo. Los valores de datos nulos se indican mediante dos delimitadores en una fila sin datos entre ellos. Las cadenas de caracteres de una línea de texto delimitada se pueden incluir entre comillas dobles (""). No se pueden producir espacios en blanco antes o después de los valores delimitados.  
  
 El ancho de cada entrada de datos en una línea de texto de ancho fijo se especifica en un esquema. Los valores de datos nulos se indican mediante espacios en blanco.  
  
 Las tablas están limitadas a un máximo de 255 campos. Los nombres de campo están limitados a 64 caracteres y los anchos de campo están limitados a 32.766 caracteres. Los registros están limitados a 65.000 bytes.  
  
 Un archivo de texto solo se puede abrir para un solo usuario. No se admiten varios usuarios.  
  
 La siguiente gramática, escrita para programadores, define el formato de un archivo de texto que puede leer el controlador de texto ODBC:  
  
|Formato|Representación|  
|------------|--------------------|  
|No itálicos|Caracteres que deben introducirse como se muestra|  
|*Cursiva*|Argumentos que se definen en otra parte de la gramática|  
|brackets ([])|Elementos opcionales|  
|llaves ({})|Una lista de opciones mutuamente excluyentes|  
|barras verticales (&#124;)|Separe las opciones mutuamente excluyentes|  
|puntos suspensivos (...)|Elementos que se pueden repetir una o más veces|  
  
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
>  El delimitador de un archivo de texto delimitado por el usuario se especifica en el archivo Schema.ini.  
  
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
>  Para los archivos delimitados, un NULL se representa mediante ningún dato entre dos delimitadores.  
  
```  
fixed-width-null ::= <SPACE>...  
```  
  
> [!NOTE]  
>  Para los archivos de ancho fijo, un NULL se representa mediante espacios.
