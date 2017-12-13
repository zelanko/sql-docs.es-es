---
title: Traducciones en modelos tabulares (Analysis Services) | Documentos de Microsoft
ms.custom: 
ms.date: 03/01/2017
ms.prod: analysis-services
ms.prod_service: analysis-services, azure-analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology: analysis-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: e67f88f5-9f0c-4f19-ab09-558c56ca9335
caps.latest.revision: "13"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 5a79c607d07a50861f87bcdec21c928231cd51bc
ms.sourcegitcommit: f1a6944f95dd015d3774a25c14a919421b09151b
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/08/2017
---
# <a name="translations-in-tabular-models-analysis-services"></a>Traducciones en modelos tabulares (Analysis Services)
[!INCLUDE[ssas-appliesto-sqlas-aas](../../includes/ssas-appliesto-sqlas-aas.md)][!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] agrega compatibilidad con la cadena de traducción para los modelos tabulares. Un único objeto del modelo puede tener varias traducciones de un nombre o una descripción, lo que hace posible admitir varios idiomas dentro de la definición del modelo.  
  
 Las cadenas traducidas solo son para los metadatos de objeto (nombres y descripciones de tablas y columnas) que aparecen en una herramienta de cliente, como una lista de tabla dinámica de Excel.  Para utilizar cadenas traducidas, la conexión de cliente especifica la referencia cultural. En la característica **Análisis en Excel** , puede seleccionar el idioma de una lista desplegable. En otras herramientas, es posible que tenga que especificar la referencia cultural en la cadena de conexión.  
  
 Esta característica no se ha diseñado para cargar datos traducidos en un modelo. Si desea cargar valores de datos traducidos, debe desarrollar una estrategia de procesamiento que incluya la extracción de cadenas traducidas a partir de un origen de datos que las proporcione.  
  
 Este es al aspecto que tiene un flujo de trabajo típico para agregar metadatos traducidos:  
  
-   Generación de un archivo de traducción JSON vacío que contiene marcadores de posición para cada traducción de cadenas  
  
-   Adición de traducciones de cadenas al archivo JSON  
  
-   Importación de las traducciones al modelo  
  
-   Creación, procesamiento e implementación del modelo  
  
-   Conexión al modelo mediante una aplicación cliente que permita un LCID en la cadena de conexión  
  
## <a name="create-an-empty-translation-file"></a>Creación de un archivo de traducción vacío  
 Use [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)] para agregar traducciones.  
  
1.  Haga clic en **Modelo** > **Traducciones** > **Administrar traducciones**.  
  
2.  Seleccione los idiomas en los que va a proporcionar traducciones y, después, haga clic en **Agregar**.  
  
3.  Elija uno o más idiomas de la lista, en función de cómo desea importar las cadenas más adelante.  
  
     El archivo de traducción puede incluir varios idiomas, pero podría administrar las traducciones de manera más sencilla si crea un archivo de traducción por idioma. El archivo de traducción que está creando ahora se importará en su totalidad más adelante. Para cambiar las opciones de importación por idioma, cada uno de ellos debe estar en su propio archivo.  
  
4.  Haga clic en **Export Language File**(Exportar archivo de idioma).  Proporcione el nombre y la ubicación del archivo.  
  
 ![SSAS-tabular-traducir-export](../../analysis-services/tabular-models/media/ssas-tabular-translate-export.png "ssas-tabular-traducir-export")  
  
## <a name="add-translations"></a>Adición de traducciones  
 Un archivo de traducción JSON vacío incluye los metadatos de las traducciones de un idioma específico. Marcadores de posición de traducción para nombres de objeto y descripciones se especifican en la sección **Culture** , que se encuentra al final de la definición del modelo. Se pueden agregar traducciones para los siguientes elementos:  
  
|||  
|-|-|  
|translatedCaption|Título de tabla o columna que aparece en cualquier aplicación cliente compatible con visualizaciones de un modelo tabular.|  
|translatedDescription|Se muestra una descripción como información sobre el modelo en una herramienta de modelado como SSDT (es menos común que los títulos).|  
  
 No elimina ningún metadato que no se haya especificado en el archivo.  Debe coincidir con el archivo en el que está basado. Agregue solo las cadenas que desee y, después, guarde el archivo.  
  
 Aunque podría parecer algo que debe modificar, la sección  **referenceCulture** contiene los metadatos de la referencia cultural predeterminada del modelo. Los cambios realizados en la sección **referenceCulture** no se leerán en durante la importación y se omitirán.  
  
 En el ejemplo siguiente se muestran los títulos y la descripción traducidos de las tablas **DimProduct** y **DimCustomer** .  
  
 ![SSAS-tabular-traducir-json](../../analysis-services/tabular-models/media/ssas-tabular-translate-json.png "ssas-tabular-traducir-json")  
  
