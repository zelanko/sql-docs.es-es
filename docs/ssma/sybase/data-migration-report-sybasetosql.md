---
title: Informe de migración de datos (SybaseToSQL) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.reviewer: ''
ms.suite: sql
ms.technology: ssma
ms.tgt_pltfrm: ''
ms.topic: conceptual
applies_to:
- Azure SQL Database
- SQL Server
ms.assetid: bac234ef-bc16-47e6-8a7c-aa6e76d860c5
caps.latest.revision: 4
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.openlocfilehash: 9e1f04f6a5df77be0bfc13227e1033842b5dd291
ms.sourcegitcommit: 603d2e588ac7b36060fa0cc9c8621ff2a6c0fcc7
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/14/2018
ms.locfileid: "40392814"
---
# <a name="data-migration-report-sybasetosql"></a>Informe de migración de datos (SybaseToSQL)
El **informe de migración de datos** aparece el cuadro de diálogo después de migrar datos a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
## <a name="options"></a>Opciones  
**Estado**  
Muestra el estado de la migración de datos desde el origen de la base de datos de destino.  
  
**De**  
La tabla de origen.  
  
**Para**  
La tabla de destino.  
  
**Número total de filas**  
El número de filas de datos en la tabla de origen.  
  
**Número de filas se migró correctamente**  
El número de filas de datos se migrado correctamente a la tabla de destino.  
  
**Relación**  
El porcentaje de filas se migrado correctamente.  
  
**Detalles**  
Si se produjo un error en cualquier migración de datos, haga clic para mostrar los detalles de la migración de la fila seleccionada en el informe. SSMA mostrará el motivo del error.  
  
**Guardar informe**  
Guarda el informe a una. CSV, archivo (valores separados por comas), que se puede examinar con Microsoft Excel.  
  
