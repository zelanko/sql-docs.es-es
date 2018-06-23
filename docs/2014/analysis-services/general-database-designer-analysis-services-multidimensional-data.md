---
title: General (Diseñador de la base de datos) (Analysis Services - datos multidimensionales) | Documentos de Microsoft
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- sql12.asvs.databasedesigner.dbconfigurationpane.f1
helpviewer_keywords:
- Database Designer
ms.assetid: 00c9c42b-db2b-4620-8fb6-1e165ff0cbdd
caps.latest.revision: 25
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: 435817b44643ddf1d3e6703ca2872dd5afe407c5
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36200028"
---
# <a name="general-database-designer-analysis-services---multidimensional-data"></a>General (Diseñador de bases de datos) (Analysis Services - Datos multidimensionales)
  Use la pestaña **General** para cambiar las propiedades de una base de datos [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] .  
  
 **Para mostrar la ficha General**  
  
1.  En [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)], abra un proyecto de [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] .  
  
2.  En el **Explorador de soluciones**, haga clic con el botón derecho en el proyecto de [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] , haga clic en **Editar base de datos**y, después, haga clic en la pestaña **General** .  
  
## <a name="basic-options"></a>Opciones de la sección Básica  
 Expanda la sección **Básica** para modificar información básica de la base de datos. Esta sección contiene las siguientes opciones:  
  
 **Nombre de la base de datos**  
 Muestra el nombre de la base de datos.  
  
> [!NOTE]  
>  Para cambiar el nombre de la base de datos, en el **Explorador de soluciones**, haga clic con el botón derecho en el proyecto y, después, haga clic en **Propiedades**. En el cuadro de diálogo **Páginas de propiedades** de la base de datos, en la página **Implementación** , cambie el valor de la propiedad **Base de datos** por el nuevo nombre de la base de datos.  
  
 **Descripción**  
 Escriba una descripción de la base de datos.  
  
## <a name="translations-options"></a>Opciones de la sección Traducciones  
 Expanda la sección **Traducciones** para crear y modificar traducciones del título y la descripción de la base de datos. Esta sección contiene una cuadrícula con las siguientes columnas:  
  
 **Lenguaje**  
 Seleccione el idioma de la transacción especificada.  
  
 Para agregar una nueva traducción a la cuadrícula, haga clic en  **\<agregar nueva traducción >**.  
  
 **Título traducido**  
 Escriba el título de la base de datos en el idioma adecuado para la traducción. Si lo deja en blanco, se utilizará el título predeterminado para la base de datos.  
  
 **Descripción traducida**  
 Escriba la descripción de la base de datos en el idioma adecuado para la traducción. Si la deja en blanco, se utilizará la descripción predeterminada para la base de datos.  
  
## <a name="account-type-mapping-options"></a>Opciones de la sección Asignación de tipo de cuenta  
 Expanda la sección **Asignación de tipo de cuenta** para modificar la función de agregación predeterminada asociada con cada **tipo** de cuenta en la base de datos seleccionada.  
  
> [!NOTE]  
>  Esta opción se aplica solo a los cubos en los que una o varias mediciones usan la función de agregación *ByAccount* .  
  
 Esta sección contiene una cuadrícula con las siguientes columnas:  
  
 **Nombre**  
 Escriba el nombre del tipo de cuenta.  
  
 Para agregar un nuevo tipo de cuenta, haga clic en  **\<Agregar nuevo tipo de cuenta >**.  
  
 **Alias**  
 Establece el nombre predeterminado del tipo de cuenta que usará el Asistente de Business Intelligence. Si se deja esta columna vacía, se utilizará el valor predeterminado de la columna **Nombre** .  
  
 **Función de agregación**  
 Seleccione la función de agregación que se utilizará para el tipo de cuenta seleccionado.  
  
## <a name="see-also"></a>Vea también  
 [Diseñadores y cuadros de diálogo de Analysis Services &#40;datos multidimensionales&#41;](analysis-services-designers-and-dialog-boxes-multidimensional-data.md)   
 [Las bases de datos de modelo multidimensional &#40;SSAS&#41;](multidimensional-models/multidimensional-model-databases-ssas.md)   
 [Advertencias &#40;Diseñador de la base de datos&#41; &#40;Analysis Services - datos multidimensionales&#41;](warnings-database-designer-analysis-services-multidimensional-data.md)  
  
  