---
title: Incluir una tabla en un script | Microsoft Docs
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-non-specified
ms.prod_service: sql-tools
ms.service: 
ms.component: ssms-tutorial
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: ea88d736-849e-4368-b55d-06aeee097bf3
caps.latest.revision: "31"
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: c047fd16f30998d831977ae422b68d40ab50513b
ms.sourcegitcommit: b6116b434d737d661c09b78d0f798c652cf149f3
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 01/17/2018
---
# <a name="lesson-2-6---script-a-table"></a>Lección 2.6: Incluir una tabla en un script
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] puede crear scripts para seleccionar, insertar, actualizar y eliminar tablas, y para crear, modificar, quitar o ejecutar procedimientos almacenados.  
  
En ocasiones, necesitará un script que ofrezca varias opciones como, por ejemplo, quitar un procedimiento y, a continuación, crear otro, o bien crear una tabla y modificarla posteriormente. Para crear scripts combinados, guarde el primer script en una ventana del Editor de consultas y el segundo en el Portapapeles para poder pegarlo en la ventana a continuación del primero.  
  
 
1.  En el Explorador de objetos, expanda el servidor, **Bases de datos**, [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)]y **Tablas**; haga clic con el botón derecho en **HumanResources.Employee**y, después, señale **Incluir tabla como**.  
  
2.  El menú contextual tiene siete opciones de scripting disponibles: **CREATE To**, **DROP To**, **DROP y CREATE To**, **SELECT To**, **INSERT To**, **UPDATE To**y **DELETE To**. Seleccione **UPDATE To**y haga clic en **Nueva ventana del Editor de consultas**.  
  
3.  Se abre una ventana nueva del Editor de consultas que establece una conexión y presenta la instrucción completa actualizada.  
  
    Este ejercicio muestra cómo la característica de scripting puede hacer mucho más que crear un script para una tabla o un procedimiento almacenado. Esta nueva función puede ayudarle a agregar scripts de manipulación de datos a su proyecto y a crear fácilmente script para la ejecución de procedimientos almacenados. Esto puede ahorrarle mucho tiempo en el caso de tablas y procedimientos con muchos campos.  
  
 
  
  
  
