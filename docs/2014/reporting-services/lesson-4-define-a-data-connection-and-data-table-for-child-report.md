---
title: 'Lección 4: Definir una conexión de datos y una tabla de datos para el informe secundario | Microsoft Docs'
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- reporting-services-native
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: a6aa2c56-227c-43c5-a28e-c7104131ac5e
caps.latest.revision: 7
author: douglaslM
ms.author: douglasl
manager: mblythe
ms.openlocfilehash: 16fbcf4bc8182a1b8f1f66be5319357f9b498034
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36110891"
---
# <a name="lesson-4-define-a-data-connection-and-data-table-for-child-report"></a>Lección 4: Definir una conexión de datos y una tabla de datos para el informe secundario
  Después de diseñar el informe primario, el paso siguiente es crear una conexión de datos y una tabla de datos para el informe secundario. En este tutorial, la conexión de datos se produce con la base de datos AdventureWorks2008. También tiene la opción de conectar con la base de datos AdventureWorks2012.  
  
### <a name="to-define-a-data-connection-and-datatable-by-adding-a-dataset-for-child-report"></a>Para definir una conexión de datos y una DataTable agregando un DataSet (para el informe secundario)  
  
1.  En el **sitio Web** menú, haga clic en **Agregar nuevo elemento**.  
  
2.  En el **Agregar nuevo elemento** cuadro de diálogo, haga clic en **conjunto de datos** y, a continuación, haga clic en **agregar**. Cuando se le pida, debe agregar el elemento a la **App_Code** carpeta haciendo clic en **Sí**.  
  
     De este modo, agrega un nuevo archivo XSD **DataSet2.xsd** al proyecto y abre el Diseñador de DataSet.  
  
3.  En la ventana del Cuadro de herramientas, arrastre un control **TableAdapter** hasta la superficie de diseño. De este modo, se inicia el Asistente para configuración de **TableAdapter** .  
  
4.  En el **elegir la conexión de datos** página, haga clic en **nueva conexión**.  
  
5.  En el cuadro de diálogo **Agregar conexión** , realice los pasos siguientes:  
  
    1.  En el **nombre del servidor** cuadro, escriba el servidor donde la **AdventureWorks2008** se encuentra la base de datos.  
  
         La instancia de SQL Server Express predeterminada es **(local)\sqlexpress**.  
  
    2.  En la sección **Iniciar sesión en el servidor** , seleccione la opción que proporciona acceso a los datos. **Usar autenticación de Windows** es el valor predeterminado.  
  
    3.  Desde el **seleccione o escriba un nombre de base de datos** la lista desplegable, haga clic en **AdventureWorks2008**.  
  
    4.  Haga clic en **Aceptar**y, a continuación, en **Siguiente**.  
  
6.  Si ha seleccionado **Usar autenticación de SQL Server** en el paso 5 (b), seleccione la opción si quiere incluir la información confidencial en la cadena o establecer la información en su código de aplicación.  
  
7.  En el **Guardar cadena de conexión en el archivo de configuración de aplicación** página, escriba el nombre de la cadena de conexión o acepte el valor predeterminado **AdventureWorks2008ConnectionString**. Haga clic en **Siguiente**.  
  
8.  En el **elegir un tipo de comando** página, seleccione **usar instrucciones SQL**y, a continuación, haga clic en **siguiente**.  
  
9. En el **escriba una instrucción SQL** página, escriba la siguiente consulta de Transact-SQL para recuperar los datos de la **AdventureWorks2008** la base de datos y, a continuación, haga clic en **siguiente**.  
  
    ```  
    SELECT PurchaseOrderID, PurchaseOrderDetailID, OrderQty, ProductID, ReceivedQty, RejectedQty, StockedQty FROM Purchasing.PurchaseOrderDetail  
    ```  
  
     También puede crear la consulta haciendo clic en **generador de consultas**y, a continuación, compruebe la consulta haciendo clic en **Ejecutar consulta** botón. Si la consulta no devuelve los datos esperados, puede utilizar una versión anterior de AdventureWorks. Para obtener más información acerca de cómo instalar la **AdventureWorks2008** versión de AdventureWorks, vea [Tutorial: instalar la base de datos de AdventureWorks](http://msdn.microsoft.com/library/aa992075\(v=vs.100\).aspx).  
  
10. En el **elija los métodos para generar** página, desactive la opción **crear métodos para enviar actualizaciones directamente a la base de datos (GenerateDBDirectMethods)** y, a continuación, haga clic en **finalizar**.  
  
     Ahora ha completado la configuración ADO.NET [DataTable](http://msdn.microsoft.com/library/system.data.datatable\(v=vs.100\).aspx) como origen de datos para el informe. En la página del Diseñador de Dataset en Visual Studio, debería ver el objeto **DataTable** que ha agregado, con las columnas especificadas en la consulta. DataSet2 contiene los datos de la tabla PurhcaseOrderDetail, según la consulta.  
  
11. Guarde el archivo.  
  
12. Para obtener una vista previa de los datos, haga clic en **vista previa de datos** en el **datos** menú y, a continuación, haga clic en **vista previa**.  
  
## <a name="next-task"></a>Tarea siguiente  
 Ha creado correctamente una conexión de datos y una tabla de datos para el informe secundario. Después, diseñará el informe secundario usando el Asistente para informes.  
  
  