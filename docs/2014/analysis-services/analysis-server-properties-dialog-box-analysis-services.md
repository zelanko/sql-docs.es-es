---
title: Cuadro de diálogo Propiedades de Analysis Server (Analysis Services) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- SQL12.ASVS.SSMSIMBI.SERVERPROPERTIES.F1
- SQL12.ASVS.SQLSERVERSTUDIO.SERVERPROPERTIES.F1
helpviewer_keywords:
- Analysis Server Properties dialog box
ms.assetid: b01ec658-c191-49c9-a6cb-549b21a368ab
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: b32b0fa678df98494f91c1026adebe701d807342
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "66062621"
---
# <a name="analysis-server-properties-dialog-box-analysis-services"></a>Cuadro de diálogo Propiedades de Analysis Server (Analysis Services)
  Use el cuadro de diálogo **Propiedades de Analysis Server** de [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] para establecer la configuración general, de idioma o intercalación, y de seguridad para una instancia de [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]. Para mostrar el cuadro de diálogo **Propiedades de Analysis Server**, haga clic con el botón derecho en una instancia de [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] en el **Explorador de objetos** y seleccione **Propiedades** en el menú contextual. El cuadro de diálogo **Propiedades de Analysis Server** contiene las propiedades siguientes.  
  
## <a name="information-properties"></a>Propiedades de información  
 Use esta página para ver el modo, la versión y el nivel de compatibilidad del servidor. Cada instancia se instala en modo de servidor tabular o multidimensional, con la posibilidad de cargar modelos tabulares o multidimensionales. Si necesita admitir ambos modos, debe instalar dos instancias.  
  
 **Nivel de compatibilidad admitido** es equivalente a la `DefaultCompatibilityLevel` propiedad en AMO. Es de solo lectura, según el modo de implementación del servidor especificado durante la instalación. El servidor comprueba esta propiedad al realizar operaciones que varían según el modo o la versión del servidor, como restaurar una copia de seguridad de una base de datos tabular en una instancia de servidor tabular. No debe confundirse con el modo de compatibilidad de la base de datos de los modelos tabulares o multidimensionales, que tienen nombres y valores similares. Entre los valores válidos de esta propiedad de servidor se incluyen:  
  
-   **1100** es el nivel de compatibilidad predeterminado para un modo de implementación de 0, para el modo multidimensional y de minería de datos.  
  
