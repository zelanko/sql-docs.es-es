---
title: Cargar datos de SQL Server en Azure SQL Data Warehouse (SSIS) | Microsoft Docs
description: Muestra cómo crear un paquete de SQL Server Integration Services (SSIS) para mover datos desde una gran variedad de orígenes de datos a SQL Data Warehouse.
documentationcenter: NA
ms.service: sql-data-warehouse
ms.component: data-movement
ms.devlang: NA
ms.topic: conceptual
ms.tgt_pltfrm: NA
ms.custom: loading
ms.date: 04/04/2018
ms.author: douglasl
author: douglaslMS
manager: craigg-msft
ms.openlocfilehash: 75a352ff4bb1f074a89ad4cc007844261d20c431
ms.sourcegitcommit: c8f7e9f05043ac10af8a742153e81ab81aa6a3c3
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/17/2018
ms.locfileid: "39087587"
---
# <a name="load-data-from-sql-server-to-azure-sql-data-warehouse-with-sql-server-integration-services-ssis"></a>Cargar datos de SQL Server en Azure SQL Data Warehouse con SQL Server Integration Services (SSIS)

Cree un paquete de SQL Server Integration Services (SSIS) para cargar datos de SQL Server en [Azure SQL Data Warehouse](/azure/sql-data-warehouse/index). Si quiere, puede reestructurar, transformar y limpiar los datos a medida que pasan a través del flujo de datos de SSIS.

En este tutorial, aprenderá a:

* Crear un nuevo proyecto de Integration Services en Visual Studio.
* Conectarse a orígenes de datos, incluidos SQL Server (como origen) y SQL Data Warehouse (como destino).
* Diseñar un paquete de SSIS que cargue datos del origen en el destino.
* Ejecutar el paquete de SSIS para cargar los datos.

En este tutorial se usa SQL Server como origen de datos. SQL Server se puede ejecutar en local o en una máquina virtual de Azure.

## <a name="basic-concepts"></a>Conceptos básicos
El paquete es la unidad de trabajo en SSIS. Los paquetes relacionados se agrupan en proyectos. Los proyectos y los paquetes de diseño se crean en Visual Studio con SQL Server Data Tools. El proceso de diseño es un proceso visual en el que se arrastran componentes del cuadro de herramientas y se colocan en la superficie de diseño, se conectan y se establecen sus propiedades. Después de terminar el paquete, puede implementarlo opcionalmente en SQL Server para una administración, supervisión y seguridad globales.

## <a name="options-for-loading-data-with-ssis"></a>Opciones para cargar datos con SSIS
SQL Server Integration Services (SSIS) es un conjunto de herramientas flexible que proporciona una serie de opciones para conectarse a SQL Data Warehouse y cargar datos en él.

1. Use un destino de ADO NET para conectarse a SQL Data Warehouse. En este tutorial se usa un destino de ADO NET porque tiene las mínimas opciones de configuración.
2. Use un destino de OLE DB para conectarse a SQL Data Warehouse. Esta opción puede proporcionar un rendimiento ligeramente mejor que el destino de ADO NET.
3. Use la tarea de carga en el blob de Azure para cargar los datos en Azure Blob Storage. Luego use la tarea Ejecutar SQL de SSIS para iniciar un script de Polybase que cargue los datos en SQL Data Warehouse. Esta opción proporciona el mejor rendimiento de las tres que se muestran aquí. Para obtener la tarea de carga en el blob de Azure, descargue [Microsoft SQL Server 2016 Integration Services Feature Pack for Azure][Microsoft SQL Server 2016 Integration Services Feature Pack for Azure]. Para obtener más información sobre Polybase, vea [Guía de PolyBase][PolyBase Guide].

## <a name="before-you-start"></a>Antes de empezar
Para realizar este tutorial, necesita:

1. **SQL Server Integration Services (SSIS)**. SSIS es un componente de SQL Server y exige una versión de evaluación o una versión con licencia de SQL Server. Para obtener una versión de evaluación de SQL Server 2016 Preview, vea [SQL Server Evaluaciones][SQL Server Evaluations].
2. **Visual Studio**. Para obtener la edición gratuita de Visual Studio Community, vea [Visual Studio Community][Visual Studio Community].
3. **SQL Server Data Tools para Visual Studio (SSDT)**. Para obtener SQL Server Data Tools para Visual Studio, vea [Descargar SQL Server Data Tools (SSDT)][Download SQL Server Data Tools (SSDT)].
4. **Datos de ejemplo**. En este tutorial se usan datos de ejemplo almacenados en SQL Server en la base de datos de ejemplo AdventureWorks como datos de origen para cargar en SQL Data Warehouse. Para obtener la base de datos de ejemplo AdventureWorks, vea [Bases de datos de ejemplo AdventureWorks 2014][AdventureWorks 2014 Sample Databases].
5. **Una base de datos de SQL Data Warehouse y permisos**. Este tutorial se conecta a una instancia de SQL Data Warehouse y carga datos en ella. Necesita permisos para crear una tabla y cargar datos.
6. **Una regla de firewall**. Tiene que crear una regla de firewall en SQL Data Warehouse con la dirección IP del equipo local para cargar datos en SQL Data Warehouse.

