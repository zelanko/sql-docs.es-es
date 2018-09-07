---
title: Carga de datos en SQL Server o Azure SQL Database con SQL Server Integration Services (SSIS) | Microsoft Docs
description: Se muestra cómo crear un paquete de SQL Server Integration Services (SSIS) para mover datos desde una gran variedad de orígenes de datos a SQL Server o Azure SQL Database.
documentationcenter: NA
ms.prod: sql
ms.prod_service: integration-services
ms.suite: sql
ms.technology: integration-services
ms.devlang: NA
ms.topic: conceptual
ms.tgt_pltfrm: NA
ms.custom: loading
ms.date: 08/20/2018
ms.author: douglasl
author: douglaslMS
manager: craigg-msft
ms.openlocfilehash: ab5ce3238285cbe687b2608edb5236d460baa197
ms.sourcegitcommit: 9cd01df88a8ceff9f514c112342950e03892b12c
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/20/2018
ms.locfileid: "40412681"
---
# <a name="load-data-into-sql-server-or-azure-sql-database-with-sql-server-integration-services-ssis"></a>Carga de datos en SQL Server o Azure SQL Database con SQL Server Integration Services (SSIS)

Cree un paquete de SQL Server Integration Services (SSIS) para cargar datos en SQL Server o [Azure SQL Database](/azure/sql-database/). Si quiere, puede reestructurar, transformar y limpiar los datos a medida que pasan a través del flujo de datos de SSIS.

En este artículo se explica cómo realizar las siguientes tareas:

* Crear un nuevo proyecto de Integration Services en Visual Studio.
* Diseñar un paquete de SSIS que cargue datos del origen en el destino.
* Ejecutar el paquete de SSIS para cargar los datos.


## <a name="basic-concepts"></a>Conceptos básicos

El paquete es la unidad de trabajo básica en SSIS. Los paquetes relacionados se agrupan en proyectos. Los proyectos y los paquetes de diseño se crean en Visual Studio con SQL Server Data Tools. El proceso de diseño es un proceso visual en el que se arrastran componentes del cuadro de herramientas y se colocan en la superficie de diseño, se conectan y se establecen sus propiedades. Después de terminar el paquete, puede ejecutarlo y puede implementarlo opcionalmente en SQL Server o SQL Database para una administración, supervisión y seguridad globales.

Una introducción detallada a SSIS queda fuera del ámbito de este artículo. Para más información, vea los siguientes artículos:

- [SQL Server Integration Services](sql-server-integration-services.md)

- [Tutorial de SSIS: Crear un paquete ETL sencillo](ssis-how-to-create-an-etl-package.md)

## <a name="about-the-solution"></a>Acerca de la solución

La solución es un paquete típico que usa una tarea Flujo de datos que contiene un origen y un destino. Este enfoque es compatible con una amplia gama de orígenes de datos, incluidos SQL Server y Azure SQL Database.

En este tutorial se usa SQL Server como origen de datos. SQL Server se ejecuta en local o en una máquina virtual de Azure.

Para conectarse a SQL Server y a SQL Database, puede usar un administrador de conexiones de ADO.NET y un origen y un destino, o bien un administrador de conexiones OLE DB y un origen y un destino. En este tutorial se usa ADO NET porque tiene las mínimas opciones de configuración. OLE DB puede proporcionar un rendimiento ligeramente mejor que ADO NET.

Como método abreviado, puede usar el Asistente para importación y exportación de SQL Server para crear el paquete básico. Después, guarde el paquete y ábralo en Visual Studio o SSDT para verlo y personalizarlo. Para más información, vea [Importar y exportar datos con el Asistente para importación y exportación de SQL Server](import-export-data/import-and-export-data-with-the-sql-server-import-and-export-wizard.md).

## <a name="prerequisites"></a>Prerequisites
Para realizar este tutorial, necesita lo siguiente:

1. **SQL Server Integration Services (SSIS)**. SSIS es un componente de SQL Server y exige una versión con licencia, de desarrollador o de evaluación de SQL Server. Para obtener una versión de evaluación de SQL Server, vea [Evaluaciones de SQL Server](https://www.microsoft.com/evalcenter/evaluate-sql-server-2017-rtm).
2. **Visual Studio** (opcional). Para obtener la edición gratuita de Visual Studio Community, vea [Visual Studio Community][Visual Studio Community]. Si no quiere instalar Visual Studio, puede instalar solo SQL Server Data Tools (SSDT). SSDT instala una versión de Visual Studio con funcionalidad limitada.
3. **SQL Server Data Tools para Visual Studio (SSDT)**. Para obtener SQL Server Data Tools para Visual Studio, vea [Descargar SQL Server Data Tools (SSDT)][Download SQL Server Data Tools (SSDT)].
4. Este tutorial se conecta a una instancia de SQL Server o SQL Database y carga datos en ella. Necesita permisos para conectarse, crear una tabla y cargar datos en:
   - **Una base de datos de Azure SQL Database**. Para obtener más información, vea [Azure SQL Database](/azure/sql-database/).  
      o Administrador de configuración de
   - **Una instancia de SQL Server**. SQL Server se ejecuta en local o en una máquina virtual de Azure. Para descargar una edición gratuita de evaluación o desarrollador de SQL Server, vea [Descargas de SQL Server](https://www.microsoft.com/sql-server/sql-server-downloads).

5. **Datos de ejemplo**. En este tutorial se usan datos de ejemplo almacenados en SQL Server en la base de datos de ejemplo AdventureWorks como los datos de origen. Para obtener la base de datos de ejemplo AdventureWorks, vea [AdventureWorks Sample Databases][AdventureWorks 2014 Sample Databases] (Bases de datos de ejemplo de AdventureWorks).
6. **Una regla de firewall** si se van a cargar datos en SQL Database. Tiene que crear una regla de firewall en SQL Database con la dirección IP del equipo local para cargar datos en SQL Database.

## <a name="create-a-new-integration-services-project"></a>Crear un proyecto de Integration Services
1. Inicie Visual Studio.
2. En el menú **Archivo**, seleccione **Nuevo | Proyecto**.
3. Vaya a los tipos de proyecto **Instalados | Plantillas | Inteligencia empresarial | Integration Services**.
4. Seleccione **Proyecto de Integration Services**. Proporcione los valores de **Nombre** y **Ubicación** y luego seleccione **Aceptar**.

Se abre Visual Studio y crea un nuevo proyecto de Integration Services (SSIS). Luego Visual Studio abre el diseñador para el nuevo paquete único de SSIS (Package.dtsx) en el proyecto. Se ven las siguientes áreas de pantalla:

* En el lado izquierdo, el **cuadro de herramientas** de componentes de SSIS.
* En el centro, la superficie de diseño, con varias pestañas. Normalmente se usan al menos las pestañas **Flujo de control** y **Flujo de datos**.
* En el lado derecho, los paneles **Explorador de soluciones** y **Propiedades**.
  
    ![][01]

## <a name="create-the-basic-data-flow"></a>Crear el flujo de datos básico
1. Arrastre una tarea Flujo de datos desde el cuadro de herramientas al centro de la superficie de diseño (en la pestaña **Flujo de control**).
   
    ![][02]
2. Haga doble clic en la tarea Flujo de datos para ir a la pestaña Flujo de datos.
3. En la lista Otros orígenes del cuadro de herramientas, arrastre un origen de ADO.NET a la superficie de diseño. Con el adaptador de origen aún seleccionado, cambie su nombre a **Origen de SQL Server** en el panel **Propiedades**.
4. Desde la lista Otros destinos del cuadro de herramientas, arrastre un destino de ADO.NET a la superficie de diseño bajo el origen de ADO.NET. Con el adaptador de destino aún seleccionado, cambie su nombre a **Destino de SQL** en el panel **Propiedades**.
   
    ![][09]

## <a name="configure-the-source-adapter"></a>Configurar el adaptador de origen
1. Haga doble clic en el adaptador de origen para abrir el **Editor de orígenes de ADO.NET**.
   
    ![][03]
2. En la pestaña **Administrador de conexiones** del **Editor de orígenes de ADO.NET**, haga clic en el botón **Nuevo** situado junto a la lista **Administrador de conexiones de ADO.NET** para abrir el cuadro de diálogo **Configurar el administrador de conexiones ADO.NET** y crear la configuración de conexión para la base de datos de SQL Server desde la que carga datos este tutorial.
   
    ![][04]
3. En el cuadro de diálogo **Configurar el administrador de conexiones ADO.NET**, haga clic en el botón **Nuevo** para abrir el cuadro de diálogo **Administrador de conexiones** y crear una nueva conexión de datos.
   
    ![][05]
4. En el cuadro de diálogo **Administrador de conexiones**, haga lo siguiente.
   
   1. En **Proveedor**, seleccione el proveedor de datos SqlClient.
   2. En **Nombre del servidor**, escriba el nombre del servidor de SQL Server.
   3. En la sección **Iniciar sesión en el servidor**, seleccione o escriba la información de autenticación.
   4. En la sección **Conectar con una base de datos**, seleccione la base de datos de ejemplo AdventureWorks.
   5. Haga clic en **Probar conexión**.
      
       ![][06]
   6. En el cuadro de diálogo que informa de los resultados de la prueba de conexión, haga clic en **Aceptar** para volver al cuadro de diálogo **Administrador de conexiones**.
   7. En el cuadro de diálogo **Administrador de conexiones**, haga clic en **Aceptar** para volver al cuadro de diálogo **Configurar el administrador de conexiones ADO.NET**.
5. En el cuadro de diálogo **Configurar el administrador de conexiones ADO.NET**, haga clic en **Aceptar** para volver al **Editor de orígenes de ADO.NET**.
6. En el **Editor de orígenes de ADO.NET**, en la lista **Nombre de la tabla o la vista**, seleccione la tabla **Sales.SalesOrderDetail**.
   
    ![][07]
7. Haga clic en **Vista previa** para ver las 200 primeras filas de datos de la tabla de origen en el cuadro de diálogo **Vista previa de los resultados de la consulta**.
   
    ![][08]
8. En el cuadro de diálogo **Vista previa de los resultados de la consulta**, haga clic en **Cerrar** para volver al **Editor de orígenes de ADO.NET**.
9. En el **Editor de orígenes de ADO.NET**, haga clic en **Aceptar** para acabar de configurar el origen de datos.

## <a name="connect-the-source-adapter-to-the-destination-adapter"></a>Conectar el adaptador de origen al adaptador de destino
1. Seleccione el adaptador de origen en la superficie de diseño.
2. Seleccione la flecha azul que va desde el adaptador de origen y arrástrela al editor de destino hasta que quede en su lugar.
   
    ![][10]
   
    En un paquete de SSIS típico, se usa una serie de otros componentes del cuadro de herramientas de SSIS entre el origen y el destino para reestructurar, transformar y limpiar los datos a medida que pasan a través del flujo de datos de SSIS. Para que este ejemplo sea lo más sencillo posible, se conecta el origen directamente al destino.

## <a name="configure-the-destination-adapter"></a>Configurar el adaptador de destino
1. Haga doble clic en el adaptador de destino para abrir el **Editor de destinos de ADO.NET**.
   
    ![][11]
2. En la pestaña **Administrador de conexiones** del **Editor de destinos de ADO.NET**, haga clic en el botón **Nuevo** situado junto a la lista **Administrador de conexiones** para abrir el cuadro de diálogo **Configurar el administrador de conexiones ADO.NET** y crear la configuración de conexión para la base de datos en la que se cargan los datos de este tutorial.
3. En el cuadro de diálogo **Configurar el administrador de conexiones ADO.NET**, haga clic en el botón **Nuevo** para abrir el cuadro de diálogo **Administrador de conexiones** y crear una nueva conexión de datos.
4. En el cuadro de diálogo **Administrador de conexiones**, haga lo siguiente.
   1. En **Proveedor**, seleccione el proveedor de datos SqlClient.
   2. En **Nombre del servidor**, escriba el nombre de SQL Server o del servidor de SQL Database.
   3. En la sección **Iniciar sesión en el servidor**, seleccione **Usar la autenticación de SQL Server** y escriba la información de autenticación.
   4. En la sección **Conectar con una base de datos**, seleccione una base de datos existente.
    A. Haga clic en **Probar conexión**.
    B. En el cuadro de diálogo que informa de los resultados de la prueba de conexión, haga clic en **Aceptar** para volver al cuadro de diálogo **Administrador de conexiones**.
    c. En el cuadro de diálogo **Administrador de conexiones**, haga clic en **Aceptar** para volver al cuadro de diálogo **Configurar el administrador de conexiones ADO.NET**.
5. En el cuadro de diálogo **Configurar el administrador de conexiones ADO.NET**, haga clic en **Aceptar** para volver al **Editor de destinos de ADO.NET**.
6. En el **Editor de destinos de ADO.NET**, haga clic en **Nuevo** junto a la lista **Usar una tabla o una vista** para abrir el cuadro de diálogo **Crear tabla** para crear una tabla de destino con una lista de columnas que coincida con la tabla de origen.
   
    ![][12a]
7. En el cuadro de diálogo **Crear tabla**, haga lo siguiente.
   
   1. Cambie el nombre de la tabla de destino a **SalesOrderDetail**.
      
       ![][12b]

   2. Haga clic en **Aceptar** para crear la tabla y volver al **Editor de destinos de ADO.NET**.
8. En el **Editor de destinos de ADO.NET**, seleccione la pestaña **Asignaciones** para ver cómo se asignan las columnas del origen a las del destino.
   
    ![][13]
9. Haga clic en **Aceptar** para acabar de configurar el destino.

## <a name="run-the-package-to-load-the-data"></a>Ejecutar el paquete para cargar los datos
Para ejecutar el paquete, haga clic en el botón **Iniciar** de la barra de herramientas o seleccione una de las opciones **Ejecutar** del menú **Depurar**.

En los siguientes párrafos se describe lo que verá si ha creado el paquete con la segunda opción que se describe en este artículo, es decir, con un flujo de datos que contiene un origen y un destino.

A medida que el paquete comienza a ejecutarse, se ven ruedas amarillas que giran para indicar actividad, además del número de filas procesadas hasta el momento.

![][14]

Cuando el paquete termina de ejecutarse, se ven marcas de verificación verdes para indicar el éxito, además del número total de filas de datos cargadas desde el origen en el destino.

![][15]

¡Enhorabuena! Ha usado correctamente SQL Server Integration Services para cargar datos en SQL Server o Azure SQL Database.

## <a name="next-steps"></a>Pasos siguientes

- Obtenga más información sobre cómo depurar paquetes y solucionar los problemas que planteen en el entorno de diseño. Empiece aquí: [Herramientas para solucionar problemas con el desarrollo de paquetes][Troubleshooting Tools for Package Development].

- Obtenga más información sobre cómo implementar los paquetes y los proyectos de SSIS en Integration Services Server u otra ubicación de almacenamiento. Empiece aquí: [Implementación de proyectos y paquetes][Deployment of Projects and Packages].

<!-- Image references -->
[01]:  ./media/load-data-to-sql-database-with-ssis/ssis-designer-01.png
[02]:  ./media/load-data-to-sql-database-with-ssis/ssis-data-flow-task-02.png
[03]:  ./media/load-data-to-sql-database-with-ssis/ado-net-source-03.png
[04]:  ./media/load-data-to-sql-database-with-ssis/ado-net-connection-manager-04.png
[05]:  ./media/load-data-to-sql-database-with-ssis/ado-net-connection-05.png
[06]:  ./media/load-data-to-sql-database-with-ssis/test-connection-06.png
[07]:  ./media/load-data-to-sql-database-with-ssis/ado-net-source-07.png
[08]:  ./media/load-data-to-sql-database-with-ssis/preview-data-08.png
[09]:  ./media/load-data-to-sql-database-with-ssis/source-destination-09.png
[10]:  ./media/load-data-to-sql-database-with-ssis/connect-source-destination-10.png
[11]:  ./media/load-data-to-sql-database-with-ssis/ado-net-destination-11.png
[12a]: ./media/load-data-to-sql-database-with-ssis/destination-query-before-12a.png
[12b]: ./media/load-data-to-sql-database-with-ssis/destination-query-after-12b.png
[13]:  ./media/load-data-to-sql-database-with-ssis/column-mapping-13.png
[14]:  ./media/load-data-to-sql-database-with-ssis/package-running-14.png
[15]:  ./media/load-data-to-sql-database-with-ssis/package-success-15.png

<!-- Article references -->

<!-- MSDN references -->
[Download SQL Server Data Tools (SSDT)]: ../ssdt/download-sql-server-data-tools-ssdt.md
[Data Flow]: ./data-flow/data-flow.md
[Troubleshooting Tools for Package Development]: ./troubleshooting/troubleshooting-tools-for-package-development.md
[Deployment of Projects and Packages]: ./packages/deploy-integration-services-ssis-projects-and-packages.md

<!--Other Web references-->
[Microsoft SQL Server 2017 Integration Services Feature Pack for Azure]: https://www.microsoft.com/download/details.aspx?id=54798
[SQL Server Evaluations]: https://www.microsoft.com/evalcenter/evaluate-sql-server-2017
[Visual Studio Community]: https://www.visualstudio.com/products/visual-studio-community-vs.aspx
[AdventureWorks 2014 Sample Databases]: https://github.com/Microsoft/sql-server-samples/releases/tag/adventureworks
