---
title: Glosario ODBC | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- ODBC [ODBC], glossary
- glossary [ODBC]
ms.assetid: e8227000-1944-42e5-a881-1f549e1ff9d1
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 33116adaf74ed2d3fc52fec460859a7672ce2d0a
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "63057790"
---
# <a name="odbc-glossary"></a>Glosario de ODBC
## <a name="a"></a>A  
 **plan de acceso**  
 Un plan generado por el motor de base de datos para ejecutar una instrucción SQL. Equivalente al código ejecutable compilado a partir de un lenguaje de tercera generación como C.  
  
 **Función de agregado**  
 Una función que genera un único valor de un grupo de valores, que se utiliza a menudo con **GROUP BY** y **HAVING** cláusulas. Incluirán funciones de agregado **AVG**, **recuento**, **MAX**, **MIN**, y **suma**. También se denomina *establecer funciones*. *Vea también* función escalar.  
  
 **ANSI**  
 American National Standards Institute. La API de ODBC se basa en la interfaz de nivel de llamada de ANSI.  
  
 **APD**  
 *Consulte* descriptor de parámetro de aplicación (APD).  
  
 **API**  
 Interfaz de programación de aplicaciones. Un conjunto de rutinas que utiliza una aplicación para solicitar y llevar a cabo servicios de nivel inferior. La API de ODBC se compone de las funciones de ODBC.  
  
 **application**  
 Un programa ejecutable que llama a funciones en la API de ODBC.  
  
 **descriptor de parámetro de aplicación (APD)**  
 Un descriptor que describe los parámetros dinámicos que se usa en una instrucción SQL antes de cualquier conversión especificado por la aplicación.  
  
 **descriptor de fila de la aplicación (descartar)**  
 Un descriptor que representa los metadatos de columna y los datos en búferes de la aplicación, que describe una fila de datos después de cualquier conversión de datos especificado por la aplicación.  
  
 **ARD**  
 *Consulte* descriptor de fila de la aplicación (descartar).  
  
 **modo de confirmación automática**  
 Modo de confirmación de transacción en el que las transacciones se confirman inmediatamente después de que se ejecutan.  
  
## <a name="b"></a>B  
 **cambio de comportamiento**  
 Un cambio en cierta funcionalidad de ODBC 3 *.x* comportamiento de ODBC 2. *x* comportamiento, o viceversa. Se produjo al cambiar el atributo de entorno SQL_ATTR_ODBC_VERSION.  
  
 **Objeto binario grande (BLOB)**  
 Cualquier dato binario en un determinado número de bytes, como 255. Suele ser mucho mayor. Estos datos generalmente se envía al y recuperarse del origen de datos en partes. También se denomina *datos long*.  
  
 **binding**  
 Como un verbo, el acto de asociación de una columna de un conjunto de resultados o un parámetro en una instrucción SQL con una variable de aplicación. Como un nombre, la asociación.  
  
 **desplazamiento de enlace**  
 Un valor agregado a las direcciones de búfer de datos y las direcciones de búfer de longitud/indicador para todos los enlaza la columna o parámetro de datos, generar nuevas direcciones.  
  
 **cursor de bloque**  
 Un cursor capaz de capturar más de una fila de datos cada vez.  
  
 **buffer**  
 Una parte de memoria de la aplicación usa para pasar datos entre la aplicación y controlador. Los búferes suelen presentan en parejas: un *búfer de datos* y un *búfer de longitud de datos*.  
  
 **byte**  
 Ocho bits o un octeto. *Vea también* octeto.  
  
