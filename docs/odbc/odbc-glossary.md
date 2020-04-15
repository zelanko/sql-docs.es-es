---
title: Glosario ODBC (ODBC Glossary) Microsoft Docs
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: ac454a8c57fe6e2f12724440dc37c3a1953e4c85
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/14/2020
ms.locfileid: "81302906"
---
# <a name="odbc-glossary"></a>Glosario de ODBC
## <a name="a"></a>Un  
 **plan de acceso**  
 Un plan generado por el motor de base de datos para ejecutar una instrucción SQL. Equivalente al código ejecutable compilado desde un lenguaje de tercera generación como C.  
  
 **función agregada**  
 Función que genera un único valor a partir de un grupo de valores, que a menudo se utiliza con las cláusulas **GROUP BY** y **HAVING.** Las funciones agregadas incluyen **AVG**, **COUNT**, **MAX**, **MIN**y **SUM**. También conocido como *funciones set*. *Véase también* función escalar.  
  
 **Ansi**  
 American National Standards Institute (Instituto Nacional de Normas De América). La API ODBC se basa en la interfaz de nivel de llamada ANSI.  
  
 **APD**  
 *Consulte* descriptor de parámetros de aplicación (APD).  
  
 **API**  
 Interfaz de programación de aplicaciones. Conjunto de rutinas que una aplicación utiliza para solicitar y llevar a cabo servicios de nivel inferior. La API ODBC se compone de las funciones ODBC.  
  
 **application**  
 Un programa ejecutable que llama a funciones en la API ODBC.  
  
 **descriptor de parámetros de aplicación (APD)**  
 Descriptor que describe los parámetros dinámicos utilizados en una instrucción SQL antes de cualquier conversión especificada por la aplicación.  
  
 **Descriptor de fila de aplicación (ARD)**  
 Descriptor que representa los metadatos de columna y los datos de los búferes de la aplicación, que describe una fila de datos después de cualquier conversión de datos especificada por la aplicación.  
  
 **Ard**  
 *Consulte* descriptor de fila de aplicación (ARD).  
  
 **modo de confirmación automática**  
 Modo de confirmación de transacción en el que las transacciones se confirman inmediatamente después de ejecutarse.  
  
## <a name="b"></a>B  
 **cambio de comportamiento**  
 Un cambio en cierta funcionalidad desde el comportamiento de ODBC *3.x* al comportamiento odbc *2.x,* o viceversa. Se produce al cambiar el atributo de entorno SQL_ATTR_ODBC_VERSION.  
  
 **Objeto binario grande (BLOB)**  
 Cualquier dato binario sobre un cierto número de bytes, como 255. Típicamente mucho más tiempo. Estos datos se envían y recuperan generalmente del origen de datos en partes. También conocido como *datos largos*.  
  
 **Vinculante**  
 Como verbo, el acto de asociar una columna en un conjunto de resultados o un parámetro en una instrucción SQL con una variable de aplicación. Como sustantivo, la asociación.  
  
 **desfase vinculante**  
 Valor añadido a las direcciones de búfer de datos y direcciones de búfer de longitud/indicador para todos los datos de columnas o parámetros enlazados, produciendo nuevas direcciones.  
  
 **cursor de bloque**  
 Un cursor capaz de capturar más de una fila de datos a la vez.  
  
 **Búfer**  
 Una parte de la memoria de la aplicación utilizada para pasar datos entre la aplicación y el controlador. Los búferes a menudo vienen en pares: un búfer de *datos* y un búfer de longitud de *datos.*  
  
 **byte**  
 Ocho bits o un octeto. *Véase también* octeto.  
  
