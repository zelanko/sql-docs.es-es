---
title: "Publicación de la ejecución de procedimientos almacenados en la publicación transaccional | Microsoft Docs"
ms.custom: 
ms.date: 03/07/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- replication
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- publishing [SQL Server replication], stored procedure execution
- stored procedures [SQL Server replication], publishing
ms.assetid: 1d3a3525-0bc5-466f-b097-5359dc74432d
caps.latest.revision: 16
author: BYHAM
ms.author: rickbyh
manager: jhubbard
translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: ebc41f2261de5a3fcb9ecc12ad990c273576c98c
ms.lasthandoff: 04/11/2017

---
# <a name="publish-execution-of-stored-procedure-in-transactional-publication"></a>Publicación de la ejecución de procedimientos almacenados en la publicación transaccional
  Especifique que la ejecución de un procedimiento almacenado (y no solo su definición) se debe publicar en el cuadro de diálogo **Propiedades del artículo: \<artículo>**. Este cuadro de diálogo está disponible en el Asistente para nueva publicación y en el cuadro de diálogo **Propiedades de la publicación: \<publicación>**. Para obtener más información sobre el uso del asistente y el acceso al cuadro de diálogo, vea [Crear una publicación](../../../relational-databases/replication/publish/create-a-publication.md) y [Ver y modificar propiedades de publicación](../../../relational-databases/replication/publish/view-and-modify-publication-properties.md).  
  
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
 [Publishing Stored Procedure Execution in Transactional Replication](../../../relational-databases/replication/transactional/publishing-stored-procedure-execution-in-transactional-replication.md)  
  
  
