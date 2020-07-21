---
title: Glosario de ODBC | Microsoft Docs
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
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/27/2020
ms.locfileid: "81302906"
---
# <a name="odbc-glossary"></a>Glosario de ODBC
## <a name="a"></a>Un  
 **Plan de acceso**  
 Un plan generado por el motor de base de datos para ejecutar una instrucción SQL. Equivalente al código ejecutable compilado a partir de un lenguaje de tercera generación como C.  
  
 **función de agregado**  
 Función que genera un único valor a partir de un grupo de valores, que a menudo se usa con cláusulas **Group by** y **having** . Las funciones de agregado incluyen **AVG**, **Count**, **Max**, **min**y **SUM**. También conocido como *funciones de conjunto*. *Vea también* función escalar.  
  
 **ANSI**  
 American National Standards Institute. La API de ODBC se basa en la interfaz de nivel de llamada ANSI.  
  
 **APD**  
 *Consulte* descriptor de parámetros de la aplicación (APD).  
  
 **API**  
 Interfaz de programación de aplicaciones. Conjunto de rutinas que una aplicación usa para solicitar y llevar a cabo servicios de nivel inferior. La API de ODBC se compone de las funciones de ODBC.  
  
 **application**  
 Programa ejecutable que llama a funciones de la API de ODBC.  
  
 **descriptor de parámetros de aplicación (APD)**  
 Descriptor que describe los parámetros dinámicos que se usan en una instrucción SQL antes de cualquier conversión especificada por la aplicación.  
  
 **descriptor de fila de aplicación (ARD)**  
 Descriptor que representa los metadatos y los datos de la columna en los búferes de la aplicación, que describe una fila de datos después de cualquier conversión de datos especificada por la aplicación.  
  
 **ARD**  
 *Consulte* descriptor de fila de la aplicación (ARD).  
  
 **modo de confirmación automática**  
 Modo de confirmación de transacción en el que las transacciones se confirman inmediatamente después de ejecutarse.  
  
## <a name="b"></a>B  
 **cambio de comportamiento**  
 Cambio en cierta funcionalidad del comportamiento de ODBC *3. x* al comportamiento de ODBC *2. x* , o viceversa. Se produce al cambiar el atributo de entorno SQL_ATTR_ODBC_VERSION.  
  
 **Objeto binario grande (BLOB)**  
 Cualquier dato binario a través de un número determinado de bytes, como 255. Normalmente es mucho más largo. Normalmente, estos datos se envían al origen de datos y se recuperan del mismo en partes. También se conoce como *datos largos*.  
  
 **enlace**  
 Como verbo, la acción de asociar una columna en un conjunto de resultados o un parámetro en una instrucción SQL con una variable de aplicación. Como sustantivo, la asociación.  
  
 **desplazamiento de enlace**  
 Un valor agregado a las direcciones del búfer de datos y las direcciones de búfer de indicador/longitud para todos los datos de parámetros o columnas enlazados, lo que produce nuevas direcciones.  
  
 **cursor de bloque**  
 Cursor capaz de capturar más de una fila de datos a la vez.  
  
 **búfer**  
 Parte de la memoria de la aplicación que se usa para pasar datos entre la aplicación y el controlador. Los búferes suelen entrar en pares: un *búfer de datos* y un búfer de longitud de *datos*.  
  
 **byte**  
 Ocho bits o un octeto. *Vea también* octeto.  
  