## <a name="c"></a>C  
 **Tipo de datos C**  
 El tipo de datos de una variable en un programa C, en este caso, la aplicación.  
  
 **catalog**  
 El conjunto de tablas del sistema en una base de datos que describen la forma de la base de datos. También se denomina un *esquema* o *diccionario de datos*.  
  
 **función de catálogo**  
 Una función ODBC que se usa para recuperar información del catálogo de la base de datos.  
  
 **CLI**  
 *Consulte* API.  
  
 **client/server**  
 Una estrategia de acceso de base de datos en el que uno o más clientes tener acceso a datos a través de un servidor. Normalmente, los clientes implementan la interfaz de usuario mientras que los controles de servidor acceso de base de datos.  
  
 **column**  
 El contenedor de un solo elemento de información en una fila. También se denomina *campo*.  
  
 **commit**  
 Para realizar los cambios en una transacción permanentes.  
  
 **concurrency**  
 La capacidad de más de una transacción para tener acceso a los mismos datos al mismo tiempo.  
  
 **nivel de cumplimiento**  
 Un conjunto discreto de funcionalidad admitida por un controlador u origen de datos. ODBC define los niveles de compatibilidad de API y los niveles de compatibilidad de SQL.  
  
 **connection**  
 Una instancia determinada de un origen de datos y el controlador.  
  
 **exploración de la conexión**  
 Buscando en la red para conectarse a los orígenes de datos. Exploración de la conexión puede implicar varios pasos. Por ejemplo, el usuario puede examinar primero la red para servidores y, a continuación, busque un servidor determinado para una base de datos.  
  
 **identificador de conexión**  
 Identificador de una estructura de datos que contiene información sobre una conexión.  
  
 **Fila actual**  
 La fila que apunta actualmente el cursor. Operaciones por posición actúan en la fila actual.  
  
 **cursor**  
 Un componente de software que devuelve filas de datos a la aplicación. Probablemente con el nombre del cursor parpadeante en un equipo de terminal; al igual que en el que el cursor indica la posición actual en la pantalla, un cursor en un conjunto de resultados indica la posición actual en el conjunto de resultados.  
  
## <a name="d"></a>D  
 **búfer de datos**  
 Un búfer que se usa para pasar datos. A menudo se asocian con datos de un búfer es un *búfer de longitud de datos*.  
  
 **diccionario de datos**  
 *Consulte* catálogo.  
  
 **búfer de longitud de datos**  
 Un búfer que se usa para pasar la longitud del valor de una correspondiente *búfer de datos*. El búfer de longitud de datos también se utiliza para almacenar los indicadores, por ejemplo, si el valor de datos está terminada en null.  
  
 **Origen de datos**  
 Los datos que el usuario desea acceso y su sistema operativo asociado, DBMS y plataforma de red (si existe).  
  
 **Tipo de datos**  
 El tipo de un elemento de datos. ODBC define los tipos de datos de C y SQL. *Vea también* indicador de tipo.  
  
 **columna de datos en ejecución**  
 Una columna para el que se envían los datos después de **SQLSetPos** se llama. Se denomina así porque los datos se envían en tiempo de ejecución en lugar de que se colocan en un búfer de conjunto de filas. Por lo general se envían datos largos en partes en tiempo de ejecución.  
  
 **parámetro de datos en ejecución**  
 Un parámetro para el que se envían los datos después de **SQLExecute** o **SQLExecDirect** se llama. Se denomina así porque los datos se envían cuando se ejecuta la instrucción SQL en lugar de que se colocan en un búfer de parámetro. Por lo general se envían datos largos en partes en tiempo de ejecución.  
  
 **database**  
 Una colección discreta de datos en un DBMS. También es un DBMS.  
  
 **Motor de base de datos**  
 El software en un sistema DBMS que se analiza y ejecuta instrucciones SQL y tiene acceso a los datos físicos.  
  
 **DBMS**  
 Sistema de administración de bases de datos. Capa de software entre la base de datos física y el usuario. El sistema DBMS administra todo el acceso a la base de datos.  
  
 **Controladores basados en DBMS**  
 Un controlador que tiene acceso a los datos físicos a través de un motor de base de datos independiente.  
  
 **DDL**  
 Lenguaje de definición de datos. Esas instrucciones en SQL que definen, en lugar de manipular los datos. Por ejemplo, **CREATE TABLE**, **CREATE INDEX**, **GRANT**, y **REVOCAR**.  
  
 **identificadores delimitados**  
 Un identificador que se incluye en los caracteres de comillas de identificador, por lo que puede contener caracteres especiales o coincidir con palabras clave (también conocido como un identificador entre comillas).  
  
 **descriptor**  
 Una estructura de datos que contiene información sobre los datos de las columnas o parámetros dinámicos. La representación física del descriptor no está definida; las aplicaciones obtienen acceso directo a un descriptor de solo manipulando sus campos mediante una llamada a funciones ODBC con el identificador de descriptor.  
  
 **desktop database**  
 Un DBMS diseñado para ejecutarse en un equipo personal. Por lo general, estos DBMS no proporcionan un motor de base de datos independiente y deben tener acceso a través de un controlador basado en archivos. Generalmente, los motores de estos controladores han reducido compatibilidad con SQL y las transacciones. Por ejemplo, dBASE, Paradox, Btrieve o Microsoft® FoxPro.  
  
 **diagnostic**  
 Un registro que contiene información de diagnóstico sobre la última función llama usa un identificador determinado. Los registros de diagnóstico se asocian con el entorno, conexión, instrucción y los identificadores de descriptor.  
  
 **DML**  
 Lenguaje de manipulación de datos. Esas instrucciones en SQL que manipulan, en lugar de para definir los datos. Por ejemplo, **insertar**, **actualización**, **eliminar**, y **seleccione**.  
  
 **driver**  
 Una biblioteca de rutina que expone las funciones de la API de ODBC. Los controladores son específicos de un DBMS único.  
  
 **Administrador de controladores**  
 Una biblioteca de rutina que administra el acceso a los controladores para la aplicación. El Administrador de controladores, carga y descarga (o se desconecta y se conecta a) controladores y pasa las llamadas a funciones ODBC para el controlador correcto.  
  
 **DLL de instalación de controlador**  
 Un archivo DLL que contiene funciones de instalación y configuración específicas del controlador.  
  
 **cursor dinámico**  
 Un cursor desplazable capaz de detectar filas actualizadas, elimina o inserta en el conjunto de resultados.  
  
 **SQL dinámico**  
 Un tipo de SQL incrustado en qué SQL instrucciones se crean y se compilan en tiempo de ejecución. *Vea también* SQL estático.  
  
