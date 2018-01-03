---
title: Crear scripts mediante plantillas | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: sql-tools
ms.service: 
ms.component: ssms-tutorial
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: article
applies_to: SQL Server 2016
ms.assetid: ed48014c-3fc9-48ff-8c0f-8d1822195f14
caps.latest.revision: "28"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: 41b8e42e5af6b1fbdd5a094ba4df63938e2dea21
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 12/21/2017
---
# <a name="lesson-3-1---create-scripts-using-templates"></a>Lección 3.1: Crear scripts mediante plantillas
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)] Microsoft [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] ofrece un gran número de plantillas de script que incluyen instrucciones [!INCLUDE[tsql](../../includes/tsql-md.md)] para muchas tareas habituales. Estas plantillas contienen parámetros para los valores proporcionados por el usuario como, por ejemplo, un nombre de tabla. Mediante los parámetros, puede escribir el nombre una sola vez y copiarlo automáticamente en todas las ubicaciones necesarias del script. Puede crear sus propias plantillas personalizadas para los scripts que escriba con más frecuencia. También puede reorganizar el árbol de plantillas, mover las plantillas o crear carpetas nuevas para alojarlas. En la práctica siguiente, utilizará una plantilla para crear una base de datos, especificando una plantilla de intercalación.  
  
## <a name="using-templates"></a>Usar plantillas  
  
#### <a name="to-create-a-script-using-a-template"></a>Para crear un script mediante una plantilla  
  
1.  En [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)], en el menú **Ver** , haga clic en el **Explorador de plantillas**.  
  
2.  Las plantillas del Explorador de plantillas están organizadas en grupos. Expanda **Base de datos**y, después, haga doble clic en **Crear base de datos**.  
  
3.  En el cuadro de diálogo **Conectarse al motor de base de datos** , rellene la información de conexión y luego haga clic en **Conectar**. Se abrirá una ventana nueva del Editor de consultas, que incluye el contenido de la plantilla **Crear base de datos** .  
  
4.  En el menú **Consulta** , haga clic en **Especificar valores para parámetros de plantilla**.  
  
5.  En el cuadro de diálogo **Especificar valores para parámetros de plantilla** , la columna **Valor** contiene un valor recomendado para el parámetro **Nombre de la base de datos** . En el cuadro de parámetro **Nombre de la base de datos** , escriba **Marketing**y, después, haga clic en **Aceptar**. Observe que "Marketing" aparece en varias ubicaciones del script.  
  
## <a name="next-task-in-lesson"></a>Siguiente tarea de la lección  
[Crear plantillas personalizadas](../../tools/sql-server-management-studio/lesson-3-2-create-custom-templates.md)  
  
  
  
