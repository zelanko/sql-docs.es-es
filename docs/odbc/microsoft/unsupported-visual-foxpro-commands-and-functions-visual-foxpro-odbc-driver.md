---
title: Comandos y funciones de Visual FoxPro no compatibles ? Microsoft Docs
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
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/14/2020
ms.locfileid: "81307656"
---
# <a name="unsupported-visual-foxpro-commands-and-functions-visual-foxpro-odbc-driver"></a>No compatible de Visual FoxPro comandos y funciones (controlador ODBC de Visual FoxPro)
En la tabla siguiente se enumeran los comandos y funciones de FoxPro que no son compatibles con el controlador ODBC de Visual FoxPro pero que son compatibles con Microsoft® Visual FoxPro®.  
  
 Si la aplicación interactúa con datos cuyas reglas, desencadenadores, valores predeterminados o procedimientos almacenados llaman a estos comandos o funciones de Visual FoxPro, el controlador puede generar un error.  
  
## <a name="unsupported-visual-foxpro-commands-and-functions"></a>Comandos y funciones de Visual FoxPro no compatibles  
  
||||  
|-|-|-|  
|#DEFINE ... #UNDEF|#IF ... Directiva de preprocesador #ENDIF|#IFDEF &#124; #IFNDEF|  
|Directiva de preprocesador #INCLUDE|:: Operador de Resolución de Alcance|! Comando (consulte RUN &#124; ! Comando)|  
|? &#124; ?? Get-Help|??? Get-Help|• \\&#124; - Comando|  
|@ ... Comando BOX|@ ... Comando CLASS|@ ... Comando CLEAR|  
|@ ... EDITAR - Comando Editar cuadros|@ ... Comando FILL|@ ... Obtener|  
|@ ... Comando MENU|@ ... Comando PROMPT|@ ... Comando SAY|  
|@ ... Comando SCROLL|@ ... PARA Comandar||  
  
## <a name="a"></a>Un  
  
||||  
|-|-|-|  
|Aceptar Comando|Función ACLASS( )|ACTIVAR el comando MENU|  
|ACTIVAR comando POPUP|ACTIVAR EL Comando PANTALLA|Activar comando de ventana|  
|Método ActivateCell|ADD CLASS Command|Función ADIR( )|  
|Función AFONT( )|Función AINSTANCE( )|Variable de memoria del sistema _ALIGNMENT|  
|Función AMEMBERS( )|Función ANSITOOEM( )|Función APRINTERS( )|  
|AsELOBJ( ) Función|Comando ASSIST||  
  
## <a name="b"></a>B  
  
||||  
|-|-|-|  
|FUNción BAR( )|Función BARCOUNT( )|Función BARPROMPT( )|  
|_BEAUTIFY Variable de memoria del sistema|_BOX variable de memoria del sistema|Comando BROWSE|  
|_BROWSER Variable de memoria del sistema|CONSTRUIR APP Comando|COMANDO BUILD EXE|  
|COMANDO CONSTRUIR PROYECTO|_BUILDER variable de memoria del sistema||  
  
## <a name="c"></a>C  
  
||||  
|-|-|-|  
|Variable de memoria del sistema _CALCVALUE|_CLIPTEXT Variable de memoria del sistema|Variable de memoria del sistema _CONVERTER|  
|_CUROBJ Variable de memoria del sistema|Comando CALL|Comando CANCEL|  
|Función CAPSLOCK( )|Comando CD|Comando CAMBIO|  
|Comando CHDIR|Función CHRSAW( )|CLOSE MEMO Command|  
|FUNción CNTBAR( )|Función CNTPAD( )|Función COL( )|  
|Comando COMPILE|Comando COMPILE DATABASE|Comando COMPILE FORM|  
|COMPOBJ( ) Función|Objeto contenedor|Objeto de control|  
|COMANDO COPY FILE|Comando COPY MEMO|CREATE CLASS Command|  
|Comando CREATE CLASSLIB|CREATE COLOR SET Command|Comando CREATE|  
|COMANDO CREATE CONNECTION|COMANDO CREATE DATABASE|COMANDO CREATE FORM|  
|CREAR DESDE Comando|Comando CREATE LABEL|COMANDO CREATE MENU|  
|COMANDO CREATE PROJECT|COMANDO CREATE QUERY|COMANDO CREATE REPORT|  
|COMANDO CREATE SCREEN|Comando CREATE SQL VIEW|CREATE TRIGGER Command|  
|COMANDO CREATE VIEW|Función CREATEOBJECT( )|CurDIR( ) Función|  
  
