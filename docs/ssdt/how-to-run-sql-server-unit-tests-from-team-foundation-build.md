---
title: 'Cómo: Ejecutar pruebas unitarias de SQL Server desde Team Foundation Build | Microsoft Docs'
ms.custom:
- SSDT
ms.date: 02/09/2017
ms.prod: sql
ms.technology: ssdt
ms.reviewer: ''
ms.topic: conceptual
ms.assetid: 24f5b85d-d6f9-415f-b09f-933b78dc0b67
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: fe4b6dd462a8f8fec6797c26f7ae0461c4b0a4ce
ms.sourcegitcommit: 9c6a37175296144464ffea815f371c024fce7032
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 11/15/2018
ms.locfileid: "51669864"
---
# <a name="how-to-run-sql-server-unit-tests-from-team-foundation-build"></a>Cómo: Ejecutar pruebas unitarias de SQL Server desde Team Foundation Build
Puede usar Team Foundation Build para ejecutar las pruebas unitarias de SQL Server como parte de una prueba de comprobación de la compilación (BVT). Puede configurar las pruebas unitarias para implementar la base de datos, generar datos de prueba y ejecutar las pruebas seleccionadas. Si no está familiarizado con Team Foundation Build, debe revisar la siguiente información antes de seguir los procedimientos de este tema:  
  
-   [Crear y definir pruebas unitarias de SQL Server](../ssdt/creating-and-defining-sql-server-unit-tests.md)  
  