## <a name="e"></a>E  
 **embedded SQL**  
 Las instrucciones SQL que se incluyen directamente en un programa escrito en otro lenguaje, como COBOL o C. ODBC no utiliza SQL incrustado. *Vea también* SQL estático *y* SQL dinámico.  
  
 **environment**  
 Un contexto global en el que se va a obtener acceso a datos; asociado con el entorno es cualquier información que es global por naturaleza, como una lista de todas las conexiones en ese entorno.  
  
 **identificador de entorno**  
 Identificador de una estructura de datos que contiene información sobre el entorno.  
  
 **cláusula de escape**  
 Una cláusula en una instrucción SQL.  
  
 **execute**  
 Para ejecutar una instrucción SQL.  
  
## <a name="f"></a>F  
 **cursor grueso**  
 *Consulte* cursor de bloque.  
  
 **fetch**  
 Para recuperar una o varias filas de un conjunto de resultados.  
  
 **field**  
 *Consulte* columna.  
  
 **controladores basados en archivos**  
 Controlador que tiene acceso directo a los datos físicos. En este caso, el controlador contiene un motor de base de datos y actúa como origen de datos y controlador.  
  
 **origen de datos de archivo**  
 Un origen de datos para la conexión de la información se almacena en un archivo DSN.  
  
 **Clave externa**  
 Una o varias columnas en una tabla que coinciden con la clave principal de otra tabla.  
  
 **cursor de solo avance**  
 Un cursor que sólo puede mover hacia delante a través del conjunto de resultados y generalmente captura solo una fila a la vez. La mayoría de bases de datos relacionales admiten solo los cursores de solo avance.  
  
## <a name="h"></a>H  
 **handle**  
 Un valor que identifica de forma algo como una estructura de datos o archivo. Los identificadores son significativos sólo para el software que crea y usa pero que se pasa por otro software para identificar las cosas. ODBC define identificadores para los entornos, las conexiones, instrucciones y los descriptores.  
  
## <a name="i"></a>I  
 **descriptor de parámetro de implementación (IPD)**  
 Un descriptor que describe los parámetros dinámicos que se usa en una instrucción SQL después de cualquier conversión especificado por la aplicación.  
  
 **descriptor de fila de implementación (IRD)**  
 Un descriptor que describe una fila de datos antes de cualquier conversión especificado por la aplicación.  
  
 **DLL instalador**  
 Un archivo DLL que instala los componentes ODBC y configura los orígenes de datos.  
  
 **Integrity Enhancement Facility**  
 Un subconjunto de SQL diseñado para mantener la integridad de una base de datos.  
  
 **nivel de conformidad con la interfaz**  
 El nivel de la interfaz ODBC 3.7 compatible con un controlador; puede ser Core, nivel 1 o nivel 2.  
  
 **interoperability**  
 La capacidad de una aplicación para usar el mismo código al obtener acceso a datos en diferentes DBMS.  
  
 **IPD**  
 *Consulte* Descriptor de parámetro de implementación (IPD).  
  
 **IRD**  
 *Consulte* Descriptor de fila de implementación (IRD).  
  
 **ISO/IEC**  
 Comisión Electrotécnica de estándares internacionales organización internacional. La API de ODBC se basa en la interfaz de nivel de llamada ISO/IEC.  
  
