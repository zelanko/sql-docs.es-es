---
title: "Crear y administrar particiones de modelos tabulares (SSAS tabular) | Microsoft Docs"
ms.custom: ""
ms.date: "03/01/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "analysis-services"
  - "analysis-services/multidimensional-tabular"
  - "analysis-services/data-mining"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: dab72cf0-95bc-4b63-95dc-505b5cd881c1
caps.latest.revision: 8
author: "Minewiskan"
ms.author: "owend"
manager: "erikre"
caps.handback.revision: 8
---
# Crear y administrar particiones de modelos tabulares (SSAS tabular)
  Las particiones dividen una tabla en partes lógicas. A continuación, cada partición se puede procesar (actualizar) de forma independiente de las demás particiones. Las particiones definidas para un modelo durante la creación de modelos se duplican en un modelo implementado. Una vez realizada la implementación, puede administrar esas particiones mediante el cuadro de diálogo **Particiones** de [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] o mediante un script. Las tareas proporcionadas en este tema describen cómo crear y administrar particiones en un modelo implementado.  
  
 En este tema se incluyen las tareas siguientes:  
  
-   [Para crear una partición](#bkmk_create_new)  
  
-   [Para copiar una partición](#bkmk_copy)  
  
-   [Para combinar dos o más particiones](#bkmk_merge)  
  
-   [Para eliminar una partición](#bkmk_delete)  
  
## Tareas  
 Para crear y administrar particiones en una base de datos de modelos tabulares implementada, usará el cuadro de diálogo **Particiones** de [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]. Para ver el cuadro de diálogo **Particiones**, en [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], haga clic con el botón derecho en una tabla y, después, haga clic en **Particiones**.  
  
###  <a name="bkmk_create_new"></a> Para crear una partición  
  
1.  En el cuadro de diálogo **Particiones** , haga clic en el botón **Nuevo** .  
  
2.  En **Nombre de partición**, escriba un nombre para la partición. De forma predeterminada, el nombre de la partición predeterminada se incrementará numéricamente para cada nueva partición.  
  
3.  En **Instrucción SQL**, escriba o pegue una instrucción de consulta SQL que defina las columnas y las cláusulas que desea incluir en la partición en la ventana de consulta.  
  
4.  Para validar la instrucción, haga clic en **Comprobar sintaxis**.  
  
###  <a name="bkmk_copy"></a> Para copiar una partición  
  
1.  En el cuadro de diálogo **Particiones** , en la lista **Particiones** , seleccione la partición que desea copiar y, a continuación, haga clic en el botón **Copiar** .  
  
2.  En **Nombre de partición**, escriba un nuevo nombre para la partición.  
  
3.  En **Instrucción SQL**, edite la instrucción de consulta SQL.  
  
###  <a name="bkmk_merge"></a> Para combinar dos o más particiones  
  
-   En el cuadro de diálogo **Particiones**, en la lista **Particiones**, use Ctrl+clic para seleccionar las particiones que quiere combinar y, después, haga clic en el botón **Combinar**.  
  
> [!IMPORTANT]  
>  Al combinar las particiones no se actualizan los metadatos de la partición. Los administradores deben modificar la instrucción SQL para la partición resultante a fin de asegurarse de que las operaciones de procesamiento procesan todos los datos de la partición combinada.  
  
###  <a name="bkmk_delete"></a> Para eliminar una partición  
  
-   En el cuadro de diálogo **Particiones** , en la lista **Particiones** , seleccione la partición que desea eliminar y, a continuación, haga clic en el botón **Eliminar** .  
  
## Vea también  
 [Particiones de modelos tabulares &#40;SSAS tabular&#41;](../../analysis-services/tabular-models/tabular-model-partitions-ssas-tabular.md)   
 [Procesar particiones de modelos tabulares &#40;SSAS tabular&#41;](../../analysis-services/tabular-models/process-tabular-model-partitions-ssas-tabular.md)  
  
  