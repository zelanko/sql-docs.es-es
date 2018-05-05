---
title: Compatibilidad con procedimientos almacenados, desencadenadores, valores predeterminados y reglas | Documentos de Microsoft
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
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: ba9045b69420b70328071cbf3859ab29676260b9
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="support-for-rules-triggers-default-values-and-stored-procedures-visual-foxpro-odbc-driver"></a>Compatibilidad con las reglas, desencadenadores, valores predeterminados y los procedimientos almacenados (controlador ODBC de Visual FoxPro)
No se puede crear reglas de Visual FoxPro, desencadenadores, valores predeterminados o procedimientos almacenados con el controlador ODBC de Visual FoxPro. Sin embargo, la aplicación puede interactuar con los procedimientos almacenados, desencadenadores, valores predeterminados o reglas existentes tal y como inserta, actualiza o eliminan datos de Visual FoxPro almacenados en una base de datos.  
  
 En la tabla siguiente se enumera los comandos de Visual FoxPro y las funciones admitidas por el controlador ODBC de Visual FoxPro cuando los comandos o las funciones existen en los procedimientos almacenados, desencadenadores, valores predeterminados o reglas.  
  
 Si su aplicación interactúa con los datos cuyas reglas, desencadenadores, valores predeterminados o procedimientos almacenados llamar a cualquier otro comando de Visual FoxPro o funciones, el controlador genera un error. Vea [comandos no compatibles de Visual FoxPro y funciones](../../odbc/microsoft/unsupported-visual-foxpro-commands-and-functions-visual-foxpro-odbc-driver.md) para obtener una lista de comandos y funciones no admitidas por el controlador.  
  
> [!TIP]  
>  Si desea insertar código condicional en sus reglas, desencadenadores o procedimientos almacenados que determina los comandos que desea ejecutar cuando se llama por el controlador, puede usar el **() versión** (función). El **() versión** función devuelve "controlador de ODBC de Visual FoxPro  *\<versión >*" cuando se llama por el controlador.  
  
## <a name="visual-foxpro-commands-and-functions-supported-in-rules-triggers-default-values-and-stored-procedures"></a>Comandos de Visual FoxPro y las funciones admitidas en procedimientos almacenados, desencadenadores, valores predeterminados y reglas  
  
||||  
|-|-|-|  
|Operador de $|% (Operador)|& Comando|  
|& & Comando|* Comando|= Comando|  
  
## <a name="a"></a>A  
  
||||  
|-|-|-|  
|ABS () (función)|Función ACOPY)|Agregar tabla (comando)|  
|Función ADATABASES)|Función ADBOBJECTS)|Función AERROR)|  
|Función de ADEL)|Función AELEMENT)|Función ALEN)|  
|Función AFIELDS)|Función AINS)|Modificar tabla - comando SQL|  
|Función ALIAS)|Función ALLTRIM)|ANEXAR de comando de matriz|  
|AND (operador)|ANEXAR comando|ANEXAR comando memorando|  
|ANEXAR de comando|ANEXAR comando GENERAL|Función ASCAN)|  
|ANEXAR comando de procedimientos|ASC (función))|Función ASUBSCRIPT)|  
|ASIN (función))|Función ASORT)|ATAN (función))|  
|EN función de)|Función AT_C)|Función ATCLINE)|  
|Función de aéreo)|Función ATCC)|Función AUSED)|  
|Función ATLINE)|ATN2, función de)||  
|Comando promedio|ACOS (función))||  
  
## <a name="b"></a>B  
  
||||  
|-|-|-|  
|Comando BEGIN TRANSACTION|ENTRE la función)|BITNOT (función))|  
|Función BITCLEAR)|Función BITLSHIFT)|BITSET (función))|  
|BITOR () (función)|Función BITRSHIFT)|Comando en blanco|  
|Función BITTEST)|BITXOR (función))||  
|Función BOF)|BITAND (función))||  
  
## <a name="c"></a>C  
  
||||  
|-|-|-|  
|CALCULAR el comando|Función de candidato)|CHR (función))|  
|Función CDX)|CEILING (función))|Comandos CLOSE|  
|Función CHRTRAN)|Función CHRTRANC)|Copiar índices, comando|  
|Función CMONTH)|Comando CONTINUE|Copie el comando extendido de estructura|  
|Copie el comando de procedimientos|Copie el comando de estructura|COPIAR al comando|  
|Copie el comando de etiqueta|COPIAR al comando de matriz|Función CPCONVERT)|  
|COS función)|RECUENTO de comandos|Función CTOD)|  
|Función CPCURRENT)|Función CPDBF)|Función CURSORSETPROP)|  
|Función CTOT)|Función CURSORGETPROP)||  
|Función CURVAL)|Función CDOW)||  
  
