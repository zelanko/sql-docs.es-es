---
title: 'Lección 2: Definir una conexión de datos y una tabla de datos para el informe primario | Microsoft Docs'
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
ms.assetid: f02dee0c-85ad-45d4-b707-10e9e8541db9
author: markingmyname
ms.author: maghan
manager: kfile
ms.openlocfilehash: 0a19f5fd51cf4e1b24e898ef3016c46edc152920
ms.sourcegitcommit: dfb1e6deaa4919a0f4e654af57252cfb09613dd5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/11/2019
ms.locfileid: "56022888"
---
# <a name="lesson-2-define-a-data-connection-and-data-table-for-parent-report"></a>Lección 2: Definir una conexión de datos y una tabla de datos para el informe primario
  Después de crear un proyecto de sitio Web nuevo con la plantilla de sitio Web ASP.NET para Visual C#, el paso siguiente consiste en crear una conexión de datos y una tabla de datos para el informe primario. En este tutorial, la conexión de datos se produce con la base de datos AdventureWorks2008. También tiene la opción de conectar con la base de datos AdventureWorks2012.  
  
### <a name="to-define-a-data-connection-and-data-table-by-adding-a-dataset-for-parent-report"></a>Para definir una conexión de datos y una tabla de datos agregando un DataSet (para el informe primario)  
  
1.  En el menú **Sitio web** , seleccione **Agregar nuevo elemento**.  
  
2.  En el **Agregar nuevo elemento** cuadro de diálogo, seleccione **DataSet** y haga clic en **agregar**. Cuando se le pida, debe agregar el elemento a la **App_Code** carpeta haciendo **Sí**.  
  
     De este modo, agrega un nuevo archivo XSD **DataSet1.xsd** al proyecto y abre el Diseñador de DataSet.  
  
3.  En la ventana del Cuadro de herramientas, arrastre un control **[TableAdapter](https://msdn.microsoft.com/library/bz9tthwx\(v=vs.100\).aspx)** hasta la superficie de diseño. De este modo, se inicia el Asistente para configuración de **TableAdapter** .  
  
4.  En el **elegir la conexión de datos** página, haga clic en **nueva conexión**.  
  
5.  Si es la primera vez que ha creado un origen de datos en Visual Studio, verá la página **Elegir origen de datos**. En el cuadro **Origen de datos** , seleccione **Microsoft SQL Server**.  
  
6.  En el cuadro de diálogo **Agregar conexión** , realice los pasos siguientes:  
  
    1.  En el **nombre del servidor** , escriba el servidor donde la **AdventureWorks2008** se encuentra la base de datos.  
  
         La instancia de SQL Server Express predeterminada es **(local)\sqlexpress**.  
  
    2.  En la sección **Iniciar sesión en el servidor** , seleccione la opción que proporciona acceso a los datos. **Usar autenticación de Windows** es el valor predeterminado.  
  
    3.  Desde el **seleccione o escriba un nombre de base de datos** la lista desplegable, haga clic en **AdventureWorks2008**.  
  
    4.  Haga clic en **Aceptar**y, a continuación, en **Siguiente**.  
  
7.  Si ha seleccionado **Usar autenticación de SQL Server** en el paso 6 (b), seleccione la opción si quiere incluir la información confidencial en la cadena o establecer la información en su código de aplicación.  
  
8.  En el **Guardar cadena de conexión en el archivo de configuración de aplicación** página, escriba el nombre de la cadena de conexión o acepte el valor predeterminado **AdventureWorks2008ConnectionString**. Haga clic en **Siguiente**.  
  
9. En el **elegir un tipo de comando** página, seleccione **usar instrucciones SQL**y, a continuación, haga clic en **siguiente**.  
  
10. En el **escriba una instrucción SQL** , escriba la siguiente consulta de Transact-SQL para recuperar datos de la **AdventureWorks2008** de base de datos y, a continuación, haga clic en **siguiente**.  
  
    ```  
    SELECT ProductID, Name, ProductNumber, SafetyStockLevel, ReorderPoint FROM  Production.Product Order By ProductID  
    ```  
  
     También puede crear la consulta haciendo clic en **generador de consultas**y, a continuación, compruebe la consulta haciendo clic en **Ejecutar consulta**. Si la consulta no devuelve los datos esperados, puede utilizar una versión anterior de AdventureWorks. Para obtener más información acerca de cómo instalar el **AdventureWorks2008** versión de AdventureWorks, vea [Tutorial: Instalación de la base de datos AdventureWorks](https://msdn.microsoft.com/library/aa992075\(v=vs.100\).aspx).  
  
11. En el **elija los métodos para generar** página, no olvide desactivar **crear métodos para enviar actualizaciones directamente a la base de datos (GenerateDBDirectMethods)** y, a continuación, haga clic en **finalizar**.  
  
    > [!WARNING]  
    >  Asegúrese de desactivar la creación  
  
     Ahora ha completado la configuración del objeto DataTable de ADO.NET como origen de datos para el informe. En la página del Diseñador de Dataset en Visual Studio, debería ver el objeto DataTable que agregó, con las columnas especificadas en la consulta. DataSet1 contiene los datos de la tabla Product, según la consulta.  
  
12. Guarde el archivo.  
  
13. Para obtener una vista previa de los datos, haga clic en **datos de vista previa** en el **datos** menú y, a continuación, haga clic en **Preview**.  
  
## <a name="next-task"></a>Tarea siguiente  
 Ha creado correctamente una conexión de datos y una tabla de datos para el informe primario. Después, diseñará el informe primario usando el Asistente para informes.  
  
  
