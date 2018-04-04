---
title: Glosario de ADO | Documentos de Microsoft
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: ''
ms.component: ado
ms.technology: drivers
ms.topic: article
helpviewer_keywords:
- ADO, glossary
ms.assetid: b0478836-4123-4357-969a-c5784fc28be5
caps.latest.revision: 15
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: f24e579d2cd1802b42ce4ae2cbc2d8b5b8e447e6
ms.sourcegitcommit: 8f1d1363e18e0c32ff250617ab6cb2da2147bf8e
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/03/2018
---
# <a name="ado-glossary"></a>Glosario de ADO
En este tema define los términos relacionados con ADO.  
  
## <a name="a"></a>A  
 dirección URL absoluta  
 Una dirección URL completa que especifica la ubicación de un recurso que reside en Internet o una intranet. Vea también *URL* y *dirección URL relativa*.  
  
 Control ActiveX  
 Registrar automáticamente, en curso componente COM que a menudo tiene un elemento visual en tiempo de diseño o tiempo de ejecución. Los controles ActiveX también tienen la capacidad de comunicarse con un contenedor de documentos activos, como Microsoft Internet Explorer.  
  
 ADISAPI (avanzada interfaz de programación de aplicaciones de servidor de Internet de datos)  
 Una DLL ISAPI que proporciona funciones de análisis, control de automatización, el cálculo de referencias de conjunto de registros y el empaquetado MIME. El componente ADISAPI funciona a través de la API proporcionada por servicios de Internet Information Server (IIS). Vea también *ISAPI*.  
  
 función de agregado  
 En una consulta, una función como COUNT, AVG o STDEV que calcula un valor con todas las filas de la columna de una tabla. Al escribir expresiones y en la programación, puede utilizar las funciones de agregado de SQL (incluidas las tres mencionadas anteriormente) y las funciones de agregado de dominio para determinar varias estadísticas.  
  
 alias  
 Un nombre alternativo que se asigna a una columna o expresión en una instrucción SELECT de SQL, a menudo más corta o más significativa. Por ejemplo, VentasPilar es un alias en la siguiente instrucción SELECT: "Select ventas-wr as VentasPilar from SalesDB". Un alias se puede utilizar para asignar columnas dinámicamente a los enlaces de control en el objeto DataControl.  
  
 subprocesamiento de apartamentos  
 Un modelo de subprocesamiento COM donde todas las llamadas a un objeto se producen en un subproceso. En el subproceso de apartamento COM sincroniza y calcula las referencias de llamadas. Vea también *COMmddefcom*.  
  
 operación asincrónica  
 Una operación que devuelve el control al programa que realiza la llamada sin tener que esperar a que finalice la operación. Antes de que la operación se completa, continúa la ejecución de código. Vea también *el funcionamiento sincrónico*.  
  
## <a name="b"></a>B  
 entrada de enlace  
 Una asignación entre un campo en una tabla y una variable. En las extensiones de Visual C++ de ADO, **Recordset** campos se asignan a variables de C o C++.  
  
 bitmask  
 Un valor numérico destinado a una comparación de valores de bit a bit con otros valores numéricos, normalmente para marcar opciones en parámetros o valores devueltos. Esta comparación se suele realizar mediante operadores lógicos bit a bit, como **y** y **o** en Visual Basic, **&** y **&#124;** en C++.  
  
 Por ejemplo, la propiedad ADO **FieldAttributeEnum** valores pueden utilizarse como máscaras de bits para determinar los atributos de un campo. Suponga que desea determinar si un campo se puede actualizar. Puede comprobar con la siguiente expresión en Visual Basic:`Field.Attributes AND adFldUpdatable`  
  
 Si el resultado es TRUE, el campo es actualizable.  
  
 marcador  
 Un marcador que identifica de forma única una fila dentro de un conjunto de filas para que un usuario puede navegar rápidamente a él.  
  
 objeto de negocios  
 Un objeto que realiza un conjunto definido de operaciones, como la lógica de regla de validación o business de datos. Objetos de negocio residen normalmente en el nivel intermedio.  
  
 regla de negocios  
 La combinación de ediciones de validación, comprobaciones de inicio de sesión, las búsquedas de la base de datos, directivas y transformaciones algorítmicas que constituyen la forma de una empresa de hacer negocios. También se denomina *lógica de negocios*.  
  
