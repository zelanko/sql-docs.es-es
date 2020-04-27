---
title: Bases de conocimiento y dominios de DQS | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: data-quality-services
ms.topic: conceptual
ms.assetid: b5879041-db1e-4c6c-b49a-33784ade2942
author: lrtoyou1223
ms.author: lle
manager: craigg
ms.openlocfilehash: a7b3c15af012675bfccecad7e8f74f99882fed11
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/26/2020
ms.locfileid: "65480833"
---
# <a name="dqs-knowledge-bases-and-domains"></a>Bases de conocimiento y dominios de DQS
  En este tema se describe lo qué es una base de conocimiento en [!INCLUDE[ssDQSnoversion](../includes/ssdqsnoversion-md.md)] (DQS). Para limpiar datos, debe tener conocimiento sobre los datos. Para preparar el conocimiento de un proyecto de calidad de datos, se crea y mantiene una base de conocimiento (BC) que DQS puede usar para identificar datos incorrectos o no válidos. Con DQS puede usar procesos asistidos por PC y procesos interactivos para crear, compilar y actualizar la base de conocimiento. El conocimiento de una base de conocimiento se mantiene en dominios, donde cada uno de ellos es específico para un campo de datos. La base de conocimiento es un repositorio de conocimiento sobre los datos que le permite comprenderlos y mantener su integridad.  
  
 Las bases de conocimiento de DQS tienen las siguientes ventajas:  
  
-   La generación de conocimiento sobre los datos es un proceso detallado. El proceso de DQS para extraer conocimiento sobre los datos automáticamente, a partir de datos de muestra, hace que el proceso sea mucho más fácil.  
  
-   DQS le permite ver su análisis de los datos y aumentar el conocimiento de la base de conocimiento por medio de la creación de reglas y modificación de los valores de datos. Esto lo puede hacer de forma repetida con el fin de mejorar el conocimiento con el paso del tiempo.  
  
-   Puede aprovechar el conocimiento existente de calidad de datos si basa una base de conocimiento en una BC existente, de forma que se importa conocimiento de dominios desde archivos en la BC, desde un proyecto nuevo a la BC o bien, mediante la BC predeterminada de DQS, datos de DQS.  
  
-   Puede garantizar la calidad de los datos si los compara con los datos que mantiene un proveedor de datos de referencia.  
  
-   Hay una diferencia clara entre generar una base de conocimiento y aplicarla en el proceso de corrección de datos, el cual ofrece flexibilidad en la forma de generar y actualizar la base de conocimiento.  
  
 El administrador de datos usa la aplicación [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)] para ejecutar y controlar los pasos asistidos por PC y realizar los pasos interactivos.  
  
 La ilustración siguiente muestra los diferentes componentes de una base de conocimiento y un dominio de DQS:  
  
 ![Bases de conocimiento y dominios en DQS](../../2014/data-quality-services/media/dqs-knowledgebasesanddomains.gif "Bases de conocimiento y dominios en DQS")  
  
##  <a name="how-to-create-and-build-a-dqs-knowledge-base"></a><a name="How"></a> Cómo crear y generar una base de conocimiento de DQS  
 Generar una base de conocimiento de DQS conlleva los siguientes procesos y componentes:  
  
 **Detección de conocimiento**  
 Proceso asistido por PC que genera conocimiento en una base de conocimiento mediante el procesamiento de una muestra de datos  
  
 **Administración de dominios**  
 Proceso interactivo que permite al administrador de datos comprobar y modificar el conocimiento que se encuentra en los dominios de la base de conocimiento, donde cada uno de ellos está asociado a un campo de datos. Esto puede incluir la configuración de propiedades en todos los campos, la creación de reglas, la modificación de valores específicos, el uso de servicios de datos de referencia o el establecimiento de relaciones basadas en términos o entre campos.  
  
 **Reference Data Services**  
 Proceso de administración de dominios para validar datos frente a los datos que mantiene y protege un proveedor de datos de referencia.  
  
 **Directiva de coincidencia**  
 Directiva que define cómo procesa DQS los registros para identificar las posibles repeticiones y la ausencia de coincidencias, que se integra en la base de conocimiento en los procesos asistidos por PC y en los procesos interactivos.  
  
