---
title: Glosario ODBC | Documentos de Microsoft
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: odbc
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- ODBC [ODBC], glossary
- glossary [ODBC]
ms.assetid: e8227000-1944-42e5-a881-1f549e1ff9d1
caps.latest.revision: "7"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 4bb77308b74a57fa192acf9aba3fa7d88090d93a
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/20/2017
---
# <a name="odbc-glossary"></a>Glosario ODBC
## <a name="a"></a>Un  
 **plan de acceso**  
 Un plan generado por el motor de base de datos para ejecutar una instrucción SQL. Equivalente a código ejecutable compilado a partir de un lenguaje de tercera generación como C.  
  
 **función de agregado**  
 Una función que genera un único valor de un grupo de valores, que se utiliza a menudo con **GROUP BY** y **HAVING** cláusulas. Las funciones de agregado son **AVG**, **recuento**, **MAX**, **MIN**, y **suma**. También se denomina *funciones de conjunto*. *Vea también* función escalar.  
  
 **ANSI**  
 American National Standards Institute. La API de ODBC se basa en la interfaz de nivel de llamada de ANSI.  
  
 **APD**  
 *Vea* descriptor de parámetro de aplicación (APD).  
  
 **API**  
 Interfaz de programación de aplicaciones. Un conjunto de rutinas que utiliza una aplicación para solicitar y realizar servicios de bajo nivel. La API de ODBC se compone de las funciones ODBC.  
  
 **aplicación**  
 Un programa ejecutable que llama a funciones de la API de ODBC.  
  
 **descriptor de parámetro de aplicación (APD)**  
 Un descriptor que describe los parámetros dinámicos que se usa en una instrucción SQL antes de realizar ninguna conversión especificado por la aplicación.  
  
 **descriptor de fila de la aplicación (descartar)**  
 Un descriptor que representa los metadatos de columna y los datos en búferes de la aplicación, que describe una fila de datos después de cualquier conversión de datos especificado por la aplicación.  
  
 **DESCARTAR**  
 *Vea* descriptor de fila de la aplicación (descartar).  
  
 **modo de confirmación automática**  
 Modo de confirmación de transacción en el que las transacciones se confirman inmediatamente después de que se ejecutan.  
  
## <a name="b"></a>B  
 **cambio de comportamiento**  
 Un cambio en cierta funcionalidad de ODBC 3*.x* comportamiento de ODBC 2. *x* comportamiento, o viceversa. Ocasiona el cambio del atributo de entorno SQL_ATTR_ODBC_VERSION.  
  
 **Objeto binario grande (BLOB)**  
 Todos los datos binarios a través de un número determinado de bytes, como 255. Suele ser mucho mayor. En general, estos datos se envía a y recuperados del origen de datos en partes. También se denomina *datos long*.  
  
 **enlace**  
 Como un verbo, la acción de asociar una columna de un conjunto de resultados o un parámetro en una instrucción SQL a una variable de aplicación. Como un nombre, la asociación.  
  
 **desplazamiento de enlace**  
 Agregado un valor a las direcciones de búfer de datos y direcciones de búfer de longitud/indicador para todos los enlaza la columna o parámetro de datos, generar nuevas direcciones.  
  
 **cursor de bloque**  
 Un cursor capaz de capturar más de una fila de datos cada vez.  
  
 **búfer**  
 Una parte de memoria de la aplicación usa para pasar datos entre la aplicación y el controlador. Búferes a menudo vienen en parejas: una *búfer de datos* y un *búfer de longitud de datos*.  
  
 **bytes**  
 Ocho bits o un octeto. *Vea también* octeto.  
  