## <a name="c"></a>C  
 **Tipo de datos C**  
 El tipo de datos de una variable en un programa C, en este caso la aplicación.  
  
 **Catálogo**  
 El conjunto de tablas del sistema en una base de datos que describe la forma de la base de datos. También conocido como *esquema* o diccionario de *datos.*  
  
 **función de catálogo**  
 Función ODBC utilizada para recuperar información del catálogo de la base de datos.  
  
 **CLI**  
 *Ver* Api.  
  
 **cliente/servidor**  
 Una estrategia de acceso a la base de datos en la que uno o varios clientes acceden a los datos a través de un servidor. Normalmente, los clientes implementan la interfaz de usuario mientras el servidor controla el acceso a la base de datos.  
  
 **Columna**  
 El contenedor de un único elemento de información en una fila. También conocido como *campo*.  
  
 **Cometer**  
 Para que los cambios en una transacción sean permanentes.  
  
 **Concurrencia**  
 La capacidad de más de una transacción para acceder a los mismos datos al mismo tiempo.  
  
 **nivel de conformidad**  
 Un conjunto discreto de funcionalidad compatible con un controlador o un origen de datos. ODBC define los niveles de conformidad de API y los niveles de conformidad de SQL.  
  
 **connection**  
 Una instancia concreta de un controlador y un origen de datos.  
  
 **navegación por conexiones**  
 Buscar en la red fuentes de datos a las que conectarse. La exploración de la conexión puede implicar varios pasos. Por ejemplo, el usuario puede examinar primero la red en busca de servidores y, a continuación, examinar una base de datos en un servidor determinado.  
  
 **manija de conexión**  
 Identificador de una estructura de datos que contiene información sobre una conexión.  
  
 **fila actual**  
 La fila a la que apunta actualmente el cursor. Las operaciones posicionadas actúan en la fila actual.  
  
 **Cursor**  
 Un software que devuelve filas de datos a la aplicación. Probablemente nombrado después del cursor parpadeante en un terminal de computadora; así como ese cursor indica la posición actual en la pantalla, un cursor en un conjunto de resultados indica la posición actual en el conjunto de resultados.  
  
## <a name="d"></a>D  
 **búfer de datos**  
 Un búfer utilizado para pasar datos. A menudo asociado a un búfer de datos es un búfer de longitud de *datos.*  
  
 **diccionario de datos**  
 *Consulte el* catálogo.  
  
 **búfer de longitud de datos**  
 Un búfer utilizado para pasar la longitud del valor en un búfer de *datos*correspondiente. El búfer de longitud de datos también se utiliza para almacenar indicadores, como si el valor de datos está terminado en null.  
  
 **fuente de datos**  
 Los datos a los que el usuario desea acceder y su sistema operativo asociado, DBMS y plataforma de red (si los hay).  
  
 **tipo de datos**  
 El tipo de un dato. ODBC define tipos de datos C y SQL. *Consulte también* el indicador de tipo.  
  
 **columna de datos en ejecución**  
 Columna para la que se envían datos después de llamar a **SQLSetPos.** Así se denomina porque los datos se envían en tiempo de ejecución en lugar de colocarse en un búfer de conjunto de filas. Los datos largos generalmente se envían en partes en tiempo de ejecución.  
  
 **parámetro de datos en ejecución**  
 Un parámetro para el que se envían datos después de **SQLExecute** o **SQLExecDirect** se llama. Así se denomina porque los datos se envían cuando se ejecuta la instrucción SQL en lugar de colocarse en un búfer de parámetros. Los datos largos generalmente se envían en partes en tiempo de ejecución.  
  
 **Base**  
 Una colección discreta de datos en un DBMS. También un DBMS.  
  
 **motor de base de datos**  
 El software de un DBMS que analiza y ejecuta instrucciones SQL y accede a los datos físicos.  
  
 **DBMS**  
 Sistema de gestión de bases de datos. Capa de software entre la base de datos física y el usuario. El sistema DBMS administra todo el acceso a la base de datos.  
  
 **Controlador basado en DBMS**  
 Controlador que tiene acceso a datos físicos a través de un motor de base de datos independiente.  
  
 **DDL**  
 Lenguaje de definición de datos. Esas instrucciones en SQL que definen, en lugar de manipular, datos. Por ejemplo, **CREATE TABLE**, **CREATE INDEX**, **GRANT**y **REVOKE**.  
  
 **identificador delimitado**  
 Identificador que se incluye en caracteres de comillas identificador para que pueda contener caracteres especiales o palabras clave de coincidencia (también conocido como identificador entre comillas).  
  
 **Descriptor**  
 Estructura de datos que contiene información sobre datos de columna o parámetros dinámicos. La representación física del descriptor no está definida; las aplicaciones obtienen acceso directo a un descriptor solo manipulando sus campos llamando a funciones ODBC con el identificador de descriptor.  
  
 **base de datos de escritorio**  
 Un DBMS diseñado para ejecutarse en un ordenador personal. Por lo general, estos DBMS no proporcionan un motor de base de datos independiente y se debe tener acceso a ellos a través de un controlador basado en archivos. Los motores de estos controladores generalmente han reducido la compatibilidad con SQL y las transacciones. Por ejemplo, dBASE, Paradox, Btrieve o Microsoft® FoxPro®.  
  
 **Diagnóstico**  
 Un registro que contiene información de diagnóstico sobre la última función llamada que utiliza un identificador determinado. Los registros de diagnóstico están asociados con identificadores de entorno, conexión, instrucción y descriptor.  
  
 **DML**  
 Lenguaje de manipulación de datos. Esas instrucciones en SQL que manipulan, en lugar de definir, datos. Por ejemplo, **INSERT**, **UPDATE**, **DELETE**y **SELECT**.  
  
 **Conductor**  
 Una biblioteca de rutina que expone las funciones de la API ODBC. Los controladores son específicos de un único DBMS.  
  
 **Administrador de controladores**  
 Una biblioteca de rutina que administra el acceso a los controladores de la aplicación. El Administrador de controladores carga y descarga (o se conecta a y se desconecta de) controladores y pasa las llamadas a las funciones ODBC al controlador correcto.  
  
 **DLL de configuración del controlador**  
 DLL que contiene funciones de instalación y configuración específicas del controlador.  
  
 **cursor dinámico**  
 Cursor desplazable capaz de detectar filas actualizadas, eliminadas o insertadas en el conjunto de resultados.  
  
 **SQL dinámico**  
 Tipo de SQL incrustado en el que se crean y compilan instrucciones SQL en tiempo de ejecución. *Consulte también* SQL estático.  
  
