---
title: Catalog.add_data_tap | Documentos de Microsoft
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: language-reference
ms.assetid: a25ebcc7-535e-4619-adf6-4e2b5a62ba37
caps.latest.revision: 23
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 686b40e7e1ad7f7843bee5af3295fdf394538f63
ms.contentlocale: es-es
ms.lasthandoff: 09/26/2017

---
# <a name="catalogadddatatap"></a>catalog.add_data_tap
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  Agrega una derivación de datos en el resultado de un componente de un flujo de datos de paquete, para una instancia de la ejecución.  
  
## <a name="syntax"></a>Sintaxis  
  
```tsql  
add_data_tap [ @execution_id = ] execution_id  
[ @task_package_path = ] task_package_path  
[ @dataflow_path_id_string = ] dataflow_path_id_string  
[ @data_filename = ] data_filename  
[ @max_rows = ] max_rows  
[ @data_tap_id = ] data_tap_id  
OUTPUT  
```  
  
## <a name="arguments"></a>Argumentos  
 [ @execution_id =] *execution_id*  
 Identificador de ejecución correspondiente a la ejecución que contiene el paquete. El *execution_id* es un **bigint**.  
  
 [ @task_package_path =] *task_package_path*  
 Ruta de acceso del paquete para la tarea Flujo de datos. El **PackagePath** propiedad para la tarea de flujo de datos especifica la ruta de acceso. La ruta de acceso distingue mayúsculas de minúsculas. Para buscar la ruta de acceso de paquete, en [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)] haga clic en la tarea flujo de datos y, a continuación, haga clic en **propiedades**. El **PackagePath** propiedad aparece en la **propiedades** ventana.  
  
 El *task_package_path* es un **nvarchar (max)**.  
  
 [ @dataflow_path_id_string =] *dataflow_path_id_string*  
 La cadena de identificación para la ruta de acceso de flujo de datos. Una ruta de acceso conecta dos componentes de flujo de datos. El **IdentificationString** propiedad para la ruta de acceso especifica la cadena.  
  
 Para buscar la cadena de identificación, en [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)] haga clic en la ruta de acceso entre componentes de flujo de datos de dos y, a continuación, haga clic en **propiedades**. El **IdentificationString** propiedad aparece en la **propiedades** ventana.  
  
 El *dataflow_path_id_string* es un **nvarchar (4000)**.  
  
 [ @data_filename =] *data_filename*  
 Nombre del archivo que almacena los datos derivados. Si la tarea Flujo de datos se ejecuta en un bucle Foreach o en un contenedor de bucles For, los datos derivados se almacenan en archivos diferentes para cada iteración del bucle. Cada archivo tiene como prefijo un número que corresponde a una iteración.  
  
 De forma predeterminada, el archivo se almacena en la \< *unidad*>: \Program Server\130\DTS\DataDumps SQL carpeta.  
  
 El *data_filename* es un **nvarchar (4000)**.  
  
 [ @max_rows =] *max_rows*  
 Número de filas que se capturan durante la derivación de datos. Si no se especifica este valor, se capturan todas las filas. El *max_rows* es un **int**.  
  
 [ @data_tap_id =] *data_tap_id*  
 Devuelve el identificador de la derivación de datos. El *data_tap_id* es un **bigint**.  
  
## <a name="example"></a>Ejemplo  
 En el ejemplo siguiente, se crea una derivación de datos en la ruta de flujo de datos, `'Paths[OLE DB Source.OLE DB Source Output]`, en la tarea de flujo de datos, `\Package\Data Flow Task`. Los datos derivados se almacenan en la `output0.txt` archivo en la carpeta DataDumps (\<*unidad*>: \Program Server\130\DTS\DataDumps de SQL).  
  
