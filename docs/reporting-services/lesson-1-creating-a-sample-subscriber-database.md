---
title: "Lecci&#243;n 1: Crear una base de datos de suscriptor de ejemplo | Microsoft Docs"
ms.custom: ""
ms.date: "05/26/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "reporting-services-native"
ms.tgt_pltfrm: ""
ms.topic: "article"
applies_to: 
  - "SQL Server 2016"
ms.assetid: 47a882b7-efe5-4ee6-bef4-06118eb56903
caps.latest.revision: 45
author: "guyinacube"
ms.author: "asaxton"
manager: "erikre"
caps.handback.revision: 45
---
# Lecci&#243;n 1: Crear una base de datos de suscriptor de ejemplo
En esta lección del tutorial de [!INCLUDE[ssRSnoversion_md](../includes/ssrsnoversion-md.md)], creará una pequeña base de datos "suscriptor" para almacenar los datos de suscripción que usados por una suscripción controlada por datos. Cuando la suscripción se haya procesado, el servidor de informes recupera estos datos y los usa para personalizar los resultados del informe. Por ejemplo, las filas de datos incluyen números de pedido específicos para usar como filtros y qué formato de archivo tendrán los informes generados cuando se creen.  
  
En esta lección se supone que está usando [!INCLUDE[ssManStudioFull_md](../includes/ssmanstudiofull-md.md)] para crear una base de datos de [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)].  
  
### Para crear una base de datos de suscriptor de ejemplo  
  
1.  Inicie [!INCLUDE[ssManStudio](../includes/ssmanstudio-md.md)] y abra una conexión a una instancia del [!INCLUDE[ssDEnoversion_md](../includes/ssdenoversion-md.md)].  
  
2.  Haga clic con el botón derecho en Bases de datos y seleccione **Nueva base de datos...**.  
  
3.  En el cuadro de diálogo Nueva base de datos, en **Nombre de la base de datos**, escriba *Subscribers*. 
4. [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
5.  Haga clic en el botón **Nueva consulta** de la barra de herramientas.  
  
6.  Copie las siguientes instrucciones [!INCLUDE[tsql](../includes/tsql-md.md)] en la consulta vacía:  
  
    ```  
    Use Subscribers  
    CREATE TABLE [dbo].[OrderInfo] (  
        [SubscriptionID] [int] NOT NULL PRIMARY KEY ,  
        [Order] [nvarchar] (20) NOT NULL,  
        [FileType] [bit],  
        [Format] [nvarchar] (20) NOT NULL ,  
    ) ON [PRIMARY]  
    GO  
  
    INSERT INTO [dbo].[OrderInfo] (SubscriptionID, [Order], FileType, Format)   
    VALUES ('1', 'so43659', '1', 'IMAGE')  
    INSERT INTO [dbo].[OrderInfo] (SubscriptionID, [Order], FileType, Format)   
    VALUES ('2', 'so43664', '1', 'MHTML')  
    INSERT INTO [dbo].[OrderInfo] (SubscriptionID, [Order], FileType, Format)   
    VALUES ('3', 'so43668', '1', 'PDF')  
    INSERT INTO [dbo].[OrderInfo] (SubscriptionID, [Order], FileType, Format)   
    VALUES ('4', 'so71949', '1', 'Excel')  
    GO  
    ```  
  
7.  Haga clic en **! en Ejecutar** en la barra de herramientas.  
  
8.  Use una instrucción SELECT para comprobar que tiene tres filas de datos. Por ejemplo: `select * from OrderInfo`  
  
## Pasos siguientes  
+ Ha creado correctamente los datos de suscripción que controlarán la distribución de informes y cambiarán los resultados del informe para cada suscriptor. 
+ Después, modificará las propiedades del origen de datos del informe para usar las credenciales almacenadas. 
+ Además, modificará el diseño de informe para que incluya un parámetro usará la suscripción con los datos del suscriptor. [Lección 2: Modificar las propiedades del origen de datos de informe](../reporting-services/lesson-2-modifying-the-report-data-source-properties.md).  
  
## Vea también  
[Crear una suscripción controlada por datos &#40;Tutorial de SSRS&#41;](../reporting-services/create-a-data-driven-subscription-ssrs-tutorial.md)  
[Crear una base de datos](../relational-databases/databases/create-a-database.md)  
[Crear un informe de tabla básico &#40;Tutorial de SSRS&#41;](../reporting-services/create-a-basic-table-report-ssrs-tutorial.md)  
  
  
  
