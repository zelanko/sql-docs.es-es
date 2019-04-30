---
title: Compatibilidad con procedimientos almacenados, desencadenadores, valores predeterminados y reglas | Microsoft Docs
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
manager: craigg
ms.openlocfilehash: 47795998b019df22b01852519f75f6e8d3d274dd
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "63269860"
---
# <a name="support-for-rules-triggers-default-values-and-stored-procedures-visual-foxpro-odbc-driver"></a>Compatibilidad con las reglas, desencadenadores, valores predeterminados y los procedimientos almacenados (controlador ODBC de Visual FoxPro)
No se puede crear reglas de Visual FoxPro, desencadenadores, valores predeterminados o procedimientos almacenados mediante el controlador ODBC de Visual FoxPro. Sin embargo, la aplicación podría interactuar con los procedimientos almacenados, desencadenadores, valores predeterminados o reglas existentes como inserta, actualiza o elimina datos de Visual FoxPro almacenados en una base de datos.  
  
 En la tabla siguiente se enumera los comandos de Visual FoxPro y las funciones admitidas por el controlador ODBC de Visual FoxPro cuando los comandos o las funciones que existen en procedimientos almacenados, desencadenadores, valores predeterminados o reglas.  
  
 Si su aplicación interactúa con los datos cuyas reglas, desencadenadores, valores predeterminados o llamar a procedimientos almacenados las otras funciones o los comandos de Visual FoxPro, el controlador generará un error. Consulte [no compatible de Visual FoxPro comandos y funciones](../../odbc/microsoft/unsupported-visual-foxpro-commands-and-functions-visual-foxpro-odbc-driver.md) para obtener una lista de comandos y funciones no admitidas por el controlador.  
  
> [!TIP]  
>  Si desea insertar código condicional en sus reglas, desencadenadores o procedimientos almacenados que determina los comandos que se ejecutará cuando se llama el controlador, puede usar el **() versión** función. El **() versión** función devuelve "controlador ODBC de Visual FoxPro  *\<versión >*" cuando lo llama el controlador.  
  
## <a name="visual-foxpro-commands-and-functions-supported-in-rules-triggers-default-values-and-stored-procedures"></a>Comandos de Visual FoxPro y las funciones admitidas en procedimientos almacenados, desencadenadores, valores predeterminados y reglas  
  
||||  
|-|-|-|  
|Operador $|% (Operador)|& Comando|  
|& & Comando|* Comando|= Comando|  
  
## <a name="a"></a>A  
  
||||  
|-|-|-|  
|ABS (función))|Función ACOPY)|Agregar tabla (comando)|  
|Función ADATABASES)|Función ADBOBJECTS)|Función AERROR)|  
|ADEL (función))|Función AELEMENT)|Función ALEN)|  
|Función AFIELDS)|Función AINS)|Modificar tabla - comando SQL|  
|Función ALIAS)|Función ALLTRIM)|ANEXAR desde el comando de matriz|  
|Y el operador|Comando APPEND|ANEXAR comando memorando|  
|ANEXAR de comando|ANEXAR comando GENERAL|Función ASCAN)|  
|ANEXE el comando de procedimientos|ASC (función))|Función ASUBSCRIPT)|  
|ASIN (función))|Función ASORT)|ATAN (función))|  
|EN función de)|Función AT_C)|Función ATCLINE)|  
|Función ATC)|Función ATCC)|Función AUSED)|  
|Función ATLINE)|ATN2 (función))||  
|Comando promedio|ACOS (función))||  
  
## <a name="b"></a>B  
  
||||  
|-|-|-|  
|Comando BEGIN TRANSACTION|ENTRE la función)|BITNOT (función))|  
|Función BITCLEAR)|Función BITLSHIFT)|Función de conjunto de bits)|  
|BITOR (función))|Función BITRSHIFT)|Comando en blanco|  
|Función BITTEST)|BITXOR (función))||  
|BOF (función))|BITAND (función))||  
  
## <a name="c"></a>C  
  
||||  
|-|-|-|  
|CALCULAR el comando|Función de candidato)|Función de CHR)|  
|Función CDX)|CEILING (función))|Comandos CLOSE|  
|Función CHRTRAN)|Función CHRTRANC)|Copie el comando de índices|  
|Función CMONTH)|Comando CONTINUE|Copie el comando extendido de estructura|  
|Copie el comando de procedimientos|Copie el comando de estructura|COPIAR en el comando|  
|Copie el comando de etiqueta|COPIAR al comando de matriz|Función CPCONVERT)|  
|COS () función|RECUENTO de comandos|Función CTOD)|  
|Función CPCURRENT)|Función CPDBF)|Función CURSORSETPROP)|  
|Función CTOT)|Función CURSORGETPROP)||  
|Función CURVAL (de)|Función CDOW)||  
  