## <a name="c"></a>C  
 **Tipo de datos C**  
 El tipo de datos de una variable en un programa de C, en este caso, la aplicación.  
  
 **catálogo**  
 El conjunto de tablas del sistema en una base de datos que describen la forma de la base de datos. También se denomina un *esquema* o *diccionario de datos*.  
  
 **función de catálogo**  
 Una función ODBC que se utiliza para recuperar información de catálogo de la base de datos.  
  
 **CLI**  
 *Vea* API.  
  
 **cliente/servidor**  
 Una estrategia de acceso de base de datos en el que uno o más clientes tener acceso a datos a través de un servidor. Los clientes implementan generalmente la interfaz de usuario, mientras que los controles de servidor acceso a la base de datos.  
  
 **columna**  
 Contenedor para un único elemento de información en una fila. También se denomina *campo*.  
  
 **confirmación**  
 Para realizar los cambios en una transacción permanentes.  
  
 **simultaneidad**  
 La capacidad de más de una transacción para tener acceso a los mismos datos al mismo tiempo.  
  
 **nivel de conformidad**  
 Un conjunto discreto de funcionalidad que admite un controlador u origen de datos. ODBC define los niveles de compatibilidad de API y los niveles de compatibilidad de SQL.  
  
 **conexión**  
 Una instancia determinada de un origen de datos y controlador.  
  
 **exploración de conexión**  
 Búsqueda de orígenes de datos para conectarse a la red. Exploración de conexión puede consistir en varios pasos. Por ejemplo, el usuario puede examinar primero la red para servidores y, a continuación, busque un servidor determinado para una base de datos.  
  
 **identificador de conexión**  
 Un identificador a una estructura de datos que contiene información sobre una conexión.  
  
 **fila actual**  
 La fila al que señala actualmente el cursor. Operaciones por posición actúan en la fila actual.  
  
 **cursor**  
 Un elemento de software que devuelve filas de datos a la aplicación. Probablemente denominado después del cursor parpadeante en un equipo de terminal; al igual que en que el cursor indica la posición actual en la pantalla, un cursor en un conjunto de resultados indica la posición actual en el conjunto de resultados.  
  
