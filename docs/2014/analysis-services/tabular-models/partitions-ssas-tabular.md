---
title: Particiones (SSAS Tabular) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
ms.assetid: 708b9bdf-8c0b-4476-809a-8f616be23a58
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 0cb150e2bf076c6cef4e05d626b71eaab05d64a6
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/02/2018
ms.locfileid: "48197217"
---
# <a name="partitions-ssas-tabular"></a>Particiones (SSAS tabular)
  Las particiones dividen una tabla en partes lógicas. A continuación, cada partición se puede procesar (actualizar) de forma independiente de las demás particiones. Las particiones que se crean mediante el cuadro de diálogo Particiones de [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] durante la creación de modelos se aplican a la base de datos del área de trabajo del modelo. Una vez implementado el modelo, las particiones definidas para la base de datos del área de trabajo del modelo se duplican en la base de datos del modelo implementada. Además, puede crear y administrar particiones para una base de datos del modelo implementada usando el cuadro de diálogo Particiones de [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)].  En este tema se describen las particiones que se crean durante la creación de modelos con el cuadro de diálogo Administrador de particiones de [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]. Para obtener información sobre cómo crear y administrar particiones para un modelo implementado, vea [Crear y administrar particiones de modelos tabulares &#40;SSAS tabular&#41;](create-and-manage-tabular-model-partitions-ssas-tabular.md).  
  
 Secciones de este tema:  
  
-   [Ventajas](#bkmk_benefits)  
  
-   [Tareas relacionadas](#bkmk_related_tasks)  
  
##  <a name="bkmk_benefits"></a> Ventajas  
 En los modelos tabulares, las particiones dividen una tabla en objetos de partición lógicos. A continuación, cada partición se puede procesar de forma independiente de las demás particiones. Por ejemplo, una tabla puede incluir ciertos conjuntos de filas cuyos datos apenas cambian y otros conjuntos de filas cuyos datos cambian con frecuencia. En estos casos, no hay necesidad de procesar todos los datos si solo se desea procesar una parte de ellos. Las particiones le permiten separar los datos que necesita procesar con frecuencia de los datos que se pueden procesar con una frecuencia menor.  
  
 Un diseño de modelos eficientes usa particiones para eliminar el procesamiento innecesario y la subsiguiente carga del procesador en los servidores de Analysis Services, asegurándose al mismo tiempo de que los datos se procesan y actualizan con la frecuencia suficiente para reflejar los datos más recientes de los orígenes de datos. El modo en que se implementan y usan las particiones durante la creación de modelos puede ser muy diferente del modo en que se implementan y se usan en los modelos implementados. Tenga presente que durante la fase de creación del modelo, es posible que trabaje con un único subconjunto de datos que finalmente estará en el modelo implementado.  
  
### <a name="processing-partitions"></a>Procesar particiones  
 En los modelos implementados, el procesamiento se realiza mediante [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], o ejecutando un script que incluya el comando Procesar y especifique las opciones y la configuración del procesamiento. Cuando cree modelos con [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)], podrá ejecutar operaciones de procesamiento con el comando Procesar del menú Modelo o de la barra de herramientas. Una operación de procesamiento se puede especificar para una partición, una tabla o para todas ellas.  
  
 Cuando se ejecuta una operación de procesamiento, se realiza una conexión con el origen de datos usando la conexión de datos. Los nuevos datos se importan en las tablas del modelo, las relaciones y las jerarquías se vuelven a generar para cada tabla, y se vuelven a realizar los cálculos de las medidas y columnas calculadas.  
  
 Mediante una mayor división de una tabla en particiones lógicas, puede determinar de forma selectiva qué datos se procesan de cada partición, y cuándo y cómo se procesan. Cuando se implementa un modelo, el procesamiento de las particiones se puede completar manualmente mediante el cuadro de diálogo Particiones de [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], o mediante un script que ejecute un comando Procesar.  
  
### <a name="partitions-in-the-model-workspace-database"></a>Particiones en la base de datos del área de trabajo del modelo  
 Con el Administrador de partición de [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)], puede crear nuevas particiones, y editar, combinar y eliminar particiones existentes. El Administrador de particiones proporciona dos modos para seleccionar las tablas, las filas y las columnas de una partición: el modo de vista previa de la tabla y el modo de consulta SQL. Todas las particiones se definen mediante una consulta SQL; sin embargo, con el modo de vista previa de tabla, puede obtener una vista previa y seleccionar los datos que desea incluir en la partición. La consulta SQL se crea y se valida automáticamente. Dado que el modo de vista previa de la tabla es la misma vista previa que aparece en el cuadro de diálogo Editar propiedades de tabla y en la página de vista previa del Asistente para la importación de tablas, el número máximo de filas de la vista previa es de 50.  
  
### <a name="partitions-in-a-deployed-model-database"></a>Particiones en una base de datos del modelo implementada  
 Cuando se implementa un modelo, las particiones de la base de datos del modelo implementada aparecen como objetos de base de datos de [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]. Puede crear, modificar, combinar y eliminar particiones de un modelo implementado con el cuadro de diálogo Particiones de [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]. Administrar particiones para un modelo implementado en [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] queda fuera del ámbito de este tema. Para obtener información sobre cómo administrar particiones en [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], vea [Crear y administrar particiones de modelos tabulares &#40;SSAS tabular&#41;](create-and-manage-tabular-model-partitions-ssas-tabular.md).  
  
##  <a name="bkmk_related_tasks"></a> Tareas relacionadas  
  
|Tema|Descripción|  
|-----------|-----------------|  
|[Crear y administrar particiones en la base de datos del área de trabajo &#40;Tabular de SSAS&#41;](workspace-database-ssas-tabular.md)|Describe cómo crear y administrar las particiones de la base de datos del área de trabajo del modelo con el Administrador de particiones de [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)].|  
|[Procesar particiones en la base de datos del área de trabajo &#40;Tabular de SSAS&#41;](process-partitions-in-the-workspace-databse-ssas-tabular.md)|Describe cómo procesar (actualizar) particiones en la base de datos del área de trabajo del modelo.|  
  
## <a name="see-also"></a>Vea también  
 [Modo DirectQuery &#40;SSAS tabular&#41;](directquery-mode-ssas-tabular.md)   
 [Procesar datos &#40;Tabular de SSAS&#41;](../process-data-ssas-tabular.md)  
  
  