## <a name="c"></a>C  
 **Tipo de datos C**  
 El tipo de datos de una variable en un programa de C, en este caso la aplicación.  
  
 **Catálogo**  
 Conjunto de tablas del sistema en una base de datos que describen la forma de la base de datos. También se conoce como Diccionario de *datos*o *esquema* .  
  
 **función de catálogo**  
 Función ODBC que se usa para recuperar información del catálogo de la base de datos.  
  
 **CLI**  
 *Vea* API.  
  
 **cliente/servidor**  
 Una estrategia de acceso a bases de datos en la que uno o más clientes tienen acceso a los datos a través de un servidor. Normalmente, los clientes implementan la interfaz de usuario mientras el servidor controla el acceso a la base de datos.  
  
 **artículo**  
 Contenedor para un único elemento de información de una fila. También conocido como *campo*.  
  
 **promete**  
 Para que los cambios en una transacción sean permanentes.  
  
 **concurrency**  
 La capacidad de más de una transacción para tener acceso a los mismos datos al mismo tiempo.  
  
 **nivel de conformidad**  
 Conjunto discreto de funcionalidad que admite un controlador o un origen de datos. ODBC define los niveles de cumplimiento de API y los niveles de cumplimiento de SQL.  
  
 **connection**  
 Una instancia concreta de un controlador y un origen de datos.  
  
 **exploración de conexiones**  
 Buscar en la red los orígenes de datos a los que conectarse. La exploración de la conexión puede implicar varios pasos. Por ejemplo, el usuario podría examinar primero la red en busca de servidores y, a continuación, examinar un servidor determinado para obtener una base de datos.  
  
 **identificador de conexión**  
 Identificador de una estructura de datos que contiene información sobre una conexión.  
  
 **fila actual**  
 Fila a la que apunta actualmente el cursor. Las operaciones posicionadas actúan sobre la fila actual.  
  
 **cursor**  
 Parte de software que devuelve filas de datos a la aplicación. Probablemente se nombra después del cursor que parpadea en un terminal de equipo; del mismo modo que ese cursor indica la posición actual en la pantalla, un cursor en un conjunto de resultados indica la posición actual en el conjunto de resultados.  
  
## <a name="d"></a>D  
 **búfer de datos**  
 Búfer que se usa para pasar datos. A menudo, se asocia a un búfer de datos como *búfer de longitud de datos*.  
  
 **diccionario de datos**  
 *Vea* catálogo.  
  
 **búfer de longitud de datos**  
 Búfer que se usa para pasar la longitud del valor en un *búfer de datos*correspondiente. El búfer de longitud de datos también se usa para almacenar indicadores, por ejemplo, si el valor de los datos está terminado en NULL.  
  
 **origen de datos**  
 Los datos a los que el usuario desea acceder y su sistema operativo asociado, DBMS y plataforma de red (si existen).  
  
 **tipo de datos**  
 Tipo de un fragmento de datos. ODBC define los tipos de datos de C y SQL. *Vea también* indicador de tipo.  
  
 **columna datos en ejecución**  
 Columna para la que se envían los datos después de que se llame a **SQLSetPos** . Con el nombre, dado que los datos se envían en tiempo de ejecución en lugar de colocarse en un búfer de conjunto de filas. Normalmente, los datos largos se envían en partes en tiempo de ejecución.  
  
 **parámetro de datos en ejecución**  
 Parámetro para el que se envían los datos después de llamar a **SQLExecute** o **SQLExecDirect** . Con el nombre, dado que los datos se envían cuando se ejecuta la instrucción SQL en lugar de colocarse en un búfer de parámetros. Normalmente, los datos largos se envían en partes en tiempo de ejecución.  
  
 **database**  
 Colección discreta de datos en un DBMS. También un DBMS.  
  
 **motor de base de datos**  
 El software de un DBMS que analiza y ejecuta instrucciones SQL y tiene acceso a los datos físicos.  
  
 **DBMS**  
 Sistema de administración de bases de datos. Capa de software entre la base de datos física y el usuario. El sistema DBMS administra todo el acceso a la base de datos.  
  
 **Controlador basado en DBMS**  
 Un controlador que tiene acceso a datos físicos a través de un motor de base de datos independiente.  
  
 **DDL**  
 Lenguaje de definición de datos. Las instrucciones de SQL que definen, en lugar de manipular los datos. Por ejemplo, **CREATE TABLE**, **Create index**, **Grant**y **REVOKE**.  
  
 **identificador delimitado**  
 Identificador que se incluye entre comillas de identificador para que pueda contener caracteres especiales o palabras clave coincidentes (también conocido como identificador entre comillas).  
  
 **scripto**  
 Una estructura de datos que contiene información sobre los datos de columna o los parámetros dinámicos. No se ha definido la representación física del descriptor; las aplicaciones obtienen acceso directo a un descriptor solo manipulando sus campos mediante una llamada a las funciones ODBC con el identificador del descriptor.  
  
 **base de datos de escritorio**  
 DBMS diseñado para ejecutarse en un equipo personal. Por lo general, estos DBMS no proporcionan un motor de base de datos independiente y se debe tener acceso a él a través de un controlador basado en archivos. Los motores de estos controladores suelen tener una compatibilidad reducida para SQL y las transacciones. Por ejemplo, dBASE, Paradox, Btrieve o Microsoft® FoxPro®.  
  
 **diagnóstico**  
 Un registro que contiene información de diagnóstico sobre la última función denominada que usó un identificador determinado. Los registros de diagnóstico se asocian con el entorno, la conexión, la instrucción y los identificadores de descriptor.  
  
 **DML**  
 Lenguaje de manipulación de datos. Las instrucciones de SQL que manipulan los datos, en lugar de definirlos. Por ejemplo, **Insert**, **Update**, **Delete**y **Select**.  
  
 **dispositivo**  
 Biblioteca de rutina que expone las funciones de la API de ODBC. Los controladores son específicos de un solo DBMS.  
  
 **Administrador de controladores**  
 Biblioteca de rutina que administra el acceso a los controladores de la aplicación. El administrador de controladores carga y descarga (o se conecta y desconecta de) los controladores y pasa las llamadas a las funciones ODBC al controlador correcto.  
  
 **DLL de instalación del controlador**  
 Un archivo DLL que contiene funciones de instalación y configuración específicas del controlador.  
  
 **cursor dinámico**  
 Cursor desplazable capaz de detectar filas actualizadas, eliminadas o insertadas en el conjunto de resultados.  
  
 **SQL dinámico**  
 Tipo de SQL incrustado en el que se crean y compilan instrucciones SQL en tiempo de ejecución. *Vea también* SQL estático.  
  