## <a name="d"></a>D  
  
||||  
|-|-|-|  
|_DBLCLICK Variable de memoria del sistema|_DIARYDATE Variable de memoria del sistema|Función DBSETPROP( )|  
|Funciones DDE|DESACTIVAR EL comando MENU|DEACTIVATE POPUP Command|  
|DEACTIVATE WINDOW Command|DECLARE - Comando DLL|Comando DECLARE|  
|Comando DEFINE BAR|Comando DEFINE BOX|Comando DEFINE CLASS|  
|Comando DEFINE MENU|Comando DEFINE PAD|Comando DEFINE POPUP|  
|Comando DE VENTANA DE DEFINE|COMANDO DELETE CONNECTION|COMANDO DELETE DATABASE|  
|COMANDO DELETE FILE|COMANDO DELETE TRIGGER|COMANDO DELETE VIEW|  
|Comando DIR|Comando DIRECTORY|Comando DISPLAY|  
|COMANDO DISPLAY CONNECTIONS|COMANDO DISPLAY DATABASE|Comando DISPLAY DLLS|  
|Comando DISPLAY FILES|Comando DISPLAY MEMORY|Comando DISPLAY OBJECTS|  
|COMANDO PROCEDIMIENTOS DE PANTALLA|COMANDO DISPLAY STATUS|Comando DISPLAY STRUCTURE|  
|Comando DISPLAY TABLES|COMANDO VER VISTAS|COMANDO DO FORM|  
  
## <a name="e"></a>E  
  
||||  
|-|-|-|  
|Comando EDIT|Comando ERROR||  
|Comando ERASE|Comando EXTERNO|Comando EXPORT|  
|Comando EJECT|Comando EJECT PAGE||  
  
## <a name="f"></a>F  
  
||||  
|-|-|-|  
|_FOXDOC Variable de memoria del sistema|variable de memoria del sistema _FOXGRAPH|Función FEOF( )|  
|Función FCLOSE( )|Función FCREATE( )|Función FGETS( )|  
|Función FERROR( )|Función FFLUSH( )|Función FKLABEL( )|  
|Comando FILER|FIND Command|Función FOPEN( )|  
|Función FKMAX( )|Función FONTMETRIC( )|Función FSEEK( )|  
|Función FPUTS( )|Función FREAD( )||  
|Función FWRITE( )|Función FCHSIZE( )||  
  
## <a name="g"></a>G  
  
||||  
|-|-|-|  
|_GENGRAPH variable de memoria del sistema|_GENMENU Variable de memoria del sistema|_GENPD variable de memoria del sistema|  
|_GENSCRN Variable de memoria del sistema|_GENXTAB Variable de memoria del sistema|FUNción GETBAR( )|  
|FUNción GETCOLOR( )|Función GETDIR( )|Comando GETEXPR|  
|FUNción GETFILE( )|Función GETFONT( )|FUNción GETOBJECT( )|  
|Función GETPAD( )|Función GETPICT( )|FUNción GETPRINTER( )|  
  
## <a name="h"></a>H  
  
||||  
|-|-|-|  
|Comando AYUDA|OCULTAR comando MENU|Comando HIDE POPUP|  
|Comando HIDE WINDOW|HOME( ) Función||  
  