## <a name="e"></a>E  
 **SQL incrustado**  
 Las instrucciones SQL que se incluyen directamente en un programa escrito en otro idioma, como COBOL o C. ODBC no usa SQL incrustado. *Consulte también* SQL estático *y* SQL dinámico.  
  
 **Ambiente**  
 Un contexto global en el que acceder a los datos; asociado con el entorno es cualquier información de naturaleza global, como una lista de todas las conexiones en ese entorno.  
  
 **manija del medio ambiente**  
 Identificador de una estructura de datos que contiene información sobre el entorno.  
  
 **cláusula de escape**  
 Una cláusula en una instrucción SQL.  
  
 **Ejecutar**  
 Para ejecutar una instrucción SQL.  
  
## <a name="f"></a>F  
 **cursor de grasa**  
 *Consulte* el cursor de bloque.  
  
 **traer**  
 Para recuperar una o más filas de un conjunto de resultados.  
  
 **campo**  
 *Ver* columna.  
  
 **controlador basado en archivos**  
 Controlador que accede directamente a los datos físicos. En este caso, el controlador contiene un motor de base de datos y actúa como controlador y origen de datos.  
  
 **fuente de datos del archivo**  
 Origen de datos para el que la información de conexión se almacena en un archivo .dsn.  
  
 **clave externa**  
 Columna o columnas de una tabla que coinciden con la clave principal de otra tabla.  
  
 **cursor de solo avance**  
 Un cursor que solo puede avanzar a través del conjunto de resultados y, por lo general, recupera solo una fila a la vez. La mayoría de las bases de datos relacionales solo admiten cursores de solo avance.  
  
## <a name="h"></a>H  
 **Manejar**  
 Valor que identifica de forma única algo como un archivo o una estructura de datos. Las manijas son significativas sólo para el software que los crea y utiliza, pero son pasados por otro software para identificar cosas. ODBC define identificadores para entornos, conexiones, instrucciones y descriptores.  
  
## <a name="i"></a>I  
 **descriptor de parámetros de implementación (IPD)**  
 Descriptor que describe los parámetros dinámicos utilizados en una instrucción SQL después de cualquier conversión especificada por la aplicación.  
  
 **descriptor de fila de implementación (IRD)**  
 Descriptor que describe una fila de datos antes de cualquier conversión especificada por la aplicación.  
  
 **DLL del instalador**  
 DLL que instala componentes ODBC y configura orígenes de datos.  
  
 **Facilidad de mejora de la integridad**  
 Un subconjunto de SQL diseñado para mantener la integridad de una base de datos.  
  
 **nivel de conformidad de la interfaz**  
 El nivel de la interfaz ODBC 3.7 compatible con un controlador; puede ser Núcleo, Nivel 1 o Nivel 2.  
  
 **Interoperabilidad**  
 La capacidad de una aplicación para utilizar el mismo código al acceder a datos en diferentes DBMS.  
  
 **IPD**  
 *Ver* Descriptor de parámetros de implementación (IPD).  
  
 **Ird**  
 *Ver* Descriptor de fila de implementación (IRD).  
  
 **ISO/IEC**  
 Organización Internacional de Normas/Comisión Electrotécnica Internacional. La API ODBC se basa en la interfaz de nivel de llamada ISO/IEC.  
  
