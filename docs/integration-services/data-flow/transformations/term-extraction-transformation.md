---
title: Transformación Extracción de términos | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.dts.designer.termextractiontrans.f1
- sql13.dts.designer.termextraction.termextraction.f1
- sql13.dts.designer.termextraction.inclusionexclusion.f1
- sql13.dts.designer.termextraction.advanced.f1
helpviewer_keywords:
- word boundaries [Integration Services]
- extracting data [Integration Services]
- sentence boundaries
- word extractions [Integration Services]
- Term Extraction transformation
- tagging words
- normalized data [Integration Services]
- tokenizing text [Integration Services]
- parts of speech [Integration Services]
- text extraction [Integration Services]
- term extractions [Integration Services]
- stemming words [Integration Services]
ms.assetid: d0821526-1603-4ea6-8322-2d901568fbeb
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 3ea9c1c590b9f09f1bd31b491d9b0170f59f8406
ms.sourcegitcommit: 7ccb8f28eafd79a1bddd523f71fe8b61c7634349
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 03/20/2019
ms.locfileid: "58282579"
---
# <a name="term-extraction-transformation"></a>Extracción de términos, transformación
  La transformación Extracción de términos extrae términos del texto en una columna de entrada de transformación y luego escribe los términos en una columna de salida de transformación. La transformación funciona solo con texto en inglés y utiliza únicamente su propio diccionario en inglés e información lingüística sobre el idioma inglés.  
  
 Puede usar la transformación Extracción de términos para detectar el contenido de un conjunto de datos. Por ejemplo, el texto que contiene mensajes de correo electrónico puede proporcionar información útil sobre productos, de manera que puede usar la transformación Extracción de términos para extraer los temas de discusión en los mensajes, como una manera de analizar dicha información.  
  
## <a name="extracted-terms-and-data-types"></a>Tipos de datos y términos extraídos  
 La transformación Extracción de términos puede extraer nombres solamente, frases solamente o nombres y frases. Un nombre es un solo sustantivo, una frase se compone de por lo menos dos palabras, de las cuales una es un sustantivo y la otra es un sustantivo o adjetivo. Por ejemplo, si la transformación usa la opción de solo nombres, extrae términos como *bicycle* y *landscape*. Si la transformación usa la opción de frase, extrae términos como *new blue bicycle*, *bicycle helmet*y *boxed bicycles*.  
  
 Los artículos y pronombres no se extraen. Por ejemplo, la transformación Extracción de términos extrae el término *bicycle* (bicicleta) del texto *the bicycle*(la bicicleta), *my bicycle*(mi bicicleta) y *that bicycle*(esa bicicleta).  
  
 La transformación Extracción de términos genera una puntuación para cada término que extrae. La puntuación puede ser un valor TFIDF o simplemente la frecuencia, que es la cantidad de veces en que aparece el término normalizado en la entrada. En cualquier caso, un número real mayor que cero representa la puntuación. Por ejemplo, la puntuación TFIDF podría tener el valor 0,5 y la frecuencia sería un valor como 1,0 o 2,0.  
  
 La salida de transformación Extracción de términos incluye solo dos columnas. Una columna contiene los términos extraídos y la otra columna contiene la puntuación. Los nombres predeterminados de las columnas son **Term** y **Score**. Debido a que la columna de texto de la entrada puede contener varios términos, la salida de transformación Extracción de términos normalmente tiene más filas que la entrada.  
  
 Si los términos extraídos se escriben en una tabla, pueden ser usados por otra transformación de búsqueda, como las transformaciones Búsqueda de términos, Búsqueda aproximada y Búsqueda.  
  
 La transformación Extracción de términos solo funciona con texto en una columna que tenga el tipo de datos DT_WSTR o DT_NTEXT. Si una columna contiene texto, pero no tiene uno de estos tipos de datos, se puede usar la transformación Conversión de datos para agregar una columna con el tipo de datos DT_WSTR o DT_NTEXT al flujo de datos y copiar los valores de columnas en la nueva columna. La salida de transformación Conversión de datos entonces se puede usar como la entrada para la transformación Extracción de términos. Para más información, consulte [Data Conversion Transformation](../../../integration-services/data-flow/transformations/data-conversion-transformation.md).  
  