##  <a name="knowledge-discovery"></a><a name="Discovery"></a> Detección de conocimiento  
 La creación de la base de conocimiento es un proceso inicialmente asistido por PC. La actividad de detección de conocimiento genera la base de conocimiento; para ello, analiza una muestra de datos para ver si cumplen los criterios de calidad de los datos, buscando incoherencias y errores de sintaxis en los datos, aplicando reglas de dominio y proponiendo cambios en los datos. Este análisis se basa en los algoritmos integrados en DQS.  
  
 El administrador de datos prepara el proceso vinculando una base de conocimiento a una tabla o vista de base de datos de SQL Server que contiene datos de ejemplo similares a los datos que la base de conocimiento utilizará para el análisis. A continuación, el administrador de datos asigna un dominio de la base de conocimiento a cada columna de los datos de ejemplo que se van a analizar. Un dominio puede tratarse de un solo dominio que se asigna a un único campo o puede ser un dominio compuesto formado de varios dominios únicos donde cada uno de ellos se asigna a parte de los datos en un solo campo (vea el tema"Dominios compuestos" a continuación). Cuando se ejecute la detección de conocimiento, DQS extraerá información sobre la calidad de datos de los datos de ejemplo y la situará en los dominios de la base de conocimiento. Cuando haya ejecutado el análisis de detección del conocimiento, tendrá una base de conocimiento con la que puede corregir datos.  
  
 La base de conocimiento de DQS es extensible. Desde la actividad de detección del conocimiento, puede agregar de forma interactiva conocimiento a la base de conocimiento después del análisis de detección del conocimiento asistido por PC. Puede agregar manualmente cambios e importar valores de dominio desde un archivo de Excel. Por otra parte, puede volver a ejecutar el proceso de detección del conocimiento más adelante si los datos de la muestra han cambiado. Puede aplicar más conocimiento desde la actividad de administración de dominios y desde la actividad de búsqueda de coincidencias de datos (se explica más adelante).  
  
 No es necesario realizar el proceso de detección del conocimiento en los mismos datos en que se realiza la corrección de datos. DQS proporciona la flexibilidad para crear conocimiento a partir de un conjunto de campos de la base de datos y aplicarlo a un segundo conjunto de datos relacionados que es necesario limpiar. El administrador de datos puede crear una nueva base de conocimiento desde cero o basarla en una base de conocimiento existente, o puede importar una base de conocimiento desde un archivo de datos. También puede volver a ejecutar la detección del conocimiento en una base de conocimiento existente. Puede mantener varias bases de conocimiento en un único servidor [!INCLUDE[ssDQSServer](../includes/ssdqsserver-md.md)]. También puede conectar varias instancias de una aplicación a la misma base de conocimiento. DQS evita conflictos de simultaneidad bloqueando la base de conocimiento al usuario que la abre en una sesión de administración del conocimiento.  
  
