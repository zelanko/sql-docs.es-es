---
title: "Suscribirse a, y comprobar, la directiva Finance Name | Microsoft Docs"
ms.custom: ""
ms.date: "02/27/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dbe-query-tuning"
ms.tgt_pltfrm: ""
ms.topic: "article"
applies_to: 
  - "SQL Server 2016"
ms.assetid: 126b4c4c-2a1c-4701-a0ad-8de23fbd7306
caps.latest.revision: 24
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
---
# Suscribirse a, y comprobar, la directiva Finance Name
En esta tarea, configurará la base de datos Finance para suscribirse a la categoría de directivas Finance. A continuación, probará la directiva Finance Name.  
  
### Para suscribirse a la categoría de directivas Finance  
  
1.  En el Explorador de objetos, expanda **Bases de datos**, haga clic con el botón derecho en **Finance**, elija **Directivas** y, después, haga clic en **Categorías**.  
  
2.  Seleccione la casilla **Suscrito** para la categoría **Finance**.  
  
3.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
### Para probar la aplicación de la directiva Finance Name  
  
1.  En [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)], abra una ventana de consulta. Ejecute las instrucciones siguientes que intentan crear una tabla que infringe la directiva **Finance Name**. La tabla infringe la directiva porque el nombre de tabla no comienza con las letras **fintbl**.  
  
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
  
### Para aplicar la directiva al servidor entero  
  
1.  Actualmente, solo la base de datos Finance se suscribe a la categoría de directiva Finance. En muchos casos, es más fácil aplicar la categoría de directiva a todo el servidor. En el Explorador de objetos, expanda **Administración**, haga clic con el botón derecho en **Administración de directivas** y, después, haga clic en **Administrar categorías**.  
  
2.  En el cuadro de diálogo **Administrar categorías de directiva**, busque la categoría Finance y seleccione la casilla **Suscripciones de base de datos de mandatos** para la categoría Finance.  
  
3.  [!INCLUDE[clickOK](../../includes/clickok-md.md)] Ahora la categoría Finance se aplica a todas las bases de datos, pero la condición que ha creado restringe la directiva Finance Name a la base de datos Finance. De esta forma, se muestra cómo se pueden utilizar combinaciones complejas de condiciones para destinar las directivas de modo que se apliquen correctamente en muchos servidores.  
  
## Resumen  
En este tutorial se ha demostrado cómo crear condiciones de la administración basada en directivas, directivas y grupos de directivas, y cómo aplicar los filtros y comprobar la compatibilidad de los destinos de la administración basada en directivas.  
  
## Siguiente  
Este tutorial ha finalizado. Para volver al inicio, haga clic en [Tutorial: Administrar servidores mediante administración basada en directivas](../../relational-databases/policy-based-management/tutorial-administering-servers-by-using-policy-based-management.md).  
  
Para obtener una lista de tutoriales, vea [Tutoriales para SQL Server 2016](../../sql-server/tutorials-for-sql-server-2016.md).  
  
## Vea también  
[Administrar servidores mediante administración basada en directivas](../../relational-databases/policy-based-management/administer-servers-by-using-policy-based-management.md)  
  
  
  