## <a name="exclusion-terms"></a>Términos de exclusión  
 Opcionalmente, la transformación Extracción de términos puede hacer referencia a una columna en una tabla que contiene términos de exclusión, lo que significa términos que la transformación debe omitir cuando extrae términos de un conjunto de datos. Esto resulta útil cuando un conjunto de términos ya ha sido identificado como insignificante en una actividad o un segmento en concreto, normalmente porque el término aparece con tanta frecuencia que resulta una palabra vacía. Por ejemplo, al extraer términos de un conjunto de datos que contiene información de asistencia al cliente sobre una marca de automóviles concreta, el nombre de la marca se puede excluir porque se menciona con demasiada frecuencia como para que resulte significativo. Por tanto, los valores en la lista de exclusión deben ser personalizados para el conjunto de datos con el que está trabajando.  
  
 Al agregar un término a la lista de exclusión, se excluyen también todos los términos (palabras o frases) que contienen el término. Por ejemplo, si la lista de exclusión incluye la palabra única *data*(datos), también se excluyen todos los términos que contienen esta palabra, como *data*(datos), *data mining*(minería de datos), *data integrity*(integridad de datos) y *data validation* (validación de datos). Si solamente desea excluir los términos compuestos que contienen la palabra *data*(datos), debe agregar explícitamente estos términos compuestos a la lista de exclusión. Por ejemplo, si desea extraer incidencias de *data*(datos), pero excluir *data validation*(validación de datos), debe agregar *data validation* a la lista de exclusión y asegurarse de que *data* (datos) se ha quitado de la lista de exclusión.  
  
 La tabla de referencia debe ser una tabla en una base de datos de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] o de Access. La transformación Extracción de términos usa una conexión OLE DB independiente para conectarse a la tabla de referencia. Para más información, consulte [OLE DB Connection Manager](../../../integration-services/connection-manager/ole-db-connection-manager.md).  
  
 La transformación Extracción de términos trabaja en un modo de almacenamiento previo en caché completo. En el tiempo de ejecución, la transformación Extracción de términos lee los términos de exclusión de la tabla de referencia y los almacena en su memoria privada antes de procesar cualquier fila de entrada de transformación.  
  
## <a name="extraction-of-terms-from-text"></a>Extracción de términos del texto  
 Para extraer términos del texto, la transformación Extracción de términos realiza las siguientes tareas.  
  
### <a name="identification-of-words"></a>Identificador de palabras  
 En primer lugar, la transformación Extracción de términos identifica palabras realizando las siguientes tareas:  
  
-   Separar texto en palabras usando espacios, saltos de línea y otros terminadores de palabras del idioma inglés. Por ejemplo, signos de puntuación como *?* y *:* son caracteres de separación de palabras.  
  
-   Conservar palabras conectadas por guiones o caracteres de subrayado. Por ejemplo, las palabras *copy-protected* y *read-only* se leen como una sola palabra.  
  
-   Mantener intactas las siglas que incluyen puntos. Por ejemplo, *A.B.C.* Company se acorta como **ABC** y **Company**.  
  
-   Dividir palabras con caracteres especiales. Por ejemplo, la palabra *date/time* se extrae como *date* y *time*, *(bicycle)* como *bicycle*y C# se trata como C. Los caracteres especiales se descartan y no se pueden lexicalizar.  
  
-   Reconocer cuando los caracteres especiales, como el apóstrofo, no deben dividir palabras. Por ejemplo, la palabra *bicycle's* no se divide en dos palabras y produce el término único *bicycle* (nombre).  
  
-   Dividir expresiones temporales, expresiones monetarias, direcciones de correo electrónico y direcciones postales. Por ejemplo, la fecha *January 31, 2004* (31 de enero de 2004) se separa en tres tokens *January*, *31*y *2004*.  
  
### <a name="tagged-words"></a>Palabras etiquetadas  
 En segundo lugar, la transformación Extracción de términos etiqueta palabras como una de las siguientes partes de la oración:  
  
-   Un nombre en su forma singular. Por ejemplo, *bicycle* (bicicleta) y *potato*(patata).  
  
-   Un nombre en su forma plural. Por ejemplo, *bicycles* (bicicletas) y *potatoes*(patatas). Todos los nombres plurales que no se lematizan se someten a desinencias.  
  
-   Un nombre propio en su forma singular. Por ejemplo, *April* y *Peter*.  
  
