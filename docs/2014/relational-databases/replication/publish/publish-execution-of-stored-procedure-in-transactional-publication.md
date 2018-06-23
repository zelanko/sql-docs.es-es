---
title: Publicar la ejecución de un procedimiento almacenado en una publicación transaccional (SQL Server Management Studio) | Documentos de Microsoft
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- replication
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- publishing [SQL Server replication], stored procedure execution
- stored procedures [SQL Server replication], publishing
ms.assetid: 1d3a3525-0bc5-466f-b097-5359dc74432d
caps.latest.revision: 14
author: craigg-msft
ms.author: craigg
manager: jhubbard
ms.openlocfilehash: cd233ba5be8c6ea5bc09381088848f96ac86a907
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36111541"
---
# <a name="publish-the-execution-of-a-stored-procedure-in-a-transactional-publication-sql-server-management-studio"></a>Publicar la ejecución de un procedimiento almacenado en una publicación transaccional (SQL Server Management Studio)
  Especifique que la ejecución de un procedimiento almacenado (y no solo su definición) se debe publicar en el cuadro de diálogo **Propiedades del artículo: \<artículo>**. Este cuadro de diálogo está disponible en el Asistente para nueva publicación y en el cuadro de diálogo **Propiedades de la publicación: \<publicación>**. Para obtener más información sobre el uso del asistente y el acceso al cuadro de diálogo, vea [Crear una publicación](create-a-publication.md) y [Ver y modificar propiedades de publicación](view-and-modify-publication-properties.md).  
  
 La definición del procedimiento (la instrucción CREATE PROCEDURE) se replica en el suscriptor cuando se inicializa la suscripción; cuando el procedimiento se ejecuta en el publicador, la replicación ejecuta el procedimiento correspondiente en el suscriptor.  
  
### <a name="to-publish-the-execution-of-a-stored-procedure"></a>Para publicar la ejecución de un procedimiento almacenado  
  
1.  En la página **Artículos** del Asistente para nueva publicación o en el cuadro de diálogo **Propiedades de la publicación: \<publicación>**, seleccione un procedimiento almacenado.  
  
2.  Haga clic en **Propiedades del artículo**y, a continuación, haga clic en **Establecer propiedades del procedimiento almacenado resaltado**.  
  
3.  En el cuadro de diálogo **Propiedades del artículo: \<artículo>**, especifique uno de los siguientes valores para la opción **Replicar**:  
  
    -   **Ejecución del procedimiento almacenado**  
  
    -   **Ejecución en una transacción serializada de SP**  
  
         Es la opción recomendada, ya que replica la ejecución del procedimiento solo si éste se ejecuta en el contexto de una transacción serializable. Si el procedimiento almacenado se ejecuta fuera de una transacción serializable, los cambios efectuados en los datos de las tablas publicadas se replican como una serie de instrucciones de lenguaje de manipulación de datos (DML).  
  
4.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
5.  Si se encuentra en el cuadro de diálogo **Propiedades de la publicación: \<publicación>**, haga clic en **Aceptar** para guardar y cerrar el cuadro de diálogo.  
  
## <a name="see-also"></a>Vea también  
 [Publicar la ejecución de procedimientos almacenados en la replicación transaccional](../transactional/publishing-stored-procedure-execution-in-transactional-replication.md)  
  
  