---
title: Almacenamiento e intercalación en los modelos tabulares de cadenas | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 8516f0ad-32ee-4688-a304-e705143642ca
caps.latest.revision: 9
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: b61d01e59aa99e6ed97a328d14cee8ab82c3427a
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/02/2018
ms.locfileid: "37280551"
---
# <a name="string-storage-and-collation-in-tabular-models"></a>Almacenamiento e intercalación de cadenas en modelos tabulares
  Las cadenas (valores de texto) se almacenan en los modelos tabulares utilizando un formato muy comprimido; debido a esta compresión, puede obtener resultados inesperados al recuperar cadenas completas o parciales. Además, dado que la configuración regional y las intercalaciones de las cadenas se heredan jerárquicamente del objeto primario más próximo, si no se define explícitamente el idioma de las cadenas, la configuración regional y la intercalación del elemento primario pueden afectar a la forma de almacenamiento de cada una de las cadenas y determinar si la cadena es única o se combina con cadenas similares tal como se define en la intercalación primaria.  
  
 En este tema se describe el mecanismo mediante el cual se comprimen y almacenan las cadenas, y se proporcionan ejemplos de cómo afectan la intercalación y el idioma a los resultados de las fórmulas de texto en los modelos tabulares.  
  
## <a name="storage"></a>Almacenamiento  
 En los modelos tabulares, todos los datos están muy comprimidos para que puedan almacenarse sin problemas en la memoria. En consecuencia, todas las cadenas consideradas léxicamente equivalentes se almacenan solo una vez. La primera instancia de la cadena se utiliza como la representación canónica y a partir de este momento cada cadena equivalente se indiza al mismo valor comprimido que la primera repetición.  
  
 La pregunta clave es: ¿qué constituye una cadena léxicamente equivalente? Dos cadenas se consideran léxicamente equivalentes si se pueden considerar como la misma palabra. Por ejemplo, cuando busca la palabra **violin** en inglés en un diccionario, puede encontrar la entrada **Violin** o **violin**, dependiendo de la directiva editorial del diccionario, pero generalmente considerará ambas palabras equivalentes, y no tendrá en cuenta la diferencia en el uso de mayúsculas. En un modelo tabular, el factor que determina si dos cadenas son léxicamente equivalentes no es la directiva editorial ni las preferencias del usuario, sino la configuración regional y la intercalación asignadas a la columna.  
  
 Por lo tanto, la decisión de si las letras mayúsculas y minúsculas se deben considerar iguales o diferentes dependerá de la intercalación y de la configuración regional. De esta manera, para cualquier palabra concreta incluida en esa configuración regional, la primera repetición que se encuentre dentro una determinada columna actuará como la representación canónica de dicha palabra, y la cadena se almacenará en un formato sin comprimir.  Todas las demás cadenas se compararán con la primera repetición y, si pasan la prueba de equivalencia, se asignarán al valor comprimido de dicha repetición. Más adelante, cuando se recuperen los valores comprimidos, se representarán mediante el valor sin comprimir de la primera repetición de la cadena.  
  
 Un ejemplo ayudará a clarificar su funcionamiento. La columna siguiente, "Classification - English", se ha extraído de una tabla que contiene información sobre plantas y árboles. La columna de clasificación muestra la categoría general para cada planta (los nombres de las plantas no se muestran aquí).  
  
|Classification - English|  
|-------------------------------|  
|trEE|  
|PlAnT|  
|trEE|  
|PlAnT|  
|PlAnT|  
|trEE|  
|PlAnT|  
|trEE|  
|trEE|  
|PlAnT|  
|trEE|  
  
 Es posible que los datos procediesen de varios orígenes diferentes, y por lo tanto el estilo de mayúsculas y minúsculas y el uso de los acentos fuese incoherente, y la base de datos relacional almacenase estas diferencias tal cual. Pero, en general, los valores son **Plant** o **Tree**, solo que con estilos distintos de mayúscula y minúscula.  
  
 Cuando se cargan estos valores en un modelo tabular que utiliza la intercalación y la forma de ordenación predeterminados para el inglés estadounidense, el uso de mayúsculas o minúsculas no es importante, por lo que solo se almacenarán dos valores para toda la columna:  
  
|Classification - English|  
|-------------------------------|  
|trEE|  
|PlAnT|  
  
 Si utiliza la columna **Classification – English**en el modelo, cuando muestre la clasificación de las plantas no verá los valores originales, con sus varios usos de mayúsculas y minúsculas, sino únicamente la primera repetición. El motivo es que todas las variantes de mayúsculas y minúsculas de **tree** se consideran equivalentes en esta intercalación y configuración regional; por lo tanto, solo se conservó una cadena y la primera instancia de esta que encuentre el sistema será la que se guarde.  
  
