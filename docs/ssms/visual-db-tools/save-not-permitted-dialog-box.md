---
title: "Cuadro de diálogo Guardar (no se permite) | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: sql-non-specified
ms.service: 
ms.component: ssms-visual-db
ms.reviewer: 
ms.suite: sql
ms.technology: tools-ssms
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords: sql13.swb.table.tablerecreatenosave.f1
ms.assetid: 7efda8e3-739f-4c97-a497-b8808a0acbea
caps.latest.revision: "4"
author: stevestein
ms.author: sstein
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: d1224061affb1882d717f184f974a176d30a24a8
ms.sourcegitcommit: b2d8a2d95ffbb6f2f98692d7760cc5523151f99d
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 12/05/2017
---
# <a name="save-not-permitted-dialog-box"></a>Guardar (no se permite), (cuadro de diálogo)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)] El cuadro de diálogo **Guardar** (no permitido) advierte de que no se permite guardar cambios porque los cambios realizados requieren que se quiten y se vuelvan a crear las tablas enumeradas.  
  
Las acciones siguientes pueden requerir que se vuelva a crear una tabla:  
  
-   Agregar una nueva columna en la mitad de la tabla  
  
-   Quitar una columna  
  
-   Cambiar la nulabilidad de columnas  
  
-   Cambiar el orden de las columnas  
  
-   Cambiar el tipo de datos de una columna  
  
Cambiar esta opción, en el menú **Herramientas** , haga clic en **Opciones**, expanda **Diseñadores**y, a continuación, haga clic en **Diseñadores de tablas y bases de datos**. Active o desactive la casilla **Impedir guardar cambios que requieran volver a crear tablas** .  
  
