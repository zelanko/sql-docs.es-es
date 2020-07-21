---
title: Funciones y comandos de Visual FoxPro no admitidos | Microsoft Docs
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 7e5b8ed06ad9f996d644df0dfb99d15adcff86bc
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/27/2020
ms.locfileid: "81307656"
---
# <a name="unsupported-visual-foxpro-commands-and-functions-visual-foxpro-odbc-driver"></a>No compatible de Visual FoxPro comandos y funciones (controlador ODBC de Visual FoxPro)
En la tabla siguiente se enumeran los comandos y las funciones de FoxPro que no son compatibles con el controlador ODBC de Visual FoxPro pero que son compatibles con Microsoft® Visual FoxPro®.  
  
 Si la aplicación interactúa con datos cuyas reglas, desencadenadores, valores predeterminados o procedimientos almacenados llaman a estos comandos o funciones de Visual FoxPro, el controlador puede generar un error.  
  
## <a name="unsupported-visual-foxpro-commands-and-functions"></a>Funciones y comandos de Visual FoxPro no admitidos  
  
||||  
|-|-|-|  
|#DEFINE... #UNDEF|#IF... #ENDIF Directiva de preprocesador|#IFDEF &#124; #IFNDEF|  
|#INCLUDE Directiva de preprocesador|:: Operador de resolución de ámbito|! Comando (vea ejecutar &#124;! Command|  
|? ¿&#124;?? Get-Help|??? Get-Help|\ &#124; \\\ comando|  
|@ ... BOX (comando)|@ ... CLASS (comando)|@ ... CLEAR (comando)|  
|@ ... Comando Editar cuadros de edición|@ ... FILL (comando)|@ ... Obtener|  
|@ ... Comando de menú|@ ... PROMPT (comando)|@ ... Comando SAY|  
|@ ... SCROLL (comando)|@ ... Comando TO||  
  
## <a name="a"></a>Un  
  
||||  
|-|-|-|  
|ACCEPT (comando)|ACLASS () (función)|Comando de menú activar|  
|ACTIVAR el comando POPUP|Activar pantalla (comando)|ACTIVAR ventana (comando)|  
|Método ActivateCell|Agregar clase (comando)|ADIR () (función)|  
|AFONT () (función)|AINSTANCE () (función)|_ALIGNMENT variable de memoria del sistema|  
|AMEMBERS () (función)|ANSITOOEM () (función)|APRINTERS () (función)|  
|ASELOBJ () (función)|AYUDA (comando)||  
  
## <a name="b"></a>B  
  
||||  
|-|-|-|  
|BAR () (función)|BARCOUNT () (función)|BARPROMPT () (función)|  
|_BEAUTIFY variable de memoria del sistema|_BOX variable de memoria del sistema|EXAMINAR (comando)|  
|_BROWSER variable de memoria del sistema|Comando de compilación de la aplicación|BUILD EXE (comando)|  
|Comando compilar proyecto|_BUILDER variable de memoria del sistema||  
  
## <a name="c"></a>C  
  
||||  
|-|-|-|  
|_CALCVALUE variable de memoria del sistema|_CLIPTEXT variable de memoria del sistema|_CONVERTER variable de memoria del sistema|  
|_CUROBJ variable de memoria del sistema|CALL (comando)|Cancelar (comando)|  
|CAPSLOCK () (función)|CD (comando)|CAMBIAR comando|  
|CHDIR (comando)|CHRSAW () (función)|CERRAR el comando de memorando|  
|CNTBAR () (función)|CNTPAD () (función)|COL () (función)|  
|Comando compilar|Comando compilar base de datos|Compilar comando de formulario|  
|COMPOBJ () (función)|Container (objeto)|Objeto de control|  
|COPIAR archivo (comando)|COPIAR memorando (comando)|Comando crear clase|  
|CREAR comando CLASSLIB|CREAR conjunto de colores (comando)|CREAR comando|  
|CREAR conexión (comando)|CREAR base de datos (comando)|CREAR formulario (comando)|  
|CREAR desde comando|Comando crear etiqueta|Comando de menú crear|  
|Comando crear proyecto|CREAR consulta (comando)|Comando crear informe|  
|CREAR pantalla (comando)|Comando crear vista SQL|CREAR DESENCADENAdor (comando)|  
|CREAR vista (comando)|CREATEOBJECT () (función)|CURDIR () (función)|  
  
## <a name="d"></a>D  
  