## <a name="c"></a>C  
 expresión calculada  
 Una expresión que no es constante, pero cuyo valor depende de otros valores. Para la evaluación, una expresión calculada debe obtener y calcular los valores de otros orígenes, normalmente en otros campos o filas.  
  
 capítulo  
 Una referencia a un rango de filas desde un origen de datos. En ADO, un capítulo suele ser una referencia a otro **conjunto de registros**.  
  
 Columnas de capítulo permiten definir una *elementos primarios y secundarios* relación donde la *primario* es el **Recordset** que contiene la columna de capítulo y  *secundario* es el **Recordset** representado por el capítulo.  
  
 chapter-alias  
 Un alias que hace referencia a la columna anexada al elemento primario.  
  
 juego de caracteres  
 Una asignación de un juego de caracteres y sus valores numéricos. Por ejemplo, Unicode es un carácter de 16 bits establecer capaz de codificar todos los caracteres conocidos y se utiliza como un estándar de codificación de caracteres en todo el mundo.  
  
 child  
 El lado dependiente de una relación jerárquica. Un elemento secundario es un nodo en una estructura jerárquica que tiene otro nodo por encima de él (más cerca de la raíz). Vea también *alias secundario*, *relación de elementos primarios y secundarios*, *primario*.  
  
 alias de elemento secundario  
 Un alias que hace referencia al elemento secundario. Vea también *alias*, *secundario*.  
  
 CLSID (identificador de clase)  
 Un identificador único universal (UUID) que identifica un componente COM. Cada componente COM tiene su CLSID en el registro de Windows para que se puede cargar por otras aplicaciones. Vea también *ProgID*, *COM*.  
  
 nivel de cliente  
 Una capa lógica de un sistema distribuido que normalmente presenta datos y procesos de entrada del usuario, a veces se denomina la *front-end*. Normalmente, el nivel de cliente solicita datos desde un servidor basado en la entrada y, a continuación, se da formato y muestra el resultado. Vea también *nivel intermedio*, *capa de origen de datos*, *aplicación distribuida*.  
  
 COM (modelo de objetos componentes)  
 Un estándar binario que permite a los objetos interactuar en un entorno de red independientemente del lenguaje en el que se desarrollaron o en los equipos que residen. Las tecnologías basadas en COM incluyen los controles ActiveX, la automatización y la vinculación e incrustación de objetos (OLE). COM permite que un objeto exponer su funcionalidad a otros componentes y aplicaciones del host. Define cómo se expone el objeto y el funcionamiento de esta información a través de procesos y redes. COM también define el ciclo de vida del objeto.  
  
 Componente de COM  
 Archivo binario, por ejemplo, .dll, .ocx y algunos archivos .exe, que admite el estándar de COM para proporcionar objetos. Este archivo contiene código para uno o varios generadores de clases, clases COM, mecanismos de entrada del registro, código de carga y así sucesivamente.  
  
 operador de comparación  
 Un operador que compara dos expresiones y devuelve un valor booleano.  
  
 Un parámetro de criterios que puede expresarse como ">" (mayor que), "\<" (menor que), "=" (igual), "> =" (mayor o igual que), "< =" (menor o igual que), "<>" (no es igual a) o "like" (coincidencia de modelos).  
  
 component  
 Un objeto que encapsula datos y código y proporciona un conjunto bien especificado de servicios públicamente disponibles.  
  
 archivo compuesto  
 Una implementación de COM había estructurado almacenamiento para los archivos. Un archivo compuesto almacena objetos independientes en un único archivo estructurado que consta de dos elementos principales: objetos de almacenamiento y objetos de flujo. Ambos funcionan conjuntamente como un sistema de archivos dentro de un archivo.  
  
 Número de archivos individuales reunidos en un archivo físico. Puede tener acceso a cada archivo individual en un archivo compuesto como si fuera un solo archivo físico.  
  
 constant  
 Un valor numérico o de cadena que no cambia. Enumeraciones de ADO con nombre (constantes enumeradas) se pueden utilizar en el código en lugar de valores reales, por ejemplo, **adUseClient** es una constante cuyo valor es 3. (Const adUseClient = 3). Vea también *enumeración*.  
  
 cursor  
 Un elemento de base de datos que controla la exploración de registros, capacidad de actualización de datos y la visibilidad de los cambios realizados por otros usuarios en la base de datos.  
  