## <a name="e"></a>E  
 **SQL incrustado**  
 Las instrucciones SQL que se incluyen directamente en un programa escrito en otro lenguaje, como COBOL o C. ODBC, no usan SQL incrustado. *Vea también* SQL estático *y* SQL dinámico.  
  
 **environment**  
 Contexto global en el que se va a obtener acceso a los datos; asociado con el entorno de es cualquier información global por naturaleza, como una lista de todas las conexiones en ese entorno.  
  
 **identificador de entorno**  
 Identificador de una estructura de datos que contiene información sobre el entorno.  
  
 **escape (cláusula)**  
 Una cláusula en una instrucción SQL.  
  
 **ejecut**  
 Para ejecutar una instrucción SQL.  
  
## <a name="f"></a>F  
 **cursor de Fat**  
 *Vea* cursor de bloque.  
  
 **recopila**  
 Para recuperar una o más filas de un conjunto de resultados.  
  
 **campo**  
 *Vea* la columna.  
  
 **controlador basado en archivos**  
 Un controlador que tiene acceso a los datos físicos directamente. En este caso, el controlador contiene un motor de base de datos y actúa como el controlador y el origen de datos.  
  
 **origen de datos de archivo**  
 Origen de datos para el que se almacena la información de conexión en un archivo. DSN.  
  
 **clave externa**  
 Columna o columnas de una tabla que coinciden con la clave principal de otra tabla.  
  
 **cursor de solo avance**  
 Cursor que solo puede avanzar por el conjunto de resultados y, generalmente, captura una fila cada vez. La mayoría de las bases de datos relacionales solo admiten cursores de solo avance.  
  
## <a name="h"></a>H  
 **asa**  
 Valor que identifica de forma única algo como un archivo o una estructura de datos. Los identificadores solo son significativos para el software que crea y utiliza, pero que son transmitidos por otro software para identificar cosas. ODBC define los identificadores de los entornos, las conexiones, las instrucciones y los descriptores.  
  
## <a name="i"></a>I  
 **descriptor de parámetros de implementación (IPD)**  
 Descriptor que describe los parámetros dinámicos que se usan en una instrucción SQL después de cualquier conversión especificada por la aplicación.  
  
 **descriptor de fila de implementación (IRD)**  
 Descriptor que describe una fila de datos antes de cualquier conversión especificada por la aplicación.  
  
 **DLL del instalador**  
 DLL que instala componentes ODBC y configura orígenes de datos.  
  
 **Instalación de la mejora de integridad**  
 Un subconjunto de SQL diseñado para mantener la integridad de una base de datos.  
  
 **nivel de conformidad de la interfaz**  
 El nivel de la interfaz ODBC 3,7 compatible con un controlador; puede ser núcleo, nivel 1 o nivel 2.  
  
 **interoperabilidad**  
 La capacidad de una aplicación de utilizar el mismo código al tener acceso a los datos de distintos DBMS.  
  
 **IPD**  
 *Vea* Descriptor de parámetros de implementación (IPD).  
  
 **IRD**  
 *Vea* Descriptor de fila de implementación (IRD).  
  
 **ISO/IEC**  
 International Standards Organization/Comisión electrotécnica internacional (CEI). La API de ODBC se basa en la interfaz de nivel de llamada ISO/IEC.  
  
