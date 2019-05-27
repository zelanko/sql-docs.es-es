---
title: Derivaciones de flujo de datos | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: 2d847adf-4b3d-4949-a195-ef43de275077
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: a1938f2389f64d7a869ae924690b8b22fa209f82
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/23/2019
ms.locfileid: "66059904"
---
# <a name="data-flow-taps"></a>Derivaciones de flujo de datos
  [!INCLUDE[ssISCurrent](../includes/ssiscurrent-md.md)] presenta una nueva característica que le permite agregar una derivación de datos en la ruta de flujo de datos en tiempo de ejecución y dirigir la salida de la derivación de datos a un archivo externo. Para usar esta característica, debe implementar el proyecto de SSIS con el modelo de implementación de proyectos en un servidor de SSIS. Después de implementar el paquete en el servidor, debe ejecutar scripts T-SQL en la base de datos SSISDB para agregar derivaciones de datos antes de ejecutar el paquete. Este es un escenario de ejemplo:  
  
1.  Cree una instancia de ejecución de un paquete con el procedimiento almacenado [catalog.create_execution &#40;base de datos de SSISDB&#41;](/sql/integration-services/system-stored-procedures/catalog-create-execution-ssisdb-database).  
  
2.  Para agregar una derivación de datos, use el procedimiento almacenado [catalog.add_data_tap](/sql/integration-services/system-stored-procedures/catalog-add-data-tap) o [catalog.add_data_tap_by_guid](/sql/integration-services/system-stored-procedures/catalog-add-data-tap-by-guid).  
  
3.  Inicie la instancia de ejecución del paquete con [catalog.start_execution &#40;base de datos de SSISDB&#41;](/sql/integration-services/system-stored-procedures/catalog-start-execution-ssisdb-database).  
  
 Este es un script SQL de ejemplo que realiza los pasos descritos en el escenario anterior:  
  
```  
  
Declare @execid bigint  
EXEC [SSISDB].[catalog].[create_execution] @folder_name=N'ETL Folder', @project_name=N'ETL Project', @package_name=N'Package.dtsx', @execution_id=@execid OUTPUT  
EXEC [SSISDB].[catalog].add_data_tap @execution_id = @execid, @task_package_path = '\Package\Data Flow Task', @dataflow_path_id_string = 'Paths[Flat File Source.Flat File Source Output]', @data_filename = 'output.txt'  
EXEC [SSISDB].[catalog].[start_execution] @execid  
  
```  
  
 Los parámetros de nombre de carpeta, nombre de proyecto y nombre de paquete del procedimiento almacenado create_execution corresponden a los nombres de carpeta, proyecto y paquete del catálogo de Integration Services. Puede obtener los nombres de carpeta, proyecto y paquete que debe usar en la llamada a create_execution desde SQL Server Management Studio, como se muestra en la ilustración siguiente. Si no ve el proyecto de SSIS aquí, quizás no haya implementado todavía el proyecto en el servidor de SSIS. Haga clic con el botón secundario en el proyecto de SSIS en Visual Studio y, a continuación, haga clic en Implementar para implementar el proyecto en el servidor de SSIS esperado.  
  
 En lugar de escribir instrucciones SQL, puede generar el script de ejecución de paquetes mediante los pasos siguientes:  
  
1.  Haga clic con el botón derecho en **Package.dtsx** y, después, haga clic en **Ejecutar**.  
  
2.  Haga clic en el botón **Script** de la barra de herramientas para generar el script.  
  
3.  Ahora, agregue la instrucción add_data_tap antes de la llamada a start_execution.  
  
 El parámetro task_package_path del procedimiento almacenado add_data_tap corresponde a la propiedad PackagePath de la tarea de flujo de datos en Visual Studio. En Visual Studio, haga clic con el botón derecho en **Tarea Flujo de datos**y, después, haga clic en **Propiedades** para abrir la ventana Propiedades.  Anote el valor de la propiedad **PackagePath** para usarlo como valor para el parámetro task_package_path en la llamada al procedimiento almacenado add_data_tap.  
  
 El parámetro dataflow_path_id_string del procedimiento almacenado add_data_tap corresponde a la propiedad IdentificationString de la ruta de flujo de datos a la que desea agregar una derivación de datos. Para obtener dataflow_path_id_string, haga clic en la ruta de flujo de datos (flecha entre las tareas del flujo de datos) y anote el valor de la propiedad **IdentificationString** de la ventana Propiedades.  
  
 Cuando se ejecuta el script, el archivo de salida se almacena en \<Archivos de programa>\Microsoft SQL Server\110\DTS\DataDumps. Si ya existe un archivo con ese nombre, se crea un archivo nuevo con un sufijo (por ejemplo: output[1].txt).  
  
 Como se ha indicado anteriormente, también puede usar el procedimiento almacenado [catalog.add_data_tap_by_guid](/sql/integration-services/system-stored-procedures/catalog-add-data-tap-by-guid), en lugar de usar el procedimiento almacenado add_data_tap. Este procedimiento almacenado toma como parámetro el identificador de la tarea Flujo de datos en lugar de task_package_path. Puede obtener el identificador de la tarea Flujo de datos de la ventana Propiedades en Visual Studio.  
  
## <a name="removing-a-data-tap"></a>Quitar una derivación de datos  
 Puede quitar una derivación de datos antes de iniciar la ejecución con el procedimiento almacenado [catalog.remove_data_tap](/sql/integration-services/system-stored-procedures/catalog-remove-data-tap) . Este procedimiento almacenado toma como parámetro el identificador de la derivación de datos, que puede obtener como resultado del procedimiento almacenado add_data_tap.  
  
```  
  
DECLARE @tap_id bigint  
EXEC [SSISDB].[catalog].add_data_tap @execution_id = @execid, @task_package_path = '\Package\Data Flow Task', @dataflow_path_id_string = 'Paths[Flat File Source.Flat File Source Output]', @data_filename = 'output.txt' @data_tap_id=@tap_id OUTPUT  
EXEC [SSISDB].[catalog].remove_data_tap @tap_id  
  
```  
  
## <a name="listing-all-data-taps"></a>Mostrar todas las derivaciones de datos  
 También puede enumerar todas las derivaciones de datos mediante la vista catalog.execution_data_taps. En el ejemplo siguiente se extraen derivaciones de datos para una instancia de ejecución de especificación (Id.: 54).  
  
```  
select * from [SSISDB].[catalog].execution_data_taps where execution_id=@execid  
```  
  
## <a name="performance-consideration"></a>Consideraciones sobre el rendimiento  
 Al habilitar el nivel de registro detallado y agregar derivaciones de datos aumentan las operaciones de E/S que realiza la solución de integración de datos. Por tanto, se recomienda agregar derivaciones de datos solo para solucionar problemas.  
  
## <a name="video"></a>Vídeo  
 En este [vídeo de TechNet](https://technet.microsoft.com/sqlserver/dn600163) se muestra cómo agregar y usar derivaciones de datos en el catálogo de SSISDB de SQL Server 2012, que permiten depurar paquetes mediante programación y capturar los resultados parciales en tiempo de ejecución. También explica cómo enumerar o quitar estas derivaciones de datos y las prácticas recomendadas para usar derivaciones de datos en paquetes de SSIS.  
  
## <a name="related-tasks"></a>Related Tasks  
 [Depurar el flujo de datos](troubleshooting/debugging-data-flow.md)  
  
 [Herramientas para solucionar problemas de la ejecución de paquetes](troubleshooting/troubleshooting-tools-for-package-execution.md)  
  
  
