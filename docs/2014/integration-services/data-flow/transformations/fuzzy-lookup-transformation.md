---
title: Transformación Búsqueda aproximada | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.fuzzylookuptrans.f1
helpviewer_keywords:
- cleaning data
- comparing data
- token delimiters [Integration Services]
- temporary indexes [Integration Services]
- temporary tables [Integration Services]
- Fuzzy Lookup transformation
- reference tables [Integration Services]
- match similar data [Integration Services]
- replacing missing values
- correcting data [Integration Services]
- cache [Integration Services]
- standardizing data [Integration Services]
- lookups [Integration Services]
- confidence scores [Integration Services]
- fuzzy matches
- missing values replaced [Integration Services]
- similarity thresholds [Integration Services]
ms.assetid: 019db426-3de2-4ca9-8667-79fd9a47a068
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: d0b77d45ca55adaa85e4e37e9da817f325ce0fc7
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "62900336"
---
# <a name="fuzzy-lookup-transformation"></a>Búsqueda aproximada, transformación
  La Transformación Búsqueda aproximada realiza tareas de limpieza de datos como normalizar datos, corregir datos y proporcionar valores que faltan.  
  
> [!NOTE]  
>  Para obtener información más detallada sobre la transformación Búsqueda aproximada, incluidas las limitaciones de rendimiento y memoria, vea las notas del producto [Búsqueda aproximada y Agrupación aproximada en SQL Server Integration Services 2005](https://go.microsoft.com/fwlink/?LinkId=96604).  
  
 La transformación Búsqueda aproximada difiere de la Búsqueda aproximada en su uso de coincidencia aproximada. La transformación Búsqueda utiliza una combinación de igualdad para localizar los registros que coinciden en la tabla de referencia. Devuelve los registros que tienen al menos un registro coincidente y devuelve registros que no tienen registros coincidentes. En cambio, la transformación Búsqueda aproximada emplea la coincidencia aproximada para devolver una o más coincidencias similares en la tabla de referencia.  
  
 La transformación Búsqueda aproximada suele ir después de una transformación Búsqueda en un flujo de datos de paquete. Primero, la transformación Búsqueda intenta encontrar una coincidencia exacta. Si no lo consigue, la transformación Búsqueda aproximada proporciona coincidencias similares de la tabla de referencia.  
  
 La transformación necesita acceso a un origen de datos de referencia que contenga los valores que se utilizan para limpiar y ampliar los datos de entrada. El origen de los datos de referencia debe ser una tabla de una base de datos de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] . La coincidencia entre el valor en una columna de entrada y el valor en la tabla de referencia puede ser exacta o aproximada. Sin embargo, la transformación requiere que se configure al menos una coincidencia de columna para la coincidencia aproximada. Si desea buscar únicamente coincidencias exactas, utilice la transformación Búsqueda.  
  
 Esta transformación tiene una entrada y una salida.  
  
 Para la coincidencia aproximada, solo se pueden utilizar columnas de entrada con tipos de datos `DT_WSTR` y `DT_STR`. Para la búsqueda exacta se puede utilizar cualquier tipo de datos DTS, excepto `DT_TEXT`, `DT_NTEXT`y `DT_IMAGE`. Para obtener más información, vea [Integration Services Data Types](../integration-services-data-types.md). Las columnas que participan en la combinación entre la entrada y la tabla de referencia deben tener tipos de datos compatibles. Por ejemplo, es válido combinar una columna con el tipo de datos `DT_WSTR` DTS en una columna con el [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] `nvarchar` tipo de datos, pero no es válido combinar una columna con `DT_WSTR` el tipo de datos en una columna `int` con el tipo de datos.  
  
 Puede personalizar esta transformación, especificando la cantidad máxima de memoria, el algoritmo de comparación de filas y el almacenamiento en caché de índices y tablas de referencia que utiliza la transformación.  
  
 La cantidad de memoria que usa la transformación Búsqueda aproximada se puede configurar al establecer la propiedad personalizada MaxMemoryUsage. Puede especificar el número de megabytes (MB) o utilizar el valor 0, lo que permite a la transformación utilizar una cantidad de memoria dinámica en función de sus necesidades y de la memoria física disponible. La propiedad personalizada MaxMemoryUsage se puede actualizar a través de una expresión de propiedad, al cargar el paquete. Para más información, vea [Expresiones de Integration Services &#40;SSIS&#41;](../../expressions/integration-services-ssis-expressions.md), [Usar expresiones de propiedad en paquetes](../../expressions/use-property-expressions-in-packages.md) y [Propiedades personalizadas de transformación](transformation-custom-properties.md).  
  
## <a name="controlling-fuzzy-matching-behavior"></a>Controlar el comportamiento de la coincidencia aproximada  
 La transformación Búsqueda aproximada incluye tres características para personalizar la búsqueda realiza: el número máximo de coincidencias que se van a devolver por fila de entrada, delimitadores de token y umbrales de similitud.  
  
 La transformación devuelve cero o más coincidencias, hasta alcanzar el número especificado. Especificar un número máximo de coincidencias no garantiza que la transformación devuelva ese número de coincidencias; solo garantiza que la transformación devolverá, como máximo, ese número de coincidencias. Si establece el número máximo de coincidencias en un valor mayor que 1, la salida de transformación puede incluir más de una fila por búsqueda y algunas de las filas pueden ser duplicados.  
  
 La transformación proporciona un conjunto predeterminado de delimitadores que se utilizan para dividir los datos en tokens, pero puede agregar delimitadores de token que se adapten a las necesidades de sus datos. La propiedad Delimiters contiene los delimitadores predeterminados. La división de los datos en tokens es importante, ya que define las unidades de los datos que se compararán con otras.  
  
 Los umbrales de similitud se pueden establecer en el nivel de componente y de combinación. El umbral de similitud en el nivel de combinación solo está disponible cuando la transformación realiza una búsqueda de coincidencias aproximadas entre las columnas de la entrada y la tabla de referencia. El intervalo de similitud es de 0 a 1. Cuanto más se acerque el umbral a 1, más similares deberán ser las filas y las columnas para ser calificadas como duplicados. El umbral de similitud se especifica estableciendo la propiedad MinSimilarity en los niveles de componente y de combinación. Para satisfacer la similitud especificada en el nivel de componente, todas las filas deben tener una similitud en todas las coincidencias igual o superior al umbral de similitud especificado en el nivel de componente. Es decir, no puede especificar una coincidencia muy próxima en el nivel de componente, a menos que las coincidencias en el nivel de fila o de combinación sean igual de próximas.  
  
 Cada coincidencia incluye una puntuación de similitud y una puntuación de confianza. La puntuación de similitud es una medida matemática de la similitud del texto entre el registro de entrada y el registro que la transformación Búsqueda aproximada devuelve de la tabla de referencia. La puntuación de confianza es una medida de la probabilidad de que un valor determinado sea la mejor coincidencia de todas las que se encuentran en la tabla de referencia. La puntuación de confianza asignada a un registro depende de los demás registros coincidentes devueltos. Por ejemplo, una coincidencia entre *St.* y *Saint* devuelve una puntuación de similitud baja, independientemente de las demás coincidencias. Si *Saint* es la única coincidencia devuelta, la puntuación de confianza será alta. Si aparecen *Saint* y *St.* en la tabla de referencia, la confianza para *St.* será alta y para *Saint* será baja. Sin embargo, una similitud alta no necesariamente significa una confianza alta. Por ejemplo, si está buscando el valor *Chapter 4*, los valores devueltos *Chapter 1*, *Chapter 2*y *Chapter 3* tendrán una puntuación de similitud alta, pero una puntuación de confianza baja, ya que no está claro cuál de los resultados es la mejor coincidencia.  
  
 La puntuación de similitud se representa mediante un valor decimal entre 0 y 1; una puntuación de similitud 1 significa una coincidencia exacta entre el valor de la columna de entrada y el valor de la tabla de referencia. La puntuación de confianza, que también es un valor decimal entre 0 y 1, indica la confianza de la coincidencia. Si no se encuentra ninguna coincidencia útil, se asignan las puntuaciones de similitud y confianza 0 a la fila, y las columnas de salida copiadas de la tabla de referencia contienen valores NULL.  
  
 En ocasiones, la búsqueda aproximada no localiza coincidencias apropiadas en la tabla de referencia. Esto puede ocurrir si el valor de entrada que se utiliza en una búsqueda es una sola palabra corta. Por ejemplo, *helo* no se corresponde con el valor *hello* de una tabla de referencia si no hay otros tokens presentes en esa columna o en cualquier otra columna de la fila.  
  
 Las columnas de salida de transformación incluyen las columnas de entrada marcadas como columnas de paso, las columnas seleccionadas en la tabla de búsqueda y las siguientes columnas adicionales:  
  
-   **_Similarity**, una columna que describe la similitud entre los valores de las columnas de entrada y de referencia.  
  
-   **_Confidence**, una columna que describe la calidad de la coincidencia.  
  
 La transformación utiliza la conexión a la base de datos de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] para crear las tablas temporales que utiliza el algoritmo de coincidencia aproximada.  
  
