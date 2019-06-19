---
title: Tipo de datos XML y columnas (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 05/17/2019
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: xml
ms.topic: conceptual
ms.assetid: 00db8f21-7d4b-4347-ae43-3a7c314d2fa1
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 6e0c0dbcb9f1cfea08ca1713f7ec46a698944255
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "65836159"
---
# <a name="xml-data-type-and-columns-sql-server"></a>Tipo de datos XML y columnas (SQL Server)

[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]
  En este tema se explican las ventajas y las limitaciones del tipo de datos **xml** en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]y le ayuda a elegir el modo de almacenar los datos XML.  
  
## <a name="relational-or-xml-data-model"></a>Modelo de datos relacionales o XML  
 Si los datos están muy estructurados con un esquema conocido, el modelo relacional tiene más probabilidades de funcionar mejor para el almacenamiento de datos. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] proporciona la funcionalidad y las herramientas necesarias. Por otra parte, si los datos están semiestructurados o no están estructurados, o no se conoce su estructura, debe contemplar la posibilidad de crear un modelo para los datos.  
  
 XML es una buena opción si desea un modelo independiente de la plataforma para garantizar la portabilidad de los datos mediante el uso de marcado estructural y semántico. Además, es una opción apropiada si se cumplen algunas de las siguientes propiedades:  
  
-   Los datos están dispersos o no se conoce la estructura de los mismos, o la estructura de los datos puede cambiar de manera importante en el futuro.  
  
-   Los datos representan una jerarquía de inclusión, en lugar de referencias entre entidades, y pueden ser recursivos.  
  
-   El orden es inherente a los datos.  
  
-   Desea realizar consultas en los datos o actualizar parte de ellos, basándose en su estructura.  
  
 Si no se cumple ninguna de estas condiciones, debe utilizar el modelo de datos relacional. Por ejemplo, si los datos tienen formato XML pero la aplicación solo usa la base de datos para almacenar y recuperar los datos, solo necesitará una columna **[n]varchar(max)** . Almacenar los datos en una columna XML tiene más ventajas. Una de ellas es que se puede hacer que el motor determine si los datos tienen un formato correcto o son válidos, y otra es la posibilidad de realizar consultas y actualizaciones detalladas en los datos XML.  
  
## <a name="reasons-for-storing-xml-data-in-sql-server"></a>Razones para almacenar datos XML en SQL Server  
 A continuación, se indican algunas de las razones para usar características XML nativas en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] en lugar de administrar los datos XML en el sistema de archivos:  
  
-   Desea compartir los datos XML, hacer consultas en ellos y modificarlos de forma eficaz y con transacciones. El acceso a datos con precisión es importante para la aplicación. Por ejemplo, tal vez desee extraer alguna sección de un documento XML, o insertar una nueva sección sin reemplazar todo el documento.  
  
-   Tiene datos relacionales y datos XML y desea que ambos tipos de datos puedan interoperar dentro de la aplicación.  
  
-   Necesita compatibilidad con lenguajes para realizar consultas y modificar datos en aplicaciones situadas en diversos dominios.  
  
-   Desea que el servidor garantice que los datos tienen un formato correcto y además, opcionalmente, validar los datos de acuerdo con esquemas XML.  
  
-   Desea indizar los datos XML para obtener un procesamiento eficiente de las consultas y una buena escalabilidad, y el uso de un optimizador de consultas de primera clase.  
  
-   Desea el acceso de SOAP, ADO.NET y OLE DB a los datos XML.  
  
-   Desea utilizar la funcionalidad administrativa del servidor de base de datos para administrar los datos XML, por ejemplo, para realizar copias de seguridad, recuperaciones y réplicas.  
  
 Si no se cumple ninguna de estas condiciones, es posible que convenga almacenar los datos como tipo de objeto grande no XML, por ejemplo, **[n]varchar(max)** o **varbinary(max)** .  
  
## <a name="xml-storage-options"></a>Opciones de almacenamiento de XML  
 Las opciones de almacenamiento para XML en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] son las siguientes:  
  
