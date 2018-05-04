---
title: Mensajes de Error nativo de Visual FoxPro ODBC Driver | Documentos de Microsoft
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: odbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- error messages [ODBC], Visual FoxPro ODBC driver
- Visual FoxPro ODBC driver [ODBC], error messages
- FoxPro ODBC driver [ODBC], error messages
ms.assetid: 7b2622e8-ccee-4853-9171-4fb10de0461d
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 699deaf882d276e4670ee7cf124a1ad12273c397
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="visual-foxpro-odbc-driver-native-error-messages"></a>Mensajes de Error nativo de controlador ODBC de Visual FoxPro
Las tablas siguientes muestran mensajes de error nativos para el controlador ODBC de Visual FoxPro.  
  
## <a name="001"></a>001  
  
|||  
|-|-|  
|1|Característica no está disponible.|  
|2|Error en la operación de entrada/salida.|  
|3|No se encuentra un identificador libre.|  
|5|Uso de un controlador sin asignar.|  
|99|Se cancelará el procedimiento.|  
  
## <a name="100"></a>100  
  
|||  
|-|-|  
|100|Hay demasiados archivos abiertos.|  
|101|No se puede abrir el archivo.|  
|102|No se puede crear el archivo.|  
|105|Error al escribir en el archivo.|  
|107|Longitud de clave no válida.|  
|109|Registro está fuera del intervalo.|  
|110|Registro no está en el índice.|  
|111|Descriptor de archivo no válido.|  
|113|Archivo no está abierto.|  
|114|No hay suficiente espacio en disco para *valor*.|  
|115|Operación no válida para el cursor.|  
|118|Archivo de índice no coincide con la tabla.|  
|119|No hay ninguna tabla está abierta.|  
|120|El archivo no existe.|  
|121|Archivo ya existe.|  
|122|Tabla no tiene ningún orden de índice.|  
|123|No es una tabla.|  
|125|Expresión de índice supera la longitud máxima.|  
|127|Debe usar una expresión lógica con FOR o WHILE (cláusula).|  
|128|No es una expresión numérica.|  
|129|No se encuentra la variable.|  
|132|Archivo está en uso.|  
|133|Índice no coincide con la tabla. Elimine el archivo de índice y volver a crear el índice.|  
|135|Final de archivo encontrado.|  
|136|Principio del archivo encontrado.|  
|137|No se encontró un alias.|  
|139|Debe utilizar una expresión lógica con el filtro.|  
|142|Relación cíclica.|  
|143|No se encontraron campos para copiar.|  
|144|Debe emitirse el comando LOCATE antes del comando de continuar.|  
|145|Debe ser un carácter o un campo de clave numérico.|  
|146|No se puede escribir en un archivo de solo lectura.|  
|147|Tabla de destino ya está ocupado en una relación.|  
|148|Expresión ha sido volver a escribir mientras se está ejecutando el filtro.|  
|149|No hay suficiente memoria para el búfer.|  
|150|No hay suficiente memoria para asignación de archivo.|  
|155|Llamada de BUFFDIRTY no es válida.|  
|156|Nombres de campo duplicados.|  
|158|No hay campos para el proceso.|  
|159|Desbordamiento numérico. Se perdieron datos.|  
|162|Procedimiento '*valor*' no se encuentra.|  
|165|*valor* no está relacionado con el área de trabajo actual.|  
|170|Variable '*valor*' no se encuentra.|  
|171|No se puede abrir el archivo *valor*.|  
|173|Archivo '*valor*' no existe.|  
|174|'*valor*' no es una variable de memoria.|  
|175|'*valor*' no es una variable de archivo.|  
|176|'*valor*' no es una matriz.|  
|177|'Alias*valor*' no se encuentra.|  
|180|No se colocó el archivo en memoria mediante el comando de carga.|  
|182|No hay memoria suficiente para completar esta operación.|  
  
## <a name="200"></a>200  
  