## <a name="d"></a>D  
 enlace de datos  
 El proceso de asociar los objetos o controles de una aplicación a un origen de datos. Un control asociado con un origen de datos se denomina un *control enlazado a datos*.  
  
 El contenido de un control enlazado a datos está asociado con los valores de una base de datos. Por ejemplo, un control de cuadrícula está enlazado a un **conjunto de registros** puede ser objeto actualizado cuando las filas de la **conjunto de registros** se actualizan. Cuando se recuperan los nuevos valores mediante la **Recordset**, nuevos valores se muestran en la cuadrícula.  
  
 proveedor de datos  
 Software que expone los datos a una aplicación ADO directamente o a través de un proveedor de servicios. Vea también proveedor de servicios.  
  
 la forma de datos  
 Una técnica que hace uso de una sintaxis formalizada (llama **forma lenguaje**) para definir un especializadas **conjunto de registros** objeto (denominado un *en forma de conjunto de registros*) que no contiene solo datos, sino también referencias a otras **Recordset** objetos o valores calculados en función de los otros **Recordset** objetos.  
  
 nivel de origen de datos  
 Una capa lógica de un sistema distribuido que representa un equipo que ejecuta un DBMS, como una base de datos de SQL Server. Vea también *nivel de cliente*, *nivel intermedio*, *aplicación distribuida*.  
  
 DCOM  
 Un protocolo de conexión que permite a los componentes COM para comunicarse directamente entre sí a través de una red. Vea también *COM*, *componente*.  
  
 DDL (lenguaje de definición de datos)  
 Estas instrucciones en SQL que definen, en lugar de manipular los datos. El esquema de una base de datos se crea o se modifica con DDL. Por ejemplo, **CREATE TABLE**, **CREATE INDEX**, **GRANT**, y **REVOCAR** son instrucciones de DDL de SQL.  
  
 flujo predeterminado  
 Una secuencia de texto o binario (representado por un **flujo** objeto) que está asociado a **registro** o **Recordset** objetos cuando se usan determinados proveedores de OLE DB, como la Proveedor Microsoft OLE DB para la publicación en Internet. Normalmente, la secuencia predeterminada contiene el contenido de un archivo como el código HTML de la raíz de un sitio Web.  
  
 aplicación distribuida  
 Un programa escrito de modo que el procesamiento se puede dividir en varios equipos a través de una red. Normalmente, una aplicación distribuida se divide en presentación, lógica de negocios y datos de las capas de almacenamiento o *niveles*. Vea también nivel de cliente, nivel intermedio y nivel de origen de datos.  
  
 conjunto de registros desconectado  
 A **Recordset** objeto en una memoria caché del cliente que ya no tiene una conexión activa con el servidor. Si el origen de datos debe tener acceso a nuevo por algún motivo, como la actualización de datos, se debe restablecer la conexión. Sin embargo, las colecciones, propiedades y métodos de un desconectada **Recordset** son accesibles.  
  
 DML (lenguaje de manipulación de datos)  
 Estas instrucciones en SQL que manipulan, en lugar de para definir los datos. Los valores de una base de datos están seleccionados y modificar con DML. Por ejemplo, **insertar**, **actualización**, **eliminar**, y **seleccione** son instrucciones DML SQL.  
  
 proveedor de código fuente del documento  
 Una clase especial de proveedores que administran carpetas y documentos. Cuando un documento se representa mediante un **registro** objeto o una carpeta de documentos se representa mediante un **Recordset** de objeto, el proveedor de origen de documentos rellena esos objetos con un único conjunto de campos que se describen las características del documento, en lugar de al propio documento. Vea también el registro de recursos.  
  
 DSN (nombre de origen de datos)  
 La recopilación de información que se utiliza para conectar la aplicación a una base de datos ODBC determinada. El Administrador de controladores ODBC utiliza esta información para crear una conexión a la base de datos. Un DSN puede almacenarse en un archivo (DSN de archivo) o en el registro de Windows (DSN de equipo).  
  
 propiedades dinámicas  
 Una propiedad específica para un proveedor de datos o el servicio de cursor. El **propiedades** colección de un objeto se rellena automáticamente con estos ("dinámicamente"). Un objeto no tiene propiedades dinámicas hasta que se conecte a un origen de datos mediante un proveedor de datos determinado. Vea también datos de proveedor, el cursor.  
  