## <a name="i"></a>I  
  
||||  
|-|-|-|  
|Función IMESTATUS( )|COMANDO IMPORTAR|Comando INPUT|  
|INDEX ON Command|Función INKEY( )|Función ISCOLOR( )|  
|Comando INSERT|Función INSMODE( )||  
|Función ISMOUSE( )|_INDENT Variable de memoria del sistema||  
  
## <a name="j"></a>J  
  
||||  
|-|-|-|  
|Unirse al comando|||  
  
## <a name="k"></a>K  
  
||||  
|-|-|-|  
|Comando KEYBOARD|||  
  
## <a name="l"></a>L  
  
||||  
|-|-|-|  
|_LMARGIN Variable de memoria del sistema|Comando LABEL|Función LASTKEY( )|  
|Función LINENO( )|Comandos LIST|COMANDO LIST CONNECTIONS|  
|Comando LOAD|Función LOCFILE( )||  
  
## <a name="m"></a>M  
  
||||  
|-|-|-|  
|Función MCOL( )|Comando MD|MENU Para Comandar|  
|FUNción MEMORY( )|Comando MENU|Comando MKDIR|  
|MENU( ) Función|Función MESSAGEBOX( )|MODIFICAR El comando CONNECTION|  
|MODIFICAR Comando COLECTIVO|MODIFICAR COMANDO COMANDO|COMANDO MODIFICAR FORMULARIO|  
|MODIFICAR EL Comando DATABASE|MODIFICAR COMANDO DE ARCHIVO|MODIFICAR EL Comando MEMO|  
|MODIFICAR Comando GENERAL|Modificar el comando LABEL|MODIFICAR El Comando PROYECTO|  
|MODIFICAR EL Comando MENU|COMANDO MODIFICAR PROCEDIMIENTO|MODIFICAR EL Comando PANTALLA|  
|MODIFICAR Comando QUERY|Comando MODIFICAR INFORME|MODIFICAR Comando DE VENTANA|  
|MODIFICAR EL Comando ESTRUCTURA|MODIFICAR COMANDO VISTA|Comando MOVE WINDOW|  
|Comando MOUSE|Comando MOVE POPUP|Función MROW( )|  
|MrKBAR( ) Función|Función MRKPAD( )||  
|Función MWINDOW( )|Función MDOWN( )||  
  
## <a name="n"></a>N  
  
||||  
|-|-|-|  
|NumLOCK( ) Función|||  
  
## <a name="o"></a>O  
  
||||  
|-|-|-|  
|OBJNUM( ) Función|OBJTOCLIENT( ) Función|Comando ON BAR|  
|Función OEMTOANSI( )|ON APLABOUT Command|COMANDO DE MENÚ DE SALIDA|  
|COMANDO ON ESCAPE|ON EXIT BAR Command|ON KEY - Comando|  
|COMANDO ON EXIT PAD|Comando POPUP ON EXIT|Comando ON PAD|  
|COMANDO ON KEY LABEL|Comando ON MACHELP|ON SELECTION BAR Command|  
|Comando ON PAGE|COMANDO ON READERROR|Comando ON SELECTION POPUP|  
|COMANDO ON SELECTION MENU|COMANDO ON SELECTION PAD||  
|Comando ON SHUTDOWN|OBJVAR( ) Función||  
  
## <a name="p"></a>P  
  
