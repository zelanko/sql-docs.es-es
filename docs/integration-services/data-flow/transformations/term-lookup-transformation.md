---
title: Transformación Búsqueda de términos | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.dts.designer.termlookuptrans.f1
- sql13.dts.designer.termlookup.termlookup.f1
- sql13.dts.designer.termlookup.referencetable.f1
- sql13.dts.designer.termlookup.advanced.f1
helpviewer_keywords:
- extracting data [Integration Services]
- match extracted terms [Integration Services]
- text extraction [Integration Services]
- term extractions [Integration Services]
- lookups [Integration Services]
- counting extracted items
- Term Lookup transformation
ms.assetid: 3c0fa2f8-cb6a-4371-b184-7447be001de1
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 61dad85fb7857b8694712f79b860f58d88e7d650
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 03/30/2020
ms.locfileid: "71291207"
---
# <a name="term-lookup-transformation"></a>Búsqueda de términos, transformación

[!INCLUDE[ssis-appliesto](../../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  La transformación Búsqueda de términos compara los términos extraídos del texto en una columna de entrada de transformación con los términos de una tabla de referencia. A continuación, cuenta la cantidad de veces que un término aparece en la tabla de búsqueda en el conjunto de datos de entrada y escribe el recuento junto con el término de la tabla de referencia en columnas en la salida de transformación. Esta transformación resulta útil para crear una lista personalizada de palabras basada en el texto de entrada, que incluye estadísticas de frecuencia de aparición de palabras.  
  
 Antes de que la transformación Búsqueda de términos realice una búsqueda, extrae palabras del texto en una columna de entrada aplicando el mismo método que la transformación Extracción de términos:  
  
-   El texto se divide en frases.  
  
-   Las frases se dividen en palabras.  
  
-   Las palabras se normalizan.  
  
 Para personalizar de forma adicional cuáles son los términos que deben coincidir, la transformación Búsqueda de términos puede configurarse para obtener coincidencias que distingan mayúsculas de minúsculas.  
  
## <a name="matches"></a>Coincide  
 La transformación Búsqueda de términos realiza una búsqueda y devuelve un valor aplicando las siguientes reglas:  
  
-   Si la transformación se configura para obtener coincidencias que distingan mayúsculas de minúsculas, se descartan las coincidencias que no pasan la comparación con distinción de mayúsculas y minúsculas. Por ejemplo, *estudiante* y *ESTUDIANTE* se consideran palabras diferentes.  
  
    > [!NOTE]  
    >  Una palabra sin mayúsculas puede coincidir con una palabra que aparece con mayúscula inicial al principio de una frase. Por ejemplo, la coincidencia entre *estudiante* y *Estudiante* resulta correcta cuando *Estudiante* es la primera palabra de una frase.  
  
-   Si la forma plural del nombre o frase existe en la tabla de referencia, la búsqueda coincide solo con la forma plural del nombre o frase. Por ejemplo, se contarían todas las instancias de *estudiantes* independientemente de las instancias de *estudiante*.  
  
-   Si solo se encuentra la forma singular de la palabra en la tabla de referencia, las formas singular y plural de la palabra o frase coinciden con la forma singular. Por ejemplo, si la tabla de búsqueda contiene la palabra *estudiante*y la transformación encuentra las palabras *estudiante* y *estudiantes*, ambas palabras se contarían como coincidencia del término buscado *estudiante*.  
  
-   Si el texto de la columna de entrada es una frase lematizada, solo la última palabra en la frase se ve afectada por la normalización. Por ejemplo, la versión lematizada de *citas con los médicos* es *cita con los médicos*.  
  
 Cuando un elemento de búsqueda contiene términos que se superponen en el conjunto de referencia (es decir, un subtérmino se encuentra en más de un registro de referencia), la transformación Búsqueda de términos solo devuelve un resultado de búsqueda. En el siguiente ejemplo se muestra el resultado cuando un elemento de la búsqueda contiene un subtérmino que se superpone. El subtérmino que se superpone en este caso es *Windows*, que se encuentra en dos términos de referencia. Sin embargo, la transformación no devuelve dos resultados, sino únicamente un solo término de referencia, *Windows*. No se devuelve el segundo término de referencia, *Windows 7 Professional*.  
  
|Elemento|Value|  
|----------|-----------|  
|Término de entrada|Windows 7 Professional|  
|Términos de referencia|Windows, Windows 7 Professional|  
|Output|Windows|  
  
 La transformación Búsqueda de términos puede obtener coincidencias de nombres y frases que contienen caracteres especiales, y los datos en la tabla de referencia pueden incluir estos caracteres. Los caracteres especiales son los siguientes: %, @, &, $, #, \*, :, ;, ., **,** , !, ?, \<, >, +, =, ^, ~, |, \\, /, (, ), [, ], {, }, " y '.  
  
## <a name="data-types"></a>Tipo de datos  
 La transformación Búsqueda de términos solo puede usar una columna que tenga el tipo de datos DT_WSTR o DT_NTEXT. Si una columna contiene texto, pero no tiene uno de estos tipos de datos, la transformación Conversión de datos puede agregar una columna con el tipo de datos DT_WSTR o DT_NTEXT al flujo de datos y copiar los valores de columnas en la nueva columna. La salida de transformación Conversión de datos posteriormente se puede usar como la entrada para la transformación Búsqueda de términos. Para más información, consulte [Data Conversion Transformation](../../../integration-services/data-flow/transformations/data-conversion-transformation.md).  
  
## <a name="configuration-the-term-lookup-transformation"></a>Configuración de la transformación Búsqueda de términos  
 Las columnas de entrada de la transformación Búsqueda de términos incluyen la propiedad InputColumnType, que indica el uso de la columna. InputColumnType puede incluir los valores siguientes:  
  
-   El valor 0 indica que la columna se pasa a la salida solamente y no se utiliza en la búsqueda.  
  
-   El valor 1 indica que la columna se usa en la búsqueda solamente.  
  
-   El valor 2 indica que la columna se pasa a la salida y también se utiliza en la búsqueda.  
  
 Las columnas de salida de transformación cuya propiedad InputColumnType se establece en 0 o 2 incluyen la propiedad CustomLineageID para una columna, que contiene el identificador de linaje asignado a la columna por un componente de flujo de datos requerido.  
  
 La transformación Búsqueda de términos agrega dos columnas a la salida de transformación, que se denomina de forma predeterminada **Term** y **Frequency**. **Term** contiene un término de la tabla de búsqueda y **Frequency** contiene el número de veces que el término en la tabla de referencia aparece en el conjunto de datos de entrada establecidos. Estas columnas no incluyen la propiedad CustomLineageID.  
  
 La tabla de búsqueda debe ser una tabla en una base de datos de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] o de Access. Si la salida de transformación Extracción de términos se guarda en una tabla, esta tabla se puede usar como tabla de referencia, pero también se pueden usar otras tablas. El texto en archivos planos, libros de Excel u otros orígenes se debe importar a una base de datos de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] o de Access antes de poder usar la transformación Búsqueda de términos.  
  
 La transformación Búsqueda de términos usa una conexión OLE DB independiente para conectarse a la tabla de referencia. Para más información, consulte [OLE DB Connection Manager](../../../integration-services/connection-manager/ole-db-connection-manager.md).  
  
 La transformación Búsqueda de términos funciona en un modo de almacenamiento previo en caché completo. En el tiempo de ejecución, la transformación Búsqueda de términos lee los términos de la tabla de referencia y los almacena en su memoria privada antes de que procese cualquier fila de entrada de transformación.  
  
 Debido a que los términos en una columna de entrada pueden repetirse, la salida de transformación Búsqueda de términos normalmente tiene más filas que la entrada de la transformación.  
  
 La transformación tiene una entrada y una salida. No admite salidas de error.  
  
 Puede establecer propiedades a través del Diseñador de [!INCLUDE[ssIS](../../../includes/ssis-md.md)] o mediante programación.  
  
 Para obtener más información acerca de las propiedades que puede establecer a través del cuadro de diálogo **Editor avanzado** o mediante programación, haga clic en uno de los temas siguientes:  
  
