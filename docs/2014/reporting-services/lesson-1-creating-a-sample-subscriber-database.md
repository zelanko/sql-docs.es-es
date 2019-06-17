---
title: 'Lección 1: Creación de una base de datos de suscriptor de ejemplo | Microsoft Docs'
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
ms.assetid: 47a882b7-efe5-4ee6-bef4-06118eb56903
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 9e68650b21ee8cddc6258ab64b874bcf51ec1a83
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "66108537"
---
# <a name="lesson-1-creating-a-sample-subscriber-database"></a>Lección 1: Creación de una base de datos de suscriptor de ejemplo
  Antes de que pueda definir una suscripción controlada por datos, debe disponer de un origen de datos que proporcione datos de suscripción. En este paso, creará una pequeña base de datos para almacenar los datos de suscripción utilizados en este tutorial. Más adelante, cuando la suscripción se haya procesado, el servidor de informes recupera estos datos y los utiliza para personalizar los resultados del informe, las opciones de entrega y el formato de presentación del informe.  
  
 En esta lección se da por supuesto que usa [!INCLUDE[ssManStudio](../includes/ssmanstudio-md.md)] para crear un [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] base de datos.  
  
### <a name="to-create-a-sample-subscriber-database"></a>Para crear una base de datos de suscriptor de ejemplo  
  
1.  Inicie [!INCLUDE[ssManStudio](../includes/ssmanstudio-md.md)] y abra una conexión a un [!INCLUDE[ssDE](../includes/ssde-md.md)].  
  
2.  Haga clic con el botón derecho en Bases de datos y seleccione **Nueva base de datos...** .  
  
3.  En el cuadro de diálogo nueva base de datos, nombre de la base de datos, escriba *suscriptores*. [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
4.  Haga clic en el botón **Nueva consulta** de la barra de herramientas.  
  
5.  Copie las siguientes instrucciones [!INCLUDE[tsql](../includes/tsql-md.md)] en la consulta vacía:  
  
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
  
6.  Haga clic en **! Ejecutar** en la barra de herramientas.  
  
7.  Use una instrucción SELECT para comprobar que tiene tres filas de datos. Por ejemplo: `select * from OrderInfo`  
  
## <a name="next-steps"></a>Pasos siguientes  
 Ha creado correctamente los datos de suscripción que controlarán la distribución de informes y cambiarán los resultados del informe para cada suscriptor. A continuación, modificará las propiedades del origen de datos del informe que distribuirá a los suscriptores. Las propiedades del origen de datos se modifican con el fin de preparar el informe para la entrega de la suscripción controlada por datos. Además, modificará el diseño de informe para que incluya un parámetro usará la suscripción con los datos del suscriptor. [Lección 2: Propiedades del origen de modificación de los datos del informe](lesson-2-modifying-the-report-data-source-properties.md).  
  
## <a name="see-also"></a>Vea también  
 [Crear una suscripción controlada por datos &#40;Tutorial de SSRS&#41;](create-a-data-driven-subscription-ssrs-tutorial.md)   
 [Crear una base de datos](../relational-databases/databases/create-a-database.md)   
 [Crear un informe de tabla básico &#40;Tutorial de SSRS&#41;](create-a-basic-table-report-ssrs-tutorial.md)  
  
  