||||  
|-|-|-|  
|_DBLCLICK variable de memoria del sistema|_DIARYDATE variable de memoria del sistema|DBSETPROP () (función)|  
|Funciones DDE|Comando de menú desactivar|DESACTIVAR comando emergente|  
|DESACTIVAR ventana (comando)|Declare-DLL (comando)|Declare (comando)|  
|Comando de barra de definición|Comando definir cuadro|Comando definir clase|  
|DEFINIR el comando de menú|Comando definir panel|DEFINIR el comando POPUP|  
|Comando definir ventana|Comando eliminar conexión|ELIMINAR base de datos (comando)|  
|Comando eliminar archivo|Comando eliminar DESENCADENAdor|ELIMINAR Vista (comando)|  
|DIR (comando)|Comando de directorio|Mostrar comando|  
|Mostrar conexiones (comando)|Mostrar base de datos (comando)|Comando Mostrar archivos dll|  
|Mostrar archivos (comando)|Mostrar memoria (comando)|MOSTRAR objetos (comando)|  
|Comando Mostrar procedimientos|Mostrar estado (comando)|Mostrar estructura (comando)|  
|Comando Mostrar tablas|Comando mostrar vistas|HACER formulario (comando)|  
  
## <a name="e"></a>E  
  
||||  
|-|-|-|  
|Editar comando|ERROR (comando)||  
|Comando ERASe|Comando externo|Comando de exportación|  
|EJECT (comando)|Comando de la página EJECT||  
  
## <a name="f"></a>F  
  
||||  
|-|-|-|  
|_FOXDOC variable de memoria del sistema|_FOXGRAPH variable de memoria del sistema|FEOF () (función)|  
|FCLOSE () (función)|FCREATE () (función)|FGETS () (función)|  
|FERROR () (función)|FFLUSH () (función)|FKLABEL () (función)|  
|Comando de filtro|BUSCAR (comando)|FOPEN () (función)|  
|FKMAX () (función)|FONTMETRIC () (función)|FSEEK () (función)|  
|FPUTS () (función)|FREAD () (función)||  
|FWRITE () (función)|FCHSIZE () (función)||  
  
## <a name="g"></a>G  
  
||||  
|-|-|-|  
|_GENGRAPH variable de memoria del sistema|_GENMENU variable de memoria del sistema|_GENPD variable de memoria del sistema|  
|_GENSCRN variable de memoria del sistema|_GENXTAB variable de memoria del sistema|GETBAR () (función)|  
|GETCOLOR () (función)|GETDIR () (función)|Comando GETEXPR|  
|GETFILE () (función)|GETFONT () (función)|GETOBJECT () (función)|  
|GETPAD () (función)|GETPICT () (función)|GETPRINTER () (función)|  
  
## <a name="h"></a>H  
  
||||  
|-|-|-|  
|Comando ayuda|OCULTAR comando de menú|OCULTAR comando emergente|  
|OCULTAR ventana (comando)|Función HOME ()||  
  
## <a name="i"></a>I  
  
||||  
|-|-|-|  
|IMESTATUS () (función)|Comando importar|Comando de entrada|  
|INDEX ON (comando)|INKEY () (función)|ISCOLOR () (función)|  
|INSERTAR comando|INSMODE () (función)||  
|ISMOUSE () (función)|_INDENT variable de memoria del sistema||  
  
## <a name="j"></a>J  
  
||||  
|-|-|-|  
|JOIN (comando)|||  
  
## <a name="k"></a>K  
  
||||  
|-|-|-|  
|Comando de teclado|||  
  
## <a name="l"></a>L  
  
||||  
|-|-|-|  
|_LMARGIN variable de memoria del sistema|ETIQUETA (comando)|LASTKEY () (función)|  
|Función de ropa ()|Mostrar comandos|Comando ENUMERAr conexiones|  
|Comando LOAD|ARCHIVO LOCFILE () (función)||  
  
## <a name="m"></a>M  
  
||||  
|-|-|-|  
|MCOL () (función)|MD (comando)|MENÚ a comando|  
|MEMORY () (función)|Comando de menú|MKDIR (comando)|  
|MENU () (función)|MESSAGEBOX () (función)|Comando modificar conexión|  
|Comando modificar clase|Comando MODIFY COMMAND|Comando modificar formulario|  
|Comando MODIFY DATABASE|Comando MODIFY FILE|MODIFICAR el comando MEMO|  
|Comando modificar GENERAL|Comando modificar etiqueta|Comando modificar proyecto|  
|Comando de menú modificar|Comando MODIFY PROCEDURE|Comando modificar pantalla|  
|Comando modificar consulta|Comando modificar informe|Comando modificar ventana|  
|Comando modificar estructura|Comando modificar vista|Comando MOVE WINDOW|  
|Comando del MOUSE|MOVE (comando emergente)|MROW () (función)|  
|MRKBAR () (función)|MRKPAD () (función)||  
|MWINDOW () (función)|MDOWN () (función)||  
  
