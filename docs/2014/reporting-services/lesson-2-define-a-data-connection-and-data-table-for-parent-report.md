---
title: 'Lección 2: Definir una conexión de datos y una tabla de datos para el informe primario | Microsoft Docs'
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
ms.assetid: f02dee0c-85ad-45d4-b707-10e9e8541db9
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 987e6924fe3fbffb416e4266861ae7cfede16596
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "66108497"
---
# <a name="lesson-2-define-a-data-connection-and-data-table-for-parent-report"></a>Lección 2: Definir una conexión de datos y una tabla de datos para el informe primario
  Después de crear un proyecto de sitio Web nuevo con la plantilla de sitio Web ASP.NET para Visual C#, el paso siguiente consiste en crear una conexión de datos y una tabla de datos para el informe primario. En este tutorial, la conexión de datos se produce con la base de datos AdventureWorks2008. También tiene la opción de conectar con la base de datos AdventureWorks2012.  
  
### <a name="to-define-a-data-connection-and-data-table-by-adding-a-dataset-for-parent-report"></a>Para definir una conexión de datos y una tabla de datos agregando un DataSet (para el informe primario)  
  
1.  En el menú **Sitio web** , seleccione **Agregar nuevo elemento**.  
  
2.  En el cuadro de diálogo **Agregar nuevo elemento** , seleccione **conjunto** de elementos y haga clic en **Agregar**. Cuando se le pida, debe agregar el elemento a la carpeta **App_Code** haciendo clic en **sí**.  
  
     De este modo, agrega un nuevo archivo XSD **DataSet1.xsd** al proyecto y abre el Diseñador de DataSet.  
  
3.  En la ventana del Cuadro de herramientas, arrastre un control **[TableAdapter](https://msdn.microsoft.com/library/bz9tthwx\(v=vs.100\).aspx)** hasta la superficie de diseño. De este modo, se inicia el Asistente para configuración de **TableAdapter** .  
  
4.  En la página **elegir la conexión de datos** , haga clic en **nueva conexión**.  
  
5.  Si es la primera vez que ha creado un origen de datos en Visual Studio, verá la página **Elegir origen de datos**. En el cuadro **Origen de datos** , seleccione **Microsoft SQL Server**.  
  
6.  En el cuadro de diálogo **Agregar conexión** , realice los pasos siguientes:  
  
    1.  En el cuadro **nombre del servidor** , escriba el servidor donde se encuentra la base de datos **AdventureWorks2008** .  
  
         La instancia de SQL Server Express predeterminada es **(local)\sqlexpress**.  
  
    2.  En la sección **Iniciar sesión en el servidor** , seleccione la opción que proporciona acceso a los datos. **Usar autenticación de Windows** es el valor predeterminado.  
  
    3.  En la lista desplegable **Seleccione o escriba un nombre de base de datos** , haga clic en **AdventureWorks2008**.  
  
    4.  Haga clic en **Aceptar** y luego en **Siguiente**.  
  
7.  Si ha seleccionado **Usar autenticación de SQL Server** en el paso 6 (b), seleccione la opción si quiere incluir la información confidencial en la cadena o establecer la información en su código de aplicación.  
  
8.  En la página **guardar la cadena de conexión en el archivo de configuración de la aplicación** , escriba el nombre de la cadena de conexión o acepte el valor predeterminado **AdventureWorks2008ConnectionString**. Haga clic en **Next**.  
  
9. En la página **elegir un tipo de comando** , seleccione **usar instrucciones SQL**y, a continuación, haga clic en **siguiente**.  
  
10. En la página **Escriba una instrucción SQL** , escriba la siguiente consulta de TRANSACT-SQL para recuperar datos de la base de datos **AdventureWorks2008** y, a continuación, haga clic en **siguiente**.  
  
    ```  
    SELECT ProductID, Name, ProductNumber, SafetyStockLevel, ReorderPoint FROM  Production.Product Order By ProductID  
    ```  
  
     También puede crear la consulta haciendo clic en **generador de consultas**y, a continuación, comprobar la consulta haciendo clic en **Ejecutar consulta**. Si la consulta no devuelve los datos esperados, puede utilizar una versión anterior de AdventureWorks. Para obtener más información acerca de cómo instalar la versión **AdventureWorks2008** de AdventureWorks, vea [Tutorial: instalar la base de datos AdventureWorks](https://msdn.microsoft.com/library/aa992075\(v=vs.100\).aspx).  
  
11. En la página **elegir los métodos que se van a generar** , asegúrese de desactivar **crear métodos para enviar actualizaciones directamente a la base de datos (GenerateDBDirectMethods)** y, a continuación, haga clic en **Finalizar**.  
  
    > [!WARNING]  
    >  Asegúrese de desactivar la creación  
  
     Ahora ha completado la configuración del objeto DataTable de ADO.NET como origen de datos para el informe. En la página del Diseñador de Dataset en Visual Studio, debería ver el objeto DataTable que agregó, con las columnas especificadas en la consulta. DataSet1 contiene los datos de la tabla Product, según la consulta.  
  
12. Guarde el archivo.  
  
13. Para obtener una vista previa de los datos, haga clic en **vista previa de datos** en el menú **datos** y, a continuación, haga clic en **vista previa**.  
  
## <a name="next-task"></a>Tarea siguiente  
 Ha creado correctamente una conexión de datos y una tabla de datos para el informe primario. Después, diseñará el informe primario usando el Asistente para informes.  
  
  
