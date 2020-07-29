---
title: Guardar (no se permite), (cuadro de diálogo)
ms.custom: seo-lt-2019
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.technology: ssms
ms.topic: conceptual
f1_keywords:
- sql13.swb.table.tablerecreatenosave.f1
ms.assetid: 7efda8e3-739f-4c97-a497-b8808a0acbea
author: markingmyname
ms.author: maghan
ms.reviewer: ''
ms.openlocfilehash: b6bd4471f14d662b6167c00d599eccf61b7dcced
ms.sourcegitcommit: f3321ed29d6d8725ba6378d207277a57cb5fe8c2
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/06/2020
ms.locfileid: "86010646"
---
# <a name="save-not-permitted-dialog-box"></a>Guardar (no se permite), (cuadro de diálogo)
[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]
El cuadro de diálogo **Guardar** (no se permite) advierte de que no se permite guardar cambios porque los cambios realizados requieren que se quiten y se vuelvan a crear las tablas enumeradas.  
  
Las acciones siguientes pueden requerir que se vuelva a crear una tabla:  
  
-   Agregar una nueva columna en la mitad de la tabla  
  
-   Quitar una columna  
  
-   Cambiar la nulabilidad de columnas  
  
-   Cambiar el orden de las columnas  
  
-   Cambiar el tipo de datos de una columna  
  
Cambiar esta opción, en el menú **Herramientas** , haga clic en **Opciones**, expanda **Diseñadores**y, a continuación, haga clic en **Diseñadores de tablas y bases de datos**. Active o desactive la casilla **Impedir guardar cambios que requieran volver a crear tablas** .  
  
