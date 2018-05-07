---
title: No admite funciones y comandos de Visual FoxPro | Documentos de Microsoft
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
- FoxPro ODBC driver [ODBC], commands and functions
- functions [ODBC], Visual FoxPro
- Visual FoxPro ODBC driver [ODBC], commands and functions
- Visual FoxPro commands and functions
- FoxPro ODBC driver
ms.assetid: afdb6b7e-738d-42ca-8053-67ae50873ca6
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: cfef52f471f9b87e7f6560b76e191aca1ba26172
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="unsupported-visual-foxpro-commands-and-functions-visual-foxpro-odbc-driver"></a>No compatible de Visual FoxPro comandos y funciones (controlador ODBC de Visual FoxPro)
En la tabla siguiente se enumera los comandos de FoxPro y funciones que no son compatibles con el controlador ODBC de Visual FoxPro pero son compatibles con Microsoft® Visual FoxPro.  
  
 Si su aplicación interactúa con los datos cuyas reglas, desencadenadores, valores predeterminados, o llamar a procedimientos almacenados de estos comandos de Visual FoxPro o funciones, el controlador puede generar un error.  
  
## <a name="unsupported-visual-foxpro-commands-and-functions"></a>Funciones y comandos de no compatible de Visual FoxPro  
  
||||  
|-|-|-|  
|#... DEFINEN #UNDEF|#IF... #ENDIF directiva de preprocesador|#IFDEF &AMP;#124; #IFNDEF|  
|#INCLUDE preprocesador (directiva)|:: Operador de resolución de ámbito|! Comando (vea ejecutar &#124; ! Comando)|  
|? &#124; ?? Comando|??? Comando|\ &#124; \\\ Comando|  
|@ ... CUADRO comando|@ ... Comando de clase|@ ... Borrar, comando|  
|@ ... Editar - Editar comando cuadros|@ ... RELLENAR, comando|@ ... GET|  
|@ ... Comando de menú|@ ... Símbolo|@ ... EJEMPLO de comando|  
|@ ... Comando de desplazamiento|@ ... AL comando||  
  
## <a name="a"></a>A  
  
||||  
|-|-|-|  
|Acepte el comando|Función ACLASS)|ACTIVAR el comando de menú|  
|ACTIVAR el comando de menú emergente|Activar comandos de pantalla|ACTIVAR la ventana de comando|  
|ActivateCell (método)|Agregar clase (comando)|Función ADIR)|  
|Función AFONT)|Función AINSTANCE)|Variable de memoria del sistema _ALIGNMENT|  
|Función AMEMBERS)|Función ANSITOOEM)|Función APRINTERS)|  
|Función ASELOBJ)|Ayudar a comandos||  
  
## <a name="b"></a>B  
  
||||  
|-|-|-|  
|BARRA () (función)|Función BARCOUNT)|Función BARPROMPT)|  
|Variable de memoria del sistema _BEAUTIFY|Variable de memoria del sistema _BOX|Busque el comando|  
|Variable de memoria del sistema _BROWSER|COMPILAR aplicaciones (comando)|COMPILAR archivo EXE (comando)|  
|COMPILAR el proyecto (comando)|Variable de memoria del sistema _BUILDER||  
  
## <a name="c"></a>C  
  
||||  
|-|-|-|  
|Variable de memoria del sistema _CALCVALUE|Variable de memoria del sistema _CLIPTEXT|Variable de memoria del sistema _CONVERTER|  
|Variable de memoria del sistema _CUROBJ|LLAMADAS (comando)|CANCEL, comando|  
|CAPSLOCK (función))|Comando CD|Comando de cambio|  
|Comando CHDIR|Función CHRSAW)|Comando de cierre de memorando|  
|Función CNTBAR)|Función CNTPAD)|Función de COL)|  
|COMPILE el comando|COMPILA el comando de base de datos|COMPILE los comandos de formulario|  
|Función COMPOBJ)|Objeto de contenedor|Objeto de control|  
|Copie el archivo (comando)|Copie el comando de memorando|CREAR un comando (clase)|  
|CREAR un comando CLASSLIB|Crear conjunto de COLOR, comando|CREATE, comando|  
|CREAR el comando de conexión|CREAR comandos de base de datos|CREAR comandos de formulario|  
|CREAR a partir de comando|CREAR comandos de etiqueta|CREAR el comando de menú|  
|Crear proyecto (comando)|CREAR el comando de consulta|CREAR informes, comando|  
|CREAR comandos de pantalla|CREAR comandos de vista SQL|CREAR comandos de DESENCADENADOR|  
|CREAR comandos de vista|CREATEOBJECT (función))|DIRACT (función))|  
  
