---
title: Suscripción a la directiva Finance Name y comprobación | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
ms.assetid: 126b4c4c-2a1c-4701-a0ad-8de23fbd7306
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 3bbf6c9640882ffca2bbdbf82b2ef2667c394096
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "66090701"
---
# <a name="subscribe-to-and-check-the-finance-name-policy"></a>Suscribirse a, y comprobar, la directiva Finance Name
  En esta tarea, configurará la base de datos Finance para suscribirse a la categoría de directivas Finance. A continuación, probará la directiva Finance Name.  
  
### <a name="to-subscribe-to-the-finance-policy-category"></a>Para suscribirse a la categoría de directivas Finance  
  
1.  En Explorador de objetos, expanda **bases de datos**, haga clic `Finance`con el botón secundario, seleccione **directivas**y, a continuación, haga clic en **categorías**.  
  
2.  Active la casilla **suscrito** para la `Finance` categoría.  
  
3.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
### <a name="to-test-the-enforcement-of-the-finance-name-policy"></a>Para probar la aplicación de la directiva Finance Name  
  
1.  En [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)], abra una ventana de consulta. Ejecute las instrucciones siguientes que intentan crear una tabla que infringe la directiva **Finance Name** . La tabla infringe la directiva porque el nombre de tabla no comienza con las letras **fintbl**.  
  
    ```  
    USE Finance ;  
    GO  
    CREATE TABLE NewTable  
    (Col1 int) ;  
    GO  
  
    ```  
  
     Observe que la directiva evita que se cree la tabla y devuelve un mensaje informativo que proporciona el nombre de la directiva.  
  
2.  Para proporcionar un nombre válido, modifique el código como sigue y ejecute la instrucción de nuevo.  
  
    ```  
    USE Finance ;  
    GO  
    CREATE TABLE fintblNewTable  
    (Col1 int) ;  
    GO  
  
    ```  
  
     Esta vez, la tabla se crea.  
  
### <a name="to-apply-the-policy-to-the-whole-server"></a>Para aplicar la directiva al servidor entero  
  
1.  Actualmente, solo la base de datos Finance se suscribe a la categoría de directiva Finance. En muchos casos, es más fácil aplicar la categoría de directiva a todo el servidor. En el Explorador de objetos, expanda **Administración**, haga clic con el botón derecho en **Administración de directivas**y, después, haga clic en **Administrar categorías**.  
  
2.  En el cuadro de diálogo **Administrar categorías de directiva** , busque la categoría Finance y seleccione la casilla **Suscripciones de base de datos de mandatos** para la categoría Finance.  
  
3.  
  [!INCLUDE[clickOK](../../includes/clickok-md.md)] Ahora la categoría Finance se aplica a todas las bases de datos, pero la condición que ha creado restringe la directiva Finance Name a la base de datos Finance. De esta forma, se muestra cómo se pueden utilizar combinaciones complejas de condiciones para destinar las directivas de modo que se apliquen correctamente en muchos servidores.  
  
## <a name="summary"></a>Resumen  
 En este tutorial se ha demostrado cómo crear condiciones de la administración basada en directivas, directivas y grupos de directivas, y cómo aplicar los filtros y comprobar la compatibilidad de los destinos de la administración basada en directivas.  
  
## <a name="next"></a>Pasos siguientes  
 Este tutorial ha finalizado. Para volver al inicio, haga clic en [Tutorial: Administrar servidores mediante administración basada en directivas](tutorial-administering-servers-by-using-policy-based-management.md).  
  
 Para obtener una lista de tutoriales, consulte los [tutoriales de SQL Server 2014](../../tutorials/tutorials-for-sql-server-2014.md).  
  
## <a name="see-also"></a>Consulte también  
 [Administrar servidores mediante administración basada en directivas](administer-servers-by-using-policy-based-management.md)  
  
  