## <a name="j"></a>J  
 **join**  
 Una operación en una base de datos relacional que vincula las filas de dos o más tablas haciendo coincidir valores en columnas especificadas.  
  
## <a name="k"></a>K  
 **key**  
 Una o varias columnas cuyos valores identifican una fila. *Vea también* clave externa *y* clave principal.  
  
 **keyset**  
 Un conjunto de claves que usa un cursor controlado por conjunto de claves o mixto para capturar filas.  
  
 **cursor controlado por conjunto de claves**  
 Un cursor desplazable que detecta las filas actualizadas y eliminadas mediante el uso de un conjunto de claves.  
  
## <a name="l"></a>L  
 **literal**  
 Una representación de caracteres de un valor de datos reales en una instrucción SQL.  
  
 **locking**  
 El proceso mediante el cual un DBMS restringe el acceso a una fila en un entorno multiusuario. El DBMS normalmente establece un bit en la página física que contiene una fila que indica la fila o una fila o página se bloquea.  
  
 **datos de tipo Long**  
 Los datos binarios o de caracteres a través de una determinada longitud, por ejemplo, 255 bytes o caracteres. Suele ser mucho mayor. Estos datos generalmente se envía al y recuperarse del origen de datos en partes. También se denomina *BLOB*s o *CLOB*s.  
  
## <a name="m"></a>M  
 **origen de datos de equipo**  
 Un origen de datos para la conexión que se almacena información en el sistema (por ejemplo, el registro).  
  
 **Modo de confirmación manual**  
 Un modo de confirmación de transacción en el que las transacciones se deben confirmar explícitamente mediante una llamada a **SQLTransact**.  
  
 **metadata**  
 Datos que describe un parámetro en una instrucción SQL o una columna de un conjunto de resultados. Por ejemplo, el tipo de datos, longitud de bytes y la precisión de un parámetro.  
  
 **controlador de varios niveles**  
 *Consulte* controladores basados en DBMS.  
  
## <a name="n"></a>N  
 **Valor nulo**  
 No tener ningún valor asignado explícitamente. En concreto, un valor NULL es diferente de cero o un espacio en blanco.  
  
## <a name="o"></a>O  
 **octet**  
 Ocho bits o un byte. *Vea también* bytes.  
  
 **longitud en octetos**  
 La longitud en octetos de un búfer o los datos que contiene.  
  
 **ODBC**  
 Conectividad abierta de base de datos. Especificación de una API que define un conjunto estándar de rutinas que una aplicación puede tener acceso a datos en un origen de datos.  
  
 **Administrador de ODBC**  
 Un programa ejecutable que llama a la DLL para configurar orígenes de datos del instalador.  
  
 Abrir grupo  
 Una compañía que publica los estándares. En concreto, publica los estándares del grupo de acceso de SQL (SAG).  
  
 **Simultaneidad optimista**  
 Una estrategia para aumentar la simultaneidad en el que no se bloquean las filas. En su lugar, antes de que se actualizan o eliminan, un cursor se comprueba para ver si se han cambiado desde que se leyeron por última vez. Si es así, la actualización o eliminación se produce un error. *Vea también* simultaneidad pesimista.  
  
 **combinación externa**  
 Combinación en qué filas no coincidentes y coincidentes se devuelven. Los valores de todas las columnas de la tabla no coincidente en las filas no coincidentes se establecen en NULL.  
  
 **owner**  
 El propietario de una tabla.  
  
