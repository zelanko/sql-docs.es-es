---
title: Glosario de ADO | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- ADO, glossary
ms.assetid: b0478836-4123-4357-969a-c5784fc28be5
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 1af86e92d689f262833e1bc00d8caf0fb0c78b39
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "66709977"
---
# <a name="ado-glossary"></a>Glosario de términos de ADO
En este tema se define términos relacionados con ADO.  
  
## <a name="a"></a>A  
 dirección URL absoluta  
 Una dirección URL completa que especifica la ubicación de un recurso que se encuentra en Internet o una intranet. Vea también *URL* y *dirección URL relativa*.  
  
 Control ActiveX  
 Registrar automáticamente, en proceso componente COM que a menudo tiene un elemento visual en tiempo de diseño o tiempo de ejecución. Controles ActiveX también tienen la capacidad de comunicarse con un contenedor de documentos activos, como Microsoft Internet Explorer.  
  
 ADISAPI (Opciones avanzadas de interfaz de programación de aplicaciones de servidor de Internet de datos)  
 Una DLL ISAPI que proporciona funciones de análisis, control de automatización, el cálculo de referencias de conjunto de registros y empaquetado MIME. El componente ADISAPI funciona a través de la API proporcionada por Internet Information Services (IIS). Vea también *ISAPI*.  
  
 función de agregado  
 En una consulta, una función como COUNT, AVG o STDEV que calcula un valor con todas las filas de la columna de una tabla. En la escritura de expresiones y en la programación, puede usar las funciones de agregado de SQL (incluidas las tres mencionadas anteriormente) y las funciones de agregado de dominio para determinar varias estadísticas.  
  
 alias  
 Un nombre alternativo que asigne a una columna o expresión en una instrucción SELECT de SQL, a menudo más corta o más significativa. Por ejemplo, VentasPilar es un alias en la siguiente instrucción SELECT: "Select ventas-wr as VentasPilar from SalesDB". Un alias puede usarse para asignar columnas dinámicamente a los enlaces de control en el objeto DataControl.  
  
 subprocesamiento de apartamentos  
 Un modelo de subprocesos COM donde se producen todas las llamadas a un objeto en un subproceso. En el apartamento de subproceso, COM sincroniza y calcula las referencias de llamadas. Vea también *COMmddefcom*.  
  
 operación asincrónica  
 Una operación que devuelva el control al programa que realiza la llamada sin esperar a que se complete la operación. Antes de la operación se complete, continúa la ejecución de código. Vea también *operación sincrónica*.  
  
## <a name="b"></a>B  
 entrada de enlace  
 Una asignación entre un campo en una tabla y una variable. En las extensiones ADO de Visual C++, **Recordset** campos se asignan a variables de C o C++.  
  
 Máscara de bits  
 Un valor numérico destinado a una comparación de valores de bit a bit con otros valores numéricos, normalmente para marcar las opciones en parámetros o valores devueltos. Normalmente, esta comparación se realiza con operadores lógicos bit a bit, como **y** y **o** en Visual Basic, **&** y **&#124;** en C++.  
  
 Por ejemplo, el ADO **FieldAttributeEnum** valores pueden utilizarse como máscaras de bits para determinar los atributos de un campo. Suponga que desea determinar si un campo se puede actualizar. Puede comprobar con la siguiente expresión en Visual Basic:`Field.Attributes AND adFldUpdatable`  
  
 Si el resultado es TRUE, el campo es actualizable.  
  
 marcador  
 Un marcador que identifica de forma única una fila dentro de un conjunto de filas para que un usuario puede navegar rápidamente a ella.  
  
 objeto de negocios  
 Un objeto que realiza un conjunto definido de operaciones, como lógica de regla de negocios o validación de datos. Objetos de negocios residen normalmente en el nivel intermedio.  
  
 regla de negocios  
 La combinación de ediciones de validación, comprobaciones de inicio de sesión, las búsquedas de la base de datos, las directivas y transformaciones algorítmicas que constituyen la forma de una empresa de hacer negocios. También se denomina *lógica de negocios*.  
  