### <a name="case-insensitivity-in-dqs"></a>Sin distinción de mayúsculas y minúsculas en DQS  
 Los valores de DQS no distinguen entre mayúsculas y minúsculas. Esto significa que cuando DQS realiza la detección del conocimiento, la administración de dominios o la búsqueda de coincidencias, no distingue valores según las mayúsculas o minúsculas. Si agrega un valor en la administración de valores que sea distinto de otro valor solo porque lleve mayúsculas o minúsculas, se considerarán el mismo valor, pero no sinónimos. Si dos valores que solo se diferencien en el uso de mayúsculas y minúsculas se comparan en el proceso de búsqueda de coincidencias, se considerarán coincidencias exactas.  
  
 Puede, no obstante, controlar el uso de mayúsculas y minúsculas en los valores que exporta en los resultados de la limpieza. Para ello, establezca la propiedad de dominio **Dar formato a la salida para** (vea [Establecer las propiedades de dominio](../../2014/data-quality-services/set-domain-properties.md)) y active la casilla **Estandarizar salida** al exportar los resultados de la limpieza (vea [Limpiar datos mediante el conocimiento de DQS &#40;interno&#41;](../../2014/data-quality-services/cleanse-data-using-dqs-internal-knowledge.md)).  
  
##  <a name="domain-management"></a><a name="Domains"></a>Administración de dominios  
 La administración de dominios permite al administrador de datos cambiar y aumentar de forma interactiva los metadatos generados por la actividad de detección de conocimiento asistido por PC. Cada cambio que realice es para un dominio de la base de conocimiento. En la actividad de administración de dominios, puede hacer lo siguiente:  
  
-   Crear un nuevo dominio. El nuevo dominio se puede vincular a un dominio existente o copiarlo a partir de este.  
  
-   Establecer las propiedades de dominio que se aplican a cada término en el dominio.  
  
-   Aplicar reglas de dominio que efectúen la validación o la normalización para un intervalo de valores que defina.  
  
-   Aplicar de forma interactiva los cambios a cualquier valor de datos específico del dominio.  
  
-   Usar el corrector ortográfico de DQS para comprobar la sintaxis, la ortografía y la estructura de la frases de los valores de cadena.  
  
-   Importar un dominio desde un archivo de datos .dqs o los valores del dominio de un archivo de Microsoft Excel.  
  
-   Importar valores que se han encontrado en un proceso de limpieza en un proyecto de calidad de datos de vuelta a una base de conocimiento.  
  
-   Adjuntar un dominio a los datos de referencia que mantiene un proveedor de datos de referencia, con el resultado de que los valores de dominio se comparan con los datos de referencia para determinar su integridad y corrección. Asimismo, puede establecer valores del proveedor de datos.  
  
-   Aplicar relaciones basadas en términos para un único dominio.  
  
 Cuando se completa la actividad de administración de dominios, puede publicar la base de conocimiento en un proyecto de datos.  
  
### <a name="setting-domain-properties"></a>Establecer las propiedades de dominio  
 Las propiedades de dominio definen y controlan el procesamiento que se va a aplicar a los valores asociados. Puede establecer el tipo de datos y el idioma de los valores, especificar que los datos de origen se limpiarán con el valor inicial (si se desactiva esta opción, los datos de origen se limpiarán con el término correcto pero no con el valor inicial), asegurar la normalización de datos configurando el formato que se aplicará cuando se generen los valores de datos del dominio, y definir los algoritmos (error de sintaxis, corrector ortográfico, y normalización de cadena) que se aplicarán.  
  
### <a name="reference-data-services"></a>Reference Data Services  
 En el proceso de administración de dominios, puede adjuntar datos de referencia en línea a un dominio. De esta forma compara los datos en el dominio con los datos que mantiene un proveedor de datos de referencia. Primero debe configurar el proveedor de datos de referencia mediante las funciones de configuración de DQS en la sección de **Administración** de aplicación de [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)] . Para obtener más información, consulte [Reference Data Services in DQS](../../2014/data-quality-services/reference-data-services-in-dqs.md).  
  
### <a name="applying-domain-rules"></a>Aplicar reglas de dominio  
 Puede crear reglas de dominio para la validación de datos. Las reglas de dominio garantizan la exactitud de los datos, e incluyen desde una restricción básica, como los posibles términos que puede ser un valor de cadena, hasta una expresión regular más compleja, como los formatos válidos para una dirección de correo electrónico.  
  
 Respecto a los dominios compuestos, puede crear una regla de CD que especifique una relación entre un valor en un solo dominio y un valor en otro dominio único, donde ambos forman parte de un dominio compuesto.  
  
### <a name="setting-domain-values"></a>Establecer valores de dominio  
 Una vez haya generado una base de conocimiento, puede rellenar y mostrar valores de datos en cada dominio de la base de conocimiento. Después de haber realizado la detección del conocimiento, DQS mostrará el número de veces que aparece cada término, cuál es el estado de cada término y las revisiones que se proponen. Puede administrar este conocimiento como sigue:  
  
-   Cambiar el estado de un valor, corregirlo, marcar un error o establecerlo como no válido  
  
-   Agregar un valor específico o eliminar un valor específico en la base de conocimiento  
  
-   Cambiar la relación de un valor con otro valor, lo cual incluye designar un reemplazo para un término que tenga un error o no sea válido  
  
-   Agregar, quitar o cambiar conocimiento asociado al dominio.  
  
 El usuario puede crear los valores de forma específica o dentro de las funcionalidades de detección o importación de datos. De esta forma, podrá alinear el dominio al negocio, lo cual facilita la implementación de su capacidad de extensión.  
  
 Puede establecer valores de dominio en la actividad de administración de dominios o en el paso de administración de valores del dominio al final de la actividad de detección de conocimiento. La funcionalidad establecer valores de dominio es la misma en ambas actividades.  
  
### <a name="setting-term-relations"></a>Establecer relaciones de términos  
 En la administración de dominios, puede especificar una relación basada en términos para un solo dominio; para ello, se especifica un cambio para un único valor.  
  
### <a name="composite-domains"></a>Dominios compuestos  
 Un dominio compuesto es una estructura formada por dos dominios únicos o más que contienen cada uno de ellos conocimiento de datos comunes. Entre los ejemplos de datos que pueden tratar los dominios compuestos se encuentran los nombres y los apellidos en los campos de nombre, el número y la calle del inmueble, la ciudad, la provincial el código postal y el país en un campo de dirección. Cuando asigna un solo campo a un dominio compuesto, DQS analiza los datos de ese campo en los diversos dominios que componen el dominio compuesto.  
  
 En ocasiones, un único dominio no representa datos de campo en su totalidad. Si se agrupan dos o más dominios en un dominio compuesto, podrá representar los datos de forma eficaz. A continuación, se presentan algunas ventajas del uso de los dominios compuestos:  
  
-   El análisis de distintos dominios únicos que componen un dominio compuesto puede ser una forma más eficaz de evaluar la calidad de los datos.  
  
-   Cuando se utiliza un dominio compuesto, también se pueden crear reglas para todos los dominios con el fin comprobar que la relación entre los datos de varios dominios es adecuada. Por ejemplo, puede comprobar que la cadena "Londres" en un dominio de ciudad se corresponde con la cadena "Inglaterra" en un dominio de país. Observe que las reglas para varios dominios se tienen en cuenta después de las reglas de dominio.  
  
-   Los datos en dominios compuestos se pueden adjuntar a un origen de datos de referencia, en cuyo caso el dominio compuesto se enviará al proveedor de datos de referencia. Esto se suele hacer con datos de direcciones.  
  
 La forma en que se analizan los datos que representan un dominio compuesto está determinada por las propiedades compuestas de dominio. Los datos se pueden analizar por un delimitador, por el orden de los dominios o basarse en el conocimiento de los dominios conectados al dominio compuesto (seleccionando la propiedad **Usar el análisis de bases de conocimiento** en el dominio compuesto). Para obtener más información, consulte [Set Composite Domain Properties](../../2014/data-quality-services/create-a-composite-domain.md#CompositeDomainProperties).  
  
 Los dominios compuestos se administran de manera diferente a los dominios únicos. En los dominios compuestos, no se administran valores; sí se hace para los dominios únicos que componen el dominio compuesto. Sin embargo, en la lista de dominios de la actividad de administración de dominios, puede ver las relaciones entre los diferentes valores en un dominio compuesto, así como las estadísticas que se aplican. Por ejemplo, puede ver el número de instancias que pertenecen a una sola dirección que está compuesta por los mismos cinco valores de cadena. En el paso de detección de la actividad de detección de conocimiento, se realiza la creación de perfiles en los dominios únicos dentro de un dominio compuesto, no en el dominio compuesto. Sin embargo, en la limpieza interactiva, se limpian los datos en el dominio compuesto, no en los dominios únicos.  
  
 Se puede realizar la búsqueda de coincidencias en los dominios únicos que componen el dominio compuesto, pero no en el dominio compuesto en sí.  
  
##  <a name="data-matching"></a><a name="Matching"></a>Coincidencia de datos  
 Además de realizar cambios manuales en una base de conocimiento mediante la administración de dominios, puede agregar conocimiento coincidente a una base de conocimiento. Al objeto de preparar a DQS para el proceso de eliminación de datos duplicados, debe crear una directiva de búsqueda de coincidencias que vaya a usar DQS para calcular la probabilidad de encontrar coincidencias. La directiva incluye una o varias reglas de búsqueda de coincidencias que crea el administrador de datos para identificar cómo DQS debe comparar filas de datos. El administrador de datos determina qué campos de datos en la fila se deben comparar y el peso que debe tener cada campo en la comparación. El administrador de datos también determinará cuán alta será la probabilidad para que se identifique como coincidencia. DQS agrega las reglas de búsqueda de coincidencias a la base de conocimiento para su uso en el desarrollo de la actividad de búsqueda de coincidencias en el proyecto de calidad de datos.  
  
 Para obtener más información acerca de la base de conocimiento y la búsqueda de coincidencias, vea [Coincidencia de datos](../../2014/data-quality-services/data-matching.md).  
  
## <a name="in-this-section"></a>En esta sección  
 Puede realizar las siguientes operaciones en una base de conocimiento y sus dominios:  
  
|||  
|-|-|  
|Crear, abrir, agregar conocimiento y llevar a cabo la detección en una base de conocimiento|[Crear una base de conocimiento](../../2014/data-quality-services/building-a-knowledge-base.md)|  
|Realizar operaciones de importación y exportación en dominios y bases de conocimiento|[Importar y exportar conocimiento](../../2014/data-quality-services/importing-and-exporting-knowledge.md)|  
|Crear un solo dominio, una regla de dominio, relaciones basadas en términos y cambiar valores de dominio|[Administrar un dominio](../../2014/data-quality-services/managing-a-domain.md)|  
|Crear un dominio compuesto, crear reglas para varios dominios y usar relaciones de valor|[Administrar un dominio compuesto](../../2014/data-quality-services/managing-a-composite-domain.md)|  
|Usar la base de conocimiento predeterminada de DQS integrada en DQS|[Utilizar la base de conocimiento predeterminada de DQS](../../2014/data-quality-services/using-the-dqs-default-knowledge-base.md)|  
  
  
