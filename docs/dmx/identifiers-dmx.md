---
title: Identificadores (DMX) | Documentos de Microsoft
ms.custom: 
ms.date: 03/02/2016
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology:
- analysis-services
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs:
- DMX
helpviewer_keywords:
- Data Mining Extensions [Analysis Services], identifiers
- delimited identifiers [DMX]
- DMX [Analysis Services], identifiers
- identifiers [DMX]
- regular identifiers [DMX]
- names [DMX]
ms.assetid: fbb487a7-1b89-482a-977e-f079379d44fc
caps.latest.revision: 35
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: a782514c378c3a8395596bf667f8964caaa6dce1
ms.contentlocale: es-es
ms.lasthandoff: 08/02/2017

---
# <a name="identifiers-dmx"></a>Identificadores (DMX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  Todos los objetos de [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] debe tener un identificador. El nombre del objeto es su identificador. Servidores, bases de datos y objetos de base de datos como orígenes de datos, vistas del origen de datos, cubos, dimensiones, modelos de minería de datos y así sucesivamente tengan identificadores.  
  
 Existen dos clases de identificadores en Extensiones de minería de datos (DMX):  
  
-   [Identificadores normales](#RegularIdentifiers)  
  
-   [Identificadores delimitados](#DelimitedIdentifiers)  
  
 El identificador de un objeto se crea cuando se define el objeto. Así puede utilizar el identificador para hacer referencia al objeto. Los identificadores pueden tener 100 caracteres como máximo.  
  
##  <a name="RegularIdentifiers"></a>Identificadores normales  
 Los identificadores normales de DMX siguen las reglas de [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] respecto al formato de identificadores. Los identificadores normales de DMX no requieren delimitadores. Aquí te mostramos un ejemplo de una instrucción DMX que utiliza un identificador normal no delimitado:  
  
```  
SELECT * FROM Clustering.CONTENT;  
```  
  
### <a name="rules-for-regular-identifiers"></a>Reglas de los identificadores normales  
 A continuación, figuran las reglas de formato de los identificadores normales:  
  
1.  El primer carácter de un identificador normal debe ser uno de los siguientes:  
  
    -   Una letra, tal como se define por el estándar Unicode 2.0. Incluye los caracteres latinos de la "a" a la "z" y de la "A" a la "Z", además de los caracteres de letras de otros idiomas.  
  
    -   Un carácter de subrayado (_).  
  
2.  Los caracteres subsiguientes pueden ser:  
  
    -   Letras, tal como se define en el estándar Unicode 2.0.  
  
    -   Números decimales del alfabeto Latín básico u otros alfabetos de otros idiomas.  
  
    -   Un carácter de subrayado (_).  
  
3.  El identificador no debe ser una palabra reservada de DMX. En las palabras reservadas de DMX, no se distinguen mayúsculas de minúsculas. Para obtener más información, consulte [palabras clave reservadas &#40; DMX &#41;](../dmx/reserved-keywords-dmx.md).  
  
4.  El identificador no puede contener espacios o caracteres especiales incrustados.  
  
 Deberá escribir entre corchetes los identificadores que no sigan estas reglas cuando los emplee en instrucciones DMX.  
  
##  <a name="DelimitedIdentifiers"></a>Identificadores delimitados  
 Los identificadores delimitados se escriben entre corchetes ([ ]).  A continuación, figura un ejemplo de una instrucción DMX que utiliza un identificador delimitado que sigue las reglas.  
  
```  
SELECT * FROM [Marketing_Clusters].CONTENT;  
```  
  
 Si un identificador no sigue las reglas de formato de los identificadores normales, debe aparecer siempre delimitado. A continuación, figura un ejemplo de una instrucción DMX con un identificador delimitado que contiene un espacio:  
  
```  
SELECT * FROM [Targeted Mailing].CONTENT;  
```  
  
 Los identificadores delimitados se emplean en estas situaciones:  
  
-   Cuando utilice palabras reservadas en los nombres de objeto o partes de nombres de objeto.  
  
     Se recomienda evitar el uso de palabras clave reservadas en los nombres de objeto. Las bases de datos actualizadas desde versiones anteriores de [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] podrían contener identificadores que incluyan palabras que no estaban reservadas en la versión anterior de [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] pero que son palabras reservadas para[!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]. Puede hacer referencia al objeto con identificadores delimitados hasta que se pueda cambiar el nombre.  
  
-   Cuando utilice caracteres no considerados como identificadores aceptados.  
  
     [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] permite que se utilice cualquier carácter de la página de códigos actual en identificadores delimitados; no obstante, el uso indiscriminado de caracteres especiales en un nombre de objeto puede dificultar la lectura y el mantenimiento de las instrucciones DMX.  
  
### <a name="rules-for-delimited-identifiers"></a>Reglas para los identificadores delimitados  
 A continuación, figuran las reglas de formato de los identificadores delimitados:  
  
1.  Los identificadores delimitados pueden contener el mismo número de caracteres que los identificadores normales (de 1 a 100 caracteres, sin incluir los caracteres delimitadores).  
  
2.  La parte de cuerpo del identificador puede contener cualquier combinación de caracteres de la página actual de códigos, incluidos los propios caracteres delimitadores. Si el propio cuerpo del identificador contiene caracteres delimitadores, será necesario un tratamiento especial:  
  
    -   Si el cuerpo del identificador contiene un corchete de apertura ([), no se requiere ninguna manipulación.  
  
    -   Si el cuerpo del identificador contiene un corchete de cierre (]), deberá especificar dos corchetes de cierre (]]) para representarlo en la página de códigos.  
  
### <a name="delimiting-identifiers-with-multiple-parts"></a>Delimitar identificadores con varias partes  
 Cuando se utilizan nombres de objetos completos, podría ser necesario delimitar varios de los identificadores que componen el nombre de objeto. Deberá delimitar cada uno de ellos por separado.  
  
## <a name="see-also"></a>Vea también  
 [Extensiones de minería de datos &#40; DMX &#41; Referencia](../dmx/data-mining-extensions-dmx-reference.md)   
 [Extensiones de minería de datos &#40; DMX &#41; Elementos de sintaxis](../dmx/data-mining-extensions-dmx-syntax-elements.md)   
 [Extensiones de minería de datos &#40; DMX &#41; Referencia de funciones](../dmx/data-mining-extensions-dmx-function-reference.md)   
 [Extensiones de minería de datos &#40; DMX &#41; Referencia de operadores](../dmx/data-mining-extensions-dmx-operator-reference.md)   
 [Extensiones de minería de datos &#40; DMX &#41; Referencia de instrucciones](../dmx/data-mining-extensions-dmx-statements.md)   
 [Extensiones de minería de datos &#40; DMX &#41; Convenciones de sintaxis](../dmx/data-mining-extensions-dmx-syntax-conventions.md)   
 [Funciones de predicción generales &#40; DMX &#41;](../dmx/general-prediction-functions-dmx.md)   
 [Estructura y el uso de consultas de predicción DMX](../dmx/structure-and-usage-of-dmx-prediction-queries.md)   
 [Descripción de la instrucción Select de DMX](../dmx/understanding-the-dmx-select-statement.md)  
  
  