## <a name="c"></a>C  
 Expresión calculada  
 Una expresión que no es constante, pero cuyo valor depende de otros valores. Para la evaluación, una expresión calculada debe obtener y calcular valores de otros orígenes, normalmente en otros campos o filas.  
  
 Capítulo  
 Una referencia a un rango de filas desde un origen de datos. En ADO, un capítulo suele ser una referencia a otro **Recordset**.  
  
 Columnas de capítulo permiten definir una *elementos primarios y secundarios* relación donde la *primario* es el **Recordset** que contiene la columna de capítulo y el  *secundarios* es el **Recordset** representado por el capítulo.  
  
 chapter-alias  
 Un alias que hace referencia a la columna anexada al elemento primario.  
  
 juego de caracteres  
 Una asignación de un juego de caracteres y sus valores numéricos. Por ejemplo, Unicode es un carácter de 16 bits establece capaz de codificar todos los caracteres conocidos y usar como un estándar de codificación de caracteres en todo el mundo.  
  
 child  
 El lado dependiente de una relación jerárquica. Un elemento secundario es un nodo en una estructura jerárquica que tiene otro nodo por encima de él (más cercana a la raíz). Vea también *alias secundario*, *relación primario-secundario*, *primario*.  
  
 alias de elemento secundario  
 Un alias que hace referencia al elemento secundario. Vea también *alias*, *secundarios*.  
  
 CLSID (identificador de clase)  
 Un identificador único universal (UUID) que identifica un componente COM. Cada componente COM tiene su CLSID en el registro de Windows para que se puede cargar por otras aplicaciones. Vea también *ProgID*, *COM*.  
  
 nivel de cliente  
 Una capa lógica de un sistema distribuido que normalmente presenta datos y procesos de entrada del usuario, a veces se denomina el *front-end*. Normalmente, el nivel de cliente solicita datos desde un servidor basado en la entrada y, a continuación, se da formato y muestra el resultado. Vea también *nivel intermedio*, *capa de origen de datos*, *aplicación distribuida*.  
  
 COM (modelo de objetos componentes)  
 Un estándar binario que permite a los objetos en un entorno de red independientemente del lenguaje en el que se desarrollaron o en los equipos que residen. Las tecnologías basadas en COM incluyen controles ActiveX, automatización y vinculación e incrustación de objetos (OLE). COM permite que un objeto exponga su funcionalidad a otros componentes y aplicaciones host. Define cómo se expone el objeto y cómo funciona esta exposición entre procesos y a través de redes. COM también define el ciclo de vida del objeto.  
  
 Componente de COM  
 Archivo binario - por ejemplo, .dll, .ocx y algunos archivos .exe - que admite el estándar de COM para proporcionar objetos. Este archivo contiene código para uno o varios generadores de clases, las clases COM, mecanismos de entrada del registro, el código de carga y así sucesivamente.  
  
 Operador de comparación  
 Un operador que compara dos expresiones y devuelve un valor booleano.  
  
 Un parámetro de criterios que puede expresarse como ">" (mayor que), "\<" (menor que), "=" (igual), "> =" (mayor o igual que), "< =" (menor o igual que), "<>" (no es igual a) o "like" (coincidencia).  
  
 component  
 Un objeto que encapsula el código y datos y proporciona un conjunto bien especificado de servicios disponibles públicamente.  
  
 archivo compuesto  
 Una implementación de COM había estructurado el almacenamiento de archivos. Un archivo compuesto almacena objetos independientes en un único archivo estructurado que consta de dos elementos principales: objetos de almacenamiento y los objetos de flujo. Ambos funcionan conjuntamente como un sistema de archivos dentro de un archivo.  
  
 Un número de archivos individuales reunidos en un archivo físico. Cada archivo individual en un archivo compuesto se puede acceder como si fuese un solo archivo físico.  
  
 constant  
 Un valor numérico o de cadena que no cambia. Enumeraciones de ADO con nombre (constantes enumeradas) se pueden utilizar en el código en lugar de los valores reales, por ejemplo, **adUseClient** es una constante cuyo valor es 3. (Const adUseClient = 3). Vea también *enumeración*.  
  
 cursor  
 Un elemento de la base de datos que controla la exploración de registros, actualización de los datos y la visibilidad de los cambios realizados en la base de datos por otros usuarios.  
  
