---
title: Comandos de Visual FoxPro y funciones no admitidas | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- FoxPro ODBC driver [ODBC], commands and functions
- functions [ODBC], Visual FoxPro
- Visual FoxPro ODBC driver [ODBC], commands and functions
- Visual FoxPro commands and functions
- FoxPro ODBC driver
ms.assetid: afdb6b7e-738d-42ca-8053-67ae50873ca6
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: c6b69c8bf15b4d56872c4030725638e4b61571e6
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "62633375"
---
# <a name="unsupported-visual-foxpro-commands-and-functions-visual-foxpro-odbc-driver"></a>No compatible de Visual FoxPro comandos y funciones (controlador ODBC de Visual FoxPro)
En la tabla siguiente se enumera FoxPro comandos y funciones que no son compatibles con el controlador ODBC de Visual FoxPro, pero son compatibles con Microsoft® Visual FoxPro.  
  
 Si su aplicación interactúa con los datos cuyas reglas, desencadenadores, valores predeterminados, o llamar a procedimientos almacenados de estos comandos de Visual FoxPro o funciones, el controlador puede generar un error.  
  
## <a name="unsupported-visual-foxpro-commands-and-functions"></a>Las funciones y comandos no compatible de Visual FoxPro  
  
||||  
|-|-|-|  
|#DEFINEN... #UNDEF|#IF... #ENDIF directiva de preprocesador|#IFDEF &#124; #IFNDEF|  
|#INCLUDE preprocesador (directiva)|:: Operador de resolución de ámbito|! Comando (vea ejecutar &#124; ! Comando)|  
|? &#124; ?? Comando|??? Comando|\ &#124; \\\ Comando|  
|@ ... Comando del cuadro|@ ... Comando de la clase|@ ... Comando CLEAR|  
|@ ... Editar - Editar comando cuadros|@ ... RELLENAR, comando|@ ... GET|  
|@ ... Comando de menú|@ ... Comando de símbolo del sistema|@ ... Comando de ejemplo|  
|@ ... Comando de desplazamiento|@ ... AL comando||  
  
## <a name="a"></a>A  
  
||||  
|-|-|-|  
|Acepte el comando|Función ACLASS)|ACTIVAR el comando de menú|  
|ACTIVAR la barra de comandos|Activar comandos de la pantalla|ACTIVAR la ventana de comando|  
|Método ActivateCell|Agregar clase (comando)|ADIR (función))|  
|Función AFONT)|Función AINSTANCE)|Variable de memoria del sistema _ALIGNMENT|  
|Función AMEMBERS)|Función ANSITOOEM)|Función APRINTERS)|  
|Función ASELOBJ)|Comando de ayuda||  
  
## <a name="b"></a>B  
  
||||  
|-|-|-|  
|BARRA de función)|Función BARCOUNT)|Función BARPROMPT)|  
|Variable de memoria del sistema _BEAUTIFY|Variable de memoria del sistema _BOX|Buscar comando|  
|Variable de memoria del sistema _BROWSER|Comando de la aplicación de compilación|GENERAR el comando EXE|  
|Comando de proyecto de compilación|Variable de memoria del sistema _BUILDER||  
  
## <a name="c"></a>C  
  
||||  
|-|-|-|  
|Variable de memoria del sistema _CALCVALUE|Variable de memoria del sistema _CLIPTEXT|Variable de memoria del sistema _CONVERTER|  
|Variable de memoria del sistema _CUROBJ|LLAMADAS (comando)|CANCELAR comandos|  
|CAPSLOCK (función))|Comando de CD|Comando de cambio|  
|Comando CHDIR|Función CHRSAW)|Comando de cierre memorando|  
|Función CNTBAR)|Función CNTPAD)|Función de COL)|  
|Comando de compilación|COMPILE el comando de base de datos|COMPILAR el formulario de comando|  
|Función COMPOBJ)|Objeto de contenedor|Objeto de control|  
|Copie el archivo (comando)|Copie el comando de RECORDATORIO|Crear comando de clase|  
|Crear comando CLASSLIB|Crear comando de conjunto de colores|CREAR un comando|  
|Crear comando de conexión|Crear comando de base de datos|CREAR comandos de formulario|  
|CREAR a partir de comando|Crear etiqueta, comando|Crear comando de menú|  
|CREAR el proyecto (comando)|Crear comando de consulta|CREAR informes, comando|  
|CREAR comandos de la pantalla|Crear comando de la vista SQL|CREAR DESENCADENADOR comando|  
|Crear comando de la vista|CREATEOBJECT (función))|DIRACT (función))|  
  