-   Un nombre propio en su forma plural. Por ejemplo, *Aprils* y *Peters*. Para que se haga la lematización de un nombre propio, tiene que formar parte del léxico interno, que se limita a palabras inglesas estándar.  
  
-   Un adjetivo. Por ejemplo, *blue*(azul).  
  
-   Un adjetivo comparativo que compara dos cosas. Por ejemplo, *higher* y *taller*(más alto).  
  
-   Un adjetivo superlativo que identifica una cosa que tiene una calidad por encima o por debajo del nivel de por lo menos otras dos. Por ejemplo, *highest* y *tallest*(el más alto).  
  
-   Un número. Por ejemplo, *62* y *2004*.  
  
 Las palabras que no son una de estas partes de la oración se descartan. Por ejemplo, se descartan los verbos y pronombres.  
  
> [!NOTE]  
>  El etiquetado de las partes de la oración se basa en un modelo estadístico y es posible que no sea completamente exacto.  
  
 Si la transformación Extracción de términos se configura para extraer solo nombres, solamente se extraen las palabras etiquetadas como las formas singular o plural de los nombres y nombres propios.  
  
 Si la transformación Extracción de términos se configura para extraer solo frases, las palabras que se etiquetan como nombres, nombres propios, adjetivos y números se pueden combinar para formar una frase, pero la frase debe tener por lo menos una palabra etiquetada como la forma singular o plural de un nombre o nombre propio. Por ejemplo, la frase *highest mountain* combina una palabra etiquetada como adjetivo superlativo (*highest*) y una palabra etiquetada como nombre (*mountain*).  
  
 Si la Extracción de términos se configura para extraer nombres y frases, se aplican tanto las reglas para nombres como las reglas para frases. Por ejemplo, la transformación extrae *bicycle* (bicicleta) y *beautiful blue bicycle* (bella bicicleta azul) del texto *many beautiful blue bicycles*(muchas bellas bicicletas azules).  
  
> [!NOTE]  
>  Los términos extraídos siguen sujetos a los límites de longitud máxima de términos y al umbral de frecuencia que usa la transformación.  
  
### <a name="stemmed-words"></a>Palabras lematizadas  
 La transformación Extracción de términos también lematiza nombres para extraer solo la forma singular de un nombre. Por ejemplo, la transformación extrae *man* (hombre) de *men*(hombres), *mouse* (ratón) de *mice*(ratones) y *bicycle* (bicicleta) de *bicycles*(bicicletas). La transformación usa su diccionario para lematizar nombres. Los gerundios se tratan como nombres si están en el diccionario.  
  
 La transformación Extracción de términos lematiza palabras a su forma de diccionario, como se muestra en estos ejemplos, mediante el diccionario interno de la transformación Extracción de términos.  
  
-   Quitar la *s* de los sustantivos. Por ejemplo, *bicycles* (bicicletas) pasa a ser *bycicle*.  
  
-   Quitar *es* de los sustantivos. Por ejemplo, *stories* (historias) pasa a ser *story*.  
  
-   Recuperar la forma singular de los nombres irregulares del diccionario. Por ejemplo, *geese* (gansos) pasa a ser *goose*.  
  
### <a name="normalized-words"></a>Palabras normalizadas  
 La transformación Extracción de términos solo normaliza términos con mayúsculas debido a su posición en una oración y utiliza la forma sin mayúsculas en su lugar. Por ejemplo, en las frases *Dogs chase catos* (Perros persiguen gatos) y *Mountain paths are steep*(Los pasos montañosos son escarpados), *Dogs* y *Mountain* se normalizan como *dog* y *mountain*.  
  
 La transformación Extracción de términos normaliza las palabras de manera tal que las versiones con mayúsculas y sin mayúsculas de las palabras no se tratan como términos diferentes. Por ejemplo, en el texto *You see many bicycles in Seattle* (Se ven muchas bicicletas en Seattle) y *Bicycles are blue*(Las bicicletas son azules) *, bicycles* y *Bicycles* se reconocen como el mismo término y la transformación solo conserva *bicycle*. Los nombres propios y las palabras que no se encuentran enumeradas en el diccionario interno no se normalizan.  
  
### <a name="case-sensitive-normalization"></a>Normalización que distingue mayúsculas y minúsculas  
 La transformación Extracción de términos se puede configurar para considerar a las palabras con mayúsculas y minúsculas como términos diferentes o como valores diferentes del mismo término.  
  
