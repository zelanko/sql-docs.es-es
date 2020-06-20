---
title: Cuadro de diálogo Guardar script de cambio (Visual Database Tools) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
f1_keywords:
- vdt.dlgbox.generatechangescript
- vdtsql.chm:65544
ms.assetid: fc9d1639-5efa-44fe-a04f-4d4d0def2833
author: stevestein
ms.author: sstein
ms.openlocfilehash: 19a2bb2ce9a219c195421e2efa203fc115e1ae1b
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/18/2020
ms.locfileid: "85044262"
---
# <a name="save-change-script-dialog-box-visual-database-tools"></a>Guardar script de cambio (cuadro de diálogo, Visual Database Tools)
  Este cuadro de diálogo muestra el script [!INCLUDE[tsql](../../includes/tsql-md.md)] de los cambios que ha realizado desde que se guardó la tabla por última vez. Permite guardar el script en un archivo de texto en la ubicación que elija.  
  
 Puede tener acceso a este cuadro de diálogo después de realizar cambios sin guardarlos en una tabla del Diseñador de tablas. En el menú **Diseñador de tablas** , haga clic en **Generar script de cambio**.  
  
> [!NOTE]  
>  Los scripts de cambio proporcionados por Visual Database Tools no incluyen ningún control de errores. Asumen que los objetos de base de datos no han cambiado desde que se abrió la herramienta y que, por lo tanto, no habrá problemas relacionados con los cambios. Antes de ejecutar un script de cambio, debe incluir las instrucciones de control de errores apropiadas.  
  
## <a name="options"></a>Opciones  
 **Generar automáticamente script de cambio al guardar**  
 Si esta opción está activada, el cuadro de diálogo **Guardar script de cambio** aparecerá cada vez que guarde los cambios en una tabla.  
  
 **Sí**  
 Abre el cuadro de diálogo **Guardar** , en el que puede elegir la ubicación del archivo de texto.  
  
 **No**  
 Cancela la creación del script de cambio.  
  
  