## <a name="running-the-fuzzy-lookup-transformation"></a>Ejecutar la transformación Búsqueda aproximada  
 Cuando el paquete ejecuta la transformación por primera vez, ésta copia la tabla de referencia, agrega una clave con un tipo de datos entero a la tabla nueva y crea un índice en la columna de clave. Después, la transformación crea un índice, llamado índice de coincidencias, en la copia de la tabla de referencia. El índice de coincidencias almacena los resultados de la división de los valores en tokens en las columnas de entrada de la transformación y posteriormente, la transformación utiliza los tokens en la operación de búsqueda. El índice de coincidencias es una tabla en una base de datos de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] .  
  
 Cuando se vuelve a ejecutar el paquete, la transformación puede utilizar un índice de coincidencias existente o crear uno. Si la tabla de referencia es estática, el paquete puede evitar el proceso potencialmente costoso de volver a crear el índice para sesiones reiteradas de limpieza de datos. Si elige utilizar un índice existente, el índice se creará la primera vez que se ejecute el paquete. Si varias transformaciones Búsqueda aproximada utilizan la misma tabla de referencia, todas pueden utilizar el mismo índice. Para volver a usar el índice, las operaciones de búsqueda deben ser idénticas; la búsqueda debe utilizar las mismas columnas. Puede asignar un nombre al índice y seleccionar la conexión a la base de datos de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] en la que se guarda el índice.  
  
 Si la transformación guarda el índice de coincidencias, éste se puede mantener de manera automática. Esto significa que cada vez que se actualiza un registro en la tabla de referencia, el índice de coincidencias también se actualiza. Mantener el índice de coincidencias puede ahorrar tiempo de procesamiento, ya que no es necesario volver a crear el índice cuando se ejecuta el paquete. Puede especificar cómo la transformación administra el índice de coincidencias.  
  
 Las opciones del índice de coincidencias se describen en la siguiente tabla.  
  