## <a name="d"></a>D  
 Enlace de datos  
 El proceso de asociar los objetos o controles de una aplicación a un origen de datos. Se llama a un control asociado a un origen de datos un *control enlazado a datos*.  
  
 El contenido de un control enlazado a datos está asociado con los valores de una base de datos. Por ejemplo, un control de cuadrícula está enlazado a un **Recordset** objeto puede ser actualizado cuando las filas de la **Recordset** se actualizan. Cuando se recuperan los nuevos valores mediante el **Recordset**, nuevos valores se muestran en la cuadrícula.  
  
 proveedor de datos  
 Software que expone los datos a una aplicación ADO directamente o a través de un proveedor de servicios. Vea también: proveedor de servicios.  
  
 la forma de datos  
 Una técnica que usa una sintaxis formalizada (denominada **lenguaje de forma**) para definir un especializado **Recordset** objeto (llamado un *en forma de conjunto de registros*) que no contiene sólo datos, sino también las referencias a otros **Recordset** objetos o valores calculados basan en las otras **Recordset** objetos.  
  
 nivel de origen de datos  
 Una capa lógica de un sistema distribuido que representa un equipo que ejecuta un DBMS, como una base de datos de SQL Server. Vea también *capa de cliente*, *nivel intermedio*, *aplicación distribuida*.  
  
 DCOM  
 Un protocolo de conexión que permite a los componentes COM para comunicarse directamente entre sí a través de una red. Vea también *COM*, *componente*.  
  
 DDL (lenguaje de definición de datos)  
 Esas instrucciones en SQL que definen, en lugar de manipular los datos. El esquema de una base de datos se crea o modifica con DDL. Por ejemplo, **CREATE TABLE**, **CREATE INDEX**, **GRANT**, y **REVOCAR** son instrucciones de DDL de SQL.  
  
 flujo predeterminado  
 Una secuencia de texto o binario (representado por un **Stream** objeto) que está asociado con **registro** o **Recordset** objetos al usar ciertos proveedores OLE DB, como la Proveedor Microsoft OLE DB para la publicación en Internet. Normalmente, la secuencia predeterminada contiene el contenido de un archivo, como el código HTML para la raíz de un sitio Web.  
  
 aplicación distribuida  
 Un programa escrito para que el procesamiento se puede dividir en varios equipos a través de una red. Normalmente, una aplicación distribuida se divide en presentación, lógica de negocios y datos de las capas del almacén, o *niveles*. Consulte también el nivel de cliente, nivel intermedio y capa de origen de datos.  
  
 conjunto de registros desconectado  
 Un **Recordset** objeto en una memoria caché del cliente que ya no tiene una conexión dinámica con el servidor. Si es necesario acceder a nuevamente por algún motivo, como la actualización de datos, el origen de datos original se debe restablecer la conexión. Sin embargo, las colecciones, propiedades y métodos de un desconectado **Recordset** todavía pueden tener acceso.  
  
 DML (lenguaje de manipulación de datos)  
 Esas instrucciones en SQL que manipulan, en lugar de para definir los datos. Los valores de una base de datos se selecciona y modificar con DML. Por ejemplo, **insertar**, **actualización**, **eliminar**, y **seleccione** son instrucciones DML SQL.  
  
 proveedor de código fuente del documento  
 Una clase especial de proveedores que administran carpetas y documentos. Cuando un documento se representa mediante un **registro** objeto o una carpeta de documentos se representa mediante un **Recordset** objeto, el proveedor de código fuente del documento rellena esos objetos con un único conjunto de campos que Describe las características del documento, en lugar del propio documento. Consulte también el registro de recursos.  
  
 DSN (nombre de origen de datos)  
 La recopilación de información que se usa para conectar la aplicación a una base de datos ODBC determinada. El Administrador de controladores ODBC utiliza esta información para crear una conexión a la base de datos. Un DSN puede almacenarse en un archivo (DSN de archivo) o en el registro de Windows (DSN de equipo).  
  
 propiedad dinámica  
 Una propiedad específica de un proveedor de datos o el servicio de cursores. El **propiedades** colección de un objeto se rellena automáticamente con estos ("dinámicamente"). Un objeto no tiene ninguna propiedad dinámica hasta que se conecte a un origen de datos a través de un proveedor de datos determinado. Vea también datos de proveedor, el cursor.  
  