-   **1103** es el nivel de compatibilidad predeterminado para los modos de implementación 1 o 2, para las instalaciones que admiten el modo tabular o [!INCLUDE[ssGeminiShort](../includes/ssgeminishort-md.md)].  
  
 El servidor devuelve este valor cuando un cliente que admite el espacio de nombres solicita DISCOVER_XML_METADATA. Para más información, vea [Conjunto de filas DISCOVER_XML_METADATA](https://docs.microsoft.com/bi-reference/schema-rowsets/xml/discover-xml-metadata-rowset).  
  
## <a name="general-properties"></a>Propiedades generales  
 Use esta página para establecer las propiedades generales básicas y avanzadas, como la ubicación de carpetas y la configuración de red de una instancia de [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] .  
  
 La página Propiedades del servidor solo muestra las propiedades que es más probable que un administrador cambie, como las propiedades de grupo de memoria y de grupo de subprocesos que se usan para optimizar la configuración del servidor. La lista siguiente contiene vínculos a los grupos principales de propiedades:  
  
-   [Propiedades generales](server-properties/general-properties.md)  
  
-   [Propiedades de minería de datos](server-properties/data-mining-properties.md)  
  
-   [Propiedades de características](server-properties/feature-properties.md)  
  
-   [Propiedades de Filestore](server-properties/filestore-properties.md)  
  
-   [Propiedades del administrador de bloqueos](server-properties/lock-manager-properties.md)  
  
-   [Propiedades de registro](server-properties/log-properties.md)  
  
-   [Propiedades de memoria](server-properties/memory-properties.md)  
  
-   [Propiedades de red](server-properties/network-properties.md)  
  
-   [Propiedades OLAP](server-properties/olap-properties.md)  
  
-   [Propiedades de seguridad](server-properties/security-properties.md)  
  
-   [Propiedades de grupos de subprocesos](server-properties/thread-pool-properties.md)  
  
## <a name="language-collation-properties"></a>Propiedades de idioma o intercalación  
 Use esta página para establecer las opciones de idioma y de intercalación predeterminadas para una instancia de [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]. La lista siguiente contiene una breve descripción de cada opción. Para descripciones más detalladas, vea [Idiomas e intercalaciones &#40;Analysis Services&#41;](languages-and-collations-analysis-services.md).  
  
-   **Binario** se usa para ordenar y comparar datos según los patrones de bits definidos para cada carácter. El orden binario distingue mayúsculas de minúsculas, es decir, las minúsculas siempre preceden a las mayúsculas, y distingue acentos. Éste es el orden más rápido.  
  
     Si no selecciona esta opción, [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] sigue el orden y las reglas de comparación definidas en los diccionarios del idioma o alfabeto asociado.  
  
    > [!NOTE]  
    >  Si selecciona esta opción, se deshabilitarán las opciones **Distinguir mayúsculas de minúsculas**, **Distinguir acentos**, **Distinguir kana**y **Distinguir ancho** .  
  
-   **Binario 2** se usa para ordenar y comparar datos Unicode según los patrones de bits definidos para cada carácter. El orden binario distingue mayúsculas de minúsculas, es decir, las minúsculas siempre preceden a las mayúsculas, y distingue acentos. Éste es el orden más rápido.  
  
-   **Distinguir mayúsculas de minúsculas** se usa para ordenar y comparar datos según las reglas de diccionario del idioma o alfabeto asociados y para distinguir letras mayúsculas de minúsculas.  
  
     Si no selecciona esta opción, [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] considera que las mayúsculas y las minúsculas son versiones de letras iguales. [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] no define si el orden de las letras minúsculas es inferior o superior en relación con mayúscula las letras si **distingue mayúsculas de minúsculas** no está seleccionada.  
  
-   **Distinguir acentos** se usa para ordenar y comparar datos según las reglas de diccionario proporcionadas para el idioma o alfabeto asociados y para distinguir los caracteres acentuados de los no acentuados. Por ejemplo, 'a' no es igual a 'á'.  
  
     Si no selecciona esta opción, [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] considera que las letras acentuadas y las no acentuadas son versiones de letras iguales.  
  
-   **Distinguir Kana** se usa para y comparar datos según las reglas de diccionario proporcionadas para el idioma o alfabeto asociado y distinguir entre los dos tipos de caracteres kana japoneses: Hiragana y Katakana.  
  
     Si no selecciona esta opción, [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] considera que los caracteres hiragana y katakana son iguales.  
  
-   **Distinguir ancho** se usa para ordenar y comparar datos según las reglas de diccionario proporcionadas para el idioma o alfabeto asociados y para distinguir entre un carácter de byte único (ancho medio) del mismo carácter representado con un carácter de doble byte (ancho completo).  
  
     Si no se selecciona esta opción, [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] considera que la representación de byte único y la de doble byte del mismo carácter son iguales.  
  
## <a name="security-properties"></a>Propiedades de seguridad  
 Use esta página para especificar las cuentas de usuario y de grupo de Windows que pertenecen al rol de administrador de servidor para una instancia de [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] . La pertenencia a este rol concede permiso para realizar tareas en todo el servidor, como crear o procesar una base de datos, modificar las propiedades del servidor, agregar o quitar otros miembros de este rol, o iniciar un seguimiento. Consulte [conceder permisos de administrador de servidor &#40;Analysis Services&#41; ](instances/grant-server-admin-rights-to-an-analysis-services-instance.md) para obtener más información.  
  
## <a name="see-also"></a>Vea también  
 [Determinar el modo de servidor de una instancia de Analysis Services](instances/determine-the-server-mode-of-an-analysis-services-instance.md)   
 [Configurar las propiedades del servidor en Analysis Services](server-properties/server-properties-in-analysis-services.md)   
 [Metodologías de autenticación admitidas por Analysis Services](instances/authentication-methodologies-supported-by-analysis-services.md)   
 [Roles y permisos &#40;Analysis Services&#41;](multidimensional-models/roles-and-permissions-analysis-services.md)   
 [Idiomas e intercalaciones &#40;Analysis Services&#41;](languages-and-collations-analysis-services.md)  
  
  