## <a name="n"></a>N  
  
||||  
|-|-|-|  
|NUMLOCK () (función)|||  
  
## <a name="o"></a>O  
  
||||  
|-|-|-|  
|OBJNUM () (función)|OBJTOCLIENT () (función)|Comando ON BAR|  
|OEMTOANSI () (función)|EN el comando APLABOUT|EN el comando de menú salir|  
|EN el comando ESCAPE|Comando al salir de la barra|EN la clave = comando|  
|Comando al salir del panel|EN salir (comando emergente)|Comando ON PAD|  
|EN el comando etiqueta de clave|EN el comando MACHELP|Comando en la barra de selección|  
|Comando ON PAGE|EN el comando READERROR|Comando emergente en la selección|  
|Comando del menú de selección|Comando en el panel de selección||  
|Comando ON SHUTDOWN|OBJVAR () (función)||  
  
## <a name="p"></a>P  
  
||||  
|-|-|-|  
|_PADVANCE variable de memoria del sistema|_PAGENO variable de memoria del sistema|_PBPAGE variable de memoria del sistema|  
|_PCOLNO variable de memoria del sistema|_PCOPIES variable de memoria del sistema|_PDRIVER variable de memoria del sistema|  
|_PDSETUP variable de memoria del sistema|_PECODE variable de memoria del sistema|_PEJECT variable de memoria del sistema|  
|_PEPAGE variable de memoria del sistema|_PLENGTH variable de memoria del sistema|_PLINENO variable de memoria del sistema|  
|_PLOFFSET variable de memoria del sistema|_PPITCH variable de memoria del sistema|_PQUALITY variable de memoria del sistema|  
|_PRETEXT variable de memoria del sistema|_PSCODE variable de memoria del sistema|_PSPACING variable de memoria del sistema|  
|_PWAIT variable de memoria del sistema|PAQUETE de base de datos (comando)|PAD () (función)|  
|PCOL () (función)|PEMSTATUS () (función)|Comando reproducir MACRO|  
|Comando de tecla de POP|Comando de menú emergente|POP (comando emergente)|  
|POPUP () (función)|PRINTJOB... Comando ENDPRINTJOB|PRINTSTATUS () (función)|  
|PRMBAR () (función)|PRMPAD () (función)|PROMPT () (función)|  
|PROW () (función)|PRTINFO () (función)|Comando de tecla de comando de extracción|  
|Comando de menú de extracción|Comando emergente de extracción|PUTFILE () (función)|  
  
## <a name="q"></a>Q  
  
||||  
|-|-|-|  
|Comando salir|||  
  
## <a name="r"></a>R  
  
||||  
|-|-|-|  
|_RMARGIN variable de memoria del sistema|RD (comando)|READKEY () (función)|  
|READ (comando)|Comando de menú leer|Comando de barra de versión|  
|REFRESH () (función)|REINDEX (comando)|Comando de la biblioteca de versión|  
|Comando RELEASE CLASSLIB|VERSIÓN (comando)|Comando del panel de versión|  
|Comando de menú de versión|Comando de módulo de versión|Comando de versión de WINDOWS|  
|Comando Mostrar elementos emergentes|Comando de procedimiento de versión|Rename (comando)|  
|QUITAR clase (comando)|Cambiar nombre de clase (comando)|Cambiar nombre de vista (comando)|  
|Comando cambiar nombre de conexión|Comando cambiar nombre de tabla|Comando restaurar desde|  
|Comando de informe|Requery () (función)|Comando restaurar ventana|  
|Comando RESTOre MACROs|Comando RESTOre SCREEN|RGBSCHEME () (función)|  
|Comando resume|RGB () (función)|EJECUTE &#124;. Get-Help|  
|RMDIR (comando)|ROW () (función)||  
|RUNSCRIPT (comando)|RDLEVEL () (función)||  
  
## <a name="s"></a>S  
  