## <a name="d"></a>D  
  
||||  
|-|-|-|  
|Variable de memoria del sistema _DBLCLICK|Variable de memoria del sistema _DIARYDATE|Función DBSETPROP)|  
|Funciones DDE|DESACTIVAR el comando de menú|DESACTIVAR la barra de comandos|  
|DESACTIVAR la ventana de comando|DECLARAR - comando DLL|DECLARAR el comando|  
|DEFINIR la barra de comandos|DEFINIR el cuadro comando|DEFINIR el comando de clase|  
|DEFINIR el comando de menú|DEFINIR el comando del panel|DEFINIR la barra de comandos|  
|DEFINIR la ventana de comando|ELIMINAR la conexión, comando|Eliminar base de datos, comando|  
|Eliminar archivo (comando)|Comando de DESENCADENADOR DELETE|ELIMINAR el comando de la vista|  
|Comando DIR|Comando de directorio|Comando Mostrar|  
|Comando de conexiones de presentación|Comando de base de datos de presentación|Comando de mostrar los archivos DLL|  
|Mostrar archivos (comando)|Mostrar memoria (comando)|Comando de objetos de visualización|  
|Comando de procedimientos de presentación|Mostrar STATUS (comando)|Comando de la estructura de presentación|  
|Comando de tablas para mostrar|Comando de vistas de presentación|FORMULARIO de comando|  
  
## <a name="e"></a>E  
  
||||  
|-|-|-|  
|Editar comandos|Comando ERROR||  
|Comando de borrado|Comando externo|Comando de exportación|  
|Comando de expulsión|EXPULSAR el comando de página||  
  
## <a name="f"></a>F  
  
||||  
|-|-|-|  
|Variable de memoria del sistema _FOXDOC|Variable de memoria del sistema _FOXGRAPH|FEOF (función))|  
|FCLOSE (función))|Función FCREATE)|FGETS (función))|  
|FERROR (función))|FFLUSH (función))|Función FKLABEL)|  
|Comando de filtro|Buscar (comando)|FOPEN (función))|  
|Función FKMAX)|Función FONTMETRIC)|FSEEK (función))|  
|FPUTS (función))|FREAD (función))||  
|FWRITE (función))|Función FCHSIZE)||  
  
## <a name="g"></a>G  
  
||||  
|-|-|-|  
|Variable de memoria del sistema _GENGRAPH|Variable de memoria del sistema _GENMENU|Variable de memoria del sistema _GENPD|  
|Variable de memoria del sistema _GENSCRN|Variable de memoria del sistema _GENXTAB|Función GETBAR)|  
|GETCOLOR (función))|Función GETDIR)|Comando GETEXPR|  
|Función GETFILE)|GETFONT (función))|GETOBJECT (función))|  
|Función GETPAD)|Función GETPICT)|Función GETPRINTER)|  
  
## <a name="h"></a>H  
  
||||  
|-|-|-|  
|Comando de ayuda|OCULTAR el comando de menú|Ocultar barra de comandos|  
|OCULTAR la ventana de comando|Función principal (de)||  
  
## <a name="i"></a>I  
  
||||  
|-|-|-|  
|Función IMESTATUS)|Comando de importación|Comandos de entrada|  
|ÍNDICE en el comando|Función INKEY (de)|Función ISCOLOR)|  
|Insertar un comando|Función INSMODE)||  
|Función ISMOUSE)|Variable de memoria del sistema _INDENT||  
  