## <a name="d"></a>D  
  
||||  
|-|-|-|  
|Función de fecha)|Función de fecha y hora)|DAY (función))|  
|DBC (función))|Función DBF)|Función DBGETPROP)|  
|Función DBUSED)|ELIMINAR, comando SQL|Comando DELETE|  
|Eliminar etiqueta, comando|Función () eliminado|DESCENDENTE () (función)|  
|Función de diferencia)|Comando de dimensión|Función de espacio en disco)|  
|Función de DMA)|HACER CASO... Comando ENDCASE|Comando|  
|WHILE... Comando ENDDO|Función de DOW)|Función DTOC)|  
|Función de Destructor)|Función de dto)|Función DTOT)|  
  
## <a name="e"></a>E  
  
||||  
|-|-|-|  
|Función vacío (de)|EVALUAR la función)|Comando EXIT|  
|Función ERROR)|EXP (función))||  
|Comando de transacción de fin|EOF (función))||  
  
## <a name="f"></a>F  
  
||||  
|-|-|-|  
|Función FCOUNT)|Función FDATE)|Función de campo)|  
|Función de archivo)|Función de filtro)|Función FLDLIST)|  
|Función de MANADA)|FLOOR (función))|Comando de VACIADO|  
|FOR... Comando ENDFOR|PARA la función)|Se encontró una función)|  
|Comando de tabla libre|Función FSIZE)|FTIME (función))|  
|FULLPATH (función))|Comando de función|VF (función))|  
  
## <a name="g"></a>G  
  
||||  
|-|-|-|  
|RECOPILAR el comando|Función GETNEXTMODIFIED)|GO/GOTO Command|  
|Función GETFLDSTATE)|Función GOMONTH)||  
|Función GETCP)|GETENV (función))||  
  
## <a name="h"></a>H  
  
|||  
|-|-|  
|Función de encabezado)|HOUR (función))|  
  
## <a name="i"></a>I  
  
||||  
|-|-|-|  
|Función IDXCOLLATE)|IF... Comando ENDIF|IIF, función)|  
|Función INDBC)|Comando de índice|Función de lista de valores)|  
|Comando Insertar SQL|INT (función))|ISALPHA (función))|  
|ESBLANCO)|ISDIGIT (función))|Función ISEXCLUSIVE)|  
|ISLEADBYTE (función))|ISLOWER (función))|ISNULL (función))|  
|ISREADONLY (función))|ISUPPER (función))||  
  
## <a name="k"></a>K  
  
||||  
|-|-|-|  
|Función llave)|Función de coincidencia de clave)||  
  
## <a name="l"></a>L  
  
||||  
|-|-|-|  
|Función LEFT (de)|Función LEFTC)|Función LIKEC)|  
|Función LENC)|Al igual que la función)|LOCK (función))|  
|Comando LOCAL|Busque el comando|Función de búsqueda)|  
|LOG (función))|LOG10 (función))|LTRIM (función))|  
|Función LOWER de)|Comando LPARAMETERS||  
|Función LUPDATE)|LEN (función))||  
  
## <a name="m"></a>M  
  
||||  
|-|-|-|  
|Variable de memoria del sistema _MLINE|MAX (), función|Función MDX)|  
|MDY (función))|Función MEMLINES)|Función de mensaje)|  
|MIN, función)|Función MINUTE (de)|Función MLINE)|  
|Función MOD (de)|MONTH (función))|Función MTON)|  
  
## <a name="n"></a>N  
  
||||  
|-|-|-|  
|Función NDX)|NORMALIZE () (función)|Operador no|  
|Comando de nota|Función NTOM)|Función NVL)|  
  
## <a name="o"></a>O  
  
||||  
|-|-|-|  
|Se produce la función)|Función OLDVAL)|EN el comando ERROR|  
|EN el comando clave|EN función de)|Comando de base de datos abierta|  
|Operador OR|Función de orden)|Función de sistema operativo)|  
  
## <a name="p"></a>P  
  
