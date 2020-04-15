---
title: Soporte para Reglas, Desencadenadores, Valores Predeterminados y Procedimientos Almacenados ? Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- Visual FoxPro ODBC driver [ODBC], stored procedures
- FoxPro ODBC driver [ODBC], commands and functions
- commands for FoxPro ODBC driver [ODBC]
- FoxPro ODBC driver [ODBC], default values
- FoxPro ODBC driver [ODBC], triggers
- stored procedures [ODBC], Visual FoxPro ODBC driver
- Visual FoxPro ODBC driver [ODBC], rules
- FoxPro commands and functions [ODBC]
- rules [ODBC]
- Visual FoxPro ODBC driver [ODBC], default values
- FoxPro ODBC driver [ODBC], rules
- functions [ODBC], Visual FoxPro
- default values [ODBC]
- Visual FoxPro ODBC driver [ODBC], commands and functions
- Visual FoxPro ODBC driver [ODBC], triggers
- FoxPro ODBC driver [ODBC], stored procedures
- Visual FoxPro commands and functions [ODBC]
ms.assetid: e449de20-d6ca-4902-9f8e-814eb6e86650
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 2fcf8e7c80b2712313cba81199489dc7cb06dce0
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/14/2020
ms.locfileid: "81301142"
---
# <a name="support-for-rules-triggers-default-values-and-stored-procedures-visual-foxpro-odbc-driver"></a>Compatibilidad con las reglas, desencadenadores, valores predeterminados y los procedimientos almacenados (controlador ODBC de Visual FoxPro)
No puede crear reglas, desencadenadores, valores predeterminados o procedimientos almacenados de Visual FoxPro mediante el controlador ODBC de Visual FoxPro. Sin embargo, la aplicación puede interactuar con reglas, desencadenadores, valores predeterminados o procedimientos almacenados existentes a medida que inserta, actualiza o elimina los datos de Visual FoxPro almacenados en una base de datos.  
  
 En la tabla siguiente se enumeran los comandos y funciones de Visual FoxPro admitidos por el controlador ODBC de Visual FoxPro cuando los comandos o funciones existen en reglas, desencadenadores, valores predeterminados o procedimientos almacenados.  
  
 Si la aplicación interactúa con datos cuyas reglas, desencadenadores, valores predeterminados o procedimientos almacenados llaman a cualquier otro comando o función de Visual FoxPro, el controlador genera un error. Consulte [Comandos y funciones](../../odbc/microsoft/unsupported-visual-foxpro-commands-and-functions-visual-foxpro-odbc-driver.md) de Visual FoxPro no compatibles para obtener una lista de comandos y funciones no compatibles con el controlador.  
  
> [!TIP]  
>  Si desea insertar código condicional en las reglas, desencadenadores o procedimientos almacenados que determina los comandos que se ejecutarán cuando el controlador lo llame, puede utilizar la función **VERSION().** La función **VERSION( )** devuelve "Visual FoxPro ODBC Driver * \<version>" *cuando el controlador lo llama.  
  
## <a name="visual-foxpro-commands-and-functions-supported-in-rules-triggers-default-values-and-stored-procedures"></a>Comandos y funciones de Visual FoxPro compatibles con reglas, desencadenadores, valores predeterminados y procedimientos almacenados  
  
||||  
|-|-|-|  
|$ Operador|Operador %|Comando &|  
|Comando && |* Comando|• Comando|  
  
## <a name="a"></a>Un  
  
||||  
|-|-|-|  
|Función ABS( )|Función ACOPY( )|COMANDO ADD TABLE|  
|Función ADATABASES( )|Función ADBOBJECTS( )|Función AERROR( )|  
|Función ADEL( )|Función AELEMENT( )|AlEN( ) Función|  
|Función AFIELDS( )|Función AINS( )|Modificar tabla - comando SQL|  
|Función ALIAS( )|Función ALLTRIM( )|APPEND FROM ARRAY Command|  
|Y Operador|Comando APPEND|Comando APPEND MEMO|  
|APPEND FROM Command|Comando APPEND GENERAL|Función ASCAN( )|  
|COMANDO PROCEDIMIENTOS DE ANEXIONAR|Función ASC( )|Función ASUBSCRIPT( )|  
|Función ASIN( )|Función ASORT( )|Función ATAN( )|  
|At( ) Función|AT_C( ) Función|Función ATCLINE( )|  
|Función ATC( )|AtCC( ) Función|Función AUSED( )|  
|Función ATLINE( )|Función ATN2( )||  
|Comando PROMEDIO|Función ACOS( )||  
  
## <a name="b"></a>B  
  
||||  
|-|-|-|  
|Begin TRANSACTION Comando|BETWEEN( ) Función|Función BITNOT( )|  
|Función BITCLEAR( )|Función BITLSHIFT( )|Función BITSET( )|  
|Función BITOR( )|Función BITRSHIFT( )|Comando BLANK|  
|Función BITTEST( )|Función BITXOR( )||  
|Función BOF( )|Función BITAND( )||  
  