## <a name="d"></a>D  
 **búfer de datos**  
 Un búfer que se usa para pasar datos. A menudo se asocian con datos de búfer es un *búfer de longitud de datos*.  
  
 **diccionario de datos**  
 *Vea* catálogo.  
  
 **búfer de longitud de datos**  
 Un búfer que se utiliza para pasar la longitud del valor en su correspondiente *búfer de datos*. El búfer de longitud de datos también se utiliza para almacenar los indicadores, por ejemplo, si el valor de datos está terminada en null.  
  
 **origen de datos**  
 Los datos que el usuario desea acceso y su sistema operativo asociado, el DBMS y la plataforma de red (si existe).  
  
 **tipo de datos**  
 El tipo de un elemento de datos. ODBC define los tipos de datos de C y SQL. *Vea también* indicador de tipo.  
  
 **columna de datos en ejecución**  
 Una columna para la que se envían los datos después de **SQLSetPos** se llama. Denominada así porque los datos se envían en tiempo de ejecución, en lugar de que se colocan en un búfer de conjunto de filas. Por lo general se envían datos largos en partes en tiempo de ejecución.  
  
 **parámetro de datos en ejecución**  
 Un parámetro para el que se envían los datos después de **SQLExecute** o **SQLExecDirect** se llama. Denominada así porque los datos se envían cuando se ejecuta la instrucción SQL en lugar de que se colocan en un búfer de parámetro. Por lo general se envían datos largos en partes en tiempo de ejecución.  
  
 **database**  
 Una colección discreta de datos en un DBMS. También un DBMS.  
  
 **motor de base de datos**  
 El software en un DBMS que analiza y ejecuta instrucciones SQL y tiene acceso a los datos físicos.  
  
 **DBMS**  
 Sistema de administración de bases de datos. Capa de software entre la base de datos física y el usuario. El sistema DBMS administra todo el acceso a la base de datos.  
  
 **Controladores basados en DBMS**  
 Un controlador que tiene acceso a los datos físicos a través de un motor de base de datos independiente.  
  
 **DDL**  
 Lenguaje de definición de datos. Estas instrucciones en SQL que definen, en lugar de manipular los datos. Por ejemplo, **CREATE TABLE**, **CREATE INDEX**, **GRANT**, y **REVOCAR**.  
  
 **identificador delimitado**  
 Un identificador que se incluye en los caracteres de comillas de identificador, por lo que puede contener caracteres especiales o coincidir con palabras clave (también conocido como un identificador entre comillas).  
  
 **descriptor**  
 Una estructura de datos que contiene información sobre los datos de las columnas o los parámetros dinámicos. No se define la representación física del descriptor; las aplicaciones tenga acceso directo a un descriptor solo mediante la manipulación de sus campos mediante una llamada a funciones ODBC con el identificador de descriptor.  
  
 **base de datos de escritorio**  
 Un DBMS diseñado para ejecutarse en un equipo personal. En general, estos DBMS no proporcionan un motor de base de datos independiente y deben ser accesible a través de un controlador basados en archivos. Por lo general los motores de estos controladores reducen el soporte para SQL y las transacciones. Por ejemplo, dBASE, Paradox, Btrieve o Microsoft® FoxPro®.  
  
 **diagnóstico**  
 Un registro que contiene información de diagnóstico sobre la última función llamada a que utiliza un identificador concreto. Los registros de diagnóstico están asociados con el entorno, conexión, instrucción e identificadores de descriptor.  
  
 **DML**  
 Lenguaje de manipulación de datos. Estas instrucciones en SQL que manipulan, en lugar de para definir los datos. Por ejemplo, **insertar**, **actualización**, **eliminar**, y **seleccione**.  
  
 **controlador**  
 Una biblioteca de la rutina que expone las funciones de la API de ODBC. Los controladores son específicos para un DBMS único.  
  
 **Administrador de controladores**  
 Una biblioteca de la rutina que administra el acceso a los controladores para la aplicación. El Administrador de controladores se carga y descarga (o se conecta a y desconecta) llamadas de controladores y pasa a funciones ODBC para el controlador adecuado.  
  
 **DLL de instalación de controlador**  
 Un archivo DLL que contiene funciones específicas del controlador de instalación y configuración.  
  
 **cursor dinámico**  
 Un cursor desplazable capaz de detectar filas actualizado, eliminadas o insertadas en el conjunto de resultados.  
  
 **SQL dinámico**  
 Un tipo de SQL incrustado en qué SQL instrucciones se crean y se compila en tiempo de ejecución. *Vea también* SQL estático.  
  
## <a name="e"></a>E  
 **SQL incrustado**  
 Instrucciones SQL que se incluyen directamente en un programa escrito en otro lenguaje, como COBOL o C. ODBC no utiliza SQL incrustado. *Vea también* SQL estático *y* SQL dinámico.  
  
 **entorno de**  
 Un contexto global en el que se va a obtener acceso a datos; asociado con el entorno es toda la información que es global por naturaleza, como una lista de todas las conexiones en ese entorno.  
  
 **identificador de entorno**  
 Un identificador a una estructura de datos que contiene información sobre el entorno.  
  
 **cláusula de escape**  
 Una cláusula en una instrucción SQL.  
  
 **ejecutar**  
 Para ejecutar una instrucción SQL.  
  
## <a name="f"></a>F  
 **cursor grueso**  
 *Vea* cursor de bloque.  
  
 **FETCH**  
 Para recuperar una o varias filas de un conjunto de resultados.  
  
 **campo**  
 *Vea* columna.  
  
 **controladores basados en archivos**  
 Un controlador que tiene acceso directo a los datos físicos. En este caso, el controlador contiene un motor de base de datos y actúa como controlador y el origen de datos.  
  
 **origen de datos de archivo**  
 Un origen de datos de conexión que la información se almacena en un archivo de DSN.  
  
 **clave externa**  
 Una o varias columnas en una tabla que coincida con la clave principal de otra tabla.  
  
 **cursor de solo avance**  
 Un cursor que solo puede desplazarse hacia delante a través del conjunto de resultados y generalmente captura solo una fila cada vez. La mayoría de bases de datos relacionales admiten solo los cursores de solo avance.  
  