## <a name="j"></a>J  
 **join**  
 Una operación en una base de datos relacional que vincula las filas de dos o más tablas haciendo coincidir los valores de las columnas especificadas.  
  
## <a name="k"></a>K  
 **key**  
 Columna o columnas cuyos valores identifican una fila. *Consulte también* clave externa *y* clave principal.  
  
 **conjunto de claves**  
 Conjunto de claves utilizadas por un cursor mixto o controlado por conjunto de claves para volver a capturar filas.  
  
 **cursor controlado por conjunto de claves**  
 Cursor desplazable que detecta filas actualizadas y eliminadas mediante un conjunto de claves.  
  
## <a name="l"></a>L  
 **Literal**  
 Representación de caracteres de un valor de datos real en una instrucción SQL.  
  
 **Bloqueo**  
 Proceso mediante el cual un DBMS restringe el acceso a una fila en un entorno multiusuario. El DBMS normalmente establece un bit en una fila o la página física que contiene una fila que indica que la fila o página está bloqueada.  
  
 **datos largos**  
 Cualquier dato binario o de caracteres de una longitud determinada, como 255 bytes o caracteres. Típicamente mucho más tiempo. Estos datos se envían y recuperan generalmente del origen de datos en partes. También conocido como *BLOB*s o *CLOB*s.  
  
## <a name="m"></a>M  
 **fuente de datos de la máquina**  
 Origen de datos para el que se almacena información de conexión en el sistema (por ejemplo, el registro).  
  
 **modo de confirmación manual**  
 Modo de confirmación de transacciones en el que las transacciones deben confirmarse explícitamente llamando a **SQLTransact**.  
  
 **metadata**  
 Datos que describen un parámetro en una instrucción SQL o una columna de un conjunto de resultados. Por ejemplo, el tipo de datos, la longitud de bytes y la precisión de un parámetro.  
  
 **conductor de varios niveles**  
 *Ver* Controlador basado en DBMS.  
  
## <a name="n"></a>N  
 **Valor NULL**  
 No tener ningún valor asignado explícitamente. En particular, un valor NULL es diferente de un cero o un espacio en blanco.  
  
## <a name="o"></a>O  
 **Octeto**  
 Ocho bits o un byte. *Véase también* byte.  
  
 **longitud del octeto**  
 La longitud en octetos de un búfer o los datos que contiene.  
  
 **ODBC**  
 Abra Conectividad de base de datos. Especificación de una API que define un conjunto estándar de rutinas con las que una aplicación puede tener acceso a los datos de un origen de datos.  
  
 **Administrador ODBC**  
 Un programa ejecutable que llama al archivo DLL del instalador para configurar orígenes de datos.  
  
 Abrir grupo  
 Una empresa que publica estándares. En particular, publica los estándares de SQL Access Group (SAG).  
  
 **simultaneidad optimista**  
 Una estrategia para aumentar la simultaneidad en la que las filas no están bloqueadas. En su lugar, antes de que se actualicen o eliminen, un cursor comprueba si se han cambiado desde la última lectura. Si es así, se produce un error en la actualización o eliminación. *Consulte también* simultaneidad pesimista.  
  
 **combinación externa**  
 Combinación en la que se devuelven filas coincidentes y no coincidentes. Los valores de todas las columnas de la tabla no coincidente en filas no coincidentes se establecen en NULL.  
  
 **Propietario**  
 El dueño de una mesa.  
  