## <a name="e"></a>E  
 Enumeración  
 Una lista de constantes con nombre. Los valores enumerados no necesitan ser únicos. Sin embargo, el nombre de cada valor debe ser único dentro del ámbito donde se define la enumeración. En ADO, las enumeraciones se utilizan para parámetros numéricos y valores devuelven, para agregar significado al código de ADO y protegen al desarrollador de los valores numéricos (que pueden variar de una versión a otra). Por ejemplo, para abrir una estática **Recordset**, utilice el **adOpenStatic** valor enumerado: `Recordset.Open ,,adOpenStatic`  
  
 También se denomina *constante enumerada*. Vea también *constante*.  
  
 event  
 Una acción reconocida por un objeto, que puede escribir código para responder. Se pueden generar eventos mediante la ejecución del comando, realización de la transacción, exploración del conjunto de registros y las actualizaciones de datos, entre otras acciones. Vea también *controlador de eventos*.  
  
 controlador de eventos  
 Un controlador de eventos es el código que se ejecuta cuando se produce un evento. Vea también: evento.  
  
## <a name="h"></a>H  
 controlador  
 Una rutina que administra una condición común y relativamente simple o una operación, como la administración de datos o recuperación de errores.  
  
 conjunto de registros jerárquico  
 Un **Recordset** que contiene otra **Recordset**. Consulte también el capítulo, la forma de datos.  
  
 Para obtener más información, consulte [obtener acceso a filas en un conjunto de registros jerárquicos](../../ado/guide/data/accessing-rows-in-a-hierarchical-recordset.md).  
  
 jerarquía  
 En general, una jerarquía es una estructura con una nivel superior de nivel y niveles subordinados. En ADO, jerárquica **conjuntos de registros** se utilizan para representar la relación de elementos primarios y secundarios entre un registro y un capítulo. También en ADO, **registro** y **Stream** objetos pueden utilizarse para tener acceso a las estructuras de árbol jerárquica, como documentos y una carpeta. ADO MD también incluye **jerarquía** objetos para representar una relación entre los niveles de una dimensión en un cubo OLAP. Vea también: conjuntos de registros jerárquicos, relación de elementos primarios y secundarios, capítulo y árbol.  
  
## <a name="i-l"></a>I-L  
 ISAPI (interfaz de programación de aplicaciones de servidor de Internet)  
 Un conjunto de funciones para servidores de Internet, como un Windows NT® Server o Windows 2000 Server ejecuta Microsoft® Internet Information Services (IIS).  
  
 Key  
 Una o varias columnas en una tabla que identifican de forma única una fila; a menudo se usa para indexar una tabla.  
  
## <a name="m"></a>M  
 El cálculo de referencias  
 El proceso de empaquetado, envío y desempaquetado de parámetros de método de interfaz a través de límites de proceso o subproceso.  
  
 Nivel intermedio  
 La capa de lógica en un sistema distribuido entre una interfaz de usuario o cliente Web y la base de datos. Normalmente es donde se crean instancias de objetos de negocios. El nivel intermedio es una colección de reglas de negocios y las funciones que generan y actúan tras recibir la información. Para lograrlo a través de reglas de negocios, que pueden cambiar con frecuencia y, por tanto, se encapsulan en componentes que están separados físicamente de la lógica de la aplicación. También se denomina *capa de aplicación servidor*. Consulte también la aplicación distribuida, el nivel de cliente y la capa de origen de datos.  
  
 MIME (extensión de correo de Internet con varios fines)  
 Un protocolo de Internet se desarrolló originalmente para permitir el intercambio de mensajes de correo electrónico con contenido enriquecido a través de una red heterogénea, equipo y entornos de correo electrónico. En la práctica, MIME también se han adoptado y ampliar las aplicaciones que no son de correo electrónico.  
  
 MIME es un estándar que permite que los datos binarios que se publican y leer en Internet. El encabezado de un archivo con datos binarios contiene el tipo MIME de los datos; Esto informa a los programas cliente (exploradores Web y paquetes de correo electrónico, por ejemplo) que necesitan administrar los datos de forma diferente que permiten controlar el texto. Por ejemplo, el encabezado de un documento Web que contiene un gráfico JPEG contiene el tipo MIME específico para el formato de archivo JPEG. Esto permite que un explorador mostrar el archivo con su visor JPEG, si hay alguno.  
  