## <a name="d"></a>D  
  
||||  
|-|-|-|  
|Variable de memoria del sistema _DBLCLICK|Variable de memoria del sistema _DIARYDATE|Función DBSETPROP)|  
|Funciones DDE|DESACTIVAR el comando de menú|DESACTIVAR el comando de menú emergente|  
|DESACTIVAR la ventana de comando|DECLARAR - DLL comando|DECLARE el comando|  
|DEFINIR la barra de comandos|Defina el cuadro comando|DEFINIR el comando de clase|  
|DEFINIR el comando de menú|DEFINIR el comando del panel|DEFINIR el comando de menú emergente|  
|Definir ventana (comando)|ELIMINAR el comando de conexión|Eliminar base de datos, comando|  
|Eliminar archivo (comando)|Comando de DESENCADENADOR DELETE|Eliminar vista, comando|  
|Comando DIR|Comando de directorio|Mostrar comando|  
|Comandos de conexiones de presentación|Comando de base de datos de pantalla|Mostrar archivos DLL comando|  
|Mostrar archivos (comando)|Mostrar memoria (comando)|Comando de objetos de visualización|  
|Comando de procedimientos de visualización|Comando de estado de visualización|Comando de la estructura de presentación|  
|Comando de tablas de presentación|Comando de vistas de presentación|Comandos de formulario|  
  
## <a name="e"></a>E  
  
||||  
|-|-|-|  
|Editar comandos|Comando ERROR||  
|ERASE, comando|Comando externo|Exportar (comando)|  
|Comando EXPULSAR|EXPULSAR el comando de página||  
  
## <a name="f"></a>F  
  
||||  
|-|-|-|  
|Variable de memoria del sistema _FOXDOC|Variable de memoria del sistema _FOXGRAPH|FEOF () (función)|  
|FCLOSE () (función)|Función FCREATE)|FGETS () (función)|  
|FERROR () (función)|FFLUSH (función))|Función FKLABEL)|  
|Comando de filtro|Buscar (comando)|FOPEN () (función)|  
|Función FKMAX)|Función FONTMETRIC)|FSEEK () (función)|  
|FPUTS (función))|FREAD () (función)||  
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
|Comandos de la Ayuda|OCULTAR el comando de menú|OCULTAR el comando de menú emergente|  
|OCULTAR la ventana de comando|Función principal)||  
  
## <a name="i"></a>I  
  
||||  
|-|-|-|  
|IMESTATUS (función))|Comando de importación|Comandos de entrada|  
|ÍNDICE de comandos|Función INKEY)|Función ISCOLOR)|  
|INSERT, comando|Función INSMODE)||  
|Función ISMOUSE)|Variable de memoria del sistema _INDENT||  
  
## <a name="j"></a>J  
  
||||  
|-|-|-|  
|UNIR, comando|||  
  
## <a name="k"></a>K  
  
||||  
|-|-|-|  
|Comando de teclado|||  
  
## <a name="l"></a>L  
  
||||  
|-|-|-|  
|Variable de memoria del sistema _LMARGIN|Comando de etiqueta|Función LASTKEY)|  
|Función LINENO)|LISTA de comandos|MOSTRAR las conexiones (comando)|  
|Comando de carga|Función de archivo LOCFILE)||  
  
## <a name="m"></a>M  
  