## <a name="h"></a>H  
 **identificador**  
 Un valor que identifica de forma única algo, como una estructura de datos o de archivos. Identificadores sólo son significativos para el software que crea y utiliza, pero se pasa por otro software para identificar las cosas. ODBC define identificadores para los entornos, las conexiones, instrucciones y descriptores.  
  
## <a name="i"></a>I  
 **descriptor de parámetro de implementación (IPD)**  
 Un descriptor que describe los parámetros dinámicos que se usa en una instrucción SQL después de realizar ninguna conversión especificado por la aplicación.  
  
 **descriptor de fila de implementación (IRD)**  
 Un descriptor que describe una fila de datos antes de realizar cualquier conversión especificado por la aplicación.  
  
 **instalador de DLL**  
 Un archivo DLL que instala los componentes de ODBC y configura los orígenes de datos.  
  
 **Integrity Enhancement Facility**  
 Un subconjunto de SQL diseñado para mantener la integridad de una base de datos.  
  
 **nivel de conformidad de interfaz**  
 El nivel de la interfaz de ODBC 3.7 admitido por un controlador; puede ser Core, nivel 1 o nivel 2.  
  
 **interoperabilidad**  
 La capacidad de una aplicación para usar el mismo código de error al obtener acceso a datos en diferentes DBMS.  
  
 **IPD**  
 *Vea* Descriptor de parámetro de implementación (IPD).  
  
 **IRD**  
 *Vea* Descriptor de fila de implementación (IRD).  
  
 **ISO/IEC**  
 Comisión Electrotécnica de estándares internacionales organización internacional. La API de ODBC se basa en la interfaz de nivel de llamada ISO/IEC.  
  
## <a name="j"></a>J  
 **combinación**  
 Una operación en una base de datos relacional que vincula las filas de dos o más tablas haciendo coincidir valores en columnas especificadas.  
  
## <a name="k"></a>K  
 **clave**  
 Una o varias columnas cuyos valores identifican una fila. *Vea también* clave externa *y* clave principal.  
  
 **conjunto de claves**  
 Un conjunto de claves que usa un cursor controlado por conjunto de claves o mixto para capturar filas.  
  
 **cursor controlado por conjunto de claves**  
 Un cursor desplazable que detecta las filas actualizadas y eliminadas mediante el uso de un conjunto de claves.  
  
## <a name="l"></a>L  
 **literal**  
 Una representación de caracteres de un valor de datos reales en una instrucción SQL.  
  
 **bloqueo**  
 El proceso mediante el cual un DBMS restringe el acceso a una fila en un entorno multiusuario. El DBMS normalmente establece un bit en la página física que contiene una fila que indica la fila o una fila o página está bloqueada.  
  
 **datos de tipo Long**  
 Los datos binarios o de caracteres en una determinada longitud como 255 bytes o caracteres. Suele ser mucho mayor. En general, estos datos se envía a y recuperados del origen de datos en partes. También se denomina *BLOB*s o *CLOB*s.  
  
## <a name="m"></a>M  
 **origen de datos de máquina**  
 Un origen de datos para la conexión que se almacena información en el sistema (por ejemplo, el registro).  
  
 **modo de confirmación manual**  
 Un modo de confirmación de transacción en el que las transacciones se deben confirmar explícitamente mediante una llamada a **SQLTransact**.  
  
 **metadatos**  
 Datos que describe un parámetro en una instrucción SQL o una columna de un conjunto de resultados. Por ejemplo, el tipo de datos, longitud de bytes y la precisión de un parámetro.  
  
 **controlador de varios niveles**  
 *Vea* controladores basados en DBMS.  
  
