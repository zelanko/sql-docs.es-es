---
title: Crear y administrar particiones en la base de datos del área de trabajo | Documentos de Microsoft
ms.custom: ''
ms.date: 02/22/2018
ms.prod: analysis-services
ms.prod_service: analysis-services, azure-analysis-services
ms.service: ''
ms.component: data-mining
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: conceptual
f1_keywords:
- sql13.asvs.bidtoolset.partitionmgr.f1
ms.assetid: 0b3027d6-652b-4eb3-a197-58b25df65218
caps.latest.revision: 15
author: Minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: 416181764e71d923a55b6a6dbd0b1448dc619476
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="create-and-manage-partitions-in-the-workspace-database"></a>Crear y administrar particiones en la base de datos del área de trabajo 
[!INCLUDE[ssas-appliesto-sqlas-aas](../../includes/ssas-appliesto-sqlas-aas.md)]
  Las particiones dividen una tabla en partes lógicas. A continuación, cada partición se puede procesar (actualizar) de forma independiente o en paralelo con otras particiones. Las particiones pueden mejorar la escalabilidad y facilitar el uso de bases de datos grandes. De forma predeterminada, cada tabla tiene una partición que incluye todas las columnas. Las tareas en este tema describe cómo crear y administrar particiones en la base de datos del área de trabajo de modelo mediante el **Partition Manager** cuadro de diálogo[!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)]  
  
 Una vez implementado un modelo en otra instancia de Analysis Services, los administradores de bases de datos pueden crear y administrar las particiones del modelo (implementado) mediante [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]. Para obtener más información, consulte [crear y administrar particiones de modelos tabulares](../../analysis-services/tabular-models/create-and-manage-tabular-model-partitions-ssas-tabular.md).  
  
> [!NOTE]  
>  No es posible mezclar particiones en la base de datos del área de trabajo del modelo usando el cuadro de diálogo Administrador de particiones. Solamente se pueden mezclar particiones en un modelo implementado mediante [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)].  
  
## <a name="tasks"></a>Tareas  
 Para crear y administrar particiones, deberá usar el cuadro de diálogo **Administrador de particiones** . Para ver el cuadro de diálogo **Administrador de particiones** , en [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)], haga clic en el menú **Tabla** y en **Particiones**.  
  
###  <a name="bkmk_create_new"></a> Para crear una partición  
  
1.  En el diseñador de modelos, seleccione la tabla en la que desea definir una partición.  
  
2.  Haga clic en el menú **Tabla** y en **Particiones**.  
  
3.  En **Administrador de particiones**, en el cuadro de lista **Tabla** , compruebe o seleccione la tabla en la que desea crear particiones y, a continuación, haga clic en **Nuevo**.  
  
4.  En **Nombre de partición**, escriba un nombre para la partición. De forma predeterminada, el nombre de la partición predeterminada se incrementará numéricamente para cada nueva partición.  
  
5.  Puede seleccionar las filas y las columnas que se incluirán en la partición mediante el modo de vista previa de tabla o mediante una consulta SQL creada con el Editor de consultas.  
  
     Para usar el modo de vista previa de tabla (valor predeterminado), haga clic en el botón **Vista previa de tabla** cerca de la esquina superior derecha de la ventana de vista previa. Seleccione las columnas que desea incluir en la partición activando la casilla situada junto al nombre de cada columna. Para filtrar las filas, haga clic con el botón secundario en un valor de celda y, a continuación, haga clic en **Filtrar por valor de celda seleccionado**.  
  
     Para usar una instrucción SQL, haga clic en el botón **Editor de consultas** cerca de la esquina superior derecha de la ventana de vista previa y, después, escriba o pegue una instrucción de consulta SQL en la ventana de consulta. Para validar la instrucción, haga clic **Validar**. Haga clic en **Diseño**para abrir el Diseñador de consultas.  
  
###  <a name="bkmk_copy"></a> Para copiar una partición  
  
1.  En **Administrador de particiones**, en el cuadro de lista **Tabla** , compruebe o seleccione la tabla que contiene la partición que desea copiar.  
  
2.  En la lista **Particiones** , seleccione la partición que desea copiar y haga clic en **Copiar**.  
  
3.  En **Nombre de partición**, escriba un nuevo nombre para la partición.  
  
###  <a name="bkmk_delete"></a> Para eliminar una partición  
  
1.  En **Administrador de particiones**, en el cuadro de lista **Tabla** , compruebe o seleccione la tabla que contiene la partición que desea eliminar.  
  
2.  En la lista **Particiones** , seleccione la partición que desea eliminar y haga clic en **Eliminar**.  
  
## <a name="see-also"></a>Vea también  
 [Particiones](../../analysis-services/tabular-models/partitions-ssas-tabular.md)   
 [Procesar particiones en la base de datos del área de trabajo](../../analysis-services/tabular-models/process-partitions-in-the-workspace-databse-ssas-tabular.md)  
  
  