## <a name="p"></a>P  
 **Parámetro**  
 Variable en una instrucción SQL, marcada con un marcador de parámetro o un signo de interrogación (?). Los parámetros se enlazan a variables de aplicación y sus valores se recuperan cuando se ejecuta la instrucción.  
  
 **descriptor de parámetros**  
 Descriptor que describe los parámetros en tiempo de ejecución utilizados en una instrucción SQL, ya sea antes de cualquier conversión especificada por la aplicación (un descriptor de parámetro de aplicación o APD) o después de cualquier conversión especificada por la aplicación (un descriptor de parámetro de implementación o IPD).  
  
 **matriz de operaciones de parámetros**  
 Matriz que contiene valores que una aplicación puede establecer para indicar que el parámetro correspondiente debe omitirse en una operación **SQLExecDirect** o **SQLExecute.**  
  
 **matriz de estado de parámetros**  
 Matriz que contiene el estado de un parámetro después de una llamada a **SQLExecDirect** o **SQLExecute**.  
  
 **simultaneidad pesimista**  
 Una estrategia para implementar la serializabilidad, en la que las filas están bloqueadas para que otras transacciones no puedan cambiarlas. *Consulte también* simultaneidad optimista *y* serializabilidad.  
  
 **operación posicionada**  
 Cualquier operación que actúe en la fila actual. Por ejemplo, instrucciones de actualización y eliminación posicionadas, **SQLGetData**y **SQLSetPos**.  
  
 **declaración de actualización posicionada**  
 Una instrucción SQL utilizada para actualizar los valores de la fila actual.  
  
 **declaración de eliminación posicionada**  
 Una instrucción SQL utilizada para eliminar la fila actual.  
  
 **Preparar**  
 Para compilar una instrucción SQL. Un plan de acceso se crea mediante la preparación de una instrucción SQL.  
  
 **clave primaria**  
 Columna o columnas que identifican de forma única una fila de una tabla.  
  
 **Procedimiento**  
 Un grupo de una o más instrucciones SQL precompiladas que se almacenan como un objeto con nombre en una base de datos.  
  
 **columna de procedimiento**  
 Un argumento en una llamada a procedimiento, el valor devuelto por un procedimiento o una columna en un conjunto de resultados creado por un procedimiento.  
  
## <a name="q"></a>Q  
 **Calificador**  
 Una base de datos que contiene una o varias tablas.  
  
 **consulta**  
 Una instrucción SQL. A veces se utiliza para significar una instrucción **SELECT.**  
  
 **identificador citado**  
 Identificador que se incluye en caracteres de comillas identificador para que pueda contener caracteres especiales o coincidir con palabras clave (también conocido en SQL-92 como identificador delimitado).  
  
## <a name="r"></a>R  
 **Radix**  
 La base de un sistema numérico. Por lo general, 2 o 10.  
  
 **grabar**  
 *Ver* fila.  
  
 **conjunto de resultados**  
 El conjunto de filas creadas mediante la ejecución de una instrucción **SELECT.**  
  
 **código de retorno**  
 El valor devuelto por una función ODBC.  
  
 **revertir**  
 Para devolver los valores cambiados por una transacción a su estado original.  
  
 **Fila**  
 Conjunto de columnas relacionadas que describen una entidad específica. También conocido como *un registro*.  
  
 **descriptor de fila**  
 Descriptor que describe las columnas de un conjunto de resultados, ya sea antes de cualquier conversión especificada por la aplicación (un descriptor de fila de implementación o IRD) o después de cualquier conversión especificada por la aplicación (un descriptor de fila de aplicación o ARD).  
  
 **matriz de operaciones de fila**  
 Matriz que contiene valores que una aplicación puede establecer para indicar que se debe omitir la fila correspondiente en una operación **SQLSetPos.**  
  
 **matriz de estado de fila**  
 Matriz que contiene el estado de una fila después de una llamada a **SQLFetch**, **SQLFetchScroll**o **SQLSetPos**.  
  
 **Filas**  
 Conjunto de filas devueltos en una sola captura por un cursor de bloque.  
  
 **buffers de conjunto de filas**  
 Los búferes enlazados a las columnas de un conjunto de resultados y en los que se devuelven los datos de todo un conjunto de filas.  
  
