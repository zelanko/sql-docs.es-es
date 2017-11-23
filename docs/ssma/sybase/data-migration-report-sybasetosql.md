---
title: "Informe de migración de datos (SybaseToSQL) | Documentos de Microsoft"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology: sql-ssma
ms.tgt_pltfrm: 
ms.topic: article
applies_to:
- Azure SQL Database
- SQL Server
ms.assetid: bac234ef-bc16-47e6-8a7c-aa6e76d860c5
caps.latest.revision: "4"
author: Shamikg
ms.author: Shamikg
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 9823a7811ceb439e1c8395c7ff88385f56af2009
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/09/2017
---
# <a name="data-migration-report-sybasetosql"></a>Informe de migración de datos (SybaseToSQL)
El **informe de migración de datos** aparece el cuadro de diálogo después de migrar datos a [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)].  
  
## <a name="options"></a>Opciones  
**Estado**  
Muestra el estado de la migración de datos desde el origen de la base de datos de destino.  
  
**De**  
La tabla de origen.  
  
**Para**  
La tabla de destino.  
  
**Número total de filas**  
El número de filas de datos en la tabla de origen.  
  
**Número de filas migradas correctamente**  
El número de filas de datos se migró correctamente a la tabla de destino.  
  
**Proporción**  
El porcentaje de filas se migró correctamente.  
  
**Detalles**  
Si se produce un error en cualquier migración de datos, haga clic para mostrar los detalles de la migración para la fila seleccionada en el informe. SSMA mostrará el motivo del error.  
  
**Guardar informe**  
Guarda el informe a una. CSV, archivo (valores separados por comas), que se puede examinar con Microsoft Excel.  
  