## <a name="n"></a>N  
 **Valor NULL**  
 No tener ningún valor asignado explícitamente. En concreto, un valor NULL es distinto de cero o un espacio en blanco.  
  
## <a name="o"></a>O  
 **octeto**  
 Ocho bits o un byte. *Vea también* bytes.  
  
 **longitud en octetos**  
 La longitud en octetos de un búfer o los datos que contiene.  
  
 **ODBC**  
 Conectividad de base de datos abierta. Especificación de una API que define un conjunto estándar de rutinas con el que una aplicación puede tener acceso a los datos en un origen de datos.  
  
 **Administrador de ODBC**  
 Un programa ejecutable que llama al archivo DLL para configurar orígenes de datos del instalador.  
  
 Abrir grupo  
 Una compañía que publica los estándares. En concreto, publica los estándares del grupo de acceso de SQL (SAG).  
  
 **simultaneidad optimista**  
 Una estrategia para aumentar la simultaneidad en el que no se bloquean las filas. En su lugar, antes de que se actualizan o eliminan, un cursor se comprueba para ver si se han cambiado desde su última lectura. Si es así, la actualización o eliminación se produce un error. *Vea también* simultaneidad pesimista.  
  
 **combinación externa**  
 Combinación en las filas que no coincidentes y coincidentes se devuelven. Los valores de todas las columnas de la tabla no coincidente de las filas no coincidentes se establecen en NULL.  
  
 **propietario**  
 El propietario de una tabla.  
  
## <a name="p"></a>P  
 **parámetro**  
 Una variable en una instrucción SQL, marcada con un marcador de parámetro o un signo de interrogación (?). Parámetros enlazados a variables de aplicación y sus valores que se recuperan cuando se ejecuta la instrucción.  
  
 **descriptor del parámetro**  
 Un descriptor que describe los parámetros de tiempo de ejecución que se usa en una instrucción SQL, ya sea antes de realizar ninguna conversión especificada por la aplicación (un descriptor de parámetro de la aplicación o APD) o después de cualquier conversión especificado por la aplicación (una implementación descriptor del parámetro, o IPD).  
  
 **matriz de operación de parámetros**  
 Una matriz que contiene valores que una aplicación puede establecer para indicar que se debe omitir el parámetro correspondiente en un **SQLExecDirect** o **SQLExecute** operación.  
  
 **matriz de Estados de parámetro**  
 Una matriz que contiene el estado de un parámetro después de llamar a **SQLExecDirect** o **SQLExecute**.  
  
 **simultaneidad pesimista**  
 Una estrategia para implementar la seriabilidad, en los que se bloquean filas para que otras transacciones no pueden cambiarlos. *Vea también* simultaneidad optimista *y* seriabilidad.  
  
 **operación por posición**  
 Cualquier operación que actúa en la fila actual. Por ejemplo, la actualización por posición y eliminar las instrucciones, **SQLGetData**, y **SQLSetPos**.  
  
 **instrucción de actualización posicionada**  
 Una instrucción SQL que se utiliza para actualizar los valores de la fila actual.  
  
 **instrucción delete posicionadas**  
 Una instrucción SQL que se usa para eliminar la fila actual.  
  
 **preparar**  
 Para compilar una instrucción SQL. Un plan de acceso se crea al preparar una instrucción SQL.  
  
 **clave principal**  
 Una o varias columnas que identifica de forma única una fila de una tabla.  
  
 **procedimiento**  
 Un grupo de uno o varios había precompilado instrucciones SQL que se almacenan como un objeto con nombre en una base de datos.  
  
 **columna de procedimiento**  
 Un argumento en una llamada de procedimiento, el valor devuelto por un procedimiento o una columna de un conjunto de resultados creado por un procedimiento.  
  