## <a name="p"></a>P  
 **parameter**  
 Una variable en una instrucción SQL, se marcan con un marcador de parámetro o un signo de interrogación (?). Los parámetros se enlazan a variables de aplicación y sus valores que se recuperan cuando se ejecuta la instrucción.  
  
 **descriptor de parámetros**  
 Un descriptor que describe los parámetros de tiempo de ejecución usados en una instrucción SQL, ya sea antes de cualquier conversión especificada por la aplicación (un descriptor de parámetro de la aplicación o APD) o después de cualquier conversión especificado por la aplicación (una implementación descriptor del parámetro o IPD).  
  
 **matriz de operación de parámetros**  
 Una matriz que contiene valores que una aplicación puede establecer para indicar que se debe omitir el parámetro correspondiente en un **SQLExecDirect** o **SQLExecute** operación.  
  
 **matriz de Estados de parámetro**  
 Una matriz que contiene el estado de un parámetro después de llamar a **SQLExecDirect** o **SQLExecute**.  
  
 **simultaneidad pesimista**  
 Una estrategia para implementar la seriabilidad, en el que las filas se bloquean para que otras transacciones no pueden cambiarlos. *Vea también* simultaneidad optimista *y* seriabilidad.  
  
 **operación posicionada**  
 Cualquier operación que actúa en la fila actual. Por ejemplo, la actualización por posición y eliminar las instrucciones, **SQLGetData**, y **SQLSetPos**.  
  
 **instrucción de actualización posicionada**  
 Una instrucción SQL que se usa para actualizar los valores de la fila actual.  
  
 **instrucción delete posicionadas**  
 Una instrucción SQL que se usa para eliminar la fila actual.  
  
 **prepare**  
 Para compilar una instrucción SQL. Se crea un plan de acceso al preparar una instrucción SQL.  
  
 **Clave principal**  
 Una o varias columnas que identifica de forma única una fila en una tabla.  
  
 **procedure**  
 Un grupo de uno o varios había precompilado instrucciones SQL que se almacenan como un objeto con nombre en una base de datos.  
  
 **columna de procedimiento**  
 Un argumento en una llamada de procedimiento, el valor devuelto por un procedimiento o una columna en un conjunto de resultados creado por un procedimiento.  
  
## <a name="q"></a>Q  
 **qualifier**  
 Una base de datos que contiene una o varias tablas.  
  
 **query**  
 Una instrucción SQL. A veces se usan para referirse a un **seleccione** instrucción.  
  
 **quoted identifier**  
 Un identificador que se incluye en los caracteres de comillas de identificador, por lo que puede contener caracteres especiales o coincidir con palabras clave (también conocidas como un identificador delimitado de SQL-92).  
  
## <a name="r"></a>R  
 **radix**  
 La base de un sistema de numeración. Por lo general, 2 ó 10.  
  
 **record**  
 *Consulte* fila.  
  
 **conjunto de resultados**  
 El conjunto de filas creadas mediante la ejecución de un **seleccione** instrucción.  
  
 **Código de retorno**  
 El valor devuelto por una función ODBC.  
  
 **revertir**  
 Para devolver los valores modificados por una transacción a su estado original.  
  
 **row**  
 Un conjunto de columnas relacionadas que describen una entidad específica. También se denomina un *registro*.  
  
 **descriptor de fila**  
 Un descriptor que describe las columnas del conjunto de resultados, ya sea antes de cualquier conversión especificada por la aplicación (un descriptor de fila de implementación o IRD) o después de cualquier conversión especificado por la aplicación (un descriptor de fila de la aplicación o descartar).  
  
 **matriz de operación de fila**  
 Una matriz que contiene valores que una aplicación puede establecer para indicar que se debe ignorar la fila correspondiente en un **SQLSetPos** operación.  
  
 **matriz de Estados de fila**  
 Una matriz que contiene el estado de una fila después de llamar a **SQLFetch**, **SQLFetchScroll**, o **SQLSetPos**.  
  
 **rowset**  
 El conjunto de filas devueltas en una sola operación de obtención de un cursor de bloque.  
  
 **búferes del conjunto de filas**  
 Los búferes enlazados a las columnas del conjunto de resultados y en la que se devuelven los datos de un conjunto de filas completo.  
  