## <a name="e"></a>E  
 Enumeración  
 Una lista de constantes con nombre. Los valores enumerados no necesitan ser únicos. Sin embargo, el nombre de cada valor debe ser único dentro del ámbito donde se define la enumeración. En ADO, las enumeraciones se utilizan para parámetros numéricos y valores devuelven, para agregar significado al código de ADO y para proteger al programador de los valores numéricos (que pueden variar de una versión a otra). Por ejemplo, para abrir una variable static **Recordset**, use la **adOpenStatic** valor enumerado: `Recordset.Open ,,adOpenStatic`  
  
 También se denomina *constante enumerada*. Vea también *constante*.  
  
 event  
 Una acción reconocida por un objeto para el que puede escribir código para responder. Eventos pueden generarse mediante la ejecución del comando, realización de la transacción, exploración del conjunto de registros y las actualizaciones de datos, entre otras acciones. Vea también *controlador de eventos*.  
  
 controlador de eventos  
 Un controlador de eventos es el código que se ejecuta cuando se produce un evento. Vea también el evento.  
  
## <a name="h"></a>H  
 Controlador  
 Una rutina que administra una condición de común y relativamente simple o una operación, como la administración de datos o recuperación de errores.  
  
 conjunto de registros jerárquico  
 A **Recordset** que contiene a otra **conjunto de registros**. Consulte también el capítulo, la forma de datos.  
  
 Para obtener más información, consulte [obtener acceso a filas en un conjunto de registros jerárquicos](../../ado/guide/data/accessing-rows-in-a-hierarchical-recordset.md).  
  
 jerarquía  
 En general, una jerarquía es una estructura con una nivel superior de nivel y niveles subordinados. En ADO, jerárquica **conjuntos de registros** se usan para representar la relación de elementos primarios y secundarios entre un registro y un capítulo. También en ADO, **registro** y **flujo** objetos se pueden usar para tener acceso a las estructuras de árbol jerárquica, como una carpeta y sus documentos. ADO MD también incluye **jerarquía** objetos para representar una relación entre los niveles de una dimensión en un cubo OLAP. Vea también conjuntos de registros jerárquicos, relación de elementos primarios y secundarios, capítulo y árbol.  
  
## <a name="i-l"></a>I-L  
 ISAPI (interfaz de programación de aplicaciones de servidor de Internet)  
 Un conjunto de funciones para servidores de Internet, como un Windows NT® Server o Windows 2000 Server ejecuta Microsoft® Internet Information Services (IIS).  
  
 Key  
 Una o varias columnas en una tabla que identifican de forma única una fila; a menudo se utiliza para indizar una tabla.  
  
## <a name="m"></a>M  
 el cálculo de referencias  
 El proceso de empaquetado, envío y desempaquetado de parámetros de método de interfaz a través de límites de proceso o subproceso.  
  
 nivel intermedio  
 El nivel lógico en un sistema distribuido entre una interfaz de usuario o cliente Web y la base de datos. Normalmente es donde se crean instancias de objetos comerciales. El nivel intermedio es una colección de reglas de negocios y las funciones que generan y actúan tras recibir la información. Para hacerlo a través de las reglas de negocios, que pueden cambiar con frecuencia y, por tanto, se encapsulan en componentes físicamente independientes de la propia lógica de aplicación. También se denomina *capa de aplicación servidor*. Vea también aplicación distribuida, nivel de cliente y nivel de origen de datos.  
  
 MIME (extensión de correo de Internet con varios fines)  
 Un protocolo de Internet desarrollado originalmente para permitir el intercambio de mensajes de correo electrónico con contenido enriquecido entre red heterogénea, automático y entornos de correo electrónico. En la práctica, MIME tiene también ha adoptado y extiende las aplicaciones no son de correo.  
  
 MIME es un estándar que permite que los datos binarios que se publican y leer en Internet. El encabezado de un archivo con datos binarios contiene el tipo MIME de los datos; Esto informa a los programas clientes (exploradores Web y paquetes de correo electrónico, por ejemplo) que deben administrar los datos de forma diferente que controlan texto recta. Por ejemplo, el encabezado de un documento Web que contiene un gráfico JPEG contiene el tipo MIME específico para el formato de archivo JPEG. Esto permite a un explorador mostrar el archivo con su visor JPEG, si hay alguno.  
  
