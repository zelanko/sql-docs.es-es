---
title: Identificadores (SSIS) | Documentos de Microsoft
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- regular identifiers [Integration Services]
- variables [Integration Services], expressions
- identifiers [Integration Services]
- expressions [Integration Services], variables
- lineage identifiers
- columns [Integration Services], identifiers
- names [Integration Services]
- expressions [Integration Services], identifiers
- qualified identifiers [Integration Services]
ms.assetid: 56af984d-88b4-4db8-b6a2-6b07315a699e
caps.latest.revision: 45
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: cc690b6318c3e9fea27fbbba74b1f1b7289a3d32
ms.contentlocale: es-es
ms.lasthandoff: 08/03/2017

---
# <a name="identifiers-ssis"></a>Identificadores (SSIS)
  En las expresiones, los identificadores son columnas y variables que están disponibles para la operación. Puede utilizar en las expresiones identificadores regulares y calificados.  
  
## <a name="regular-identifiers"></a>Identificadores regulares  
 Un identificador regular es un identificador que no necesita calificadores adicionales. Por ejemplo, **MiddleName**, una columna de la tabla **Contacts** de la base de datos **AdventureWorks** , es un identificador regular.  
  
 La nomenclatura de los identificadores regulares debe seguir estas reglas:  
  
-   El primer carácter del nombre tiene que ser una letra (según se define en Unicode Standard 2.0) o un carácter de subrayado (_).  
  
-   Los caracteres siguientes pueden ser letras o números, tal como se define en el Estándar Unicode 2.0, el carácter de subrayado (_), o los caracteres @, $ y #.  
  
> [!IMPORTANT]  
>  Los espacios incrustados y los caracteres especiales distintos de los especificados no son válidos en los identificadores regulares. Para poder usar espacios y caracteres especiales, debe utilizar un identificador calificado en lugar de un identificador regular.  
  
## <a name="qualified-identifiers"></a>Identificadores calificados  
 Un identificador calificado es un identificador delimitado por corchetes. Si el nombre del identificador incluye espacios o el primer carácter del mismo no es una letra ni el carácter de subrayado, el identificador puede requerir un delimitador. Por ejemplo, es necesario escribir el nombre de columna **Segundo nombre** entre corchetes y en una expresión como [Segundo nombre].  
  
 Si el nombre del identificador incluye espacios, o no es un nombre de identificador regular válido, el identificador debe ser calificado. El evaluador de expresiones utiliza corchetes de apertura y cierre ([]) para calificar los identificadores. Los corchetes se colocan en la primera y la última posición de la cadena. Por ejemplo, el identificador 5$> se convierte en [5$>]. Se puede usar corchetes en los nombres de columnas, variables y funciones.  
  
 Si genera expresiones con los cuadros de diálogo del Diseñador [!INCLUDE[ssIS](../../includes/ssis-md.md)] , los identificadores regulares se escriben automáticamente entre corchetes. Sin embargo, solo es necesario utilizar corchetes si el nombre incluye algún carácter no válido. Por ejemplo, la columna denominada **MiddleName** es válida sin corchetes.  
  
 No se puede hacer referencia a nombres de columna que incluyan corchetes en las expresiones. Por ejemplo, el nombre de columna **Columna[1]** no se puede usar en una expresión. Para utilizar la columna en una expresión, se debe cambiar el nombre de la columna por un nombre sin corchetes.  
  
## <a name="lineage-identifiers"></a>linaje, identificadores  
 Las expresiones pueden usar identificadores de linaje para hacer referencia a columnas. Los identificadores de linaje se asignan automáticamente al crear por primera vez el paquete. Puede ver el identificador de linaje para una columna en la pestaña **Propiedades de columna** del cuadro de diálogo **Editor avanzado** del Diseñador [!INCLUDE[ssIS](../../includes/ssis-md.md)] .  
  
 Si se hace referencia a una columna por su identificador de linaje, el identificador debe incluir el prefijo #. Por ejemplo, para hacer referencia a una columna con el identificador de linaje 147, debe utilizarse #147.  
  
 Si una expresión se analiza correctamente, el evaluador de expresiones reemplaza los identificadores de linaje por nombres de columna en el cuadro de diálogo.  
  
## <a name="unique-column-names"></a>Nombres de columna únicos  
 Varios componentes de un paquete pueden exponer columnas con el mismo nombre. Si estas columnas se usan en expresiones, se debe eliminar la ambigüedad para que se puedan analizar las expresiones correctamente. El evaluador de expresiones admite la notación de puntos para identificar el origen de la columna. Por ejemplo, dos columnas denominadas **Age** se convierten en **FlatFileSource.Age** y **OLEDBSource.Age**, lo que indica que sus orígenes respectivos son FlatFileSource y OLEDBSource. El analizador trata el nombre completo como un nombre de columna individual.  
  
 Los nombres de componente de origen y los nombres de columna se califican por separado. Los siguientes ejemplos muestran un uso válido de los corchetes con la notación de puntos:  
  
