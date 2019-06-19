---
title: Detalles de traducción (pestaña traducciones, Diseñador de dimensiones) (Analysis Services - datos multidimensionales) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.dimensiondesigner.translations.translationpane.tranlationdetails.f1
ms.assetid: 0aa61df3-f2b0-4703-a63b-124da672dcc3
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 9f8debb50a798ba46457942e0e79a9d45ab392c1
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "66065851"
---
# <a name="translation-details-translations-tab-dimension-designer-analysis-services---multidimensional-data"></a>Detalles de la traducción (pestaña Traducciones, Diseñador de dimensiones) (Analysis Services – Datos multidimensionales)
  Use el panel de **Detalles de la traducción** de la pestaña **Traducciones** del Diseñador de dimensiones para definir y administrar traducciones para la dimensión seleccionada actualmente.  
  
 **Para mostrar el panel de detalles de las traducciones**  
  
1.  En [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)], abra el proyecto de [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] y, a continuación, abra la dimensión que desea.  
  
2.  Haga clic en la pestaña **Traducciones** .  
  
## <a name="options"></a>Opciones  
 **Idioma predeterminado**  
 Establece los nombres de los objetos de la dimensión en el idioma predeterminado.  
  
 **Tipo de objeto**  
 Muestra la propiedad que se va a traducir. Solo se pueden traducir los objetos y las propiedades para los cuales se han especificado valores. Es posible traducir las siguientes propiedades:  
  
-   Dimensión  
  
     Propiedades `Caption` y `AttributeAllMember`  
  
-   Attribute  
  
     Propiedades `Caption`, `AttributeHierarchyDisplayFolder` y `NamingTemplate`.  
  
    > [!NOTE]  
    >  La propiedad `NamingTemplate` solo está disponible para atributos primarios.  
  
-   Hierarchy  
  
     Propiedades `Caption` y `AllMemberName`  
  
-   Nivel  
  
     Propiedad `Caption`  
  
 **\<Language>**  
 Escriba o seleccione el valor de la propiedad del objeto de la dimensión en el idioma seleccionado. Si hace clic en el botón de puntos suspensivos ( **…** ), se abrirán otros cuadros de diálogo, según la propiedad que edite:  
  
-   Propiedad `NamingTemplate`  
  
     Muestra el [Cuadro de diálogo Plantilla de asignación de nombres de nivel &#40;Analysis Services - Datos multidimensionales&#41;](level-naming-template-dialog-box-analysis-services-multidimensional-data.md).  
  
-   Propiedad `Caption` (para atributos)  
  
     Muestra el [Cuadro de diálogo Traducción de datos de atributos &#40;Analysis Services - Datos multidimensionales&#41;](attribute-data-translation-dialog-box-analysis-services-multidimensional-data.md).  
  
## <a name="shortcut-menu"></a>Menú contextual  
 Las opciones siguientes están disponibles en el menú contextual que se abre al hacer clic con el botón derecho en el panel **Detalles de traducción** :  
  
 **Nueva traducción**  
 Seleccione esta opción para mostrar el cuadro de diálogo **Seleccionar idioma** y crear una nueva traducción. La traducción aparecerá como una nueva columna en la cuadrícula **Detalles de la traducción** .  
  
 **Eliminar traducción**  
 Seleccione esta opción para eliminar la traducción seleccionada.  
  
> [!NOTE]  
>  Esta opción solo se habilita si hizo clic con el botón secundario en una celda para eliminar una traducción.  
  
 **Nueva columna de leyenda**  
 Seleccione esta opción para mostrar el cuadro de diálogo **Traducción de datos de atributos** y definir una nueva columna de leyendas cuando modifique un atributo en la cuadrícula **Detalles de traducción** . Para habilitar esta opción, se debe seleccionar una celda de una columna de traducción para un atributo en la cuadrícula **Detalles de traducción** .  
  
> [!NOTE]  
>  Esta opción solo se habilita si hizo clic con el botón secundario en una celda para eliminar la columna de traducción de un atributo.  
  
 **Editar columna de leyenda**  
 Seleccione esta opción para mostrar el cuadro de diálogo **Traducción de datos de atributos** y modificar una columna de leyendas existente al modificar un atributo en la cuadrícula **Detalles de traducción** .  
  
> [!NOTE]  
>  La opción solo se habilita si se ha seleccionado una celda de una columna traducción que contiene una columna de leyenda de un atributo en la cuadrícula **Detalles de traducción** .  
  
 **Eliminar columna de leyenda**  
 Elija esta opción para eliminar la columna de leyendas del atributo seleccionado en la cuadrícula **Detalles de traducción** .  
  
> [!NOTE]  
>  Esta opción solo se habilita si hizo clic con el botón secundario en una columna de traducción que contiene una columna de leyenda para un atributo.  
  
 **Mostrar todos los atributos**  
 Seleccione esta opción para alternar la visualización de todos los atributos definidos para la dimensión seleccionada. Entre ellos se incluyen los atributos en los que se han deshabilitado las jerarquías de atributo.  
  
## <a name="see-also"></a>Vea también  
 [Traducciones &#40;Diseñador de dimensiones&#41; &#40;Analysis Services - datos multidimensionales&#41;](translations-dimension-designer-analysis-services-multidimensional-data.md)  
  
  