-   Si la transformación se configura para reconocer las diferencias de mayúsculas y minúsculas, los términos *Method* y *method* se extraen como dos términos diferentes. Las palabras con mayúsculas que no son la primera palabra en una oración nunca se normalizan y se etiquetan como nombres propios.  
  
-   Si la transformación se configura para no reconocer las diferencias de mayúsculas y minúsculas, los términos *Method* y *method* se reconocen como variantes de un único término. La lista de términos extraídos puede incluir *Method* o *method*, en función de la palabra que aparezca en primer lugar en el conjunto de datos de entrada. Si *Method* aparece con mayúsculas solo porque es la primera palabra en una oración, se extrae en su forma normalizada.  
  
## <a name="sentence-and-word-boundaries"></a>Límites de palabras y oraciones  
 La transformación Extracción de términos separa texto en oraciones mediante los siguientes caracteres que funcionan como límites de oración:  
  
-   Caracteres de salto de línea ASCII 0x0d (retorno de carro) y 0x0a (avance de línea). Para usar este carácter como límite de oración, debe haber dos o más caracteres de salto de línea en una fila.  
  
-   Guiones (-). Para usar este carácter como límite de oración, el carácter situado a la izquierda o a la derecha del guión no puede ser una letra.  
  
-   Carácter de subrayado (_). Para usar este carácter como límite de oración, el carácter situado a la izquierda o a la derecha del guión no puede ser una letra.  
  
-   Todos los caracteres Unicode que son menores o iguales que 0x19, o mayores o iguales que 0x7b.  
  
-   Combinaciones de números, signos de puntuación y caracteres alfabéticos. Por ejemplo, *A23B#99* devuelve el término *A23B*.  
  
-   Los caracteres %, @, &, $, #, \*, :, ;, ., **,** , !, ?, \<, >, +, =, ^, ~, |, \\, /, (, ), [, ], {, }, " y '.  
  
    > [!NOTE]  
    >  Las siglas que incluyen uno o más puntos (.) no se separan en varias oraciones.  
  
 La transformación Extracción de términos separa la oración en palabras aplicando los siguientes límites de palabras:  
  
-   Space  
  
-   Pestaña  
  
-   ASCII 0x0d (retorno de carro)  
  
-   ASCII 0x0a (avance de línea)  
  
    > [!NOTE]  
    >  Si se usa un apóstrofo en una palabra que es una contracción, como *we're* o *it's*, la palabra se divide en el apóstrofo. De lo contrario, las letras que aparecen después del apóstrofo se eliminan. Por ejemplo, *we're* se divide en *we* y *'re*, y *bicycle's* se reduce a *bicycle*.  
  
## <a name="configuration-of-the-term-extraction-transformation"></a>Configuración de la transformación Extracción de términos  
 La transformación Extracción de términos usa algoritmos internos y modelos estadísticos para generar sus resultados. Es posible que tenga que ejecutar la transformación Extracción de términos varias veces y examinar los resultados para configurar la transformación con el fin de generar el tipo de resultados que funciona para la solución de minería de texto.  
  
 La transformación Extracción de términos tiene una entrada normal, una salida y una salida de error.  
  
 Puede establecer propiedades a través del Diseñador de [!INCLUDE[ssIS](../../../includes/ssis-md.md)] o mediante programación.  
  
 Para obtener más información acerca de las propiedades que puede establecer a través del cuadro de diálogo **Editor avanzado** o mediante programación, haga clic en uno de los temas siguientes:  
  