## <a name="j"></a>J  
  
||||  
|-|-|-|  
|Comando de combinación|||  
  
## <a name="k"></a>K  
  
||||  
|-|-|-|  
|Comando de teclado|||  
  
## <a name="l"></a>L  
  
||||  
|-|-|-|  
|Variable de memoria del sistema _LMARGIN|Comando de etiqueta|Función LASTKEY)|  
|Función LINENO)|LISTA de comandos|Mostrar conexiones (comando)|  
|Comando de carga|Función de archivo LOCFILE)||  
  
## <a name="m"></a>M  
  
||||  
|-|-|-|  
|Función MCOL)|Comando MD|MENÚ de comandos|  
|Función de memoria)|Comando de menú|Comando MKDIR|  
|Función de menú)|Cuadro de mensajes (función))|Modifique el comando de conexión|  
|Modifique el comando de clase|MODIFICAR comandos (comando)|MODIFICAR comandos de formulario|  
|Modifique el comando de base de datos|MODIFICAR el archivo (comando)|Modifique el comando de RECORDATORIO|  
|Modifique el comando de GENERAL|Modifique el comando de etiqueta|MODIFICAR el proyecto (comando)|  
|MODIFICAR comandos de menú|MODIFICAR comandos de procedimiento|MODIFICAR comandos de la pantalla|  
|Modifique el comando de consulta|MODIFICAR comandos de informe|VENTANA comandos de modificación|  
|Modifique el comando de estructura|Modifique el comando de la vista|MOVER la ventana de comando|  
|Comando de MOUSE|MOVER la barra de comandos|Función MROW)|  
|Función MRKBAR)|Función MRKPAD)||  
|Función MWINDOW)|Función MDOWN)||  
  
## <a name="n"></a>N  
  
||||  
|-|-|-|  
|Función de BLOQ NUM)|||  
  
## <a name="o"></a>O  
  
||||  
|-|-|-|  
|Función OBJNUM)|Función OBJTOCLIENT)|ON barra de comandos|  
|Función OEMTOANSI)|EN el comando APLABOUT|Comando de menú EXIT ON|  
|EN el comando de ESCAPE|EN la barra de comandos de salida|CLAVE = comando|  
|Comando del panel ON EXIT|Comando de menú emergente ON EXIT|Comando del panel ON|  
|EN el comando de la etiqueta de tecla|EN el comando MACHELP|EN la selección de la barra de comandos|  
|EN la página de comando|EN el comando READERROR|EN la barra de comandos de selección|  
|EN el comando de menú de selección|EN el comando del panel de selección||  
|EN el comando de apagado|Función OBJVAR)||  
  
## <a name="p"></a>P  
  
||||  
|-|-|-|  
|Variable de memoria del sistema _PADVANCE|Variable de memoria del sistema _PAGENO|Variable de memoria del sistema _PBPAGE|  
|Variable de memoria del sistema _PCOLNO|Variable de memoria del sistema _PCOPIES|Variable de memoria del sistema _PDRIVER|  
|Variable de memoria del sistema _PDSETUP|Variable de memoria del sistema _PECODE|Variable de memoria del sistema _PEJECT|  
|Variable de memoria del sistema _PEPAGE|Variable de memoria del sistema _PLENGTH|Variable de memoria del sistema _PLINENO|  
|Variable de memoria del sistema _PLOFFSET|Variable de memoria del sistema _PPITCH|Variable de memoria del sistema _PQUALITY|  
|Variable de memoria del sistema _PRETEXT|Variable de memoria del sistema _PSCODE|Variable de memoria del sistema _PSPACING|  
|Variable de memoria del sistema _PWAIT|Comando de base de datos del paquete|Función de panel)|  
|Función PCOL)|Función PEMSTATUS)|Comando de reproducción (macro)|  
|Comando ventana emergente de clave|Comando de menú emergente|Comando de menú emergente de confirmación|  
|Función de ventana emergente)|PRINTJOB... Comando ENDPRINTJOB|Función PRINTSTATUS)|  
|Función PRMBAR)|Función PRMPAD)|Función de símbolo del sistema (de)|  
|Función PROW)|Función PRTINFO)|TECLAS de comando de INSERCIÓN|  
|Comando de menú de INSERCIÓN|BARRA de comandos de INSERCIÓN|Función PUTFILE)|  
  