> [!WARNING]  
>  Quizá decida que desea definir la cadena que se almacenará en primer lugar, de acuerdo con lo que considera correcto, pero esto puede resultar muy difícil. No es fácil determinar con antelación qué fila debe procesar el motor en primer lugar, dado que todos los valores se consideran iguales. En lugar de ello, si necesita establecer el valor estándar, deberá limpiar todas las cadenas antes de cargar el modelo.  
  
## <a name="locale-and-collation-order"></a>Orden de la intercalación y de la configuración regional  
 Cuando se comparan cadenas (valores de texto), lo que define la equivalencia es normalmente el aspecto cultural de cómo se interpretan dichas cadenas. En algunas referencias culturales, el acento o el uso de mayúsculas en un carácter puede cambiar completamente el significado de la cadena; por lo tanto, normalmente están diferencias se tienen en consideración a la hora de determinar la equivalencia para un idioma o una región concretos.  
  
 Generalmente, cuando utiliza su equipo, este ya está configurado para que reconozca sus propias expectativas culturales y comportamientos lingüísticos, y las operaciones de cadena como la ordenación y la comparación de valores de texto se comportan de la forma esperada. La configuración que controla el comportamiento específico del idioma se define con los valores de **Configuración regional** de Windows. Las aplicaciones leen estos valores y cambian su comportamiento en consecuencia. En algunos casos, una aplicación puede incluir una característica que le permita cambiar su comportamiento cultural o la manera en que se comparan las cadenas.  
  
 Cuando se crea una base de datos de modelos tabulares, esta hereda de forma predeterminada estos valores culturales y lingüísticos en forma de un identificador de idioma y una intercalación.  
  
-   El identificador de idioma define el juego de caracteres que se desea utilizar para las cadenas en función de las referencias culturales.  
  
-   La intercalación define el orden de los caracteres y su equivalencia.  
  
 Es importante resaltar que un identificador de idioma no solo identifica un idioma, sino también el país o la región donde se utiliza dicho idioma. Cada identificador de idioma también tiene una especificación de intercalación predeterminada. Para obtener más información acerca de los identificadores de idioma, vea [Id. de configuración regional asignados por Microsoft](http://msdn.microsoft.com/goglobal/bb964664.aspx). Puede utilizar la columna LCID Dec para obtener el identificador correcto al insertar manualmente un valor. Para más información sobre el concepto de intercalaciones en SQL, vea [COLLATE &#40;Transact-SQL&#41;](/sql/t-sql/statements/collations). Para obtener información sobre los designadores de colación y los estilos de comparación para los nombres de intercalación de Windows, vea [Nombre de intercalación de Windows &#40;Transact-SQL&#41;](/sql/t-sql/statements/windows-collation-name-transact-sql). En el tema [Nombre de intercalación de SQL Server &#40;Transact-SQL&#41;](/sql/t-sql/statements/sql-server-collation-name-transact-sql) se asignan los nombres de intercalación de Windows a los nombres usados para SQL.  
  
 Una vez creada la base de datos de modelos tabulares, todos los objetos nuevos del modelo heredarán los atributos de idioma y de intercalación de los atributos de base de datos. Esto es válido para todos los objetos. La ruta de herencia comienza en el objeto, examina el elemento primario para comprobar si se debe heredar algún atributo de idioma y de intercalación y, si no encuentra ninguno, continúa hacia la parte superior y busca los atributos de idioma e intercalación en el nivel de base de datos. En otras palabras, si no se especifican los atributos de idioma y de intercalación para un objeto, este hereda de forma predeterminada los atributos de su elemento primario más próximo.  
  
 En las columnas, los atributos de idioma y de intercalación se heredan en el momento de su creación, según las reglas siguientes:  
  
1.  Los atributos de idioma y de intercalación se buscan en el objeto de dimensión primario. Si existen ambos valores, estos se copian a los atributos de la columna; si solo existe uno de ellos, el otro se deduce de este y se asignan ambos; si no existe ninguno, ir al paso siguiente.  
  
2.  Los atributos se buscan en el objeto de base de datos utilizando el mismo proceso descrito en el paso 1 para las dimensiones; si no se encuentra ninguno, ir al paso siguiente.  
  
3.  Los atributos se buscan en el objeto de servidor utilizando el mismo proceso descrito en el paso 1 para las dimensiones; si no se encuentra ninguno, la columna utiliza el identificador de idioma de Windows y deduce el atributo de intercalación de ese valor.  
  
 Es importante resaltar que, normalmente, el identificador de idioma y la intercalación de la base de datos de origen apenas influyen en la forma en la que se almacenan los valores en la columna del modelo tabular. La excepción es cuando la base de datos de origen transforma o filtra los valores solicitados.  
  
  