## <a name="q"></a>Q  
 **calificador**  
 Una base de datos que contiene una o varias tablas.  
  
 **consulta**  
 Una instrucción SQL. A veces se usan para diferenciar una **seleccione** instrucción.  
  
 **quoted identifier**  
 Un identificador que se incluye en los caracteres de comillas de identificador, por lo que puede contener caracteres especiales o coincidir con palabras clave (también conocida como identificadores delimitados de SQL-92).  
  
## <a name="r"></a>L  
 **base**  
 La base de un sistema de numeración. Por lo general, 2 o 10.  
  
 **registro**  
 *Vea* fila.  
  
 **conjunto de resultados**  
 El conjunto de filas creadas mediante la ejecución de un **seleccione** instrucción.  
  
 **código de retorno**  
 El valor devuelto por una función ODBC.  
  
 **revertir**  
 Para devolver los valores cambiados por una transacción a su estado original.  
  
 **fila**  
 Un conjunto de columnas relacionadas que describen una entidad específica. También se denomina un *registro*.  
  
 **descriptor de fila**  
 Un descriptor que describe las columnas del conjunto de resultados, ya sea antes de realizar ninguna conversión especificada por la aplicación (un descriptor de fila de implementación o IRD) o después de cualquier conversión especificado por la aplicación (un descriptor de fila de la aplicación o descartar).  
  
 **matriz de operación de fila**  
 Una matriz que contiene valores que una aplicación puede establecer para indicar que se debe omitir la fila correspondiente en un **SQLSetPos** operación.  
  
 **matriz de Estados de fila**  
 Una matriz que contiene el estado de una fila después de llamar a **SQLFetch**, **SQLFetchScroll**, o **SQLSetPos**.  
  
 **conjunto de filas**  
 El conjunto de filas devueltas en una sola operación de obtención de un cursor de bloque.  
  
 **búferes de conjunto de filas**  
 Los búferes enlazados a las columnas del conjunto de resultados y en la que se devuelven los datos de un conjunto de filas completo.  
  
## <a name="s"></a>S  
 **SAG**  
 *Vea* grupo de acceso SQL (SAG).  
  
 **función escalar**  
 Una función que genera un único valor de un solo valor. Por ejemplo, una función que cambia el caso de los datos de caracteres.  
  
 **esquema**  
 *Vea* catálogo.  
  
 **cursores desplazables**  
 Un cursor que puede desplazarse hacia delante o hacia atrás por el conjunto de resultados.  
  
 **la posibilidad de serializar**  
 Si dos transacciones que se ejecutan simultáneamente generan un resultado que es el mismo que la ejecución de la serie (o secuencial) de esas transacciones. Las transacciones serializables están obligadas a mantener la integridad de la base de datos.  
  
 **base de datos de servidor**  
 Un DBMS diseñado para ejecutarse en un entorno de cliente/servidor. Estos DBMS proporcionan un motor de base de datos independiente que proporciona compatibilidad enriquecida para SQL y las transacciones. Se accede a estos a través de controladores basados en DBMS. Por ejemplo, Oracle, Informix, DB/2 o Microsoft® SQL Server.  
  
 **función de conjunto**  
 *Vea* función de agregado.  
  
 **archivo DLL de configuración**  
 *Vea* el programa de instalación de controlador DLL *y* el programa de instalación de traductor DLL.  
  
 **controlador de nivel único**  
 *Vea* controladores basados en archivos.  
  
 **SQL**  
 Lenguaje de consulta estructurado. Un idioma usado por las bases de datos relacionales para consultar, actualizar y administrar datos.  
  
 **Grupo de acceso SQL (SAG)**  
 Un consorcio de la industria de las empresas afectadas con DBMS de SQL. Interfaz de nivel de llamada del grupo abierto se basa en el trabajo realizado originalmente por el grupo de acceso de SQL.  
  
 **Nivel de conformidad de SQL**  
 El nivel de gramática de SQL-92 compatible con un controlador; puede ser la entrada, transición de FIPS, intermedio o completo.  
  
 **Tipo de datos SQL**  
 El tipo de datos de una columna o parámetro tal y como se almacena en el origen de datos.  
  
 **SQLSTATE**  
 Un valor de cinco caracteres que indica un error determinado.  
  
 **Instrucción SQL**  
 Una frase completa en SQL que comienza con una palabra clave y se describe completamente una acción que se realizará. Por ejemplo, seleccione * FROM Orders. Las instrucciones SQL no deben confundirse con las instrucciones.  
  
 **estado**  
 Una condición bien definida de un elemento. Por ejemplo, una conexión tiene siete estados, incluidos los datos sin asignar, asignados, conectados y que necesitan. Ciertas operaciones pueden realizarse solo cuando un elemento está en un estado determinado. Por ejemplo, se puede liberar una conexión solo cuando está en un estado de asignación y no es así, por ejemplo, cuando está en estado conectado.  
  
 **transición de estado**  
 El movimiento de un elemento de un estado a otro. ODBC define las transiciones de estado rigurosas para entornos, las conexiones y las instrucciones.  
  
 **instrucción**  
 Un contenedor para toda la información relacionada con una instrucción SQL. Las instrucciones no deben confundirse con instrucciones SQL.  
  
 **identificador de instrucción**  
 Un identificador a una estructura de datos que contiene información sobre una instrucción.  
  
 **cursor estático**  
 Un cursor desplazable que no puede detectar las actualizaciones, elimina o inserta en el conjunto de resultados. Normalmente se implementa mediante la realización de una copia del conjunto de resultados.  
  
 **SQL estático**  
 Un tipo de SQL incrustado en qué SQL instrucciones están codificados de forma rígida y compiladas cuando se compila el resto del programa. *Vea también* SQL dinámico.  
  
 **procedimiento almacenado**  
 *Vea* procedimiento.  
  