||||  
|-|-|-|  
|_PADVANCE Variable de memoria del sistema|_PAGENO Variable de memoria del sistema|_PBPAGE Variable de memoria del sistema|  
|_PCOLNO Variable de memoria del sistema|_PCOPIES Variable de memoria del sistema|Variable de memoria del sistema _PDRIVER|  
|_PDSETUP variable de memoria del sistema|Variable de memoria del sistema _PECODE|Variable de memoria del sistema _PEJECT|  
|_PEPAGE Variable de memoria del sistema|_PLENGTH Variable de memoria del sistema|_PLINENO Variable de memoria del sistema|  
|_PLOFFSET Variable de memoria del sistema|_PPITCH Variable de memoria del sistema|_PQUALITY Variable de memoria del sistema|  
|_PRETEXT Variable de memoria del sistema|_PSCODE Variable de memoria del sistema|_PSPACING variable de memoria del sistema|  
|_PWAIT Variable de memoria del sistema|Comando PACK DATABASE|Función PAD( )|  
|Función PCOL( )|PemSTATUS( ) Función|Comando PLAY MACRO|  
|Comando POP KEY|Comando POP MENU|Comando POP POPUP|  
|Función POPUP( )|Printjob... Comando ENDPRINTJOB|Función PRINTSTATUS( )|  
|Función PRMBAR( )|Función PRMPAD( )|Función PROMPT( )|  
|Función PROW( )|Función PRTINFO( )|Comando PUSH KEY|  
|Comando PUSH MENU|Comando PUSH POPUP|Función PUTFILE( )|  
  
## <a name="q"></a>Q  
  
||||  
|-|-|-|  
|Comando QUIT|||  
  
## <a name="r"></a>R  
  
||||  
|-|-|-|  
|_RMARGIN variable de memoria del sistema|Comando RD|Función READKEY( )|  
|Comando READ|LEER EL Comando MENU|COMANDO RELEASE BAR|  
|FUNción REFRESH()|Comando REINDEX|Comando RELEASE LIBRARY|  
|Comando RELEASE CLASSLIB|Comando RELEASE|Comando RELEASE PAD|  
|Comando RELEASE MENUS|Comando RELEASE MODULE|COMANDO RELEASE WINDOWS|  
|Comando RELEASE POPUPS|COMANDO RELEASE PROCEDURE|Comando RENAME|  
|REMOVE CLASS Command|Comando RENAME CLASS|Comando RENOMBRAR VISTA|  
|Comando RENAME CONNECTION|Comando RENAME TABLE|RESTORE FROM Command|  
|Comando INFORME|ReQUERY( ) Función|Comando RESTORE WINDOW|  
|Comando RESTORE MACROS|Comando RESTORE SCREEN|Función RGBSCHEME( )|  
|Comando RESUME|Función RGB( )|RUN &#124; ! Get-Help|  
|Comando RMDIR|Función ROW( )||  
|Comando RUNSCRIPT|Función RDLEVEL( )||  
  
## <a name="s"></a>S  
  