## <a name="step-1-create-a-new-integration-services-project"></a>Paso 1: Crear un nuevo proyecto de Integration Services
1. Inicie Visual Studio.
2. En el menú **Archivo**, seleccione **Nuevo | Proyecto**.
3. Vaya a los tipos de proyecto **Instalados | Plantillas | Inteligencia empresarial | Integration Services**.
4. Seleccione **Proyecto de Integration Services**. Proporcione los valores de **Nombre** y **Ubicación** y luego seleccione **Aceptar**.

Se abre Visual Studio y crea un nuevo proyecto de Integration Services (SSIS). Luego Visual Studio abre el diseñador para el nuevo paquete único de SSIS (Package.dtsx) en el proyecto. Se ven las siguientes áreas de pantalla:

* En el lado izquierdo, el **cuadro de herramientas** de componentes de SSIS.
* En el centro, la superficie de diseño, con varias pestañas. Normalmente se usan al menos las pestañas **Flujo de control** y **Flujo de datos**.
* En el lado derecho, los paneles **Explorador de soluciones** y **Propiedades**.
  
    ![][01]

## <a name="step-2-create-the-basic-data-flow"></a>Paso 2: Crear el flujo de datos básico
1. Arrastre una tarea Flujo de datos desde el cuadro de herramientas al centro de la superficie de diseño (en la pestaña **Flujo de control**).
   
    ![][02]
2. Haga doble clic en la tarea Flujo de datos para ir a la pestaña Flujo de datos.
3. En la lista Otros orígenes del cuadro de herramientas, arrastre un origen de ADO.NET a la superficie de diseño. Con el adaptador de origen aún seleccionado, cambie su nombre a **Origen de SQL Server** en el panel **Propiedades**.
4. Desde la lista Otros destinos del cuadro de herramientas, arrastre un destino de ADO.NET a la superficie de diseño bajo el origen de ADO.NET. Con el adaptador de destino aún seleccionado, cambie su nombre a **Destino de SQL DW** en el panel **Propiedades**.
   
    ![][09]

## <a name="step-3-configure-the-source-adapter"></a>Paso 3: Configurar el adaptador de origen
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

## <a name="step-4-connect-the-source-adapter-to-the-destination-adapter"></a>Paso 4: Conectar el adaptador de origen al adaptador de destino
1. Seleccione el adaptador de origen en la superficie de diseño.
2. Seleccione la flecha azul que va desde el adaptador de origen y arrástrela al editor de destino hasta que quede en su lugar.
   
    ![][10]
   
    En un paquete de SSIS típico, se usa una serie de otros componentes del cuadro de herramientas de SSIS entre el origen y el destino para reestructurar, transformar y limpiar los datos a medida que pasan a través del flujo de datos de SSIS. Para que este ejemplo sea lo más sencillo posible, se conecta el origen directamente al destino.

## <a name="step-5-configure-the-destination-adapter"></a>Paso 5: Configurar el adaptador de destino
1. Haga doble clic en el adaptador de destino para abrir el **Editor de destinos de ADO.NET**.
   
    ![][11]
2. En la pestaña **Administrador de conexiones** del **Editor de destinos de ADO.NET**, haga clic en el botón **Nuevo** situado junto a la lista **Administrador de conexiones** para abrir el cuadro de diálogo **Configurar el administrador de conexiones ADO.NET** y crear la configuración de conexión para la base de datos de Azure SQL Data Warehouse en la que carga datos este tutorial.
3. En el cuadro de diálogo **Configurar el administrador de conexiones ADO.NET**, haga clic en el botón **Nuevo** para abrir el cuadro de diálogo **Administrador de conexiones** y crear una nueva conexión de datos.
4. En el cuadro de diálogo **Administrador de conexiones**, haga lo siguiente.
   1. En **Proveedor**, seleccione el proveedor de datos SqlClient.
   2. En **Nombre del servidor**, escriba el nombre de SQL Data Warehouse.
   3. En la sección **Iniciar sesión en el servidor**, seleccione **Usar la autenticación de SQL Server** y escriba la información de autenticación.
   4. En la sección **Conectar con una base de datos**, seleccione una base de datos de SQL Data Warehouse existente.
   5. Haga clic en **Probar conexión**.
   6. En el cuadro de diálogo que informa de los resultados de la prueba de conexión, haga clic en **Aceptar** para volver al cuadro de diálogo **Administrador de conexiones**.
   7. En el cuadro de diálogo **Administrador de conexiones**, haga clic en **Aceptar** para volver al cuadro de diálogo **Configurar el administrador de conexiones ADO.NET**.
5. En el cuadro de diálogo **Configurar el administrador de conexiones ADO.NET**, haga clic en **Aceptar** para volver al **Editor de destinos de ADO.NET**.
6. En el **Editor de destinos de ADO.NET**, haga clic en **Nuevo** junto a la lista **Usar una tabla o una vista** para abrir el cuadro de diálogo **Crear tabla** para crear una tabla de destino con una lista de columnas que coincida con la tabla de origen.
   
    ![][12a]