## <a name="n-o"></a>N-O  
 Nodo  
 Un elemento en una estructura de árbol jerárquico. Un nodo puede ser la raíz o el elemento secundario de otro nodo. Un nodo también puede ser el elemento primario de varios elementos secundarios. Vea también jerarquía, árbol, raíz, secundario y primario.  
  
 variable de objeto  
 Variable que contiene una referencia a un objeto. Por ejemplo, `objCustomObject` es una variable que apunta a un objeto de tipo CustomObject:`Set objCustomObject = CreateObject(adodb.Recordset)`  
  
 ODBC (Conectividad abierta de bases de datos)  
 Estándar lenguaje interfaz de programación utilizada para conectarse a una variedad de orígenes de datos. Normalmente, esto se administra a través del Panel de Control, donde se pueden asignar los nombres de origen de datos (DSN) para usar controladores ODBC específicos.  
  
 OLE DB  
 Un conjunto de interfaces que exponen datos desde una variedad de orígenes mediante COM. Interfaces de OLE DB proporcionan aplicaciones con acceso uniforme a los datos almacenados en diversos orígenes de información. Estas interfaces admiten la cantidad de la funcionalidad DBMS adecuada para el origen de datos, lo que le permite compartir sus datos. Vea también COM.  
  
 bloqueo optimista  
 Tipo de bloqueo en que la página de datos que contiene uno o más registros, incluido el registro que se está editando, no está disponible para otros usuarios sólo mientras se está actualizando el registro mediante el **actualización** método, pero está disponible antes y después de la la llamada a **actualización**.  
  
 Bloqueo optimista se utiliza cuando la **Recordset** objeto se abre con la **LockType** parámetro o la propiedad **adLockOptimistic** o  **adLockBatchOptimistic**. Vea también el bloqueo pesimista.  
  
 valor ordinal  
 La ubicación numérica de un elemento dentro de un pedido. En una colección de ADO, el valor ordinal del primer elemento es cero (0). El elemento siguiente es uno (1) y así sucesivamente.  
  
## <a name="p"></a>P  
 comando con parámetros  
 Una consulta o un comando que permite establecer valores de parámetro antes de que se ejecuta el comando. Por ejemplo, una cadena de SQL se puede parametrizar incrustando marcadores de parámetros en la cadena de SQL (designado por el '?' caracteres). La aplicación, a continuación, especifica valores para cada parámetro y ejecuta el comando.  
  
 primario  
 La parte que controla una relación jerárquica. En una estructura jerárquica, un elemento primario tiene uno o varios nodos secundarios directamente debajo de él en la jerarquía. Vea también alias primario, relación de elementos primarios y secundarios y secundarios.  
  
 alias del primario  
 Un alias que hace referencia al elemento primario. Vea también alias, principal.  
  
 relación de elementos primarios y secundarios  
 Una relación en una estructura jerárquica en el que el elemento primario es un nivel superior y directamente asociado a uno o más elementos secundarios. Un elemento secundario es un nivel inferior y debe tener un elemento primario. Vea también principal, secundario.  
  
 el bloqueo pesimista  
 Tipo de bloqueo en que la página que contiene uno o más registros, incluido el registro que se está editando, no está disponible para otros usuarios para asegurarse de que se realizará una actualización. El comportamiento del bloqueo pesimista se define mediante el proveedor OLE DB. Normalmente, los registros se bloquean durante una modificación y permanece disponibles hasta que el **actualización** método ha completado.  
  
 El bloqueo pesimista está habilitado cuando el **conjunto de registros** objeto se abre con la **LockType** parámetro o la propiedad establecida en **adLockPessimistic**. Vea también bloqueo optimista.  
  
 agrupación  
 Optimización del rendimiento en función de las colecciones de recursos preasignados, como objetos o conexiones de base de datos. Es más eficaz para dibujar un recurso existente desde el grupo que al crear un nuevo recurso.  
  
 ProgID (identificador de programación)  
 Un nombre único asignado al registro de Windows por una aplicación COM. El ProgID para una conexión ADO es "ADODB." "Conexión". Vea también CLSID y COM.  
  
 Proxy  
 Un objeto específico de la interfaz que proporciona la serialización de parámetros y la comunicación requerida para que un cliente llamar a un objeto de aplicación que se ejecuta en un entorno de ejecución diferente, como en un subproceso diferente o en otro proceso. El proxy se encuentra en el cliente y se comunica con un código auxiliar correspondiente que se encuentra en el objeto de aplicación que se está llamando. Vea también código auxiliar.  
  
