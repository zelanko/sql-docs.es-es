---
description: Guardar script de cambio (cuadro de diálogo, Visual Database Tools)
title: Cuadro de diálogo Guardar script de cambios
ms.custom: seo-lt-2019
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.technology: ssms
ms.topic: conceptual
f1_keywords:
- vdt.dlgbox.generatechangescript
- vdtsql.chm:65544
ms.assetid: fc9d1639-5efa-44fe-a04f-4d4d0def2833
author: markingmyname
ms.author: maghan
ms.reviewer: ''
ms.openlocfilehash: 7388283d4605547a400c284c2499e4f0d9c4db46
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/17/2020
ms.locfileid: "88468344"
---
# <a name="save-change-script-dialog-box-visual-database-tools"></a>Guardar script de cambio (cuadro de diálogo, Visual Database Tools)
[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]
Este cuadro de diálogo muestra el script [!INCLUDE[tsql](../../includes/tsql-md.md)] de los cambios que ha realizado desde que se guardó la tabla por última vez. Permite guardar el script en un archivo de texto en la ubicación que elija.  
  
Puede tener acceso a este cuadro de diálogo después de realizar cambios sin guardarlos en una tabla del Diseñador de tablas. En el menú **Diseñador de tablas** , haga clic en **Generar script de cambio**.  
  
> [!NOTE]  
> Los scripts de cambio proporcionados por Visual Database Tools no incluyen ningún control de errores. Asumen que los objetos de base de datos no han cambiado desde que se abrió la herramienta y que, por lo tanto, no habrá problemas relacionados con los cambios. Antes de ejecutar un script de cambio, debe incluir las instrucciones de control de errores apropiadas.  
  
## <a name="options"></a>Opciones  
**Generar automáticamente script de cambio al guardar**  
Si esta opción está activada, el cuadro de diálogo **Guardar script de cambio** aparecerá cada vez que guarde los cambios en una tabla.  
  
**Sí**  
Abre el cuadro de diálogo **Guardar** , en el que puede elegir la ubicación del archivo de texto.  
  
**No**  
Cancela la creación del script de cambio.  
  