|Opción|Descripción|  
|------------|-----------------|  
|**GenerateAndMaintainNewIndex**|Crea un índice, lo guarda y lo mantiene. La transformación instala desencadenadores en la tabla de referencia para mantener la tabla de referencia sincronizada con la tabla del índice.|  
|**GenerateAndPersistNewIndex**|Crea un índice y lo guarda, pero no lo mantiene.|  
|**GenerateNewIndex**|Crea un índice, pero no lo guarda.|  
|**ReuseExistingIndex**|Vuelve a utilizar un índice existente.|  
  
### <a name="maintenance-of-the-match-index-table"></a>Mantenimiento de la tabla del índice de coincidencias  
 La opción **GenerateAndMaintainNewIndex** instala desencadenadores en la tabla de referencia para mantener la tabla del índice de coincidencias sincronizada con la tabla de referencia. Si tiene que quitar el desencadenador instalado, debe ejecutar el procedimiento almacenado **sp_FuzzyLookupTableMaintenanceUnInstall** y proporcionar el nombre especificado en la propiedad MatchIndexName como valor del parámetro de entrada.  
  
 No debe eliminar la tabla del índice de coincidencias mantenida antes de ejecutar el procedimiento almacenado **sp_FuzzyLookupTableMaintenanceUnInstall** . Si elimina la tabla del índice de coincidencias, los desencadenadores de la tabla de referencia no se ejecutarán correctamente. Todas las actualizaciones posteriores de la tabla de referencia generarán errores hasta que quite manualmente los desencadenadores de la tabla de referencia.  
  
 El comando SQL TRUNCATE TABLE no invoca desencadenadores DELETE. Si se utiliza el comando TRUNCATE TABLE en la tabla de referencia, la tabla de referencia y el índice de coincidencias dejarán de estar sincronizados y la Transformación Búsqueda aproximada generará un error. Mientras estén instalados en la tabla de referencia los desencadenadores que mantienen la tabla del índice de coincidencias, debe utilizar el comando SQL DELETE en lugar del comando TRUNCATE TABLE.  
  