||||  
|-|-|-|  
|Función MCOL)|Comando MD|MENÚ de comandos|  
|Función de memoria)|Comando de menú|Comando MKDIR|  
|Función de menú)|Función de cuadro de mensajes)|MODIFICAR el comando de conexión|  
|MODIFICAR el comando de clase|MODIFICAR comandos (comando)|MODIFICAR los comandos de formulario|  
|MODIFICAR el comando de base de datos|MODIFICAR el archivo (comando)|MODIFICAR memorando comando|  
|MODIFICAR comando GENERAL|MODIFICAR el comando de etiqueta|MODIFICAR el proyecto (comando)|  
|MODIFICAR el comando de menú|MODIFICAR PROCEDURE (comando)|MODIFICAR los comandos de pantalla|  
|MODIFICAR el comando de consulta|MODIFICAR los comandos de informe|MODIFICAR la ventana (comando)|  
|MODIFICAR el comando de estructura|MODIFICAR el comando de vista|MOVER la ventana de comando|  
|Comando de mouse (ratón)|MOVER el comando de menú emergente|Función MROW)|  
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
|Función OEMTOANSI)|EN el comando APLABOUT|ON EXIT, comando de menú|  
|EN el comando ESCAPE|EN la barra de EXIT, comando|CLAVE = comando|  
|Comando del panel de salida ON|ON EXIT, comando de menú emergente|Comando del panel ON|  
|EN el comando de etiqueta de la clave|EN el comando MACHELP|EN selección de barra de comandos|  
|EN la página, comando|EN el comando READERROR|EN el comando de menú emergente de selección|  
|EN el comando de menú de selección|EN el comando del panel de selección||  
|EN el comando SHUTDOWN|Función OBJVAR)||  
  
## <a name="p"></a>P  
  
||||  
|-|-|-|  
|Variable de memoria del sistema _PADVANCE|Variable de memoria del sistema _PAGENO|Variable de memoria del sistema _PBPAGE|  
|Variable de memoria del sistema _PCOLNO|Variable de memoria del sistema _PCOPIES|Variable de memoria del sistema _PDRIVER|  
|Variable de memoria del sistema _PDSETUP|Variable de memoria del sistema _PECODE|Variable de memoria del sistema _PEJECT|  
|Variable de memoria del sistema _PEPAGE|Variable de memoria del sistema _PLENGTH|Variable de memoria del sistema _PLINENO|  
|Variable de memoria del sistema _PLOFFSET|Variable de memoria del sistema _PPITCH|Variable de memoria del sistema _PQUALITY|  
|Variable de memoria del sistema _PRETEXT|Variable de memoria del sistema _PSCODE|Variable de memoria del sistema _PSPACING|  
|Variable de memoria del sistema _PWAIT|Comando de base de datos de paquete|Función de controlador)|  
|Función PCOL)|Función PEMSTATUS)|Comando MACRO de reproducir|  
|Comando de teclas ventana emergente|Comando de menú emergente|Comando de menú emergente de confirmación|  
|Función de ventana emergente)|PRINTJOB... Comando ENDPRINTJOB|Función PRINTSTATUS)|  
|Función PRMBAR)|Función PRMPAD)|Función de símbolo del sistema)|  
|Función PROW)|Función PRTINFO)|Comando de teclas de INSERCIÓN|  
|Comando de menú de INSERCIÓN|Comando de menú emergente de INSERCIÓN|Función PUTFILE)|  
  
## <a name="q"></a>Q  
  
||||  
|-|-|-|  
|Salga de comando|||  
  
## <a name="r"></a>L  
  
||||  
|-|-|-|  
|Variable de memoria del sistema _RMARGIN|Comando de escritorio remoto|Función READKEY)|  
|LEER el comando|LEER el comando de menú|Comando de barra de versión|  
|Función Actualizar()|REINDIZACIÓN de comando|Comando de la biblioteca de versión|  
|VERSIÓN CLASSLIB comando|Comando de versión|Comando del panel de versión|  
|Comandos de menús de versión|Comandos del módulo de versión|Comandos de WINDOWS de versión|  
|Comando de elementos emergentes de versión|VERSIÓN PROCEDURE (comando)|Cambiar el nombre de comando|  
|QUITAR el comando de clase|Cambiar el nombre de comando de clase|Cambiar el nombre de comando de vista|  
|Cambiar el nombre de comando de conexión|Cambiar el nombre de comando de tabla|RESTAURAR a partir de comando|  
|Comando de informe|REQUERY () (función)|RESTAURAR la ventana de comando|  
|RESTAURAR comandos de MACROS|RESTAURAR comandos de pantalla|Función RGBSCHEME)|  
|Comando RESUME|RGB (función))|EJECUTAR &AMP;#124; ! Comando|  
|Comando RMDIR|Función de fila)||  
|Comando RUNSCRIPT|Función RDLEVEL)||  
  
## <a name="s"></a>S  
  
