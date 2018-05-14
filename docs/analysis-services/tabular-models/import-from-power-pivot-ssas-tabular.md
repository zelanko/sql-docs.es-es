---
title: Importación desde PowerPivot | Documentos de Microsoft
ms.date: 05/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: tabular-models
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 63a1619b09475bfa0ec8d4a1f21aaf88791a5b6c
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/10/2018
---
# <a name="import-from-power-pivot"></a>Importación desde PowerPivot 
[!INCLUDE[ssas-appliesto-sqlas-aas](../../includes/ssas-appliesto-sqlas-aas.md)]
  Este artículo describe cómo crear un nuevo proyecto de modelos tabulares importando los metadatos y los datos de un [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] libro mediante el uso de la importación de [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] plantilla de proyecto en [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)].  
  
## <a name="create-a-new-tabular-model-from-a-power-pivot-for-excel-file"></a>Creación de un nuevo modelo tabular desde un archivo de PowerPivot para Excel  
 Al crear un nuevo proyecto de modelos tabulares importando desde un libro [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] , los metadatos que definen la estructura del libro se usan para crear y definir la estructura del proyecto de modelo tabular en [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)]. Los objetos como tablas, columnas, medidas y relaciones se conservan, y aparecerán en el proyecto de modelos tabulares tal como están en el libro [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] . No se realizan cambios en el archivo de libro .xlsx.  
  
> [!NOTE]  
>  Los modelos tabulares no admiten tablas vinculadas. Al importar datos de un libro [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] que contiene una tabla vinculada, los datos de la tabla vinculada se tratan como datos copiados y pegados y se almacenan en el archivo Model.bim. Al ver las propiedades de una tabla copiada y pegada, la propiedad **Datos de origen** está deshabilitada y el cuadro de diálogo **Propiedades de la tabla** del menú **Tabla** está deshabilitado.  
>   
>  Hay un límite de 10 000 filas que se pueden agregar a los datos incrustados en el modelo. Si importa un modelo de [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] y aparece el error "Los datos se truncaron. Las tablas pegadas no pueden contener más de 10 000 filas”, revise el modelo de [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] moviendo los datos incrustados a otro origen de datos (por ejemplo, a una tabla de SQL Server) y, después, vuelva a importarlos.  
  
 Existen consideraciones especiales que dependen de si la base de datos del área de trabajo está o no en una instancia de Analysis Services del mismo equipo (local) como [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] o está en una instancia remota de Analysis Services.  
  
 Si la base de datos del área de trabajo está en una instancia local de Analysis Services, puede importar los metadatos y datos del libro [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] . Los metadatos se copian del libro y se usan para crear el proyecto de modelos tabulares. A continuación, se copian los datos del libro y se almacenan en la base de datos del área de trabajo del proyecto (excepto los datos copiados/pegados, que se almacenan en el archivo Model.bim).  
  
 Si la base de datos del área de trabajo está en una instancia remota de Analysis Services, no podrá importar datos de un libro [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] para Excel. Todavía puede importar metadatos del libro; sin embargo, esto hará que se ejecute un script en la instancia remota de Analysis Services. Solo debería importar metadatos de un libro [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] de plena confianza. Los datos se deben importar de los orígenes definidos en las conexiones a un origen de datos. Los datos copiados/pegados y los datos de la tabla vinculada del libro [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] han de copiarse y pegarse en el proyecto de modelos tabulares.  
  
#### <a name="to-create-a-new-tabular-model-project-from-a-power-pivot-for-excel-file"></a>Para crear un nuevo proyecto de modelos tabulares a partir de un archivo de PowerPivot para Excel  
  
1.  En [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)], en el menú **Archivo** , haga clic en **Nuevo**y, a continuación, en **Proyecto**.  
  
2.  En el cuadro de diálogo **Nuevo proyecto**, debajo de **Plantillas instaladas**, haga clic en **Business Intelligence** y, después, en **Importar del [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)]**.  
  
3.  En  **Nombre**, escriba un nombre para el proyecto, después especifique una ubicación y un nombre de solución, y haga clic en **Aceptar**.  
  
4.  En el cuadro de diálogo **Abrir** , seleccione el archivo de [!INCLUDE[ssGeminiClient](../../includes/ssgeminiclient-md.md)] que contiene los metadatos del modelo y los datos que desea importar y, a continuación, haga clic en **Abrir**.  
  
## <a name="see-also"></a>Vea también  
 [Base de datos del área de trabajo](../../analysis-services/tabular-models/workspace-database-ssas-tabular.md)   
 [Copiar y pegar datos](../../analysis-services/tabular-models/ssas-import-data-copy-and-paste-data.md)  
  
  
