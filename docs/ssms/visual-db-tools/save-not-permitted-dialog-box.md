---
title: "Cuadro de diálogo Guardar (no se permite) | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: sql-tools
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
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: e20cf232c629564cb43bcaaa0e3e8ce184ec04f8
ms.sourcegitcommit: b6116b434d737d661c09b78d0f798c652cf149f3
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 01/17/2018
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
  
