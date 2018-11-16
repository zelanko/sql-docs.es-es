---
title: 'Lección 2: Creación y aplicación de una directiva de normas de denominación | Microsoft Docs'
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
ms.assetid: 87e51f4e-156c-4def-8572-76a15075d75e
author: VanMSFT
ms.author: vanto
manager: craigg
ms.openlocfilehash: fb7082aec21e75c2852ac7efdc2d7a4fa565768d
ms.sourcegitcommit: ef6e3ec273b0521e7c79d5c2a4cb4dcba1744e67
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 11/10/2018
ms.locfileid: "51512830"
---
# <a name="lesson-2-create-and-apply-a-naming-standards-policy"></a>Lección 2: Crear y aplicar una directiva de normas de denominación
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
Algunos tipos de directivas de administración basada en directivas pueden crear desencadenadores para exigir el cumplimiento futuro con la directiva. En esta lección, va a crear una directiva que exige una denominación estándar para tablas. A continuación, va a probar la directiva intentando crear una tabla que infrinja dicha directiva.  


## <a name="prerequisites"></a>Prerequisites
Para llevar a cabo este tutorial necesita tener SQL Server Management Studio y acceso a un servidor que ejecute SQL Server.

- Instale [SQL Server Management Studio](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms).
- Instale [SQL Server 2017 Developer Edition](https://www.microsoft.com/sql-server/sql-server-downloads).
  
## <a name="create-the-finance-database"></a>Creación de la base de datos Finance  
  
1.  En [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)], abra una ventana de consulta y ejecute la instrucción siguiente:  
  
    ```sql  
    CREATE DATABASE Finance ;  
    GO  
    ```  
  
2.  En el Explorador de objetos, haga clic en **Bases de datos**y, a continuación, presione F5 para actualizar la lista de bases de datos.  


## <a name="create-the-finance-tables-condition"></a>Creación de la condición Finance Tables 

1.  En el Explorador de objetos, expanda **Administración**, expanda **Administración de directivas**, haga clic con el botón derecho en **Condiciones**y, después, haga clic en **Nueva condición**. 

   ![Nueva condición](Media/lesson-2-create-and-apply-a-naming-standards-policy/new-condition.png)
  
2.  En el cuadro de diálogo **Crear nueva condición** , en el cuadro **Nombre** , escriba **Finance Tables**.  
    1. En la lista **Faceta** , seleccione **Nombre de varias partes**. 
    1. En el cuadro de diálogo **Expresión**, en el cuadro **Campo**, seleccione **@Name**; en el cuadro **Operador**, seleccione **Like**; y en el cuadro **Valor**, escriba ```'fintbl%'``` para hacer que todos los nombres de tabla comiencen con las letras **fintbl**.
    1. En la página **Descripción** , escriba **Los nombres de tablas de finanzas deben comenzar con fintbl**y, a continuación, haga clic en **Aceptar** para crear la condición.  

    ![Condición Finance Tables](Media/lesson-2-create-and-apply-a-naming-standards-policy/finance-tables-condition.png)
 
## <a name="create-the-finance-name-policy"></a>Creación de la directiva Finance Name  
  
1.  En el Explorador de objetos, haga clic con el botón derecho en **Directivas**y, después, haga clic en **Nueva directiva**.  

   ![Nueva directiva](Media/lesson-2-create-and-apply-a-naming-standards-policy/new-policy.png)
  
2.  En el cuadro de diálogo **Crear nueva directiva** , en el cuadro **Nombre** , escriba **Finance Name**.
    1. En la lista **Condición de comprobación** , seleccione **Finance Tables**. Está en el área **Nombre de varias partes** . 
    1. En el área **Contra** verá una lista de los objetos de base de datos que podrían aplicar esta directiva. Active la casilla de **Cada tabla**.
    1. Seleccione la lista **Habilitado** . (El cuadro **Habilitado** no se aplica a las directivas **A petición** ).
    1. En la lista **Modo de evaluación** , seleccione **Al cambiar: impedir**. Esto exigirá la directiva creando un desencadenador de base de datos en la base de datos Finance. 
    1. En la lista **Restricción de servidor** , seleccione **Ninguna**. 
    1. En la página **Descripción**, agregue la descripción "Los nombres de tabla de la base de datos Finance deben contener 'fintbl%'". 
    1. Vuelva a la página **General** y, en el área **Cada base de datos**, expanda **Cada** y, a continuación, haga clic en **Nueva condición**.

    ![Creación de la directiva Finance Name](Media/lesson-2-create-and-apply-a-naming-standards-policy/create-new-policy-finance-name.png)
  
6.  En el cuadro de diálogo **Crear nueva condición** , en el cuadro **Nombre** , escriba **Finance Database**.
    1. En el cuadro **Expresión**, complete la expresión para incluir @Name = "Finance" y, después, haga clic en **Aceptar** para cerrar la página de la condición. 
  
    ![Creación de la nueva condición "finance database"](Media/lesson-2-create-and-apply-a-naming-standards-policy/create-new-condition.png)

    > [!NOTE]  
    > Es posible que tenga que salir del cuadro **Valor** para habilitar el botón **Aceptar** .  
  