|||  
|-|-|  
|200|Error de sintaxis.|  
|201|Hay demasiados nombres utilizados.|  
|202|Programa es demasiado grande.|  
|203|Hay demasiadas variables de memoria.|  
|205|Error de anidamiento.|  
|206|Definición de macro recursiva.|  
|209|Línea es demasiado larga.|  
|210|Permite el anidamiento de DO que se excedió el nivel.|  
|211|IF &#124; ELSE &#124; instrucción ENDIF es que faltan.|  
|212|La estructura de anidamiento es demasiado profunda.|  
|213|Hay una palabra clave que falta en la para... ENDFOR o DO CASE... Estructura del comando ENDCASE.|  
|219|El comando contiene frase o palabra clave no reconocida.|  
|221|Comando falta una cláusula necesaria.|  
|222|Verbo del comando no reconocido.|  
|224|Referencia de subíndice no válida.|  
|227|Expresión que falta.|  
|228|Número de la tabla no es válido.|  
|229|Argumentos insuficientes.|  
|230|Hay demasiados argumentos.|  
|233|No se permite la instrucción en modo interactivo.|  
|234|Subíndice está fuera del intervalo definido.|  
|236|Suspenda el programa antes de usar RESUME.|  
|238|No se encuentra ninguna declaración de parámetro.|  
|239|Debe especificar parámetros adicionales.|  
|240|No es una expresión de caracteres.|  
|250|Hay demasiados comandos de procedimiento están en vigor.|  
|252|El código compilado para esta línea es demasiado largo.|  
|257|Cadena de clave es demasiado larga.|  
|291|La expresión usada con ASIN() está fuera del intervalo.|  
|292|No se puede usar 0 o un valor negativo como argumento para LOG10 ().|  
|293|La expresión usada con ACOS() está fuera del intervalo.|  
|294|FOXUSER. Archivo DBF no es válido.|  
|295|Nombre de archivo o ruta de acceso no válido.|  
|296|Error al leer el recurso.|  
|297|Comando solo se permite en el modo interactivo.|  
  
## <a name="300"></a>300  
  
|||  
|-|-|  
|301|Error de coincidencia de tipo de operador u operando.|  
|302|Error de coincidencia de tipo de datos.|  
|305|Expresión se evaluó como un valor no válido.|  
|307|No se puede dividir por 0.|  
|308|Espacio de pila insuficiente.|  
|337|No se pueden anidar el comando PRINTJOB.|  
  
## <a name="400"></a>400  
  
|||  
|-|-|  
|406|Impresora no está preparada.|  
|407|Argumento no válido que se utiliza con la función de conjunto.|  
|410|No se puede crear archivos de trabajo temporales.|  
|423|Error al crear el objeto OLE.|  
|424|Error al copiar el objeto OLE en el Portapapeles.|  
|462|*valor* error de coherencia interna.|  
|465|Error de coherencia interna paso a través de SQL.|  
|466|Identificador de conexión no es válido.|  
|467|Propiedad no es válida para los cursores locales.|  
|468|Propiedad no es válida para los cursores de la tabla.|  
|469|Valor de propiedad está fuera de los límites.|  
|470|Nombre de propiedad incorrecto.|  
|471|Formato de columna es incorrecto.|  
|473|Propiedad de nivel de entorno no es válida.|  
|474|Llamada no válida mientras se ejecutaba una secuencia SQLEXEC().|  
|479|Nombre de la columna de actualización no válida \\ *valor*\\.|  
|489|No se puede usar campos generales en la condición WHERE de una instrucción update. Cambie la propiedad WhereType de la vista.|  
|491|No actualizar las tablas se especifican. Use la propiedad de las tablas del cursor.|  
|492|Ninguna columna de clave se especifica para la tabla de actualización \\ *valor*\\. Use la propiedad KeyFieldList del cursor.|  
|493|Parámetro SQL no está.|  
|494|Ha cambiado la definición de la vista.|  
|495|Advertencia: La clave definida por la propiedad KeyField para la tabla *valor* no es único.|  
|498|Instrucción SELECT de SQL no es válido.|  
|499|Parámetro SQL *valor* no es válido.|  
  
## <a name="500"></a>500  
  