## <a name="r"></a>L  
 dirección URL relativa  
 Dirección URL parcialmente cualificada que especifica un recurso en Internet o en una intranet cuya ubicación es relativa a un punto de partida especificado por una dirección URL absoluta o el objeto de conexión ADO equivalente. De hecho, la constituyen de direcciones URL concatenado de absolutas y relativa una dirección URL completa. Vea también URL y URL absoluta.  
  
 origen de datos remoto  
 Un origen de datos que existe en otro equipo, en lugar de en el sistema local (donde se ejecuta la aplicación cliente).  
  
 registro de recursos  
 Un registro de un proveedor de código fuente del documento que contiene campos para la definición y descripción de un documento o carpeta. El propio documento no está contenido en el registro de recursos, pero normalmente puede tener acceso a la secuencia predeterminada o un campo en el registro de recursos que contiene una dirección URL. Vea también proveedor de origen de documentos, secuencia predeterminada y URL.  
  
 conjunto de filas  
 Un conjunto de filas de un origen de datos, todos los que tengan el mismo esquema de campo. Un conjunto de filas puede representar algunos o todos los campos de una tabla. Un conjunto de filas también puede representar una tabla virtual, creada mediante una consulta o una combinación de dos o más tablas. En ADO, los conjuntos de filas se representan mediante **Recordset** objetos.  
  
## <a name="s"></a>S  
 Ámbito  
 El intervalo de referencia para un objeto o variable o un intervalo de registros en una tabla o vista. Por ejemplo, pueden hacer referencia a variables locales solo dentro del procedimiento en el que se definieron. Las variables públicas son accesibles desde cualquier parte de la aplicación. Objetos, como la base de datos actual, están en ámbito si se encuentran en la ruta de acceso de búsqueda definida. Los intervalos de registros se pueden especificar con una cláusula de ámbito en muchos comandos.  
  
 proveedor de servicios  
 Software que encapsula un servicio al producir y consumir datos, aumentan las características de las aplicaciones ADO. Es un proveedor que no expone datos directamente, sino que proporciona un servicio, como el procesamiento de consultas. El proveedor de servicios puede procesar los datos proporcionados por un proveedor de datos. Vea también proveedor de datos.  
  
 conjunto de registros con forma  
 A **Recordset** cuyas columnas se han definido específicamente para contener no sólo datos, sino también referencias (denominadas capítulos) a otras **Recordset** objetos o valores calculados en función de otros **Recordset** objetos.  
  
 elemento relacionado  
 Dos o más nodos en una estructura jerárquica que se encuentran en el mismo nivel en la jerarquía. El nodo raíz de una jerarquía no tiene ningún elementos del mismo nivel.  
  
 procedimiento almacenado  
 Colección precompilada de código como instrucciones SQL e instrucciones de control de flujo opcionales almacenadas con un nombre y procesadas como una unidad. Los procedimientos almacenados se almacenan en una base de datos; se puede ejecutar con una llamada desde una aplicación y permiten variables declaradas por el usuario, ejecución condicional y otras características de programación eficaces.  
  
 código auxiliar  
 Un objeto específico de la interfaz que proporciona la serialización de parámetros y comunicación requerida para que un objeto de aplicación recibir llamadas desde un cliente que se ejecuta en un entorno de ejecución diferente, como en un subproceso diferente o en otro proceso. El código auxiliar se encuentra en el objeto de aplicación y se comunica con un proxy correspondiente que se encuentra en el cliente que lo llama. Vea también proxy.  
  
 nodo secundario  
 Vea a secundario.  
  
 operación sincrónica  
 Una operación iniciada por el código que se completa antes de que puede comenzar la siguiente operación. Vea también la operación asincrónica.  
  
## <a name="t-z"></a>T-Z  
 trEE  
 Una estructura que representa una relación jerárquica entre elementos (nodos). Hay un nodo en el nivel superior de un árbol (la raíz). Debajo de la raíz, puede haber varios elementos secundarios. Cada elemento secundario a su vez puede ser el elemento primario de otros elementos secundarios, bifurcando así la estructura como un árbol. Una carpeta que contiene documentos y otras carpetas es un ejemplo típico de una estructura de árbol. Vea también jerarquía, nodo, raíz, secundario y primario.  
  
 Servidor Web  
 Un equipo que proporciona servicios Web y páginas de la intranet y los usuarios de Internet.