## <a name="j"></a>J  
 **join**  
 Operación en una base de datos relacional que vincula las filas de dos o más tablas coincidentes con los valores de las columnas especificadas.  
  
## <a name="k"></a>K  
 **key**  
 Columna o columnas cuyos valores identifican una fila. *Vea también* clave externa *y* clave principal.  
  
 **curso**  
 Conjunto de claves utilizado por un cursor mixto o controlado por conjunto de claves para volver a capturar filas.  
  
 **cursor controlado por conjunto de claves**  
 Cursor desplazable que detecta filas actualizadas y eliminadas mediante un conjunto de claves.  
  
## <a name="l"></a>L  
 **literal**  
 Representación de caracteres de un valor de datos real en una instrucción SQL.  
  
 **tienda**  
 Proceso por el que un DBMS restringe el acceso a una fila en un entorno multiusuario. El DBMS normalmente establece un bit en una fila o en la página física que contiene una fila que indica que la fila o la página está bloqueada.  
  
 **datos largos**  
 Cualquier dato binario o de caracteres sobre una longitud determinada, como 255 bytes o caracteres. Normalmente es mucho más largo. Normalmente, estos datos se envían al origen de datos y se recuperan del mismo en partes. También conocido como *BLOB*s o *CLOB*s.  
  
## <a name="m"></a>M  
 **origen de datos de la máquina**  
 Origen de datos para el que se almacena la información de conexión en el sistema (por ejemplo, el registro).  
  
 **modo de confirmación manual**  
 Modo de confirmación de transacción en el que las transacciones se deben confirmar explícitamente mediante una llamada a **SQLTransact**.  
  
 **metadata**  
 Datos que describen un parámetro en una instrucción SQL o en una columna de un conjunto de resultados. Por ejemplo, el tipo de datos, la longitud de bytes y la precisión de un parámetro.  
  
 **controlador de varios niveles**  
 *Vea* Controlador basado en DBMS.  
  
## <a name="n"></a>N  
 **Valor NULL**  
 No tener ningún valor asignado explícitamente. En concreto, un valor NULL es diferente de un cero o un espacio en blanco.  
  
## <a name="o"></a>O  
 **altos**  
 Ocho bits o un byte. *Vea también* byte.  
  
 **longitud de octeto**  
 La longitud en octetos de un búfer o los datos que contiene.  
  
 **ODBC**  
 Abra conectividad de base de datos. Especificación de una API que define un conjunto estándar de rutinas con las que una aplicación puede obtener acceso a los datos de un origen de datos.  
  
 **Administrador de ODBC**  
 Un programa ejecutable que llama al archivo DLL del instalador para configurar los orígenes de datos.  
  
 Abrir grupo  
 Una empresa que publica estándares. En concreto, publica los estándares del grupo de acceso de SQL (SAG).  
  
 **simultaneidad optimista**  
 Estrategia para aumentar la simultaneidad en la que no se bloquean las filas. En su lugar, antes de que se actualicen o eliminen, un cursor comprueba si se han cambiado desde la última vez que se leyeron. Si es así, se produce un error en la actualización o la eliminación. *Vea también* simultaneidad pesimista.  
  
 **combinación externa**  
 Combinación en la que se devuelven las filas coincidentes y las no coincidentes. Los valores de todas las columnas de la tabla no coincidentes en filas no coincidentes se establecen en NULL.  
  
 **propietario**  
 Propietario de una tabla.  
  