> [!NOTE]  
>  Al seleccionar **Mantener el índice almacenado** en la pestaña **Tabla de referencia** del **Editor de transformación Búsqueda aproximada**, la transformación utiliza los procedimientos almacenados administrados para mantener el índice. Estos procedimientos almacenados administrados usan la característica de integración de Common Language Runtime (CLR) en [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. De forma predeterminada, la integración de CLR en [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] no está habilitada. Para utilizar la funcionalidad **Mantener el índice almacenado** , debe habilitar la integración de CLR. Para más información, consulte [Enabling CLR Integration](../../../relational-databases/clr-integration/clr-integration-enabling.md).  
>   
>  Dado que la opción **Mantener el índice almacenado** requiere la integración con CLR, esta característica solo funciona al seleccionar una tabla de referencia en una instancia de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] donde se habilite la integración con CLR.  
  
## <a name="row-comparison"></a>Comparar filas  
 Al configurar la transformación Búsqueda aproximada, puede especificar el algoritmo de comparación que utiliza la transformación para localizar los registros que coinciden en la tabla de referencia. Si establece la propiedad exhaustiva en `True`, la transformación compara cada fila de la entrada con cada fila de la tabla de referencia. Este algoritmo de comparación puede producir resultados más exactos, pero es probable que la transformación sea más lenta, a menos que la tabla de referencia tenga un número de filas reducido. Si la propiedad exhaustiva está establecida en `True`, toda la tabla de referencia se carga en la memoria. Para evitar problemas de rendimiento, es aconsejable establecer la propiedad exhaustiva en `True` solo durante el desarrollo de paquetes.  
  
 Si la propiedad exhaustiva está establecida en `False`, la transformación búsqueda aproximada devuelve solo las coincidencias que tienen al menos un token indizado o una subcadena (la subcadena se denomina *q-Gram*) en común con el registro de entrada. Para maximizar la eficacia de las búsquedas, solamente se indiza un subconjunto de los tokens de cada fila de la tabla en la estructura de índice invertido que utiliza la transformación Búsqueda aproximada para localizar coincidencias. Cuando el conjunto de datos de entrada es pequeño, puede establecer `True` exhaustivo en para evitar que falten coincidencias para las que no existen tokens comunes en la tabla de índice.  
  