||||  
|-|-|-|  
|Comando PACK|Función de los parámetros)|Función de pago)|  
|Comando de parámetros|Función principal (de)|Comando privada|  
|Función de PI)|Función de programa)|Función () adecuado|  
|Comando de procedimiento|PV () (función)||  
|Comando pública|() PADL &#124; () PADR &#124; PADC funciones de)||  
  
## <a name="r"></a>R  
  
||||  
|-|-|-|  
|RAND (función))|Función RAT)|Función RATC)|  
|Función RATLINE)|RECUPERAR comando|Función RECCOUNT)|  
|Función RECNO)|Función RECSIZE)|Comando REGIONAL|  
|Función de relación)|Quitar comando de tabla|Reemplazar (comando)|  
|REEMPLAZAR desde el comando de matriz|REPLICATE (función))|Vuelva a intentar el comando|  
|DEVOLVER el comando|Función () adecuado|Función RIGHTC)|  
|Función RLOCK)|Comando de recuperación|Función ROUND (de)|  
|Función RTOD)|RTRIM, función)||  
  
## <a name="s"></a>S  
  
||||  
|-|-|-|  
|SCAN ... Comando ENDSCAN|Comando de DISPERSIÓN|Función de seg.)|  
|Función de segundos)|Comando Buscar|SEEK (función))|  
|Seleccione el comando|Función SELECT (de)|Comando SELECT-SQL|  
|Comando BLOCKSIZE Set|SET CARRY Command|Comando de siglo Set.|  
|Comando COLLATE Set|CONJUNTO de comandos de base de datos|CONJUNTO de comandos de fecha|  
|Comando de conjunto predeterminado|Comando de eliminaciones de Set|Comando exacto de conjunto|  
|Comando exclusivo de Set|Comando FDOW Set.|Comando de conjunto de campos|  
|Comando de filtro de conjunto|CONJUNTO de comandos fijos|Comando FULLPATH Set.|  
|Comando FWEEK Set.|HORAS de conjunto de comandos|CONJUNTO de comandos de índice|  
|CONJUNTO de comandos de bloqueo|Comando MULTILOCKS tenga el valor de SET|ESTABLECER cerca del comando|  
|Comando NOCPTRANS Set.|CONJUNTO de comandos de notificación|Comando NULL del conjunto|  
|CONJUNTO de comandos de optimización|Comando de orden del conjunto|Comando de ruta de acceso set|  
|CONJUNTO de comandos de procedimiento|CONJUNTO de comandos de relación|RELACIÓN de conjunto de comando de apagado|  
|CONJUNTO de comandos de volver a procesar|ESTABLECE el comando omitir|Comando UDFPARMS Set.|  
|CONJUNTO único comando|CONJUNTO de comandos de volumen|Función de conjunto)|  
|Función SETFLDSTATE)|Función de inicio de sesión)|Función de seno)|  
|Comando omitir|Comando SORT|Función de espacio)|  
|SQRT (función))|Comando de almacén|Función de STR)|  
|STRCONV (función))|Función STRTRAN)|Función de material)|  
|Función STUFFC)|SUBSTR (función))|Función SUBSTRC)|  
|Comando suma|Función sys(2011)||  
  
## <a name="t"></a>T  
  
||||  
|-|-|-|  
|Variable de memoria del sistema _TALLY|Variable de memoria del sistema _TRIGGERLEVEL|Función TAGCOUNT)|  
|Ejecute TABLEUPDATE (función))|Función de etiqueta)|Función de destino)|  
|Función TAGNO)|Función TAN (de)|TRIM (función))|  
|Función de tiempo)|Comando TOTAL|Función TXNLEVEL)|  
|Función TTOC)|Función TTOD)||  
|Función de tipo)|Función TABLEREVERT)||  
  
## <a name="u"></a>U  
  
||||  
|-|-|-|  
|Función únicos de)|UNLOCK, comando|USE el comando|  
|Comando de actualización|Función UPPER)||  
|USA la función)|Comando de SQL de actualización||  
  
## <a name="v"></a>V  
  
||||  
|-|-|-|  
|VAL (función))|Función de versión)||  
  
## <a name="w"></a>W  
  
||||  
|-|-|-|  
|SEMANA (función))|||  
  
## <a name="y"></a>S  
  
||||  
|-|-|-|  
|YEAR (función))|||  
  
## <a name="z"></a>Z  
  
||||  
|-|-|-|  
|Comando ZAP|||