## <a name="p"></a>P  
 **parámetro**  
 Una variable en una instrucción SQL, marcada con un marcador de parámetro o un signo de interrogación (?). Los parámetros se enlazan a las variables de la aplicación y sus valores recuperados cuando se ejecuta la instrucción.  
  
 **descriptor de parámetros**  
 Descriptor que describe los parámetros en tiempo de ejecución que se usan en una instrucción SQL, antes de cualquier conversión especificada por la aplicación (un descriptor de parámetros de la aplicación o APD) o después de cualquier conversión especificada por la aplicación (un descriptor de parámetro de implementación o IPD).  
  
 **matriz de operaciones de parámetros**  
 Una matriz que contiene valores que una aplicación puede establecer para indicar que el parámetro correspondiente se debe omitir en una operación **SQLExecDirect** o **SQLExecute** .  
  
 **matriz de estado de parámetro**  
 Una matriz que contiene el estado de un parámetro después de una llamada a **SQLExecDirect** o **SQLExecute**.  
  
 **simultaneidad pesimista**  
 Estrategia para implementar la serialización, en la que las filas están bloqueadas para que otras transacciones no puedan cambiarlas. *Vea también* simultaneidad optimista *y* serialización.  
  
 **operación posicionada**  
 Cualquier operación que actúe en la fila actual. Por ejemplo, instrucciones Update y DELETE posicionadas, **SQLGetData**y **SQLSetPos**.  
  
 **instrucción UPDATE posicionada**  
 Instrucción SQL que se usa para actualizar los valores de la fila actual.  
  
 **instrucción Delete posicionada**  
 Instrucción SQL que se usa para eliminar la fila actual.  
  
 **prepara**  
 Para compilar una instrucción SQL. Un plan de acceso se crea mediante la preparación de una instrucción SQL.  
  
 **clave principal**  
 Columna o columnas que identifican de forma única una fila de una tabla.  
  
 **pasos**  
 Grupo de una o varias instrucciones SQL precompiladas que se almacenan como un objeto con nombre en una base de datos.  
  
 **columna de procedimientos**  
 Un argumento en una llamada a procedimiento, el valor devuelto por un procedimiento o una columna en un conjunto de resultados creado por un procedimiento.  
  
## <a name="q"></a>Q  
 **calificador**  
 Base de datos que contiene una o más tablas.  
  
 **consulta**  
 Instrucción SQL. A veces se usa para referirse a una instrucción **Select** .  
  
 **identificador entre comillas**  
 Identificador que se incluye entre comillas de identificador para que pueda contener caracteres especiales o palabras clave coincidentes (también conocido en SQL-92 como identificador delimitado).  
  
## <a name="r"></a>R  
 **fijo**  
 Base de un sistema numérico. Normalmente 2 o 10.  
  
 **Record**  
 *Vea* la fila.  
  
 **conjunto de resultados**  
 Conjunto de filas creado mediante la ejecución de una instrucción **Select** .  
  
 **código de retorno**  
 El valor devuelto por una función ODBC.  
  
 **revertir**  
 Para devolver los valores modificados por una transacción a su estado original.  
  
 **columna**  
 Un conjunto de columnas relacionadas que describen una entidad específica. También se conoce como *registro*.  
  
 **descriptor de filas**  
 Descriptor que describe las columnas de un conjunto de resultados, antes de cualquier conversión especificada por la aplicación (un descriptor de fila de implementación o IRD) o después de cualquier conversión especificada por la aplicación (un descriptor de fila de la aplicación o ARD).  
  
 **matriz de operación de fila**  
 Una matriz que contiene valores que una aplicación puede establecer para indicar que la fila correspondiente se debe omitir en una operación **SQLSetPos** .  
  
 **matriz de estado de fila**  
 Una matriz que contiene el estado de una fila después de una llamada a **SQLFetch**, **SQLFetchScroll**o **SQLSetPos**.  
  
 **MultiRow**  
 Conjunto de filas devueltas en una captura única por un cursor de bloque.  
  
 **búferes de conjunto de filas**  
 Los búferes enlazados a las columnas de un conjunto de resultados y en el que se devuelven los datos de un conjunto de filas completo.  
  