## <a name="t"></a>T  
 **table**  
 Una colección de filas.  
  
 **thunk**  
 La conversión de 16 bits direcciones a direcciones de 32 bits, o viceversa, cuando se utilizan las aplicaciones de 16 bits con controladores ODBC de 32 bits.  
  
 **transacción**  
 Una unidad atómica de trabajo. El trabajo en una transacción debe completarse como un todo; Si se produce un error en cualquier parte de la transacción, se produce un error en toda la transacción.  
  
 **aislamiento de transacción**  
 El acto de aislamiento de una transacción de los efectos de todas las demás transacciones.  
  
 **nivel de aislamiento de transacción**  
 Una medida de la medida una transacción está aislada. Hay cinco niveles de aislamiento de transacción: Read Uncommitted, Read Committed, Repeatable Read, Serializable y control de versiones.  
  
 **archivo DLL de traducción**  
 Un archivo DLL se usa para traducir los datos de un juego de caracteres a otro.  
  
 **programa de instalación de traductor DLL**  
 Un archivo DLL que contiene las funciones de instalación y configuración de traductor específica.  
  
 **confirmación en dos fases**  
 El proceso de confirmación de una transacción distribuida en dos fases. En la primera fase, el procesador de transacción comprueba que se pueden confirmadas todas las partes de la transacción. En la segunda fase, se confirman todas las partes de la transacción. Si cualquier parte de la transacción se indica en la primera fase que no se puede confirmar, no se produce la segunda fase. ODBC no admite confirmaciones en dos fases.  
  
 **indicador de tipo**  
 Un valor entero pasados o devueltos desde una función ODBC para indicar el tipo de datos de una variable de aplicación, un parámetro o una columna. ODBC define indicadores de tipo para tipos de datos C y SQL.  
  
## <a name="v"></a>V  
 **vista**  
 Una manera alternativa de mirando los datos en una o varias tablas. Normalmente se crea una vista como un subconjunto de las columnas de una o más tablas. En ODBC, las vistas son suele ser equivalentes a las tablas.