## <a name="s"></a>S  
 **Sag**  
 *Ver* Grupo de acceso SQL (SAG).  
  
 **función escalar**  
 Función que genera un único valor a partir de un único valor. Por ejemplo, una función que cambia el caso de los datos de caracteres.  
  
 **Esquema**  
 *Consulte el* catálogo.  
  
 **cursor desplazable**  
 Un cursor que puede avanzar o retroceder por el conjunto de resultados.  
  
 **serializabilidad**  
 Si dos transacciones que se ejecutan simultáneamente producen un resultado que es el mismo que la ejecución en serie (o secuencial) de esas transacciones. Las transacciones serializables son necesarias para mantener la integridad de la base de datos.  
  
 **base de datos del servidor**  
 Un DBMS diseñado para ejecutarse en un entorno cliente/servidor. Estos DBMS proporcionan un motor de base de datos independiente que proporciona compatibilidad enriquecida para SQL y transacciones. Se accede a ellos a través de controladores basados en DBMS. Por ejemplo, Oracle, Informix, DB/2 o Microsoft® SQL Server.  
  
 **función de ajuste**  
 *Consulte la* función de agregado.  
  
 **DLL de configuración**  
 *Consulte* DLL de instalación del controlador *y* DLL de instalación del traductor.  
  
 **conductor de un solo nivel**  
 *Consulte* Controlador basado en archivos.  
  
 **SQL**  
 Lenguaje de consulta estructurado. Lenguaje utilizado por las bases de datos relacionales para consultar, actualizar y administrar datos.  
  
 **Grupo de acceso SQL (SAG)**  
 Un consorcio de empresas de la industria que se ocupan de los DBMS SQL. La interfaz de nivel de llamada del grupo abierto se basa en el trabajo realizado originalmente por el grupo de acceso SQL.  
  
 **Nivel de conformidad SQL**  
 El nivel de gramática SQL-92 compatible con un controlador; puede ser Entrada, FIPS Transición, Intermedio o Completo.  
  
 **Tipo de datos de SQL**  
 El tipo de datos de una columna o parámetro tal como se almacena en el origen de datos.  
  
 **SQLSTATE**  
 Un valor de cinco caracteres que indica un error determinado.  
  
 **Instrucción SQL**  
 Una frase completa en SQL que comienza con una palabra clave y describe completamente una acción que se va a realizar. Por ejemplo, SELECT * FROM Orders. Las instrucciones SQL no deben confundirse con instrucciones.  
  
 **state**  
 Una condición bien definida de un elemento. Por ejemplo, una conexión tiene siete estados, incluidos datos no asignados, asignados, conectados y que necesitan datos. Ciertas operaciones solo se pueden realizar cuando un elemento está en un estado determinado. Por ejemplo, una conexión solo se puede liberar cuando está en un estado asignado y no, por ejemplo, cuando está en un estado conectado.  
  
 **transición estatal**  
 El movimiento de un elemento de un estado a otro. ODBC define transiciones de estado rigurosas para entornos, conexiones e instrucciones.  
  
 **Declaración**  
 Contenedor para toda la información relacionada con una instrucción SQL. Las instrucciones no deben confundirse con instrucciones SQL.  
  
 **declaración manejar**  
 Identificador de una estructura de datos que contiene información sobre una instrucción.  
  
 **cursor estático**  
 Cursor desplazable que no puede detectar actualizaciones, eliminaciones o inserciones en el conjunto de resultados. Normalmente se implementa haciendo una copia del conjunto de resultados.  
  
 **SQL estático**  
 Tipo de SQL incrustado en el que las instrucciones SQL se codifican y compilan de forma rígida cuando se compila el resto del programa. *Consulte también* SQL dinámico.  
  
 **procedimiento almacenado**  
 *Véase el* procedimiento.  
  
## <a name="t"></a>T  
 **table**  
 Una colección de filas.  
  
 **thunking**  
 La conversión de direcciones de 16 bits a direcciones de 32 bits, o viceversa, cuando se utilizan aplicaciones de 16 bits con controladores ODBC de 32 bits.  
  
 **Transacción**  
 Unidad atómica de trabajo. El trabajo de una transacción debe completarse como un todo; si se produce un error en cualquier parte de la transacción, no se puede realizar la transacción.  
  
 **aislamiento de transacciones**  
 El acto de aislar una transacción de los efectos de todas las demás transacciones.  
  
 **nivel de aislamiento de transacciones**  
 Una medida de lo bien que se aísla una transacción. Hay cinco niveles de aislamiento de transacción: lectura no confirmada, lectura confirmada, lectura repetible, serializable y control de versiones.  
  
 **DLL traductor**  
 DLL que se usa para traducir datos de un juego de caracteres a otro.  
  
 **DLL de configuración del traductor**  
 DLL que contiene funciones de instalación y configuración específicas del traductor.  
  
 **confirmación en dos fases**  
 El proceso de confirmación de una transacción distribuida en dos fases. En la primera fase, el procesador de transacciones comprueba que se pueden confirmar todas las partes de la transacción. En la segunda fase, se confirman todas las partes de la transacción. Si alguna parte de la transacción indica en la primera fase que no se puede confirmar, no se produce la segunda fase. ODBC no admite confirmaciones de dos fases.  
  
 **indicador de tipo**  
 Un valor entero pasado o devuelto desde una función ODBC para indicar el tipo de datos de una variable de aplicación, un parámetro o una columna. ODBC define indicadores de tipo para los tipos de datos C y SQL.  
  
## <a name="v"></a>V  
 **Vista**  
 Una forma alternativa de ver los datos en una o más tablas. Normalmente, una vista se crea como un subconjunto de las columnas de una o varias tablas. En ODBC, las vistas suelen ser equivalentes a las tablas.