> [!TIP]  
>  Puede usar cualquier editor JSON para abrir el archivo, pero se recomienda usar el editor de JSON en Visual Studio para que también puede utilizar el comando Ver código del Explorador de soluciones con el fin de ver la definición de modelo tabular en SSDT. Para obtener el editor de JSON, necesita una [instalación de versión instalación completa de Visual Studio 2015](https://www.visualstudio.com/en-us/downloads/download-visual-studio-vs.aspx). La edición gratuita Community incluye el editor de JSON.  
  
## <a name="import-a-translation-file"></a>Importación de un archivo de traducción  
 Las cadenas de traducción importadas pasarán a formar parte para siempre de la definición del modelo. Una vez que se importen las cadenas, ya no se volverá a hacer referencia el archivo de traducción.  
  
1.  Haga clic en **Modelo** > **Traducciones** > **Importar traducciones**.  
  
2.  Busque el archivo de traducción y, después, haga clic en **Abrir**.  
  
3.  Si lo desea, especifique las opciones de importación.  
  
    |||  
    |-|-|  
    |Sobrescribir traducciones existentes|Reemplaza todos los títulos y descripciones existentes del mismo idioma que el archivo que se va a importar.|  
    |Ignore invalid objects (Omitir objetos no válidos)|Especifica si las discrepancias en los metadatos deben omitirse o marcarse como error.|  
    |Write import results to a log file (Escribir los resultados de importación en un archivo de registro)|Los archivos de registro se guardan en la carpeta del proyecto de forma predeterminada. Cuando finaliza la importación, se proporciona la ruta de acceso exacta al archivo. El nombre de archivo de registro es SSDT_Translations_Log_\<timestamp >.|  
    |Back up translations to a JSON file before importing (Realizar copia de seguridad de las traducciones en un archivo JSON antes de importar)|Realiza una copia de seguridad de una traducción existente que coincida con la referencia cultural de las cadenas que se van a importar.  Si la referencia cultural que se va a importar no se encuentra en el modelo, la copia de seguridad estará vacía.<br /><br /> Si necesita restaurar este archivo más adelante, puede reemplazar el contenido de model.bim por este archivo JSON.|  
  
4.  Haga clic en **Importar**.  
  
5.  Si lo desea, si ha generado un archivo de registro o una copia de seguridad, puede encontrar los archivos en la carpeta del proyecto (por ejemplo, C:\Users\Documents\Visual Studio 2015\Projects\Tabular1200-AW\Tabular1200-AW).  
  
6.  Para comprobar la importación, siga estos pasos:  
  
    -   Haga clic con el botón derecho en el archivo **model.bim** en el Explorador de soluciones y elija **Ver código**. Haga clic en **Sí** para cerrar la vista de diseño y volver a abrir **model.bim** en la vista código.  Si ha instalado una versión completa de Visual Studio, como la versión gratuita Community Edition, el archivo se abrirá con el editor integrado de JSON.  
  
    -   Busque **Referencia cultural** o una cadena traducida específica para comprobar que las cadenas que espera ver están presentes en realidad.  
  
## <a name="connect-using-a-locale-identifier"></a>Conexión con un identificador de configuración regional  
 En esta sección se describe un método para validar que el modelo devuelva las cadenas correctas.  
  
1.  En Excel, conéctese al modelo tabular. En este paso se da por hecho que se ha implementado el modelo. Si el modelo solo se encuentra en el área de trabajo, impleméntelo en una instancia de Analysis Services para completar la comprobación de validación.  
  
     Como alternativa, puede utilizar la característica **Analyze in Excel** (Analizar en Excel) para conectarse con el modelo.  
  
2.  En el cuadro de diálogo de conexión de Excel, elija la referencia cultural de las traducciones de cadenas que hay en el modelo. Excel detecta las referencias culturales definidas en el modelo y rellena la lista desplegable según corresponda.  
  
     ![SSAS-tabular-traducciones-excel](../../analysis-services/tabular-models/media/ssas-tabular-translations-excel.png "ssas-tabular-traducciones-excel")  
  
     Cuando se crea una tabla dinámica, debería ver los nombres de columna y tabla traducidos.  
  
## <a name="see-also"></a>Vea también  
 [Nivel de compatibilidad para modelos tabulares de Analysis Services](../../analysis-services/tabular-models/compatibility-level-for-tabular-models-in-analysis-services.md)   
 [Escenarios de globalización para Analysis Services](../../analysis-services/globalization-scenarios-for-analysis-services.md)   
 [Analizar en Excel &#40;SSAS tabular&#41;](../../analysis-services/tabular-models/analyze-in-excel-ssas-tabular.md)  
  
  