||||  
|-|-|-|  
|Comando Guardar MACROs|Comando Guardar pantalla|GUARDAR en (comando)|  
|GUARDAR comando de WINDOWS|SCHEME () (función)|SCOLS () (función)|  
|SCROLL (comando)|_SCREEN variable de memoria del sistema|SET (comando)|  
|ESTABLECER comando alternativo|Comando de ANSI SET|Comando SET APLABOUT|  
|ESTABLECER el comando autosave|Comando SET BELL|ESTABLECER parpadeo (comando)|  
|Comando establecer borde|Comando SET BRSTATUS|Comando SET CLASSLIB|  
|Comando SET CLEAR|ESTABLECER reloj (comando)|ESTABLECER el COLOR del comando|  
|ESTABLECER COLOR del esquema (comando)|ESTABLECER conjunto de colores (comando)|ESTABLECER el COLOR en el comando|  
|ESTABLECER comando COMPATIBLE|ESTABLECER comando CONFIRM|ESTABLECER comando de consola|  
|ESTABLECER CPCOMPILE|ESTABLECER CPDIALOG|ESTABLECER moneda (comando)|  
|Comando SET CURSOR|ESTABLECER el comando de la sesión|ESTABLECER comando de depuración|  
|Comando SET DECIMALs|Comando establecer delimitadores|ESTABLECER el comando de desarrollo|  
|ESTABLECER dispositivo (comando)|ESTABLECER comando para mostrar|SET-HISTOry (comando)|  
|ESTABLECER Eco (comando)|ESTABLECER ESCAPE (comando)|Comando SET FORMAT|  
|Comando de la función SET|Comando establecer encabezados|ESTABLECER comando de ayuda|  
|Comando SET HELPFILTER|ESTABLECER intensidad (comando)|Comando SET KEY|  
|Comando SET KEYCOMP|Comando SET LOGERRORS|Comando SET MACDESKTOP|  
|Comando SET MACHELP|Comando SET MACKEY|ESTABLECER margen (comando)|  
|ESTABLECER marca de comando|ESTABLECER marcar en comando|Comando SET MEMOWIDTH|  
|Comando SET MESSAGE|ESTABLECER comando del MOUSE|Comando SET odómetro|  
|SET OLEOBJECT (comando)|Comando SET PALETte|Comando SET PDSETUP|  
|Comando SET POINT|Comando establecer impresora|Comando SET READBORDER|  
|ESTABLECER comando de actualización|ESTABLECER recurso (comando)|ESTABLECER comando de seguridad|  
|ESTABLECER el comando del panel de resultados|SET SECONDs (comando)|ESTABLECER separador (comando)|  
|Comando SET SHADOWs|Comando SET SKIP OF|Comando SET SPACE|  
|Comando SET STATUs|ESTABLECER la barra de estado (comando)|Comando SET STEP|  
|ESTABLECER comando permanente|Comando SET SYSFORMATS|Comando SET SYSMENU|  
|Comando SET TALK|Comando SET TEXTMERGE|Comando SET TEXTMERGE Delimiters|  
|Comando establecer tema|Comando establecer ID. de tema|Comando SET TRBETWEEN|  
|Comando SET escritura anticipada|Comando establecer vista|ESTABLECER ventana de comando de memorando|  
|Comando SET XCMDFILE|_SHELL variable de memoria del sistema|Mostrar comando GET|  
|Mostrar obtiene el comando|Mostrar comando de menú|Mostrar objeto (comando)|  
|Mostrar comando emergente|Mostrar ventana (comando)|SIZE (comando emergente)|  
|TAMAÑO de la ventana (comando)|SKPBAR () (función)|SKPPAD () (función)|  
|SOUNDEX () (función)|_SPELLCHK variable de memoria del sistema|Funciones SQL|  
|SROWS () (función)|_STARTUP variable de memoria del sistema|SUSPENDEr (comando)|  
|Funciones SYS () excepto SYS (2011)|SYSMETRIC () (función)||  
  
## <a name="t"></a>T  
  
||||  
|-|-|-|  
|_TABS variable de memoria del sistema|TEXTO... Comando ENDTEXT|TXTWIDTH () (función)|  
|TRANSFORM () (función)|_TRANSPORT variable de memoria del sistema||  
|Comando TYPE|_THROTTLE variable de memoria del sistema||  
  
## <a name="u"></a>U  
  
||||  
|-|-|-|  
|Función UPDATEd ()|USAR comando||  
  
## <a name="v"></a>V  
  
||||  
|-|-|-|  
|Comando validar base de datos|VARREAD () (función)|VERSION () (función)|  
  
## <a name="w"></a>W  
  
||||  
|-|-|-|  
|_WINDOWS variable de memoria del sistema|_WIZARD variable de memoria del sistema|WCHILD () (función)|  
|Comando WAIT|WBORDER () (función)|WFONT () (función)|  
|WCOLS () (función)|WEXIST () (función)|WLROW () (función)|  
|CON... Comando ENDWITH|WLAST () (función)|WONTOP () (función)|  
|WMAXIMUM () (función)|WLCOL () (función)|WREAD () (función)|  
|WOUTPUT () (función)|WMINIMUM () (función)|WVISIBLE () (función)|  
|WPARENT () (función)|WTITLE () (función)||  
|WROWS () (función)|_WRAP variable de memoria del sistema||  
  
## <a name="z"></a>Z  
  
||||  
|-|-|-|  
|Comando de la ventana ZOOM|||
