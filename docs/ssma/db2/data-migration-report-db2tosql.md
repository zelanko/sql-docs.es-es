---
title: Informe de migración de datos (DB2ToSQL) | Documentos de Microsoft
ms.prod: sql
ms.prod_service: sql-tools
ms.component: ssma-db2
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.technology: ssma
ms.tgt_pltfrm: ''
ms.topic: conceptual
applies_to:
- Azure SQL Database
- SQL Server
ms.assetid: 46ebada7-db36-4ae9-b7ae-baa4b854b237
caps.latest.revision: 4
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.openlocfilehash: bba7d7e2734ad40d47e6e7e0037df6406e97b0ca
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="data-migration-report-db2tosql"></a>Informe de migración de datos (DB2ToSQL)
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
  
