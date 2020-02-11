---
title: Compatibilidad con reglas, desencadenadores, valores predeterminados y procedimientos almacenados | Microsoft Docs
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 90a39ad540f3320ed78e981030679b59d911eeef
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "68080771"
---
# <a name="support-for-rules-triggers-default-values-and-stored-procedures-visual-foxpro-odbc-driver"></a>Compatibilidad con las reglas, desencadenadores, valores predeterminados y los procedimientos almacenados (controlador ODBC de Visual FoxPro)
No se pueden crear reglas, desencadenadores, valores predeterminados o procedimientos almacenados de Visual FoxPro mediante el controlador ODBC de Visual FoxPro. Sin embargo, la aplicación podría interactuar con las reglas, los desencadenadores, los valores predeterminados o los procedimientos almacenados existentes a medida que inserta, actualiza o elimina los datos de Visual FoxPro almacenados en una base de datos.  
  
 En la tabla siguiente se enumeran los comandos y las funciones de Visual FoxPro admitidos por el controlador ODBC de Visual FoxPro cuando los comandos o las funciones existen en reglas, desencadenadores, valores predeterminados o procedimientos almacenados.  
  
 Si la aplicación interactúa con datos cuyas reglas, desencadenadores, valores predeterminados o procedimientos almacenados llaman a cualquier otra función o comando de Visual FoxPro, el controlador genera un error. Consulte [funciones y comandos de Visual FoxPro no compatibles](../../odbc/microsoft/unsupported-visual-foxpro-commands-and-functions-visual-foxpro-odbc-driver.md) para obtener una lista de comandos y funciones no admitidos por el controlador.  
  
> [!TIP]  
>  Si desea insertar código condicional en las reglas, los desencadenadores o los procedimientos almacenados que determinan los comandos que se ejecutan cuando el controlador los llama, puede usar la función **version ()** . La función **version ()** devuelve " * \<versión *del controlador ODBC de Visual FoxPro>" cuando lo llama el controlador.  
  
## <a name="visual-foxpro-commands-and-functions-supported-in-rules-triggers-default-values-and-stored-procedures"></a>Comandos y funciones de Visual FoxPro admitidos en reglas, desencadenadores, valores predeterminados y procedimientos almacenados  
  
||||  
|-|-|-|  
|$ (Operador)|% (Operador)|Comando &|  
|Comando && |* Comando|= (Comando)|  
  
## <a name="a"></a>Un  
  
||||  
|-|-|-|  
|ABS () (función)|ACOPY () (función)|Agregar tabla (comando)|  
|ADATABASES () (función)|ADBOBJECTS () (función)|AERROR () (función)|  
|ADEL () (función)|AELEMENT () (función)|ALEN () (función)|  
|AFIELDS () (función)|AINS () (función)|Modificar tabla - comando SQL|  
|Función ALIAS ()|ALLTRIM () (función)|ANEXAr de la matriz (comando)|  
|AND (operador)|APPEND (comando)|APPEND (comando de memorando)|  
|ANEXAr desde (comando)|ANEXAr comando GENERAL|ASCAN () (función)|  
|Comando APPEND PROCEDUREs|ASC () (función)|ASUBSCRIPT () (función)|  
|ASIN () (función)|ASORT () (función)|ATAN () (función)|  
|AT () (función)|AT_C () (función)|ATCLINE () (función)|  
|ATC () (función)|ATCC () (función)|AUSED () (función)|  
|ATLINE () (función)|ATN2 () (función)||  
|PROMEDIO (comando)|ACOS () (función)||  
  
## <a name="b"></a>B  
  
||||  
|-|-|-|  
|Comando BEGIN TRANSACTION|BETWEEN () (función)|BITNOT () (función)|  
|BITCLEAR () (función)|BIT a bit () (función)|BITSET () (función)|  
|BITOR () (función)|BITRSHIFT () (función)|Comando en blanco|  
|Función DEBITTEST ()|Función BITXOR ()||  
|BOF () (función)|BITAND () (función)||  
  
## <a name="c"></a>C  
  
||||  
|-|-|-|  
|Comando CALCULAte|Función CANDIDAte ()|CHR () (función)|  
|CDX () (función)|Función CEILING ()|CERRAR comandos|  
|CHRTRAN () (función)|CHRTRANC () (función)|Comando Copiar índices|  
|CMONTH () (función)|Comando continuar|COPIAR estructura (comando extendido)|  
|Comando Copiar procedimientos|COPIAR estructura (comando)|COPIAR a (comando)|  
|Comando Copiar etiqueta|COPIAR en matriz (comando)|CPCONVERT () (función)|  
|COS () (función)|Recuento (comando)|CTOD () (función)|  
|CPCURRENT () (función)|CPDBF () (función)|CURSORSETPROP () (función)|  
|CTOT () (función)|CURSORGETPROP () (función)||  
|Función CURVAl ()|CDOW () (función)||  
  