-   [Propiedades comunes](https://msdn.microsoft.com/library/51973502-5cc6-4125-9fce-e60fa1b7b796)  
  
-   [Propiedades personalizadas de transformación](../../../integration-services/data-flow/transformations/transformation-custom-properties.md)  
  
 Para más información sobre cómo establecer propiedades, vea [Establecer las propiedades de un componente de flujo de datos](../../../integration-services/data-flow/set-the-properties-of-a-data-flow-component.md).  
  
## <a name="term-extraction-transformation-editor-term-extraction-tab"></a>Editor de transformación Extracción de términos (pestaña Extracción de términos)
  Use la pestaña **Extracción de términos** del cuadro de diálogo **Editor de transformación Extracción de términos** para especificar la columna de texto que contiene el texto que se extraerá.  
  
### <a name="options"></a>Opciones  
 **Columnas de entrada disponibles**  
 Con las casillas, seleccione la única columna de texto que se utilizará para la extracción de términos.  
  
 **Término**  
 Proporcione un nombre para la columna de salida que contendrá los términos extraídos.  
  
 **Puntuación**  
 Proporcione un nombre para la columna de salida que contendrá la puntuación de cada término extraído.  
  
 **Configurar la salida de errores**  
 Use el cuadro de diálogo [Configurar la salida de errores](https://msdn.microsoft.com/library/5f8da390-fab5-44f8-b268-d8fa313ce4b9) para especificar las opciones de control de errores para las filas que provocan errores.  
  
## <a name="term-extraction-transformation-editor-exclusion-tab"></a>Editor de transformación Extracción de términos (pestaña Exclusión)
  Use la pestaña **Exclusión** del cuadro de diálogo **Editor de transformación Extracción de términos** para establecer una conexión con una tabla de exclusión y especificar las columnas que contienen términos de exclusión.  
  
### <a name="options"></a>Opciones  
 **Utilizar términos de exclusión**  
 Esta opción indica si se excluirán términos específicos durante la extracción de términos mediante la especificación de una columna que contiene los términos de exclusión. Si desea excluir términos, debe especificar las siguientes propiedades del origen:  
  
 **Administrador de conexiones OLE DB**  
 Permite seleccionar un administrador de conexiones OLE DB o crear una conexión haciendo clic en **Nueva**.  
  
 **Nueva**  
 Crea una conexión a una base de datos mediante el cuadro de diálogo **Configurar el administrador de conexiones OLE DB** .  
  
 **Tabla o vista**  
 Permite seleccionar la tabla o vista que contiene los términos de exclusión.  
  
 **Columna**  
 Permite seleccionar la columna de la tabla o vista que contiene los términos de exclusión.  
  
 **Configurar la salida de errores**  
 Use el cuadro de diálogo [Configurar la salida de errores](https://msdn.microsoft.com/library/5f8da390-fab5-44f8-b268-d8fa313ce4b9) para especificar las opciones de control de errores para las filas que provocan errores.  
  
## <a name="term-extraction-transformation-editor-advanced-tab"></a>Editor de transformación Extracción de términos (pestaña Avanzadas)
  Use la pestaña **Avanzadas** del cuadro de diálogo **Editor de transformación Extracción de términos** para especificar las propiedades de la extracción, tales como la frecuencia, la longitud y si deben extraerse palabras o frases.  
  
### <a name="options"></a>Opciones  
 **Nombre**  
 Especifica que la transformación extrae únicamente nombres individuales.  
  
 **Frase**  
 Especifica que la transformación extrae únicamente frases.  
  
 **Nombre y frase**  
 Especifica que la transformación extrae nombres y frases.  
  
 **Frecuencia**  
 Especifica que la puntuación está determinada por la frecuencia del término.  
  
 **TFIDF**  
 Mediante esta opción se indica que la puntuación está determinada por el valor TFIDF del término. La puntuación TFIDF es el producto de la frecuencia del término y la frecuencia inversa del documento, tal y como se define a continuación: TFIDF de un término T = (frecuencia de T) * log ((#filas en entrada)/(#filas con T))  
  
 **Umbral de frecuencia**  
 Permite especificar el número de veces que una palabra o frase debe aparecer antes de extraerla. El valor predeterminado es 2.  
  
 **Longitud máxima del término**  
 Permite especificar la longitud máxima de una frase en palabras. Esta opción afecta únicamente a frases. El valor predeterminado es 12.  
  
 **Utilizar extracción de términos con distinción de mayúsculas y minúsculas**  
 Permite especificar si la extracción distinguirá mayúsculas de minúsculas. El valor predeterminado es **False**.  
  
 **Configurar la salida de errores**  
 Use el cuadro de diálogo [Configurar la salida de errores](https://msdn.microsoft.com/library/5f8da390-fab5-44f8-b268-d8fa313ce4b9) para especificar las opciones de control de errores para las filas que provocan errores.  
  
## <a name="see-also"></a>Consulte también  
 [Referencia de errores y mensajes de Integration Services](../../../integration-services/integration-services-error-and-message-reference.md)   
 [Transformación Búsqueda de términos](../../../integration-services/data-flow/transformations/term-lookup-transformation.md)  

