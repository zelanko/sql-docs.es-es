---
title: 'Lección 2: Definir una conexión de datos y una tabla de datos para el informe primario | Microsoft Docs'
ms.date: 05/18/2016
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: reporting-services
ms.suite: pro-bi
ms.topic: conceptual
applies_to:
- SQL Server 2016
ms.assetid: f02dee0c-85ad-45d4-b707-10e9e8541db9
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 83f42082a264a9f2e06c93c915afe6ba2d287f48
ms.sourcegitcommit: d96b94c60d88340224371926f283200496a5ca64
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/30/2018
ms.locfileid: "43272245"
---
# <a name="lesson-2-define-a-data-connection-and-data-table-for-parent-report"></a>Lección 2: Definir una conexión de datos y una tabla de datos para el informe primario
Después de crear un proyecto de sitio Web nuevo con la plantilla de sitio Web ASP.NET para Visual C#, el paso siguiente consiste en crear una conexión de datos y una tabla de datos para el informe primario. En este tutorial, la conexión de datos se produce con la base de datos AdventureWorks2014.  
  
## <a name="to-define-a-data-connection-and-data-table-by-adding-a-dataset-for-parent-report"></a>Para definir una conexión de datos y una tabla de datos agregando un DataSet (para el informe primario)  
  
1.  En el menú **Sitio web** , seleccione **Agregar nuevo elemento**.  
  
2.  En el cuadro de diálogo **Agregar nuevo elemento** , seleccione **DataSet** y haga clic en **Agregar**. Cuando se le pida, debe agregar el elemento a la carpeta **App_Code** ; para ello, haga clic en **Sí**.  
  
    De este modo, agrega un nuevo archivo XSD **DataSet1.xsd** al proyecto y abre el Diseñador de DataSet.  
  
3.  En la ventana del Cuadro de herramientas, arrastre un control **[TableAdapter](http://msdn.microsoft.com/library/bz9tthwx.aspx)** hasta la superficie de diseño. De este modo, se inicia el Asistente para configuración de **TableAdapter** .  
  
4.  En la página **Elegir la conexión de datos** , haga clic en **Nueva conexión**.  
  
5.  Si es la primera vez que crea un origen de datos en Visual Studio, verá la página **Elegir origen de datos** . En el cuadro **Origen de datos** , seleccione **Microsoft SQL Server**.  
  
6.  En el cuadro de diálogo **Agregar conexión** , realice los pasos siguientes:  
  
    1.  En el cuadro **Nombre del servidor** , escriba el servidor donde se encuentra la base de datos **AdventureWorks2014** .  
  
        La instancia de SQL Server Express predeterminada es **(local)\sqlexpress**.  
  
    2.  En la sección **Iniciar sesión en el servidor** , seleccione la opción que proporciona acceso a los datos. **Usar autenticación de Windows** es el valor predeterminado.  
  
    3.  En la lista desplegable **Seleccione o escriba un nombre de base de datos** , haga clic en **AdventureWorks2014**.  
  
    4.  Seleccione **Aceptar**y luego seleccione **Siguiente**.  
  
7.  Si ha seleccionado **Usar autenticación de SQL Server** en el paso 6 (b), seleccione la opción si quiere incluir la información confidencial en la cadena o establecer la información en su código de aplicación.  
  
8.  En la página **Guardar la cadena de conexión en el archivo de configuración de la aplicación** , escriba el nombre de la cadena de conexión o acepte el predeterminado **AdventureWorks2014ConnectionString**. Seleccione **Siguiente**.  
  
9. En la página **Elegir un tipo de comando** , seleccione **Usar instrucciones SQL**y, después, haga clic en **Siguiente**.  
  
10. En la página **Escriba una instrucción SQL** , escriba la siguiente consulta de Transact-SQL para recuperar los datos de la base de datos **AdventureWorks2014** y seleccione **Siguiente**.  
  
    ```  
    SELECT ProductID, Name, ProductNumber, SafetyStockLevel, ReorderPoint FROM  Production.Product Order By ProductID  
    ```  
  
    También puede crear la consulta si hace clic en **Generador de consultas**y, después, compruebe la consulta al hacer clic en **Ejecutar consulta**. Si la consulta no devuelve los datos esperados, puede utilizar una versión anterior de AdventureWorks. Para más información sobre cómo obtener la base de datos de ejemplo **AdventureWorks2014**, vea [Bases de datos de ejemplo AdventureWorks](https://github.com/Microsoft/sql-server-samples/releases).  
  
11. En la página **Elegir los métodos que se van a generar** , asegúrese de desactivar **Crear métodos para enviar actualizaciones directamente a la base de datos (GenerateDBDirectMethods)** y seleccione **Finalizar**.  
  
    > [!WARNING]  
    > Asegúrese de desactivar **Crear métodos para enviar actualizaciones directamente a la base de datos (GenerateDBDirectMethods)**  
  
    Ahora ha completado la configuración del objeto DataTable de ADO.NET como origen de datos para el informe. En la página del Diseñador de Dataset en Visual Studio, debería ver el objeto DataTable que agregó, con las columnas especificadas en la consulta. DataSet1 contiene los datos de la tabla Product, según la consulta.  
  
12. Guarde el archivo.  
  
13. Para obtener una vista previa de los datos, seleccione **Vista previa de los datos** en el menú **Datos** y seleccione **Vista previa**.  
  
## <a name="next-task"></a>Tarea siguiente  
Ha creado correctamente una conexión de datos y una tabla de datos para el informe primario. Después, diseñará el informe primario usando el Asistente para informes. Consulte [Lección 3: Diseñar el informe primario usando el Asistente para informes](../reporting-services/lesson-3-design-the-parent-report-using-the-report-wizard.md).  
  