## <a name="c"></a>C  
  
||||  
|-|-|-|  
|Comando CALCULATE|Función CANDIDATE( )|Función CHR( )|  
|Función CDX( )|Función CEILING( )|Comandos CLOSE|  
|Función CHRTRAN( )|Función CHRTRANC( )|Comando COPY INDEXES|  
|Función CMONTH( )|COMANDO CONTINUAR|COPY STRUCTURE EXTENDED Command|  
|COMANDO COPY PROCEDURES|COMANDO COPY STRUCTURE|COPY TO Command|  
|Comando COPY TAG|COMANDO COPY TO ARRAY|Función CPCONVERT( )|  
|Función COS( )|Comando COUNT|Función CTOD( )|  
|Función CPCURRENT( )|Función CPDBF( )|FUNción CURSORSETPROP( )|  
|Función CTOT( )|FUNción CURSORGETPROP( )||  
|Función CURVAL( )|Función CDOW( )||  
  
## <a name="d"></a>D  
  
||||  
|-|-|-|  
|FUNción DATE( )|DateTIME( ) Función|Función DAY( )|  
|Función DBC( )|Función DBF( )|Función DBGETPROP( )|  
|Función DBUSED( )|ELIMINAR, comando SQL|Comando DELETE|  
|Eliminar etiqueta, comando|Función DELETED( )|Función DESCENDING( )|  
|FUNción DIFFERENCE( )|Comando DIMENSION|DiskSPACE( ) Función|  
|Función DMY( )|CASO DE HACER ... Comando ENDCASE|Comando DO|  
|HACER MIENTRAS ... Comando ENDDO|Función DOW( )|Función DTOC( )|  
|Función DTOR( )|Función DTOS( )|Función DTOT( )|  
  
## <a name="e"></a>E  
  
||||  
|-|-|-|  
|Función EMPTY( )|Función EVALUATE( )|Comando EXIT|  
|FUNción ERROR( )|Función EXP( )||  
|End TRANSACTION Comando|Función EOF( )||  
  
## <a name="f"></a>F  
  
||||  
|-|-|-|  
|Función FCOUNT( )|Función FDATE( )|FIELD( ) Función|  
|Función FILE( )|FUNción FILTER( )|Función FLDLIST( )|  
|Flock( ) Función|FUNCIÓN FLOOR( )|Comando FLUSH|  
|Para... Comando ENDFOR|Función FOR( )|Función FOUND( )|  
|Comando DE TABLA GRATIS|Función FSIZE( )|Función FTIME( )|  
|FullPATH( ) Función|Comando FUNCTION|Función FV( )|  
  
## <a name="g"></a>G  
  
||||  
|-|-|-|  
|MANDATO GATHER|FUNción GETNEXTMODIFIED( )|Comando GO/GOTO|  
|FUNción GETFLDSTATE( )|GOMONTH( ) Función||  
|Función GETCP( )|GETENV( ) Función||  
  
## <a name="h"></a>H  
  
|||  
|-|-|  
|Función HEADER( )|Función HOUR( )|  
  
## <a name="i"></a>I  
  
||||  
|-|-|-|  
|Función IDXCOLLATE( )|Si... Comando ENDIF|Función IIF( )|  
|Función INDBC( )|Comando de índice|Función INLIST( )|  
|Comando INSERT-SQL|Función INT( )|Función ISALPHA( )|  
|Función ISBLANK( )|Función ISDIGIT( )|Función ISEXCLUSIVE( )|  
|Función ISLEADBYTE( )|Función ISLOWER( )|Función ISNULL( )|  
|Función ISREADONLY( )|Función ISUPPER( )||  
  
## <a name="k"></a>K  
  
||||  
|-|-|-|  
|FUNción KEY( )|Función KEYMATCH( )||  
  
## <a name="l"></a>L  
  
||||  
|-|-|-|  
|Función IZQUIERDA( )|Función LEFTC( )|Función LIKEC( )|  
|Función LENC( )|Función LIKE( )|Función LOCK( )|  
|Comando LOCAL|Comando LOCATE|FUNción LOOKUP( )|  
|Función LOG( )|Función LOG10( )|Función LTRIM( )|  
|Función LOWER( )|Comando LPARAMETERS||  
|LUPDATE( ) Función|Función LEN( )||  
  
## <a name="m"></a>M  
  
||||  
|-|-|-|  
|_MLINE Variable de memoria del sistema|MAX( ) Función|Función MDX( )|  
|MdY( ) Función|Función MEMLINES( )|Función MESSAGE( )|  
|Función MIN( )|FUNción MINUTE( )|Función MLINE( )|  
|Función MOD( )|FUNción MONTH( )|Función MTON( )|  
  
## <a name="n"></a>N  
  
