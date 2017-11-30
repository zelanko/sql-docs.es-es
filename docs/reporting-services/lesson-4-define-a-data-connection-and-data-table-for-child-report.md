---
title: "Lección 4: Definir una conexión de datos y una tabla de datos para el informe secundario | Microsoft Docs"
ms.custom: 
ms.date: 05/18/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
applies_to: SQL Server 2016
ms.assetid: a6aa2c56-227c-43c5-a28e-c7104131ac5e
caps.latest.revision: "7"
author: guyinacube
ms.author: asaxton
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 0c717fecbc14933bdfaac30e64faa2b8a9ff2940
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 11/09/2017
---
# <a name="lesson-4-define-a-data-connection-and-data-table-for-child-report"></a>Lección 4: Definir una conexión de datos y una tabla de datos para el informe secundario
Después de diseñar el informe primario, el paso siguiente es crear una conexión de datos y una tabla de datos para el informe secundario. En este tutorial, la conexión de datos se produce con la base de datos AdventureWorks2014.  
  
### <a name="to-define-a-data-connection-and-datatable-by-adding-a-dataset-for-child-report"></a>Para definir una conexión de datos y una DataTable agregando un DataSet (para el informe secundario)  
  
1.  En el menú **Sitio web** , seleccione **Agregar nuevo elemento**.  
  
2.  En el cuadro de diálogo **Agregar nuevo elemento** , seleccione **DataSet** y, después, haga clic en **Agregar**. Cuando se le pida, debe agregar el elemento a la carpeta **App_Code** ; para ello, haga clic en **Sí**.  
  
    De este modo, agrega un nuevo archivo XSD **DataSet2.xsd** al proyecto y abre el Diseñador de DataSet.  
  
3.  En la ventana del Cuadro de herramientas, arrastre un control **TableAdapter** hasta la superficie de diseño. De este modo, se inicia el Asistente para configuración de **TableAdapter** .  
  
4.  En la página **Elegir la conexión de datos** , puede seleccionar la conexión que ha creado en la lección 2. Si lo hace, seleccione **Siguiente** y vaya al paso 8. En caso contrario, seleccione **Nueva conexión**.  
  
5.  En el cuadro de diálogo **Agregar conexión** , realice los pasos siguientes:  
  
    1.  En el cuadro **Nombre del servidor** , escriba el servidor donde se encuentra la base de datos **AdventureWorks2014** .  
  
        La instancia de SQL Server Express predeterminada es **(local)\sqlexpress**.  
  
    2.  En la sección **Iniciar sesión en el servidor** , seleccione la opción que proporciona acceso a los datos. **Usar autenticación de Windows** es el valor predeterminado.  
  
    3.  En la lista desplegable **Seleccione o escriba un nombre de base de datos** , haga clic en **AdventureWorks2014**.  
  
    4.  Seleccione **Aceptar**y luego seleccione **Siguiente**.  
  
6.  Si ha seleccionado **Usar autenticación de SQL Server** en el paso 5 (b), seleccione la opción si quiere incluir la información confidencial en la cadena o establecer la información en su código de aplicación.  
  
7.  En la página **Guardar la cadena de conexión en el archivo de configuración de la aplicación** , escriba el nombre de la cadena de conexión o acepte el predeterminado **AdventureWorks2014ConnectionString**. Seleccione **Siguiente**.  
  
8.  En la página **Elegir un tipo de comando** , seleccione **Usar instrucciones SQL**y, después, haga clic en **Siguiente**.  
  
9. En la página **Escriba una instrucción SQL** , escriba la siguiente consulta de Transact-SQL para recuperar los datos de la base de datos **AdventureWorks2014** y seleccione **Siguiente**.  
  
    ```  
    SELECT PurchaseOrderID, PurchaseOrderDetailID, OrderQty, ProductID, ReceivedQty, RejectedQty, StockedQty FROM Purchasing.PurchaseOrderDetail  
    ```  
  
    También puede crear la consulta si hace clic en **Generador de consultas**y, después, comprobar la consulta al hacer clic en **Ejecutar consulta** . Si la consulta no devuelve los datos esperados, puede utilizar una versión anterior de AdventureWorks. Para más información sobre cómo obtener la base de datos de ejemplo **AdventureWorks2014**, vea [Bases de datos de ejemplo AdventureWorks](https://github.com/Microsoft/sql-server-samples/releases).  
  
10. En la página **Elegir los métodos que se van a generar** , desactive **Crear métodos para enviar actualizaciones directamente a la base de datos (GenerateDBDirectMethods)**y seleccione **Finalizar**.  
  
    > [!WARNING]  
    > Asegúrese de desactivar **Crear métodos para enviar actualizaciones directamente a la base de datos (GenerateDBDirectMethods)**  
  
    Ahora ha completado la configuración del objeto [DataTable](http://msdn.microsoft.com/library/system.data.datatable.aspx) de ADO.NET como origen de datos para el informe. En la página del Diseñador de Dataset en Visual Studio, debería ver el objeto **DataTable** que ha agregado, con las columnas especificadas en la consulta. DataSet2 contiene los datos de la tabla PurhcaseOrderDetail, según la consulta.  
  
11. Guarde el archivo.  
  
12. Para obtener una vista previa de los datos, seleccione **Vista previa de los datos** en el menú **Datos** y seleccione **Vista previa**.  
  
## <a name="next-task"></a>Tarea siguiente  
Ha creado correctamente una conexión de datos y una tabla de datos para el informe secundario. Después, diseñará el informe secundario usando el Asistente para informes. Consulte [Lección 5: Diseñar el informe secundario usando el Asistente para informes](../reporting-services/lesson-5-design-the-child-report-using-the-report-wizard.md).  
  