11. [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
## <a name="create-the-finance-policy-category"></a>Creación de la categoría de directivas Finance  
  
1.  En el Explorador de objetos, expanda **Administración**, haga clic con el botón derecho en **Administración de directivas**y, después, haga clic en **Administrar categorías**.  

   ![Administración de categorías](Media/lesson-2-create-and-apply-a-naming-standards-policy/manage-categories.png)
  
2.  En el cuadro de diálogo **Administrar categorías de directivas** , en **Nombre**, escriba **Finance** en el cuadro en blanco y, a continuación, anule la selección de **Suscripciones de base de datos de mandatos**. **Suscripciones de base de datos de mandatos** exigirá que cada base de datos en la instancia se suscriba a las directivas que pertenecen a esta categoría de directiva. Para esta lección, solo la base de datos Finance debería suscribirse a la directiva Finance Name.  

    ![Administración de categorías de directiva](Media/lesson-2-create-and-apply-a-naming-standards-policy/manage-policy-categories.png)
  
3.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  

## <a name="subscribe-to-the-finance-policy-category"></a>Suscripción a la categoría de directivas Finance  
  
1.  En el Explorador de objetos, expanda **Bases de datos**, haga clic con el botón derecho en **Finance**, elija **Directivas**y, después, haga clic en **Categorías**. 

   ![Categorías de directivas Finance](Media/lesson-2-create-and-apply-a-naming-standards-policy/finance-categories.png)
  
2.  Seleccione la casilla **Suscrito** para la categoría **Finance** .  

   ![Suscrito a la directiva Finance](Media/lesson-2-create-and-apply-a-naming-standards-policy/subscribe-to-finance.png)
  
3.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
## <a name="test-the-enforcement-of-the-finance-name-policy"></a>Prueba del cumplimiento de la directiva Finance Name  
  
1.  En [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)], abra una ventana de consulta. Ejecute las instrucciones siguientes que intentan crear una tabla que infringe la directiva **Finance Name** . La tabla infringe la directiva porque el nombre de tabla no comienza con las letras **fintbl**.  
  
    ```sql  
    USE Finance ;  
    GO  
    CREATE TABLE NewTable  
    (Col1 int) ;  
    GO    
    ```  
  
    Observe que la directiva evita que se cree la tabla y devuelve un mensaje informativo que proporciona el nombre de la directiva. 

   ```
     Policy 'Finance Name' has been violated by 'SQLSERVER:\SQL\SQL\SQL2017\Databases\Finance\Tables\dbo.NewTable'.
     This transaction will be rolled back.
     Policy condition: '@Name LIKE 'fintbl%''
     Policy description: 'Tables names in the Finance database must contain 'fintbl%''.
     Additional help: '' : ''
     Statement: 'CREATE TABLE NewTable  
         (Col1 int)'.
     Msg 515, Level 16, State 2, Procedure msdb.sys.sp_syspolicy_execute_policy, Line 69 [Batch Start Line 2]
     Cannot insert the value NULL into column 'target_query_expression', table 'msdb.dbo.syspolicy_policy_execution_history_details_internal'; column does not allow nulls. INSERT fails.
     The statement has been terminated.
   ``` 
  
2.  Para proporcionar un nombre válido, modifique el código como sigue y ejecute la instrucción de nuevo.  
  
    ```sql  
    USE Finance ;  
    GO  
    CREATE TABLE fintblNewTable  
    (Col1 int) ;  
    GO    
    ```  
  
    Esta vez, la tabla se crea.  
  
## <a name="apply-the-policy-to-the-whole-server"></a>Aplicación de la directiva al servidor entero  
  
1.  Actualmente, solo la base de datos Finance se suscribe a la categoría de directiva Finance. En muchos casos, es más fácil aplicar la categoría de directiva a todo el servidor. En el Explorador de objetos, expanda **Administración**, haga clic con el botón derecho en **Administración de directivas**y, después, haga clic en **Administrar categorías**.  
  
2.  En el cuadro de diálogo **Administrar categorías de directiva** , busque la categoría Finance y seleccione la casilla **Suscripciones de base de datos de mandatos** para la categoría Finance.  
  
3.  [!INCLUDE[clickOK](../../includes/clickok-md.md)] Ahora la categoría Finance se aplica a todas las bases de datos, pero la condición que ha creado restringe la directiva Finance Name a la base de datos Finance. De esta forma, se muestra cómo se pueden utilizar combinaciones complejas de condiciones para destinar las directivas de modo que se apliquen correctamente en muchos servidores.  
  
## <a name="summary"></a>Resumen  
En este tutorial se ha demostrado cómo crear condiciones de la administración basada en directivas, directivas y grupos de directivas, y cómo aplicar los filtros y comprobar la compatibilidad de los destinos de la administración basada en directivas.  
  
## <a name="next"></a>Siguiente  
Este tutorial ha finalizado. Para volver al inicio, visite [Tutorial: Administrar servidores mediante administración basada en directivas](../../relational-databases/policy-based-management/tutorial-administering-servers-by-using-policy-based-management.md).  
  
Para obtener una lista de tutoriales, vea [Tutoriales para SQL Server 2016](../../sql-server/tutorials-for-sql-server-2016.md).  
  
## <a name="see-also"></a>Ver también  
[Administrar servidores mediante administración basada en directivas](../../relational-databases/policy-based-management/administer-servers-by-using-policy-based-management.md)  