## <a name="s"></a>S  
 **SAG**  
 *Consulte* grupo de acceso de SQL (SAG).  
  
 **Función escalar**  
 Una función que genera un único valor de un solo valor. Por ejemplo, una función que cambia el caso de los datos de caracteres.  
  
 **schema**  
 *Consulte* catálogo.  
  
 **cursor desplazable**  
 Un cursor que puede desplazarse hacia delante o hacia atrás por el conjunto de resultados.  
  
 **serializability**  
 Si dos transacciones que se ejecutan simultáneamente producen un resultado que es el mismo que la ejecución de la serie (o secuencial) de esas transacciones. Las transacciones serializables están obligadas a mantener la integridad de la base de datos.  
  
 **base de datos del servidor**  
 Un DBMS diseñado para ejecutarse en un entorno de cliente/servidor. Estos DBMS proporcionan un motor de base de datos independiente que proporciona compatibilidad enriquecida para SQL y las transacciones. Se accede a estos a través de controladores basados en DBMS. Por ejemplo, Oracle, Informix, DB/2 o Microsoft® SQL Server.  
  
 **función Set**  
 *Consulte* función de agregado.  
  
 **archivo DLL de configuración**  
 *Consulte* DLL de instalación de controlador *y* DLL de instalación de traductor.  
  
 **controlador de nivel único**  
 *Consulte* controladores basados en archivos.  
  
 **SQL**  
 Lenguaje de consulta estructurado. Un lenguaje utilizado por las bases de datos relacionales para consultar, actualizar y administrar datos.  
  
 **Grupo de acceso de SQL (SAG)**  
 Un consorcio del sector de las empresas afectadas con DBMS de SQL. Interfaz de nivel de llamada del grupo abierto se basa en el trabajo realizado originalmente por el grupo de acceso de SQL.  
  
 **Nivel de conformidad con SQL**  
 El nivel de gramática de SQL-92 compatible con un controlador; puede ser la entrada, FIPS transitorias, intermedio o completo.  
  
 **Tipo de datos SQL**  
 El tipo de datos de una columna o parámetro tal y como se almacena en el origen de datos.  
  
 **SQLSTATE**  
 Un valor de cinco caracteres que indica un error determinado.  
  
 **Instrucción SQL**  
 Una frase completa de SQL que comienza con una palabra clave y describe una acción que se realizará por completo. Por ejemplo, seleccione * FROM Orders. Las instrucciones SQL no deben confundirse con las instrucciones.  
  
 **state**  
 Una condición bien definida de un elemento. Por ejemplo, una conexión tiene siete estados, incluidos los datos que necesita, conectados, asignados y sin asignar. Ciertas operaciones pueden realizarse solo cuando un elemento está en un estado determinado. Por ejemplo, se puede liberar una conexión solo cuando está en un estado de asignación y no, por ejemplo, cuando se encuentra en estado conectado.  
  
 **transición de estado**  
 El movimiento de un elemento de un estado a otro. ODBC define las transiciones de estado rigurosas para entornos, las conexiones y las instrucciones.  
  
 **instrucción**  
 Un contenedor para toda la información relacionada con una instrucción SQL. Las instrucciones no deben confundirse con las instrucciones SQL.  
  
 **identificador de instrucción**  
 Identificador de una estructura de datos que contiene información sobre una instrucción.  
  
 **cursor estático**  
 Un cursor desplazable que no puede detectar las actualizaciones, elimina o inserta en el conjunto de resultados. Normalmente se implementa mediante la realización de una copia del conjunto de resultados.  
  
 **SQL estático**  
 Un tipo de SQL incrustado en qué SQL las instrucciones están codificados de forma rígida y compilan cuando se compila el resto del programa. *Vea también* SQL dinámico.  
  
 **procedimiento almacenado**  
 *Consulte* procedimiento.  
  
## <a name="t"></a>T  
 **table**  
 Una colección de filas.  
  
 **thunking**  
 La conversión de 16 bits direcciones a las direcciones de 32 bits, o viceversa, cuando se usan las aplicaciones de 16 bits con controladores ODBC de 32 bits.  
  
 **transaction**  
 Una unidad atómica de trabajo. El trabajo en una transacción debe completarse como un todo; Si se produce un error en cualquier parte de la transacción, se produce un error en toda la transacción.  
  
 **aislamiento de transacción**  
 El acto de aislar una transacción de los efectos de todas las demás transacciones.  
  
 **nivel de aislamiento de transacción**  
 Una medida de lo bien una transacción está aislada. Hay cinco niveles de aislamiento de transacción: Read Uncommitted, leer Committed, Repeatable Read, Serializable y control de versiones.  
  
 **translator DLL**  
 Un archivo DLL que se usa para traducir datos de un juego de caracteres a otro.  
  
 **DLL de instalación de traductor**  
 Un archivo DLL que contiene funciones de instalación y configuración específicas del traductor.  
  
 **confirmación en dos fases**  
 El proceso de confirmar una transacción distribuida en dos fases. En la primera fase, el procesador de transacción comprueba que todas las partes de la transacción se pueden confirmadas. En la segunda fase, se confirman todas las partes de la transacción. Si cualquier parte de la transacción se indica en la primera fase que no se puede confirmar, no se produce la segunda fase. ODBC no es compatible con las confirmaciones en dos fases.  
  
 **Indicador de tipo**  
 Un valor entero pasa o devolver desde una función ODBC para indicar el tipo de datos de una variable de aplicación, un parámetro o una columna. ODBC define los indicadores de tipo para tipos de datos C y SQL.  
  
## <a name="v"></a>V  
 **view**  
 Una manera alternativa de mirar los datos en una o varias tablas. Normalmente, se crea una vista como un subconjunto de las columnas de una o varias tablas. En ODBC, las vistas son generalmente son equivalentes a las tablas.