## <a name="s"></a>S  
 **SAG**  
 *Vea* Grupo de acceso de SQL (SAG).  
  
 **función escalar**  
 Función que genera un valor único a partir de un valor único. Por ejemplo, una función que cambia las mayúsculas y minúsculas de los datos de caracteres.  
  
 **esquema**  
 *Vea* catálogo.  
  
 **cursor desplazable**  
 Cursor que puede moverse hacia delante o hacia atrás por el conjunto de resultados.  
  
 **seriabilidad**  
 Si dos transacciones que se ejecutan simultáneamente producen un resultado que es igual que la ejecución en serie (o secuencial) de esas transacciones. Las transacciones serializables son necesarias para mantener la integridad de la base de datos.  
  
 **base de datos del servidor**  
 DBMS diseñado para ejecutarse en un entorno cliente/servidor. Estos DBMS proporcionan un motor de base de datos independiente que proporciona una amplia compatibilidad con SQL y transacciones. Se obtiene acceso a ellos a través de controladores basados en DBMS. Por ejemplo, Oracle, Informix, DB/2 o Microsoft® SQL Server.  
  
 **Set (función)**  
 *Vea* función de agregado.  
  
 **DLL de instalación**  
 *Consulte* dll de instalación del controlador *y dll de* instalación del traductor.  
  
 **controlador de un solo nivel**  
 *Consulte* controlador basado en archivos.  
  
 **SQL**  
 Lenguaje de consulta estructurado. Lenguaje utilizado por las bases de datos relacionales para consultar, actualizar y administrar datos.  
  
 **Grupo de acceso de SQL (SAG)**  
 Un consorcio del sector de empresas preocupadas por DBMS de SQL. La interfaz de nivel de llamada del grupo abierto se basa en el trabajo realizado originalmente por el grupo de acceso de SQL.  
  
 **Nivel de conformidad de SQL**  
 El nivel de gramática SQL-92 compatible con un controlador; puede ser entrada, transitorio de FIPS, intermedio o completa.  
  
 **Tipo de datos SQL**  
 El tipo de datos de una columna o parámetro tal y como se almacena en el origen de datos.  
  
 **SQLSTATE**  
 Un valor de cinco caracteres que indica un error determinado.  
  
 **Instrucción SQL**  
 Una frase completa en SQL que comienza con una palabra clave y describe por completo una acción que se va a realizar. Por ejemplo, SELECT * FROM Orders. Las instrucciones SQL no se deben confundir con las instrucciones.  
  
 **state**  
 Condición bien definida de un elemento. Por ejemplo, una conexión tiene siete Estados, como sin asignar, asignado, conectado y que necesita datos. Ciertas operaciones solo se pueden realizar cuando un elemento se encuentra en un estado determinado. Por ejemplo, una conexión solo se puede liberar cuando está en un estado asignado y no, por ejemplo, cuando está en estado conectado.  
  
 **transición de estado**  
 Movimiento de un elemento de un estado a otro. ODBC define transiciones de estado rigurosas para entornos, conexiones e instrucciones.  
  
 **privacidad**  
 Contenedor para toda la información relacionada con una instrucción SQL. Las instrucciones no se deben confundir con las instrucciones SQL.  
  
 **identificador de instrucción**  
 Identificador de una estructura de datos que contiene información sobre una instrucción.  
  
 **cursor estático**  
 Cursor desplazable que no puede detectar actualizaciones, eliminaciones o inserciones en el conjunto de resultados. Normalmente se implementa mediante la realización de una copia del conjunto de resultados.  
  
 **SQL estático**  
 Tipo de SQL incrustado en el que las instrucciones SQL están codificadas de forma rígida y se compilan cuando se compila el resto del programa. *Vea también* SQL dinámico.  
  
 **procedimiento almacenado**  
 *Vea* el procedimiento.  
  
## <a name="t"></a>T  
 **table**  
 Colección de filas.  
  
 **procesadores**  
 Conversión de direcciones de 16 bits a direcciones de 32 bits, o viceversa, cuando las aplicaciones de 16 bits se utilizan con controladores ODBC de 32 bits.  
  
 **transacción**  
 Unidad atómica de trabajo. El trabajo de una transacción debe completarse como un todo; si se produce un error en cualquier parte de la transacción, no se puede realizar la transacción.  
  
 **aislamiento de transacción**  
 Acto de aislar una transacción de los efectos de todas las demás transacciones.  
  
 **nivel de aislamiento de transacción**  
 Medida del grado de aislamiento de una transacción. Hay cinco niveles de aislamiento de transacción: lectura no confirmada, lectura confirmada, lectura repetible, Serializable y control de versiones.  
  
 **archivo DLL de traductor**  
 DLL que se usa para convertir datos de un juego de caracteres a otro.  
  
 **DLL de instalación de Translator**  
 Un archivo DLL que contiene funciones de instalación y configuración específicas del traductor.  
  
 **confirmación en dos fases**  
 Proceso de confirmación de una transacción distribuida en dos fases. En la primera fase, el procesador de transacciones comprueba que se pueden confirmar todas las partes de la transacción. En la segunda fase, se confirman todas las partes de la transacción. Si alguna parte de la transacción indica en la primera fase que no se puede confirmar, no se produce la segunda fase. ODBC no admite confirmaciones en dos fases.  
  
 **indicador de tipo**  
 Valor entero que se pasa a una función ODBC o que se devuelve desde ella para indicar el tipo de datos de una variable de aplicación, un parámetro o una columna. ODBC define indicadores de tipo para tipos de datos de C y SQL.  
  
## <a name="v"></a>V  
 **Visores**  
 Una manera alternativa de ver los datos de una o varias tablas. Una vista se crea normalmente como un subconjunto de las columnas de una o varias tablas. En ODBC, las vistas suelen ser equivalentes a las tablas.
