---
title: Nivel de compatibilidad (SSAS Tabular SP1) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.bidtoolset.versioncompat.f1
ms.assetid: 8943d78d-4a73-4be8-ad14-3d428f5abd06
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 4587dda82f8e6e3d02581ebcd5a13bf0005b14ed
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "62757625"
---
# <a name="compatibility-level-ssas-tabular-sp1"></a>Nivel de compatibilidad (SSAS tabular SP1)
  Puede especificar *ivel* al crear proyectos de modelos tabulares, actualizar proyectos de modelos tabulares existentes, actualizar los existentes implementadas las bases de datos de modelo Tabular, o importar libros PowerPivot.  
  
## <a name="compatibility-level"></a>Nivel de compatibilidad  
 Es una práctica habitual instalar las nuevas versiones y los Service Packs en equipos de desarrollo y de prueba antes de instalarlos en los equipos de producción. En estos casos, es importante comprender la configuración del nivel de compatibilidad tanto para los nuevos proyectos de modelos tabulares como para los que ya se han implementado en un entorno de producción.  
  
 Una instancia de Analysis Services de [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] admite los niveles de compatibilidad (versión de la base de datos) siguientes:  
  
-   SQL Server 2012 (1100)  
  
-   SQL Server 2012 SP1 (1103)  
  
-   SQL Server 2014 (1103)  
  
### <a name="set-compatibility-level-when-creating-a-new-tabular-model-project"></a>Configurar el nivel de compatibilidad al crear un nuevo proyecto de modelos tabulares  
 Al crear un nuevo proyecto de modelo Tabular en SQL Server Data Tools (SSDT), en el **opciones del proyecto Tabular nueva** cuadro de diálogo puede especificar el nivel de compatibilidad. Puede elegir entre crear un nuevo proyecto para implementarlo en una instancia de Analysis Services de [!INCLUDE[ssSQL11SP1](../../includes/sssql11sp1-md.md)] o posterior, o en una instancia de SQL Server 2012 Analysis Services (sin el Service Pack 1).  
  
 También puede especificar un nivel de compatibilidad predeterminado si selecciona la opción **No volver a mostrar este mensaje** . Todos los proyectos posteriores usarán el nivel de compatibilidad que especificó. Puede cambiar el nivel de compatibilidad predeterminado en SSDT en Opciones.  
  
### <a name="upgrade-an-existing-tabular-model-project-to-1103-compatibility-level"></a>Actualizar un proyecto de modelos tabulares existente al nivel de compatibilidad 1103  
 Puede actualizar un proyecto de modelos tabulares creado en SSDT antes de instalar [!INCLUDE[ssSQL11SP1](../../includes/sssql11sp1-md.md)] o posterior para que sea compatible con la versión de base de datos 1103 mediante el uso de la **ivel** propiedad en el modelo **propiedades**ventana. Para actualizar un proyecto de modelos tabulares, el equipo en el que está instalado SSDT debe tener instalado [!INCLUDE[ssSQL11SP1](../../includes/sssql11sp1-md.md)] o posterior y la instancia de Analysis Services en que reside la base de datos del área de trabajo también debe tener instalado [!INCLUDE[ssSQL11SP1](../../includes/sssql11sp1-md.md)] o posterior. No puede cambiar a una versión anterior.  
  
### <a name="upgrade-a-deployed-tabular-model-database-to-1103-compatibility-level"></a>Actualizar una base de datos de modelos tabulares implementada al nivel de compatibilidad 1103  
 Puede actualizar una versión de base de datos a la base de datos de modelos tabulares implementada existente 1103 compatible en SQL Server Management Studio (SSMS) mediante el **ivel** propiedad en **propiedades de la base de datos**. Para realizar la actualización, el equipo en el que está instalada la instancia de SQL Server Analysis Services debe tener [!INCLUDE[ssSQL11SP1](../../includes/sssql11sp1-md.md)] instalado. No puede cambiar a una versión anterior una base de datos de modelos tabulares implementada.  
  
### <a name="import-from-powerpivot"></a>Importar desde PowerPivot  
 Al crear un nuevo proyecto de modelos tabulares mediante la importación desde PowerPivot, puede especificar si desea actualizar el nivel de compatibilidad al predeterminado (si se ha configurado previamente en SSDT) o dejar el nivel de compatibilidad tal como está especificado en el libro PowerPivot.  
  
### <a name="check-compatibility-level-for-a-tabular-model-database-in-ssms"></a>Comprobar el nivel de compatibilidad para una base de datos de modelos tabulares en SSMS  
 Puede comprobar el nivel de compatibilidad para una base de datos de modelos tabulares en SSMS si examina el **ivel** propiedad (nuevo en [!INCLUDE[ssSQL11SP1](../../includes/sssql11sp1-md.md)]) en **propiedades de la base de datos**.  
  
### <a name="check-supported-compatibility-level-for-an-analysis-services-instance-in-ssms"></a>Comprobar el nivel de compatibilidad admitido para una instancia de Analysis Services en SSMS  
 Puede comprobar el nivel de compatibilidad admitido en SSMS si examina el **nivel de compatibilidad admitido** propiedad en el **información** página (nuevo en [!INCLUDE[ssSQL11SP1](../../includes/sssql11sp1-md.md)]) en **Analysis Propiedades de los servicios**. Un nivel de compatibilidad admitido de 1103 indica que está instalado SQL Server SP1 o posterior. El nivel de compatibilidad admitido no se puede cambiar.  
  
  