## <a name="d"></a>D  
  
||||  
|-|-|-|  
|Función de fecha)|Función de fecha y hora)|DAY (función))|  
|Función DBC)|Función DBF)|Función DBGETPROP)|  
|Función DBUSED)|ELIMINAR, comando SQL|Comando DELETE|  
|Eliminar etiqueta, comando|Función eliminada)|DESCENDENTE () (función)|  
|DIFFERENCE () (función)|Comando de dimensión|Función () de espacio en disco|  
|Función de DMA)|HACER CASO... Comando ENDCASE|Comando|  
|WHILE... Comando ENDDO|Función de ventana)|Función DTOC)|  
|Función de Destructor)|Función de dto)|Función DTOT)|  
  
## <a name="e"></a>E  
  
||||  
|-|-|-|  
|Función vacío)|EVALUAR la función)|EXIT, comando|  
|Función ERROR)|EXP () (función)||  
|Comando END TRANSACTION|EOF () (función)||  
  
## <a name="f"></a>F  
  
||||  
|-|-|-|  
|Función FCOUNT)|Función FDATE)|Función de campo)|  
|Función de archivo)|FILTER () (función)|Función FLDLIST)|  
|Función de genealógico)|FLOOR (función))|Comando de VACIADO|  
|FOR... Comando ENDFOR|PARA la función)|Se encontró una función)|  
|Comando tabla libre|Función FSIZE)|FTIME (función))|  
|FULLPATH (función))|Comando (función)|VF (función))|  
  
## <a name="g"></a>G  
  
||||  
|-|-|-|  
|RECOPILAR el comando|Función GETNEXTMODIFIED)|Comando GO/GOTO|  
|Función GETFLDSTATE)|Función GOMONTH)||  
|Función GETCP)|GETENV () (función)||  
  
## <a name="h"></a>H  
  
|||  
|-|-|  
|Función de encabezado)|HOUR, función)|  
  
## <a name="i"></a>I  
  
||||  
|-|-|-|  
|Función IDXCOLLATE)|IF... Comando ENDIF|IIF, función)|  
|Función INDBC)|Comando de índice|Función de lista de valores)|  
|Comando SQL INSERT|INT () (función)|ISALPHA (función))|  
|Función ISBLANK)|ISDIGIT (función))|Función ISEXCLUSIVE)|  
|ISLEADBYTE (función))|ISLOWER (función))|ISNULL (), función|  
|ISREADONLY (función))|ISUPPER (función))||  
  
## <a name="k"></a>K  
  
||||  
|-|-|-|  
|Función de llave)|Función de coincidencia de clave)||  
  
## <a name="l"></a>L  
  
||||  
|-|-|-|  
|Función izquierdo)|Función LEFTC)|Función LIKEC)|  
|Función LENC)|Al igual que la función)|LOCK () (función)|  
|Comando LOCAL|Busque el comando|Función de búsqueda)|  
|LOG () (función)|LOG10 () (función)|LTRIM, función)|  
|LOWER, función)|Comando LPARAMETERS||  
|Función LUPDATE)|LEN (función))||  
  
## <a name="m"></a>M  
  
||||  
|-|-|-|  
|Variable de memoria del sistema _MLINE|MAX, función)|Función MDX)|  
|MDA (función))|Función MEMLINES)|Función del mensaje)|  
|MIN () (función)|Función MINUTE)|Función MLINE)|  
|Función MOD)|MONTH (función))|Función MTON)|  
  
## <a name="n"></a>N  
  
||||  
|-|-|-|  
|Función NDX)|NORMALIZAR función)|NOT (operador)|  
|Comando de nota|Función NTOM)|Función NVL)|  
  
## <a name="o"></a>O  
  
||||  
|-|-|-|  
|Se produce la función)|Función OLDVAL)|EN el comando ERROR|  
|EN el comando de teclas|EN función de)|Comando Abrir base de datos|  
|Operador OR|Función de orden)|Función de sistema operativo)|  
  
## <a name="p"></a>P  
  