## <a name="d"></a>D  
  
||||  
|-|-|-|  
|DATE () (función)|DATETIME () (función)|DAY () (función)|  
|DBC () (función)|DBF () (función)|DBGETPROP () (función)|  
|DBUSED () (función)|ELIMINAR, comando SQL|ELIMINAR comando|  
|Eliminar etiqueta, comando|Función DELETEd ()|Descending () (función)|  
|DIFFERENCE () (función)|Comando de dimensión|Función de espacio en la ()|  
|DMY () (función)|CASO... Comando ENDCASE|DO (comando)|  
|DO WHILE... Comando ENDDO|DOW () (función)|DTOC () (función)|  
|DTOR () (función)|DTO () (función)|DTOT () (función)|  
  
## <a name="e"></a>E  
  
||||  
|-|-|-|  
|EMPTY () (función)|EVALUAte () (función)|EXIT (comando)|  
|ERROR () (función)|EXP () (función)||  
|END TRANSACTION (comando)|EOF () (función)||  
  
## <a name="f"></a>F  
  
||||  
|-|-|-|  
|FCOUNT () (función)|FDATE () (función)|FIELD () (función)|  
|FILE () (función)|FILTER () (función)|FLDLIST () (función)|  
|Función de rebaño ()|Función FLOOR ()|VACIAr comando|  
|PARA... Comando ENDFOR|Función FOR ()|FOUND () (función)|  
|Comando de tabla libre|FSIZE () (función)|FTIME () (función)|  
|FULLPATH () (función)|Comando de función|FV () (función)|  
  
## <a name="g"></a>G  
  
||||  
|-|-|-|  
|RECOPILAr (comando)|GETNEXTMODIFIED () (función)|GO/GOTO (comando)|  
|GETFLDSTATE () (función)|GOMONTH () (función)||  
|GETCP () (función)|GETENV () (función)||  
  
## <a name="h"></a>H  
  
|||  
|-|-|  
|HEADER () (función)|HOUR () (función)|  
  
## <a name="i"></a>I  
  
||||  
|-|-|-|  
|IDXCOLLATE () (función)|IF... ENDIF (comando)|IIF () (función)|  
|INDBC () (función)|Comando de índice|Inlist () (función)|  
|Comando INSERT-SQL|INT () (función)|ISALPHA () (función)|  
|Función esblanco ()|ISDIGIT () (función)|ISEXCLUSIVE () (función)|  
|ISLEADBYTE () (función)|ISLOWER () (función)|ISNULL () (función)|  
|ISREADONLY () (función)|ISUPPER () (función)||  
  
## <a name="k"></a>K  
  
||||  
|-|-|-|  
|KEY () (función)|KEYMATCH () (función)||  
  
## <a name="l"></a>L  
  
||||  
|-|-|-|  
|LEFT () (función)|LEFTC () (función)|LIKEC () (función)|  
|LENC () (función)|LIKE () (función)|LOCK () (función)|  
|Comando LOCAL|LOCATE (comando)|LOOKUP () (función)|  
|Función LOG ()|LOG10 () (función)|LTRIM () (función)|  
|LOWER () (función)|Comando LPARAMETERS||  
|LUPDATE () (función)|LEN () (función)||  
  
## <a name="m"></a>M  
  
||||  
|-|-|-|  
|_MLINE variable de memoria del sistema|MAX () (función)|MDX () (función)|  
|MDA () (función)|MEMLINES () (función)|MESSAGE () (función)|  
|MIN () (función)|MINUTE () (función)|MLINE () (función)|  
|MOD () (función)|MONTH () (función)|MTON () (función)|  
  
## <a name="n"></a>N  
  
||||  
|-|-|-|  
|NDX () (función)|NORMALIZE () (función)|NOT (operador)|  
|NOTE (comando)|NTOM () (función)|NVL () (función)|  
  
## <a name="o"></a>O  
  
||||  
|-|-|-|  
|Función produce ()|OLDVAL () (función)|ON ERROR (comando)|  
|ON KEY (comando)|ON () (función)|Comando abrir base de datos|  
|Operador OR|ORDER () (función)|Función OS ()|  
  
## <a name="p"></a>P  
  
