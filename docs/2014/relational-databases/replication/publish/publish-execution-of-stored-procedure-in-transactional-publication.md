---
title: Publicar la ejecución de un procedimiento almacenado en una publicación transaccional (SQL Server Management Studio) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- publishing [SQL Server replication], stored procedure execution
- stored procedures [SQL Server replication], publishing
ms.assetid: 1d3a3525-0bc5-466f-b097-5359dc74432d
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: a226d7c58b3b72caf415d8e873b58ca38d3c749f
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/18/2020
ms.locfileid: "85060429"
---
# <a name="publish-the-execution-of-a-stored-procedure-in-a-transactional-publication-sql-server-management-studio"></a>Publicar la ejecución de un procedimiento almacenado en una publicación transaccional (SQL Server Management Studio)
  Especifique que la ejecución de un procedimiento almacenado (en lugar de solo su definición) se debe publicar en el cuadro de diálogo **propiedades del artículo: \<Article> ** . Este cuadro de diálogo está disponible en el Asistente para nueva publicación y en el cuadro **de diálogo Propiedades de la publicación \<Publication> :** . Para obtener más información sobre el uso del asistente y el acceso al cuadro de diálogo, consulte [Create a Publication](create-a-publication.md) (Crear una publicación) y [Ver y modificar propiedades de publicación](view-and-modify-publication-properties.md).  
  
 La definición del procedimiento (la instrucción CREATE PROCEDURE) se replica en el suscriptor cuando se inicializa la suscripción; cuando el procedimiento se ejecuta en el publicador, la replicación ejecuta el procedimiento correspondiente en el suscriptor.  
  
### <a name="to-publish-the-execution-of-a-stored-procedure"></a>Para publicar la ejecución de un procedimiento almacenado  
  
1.  En la página **artículos** del Asistente para nueva publicación o en el cuadro **de \<Publication> diálogo Propiedades de la publicación:** , seleccione un procedimiento almacenado.  
  
2.  Haga clic en **Propiedades del artículo**y, a continuación, haga clic en **Establecer propiedades del procedimiento almacenado resaltado**.  
  
3.  En el cuadro de diálogo **propiedades del artículo \<Article> :** , especifique uno de los siguientes valores para la opción **replicar** :  
  
    -   **Ejecución del procedimiento almacenado**  
  
    -   **La ejecución en una transacción serializada de SP**  
  
         Es la opción recomendada, ya que replica la ejecución del procedimiento solo si éste se ejecuta en el contexto de una transacción serializable. Si el procedimiento almacenado se ejecuta fuera de una transacción serializable, los cambios efectuados en los datos de las tablas publicadas se replican como una serie de instrucciones de lenguaje de manipulación de datos (DML).  
  
4.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
5.  Si está en el cuadro de diálogo **propiedades \<Publication> de la publicación:** , haga clic en **Aceptar** para guardar y cerrar el cuadro de diálogo.  
  
## <a name="see-also"></a>Consulte también  
 [Publicar la ejecución de un procedimiento almacenado en la replicación transaccional](../transactional/publishing-stored-procedure-execution-in-transactional-replication.md)  
  
  