## <a name="q"></a>Q  
  
||||  
|-|-|-|  
|Salga de comando|||  
  
## <a name="r"></a>R  
  
||||  
|-|-|-|  
|Variable de memoria del sistema _RMARGIN|Comando de escritorio remoto|Función READKEY)|  
|LEER el comando|LEER el comando de menú|VERSIÓN de la barra de comandos|  
|Función Actualizar()|Volver a INDIZAR comando|Comando de la biblioteca de versión|  
|VERSIÓN CLASSLIB comando|Comando de versión|Comando del panel versión|  
|Comando de menús de la versión|Comando del módulo de versión|Comando de WINDOWS versión|  
|Comando de elementos emergentes de versión|Comando del procedimiento de versión|Cambiar el nombre de comando|  
|QUITAR el comando de la clase|Cambiar el nombre de comando de la clase|Cambiar el nombre de comando de la vista|  
|Cambiar el nombre de comando de conexión|Cambiar el nombre de comando de tabla|RESTAURAR a partir de comando|  
|Comando de informe|REQUERY () (función)|RESTAURAR ventana (comando)|  
|RESTAURAR comandos de MACROS|RESTAURAR comandos de la pantalla|Función RGBSCHEME)|  
|Comando RESUME|Función RGB)|EJECUTE &AMP;#124; ! Comando|  
|Comando RMDIR|Función de fila)||  
|Comando RUNSCRIPT|Función RDLEVEL)||  
  
## <a name="s"></a>S  
  