|||  
|-|-|  
|502|No se puede escribir en el registro porque está en uso.|  
|503|No se puede bloquear el archivo.|  
|508|Error al inicializar OLE.|  
|520|Ninguna base de datos está abierta o establecida como la base de datos actual.|  
|522|Error de coherencia interna de conectividad.|  
|523|Ejecución cancelada por el usuario.|  
|525|Función no se admite en las tablas remotas.|  
|526|Error de conectividad: *valor.*|  
|527|No se puede cargar la biblioteca ODBC, ODBC32. DLL.|  
|528|ODBC falta de punto de entrada, *valor*.|  
|530|Búsqueda cancelada; se cerró una tabla remota.|  
|532|No se admite la conversión de tipos.|  
|533|Esta propiedad es de solo lectura.|  
|536|Función no se admite en las tablas nativas.|  
|538|Se está ejecutando un procedimiento almacenado.|  
|540|Número de sesión no es válido.|  
|541|Conexión *valor* está ocupado.|  
|542|Campos de la tabla base han cambiado y ya no coinciden con los campos de la vista. No se puede establecer propiedades de campo de vista.|  
|543|Requerido por la propiedad de tipo de datos de campo de conversión de tipos '*valor*' no es válido.|  
|544|Propiedad DataType para el campo '*valor*' no es válido.|  
|545|Búfer de la tabla de alias \\ *valor*\ contiene cambios sin confirmar.|  
|546|No se puede cerrar la tabla durante la ejecución de la expresión de tabla enlazado.|  
|547|No se puede insertar una fila vacía desde una vista en sus tablas base.|  
|548|Tabla *valor* tiene uno o más índices no estructurales abierto. Por favor, cierre y vuelva a intentar Begin Transaction.|  
|549|Sesión de datos #*valor* no se puede liberar con transacciones abiertas.|  
|550|. Error de coherencia interna de DBC.|  
|557|La base de datos debe estar abierto exclusivamente.|  
|559|No se encuentra la propiedad.|  
|560|Valor de propiedad no es válido.|  
|561|Base de datos no es válido. Valide.|  
|562|No se puede encontrar el objeto *valor* en la base de datos.|  
|563|No se puede encontrar la vista *valor* en la base de datos actual.|  
|566|No se puede emitir el comando PACK en una base de datos mientras sus tablas están en uso.|  
|567|Propiedad de clave principal no es válido; Valide la base de datos.|  
|570|Base de datos es de solo lectura.|  
|571|El nombre *valor* ya está en uso por otra cosa|  
|575|Nombre de objeto no es válido.|  
|577|Tabla *valor* se hace referencia en una relación.|  
|578|Nombre de la tabla de base de datos no válido.|  
|579|No se puede emitir comandos en una tabla con los cursores de tabla de modo de almacenamiento en búfer.|  
|580|Característica no se admite para no. Tablas DBC.|  
|581|Campo *valor* no aceptar valores null *valor*.|  
|583|Se infringe la regla de validación de registro.|  
|585|Conflicto de actualización. Use TABLEUPDATE() con el parámetro lForce para confirmar la actualización o TABLEREVERT() para revertir la actualización.|  
|586|Función requiere la fila o tabla de modo de almacenamiento en búfer.|  
|587|Ilegal anidar OLDVAL() o CURVAL().|  
|589|Tabla o fila de almacenamiento en búfer requiere que establezca MULTILOCKS tenga el valor está establecido en ON.|  
|590|Error del comando BEGIN TRANSACTION. Nivel de anidamiento es demasiado profundo.|  
|591|No se puede emitir el comando END TRANSACTION sin un comando BEGIN TRANSACTION correspondiente.|  
|592|No se puede emitir el comando ROLLBACK sin un comando BEGIN TRANSACTION correspondiente.|  
|593|No se puede emitir el comando dentro de una transacción.|  
|594|No es posible un archivo de bloqueo en una transacción después de bloquear los registros primarios.|  
|596|No está habilitado el almacenamiento en búfer en la tabla.|  
|597|Las vistas requieren DB_BUFOPTROW o DB_BUFOPTTABLE.|  
|598|Regla y el código desencadenador debe equilibrar el uso de transacciones.|  
|599|Sesión de datos #*valor* se forzó la reversión todas las transacciones para evitar un interbloqueo.|  
  
## <a name="600"></a>600  
  
|||  
|-|-|  
|601|Nombre de alias ya está en uso.|  
|602|Operación no es válida para un campo Memo, General o imagen.|  
|612|Se define ninguna dicho menú o elemento de menú.|  
|618|Menú no se ha definido mediante DEFINE MENU.|  
|624|Título de menú no se ha definido mediante DEFINE PAD.|  
|625|Menú no se ha definido mediante DEFINE POPUP.|  
|631|Dimensiones de la matriz no son válidas.|  
|637|Exclusivamente para convertir el archivo Memo se debe abrir el archivo.|  
|638|Campo debe ser un campo de memorando.|  
|649|No hay ningún comando PRINTJOB anterior que corresponda a este comando.|  
|651|No se permite cancelar o suspender.|  
|659|La tabla tiene campos memo que no se puede convertir al abrir como de sólo lectura.|  
|683|No se encuentra la etiqueta de índice.|  
  