||||  
|-|-|-|  
|Comando SAVE MACROS|Comando SAVE SCREEN|GUARDAR PARA Comandar|  
|Comando GUARDAR VENTANAS|SCHEME( ) Función|Función SCOLS( )|  
|Comando SCROLL|_SCREEN Variable de memoria del sistema|Comando SET|  
|SET ALTERNATE Command|Comando de ANSI SET|Comando SET APLABOUT|  
|Comando SET AUTOSAVE|Comando SET BELL|Comando SET BLINK|  
|Comando SET BORDER|Comando SET BRSTATUS|Comando SET CLASSLIB|  
|Comando SET CLEAR|Comando SET CLOCK|SET COLOR OF Command|  
|SET COLOR OF SCHEME Command|Comando SET COLOR SET|SET COLOR TO Command|  
|Comando COMPATIBLE SET|COMANDO SET CONFIRM|Comando SET CONSOLE|  
|SET CPCOMPILE|SET CPDIALOG|Comando SET CURRENCY|  
|Comando SET CURSOR|Comando SET DATASESSION|Comando SET DEBUG|  
|Comando SET DECIMALS|Comando SET DELIMITERS|Comando SET DEVELOPMENT|  
|Comando SET DEVICE|Comando SET DISPLAY|SET DOHISTORY Command|  
|Comando SET ECHO|Comando SET ESCAPE|Comando SET FORMAT|  
|Comando SET FUNCTION|Comando SET HEADINGS|SET HELP Command|  
|SET HELPFILTER Command|Comando SET INTENSITY|Comando SET KEY|  
|Comando SET KEYCOMP|Comando SET LOGERRORS|Comando SET MACDESKTOP|  
|Comando SET MACHELP|Comando SET MACKEY|Comando SET MARGIN|  
|SET MARK OF Command|ESTABLECER MARCA AL Comando|Comando SET MEMOWIDTH|  
|Comando SET MESSAGE|Comando SET MOUSE|Comando SET ODOMETER|  
|Comando SET OLEOBJECT|Comando SET PALETTE|Comando SET PDSETUP|  
|Comando SET POINT|COMANDO SET PRINTER|COMANDO SET READBORDER|  
|Comando SET REFRESH|Comando SET RESOURCE|Comando SET SAFETY|  
|Comando SET SCOREBOARD|Comando SET SECONDS|Comando SET SEPARATOR|  
|Comando SET SHADOWS|SET SKIP OF Command|Comando SET SPACE|  
|Comando SET STATUS|COMANDO SET STATUS BAR|Comando SET STEP|  
|Comando SET STICKY|Comando SET SYSFORMATS|Comando SET SYSMENU|  
|Comando SET TALK|Comando SET TEXTMERGE|Comando SET TEXTMERGE DELIMITERS|  
|Comando SET TOPIC|Comando SET TOPIC ID|Comando SET TRBETWEEN|  
|Comando SET TYPEAHEAD|Comando SET VIEW|SET WINDOW OF MEMO Command|  
|Comando SET XCMDFILE|_SHELL Variable de memoria del sistema|SHOW GET Command|  
|Comando SHOW GETS|Comando SHOW MENU|Comando SHOW OBJECT|  
|Comando SHOW POPUP|Comando SHOW WINDOW|Comando POPUP DE TALLA|  
|Comando DE VENTANA DE TALLA|Función SKPBAR( )|Función SKPPAD( )|  
|Función SOUNDEX( )|_SPELLCHK Variable de memoria del sistema|Funciones SQL|  
|Función SROWS( )|_STARTUP Variable de memoria del sistema|COMANDO SUSPEND|  
|Funciones SYS() excepto SYS(2011)|Función SYSMETRIC( )||  
  
## <a name="t"></a>T  
  
||||  
|-|-|-|  
|_TABS Variable de memoria del sistema|Texto... Comando ENDTEXT|FUNción TXTWIDTH( )|  
|FUNción TRANSFORM( )|_TRANSPORT Variable de memoria del sistema||  
|COMANDO TIPO|_THROTTLE Variable de memoria del sistema||  
  
## <a name="u"></a>U  
  
||||  
|-|-|-|  
|Función UPDATED( )|Comando USE||  
  
## <a name="v"></a>V  
  
||||  
|-|-|-|  
|COMANDO VALIDATE DATABASE|Función VARREAD( )|FUNción VERSION( )|  
  
## <a name="w"></a>W  
  
||||  
|-|-|-|  
|_WINDOWS Variable de memoria del sistema|Variable de memoria del sistema _WIZARD|Función WCHILD( )|  
|Comando WAIT|Función WBORDER( )|Función WFONT( )|  
|Función WCOLS( )|Función WEXIST( )|Función WLROW( )|  
|Con... ENDWITH Command|WLAST( ) Función|FUNción WONTOP( )|  
|WMAXIMUM( ) Función|Funcionamiento WLCOL( )|Función WREAD( )|  
|Función WOUTPUT( )|WMINIMUM( ) Función|WVISIBLE( ) Función|  
|Función WPARENT( )|Función WTITLE( )||  
|WROWS( ) Función|_WRAP Variable de memoria del sistema||  
  
## <a name="z"></a>Z  
  
||||  
|-|-|-|  
|Comando ZOOM WINDOW|||