||||  
|-|-|-|  
|Guarde las MACROS de comandos|Guardar comandos de la pantalla|Guardar en el comando|  
|Guardar comandos de WINDOWS|Función de esquema)|Función SCOLS)|  
|Comando de desplazamiento|Variable de memoria del sistema _SCREEN|Comando Set.|  
|CONJUNTO de comandos alternativo|Comando de ANSI SET|Comando APLABOUT Set.|  
|Comando de AUTOGUARDADO Set.|Comando de la CAMPANA de SET|CONJUNTO de comandos de INTERMITENCIA|  
|CONJUNTO de comandos de borde|Comando BRSTATUS Set.|Comando CLASSLIB Set.|  
|Comando CLEAR conjunto|CONJUNTO de comandos de RELOJ|ESTABLECER el COLOR del comando|  
|ESTABLECER el COLOR del comando de esquema|Comando de conjunto de conjunto de COLOR|ESTABLECER el COLOR al comando|  
|Comando de conjunto COMPATIBLE|Comando de confirmación de SET|CONJUNTO de comandos de consola|  
|CONJUNTO CPCOMPILE|SET CPDIALOG|CONJUNTO de comandos de moneda|  
|SET CURSOR (comando)|Comando DATASESSION Set.|CONJUNTO de comandos de depuración|  
|CONJUNTO de comandos de decimales|Comando de conjunto de DELIMITADORES|CONJUNTO de comandos de desarrollo|  
|CONJUNTO de comandos de dispositivo|CONJUNTO de comandos de visualización|Comando DOHISTORY Set.|  
|Comando de eco Set.|Comando ESCAPE de SET|Comando de formato de conjunto|  
|Comando de la función de conjunto|Comando de conjunto de ENCABEZADOS|Comando de Ayuda de SET|  
|Comando HELPFILTER Set.|Comando de intensidad de SET|Comando de conjunto de claves|  
|Comando KEYCOMP Set.|Comando LOGERRORS Set.|Comando MACDESKTOP Set.|  
|Comando MACHELP Set.|Comando MACKEY Set.|CONJUNTO de comandos de margen|  
|MARQUE el conjunto de comandos|ESTABLECER la marca de comando|Comando del ancho del campo Memo Set.|  
|CONJUNTO de comandos de mensaje|CONJUNTO de comandos de MOUSE|Comando del CUENTAKILÓMETROS Set.|  
|CONJUNTO de clases OLEOBJECT comando|CONJUNTO de comandos de PALETA|Comando PDSETUP Set.|  
|Comando de punto fijo|CONJUNTO de comandos de impresora|Comando READBORDER Set.|  
|Comando de actualización de SET|Comando de conjunto de recursos|CONJUNTO de comandos de seguridad|  
|Comando del panel de resultados de conjunto|CONJUNTO de comandos de segundos|CONJUNTO de comandos de separador|  
|CONJUNTO de comandos de SOMBRAS|OMITIR del conjunto de comandos|CONJUNTO de comandos de espacio|  
|CONJUNTO STATUS (comando)|ESTABLECE el comando de barra de estado|CONJUNTO de comandos de paso|  
|Comando rápidas de SET|Comando SYSFORMATS Set.|Comando SYSMENU Set.|  
|CONJUNTO de comandos de charla|CONJUNTO de comandos de la combinación de texto|Comando de DELIMITADORES de la combinación de texto de SET|  
|CONJUNTO de comandos de tema|Comando de Id. de conjunto de tema|Comando TRBETWEEN Set.|  
|CONJUNTO de comandos de escritura anticipada|Comando de la vista de conjunto|VENTANA de conjunto de comandos de RECORDATORIO|  
|Comando XCMDFILE Set.|Variable de memoria del sistema _SHELL|Mostrar el comando GET|  
|Mostrar comando OBTIENE|Comando de menú Ver|Mostrar objeto (comando)|  
|Mostrar barra de comandos|Mostrar la ventana de comando|Comando de menú emergente de tamaño|  
|Comando de la ventana de tamaño|Función SKPBAR)|Función SKPPAD)|  
|Función SOUNDEX)|Variable de memoria del sistema _SPELLCHK|Funciones de SQL|  
|Función SROWS)|Variable de memoria del sistema _STARTUP|Comando de suspensión|  
|Funciones sys() excepto SYS(2011)|Función SYSMETRIC)||  
  
## <a name="t"></a>T  
  
||||  
|-|-|-|  
|Variable de memoria del sistema _TABS|TEXTO... Comando ENDTEXT|Función TXTWIDTH)|  
|TRANSFORMACIÓN de función)|Variable de memoria del sistema _TRANSPORT||  
|Comando de tipo|Variable de memoria del sistema _THROTTLE||  
  
## <a name="u"></a>U  
  
||||  
|-|-|-|  
|Función actualizada (de)|USE el comando||  
  
## <a name="v"></a>V  
  
||||  
|-|-|-|  
|VALIDAR el comando de base de datos|Función VARREAD)|Función de versión)|  
  
## <a name="w"></a>W  
  
||||  
|-|-|-|  
|Variable de memoria del sistema _WINDOWS|Variable de memoria del sistema _WIZARD|Función WCHILD)|  
|ESPERA de comando|Función WBORDER)|Función WFONT)|  
|Función WCOLS)|Función WEXIST)|Función WLROW)|  
|CON... Comando ENDWITH|Función WLAST)|Función WONTOP)|  
|Función de w máxima)|Función WLCOL)|Función WREAD)|  
|Función WOUTPUT)|Función WMINIMUM)|Función WVISIBLE)|  
|Función WPARENT)|Función WTITLE)||  
|Función WROWS)|Variable de memoria del sistema _WRAP||  
  
## <a name="z"></a>Z  
  
||||  
|-|-|-|  
|Comando de la ventana de ZOOM|||