-   Almacenamiento nativo como tipo de datos **xml** .  
  
     Los datos se almacenan en una representación interna que conserva el contenido XML de los mismos. Esta representación interna incluye información sobre la jerarquía de inclusión, el orden de los documentos y los valores de los elementos y los atributos. En concreto, se conserva el contenido InfoSet de los datos XML. Para obtener más información sobre InfoSet, visite [http://www.w3.org/TR/xml-infoset](https://go.microsoft.com/fwlink/?LinkId=48843). El contenido del InfoSet puede no ser una copia idéntica del texto XML, porque no se retiene la información siguiente: espacios en blanco no significativos, orden de los atributos, prefijos de los espacios de nombres y declaración XML.  
  
     En el caso del tipo de datos **xml** con tipo, un tipo de datos **xml** enlazado a esquemas XML, el contenido InfoSet de validación de esquema posterior (PSVI) agrega información del tipo a InfoSet y se codifica en la representación interna. De este modo, se mejora considerablemente la velocidad de análisis. Para obtener más información, vea las especificaciones del esquema XML de W3C en [http://www.w3.org/TR/xmlschema-1](https://go.microsoft.com/fwlink/?LinkId=48881) y [http://www.w3.org/TR/xmlschema-2](https://go.microsoft.com/fwlink/?LinkId=4871).  
  
-   Asignar entre almacenamiento XML y relacional  
  
     El esquema anotado (AXSD) permite descomponer el código XML en columnas en una o más tablas. Así, se preserva la fidelidad de los datos en el nivel relacional. Como resultado, la estructura jerárquica se mantiene aunque se omita el orden entre los elementos. El esquema no puede ser recursivo.  
  
-   Almacenamiento de objetos grandes, **[n]varchar(max)** y **varbinary(max)**  
  
     Se almacena una copia idéntica de los datos. Esto resulta útil en el caso de aplicaciones para fines específicos, como documentos legales. La mayoría de las aplicaciones no requieren una copia exacta y les basta con el contenido XML (fidelidad InfoSet).  
  
 En general, es posible que se tenga que usar una combinación de estos enfoques. Por ejemplo, tal vez desee almacenar los datos XML en una columna de tipo de datos **xml** y promover las propiedades correspondientes en columnas relacionales. O tal vez quiera usar tecnología de asignaciones para almacenar partes no recursivas en columnas no XML y solo las partes recursivas en columnas de tipo de datos **xml** .  
  
### <a name="choice-of-xml-technology"></a>Elección de la tecnología XML  
 La elección de la tecnología XML, XML nativo frente a vista XML, en general depende de los siguientes factores:  
  
-   Opciones de almacenamiento  
  
     Los datos XML pueden ser más apropiados para el almacenamiento de objetos grandes (por ejemplo, el manual de un producto) o más sensibles al almacenamiento en columnas relacionales (por ejemplo, un elemento de línea convertido a XML). Cada opción de almacenamiento preserva la fidelidad del documento en distinta medida.  
  
-   Funciones de consultas  
  
     Es posible que una opción de almacenamiento le parezca más apropiada que otra en función de la naturaleza de las consultas y del nivel de detalle con que desea consultar los datos XML. La consulta detallada de los datos XML (por ejemplo, evaluación de predicados en nodos XML) se admite en diversos grados en las dos opciones de almacenamiento.  
  
-   Indizar datos XML  
  
     Tal vez desee indizar los datos XML para acelerar el rendimiento de las consultas XML. Las opciones de indización varían según las opciones de almacenamiento; es necesario hacer la elección apropiada para optimizar la carga de trabajo.  
  
-   Funciones para la modificación de datos  
  
     Algunas cargas de trabajo implican una modificación detallada de los datos XML. Éste es el caso de agregar una sección nueva a un documento. Sin embargo, otras cargas de trabajo, como el contenido web, no implican la modificación detallada de los datos XML. La compatibilidad con el lenguaje de modificación de datos puede ser importante para la aplicación.  
  
-   Compatibilidad con esquemas  
  
     Los datos XML se pueden describir mediante un esquema que puede ser o no un documento de esquema XML. La compatibilidad con XML enlazado a un esquema depende de la tecnología XML.  
  
 Las diferentes opciones también tienen distintas características en cuanto al rendimiento.  
  
### <a name="native-xml-storage"></a>Almacenamiento de XML nativo  
 Los datos XML se pueden almacenar en una columna de tipo de datos **xml** en el servidor. Esta es una elección apropiada si se cumple lo siguiente:  
  
-   Desea una manera directa de almacenar los datos XML en el servidor y, al mismo tiempo, preservar el orden y la estructura de los documentos.  
  
-   Puede tener o no un esquema para los datos XML.  
  
-   Desea consultar y modificar los datos XML.  
  
-   Desea indizar los datos XML para procesar más rápido las consultas.  
  
-   La aplicación necesita vistas de catálogo del sistema para administrar los datos XML y los esquemas XML.  
  
 El almacenamiento XML nativo es útil cuando se tienen documentos XML con una serie de estructuras, o si se tienen documentos XML que se ajustan a esquemas diferentes o completos que son demasiado difíciles de asignar a estructuras relacionales.  
  
#### <a name="example-modeling-xml-data-using-the-xml-data-type"></a>Ejemplo: modelado de datos XML mediante el tipo de datos xml  
 Piense en el manual de un producto en formato XML compuesto por un capítulo independiente para cada tema y por varias secciones dentro de cada capítulo. Una sección puede contener subsecciones. Como resultado, \<section> es un elemento recursivo. Los manuales de productos contienen una gran cantidad de contenido, diagramas y material técnico entremezclado; los datos están semiestructurados. Es posible que los usuarios deseen efectuar búsquedas contextuales de temas de interés, como la sección sobre "índices clúster" en el capítulo sobre "indización", y consultar dimensiones técnicas.  
  
 Un modelo de almacenamiento apropiado para los documentos XML es una columna de tipo de datos **xml** . Así se preserva el contenido InfoSet de los datos XML. La indización de la columna XML favorece el rendimiento de las consultas.  
  
#### <a name="example-retaining-exact-copies-of-xml-data"></a>Ejemplo: conservación de copias exactas de los datos XML  
 A modo de ilustración, suponga que las normativas del gobierno le exigen que retenga copias textuales exactas de sus documentos XML, como documentos firmados, documentos legales o pedidos de transacciones de almacén. Tal vez quiera almacenar los documentos en una columna **[n]varchar(max)** .  
  
 Para realizar consultas, convierta los datos al tipo de datos **xml** en tiempo de ejecución y ejecute Xquery. La conversión en tiempo de ejecución puede ser larga, especialmente si el documento es grande. Si realiza consultas con frecuencia, puede almacenar repetidamente los documentos en una columna de tipo de datos **xml** e indexarla mientras devuelve copias exactas de los documentos desde la columna **[n]varchar(max)** .  
  
 La columna XML puede ser una columna calculada basada en la columna **[n]varchar(max)** . Pero no se puede crear un índice XML en una columna XML calculada, ni se puede generar un índice XML en columnas **[n]varchar(max)** o **varbinary(max)** .  
  
### <a name="xml-view-technology"></a>Tecnología de vistas XML  
 La definición de una asignación entre los esquemas XML y las tablas de una base de datos permite crear una "vista XML" de los datos permanentes. Se puede efectuar una carga masiva de XML para rellenar las tablas subyacentes mediante la vista XML. Puede efectuar una consulta en la vista XML mediante XPath versión 1.0; la consulta se traduce en consultas SQL en las tablas. Del mismo modo, las actualizaciones también se propagan a dichas tablas.  
  
 Esta tecnología es útil en las situaciones siguientes:  
  
-   Desea tener un modelo de programación centrado en XML utilizando vistas XML sobre los datos relacionales existentes.  
  
-   Tiene un esquema (XSD, XDR) para los datos XML que puede haberle proporcionado un asociado externo.  
  
-   El orden no es importante para los datos, los datos de la tabla de la consulta no son recursivos, o el grado máximo de recursividad se conoce de antemano.  
  
-   Desea consultar y modificar los datos a través de la vista XML mediante XPath versión 1.0.  
  
-   Desea efectuar una carga masiva de datos XML y distribuirlos en las tablas subyacentes mediante la vista XML.  
  
 Algunos ejemplos son datos relacionales expuestos como XML para el intercambio de datos y servicios web, y datos XML con esquema fijo. Para obtener más información, vea la biblioteca en línea [MSDN Library](https://go.microsoft.com/fwlink/?linkid=31174).  
  
#### <a name="example-modeling-data-using-an-annotated-xml-schema-axsd"></a>Ejemplo: modelado de datos con un esquema XML anotado (AXSD)  
 A modo de ilustración, suponga que tiene datos relacionales como clientes, pedidos y artículos de línea, que desea tratar como XML. Defina una vista XML utilizando AXSD sobre los datos relacionales. La vista XML permite efectuar una carga masiva de datos XML en las tablas así como consultar y actualizar los datos relacionales utilizando dicha vista. Este modelo es útil si hay que intercambiar datos que contienen marcado XML con otras aplicaciones, mientras las aplicaciones SQL se ejecutan ininterrumpidamente.  
  
### <a name="hybrid-model"></a>Modelo híbrido  
 Con frecuencia, para crear modelos de datos, resulta apropiada una combinación de columnas de tipo de datos relacionales y **xml** . Algunos valores de los datos XML se pueden almacenar en columnas relacionales y, el resto, o el conjunto de valores XML, en una columna XML. De este modo, se puede obtener un mejor rendimiento ya que se tiene más control sobre los índices creados en las columnas relacionales y las características de bloqueo.  
  
 Los valores para almacenar en columnas relacionales dependen de la carga de trabajo. Por ejemplo, si se recuperan todos los valores XML basados en la expresión de ruta de acceso, /Customer/@CustId, promoviendo el valor del atributo **CustId** a una columna relacional e indexándolo, se puede lograr un mejor rendimiento en las consultas. Por otra parte, si los datos XML se distribuyen ampliamente y sin redundancias en columnas relacionales, el costo del reensamblado puede ser importante.  
  
 En el caso de datos XML muy estructurados, por ejemplo, el contenido de una tabla se ha convertido en XML; se pueden asignar todos los valores a columnas relacionales y, posiblemente, usar la tecnología de vistas XML.  
  
## <a name="granularity-of-xml-data"></a>Granularidad de los datos XML  
 La granularidad de los datos XML almacenados en una columna XML es muy importante para los bloqueos y, en menor medida, para las actualizaciones. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usa el mismo mecanismo de bloqueo tanto para datos XML como no XML. Por lo tanto, un bloqueo de nivel de fila provoca que todas las instancias XML de la fila queden bloqueadas. Cuando la granularidad es grande, el bloqueo de instancias XML grandes provoca una disminución del rendimiento en un escenario multiusuario. Por otra parte, una distribución amplia provoca una pérdida de la encapsulación de objetos e incrementa el costo del reensamblado.  
  
 Para lograr un buen diseño, es importante alcanzar un equilibrio entre los requisitos necesarios para crear modelos de datos y las características de bloqueo y actualización. Sin embargo, en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], el tamaño de las instancias XML almacenadas realmente no es tan importante.  
  
 Por ejemplo, las actualizaciones de una instancia XML se efectúan utilizando el nuevo soporte para actualizaciones parciales de objetos binarios grandes (BLOB) y de índices en las que la instancia XML almacenada existente se compara con su versión actualizada. La actualización parcial de objetos binarios grandes (BLOB) realiza una comparación diferencial entre las dos instancias XML y únicamente actualiza las diferencias. Las actualizaciones parciales de índices solo modifican aquellas filas que se deben cambiar en el índice XML.  
  
## <a name="limitations-of-the-xml-data-type"></a>Limitaciones del tipo de datos xml  
 Tenga en cuenta que el tipo de datos **xml** tiene las limitaciones siguientes:  
  
-   La representación almacenada de las instancias del tipo de datos **xml** no puede superar los 2 GB.  
  
-   No puede usarse como un subtipo de una instancia de **sql_variant** .  
  
-   No admite la conversión a **text** ni a **ntext**. Use en su lugar **varchar(max)** o **nvarchar(max)** .  
  
-   No puede compararse ni ordenarse. Esto significa que un tipo de datos **xml** no puede utilizarse en una instrucción GROUP BY.  
  
-   No puede utilizarse como parámetro de ninguna función integrada escalar que no sea ISNULL, COALESCE o DATALENGTH.  
  
-   No puede utilizarse como columna de clave de un índice. Sin embargo, puede incluirse en forma de datos en un índice clúster o puede agregarse explícitamente a un índice no clúster mediante el uso de la palabra clave INCLUDE al crear el índice no clúster.  

- Los elementos XML se pueden anidar hasta 128 niveles.
  
## <a name="see-also"></a>Consulte también  
 [Ejemplos de importación y exportación en bloque de documentos XML &#40;SQL Server&#41;](../../relational-databases/import-export/examples-of-bulk-import-and-export-of-xml-documents-sql-server.md)  
  
  