## <a name="700"></a>700  
  
|||  
|-|-|  
|700|Registro está en uso por otro usuario.|  
|701|Se debe abrir archivo exclusivamente.|  
|702|Archivo está en uso por otro usuario.|  
|703|Registro no está bloqueado.|  
|705|Se denegó el acceso de archivo.|  
|706|No se puede ordenar. Archivos IDX en orden descendente.|  
|707|Estructural. No se encuentra el archivo CDX.|  
|708|Archivo está abierto en otra área de trabajo.|  
|712|Nombre del campo es un duplicado o no es válido.|  
|714|Ventana '*valor*' no se ha definido.|  
|718|Archivo es de solo lectura.|  
|722|Expresión de preprocesador no es válido.|  
|734|Propiedad *valor* no se encuentra.|  
|737|*valor* es un método, evento u objeto.|  
|738|Propiedad *valor* no es un método o el evento.|  
|740|*valor* es una propiedad de solo lectura.|  
|748|Este archivo es incompatible con la versión actual de Visual FoxPro.|  
|750|Archivo se creó en una versión de Visual FoxPro posterior a la versión actual.|  
|763|Propiedad *valor* ya existe.|  
|773|Tipo de objeto de base de datos no es válido.|  
|784|Este objeto se deriva de una clase base y no tiene una clase primaria.|  
  
## <a name="800"></a>800  
  
|||  
|-|-|  
|802|SQL: No se encuentra la tabla.|  
|872|Hay demasiadas columnas.|  
|879|Ninguna clave principal.|  
|884|Unicidad de índice *valor* se ha infringido.|  
|885|Sólo las etiquetas estructurales pueden definirse como candidato.|  
|886|Índice no aceptar valores NULL.|  
|887|Recursión no válida en la evaluación de la regla.|  
|888|Nombre de etiqueta es demasiado largo.|  
  
## <a name="900"></a>900  
  
|||  
|-|-|  
|901|Valor de argumento de función, tipo o número no es válido.|  
|902|No se pudo evaluador de expresiones.|  
|903|Cadena es demasiado larga para ajustarla.|  
|904|** o ^ error de dominio.|  
|905|LOG(): Cero o negativo que se utiliza como argumento.|  
|906|El argumento de Sqrt() no puede ser negativo.|  
|912|Operación no es válida para un campo General.|  
|914|Número de página de códigos no es válido.|  
|915|Secuencia de intercalación '*valor*' no se encuentra.|  
|918|Nombre de archivo es demasiado largo.|  
|922|El volumen no existe.|  
|923|Objeto *valor* no se encuentra.|  
|924|*valor* no es un objeto.|  
|925|Miembro desconocido *valor*.|  
|928|Instrucción solo es válida dentro de una definición de clase.|  
|929|*valor* sólo puede utilizarse dentro de un método.|  
|930|No se puede redefinir *valor*.|  
|931|Instrucción no está en un procedimiento.|  
|934|Instrucción solo es válida dentro de un método.|  
|935|El objeto actual no hereda de la clase *valor*.|  
|937|Archivo de procedimiento '*valor*' no se encuentra.|  
|938|Objeto no se encuentra en un *valor*.|  
|939|CON / error de coincidencia de ENDWITH.|  
|940|Expresión no es válida fuera de WITH / ENDWITH.|  
|941|Código de error no es válido.|  
|942|Objetos no se puede asignar a las matrices.|  
|943|Miembro *valor* no se evalúa como un objeto.|  
|945|Se ha liberado el objeto actual.|  
|947|Expresión es demasiado compleja.|  
|951|No se puede borrar el objeto en uso.|  
|955|WIN. INI o el registro está dañado.|  
|957|Cola de impresión al obtener acceso al error.|  
|959|Coordenadas no válidas.|  
|960|Redefinición no válida de la variable *valor*.|  
|971|No se puede compilar hasta que haya completado el comando de compilación actual.|  
|972|Matriz *valor* está en uso.|  
|974|Las matrices no se puede asignar a elementos de matriz.|  
|976|No se puede resolver el vínculo primario.|  
|988|Valor de moneda está fuera del intervalo.|  
|990|Cancelar.|  
|999|Función no está implementada.|