## <a name="n-o"></a>N-O  
 Nodo  
 Un elemento en una estructura de árbol jerárquico. Un nodo puede ser la raíz o el elemento secundario de otro nodo. Un nodo puede ser también el elemento primario de varios elementos secundarios. Vea también jerarquía, árbol, raíz, secundario y primario.  
  
 variable de objeto  
 Variable que contiene una referencia a un objeto. Por ejemplo, `objCustomObject` es una variable que señala a un objeto de tipo CustomObject:`Set objCustomObject = CreateObject(adodb.Recordset)`  
  
 ODBC (Conectividad abierta de bases de datos)  
 Estándar lenguaje interfaz de programación utilizada para conectarse a una variedad de orígenes de datos. Esto normalmente se accede a través del Panel de Control, donde se pueden asignar nombres de origen de datos (DSN) a usar controladores ODBC específicos.  
  
 OLE DB  
 Un conjunto de interfaces que exponen datos desde una variedad de orígenes mediante COM. Las interfaces de OLE DB proporcionan aplicaciones con acceso uniforme a los datos almacenados en diversos orígenes de información. Estas interfaces de compatibilidad de la cantidad de funcionalidad del DBMS adecuada para el origen de datos, lo que le permite compartir sus datos. Vea también COM.  
  
 bloqueo optimista  
 Tipo de bloqueo en la que la página de datos que contiene uno o más registros, incluido el registro que se está editando, está disponible para otros usuarios sólo mientras se está actualizando el registro por el **Update** método, pero está disponible antes y después de la la llamada a **actualización**.  
  
 Bloqueo optimista se utiliza cuando el **Recordset** se abre el objeto con el **LockType** parámetro o la propiedad establecida en **adLockOptimistic** o  **adLockBatchOptimistic**. Consulte también el bloqueo pesimista.  
  
 valor ordinal  
 La ubicación numérica de un elemento dentro de un pedido. En una colección de ADO, el valor ordinal del primer elemento es cero (0). El elemento siguiente es uno (1) y así sucesivamente.  
  
## <a name="p"></a>P  
 comando con parámetros  
 Una consulta o comando que permite establecer los valores de parámetro antes de ejecutar el comando. Por ejemplo, una cadena SQL se puede parametrizar incrustando marcadores de parámetros en la cadena de SQL (designado por el '?' caracteres). La aplicación, a continuación, especifica valores para cada parámetro y ejecuta el comando.  
  
 primario  
 La parte que controla una relación jerárquica. En una estructura jerárquica, un elemento primario tiene uno o más nodos secundarios debajo de ella en la jerarquía. Vea también alias del primario, relación de elementos primarios y secundarios y secundarios.  
  
 parent-alias  
 Un alias que hace referencia al elemento primario. Vea también alias, elemento primario.  
  
 relación de elementos primarios y secundarios  
 Una relación en una estructura jerárquica en el que el elemento primario es un nivel superior y directamente asociado con uno o más elementos secundarios. Un elemento secundario es un nivel inferior y debe tener un elemento primario. Consulte también el elemento primario, secundario.  
  
 El bloqueo pesimista  
 Tipo de bloqueo en la que la página que contiene uno o más registros, incluido el registro que se está editando, está disponible para otros usuarios para asegurarse de que se realizará una actualización. Comportamiento de bloqueo pesimista se define mediante el proveedor OLE DB. Normalmente, los registros se bloquean durante la edición y permanecen disponibles hasta que el **actualización** método ha finalizado.  
  
 El bloqueo pesimista está habilitado cuando la **Recordset** se abre el objeto con el **LockType** parámetro o la propiedad establecida en **adLockPessimistic**. Vea también bloqueo optimista.  
  
 Agrupación  
 Optimización del rendimiento en función de las colecciones de recursos asignados previamente, como objetos o conexiones de base de datos. Resulta más eficaz para dibujar un recurso existente desde el grupo que la creación de un nuevo recurso.  
  
 ProgID (identificador de programación)  
 Un nombre único asignado al registro de Windows por una aplicación COM. El ProgID para una conexión ADO es "ADODB. Conexión". Vea también CLSID y COM.  
  
 Proxy  
 Un objeto de específica de la interfaz que proporciona el cálculo de referencias de parámetro y la comunicación necesaria para que un cliente llamar a un objeto de aplicación que se ejecuta en un entorno de ejecución diferente, como en un subproceso diferente o en otro proceso. El proxy se encuentra con el cliente y se comunica con un código auxiliar correspondiente que se encuentra con el objeto de aplicación que se llama. Vea también: código auxiliar.  
  