||||  
|-|-|-|  
|Guardar MACROS, comando|Guardar comandos de pantalla|Guardar en el comando|  
|Guardar comandos de WINDOWS|Función de esquema)|Función SCOLS)|  
|Comando de desplazamiento|Variable de memoria del sistema _SCREEN|Comando Set.|  
|CONJUNTO de comandos alternativo|Comando de ANSI SET.|Comando APLABOUT|  
|Comando de AUTOGUARDADO Set.|Comando de CAMPANA Set.|Comando de INTERMITENCIA Set.|  
|Comando de borde de Set.|Comando BRSTATUS Set.|Comando CLASSLIB|  
|Comando Borrar conjunto|Comando de RELOJ de Set.|ESTABLECER el COLOR de comando|  
|ESTABLECER el COLOR del comando de combinación|Comando de conjunto de COLOR de Set.|ESTABLECER el COLOR a controlar|  
|Comando COMPATIBLE|Comando de confirmar Set.|CONJUNTO de comandos de consola|  
|CONJUNTO CPCOMPILE|CONJUNTO CPDIALOG|Comando de moneda Set.|  
|CURSOR de conjunto (comando)|Comando DATASESSION|CONJUNTO de comandos de depuración|  
|Comando de decimales Set.|Comando de conjunto de DELIMITADORES|CONJUNTO de comandos de desarrollo|  
|Comando de dispositivo de Set.|Mostrar comando|Comando DOHISTORY|  
|Comando de eco de Set.|Comando ESCAPE de Set.|Comandos de formato de conjunto|  
|Comando de función de conjunto|Comando de conjunto de ENCABEZADOS|Comando de Ayuda de SET|  
|Comando HELPFILTER|Comando de intensidad de Set.|Comando de teclas de conjunto|  
|Comando KEYCOMP|Comando LOGERRORS|Comando MACDESKTOP|  
|Comando MACHELP|Comando MACKEY|Comando de margen de Set.|  
|MARCAR el conjunto de comandos|ESTABLECER la marca de comando|Comando del ancho del campo Memo Set.|  
|CONJUNTO de comandos de mensaje|Comando del MOUSE|Comando de ODÓMETRO Set.|  
|Comando OLEOBJECT Set.|Comando de la PALETA de Set.|Comando PDSETUP|  
|PUNTO de conjunto de comandos|CONJUNTO de comandos de impresora|Comando READBORDER|  
|CONJUNTO de comandos de actualización|CONJUNTO de comandos de recursos|CONJUNTO de comandos de seguridad|  
|Comando del panel de resultados|Comando de segundos de Set.|Comando de separador de Set.|  
|Comando de SOMBRAS Set.|OMITIR del conjunto de comandos|Comando de espacio de Set.|  
|Comando de estado del conjunto|ESTABLECE el comando de barra de estado|Comando del paso de conjunto|  
|Comando rápidas de Set.|Comando SYSFORMATS|Comando SYSMENU|  
|CHARLA de comando|CONJUNTO de comandos de la combinación de texto|Comando de DELIMITADORES de la combinación de texto de Set.|  
|CONJUNTO de comandos de tema|Comando de Id. de conjunto de tema|Comando TRBETWEEN|  
|Comando de escritura anticipada Set.|Comando de la vista de conjunto|ESTABLECER la ventana de comandos de memorando|  
|Comando XCMDFILE|Variable de memoria del sistema _SHELL|Mostrar GET (comando)|  
|Mostrar OBTIENE (comando)|Mostrar comando de menú|Mostrar objeto (comando)|  
|Mostrar menú emergente (comando)|Mostrar ventana (comando)|Comando de menú emergente de tamaño|  
|VENTANA de tamaño (comando)|Función SKPBAR)|Función SKPPAD)|  
|Función SOUNDEX)|Variable de memoria del sistema _SPELLCHK|Funciones SQL|  
|Función SROWS)|Variable de memoria del sistema _STARTUP|Comando de suspensión|  
|Funciones sys() excepto SYS(2011)|Función SYSMETRIC)||  
  
## <a name="t"></a>T  
  
||||  
|-|-|-|  
|Variable de memoria del sistema _TABS|TEXTO... Comando ENDTEXT|Función TXTWIDTH)|  
|TRANSFORM () (función)|Variable de memoria del sistema _TRANSPORT||  
|Comando de tipo|Variable de memoria del sistema _THROTTLE||  
  
## <a name="u"></a>U  
  
||||  
|-|-|-|  
|Función actualizada)|USE el comando||  
  
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
|VENTANA de ZOOM (comando)|||
