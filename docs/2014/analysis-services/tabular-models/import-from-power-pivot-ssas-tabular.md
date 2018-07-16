---
title: Importar desde PowerPivot (SSAS Tabular) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
f1_keywords:
- sql12.asvs.bidtoolset.importfromppt.f1
ms.assetid: ac1a6a79-bda3-4122-a717-8b1e2f77da02
caps.latest.revision: 23
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 3f6480cf0b577a0faa48691a85248efb77a84531
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/02/2018
ms.locfileid: "37245745"
---
# <a name="import-from-powerpivot-ssas-tabular"></a>Importar desde PowerPivot (SSAS tabular)
  En este tema se describe cómo crear un nuevo proyecto de modelos tabulares importando los metadatos y datos desde un libro PowerPivot mediante la importación desde PowerPivot de plantilla de proyecto en [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)].  
  
## <a name="create-a-new-tabular-model-from-a-powerpivot-for-excel-file"></a>Cree un nuevo modelo tabular desde un archivo de PowerPivot para Excel  
 Al crear un nuevo proyecto de modelos tabulares importando desde un libro PowerPivot, los metadatos que definen la estructura del libro se usan para crear y definir la estructura del proyecto de modelos tabulares en [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)]. Los objetos como tablas, columnas, medidas y relaciones se conservan, y aparecerán en el proyecto de modelos tabulares tal como están en el libro PowerPivot. No se realizan cambios en el archivo de libro .xlsx.  
  
> [!NOTE]  
>  Los modelos tabulares no admiten tablas vinculadas. Al importar datos de un libro PowerPivot que contiene una tabla vinculada, los datos de la tabla vinculada se tratan como datos copiados y pegados y se almacenan en el archivo Model.bim. Al ver las propiedades de una tabla copiada y pegada, la propiedad **Datos de origen** está deshabilitada y el cuadro de diálogo **Propiedades de la tabla** del menú **Tabla** está deshabilitado.  
>   
>  Hay un límite de 10 000 filas que se pueden agregar a los datos incrustados en el modelo. Si importa un modelo de PowerPivot y aparece el error "Los datos se truncaron. Las tablas pegadas no pueden contener más de 10000 filas”, debe revisar el modelo de PowerPivot moviendo los datos incrustados a otro origen de datos, por ejemplo, a una tabla de SQL Server, y después vuelva a importarlos.  
  
 Existen consideraciones especiales que dependen de si la base de datos del área de trabajo está o no en una instancia de Analysis Services del mismo equipo (local) como [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] o está en una instancia remota de Analysis Services.  
  
 Si la base de datos del área de trabajo está en una instancia local de Analysis Services, puede importar los metadatos y datos del libro PowerPivot. Los metadatos se copian del libro y se usan para crear el proyecto de modelos tabulares. A continuación, se copian los datos del libro y se almacenan en la base de datos del área de trabajo del proyecto (excepto los datos copiados/pegados, que se almacenan en el archivo Model.bim).  
  
 Si la base de datos del área de trabajo está en una instancia remota de Analysis Services, no podrá importar datos de un libro PowerPivot para Excel. Todavía puede importar metadatos del libro; sin embargo, esto hará que se ejecute un script en la instancia remota de Analysis Services. Solo debería importar metadatos de un libro PowerPivot de plena confianza. Los datos se deben importar de los orígenes definidos en las conexiones a un origen de datos. Los datos copiados/pegados y los datos de la tabla vinculada del libro PowerPivot se deben copiar y pegar en el proyecto de modelos tabulares.  
  
#### <a name="to-create-a-new-tabular-model-project-from-a-powerpivot-for-excel-file"></a>Para crear un nuevo proyecto de modelo tabular desde un archivo de PowerPivot para Excel  
  
1.  En [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)], en el menú **Archivo** , haga clic en **Nuevo**y, a continuación, en **Proyecto**.  
  
2.  En el **nuevo proyecto** cuadro de diálogo **plantillas instaladas**, haga clic en **Business Intelligence**y, a continuación, haga clic en **importar desde PowerPivot**.  
  
3.  En  **Nombre**, escriba un nombre para el proyecto, después especifique una ubicación y un nombre de solución, y haga clic en **Aceptar**.  
  
4.  En el cuadro de diálogo **Abrir** , seleccione el archivo de [!INCLUDE[ssGeminiClient](../../includes/ssgeminiclient-md.md)] que contiene los metadatos del modelo y los datos que desea importar y, a continuación, haga clic en **Abrir**.  
  
## <a name="see-also"></a>Vea también  
 [Base de datos del área de trabajo &#40;Tabular de SSAS&#41;](workspace-database-ssas-tabular.md)   
 [Copiar y pegar datos &#40;Tabular de SSAS&#41;](../copy-and-paste-data-ssas-tabular.md)  
  
  