## <a name="r"></a>R  
 dirección URL relativa  
 Dirección URL parcialmente completa que especifica un recurso en Internet o una intranet cuya ubicación es relativa a un punto inicial especificado por una dirección URL absoluta o un objeto de conexión ADO equivalente. En efecto, la constituyen de direcciones URL concatenado de absolutas y relativa una dirección URL completa. Vea también URL y la dirección URL absoluta.  
  
 origen de datos remoto  
 Un origen de datos que existe en otro equipo, en lugar de en el sistema local (donde se ejecuta la aplicación cliente).  
  
 registro de recursos  
 Un registro de un proveedor de código fuente del documento que contiene campos para la definición y descripción de un documento o carpeta. El propio documento no está contenido en el registro de recursos, pero normalmente puede obtenerse mediante la secuencia predeterminada o un campo en el registro de recursos que contiene una dirección URL. Vea también: proveedor de código fuente del documento, secuencia predeterminada y dirección URL.  
  
 conjunto de filas  
 Un conjunto de filas desde un origen de datos tienen el mismo esquema de campo. Un conjunto de filas puede representar algunos o todos los campos de una tabla. Un conjunto de filas también puede representar una tabla virtual, creada por una consulta o una combinación de dos o más tablas. En ADO, los conjuntos de filas se representan mediante **Recordset** objetos.  
  
## <a name="s"></a>S  
 Scope  
 El intervalo de referencia para un objeto o variable o un intervalo de registros en una tabla o vista. Por ejemplo, pueden hacer referencia a variables locales solo dentro del procedimiento en el que se hubieran definido. Las variables públicas son accesibles desde cualquier parte de la aplicación. Los objetos, como la base de datos actual, están en ámbito si se encuentran en la ruta de acceso de búsqueda definida. Los intervalos de registros se pueden especificar con una cláusula de ámbito de muchos comandos.  
  
 proveedor de servicios  
 Software que encapsula un servicio al producir y consumir datos, aumentan las características de las aplicaciones ADO. Es un proveedor que no exponen datos directamente, sino que proporciona un servicio, como el procesamiento de consultas. El proveedor de servicios puede procesar los datos proporcionados por un proveedor de datos. Vea también: proveedor de datos.  
  
 conjunto de registros con forma  
 Un **Recordset** cuyas columnas se han definido específicamente para contener no solo datos, sino también las referencias (denominadas capítulos) Sí **Recordset** objetos o valores calculados basándose en otros **Recordset** objetos.  
  
 elemento relacionado  
 Dos o más nodos en una estructura jerárquica que se encuentran en el mismo nivel en la jerarquía. El nodo raíz en una jerarquía no tiene ningún elementos del mismo nivel.  
  
 procedimiento almacenado  
 Colección precompilada de código, como las instrucciones SQL e instrucciones de control de flujo opcionales almacenadas con un nombre y procesadas como una unidad. Los procedimientos almacenados se almacenan en una base de datos; que se pueden ejecutar con una llamada desde una aplicación y permiten variables declarado por el usuario, la ejecución condicional y otras características de programación eficaces.  
  
 Código auxiliar  
 Un objeto de específica de la interfaz que proporciona el cálculo de referencias de parámetro y la comunicación necesaria para que un objeto de aplicación recibir llamadas desde un cliente que se ejecuta en un entorno de ejecución diferente, como en un subproceso diferente o en otro proceso. El código auxiliar se encuentra con el objeto de aplicación y se comunica con un proxy correspondiente que se encuentra con el cliente que lo llama. Consulte también el proxy.  
  
 nodo secundario  
 Vea el elemento secundario.  
  
 operación sincrónica  
 Una operación iniciada por el código que se complete antes de que puede comenzar la siguiente operación. Consulte también la operación asincrónica.  
  
## <a name="t-z"></a>T-Z  
 trEE  
 Una estructura que representa una relación jerárquica entre elementos (nodos). Hay un nodo en el nivel superior de un árbol (la raíz). Debajo de la raíz, puede haber varios elementos secundarios. Cada elemento secundario a su vez puede ser el elemento primario de otro elemento secundario, así como un árbol de la bifurcación. Una carpeta que contiene los documentos y otras carpetas es un ejemplo típico de una estructura de árbol. Vea también jerarquía, nodo, raíz, secundario y primario.  
  
 Servidor Web  
 Un equipo que proporciona servicios Web y páginas de intranet y los usuarios de Internet.