||||  
|-|-|-|  
|Función NDX( )|Función NORMALIZE( )|NO Operador|  
|NOTA Comando|Función NTOM( )|Función NVL( )|  
  
## <a name="o"></a>O  
  
||||  
|-|-|-|  
|Función OCCURS( )|Función OLDVAL( )|Comando ON ERROR|  
|COMANDO ON KEY|Función ON( )|Comando OPEN DATABASE|  
|Operador OR|ORDER( ) Función|Función OS( )|  
  
## <a name="p"></a>P  
  
||||  
|-|-|-|  
|Comando PACK|Función PARAMETERS( )|FUNción PAGO( )|  
|Comando PARAMETERS|FUNción PRIMARY( )|Comando PRIVADO|  
|PI( ) Función|FUNción PROGRAM( )|Función PROPER( )|  
|Comando PROCEDURE|Función PV( )||  
|Comando PUBLICO|PADL( ) &#124; PADR( ) &#124; funciones PADC( )||  
  
## <a name="r"></a>R  
  
||||  
|-|-|-|  
|Función RAND( )|Función RAT( )|Función RATC( )|  
|Función RATLINE( )|COMANDO RECALL|RecCOUNT( ) Función|  
|RecNO( ) Función|RecSIZE( ) Función|Comando REGIONAL|  
|Relation( ) Función|Comando REMOVE TABLE|Comando REPLACE|  
|REPLACE FROM ARRAY Command|REPLICATE( ) Función|Comando RETRY|  
|Comando RETURN|Función DERECHA( )|Función RIGHTC( )|  
|Función RLOCK( )|Comando ROLLBACK|FUNción ROUND( )|  
|Función RTOD( )|Función RTRIM( )||  
  
## <a name="s"></a>S  
  
||||  
|-|-|-|  
|escanear... Comando ENDSCAN|Comando SCATTER|Función SEC( )|  
|Función SECONDS( )|SEEK Command|SEEK( ) Función|  
|Comando SELECT|Función SELECT( )|Comando SELECT-SQL|  
|Comando BLOCKSIZE Set|Comando SET CARRY|Comando SET CENTURY|  
|Comando COLLATE Set|Comando SET DATABASE|Comando SET DATE|  
|COMANDO SET DEFAULT|Comando de eliminaciones de Set|Comando exacto de conjunto|  
|Comando exclusivo de Set|Comando SET FDOW|Comando SET FIELDS|  
|Comando SET FILTER|SET FIXED Command|SET FULLPATH Command|  
|Comando SET FWEEK|Comando SET HOURS|Comando SET INDEX|  
|Comando SET LOCK|Comando SET MULTILOCKS|SET NEAR Command|  
|COMANDO SET NOCPTRANS|COMANDO SET NOTIFY|Comando NULL del conjunto|  
|COMANDO SET OPTIMIZE|Comando SET ORDER|Comando de ruta de acceso set|  
|COMANDO SET PROCEDURE|Comando SET RELATION|ESTABLECER RELACIÓN OFF Comando|  
|CONJUNTO de comandos de volver a procesar|Comando SET SKIP|Comando SET UDFPARMS|  
|CONJUNTO único comando|Comando SET VOLUME|Función SET( )|  
|Función SETFLDSTATE( )|FUNción SIGN ( )|Función SIN( )|  
|Comando SKIP|Comando SORT|Función SPACE( )|  
|Función SQRT( )|Comando STORE|Función STR( )|  
|Función STRCONV( )|Función STRTRAN( )|Stuff( ) Función|  
|Función STUFFC( )|FUNción SUBSTR( )|Función SUBSTRC( )|  
|Comando SUM|Función SYS(2011)||  
  
## <a name="t"></a>T  
  
||||  
|-|-|-|  
|_TALLY Variable de memoria del sistema|Variable de memoria del sistema _TRIGGERLEVEL|Función TAGCOUNT( )|  
|Función TABLEUPDATE( )|Función TAG( )|TARGET( ) Función|  
|Función TAGNO( )|Función TAN( )|Función TRIM( )|  
|Función TIME( )|Comando TOTAL|Función TXNLEVEL( )|  
|Función TTOC( )|Función TTOD( )||  
|Función TYPE( )|Función TABLEREVERT( )||  
  
## <a name="u"></a>U  
  
||||  
|-|-|-|  
|Función UNIQUE( )|Comando DESBLOQUEAR|Comando USE|  
|Comando UPDATE|Función UPPER( )||  
|FUNción US( )|Comando de SQL de actualización||  
  
## <a name="v"></a>V  
  
||||  
|-|-|-|  
|Función VAL( )|FUNción VERSION( )||  
  
## <a name="w"></a>W  
  
||||  
|-|-|-|  
|FUNción WEEK( )|||  
  
## <a name="y"></a>Y  
  
||||  
|-|-|-|  
|Year( ) Función|||  
  
## <a name="z"></a>Z  
  
||||  
|-|-|-|  
|Comando ZAP|||
