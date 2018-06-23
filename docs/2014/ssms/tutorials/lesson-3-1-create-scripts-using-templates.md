---
title: Crear scripts mediante plantillas | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- tools-ssms
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: ed48014c-3fc9-48ff-8c0f-8d1822195f14
caps.latest.revision: 27
author: craigg-msft
ms.author: craigg
manager: jhubbard
ms.openlocfilehash: 82ec1d5e44fd87b4a15e51a29bd2963c1aa1bd44
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36200261"
---
# <a name="create-scripts-using-templates"></a>Crear scripts mediante plantillas
  Microsoft [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] ofrece un gran número de plantillas de script que incluyen instrucciones [!INCLUDE[tsql](../../includes/tsql-md.md)] para muchas de las tareas habituales. Estas plantillas contienen parámetros para los valores proporcionados por el usuario como, por ejemplo, un nombre de tabla. Mediante los parámetros, puede escribir el nombre una sola vez y copiarlo automáticamente en todas las ubicaciones necesarias del script. Puede crear sus propias plantillas personalizadas para los scripts que escriba con más frecuencia. También puede reorganizar el árbol de plantillas, mover las plantillas o crear carpetas nuevas para alojarlas. En la práctica siguiente, utilizará una plantilla para crear una base de datos, especificando una plantilla de intercalación.  
  
## <a name="using-templates"></a>Usar plantillas  
  
#### <a name="to-create-a-script-using-a-template"></a>Para crear un script mediante una plantilla  
  
1.  En [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)], en el menú **Ver** , haga clic en el **Explorador de plantillas**.  
  
2.  Las plantillas del Explorador de plantillas están organizadas en grupos. Expanda **Base de datos**y, después, haga doble clic en **Crear base de datos**.  
  
3.  En el cuadro de diálogo **Conectarse al motor de base de datos** , rellene la información de conexión y luego haga clic en **Conectar**. Se abrirá una ventana nueva del Editor de consultas, que incluye el contenido de la plantilla **Crear base de datos** .  
  
4.  En el menú **Consulta** , haga clic en **Especificar valores para parámetros de plantilla**.  
  
5.  En el cuadro de diálogo **Especificar valores para parámetros de plantilla** , la columna **Valor** contiene un valor recomendado para el parámetro **Nombre de la base de datos** . En el cuadro de parámetro **Nombre de la base de datos** , escriba **Marketing**y, después, haga clic en **Aceptar**. Observe que "Marketing" aparece en varias ubicaciones del script.  
  
## <a name="next-task-in-lesson"></a>Siguiente tarea de la lección  
 [Crear plantillas personalizadas](lesson-3-2-create-custom-templates.md)  
  
  