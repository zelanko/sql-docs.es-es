---
title: Propiedades del índice de texto completo (página programaciones) | Documentos de Microsoft
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- dbe-search
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- sql12.swb.fulltextsearch.fulltextindexproperties.schedule.f1
ms.assetid: a828e284-097e-4854-8c49-931934eb73bf
caps.latest.revision: 15
author: craigg-msft
ms.author: craigg
manager: jhubbard
ms.openlocfilehash: e564784e5f3fcae652068dcb200a805062a5e6bf
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36111845"
---
# <a name="full-text-index-properties-schedules-page"></a>Propiedades del índice de texto completo (página Programaciones)
  Utilice esta página con el fin de ver y crear calendarios para ejecutar un trabajo del Agente SQL Server que inicia un rellenado incremental de actualizaciones en la tabla base del índice de texto completo. Si la tabla base o vista no contiene una columna de la `timestamp` de tipo de datos, se realiza un rellenado completo.  
  
 **Para ver o cambiar las propiedades de un índice de texto completo**  
  
-   [Administrar índices de texto completo](../relational-databases/indexes/indexes.md)  
  
## <a name="uielement-list"></a>Lista de UIElement  
 **Programaciones**  
 Enumera cada rellenado incremental programado, si lo hay, en la tabla base para el índice de texto completo.  
  
 **Nombre**  
 Muestra el nombre de cada rellenado programado.  
  
 **Tipo de rellenado**  
 Muestra el tipo de cada rellenado programado.  
  
 **Enabled**  
 Indica si el rellenado programado está habilitado o deshabilitado actualmente.  
  
 **Descripción**  
 Muestra la descripción que se especificó cuando se creó la programación.  
  
 **Nueva**  
 Haga clic en esta opción si desea crear una programación nueva para rellenar el índice de texto completo.  
  
## <a name="see-also"></a>Vea también  
 [Use el Asistente para indización de texto completo](../relational-databases/search/use-the-full-text-indexing-wizard.md)   
 [Rellenar índices de texto completo](../relational-databases/search/populate-full-text-indexes.md)  
  
  