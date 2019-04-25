---
title: Crear y administrar particiones de modelos tabulares | Microsoft Docs
ms.date: 05/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: tabular-models
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 7067449c0de9958e98a7a9dc5cc09c7f89f33fa9
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "62472297"
---
# <a name="create-and-manage-tabular-model-partitions"></a>Crear y administrar particiones de modelos tabulares
[!INCLUDE[ssas-appliesto-sqlas-aas](../../includes/ssas-appliesto-sqlas-aas.md)]

  Las particiones dividen una tabla en partes lógicas. A continuación, cada partición se puede procesar (actualizar) de forma independiente de las demás particiones. Las particiones definidas para un modelo durante la creación de modelos se duplican en un modelo implementado. Una vez realizada la implementación, puede administrar esas particiones mediante el cuadro de diálogo **Particiones** de [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] o mediante un script. Las tareas proporcionadas en este tema describen cómo crear y administrar particiones en un modelo implementado.  
  
  > [!NOTE]  
>  Las particiones en modelos tabulares creados en el nivel de compatibilidad 1400 se definen mediante una instrucción de consulta M. Para obtener más información, consulte [M referencia](https://msdn.microsoft.com/library/mt211003.aspx). 
>
  
## <a name="tasks"></a>Tareas  
 Para crear y administrar particiones en una base de datos de modelos tabulares implementada, usará el cuadro de diálogo **Particiones** de [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]. Para ver el cuadro de diálogo **Particiones** , en [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], haga clic con el botón derecho en una tabla y, después, haga clic en **Particiones**.  
  
###  <a name="bkmk_create_new"></a> Para crear una partición  
  
1.  En el cuadro de diálogo **Particiones** , haga clic en el botón **Nuevo** .  
  
2.  En **Nombre de partición**, escriba un nombre para la partición. De forma predeterminada, el nombre de la partición predeterminada se incrementará numéricamente para cada nueva partición.  
  
3.  En **instrucción de consulta**, escriba o pegue una instrucción de consulta SQL o M que define las columnas y las cláusulas que desea incluir en la partición en la ventana de consulta.  
  
4.  Para validar la instrucción, haga clic en **Comprobar sintaxis**.  
  
###  <a name="bkmk_copy"></a> Para copiar una partición  
  
1.  En el cuadro de diálogo **Particiones** , en la lista **Particiones** , seleccione la partición que desea copiar y, a continuación, haga clic en el botón **Copiar** .  
  
2.  En **Nombre de partición**, escriba un nuevo nombre para la partición.  
  
3.  En **instrucción de consulta**, editar la instrucción de consulta.  
  
###  <a name="bkmk_merge"></a> Para combinar dos o más particiones  
  
-   En el cuadro de diálogo **Particiones** , en la lista **Particiones** , use Ctrl+clic para seleccionar las particiones que quiere combinar y, después, haga clic en el botón **Combinar** .  
  
> [!IMPORTANT]  
>  Al combinar las particiones no se actualizan los metadatos de la partición. Debe editar la instrucción SQL o M para la partición resultante para asegurarse de que las operaciones de procesamiento procesan todos los datos de la partición combinada.  
  
###  <a name="bkmk_delete"></a> Para eliminar una partición  
  
-   En el cuadro de diálogo **Particiones** , en la lista **Particiones** , seleccione la partición que desea eliminar y, a continuación, haga clic en el botón **Eliminar** .  
  
## <a name="see-also"></a>Vea también  
 [Particiones de modelos tabulares](../../analysis-services/tabular-models/tabular-model-partitions-ssas-tabular.md)   
 [Particiones de modelos tabulares procesos](../../analysis-services/tabular-models/process-tabular-model-partitions-ssas-tabular.md)  
  
  