7. En el cuadro de diálogo **Crear tabla**, haga lo siguiente.
   
   1. Cambie el nombre de la tabla de destino a **SalesOrderDetail**.
   2. Quite la columna **rowguid**. El tipo de datos **uniqueidentifier** no se admite en SQL Data Warehouse.
   3. Cambie el tipo de datos de la columna **LineTotal** a **money**. El tipo de datos **decimal** no se admite en SQL Data Warehouse. Para obtener información sobre los tipos de datos admitidos, vea [CREATE TABLE (Azure SQL Data Warehouse, Almacenamiento de datos paralelos)][CREATE TABLE (Azure SQL Data Warehouse, Parallel Data Warehouse)].
      
       ![][12b]
   4. Haga clic en **Aceptar** para crear la tabla y volver al **Editor de destinos de ADO.NET**.
8. En el **Editor de destinos de ADO.NET**, seleccione la pestaña **Asignaciones** para ver cómo se asignan las columnas del origen a las del destino.
   
    ![][13]
9. Haga clic en **Aceptar** para acabar de configurar el origen de datos.

## <a name="step-6-run-the-package-to-load-the-data"></a>Paso 6: Ejecutar el paquete para cargar los datos
Para ejecutar el paquete, haga clic en el botón **Iniciar** de la barra de herramientas o seleccione una de las opciones **Ejecutar** del menú **Depurar**.

A medida que el paquete comienza a ejecutarse, se ven ruedas amarillas que giran para indicar actividad, además del número de filas procesadas hasta el momento.

![][14]

Cuando el paquete termina de ejecutarse, se ven marcas de verificación verdes para indicar el éxito, además del número total de filas de datos cargadas desde el origen en el destino.

![][15]

¡Enhorabuena! Ha usado correctamente SQL Server Integration Services para cargar datos en Azure SQL Data Warehouse.

## <a name="next-steps"></a>Pasos siguientes
* Obtenga más información sobre el flujo de datos de SSIS. Empiece aquí: [Flujo de datos][Data Flow].
* Obtenga más información sobre cómo depurar paquetes y solucionar los problemas que planteen en el entorno de diseño. Empiece aquí: [Herramientas para solucionar problemas con el desarrollo de paquetes][Troubleshooting Tools for Package Development].
* Obtenga más información sobre cómo implementar los paquetes y los proyectos de SSIS en Integration Services Server u otra ubicación de almacenamiento. Empiece aquí: [Implementación de proyectos y paquetes][Deployment of Projects and Packages].

<!-- Image references -->
[01]:  ./media/load-data-to-sql-data-warehouse/ssis-designer-01.png
[02]:  ./media/load-data-to-sql-data-warehouse/ssis-data-flow-task-02.png
[03]:  ./media/load-data-to-sql-data-warehouse/ado-net-source-03.png
[04]:  ./media/load-data-to-sql-data-warehouse/ado-net-connection-manager-04.png
[05]:  ./media/load-data-to-sql-data-warehouse/ado-net-connection-05.png
[06]:  ./media/load-data-to-sql-data-warehouse/test-connection-06.png
[07]:  ./media/load-data-to-sql-data-warehouse/ado-net-source-07.png
[08]:  ./media/load-data-to-sql-data-warehouse/preview-data-08.png
[09]:  ./media/load-data-to-sql-data-warehouse/source-destination-09.png
[10]:  ./media/load-data-to-sql-data-warehouse/connect-source-destination-10.png
[11]:  ./media/load-data-to-sql-data-warehouse/ado-net-destination-11.png
[12a]: ./media/load-data-to-sql-data-warehouse/destination-query-before-12a.png
[12b]: ./media/load-data-to-sql-data-warehouse/destination-query-after-12b.png
[13]:  ./media/load-data-to-sql-data-warehouse/column-mapping-13.png
[14]:  ./media/load-data-to-sql-data-warehouse/package-running-14.png
[15]:  ./media/load-data-to-sql-data-warehouse/package-success-15.png

<!-- Article references -->

<!-- MSDN references -->
[PolyBase Guide]: ../relational-databases/polybase/polybase-guide.md
[Download SQL Server Data Tools (SSDT)]: ../ssdt/download-sql-server-data-tools-ssdt.md
[CREATE TABLE (Azure SQL Data Warehouse, Parallel Data Warehouse)]: ../t-sql/statements/create-table-azure-sql-data-warehouse.md
[Data Flow]: ./data-flow/data-flow.md
[Troubleshooting Tools for Package Development]: ./troubleshooting/troubleshooting-tools-for-package-development.md
[Deployment of Projects and Packages]: ./packages/deploy-integration-services-ssis-projects-and-packages.md

<!--Other Web references-->
[Microsoft SQL Server 2016 Integration Services Feature Pack for Azure]: http://go.microsoft.com/fwlink/?LinkID=626967
[SQL Server Evaluations]: https://www.microsoft.com/evalcenter/evaluate-sql-server-2016
[Visual Studio Community]: https://www.visualstudio.com/products/visual-studio-community-vs.aspx
[AdventureWorks 2014 Sample Databases]: https://github.com/Microsoft/sql-server-samples/releases/tag/adventureworks
