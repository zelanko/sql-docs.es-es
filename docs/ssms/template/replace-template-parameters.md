---
title: "Reemplazar los parámetros de plantilla | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- tools-ssms
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.swb.templates.replaceparameters.f1
helpviewer_keywords:
- template parameters [Template Explorer]
- templates [Transact-SQL], replacing parameters
- Replace (Query) Template Parameters dialog box
- replacing template parameters
ms.assetid: 1234aa14-3464-4a3e-922a-5cfb8fb23627
caps.latest.revision: 4
author: stevestein
ms.author: sstein
manager: jhubbard
translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 46e39ef54d2caf54cf68fa3ff3823d9111c05e0d
ms.lasthandoff: 04/11/2017

---
# <a name="replace-template-parameters"></a>Reemplazar los parámetros de plantilla
Las plantillas contienen parámetros que se pueden reemplazar por valores específicos de la implementación cada vez que se use la plantilla. Después de abrir una plantilla en un editor de código, puede reemplazar los parámetros por valores relevantes para su implementación.  
  
## <a name="before-you-begin"></a>Antes de comenzar  
El cuadro de diálogo **Especificar valores para parámetros de plantilla** es una cuadrícula de tres columnas. Las columnas **Parámetro** y **Tipo** son de solo lectura y no se pueden cambiar. Revise el contenido de la columna **Valor** y cambie cualquiera de los valores predeterminados por los valores adecuados para su implementación.  
  
Para usar este cuadro de diálogo, los parámetros del script deben aparecer entre corchetes angulares (`< >`) in con el formato `<`*parameter_name*`,` *data_type*`,` *default_value*`>`.  
  
## <a name="replace-template-parameters"></a>Reemplazar los parámetros de plantilla  
Después de abrir la plantilla en una ventana del editor de código:  
  
1.  En el menú **Consulta** , haga clic en **Especificar valores para parámetros de plantilla**.  
  
2.  En el cuadro de diálogo **Especificar valores para parámetros de plantilla** , la columna **Valores** contiene un valor sugerido para cada parámetro. Acepte el valor o reemplácelo por otro nuevo.  
  
3.  Haga clic en **Aceptar** para cerrar el cuadro de diálogo **Reemplazar parámetros de plantilla** y modificar el script en el editor de consultas.  
  
## <a name="see-also"></a>Vea también  
[Explorador de plantillas](../../ssms/template/template-explorer.md)  
[Abrir una plantilla](../../ssms/template/open-a-template.md)  
  