```  
Declare @execution_id bigint  
Exec SSISDB.Catalog.create_execution @folder_name='Packages',@project_name='SSISPackages', @package_name='Package.dtsx',@reference_id=Null, @use32bitruntime=False, @execution_id=@execution_id OUTPUT  
  
Exec SSISDB.Catalog.set_execution_parameter_value @execution_id,50, 'LOGGING_LEVEL', 0  
  
Exec SSISDB.Catalog.add_data_tap @execution_id, @task_package_path='\Package\Data Flow Task', @dataflow_path_id_string = 'Paths[OLE DB Source.OLE DB Source Output]', @data_filename = 'output0.txt'  
  
Exec SSISDB.Catalog.start_execution @execution_id  
  
```  
  
## <a name="remarks"></a>Comentarios  
 Para agregar derivaciones de datos, la instancia de la ejecución debe estar en estado creado (un valor de 1 en el **estado** columna de la [catalog.operations &#40; Base de datos SSISDB &#41; ](../../integration-services/system-views/catalog-operations-ssisdb-database.md)vista). El valor de estado cambia cuando se ejecuta la ejecución. Puede crear una ejecución mediante una llamada a [catalog.create_execution &#40; Base de datos SSISDB &#41; ](../../integration-services/system-stored-procedures/catalog-create-execution-ssisdb-database.md).  
  
 A continuación se indican algunas consideraciones sobre el procedimiento almacenado add_data_tap.  
  
-   Si una ejecución contiene un paquete primario y uno o varios paquetes secundarios, necesita agregar una derivación de datos para cada paquete para el que desee derivar datos.  
  
-   Si un paquete contiene más de una tarea Flujo de datos con el mismo nombre, task_package_path identifica de forma única la tarea Flujo de datos que contiene la salida del componente derivado.  
  
-   Al agregar derivación de datos, no se valida antes de que se ejecuta el paquete.  
  
-   Se recomienda que limite el número de filas que se capturan durante la derivación de datos para evitar que se generen archivos de datos grandes. Si el equipo en el que se ejecuta el procedimiento almacenado se queda sin espacio de almacenamiento para los archivos de datos, el paquete deja de ejecutarse y se escribe un mensaje de error en el registro.  
  
-   La ejecución del procedimiento almacenado add_data_tap afecta al rendimiento del paquete. Se recomienda que ejecute el procedimiento almacenado solo para solucionar problemas de datos.  
  
-   Para tener acceso al archivo que almacena los datos derivados, debe ser administrador en el equipo en el que se ejecuta el procedimiento almacenado. También debe ser el usuario que inició la ejecución que contiene el paquete con la derivación de datos.  
  
## <a name="return-codes"></a>Códigos de retorno  
 0 (correcto)  
  
 Cuando se produce un error en el procedimiento almacenado, se genera un error.  
  
## <a name="result-set"></a>Conjunto de resultados  
 Ninguno  
  
## <a name="permissions"></a>Permissions  
 Este procedimiento almacenado necesita uno de los permisos siguientes:  
  
-   Permisos MODIFY en la instancia de ejecución  
  
-   La pertenencia a la **ssis_admin** rol de base de datos  
  
-   La pertenencia a la **sysadmin** rol de servidor  
  
## <a name="errors-and-warnings"></a>Errores y advertencias  
 En la lista siguiente se describen las condiciones que hacen que el procedimiento almacenado genere un error.  
  
-   El usuario no tiene permisos MODIFY.  
  
-   La derivación de datos para el componente especificado, en el paquete indicado, ya se ha agregado.  
  
-   El valor especificado para el número de filas para capturar no es válido.  
  
## <a name="requirements"></a>Requisitos  
  
## <a name="external-resources"></a>Recursos externos  
 Entrada de blog, [SSIS 2012: Peek A derivaciones de datos](http://go.microsoft.com/fwlink/?LinkId=239983), en rafael-salas.com.  
  
## <a name="see-also"></a>Vea también  
 [catalog.add_data_tap_by_guid](../../integration-services/system-stored-procedures/catalog-add-data-tap-by-guid.md)  
  
  