-   [Cómo: Configurar y ejecutar pruebas programadas después de compilar la aplicación](https://msdn.microsoft.com/library/ms182465(VS.100).aspx)  
  
-   [Crear una definición de compilación básica](https://msdn.microsoft.com/library/ms181716(VS.100).aspx)  
  
Para usar estos procedimientos, primero debe configurar el entorno de trabajo realizando las siguientes tareas:  
  
-   Instalar Team Foundation Build y el control de versiones de Team Foundation. Probablemente tenga que instalar Team Foundation Build y el control de versiones de Team Foundation en distintos equipos.  
  
-   Instalar las utilidades de compilación de MicrosoftSQL Server Data en el mismo equipo que Team Foundation Build. Para instalar las utilidades de compilación de SQL Server Data Tools, realice primero un punto de instalación administrativa. Para más información sobre un punto de instalación administrativa, consulte [Instalar SQL Server Data Tools](../ssdt/install-sql-server-data-tools.md). Después, instale SSDTBuildUtilties.msi en el servidor de compilación desde la ubicación (/location) empleada para el punto de instalación administrativa.  
  
-   Conéctese a una instancia de Visual Studio Team Foundation Server.  
  
Después de configurar el entorno de trabajo, debe seguir estos pasos:  
  
1.  Cree un proyecto de base de datos.  
  
2.  Importe o cree el esquema y los objetos del proyecto de base de datos.  
  
3.  Configure las propiedades del proyecto de base de datos para la compilación y la implementación.  
  
4.  Cree una o varias pruebas unitarias.  
  
5.  Agregue la solución que contiene el proyecto de base de datos y el proyecto de prueba unitaria al control de versiones y proteja todos los archivos.  
  
Los procedimientos de este tema explican cómo crear una definición de compilación para ejecutar las pruebas unitarias como parte de una ejecución de pruebas automatizada:  
  
1.  [Configurar los valores de prueba para ejecutar las pruebas unitarias de base de datos en un agente de compilación x64](#ConfigureX64)  
  
2.  [Asignar pruebas a una categoría de prueba (opcional)](#CreateATestList)  
  
3.  [Modificar el proyecto de prueba](#ModifyTestProject)  
  
4.  [Proteger la solución](#CheckInTheTestList)  
  
5.  [Crear una definición de compilación](#CreateBuildDef)  
  
6.  [Ejecutar la nueva definición de compilación](#RunBuild)  
  
**Ejecutar pruebas unitarias de SQL Server en un equipo de compilación**  
  
Cuando ejecute pruebas unitarias en un equipo de compilación, puede que las pruebas unitarias no encuentren los archivos de proyecto de base de datos (.sqlproj). Este problema aparece porque el archivo app.config hace referencias a esos archivos mediante rutas de acceso relativas. Además, las pruebas unitarias podrían producir un error si no pueden encontrar la instancia de SQL Server que desea usar para ejecutar las pruebas unitarias. Este problema puede aparecer si las cadenas de conexión almacenadas en el archivo app.config no son válidas en el equipo de compilación.  
  
Para resolver estos problemas, debe especificar una sección de invalidación en el archivo app.config que reemplace app.config por un archivo de configuración que sea específico del entorno de Team Foundation Build. Para más información, consulte [Modificar el proyecto de prueba](#ModifyTestProject), más adelante en este tema.  
  
## <a name="ConfigureX64"></a>Configurar las pruebas para ejecutar pruebas unitarias de SQL Server en un agente de compilación x64  
Para poder ejecutar las pruebas unitarias en un agente de compilación x64, debe configurar las pruebas para cambiar la plataforma de proceso host.  
  
#### <a name="to-specify-the-host-process-platform"></a>Para especificar la plataforma de proceso de host  
  
1.  Abra la solución que contiene el proyecto de prueba cuyos valores desea configurar.  
  
2.  En el **Explorador de soluciones**, en la carpeta **Elementos de la solución**, haga doble clic en el archivo **Local.testsettings**.  
  
    Se muestra el cuadro de diálogo **Configuración de pruebas**.  
  
3.  En la lista, haga clic en **Hosts**.  
  
4.  En el panel de detalles, en **Plataforma de proceso de host**, haga clic en **MSIL** para configurar las pruebas que se van a ejecutar en un agente de compilación x64.  
  
5.  Haga clic en **Aplicar**.  
  
## <a name="CreateATestList"></a>Asignar pruebas a una categoría de prueba (opcional)  
Normalmente, cuando se crea una definición de compilación para ejecutar pruebas unitarias, se especifica una o varias categorías de prueba. Todas las pruebas de las categorías especificadas se ejecutan cuando se ejecuta la compilación.  
  
#### <a name="to-assign-tests-to-a-test-category"></a>Para asignar pruebas a una categoría de prueba  
  
1.  Abra la ventana **Vista de pruebas**.  
  
2.  Seleccione una prueba.  
  
3.  En el panel de propiedades, haga clic en **Categorías de prueba** y haga clic en los puntos suspensivos (...) en la columna de la derecha.  
  
4.  En la ventana **Categoría de prueba**, en el cuadro **Agregar nueva categoría**, escriba un nombre para la nueva categoría de prueba.  
  
5.  Haga clic en **Agregar** y, a continuación, en **Aceptar**.  
  
    La nueva categoría de prueba se asignará a la prueba y estará disponible para otras pruebas mediante sus propiedades.  
  
## <a name="ModifyTestProject"></a>Modificar el proyecto de prueba  
De forma predeterminada, Team Foundation Build crea un archivo de configuración a partir del archivo app.config del proyecto cuando compila el proyecto de pruebas unitarias. La ruta de acceso al proyecto de base de datos se almacena como ruta de acceso relativa en el archivo app.config. Las rutas de acceso relativas que funcionan en Visual Studio no funcionarán porque Team Foundation Build coloca los archivos compilados en ubicaciones diferentes con respecto al lugar donde se ejecutan las pruebas unitarias. Además, el archivo app.config contiene las cadenas de conexión que especifican la base de datos que desea probar. También necesita un archivo app.config independiente para Team Foundation Build si las pruebas unitarias deben conectarse a una base de datos diferente de la usada cuando se creó el proyecto de prueba. Al realizar modificaciones en el procedimiento siguiente, puede configurar el proyecto de prueba y el servidor de compilación de modo que Team Foundation Build use una configuración diferente.  
  
> [!IMPORTANT]  
> Debe realizar este procedimiento para cada proyecto de prueba (.vbproj o .vsproj).  
  
#### <a name="to-specify-an-appconfig-file-for-team-foundation-build"></a>Para especificar un archivo app.config de Team Foundation Build  
  
1.  En el **Explorador de soluciones**, haga clic con el botón derecho en el archivo app.config y haga clic en **Copiar**.  
  
2.  Haga clic con el botón derecho en el proyecto de prueba y haga clic en **Pegar**.  
  
3.  Haga clic con el botón derecho en el archivo denominado **Copia de app.config** y haga clic en Cambiar nombre.  
  
4.  Escriba _BuildComputer_**.sqlunitttest.config** y presione ENTRAR, donde *BuildComputer* es el nombre del equipo en el que se ejecuta el agente de compilación.  
  
5.  Haga doble clic en *BuildComputer*.sqlunitttest.config.  
  
    Se abrirá el archivo de configuración en el editor.  
  
6.  Cambie la ruta de acceso relativa al archivo .sqlproj agregando un nivel de carpeta para la carpeta Orígenes y una subcarpeta con el mismo nombre que la solución. Por ejemplo, si el archivo de configuración contiene inicialmente la entrada siguiente:  
  
    ```  
    <DatabaseDeployment DatabaseProjectFileName="..\..\..\Database3\Database3.sqlproj"      Configuration="Debug" />  
    ```  
  
    Actualice el archivo de la forma siguiente:  
  
    ```  
    <DatabaseDeployment DatabaseProjectFileName="..\..\..\Database3\Database3.sqlproj"      Configuration="Debug" />  
    ```  
  
    Cuando haya terminado, su archivo *BuildComputer*.sqlunitttest.config debe ser similar al siguiente ejemplo para Visual Studio 2010:  
  
    ```  
    <SqlUnitTesting_VS2010>  
        <DatabaseDeployment DatabaseProjectFileName="..\..\..\Database4\Database4.sqlproj"  
            Configuration="Debug" />  
        <DataGeneration ClearDatabase="true" />  
        <ExecutionContext Provider="System.Data.SqlClient" ConnectionString="Data Source=(localdb)\Projects;Initial Catalog=Database4;Integrated Security=True;Pooling=False"  
            CommandTimeout="30" />  
        <PrivilegedContext Provider="System.Data.SqlClient" ConnectionString="Data Source=(localdb)\Projects;Initial Catalog=Database4;Integrated Security=True;Pooling=False"  
            CommandTimeout="30" />  
    </SqlUnitTesting_VS2010>  
    ```  
  
    O bien, si utiliza Visual Studio 2012:  
  
    ```  
    <SqlUnitTesting_VS2012>  
            <DatabaseDeployment DatabaseProjectFileName="..\..\..\Database4\Database4.sqlproj"  
                Configuration="Debug" />  
            <DataGeneration ClearDatabase="true" />  
            <ExecutionContext Provider="System.Data.SqlClient" ConnectionString="Data Source=(localdb)\Projects;Initial Catalog=Database4;Integrated Security=True;Pooling=False"  
                CommandTimeout="30" />  
            <PrivilegedContext Provider="System.Data.SqlClient" ConnectionString="Data Source=(localdb)\Projects;Initial Catalog=Database4;Integrated Security=True;Pooling=False"  
                CommandTimeout="30" />  
        </SqlUnitTesting_VS2012>  
    ```  
  
7.  Actualice el atributo ConnectionString de ExecutionContext y PrivilegedContext para especificar las conexiones a la base de datos de destino en la que desea implementarlo.  
  
8.  En el menú **Archivo** , haga clic en **Guardar todo**.  
  
9. En el Explorador de soluciones, haga doble clic en app.config.  
  
10. En el editor, para cada nodo \<SqlUnitTesting_*VSVersion*>, agregue `AllowConfigurationOverride="true"`. Por ejemplo:  
  
    ```  
    -- Update SqlUnitTesting_VS2010 node to:  
    <SqlUnitTesting_VS2010 AllowConfigurationOverride="true">   
  
    -- Update SqlUnitTesting_VS2012 node to:  
    <SqlUnitTesting_VS2012 AllowConfigurationOverride="true">  
    ```  
  
    Al realizar este cambio, permitirá que Team Foundation Build use el archivo de configuración de reemplazo que ha creado.  
  
11. En el menú **Archivo** , haga clic en **Guardar todo**.  
  
    A continuación, debe actualizar Local.testsettings para incluir el archivo de configuración personalizado.  
  
#### <a name="to-customize-localtestsettings-to-deploy-the-customized-configuration-file"></a>Para personalizar Local.testsettings con el fin de implementar el archivo de configuración personalizado  
  
1.  En el Explorador de soluciones, haga doble clic en Local.testsettings.  
  
    Se muestra el cuadro de diálogo **Configuración de pruebas**.  
  
2.  En la lista de categorías, haga clic en **Implementación**.  
  
3.  Active la casilla de verificación **Habilitar implementación**.  
  
4.  Haga clic en **Agregar archivo**.  
  
5.  En el cuadro de diálogo **Agregar archivos de implementación**, especifique el archivo *BuildComputer*.sqlunitttest.config que ha creado.  
  
6.  Haga clic en **Aplicar**.  
  
7.  Haga clic en **Cerrar**.  
  
8.  En el menú **Archivo** , haga clic en **Guardar todo**.  
  
    A continuación, puede proteger la solución en el control de versiones.  
  
## <a name="CheckInTheTestList"></a>Proteger la solución  
En este procedimiento, va a proteger todos los archivos de la solución. Estos archivos incluyen el archivo de metadatos de prueba de la solución, que contiene las asociaciones y pruebas de la categoría de prueba. Cada vez que agregue, elimine, reorganice o cambie el contenido de las pruebas, el archivo de metadatos de prueba se actualizará automáticamente para reflejar estos cambios.  
  
> [!NOTE]  
> En este procedimiento se describen los pasos que debe seguir si usa el control de versiones de Team Foundation. Si usa otro software de control de versiones, debe seguir los pasos que sean adecuados para el software.  
  
#### <a name="to-check-in-the-solution"></a>Para proteger la solución  
  
1.  Conéctese a un equipo que ejecute Team Foundation Server.  
  
    Para más información, consulte [Usar el Explorador de control de código fuente](https://msdn.microsoft.com/library/ms181370(VS.100).aspx).  
  
2.  Si la solución no está ya en control de código fuente, agréguela.  
  
    Para más información, consulte [Agregar un proyecto o una solución al control de versiones](https://msdn.microsoft.com/library/ms181374(VS.100).aspx).  
  
3.  Haga clic en **Ver** y, a continuación, en **Protecciones pendientes**.  
  
4.  Proteja todos los archivos de la solución.  
  
    Para más información, consulte [Proteger cambios Pendientes](https://msdn.microsoft.com/library/ms181411(VS.100).aspx).  
  
    > [!NOTE]  
    > Puede tener un proceso específico del equipo que controle cómo se crean y se administran las pruebas automatizadas. Por ejemplo, el proceso puede requerir que compruebe localmente la compilación antes de proteger el código, así como las pruebas que se ejecutarán en él.  
  
    En el **Explorador de soluciones** aparecerá un icono de candado junto a cada archivo para indicar que está protegido. Para más información, consulte [Ver archivo de control de versiones y propiedades de la carpeta](https://msdn.microsoft.com/library/ms245468(VS.100).aspx).  
  
    Las pruebas están disponibles en Team Foundation Build. A continuación puede crear una definición de compilación que contenga las pruebas que desee ejecutar.  
  
## <a name="CreateBuildDef"></a>Crear una definición de compilación  
  
#### <a name="to-create-a-build-definition"></a>Para crear una definición de compilación  
  
1.  En Team Explorer, haga clic en el proyecto del equipo, haga clic con el botón derecho en el nodo **Compilaciones** y, a continuación, haga clic en **Nueva definición de compilación**.  
  
    Aparecerá la ventana **Nueva definición de compilación**.  
  
2.  En **Nombre de definición de compilación**, escriba el nombre que desea usar para la definición de compilación.  
  
3.  En la barra de navegación, haga clic en **Valores predeterminados de compilación**.  
  
4.  En **Copiar la salida de la compilación en la siguiente carpeta de entrega (ruta UNC, como \\\servidor\recurso compartido)**, especifique una carpeta que contenga la salida de la compilación.  
  
    Puede especificar una carpeta compartida en el equipo local o en cualquier ubicación de red en los que el proceso de compilación tenga permisos.  
  
5.  En la barra de navegación, haga clic en **Proceso**.  
  
6.  En el grupo **Requerido**, en **Elementos para compilar**, haga clic en el botón Examinar (…).  
  
7.  En el cuadro de diálogo **Editor de lista de proyectos de compilación**, haga clic en **Agregar**.  
  
8.  Especifique el archivo de solución (.sln) que ha agregado al control de versiones anteriormente en este tutorial y haga clic en **Aceptar**.  
  
    La solución aparece en la lista **Archivos de la solución o del proyecto que se van a compilar**.  
  
9. Haga clic en **Aceptar**.  
  
10. En el grupo **Básico**, en **Pruebas automatizadas**, especifique las pruebas que desea ejecutar. De manera predeterminada, se ejecutarán las pruebas que se encuentran en los archivos denominados *test\*.dll de la solución.  
  
11. En el menú **Archivo**, haga clic en **Guardar** *NombreDeProyecto*.  
  
    Ha creado una definición de compilación. A continuación, modifique el proyecto de prueba.  
  
## <a name="RunBuild"></a>Ejecutar la nueva definición de compilación  
  
#### <a name="to-run-the-new-build-type"></a>Para ejecutar el nuevo tipo de compilación  
  
1.  En Team Explorer, expanda el nodo de proyecto de equipo, expanda el nodo Compilaciones, haga clic con el botón secundario en la definición de compilación que desea ejecutar y, a continuación, haga clic en Poner nueva compilación en cola.  
  
    Se abrirá el cuadro de diálogo **Poner en cola compilación {**_NombreDelProyectoDeEquipo_**}** con una lista de todos los tipos de compilación existentes.  
  
2.  Si fuera necesario, en **Definición de compilación**, haga clic en la nueva definición de compilación.  
  
3.  Confirme que los valores de **Definición de compilación**, **Agente de compilación** y los campos de **Carpeta de entrega para esta compilación** son todos adecuados y haga clic en **Cola**.  
  
    Aparecerá la pestaña **Puesta en cola** del **Explorador de compilaciones**. Para más información, consulte [Administrar y ver compilaciones completadas (Visual Studio 2010)](https://msdn.microsoft.com/library/ms181730(VS.100).aspx) o [Administrar compilaciones en el Explorador de compilaciones (Visual Studio 2012)](https://msdn.microsoft.com/library/ms181732.aspx).  
  
## <a name="see-also"></a>Ver también  
[Ejecutar pruebas unitarias de SQL Server](../ssdt/running-sql-server-unit-tests.md)  
[Crear una definición de compilación básica](https://msdn.microsoft.com/library/ms181716(VS.100).aspx)  
[Poner en cola una compilación](https://msdn.microsoft.com/library/ms181722(VS.100).aspx)  
[Supervisar el progreso de una compilación en ejecución](https://msdn.microsoft.com/library/ms181724(VS.100).aspx)  
  