||||  
|-|-|-|  
|Comando PACK|Función de parámetros)|Función de pago)|  
|Comando de parámetros|Función principal)|Comando privada|  
|Función de PI)|Función de programa)|Función correcta)|  
|PROCEDURE (comando)|PV () (función)||  
|Comando pública|() PADL &#124; () PADR &#124; funciones PADC)||  
  
## <a name="r"></a>L  
  
||||  
|-|-|-|  
|RAND (función))|Función de RATA)|Función RATC)|  
|Función RATLINE)|Recuerde comando|Función RECCOUNT)|  
|Función RECNO)|Función RECSIZE)|Comando REGIONAL|  
|Función de relación)|QUITAR el comando de tabla|Reemplazar (comando)|  
|REEMPLAZAR de comando de matriz|REPLICATE () (función)|Vuelva a ejecutar comando|  
|DEVOLVER el comando|Función derecho)|Función RIGHTC)|  
|Función RLOCK)|Comando de reversión|Función ROUND)|  
|Función RTOD)|RTRIM, función)||  
  
## <a name="s"></a>S  
  
||||  
|-|-|-|  
|EXAMINAR... Comando ENDSCAN|Comando de DISPERSIÓN|Función de seg.)|  
|Función de segundos)|Comando SEEK|SEEK (función))|  
|Seleccione el comando|SELECT () (función)|Comando SQL SELECT|  
|Comando BLOCKSIZE Set.|Comando de LLEVAN Set.|Comando de siglo Set.|  
|Comando COLLATE Set.|CONJUNTO de comandos de base de datos|CONJUNTO de comandos de fecha|  
|CONJUNTO de comandos predeterminado|Comando de eliminaciones de Set.|Comando exacto de conjunto|  
|Comando exclusivo de Set.|Comando FDOW|Comando de campos de conjunto|  
|Comando de filtro de conjunto|CONJUNTO de comandos fijos|Comando FULLPATH Set.|  
|Comando FWEEK|HORAS de conjunto de comandos|CONJUNTO de comandos de índice|  
|Comando de bloqueo de Set.|Comando MULTILOCKS tenga el valor de SET|ESTABLECER cerca del comando|  
|Comando NOCPTRANS|Comando de notificación de Set.|Comando NULL del conjunto|  
|Comando de optimizar Set.|Comando de orden de Set.|Comando de ruta de acceso set.|  
|CONJUNTO PROCEDURE (comando)|Comando de relación de Set.|RELACIÓN de conjunto de comando de apagado|  
|CONJUNTO de comandos de volver a procesar|ESTABLECE el comando omitir|Comando UDFPARMS|  
|CONJUNTO único comando|CONJUNTO de comandos de volumen|Función de conjunto)|  
|Función SETFLDSTATE)|Función de inicio de sesión)|SIN () (función)|  
|Comando omitir|Comando SORT|Función de espacio)|  
|SQRT (función))|Comando de almacenamiento|Función de STR)|  
|STRCONV () (función)|Función STRTRAN)|STUFF, función de)|  
|Función STUFFC)|SUBSTR (función))|Función SUBSTRC)|  
|Comando de suma|SYS(2011) (función)||  
  
## <a name="t"></a>T  
  
||||  
|-|-|-|  
|Variable de memoria del sistema _TALLY|Variable de memoria del sistema _TRIGGERLEVEL|Función TAGCOUNT)|  
|Ejecute TABLEUPDATE (función))|Función de etiqueta)|Función de destino)|  
|Función TAGNO)|Función TAN)|TRIM, función)|  
|Función de tiempo)|Comando TOTAL|Función TXNLEVEL)|  
|Función TTOC)|Función TTOD)||  
|Función de tipo)|Función TABLEREVERT)||  
  
## <a name="u"></a>U  
  
||||  
|-|-|-|  
|Función único)|UNLOCK, comando|USE el comando|  
|Comando de actualización|Función UPPER)||  
|USA la función)|Comando de SQL de actualización:||  
  
## <a name="v"></a>V  
  
||||  
|-|-|-|  
|VAL () (función)|Función de versión)||  
  
## <a name="w"></a>W  
  
||||  
|-|-|-|  
|SEMANA () (función)|||  
  
## <a name="y"></a>S  
  
||||  
|-|-|-|  
|YEAR (función))|||  
  
## <a name="z"></a>Z  
  
||||  
|-|-|-|  
|Comando ZAP|||