||||  
|-|-|-|  
|Comando PACK|Parameters () (función)|PAYMENT () (función)|  
|PARÁMETROS (comando)|PRIMAry () (función)|Comando privado|  
|PI () (función)|Función PROGRAM ()|NOMPROPIO () (función)|  
|PROCEDIMIENTO (comando)|PV () (función)||  
|Comando público|PADL () &#124; PADR () &#124; funciones PADC ()||  
  
## <a name="r"></a>R  
  
||||  
|-|-|-|  
|RAND () (función)|RAT () (función)|RATC () (función)|  
|RATLINE () (función)|Comando de recuperación|RECCOUNT () (función)|  
|RECNO () (función)|RECSIZE () (función)|Comando REGIONAL|  
|Función Relation ()|Comando quitar tabla|REEMPLAZAR (comando)|  
|REEMPLAZAR de la matriz (comando)|REPLICAte () (función)|Reintentar (comando)|  
|Comando Return|RIGHT () (función)|RIGHTC () (función)|  
|RLOCK () (función)|ROLLBACK (comando)|ROUND () (función)|  
|RTOD () (función)|RTRIM () (función)||  
  
## <a name="s"></a>S  
  
||||  
|-|-|-|  
|EXAMINAR... Comando ENDSCAN|DISPERSIÓN (comando)|SEC () (función)|  
|SECONDs () (función)|Comando de búsqueda|SEEK () (función)|  
|SELECCIONAR comando|SELECT () (función)|Comando SELECT-SQL|  
|Comando BLOCKSIZE Set|ESTABLECER comando de transporte|Comando SET CENTURY|  
|Comando COLLATE Set|ESTABLECER base de datos (comando)|ESTABLECER fecha (comando)|  
|ESTABLECER comando predeterminado|Comando de eliminaciones de Set|Comando exacto de conjunto|  
|Comando exclusivo de Set|Comando SET FDOW|Comando SET FIELDs|  
|ESTABLECER filtro (comando)|ESTABLECER comando fijo|SET FULLPATH (comando)|  
|Comando SET FWEEK|ESTABLECER horas (comando)|Comando SET INDEX|  
|ESTABLECER comando de bloqueo|ESTABLECER el comando de multilocks|ESTABLECER NEAR (comando)|  
|Comando SET NOCPTRANS|Comando SET NOTIFY|Comando NULL del conjunto|  
|Comando SET OPTIMIZe|Comando SET ORDER|Comando de ruta de acceso set|  
|Comando SET PROCEDURE|Comando SET Relation|Comando establecer relación desactivada|  
|CONJUNTO de comandos de volver a procesar|SET SKIP (comando)|Comando SET UDFPARMS|  
|CONJUNTO único comando|Comando SET VOLUME|SET () (función)|  
|SETFLDSTATE () (función)|SIGN () (función)|SIN () (función)|  
|SKIP (comando)|SORT (comando)|SPACE () (función)|  
|SQRT () (función)|Comando de almacenamiento|STR () (función)|  
|STRCONV () (función)|STRTRAN () (función)|Función material ()|  
|STUFFC () (función)|SUBSTR () (función)|SUBSTRC () (función)|  
|SUM (comando)|SYS (2011) (función)||  
  
## <a name="t"></a>T  
  
||||  
|-|-|-|  
|_TALLY variable de memoria del sistema|_TRIGGERLEVEL variable de memoria del sistema|TAGCOUNT () (función)|  
|TABLEUPDATE () (función)|TAG () (función)|TARGET () (función)|  
|TAGNO () (función)|TAN () (función)|TRIM () (función)|  
|TIME () (función)|TOTAL (comando)|TXNLEVEL () (función)|  
|TTOC () (función)|TTOD () (función)||  
|TYPE () (función)|TABLEREVERT () (función)||  
  
## <a name="u"></a>U  
  
||||  
|-|-|-|  
|UNIQUE () (función)|DESBLOQUEAR (comando)|USAR comando|  
|Comando UPDATE|UPPER () (función)||  
|Función USED ()|Comando de SQL de actualización||  
  
## <a name="v"></a>V  
  
||||  
|-|-|-|  
|VAL () (función)|VERSION () (función)||  
  
## <a name="w"></a>W  
  
||||  
|-|-|-|  
|WEEK () (función)|||  
  
## <a name="y"></a>Y  
  
||||  
|-|-|-|  
|YEAR () (función)|||  
  
## <a name="z"></a>Z  
  
||||  
|-|-|-|  
|ZAP (comando)|||