-   El nombre del componente de origen incluye espacios.  
  
    ```  
    [MySo urce].Age  
    ```  
  
-   El primer carácter del nombre de la columna no es válido.  
  
    ```  
    MySource.[#Age]  
    ```  
  
-   El componente de origen y los nombres de columna contienen caracteres no válidos.  
  
    ```  
    [MySource?].[#Age]  
    ```  
  
> [!IMPORTANT]  
>  Si se escriben ambos elementos con notación de puntos entre corchetes, el evaluador de expresiones interpretará el par como un identificador individual, no como una combinación de columnas de origen.  
  
## <a name="variables-in-expressions"></a>Variables en expresiones  
 Para hacer referencia a estas variables en expresiones, debe incluirse el prefijo @. Por ejemplo, el **contador** variable hace referencia mediante el uso de @Counter. El carácter @ no forma parte del nombre de la variable; solo identifica la variable al evaluador de expresiones. Si genera expresiones a través de los cuadros de diálogo proporcionados por el Diseñador [!INCLUDE[ssIS](../../includes/ssis-md.md)] , se agrega automáticamente el carácter @ al nombre de la variable. No se permite incluir espacios entre el carácter @ y el nombre de la variable.  
  
 Los nombres de las variables siguen las mismas reglas que los otros identificadores regulares:  
  
-   El primer carácter del nombre tiene que ser una letra (según se define en Unicode Standard 2.0) o un carácter de subrayado (_).  
  
-   Los caracteres siguientes pueden ser letras o números, tal como se define en el Estándar Unicode 2.0, el carácter de subrayado (_), o los caracteres @, $ y #.  
  
 Si un nombre de variable contiene caracteres distintos de los especificados, debe escribir la variable entre corchetes. Por ejemplo, los nombres de variables con espacios deben escribirse entre corchetes. El corchete de apertura sigue al carácter @. Por ejemplo, para hacer referencia a la variable **Mi nombre** se usa @[Mi nombre]. No se permite incluir espacios entre el nombre de la variable y los corchetes.  
  
> [!NOTE]  
>  Los nombres están definidos por el usuario y las variables del sistema distinguen mayúsculas y minúsculas.  
  
## <a name="unique-variable-names"></a>Nombres de variable únicos  
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] admite variables personalizadas y proporciona un conjunto de variables del sistema. De manera predeterminada, las variables personalizadas pertenecen al espacio de nombres **User** y las variables del sistema pertenecen al espacio de nombres **System** . Puede crear espacios de nombres adicionales para variables personalizadas y actualizar los nombres de los espacios de nombres según las necesidades de la aplicación. El generador de expresiones muestra las variables del ámbito en todos los espacios de nombres.  
  
 Todas las variables tienen un ámbito y pertenecen a un espacio de nombres. Una variable tiene ámbito de paquete o ámbito de un contenedor o una tarea del paquete. El generador de expresiones del Diseñador [!INCLUDE[ssIS](../../includes/ssis-md.md)] muestra únicamente las variables que estén dentro del ámbito. Para más información, vea [Variables de Integration Services &#40;SSIS&#41;](../../integration-services/integration-services-ssis-variables.md) y [Usar variables en paquetes](http://msdn.microsoft.com/library/7742e92d-46c5-4cc4-b9a3-45b688ddb787).  
  
 Las variables usadas en expresiones deben tener nombres únicos para que el evaluador de expresiones evalúe la expresión correctamente. Si un paquete usa varias variables con el mismo nombre, sus espacios de nombres deben ser diferentes. [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] proporciona un operador de resolución de espacio de nombres, formado por dos signos de dos puntos (::), para calificar una variable con su espacio de nombres. Por ejemplo, la siguiente expresión utiliza dos variables denominadas **Count**; una pertenece al espacio de nombres **User** y la otra al espacio de nombres **MyNamespace** .  
  
```  
@[User::Count] > @[MyNamespace::Count]  
```  
  
> [!IMPORTANT]  
>  Debe escribir la combinación de espacio de nombres y nombre calificado de la variable entre corchetes para que el evaluador de expresiones reconozca la variable.  
  
 Si el valor de **Count** en el espacio de nombres **User** es 10 y el valor de **Count** en el espacio de nombres **MyNamespace** es 2, la expresión se evalúa como **true** , ya que el evaluador de expresiones reconoce dos variables distintas.  
  
 Si los nombres de las variables no son únicos, no se produce un error. El evaluador de expresiones utilizará una sola instancia de la variable para evaluar la expresión y devolverá un resultado incorrecto. Por ejemplo, la siguiente expresión intenta comparar los valores (10 y 2) de dos variables **Count** por separado, pero la expresión da como resultado **falso** , ya que el evaluador de expresiones usa la misma instancia de la variable **Count** dos veces.  
  
```  
@Count > @Count  
```  
  
## <a name="related-content"></a>Contenido relacionado  
 Artículo técnico, sobre la [referencia rápida de expresiones de SSIS](http://go.microsoft.com/fwlink/?LinkId=746575), en pragmaticworks.com  
  
  