## <a name="caching-of-indexes-and-reference-tables"></a>Almacenar en caché índices y tablas de referencia  
 Al configurar la transformación Búsqueda aproximada, puede especificar si la transformación almacenará parcialmente en caché el índice y la tabla de referencia antes de que la transformación realice su trabajo. Si establece la propiedad WarmCaches en `True`, el índice y la tabla de referencia se cargan en la memoria. Cuando la entrada tiene muchas filas, el establecimiento de la propiedad `True` WarmCaches en puede mejorar el rendimiento de la transformación. Cuando el número de filas de entrada es pequeño, el establecimiento de la `False` propiedad WarmCaches en puede hacer que la reutilización de un índice grande sea más rápida.  
  
## <a name="temporary-tables-and-indexes"></a>Tablas e índices temporales  
 En tiempo de ejecución, la transformación Búsqueda aproximada crea objetos temporales, como tablas e índices, en la base de datos de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] a la que se conecta la transformación. El tamaño de estas tablas e índices temporales es proporcional al número de filas y tokens de la tabla de referencia y al número de tokens que crea la transformación Búsqueda aproximada; por lo tanto, podría consumir una cantidad importante de espacio en disco. La transformación también consulta estas tablas temporales. Por lo tanto, debe considerar la posibilidad de conectar la transformación Búsqueda aproximada a una instancia de la base de datos de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] que no sea de producción, en especial si el servidor de producción tiene un espacio en disco disponible limitado.  
  
 El rendimiento de esta transformación puede mejorar si las tablas e índices que utiliza están ubicados en el equipo local. Si la tabla de referencia que utiliza la transformación Búsqueda aproximada está en el servidor de producción, debe plantearse copiar la tabla a un servidor que no sea de producción y configurar la transformación Búsqueda aproximada para que tenga acceso a la copia. Haciendo esto, puede evitar que las consultas de búsqueda consuman recursos del servidor de producción. Además, si la transformación “Búsqueda aproximada” mantiene el índice de coincidencia (es decir, si MatchIndexOptionsis se establece en **GenerateAndMaintainNewIndex**), la transformación puede bloquear la tabla de referencia durante la operación de limpieza de datos, lo que evitaría que otros usuarios y aplicaciones accedan a ella.  
  
## <a name="configuring-the-fuzzy-lookup-transformation"></a>Configurar la transformación Búsqueda aproximada  
 Puede establecer propiedades a través del Diseñador de [!INCLUDE[ssIS](../../../includes/ssis-md.md)] o mediante programación.  
  
 Para obtener más información acerca de las propiedades que puede establecer en el cuadro de diálogo **Editor de transformación Búsqueda aproximada** , haga clic en uno de los temas siguientes:  
  
-   [Editor de transformación búsqueda aproximada &#40;pestaña tabla de referencia&#41;](../../fuzzy-lookup-transformation-editor-reference-table-tab.md)  
  
-   [Editor de transformación Búsqueda aproximada &#40;pestaña Columnas&#41;](../../fuzzy-lookup-transformation-editor-columns-tab.md)  
  
-   [Editor de transformación búsqueda aproximada &#40;pestaña avanzadas&#41;](../../fuzzy-lookup-transformation-editor-advanced-tab.md)  
  
 Para obtener más información acerca de las propiedades que puede establecer a través del cuadro de diálogo **Editor avanzado** o mediante programación, haga clic en uno de los temas siguientes:  
  
-   [Common Properties](../../common-properties.md)  
  
-   [Propiedades personalizadas de transformación](transformation-custom-properties.md)  
  
## <a name="related-tasks"></a>Related Tasks  
 Para obtener más detalles sobre cómo establecer las propiedades de un componente de flujo de datos, vea [Establecer las propiedades de un componente de flujo de datos](../set-the-properties-of-a-data-flow-component.md).  
  
## <a name="see-also"></a>Consulte también  
 [Transformación búsqueda](lookup-transformation.md)   
 [Fuzzy Grouping Transformation](fuzzy-grouping-transformation.md)   
 [Transformaciones de Integration Services](integration-services-transformations.md)  
  
  