-   [Common Properties](https://msdn.microsoft.com/library/51973502-5cc6-4125-9fce-e60fa1b7b796)  
  
-   [Propiedades personalizadas de transformación](../../../integration-services/data-flow/transformations/transformation-custom-properties.md)  
  
 Para más información sobre cómo establecer propiedades, vea [Establecer las propiedades de un componente de flujo de datos](../../../integration-services/data-flow/set-the-properties-of-a-data-flow-component.md).  
  
## <a name="term-lookup-transformation-editor-term-lookup-tab"></a>Editor de transformación Búsqueda de términos (pestaña Búsqueda de términos)
  Use la pestaña **Búsqueda de términos** del cuadro de diálogo **Editor de transformación Búsqueda de términos** para asignar una columna de entrada a una columna de búsqueda en una tabla de referencia y para proporcionar un alias a cada columna de salida.  
  
### <a name="options"></a>Opciones  
 **Columnas de entrada disponibles**  
 Con las casillas, seleccione las columnas de entrada que se van a pasar directamente a la salida sin cambios. Arrastre una columna de entrada a la lista **Columnas de referencia disponibles** para asignarla a una columna de búsqueda en la tabla de referencia. Las columnas de entrada y búsqueda deben coincidir en los tipos de datos admitidos, DT_NTEXT o DT_WSTR. Seleccione una línea de asignación y haga clic con el botón derecho para editar las asignaciones en el cuadro de diálogo [Crear relaciones](../../../integration-services/data-flow/transformations/create-relationships.md) .  
  
 **Columnas de referencia disponibles**  
 Vea las columnas disponibles en la tabla de referencia. Elija la columna que contiene la lista de términos que coincidirán.  
  
 **Columna de paso a través**  
 Seleccione las columnas de entrada disponibles de la lista. Las selecciones se reflejan en las casillas activadas en la tabla **Columnas de entrada disponibles** .  
  
 **Alias de columna de salida**  
 Escriba un alias para cada columna de salida. El valor predeterminado es el nombre de la columna; no obstante, puede elegir un nombre descriptivo exclusivo.  
  
 **Configurar la salida de errores**  
 Use el cuadro de diálogo [Configurar la salida de errores](https://msdn.microsoft.com/library/5f8da390-fab5-44f8-b268-d8fa313ce4b9) para especificar las opciones de control de errores de las filas que provocan errores.  
  
## <a name="term-lookup-transformation-editor-reference-table-tab"></a>Editor de transformación Búsqueda de términos (pestaña Tabla de referencia)
  Use la pestaña **Tabla de referencia** del cuadro de diálogo **Editor de transformación Búsqueda de términos** para especificar la conexión con la tabla de referencia (búsqueda).  
  
### <a name="options"></a>Opciones  
 **Administrador de conexiones OLE DB**  
 Seleccione un administrador de conexiones de la lista o cree una conexión haciendo clic en **Nuevo**.  
  
 **Nuevo**  
 Cree una conexión mediante el cuadro de diálogo **Configurar el administrador de conexiones OLE DB** .  
  
 **Nombre de la tabla de referencia**  
 Seleccione una tabla de búsqueda o una vista de la base de datos; para ello, seleccione un elemento de la lista. La tabla o vista debe contener una columna con una lista de términos con los que se pueda comparar el texto de la columna de origen.  
  
 **Configurar la salida de errores**  
 Use el cuadro de diálogo [Configurar la salida de errores](https://msdn.microsoft.com/library/5f8da390-fab5-44f8-b268-d8fa313ce4b9) para especificar las opciones de control de errores de las filas que provocan errores.  
  
## <a name="term-lookup-transformation-editor-advanced-tab"></a>Editor de transformación Búsqueda de términos (pestaña Avanzadas)
  Use la pestaña **Avanzadas** del cuadro de diálogo **Editor de transformación Búsqueda de términos** para especificar si en la búsqueda es necesario distinguir mayúsculas de minúsculas.  
  
### <a name="options"></a>Opciones  
 **Utilizar búsqueda de términos con distinción de mayúsculas y minúsculas**  
 Indique si desea que en la búsqueda se distingan las mayúsculas de las minúsculas. El valor predeterminado es **False**.  
  
 **Configurar la salida de errores**  
 Use el cuadro de diálogo [Configurar la salida de errores](https://msdn.microsoft.com/library/5f8da390-fab5-44f8-b268-d8fa313ce4b9) para especificar las opciones de control de errores de las filas que provocan errores.  
  
## <a name="see-also"></a>Consulte también  
 [Referencia de errores y mensajes de Integration Services](../../../integration-services/integration-services-error-and-message-reference.md)   
 [Transformación Extracción de términos](../../../integration-services/data-flow/transformations/term-extraction-transformation.md)  
  
