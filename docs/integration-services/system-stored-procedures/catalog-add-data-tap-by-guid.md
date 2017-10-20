---
title: Catalog.add_data_tap_by_guid | Documentos de Microsoft
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: language-reference
ms.assetid: ed9d7fa3-61a1-4e21-ba43-1ead7dfc74eb
caps.latest.revision: 15
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 9bd4ecb4a6a419f1965a349d46d16d764dd83708
ms.contentlocale: es-es
ms.lasthandoff: 09/26/2017

---
# <a name="catalogadddatatapbyguid"></a>catalog.add_data_tap_by_guid
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  Agrega una derivación de datos a una ruta de acceso de flujo de datos específica de un flujo de datos de paquete, para una instancia de la ejecución.  
  
## <a name="syntax"></a>Sintaxis  
  
```sql  
add_data_tap_by_guid [ @execution_id = ] execution_id  
[ @dataflow_task_guid = ] dataflow_task_guid   
[ @dataflow_path_id_string = ] dataflow_path_id_string  
[ @data_filename = ] data_filename  
[ @max_rows = ] max_rows  
[ @data_tap_id = ] data_tap_id  
```  
  
## <a name="arguments"></a>Argumentos  
 [ @execution_id =] *execution_id*  
 Identificador de ejecución correspondiente a la ejecución que contiene el paquete. El *execution_id* es un **bigint**.  
  
 [ @dataflow_task_guid =] *dataflow_task_guid*  
 El identificador del flujo de tarea de datos del paquete que contiene la ruta de flujo de datos que se va a derivar. El *dataflow_task_guid* es un**uniqueidentifier**.  
  
 [ @dataflow_path_id_string =] *dataflow_path_id_string*  
 La cadena de identificación para la ruta de acceso de flujo de datos. Una ruta de acceso conecta dos componentes de flujo de datos. El **IdentificationString** propiedad para la ruta de acceso especifica la cadena.  
  
 Para buscar la cadena de identificación, en [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)] haga clic en la ruta de acceso entre componentes de flujo de datos de dos y, a continuación, haga clic en **propiedades**. El **IdentificationString** propiedad aparece en la **propiedades** ventana.  
  
 El *dataflow_path_id_string* es un **nvarchar (4000)**.  
  
 [ @data_filename =] *data_filename*  
 Nombre del archivo que almacena los datos derivados. Si la tarea Flujo de datos se ejecuta en un bucle Foreach o en un contenedor de bucles For, los datos derivados se almacenan en archivos diferentes para cada iteración del bucle. Cada archivo tiene como prefijo un número que corresponde a una iteración. Archivos de derivación de datos se escriben en la carpeta "*\<carpeta de instalación de SQL Server >*\130\DTS\\". El *data_filename* es un **nvarchar (4000)**.  
  
 [ @max_rows =] max_rows  
 Número de filas que se capturan durante la derivación de datos. Si no se especifica este valor, se capturan todas las filas. El valor max_rows es un **int**.  
  
 [ @data_tap_id =] *data_tap_id*  
 Identificador de la derivación de datos. El *data_tap_id* es un **bigint**.  
  
## <a name="example"></a>Ejemplo  
 En el ejemplo siguiente, se crea una derivación de datos en la ruta de acceso del flujo de datos, `Paths[SRC DimDCVentor.OLE DB Source Output]`, en el flujo de datos tarea `{D978A2E4-E05D-4374-9B05-50178A8817E8}`. Los datos derivados se almacenan en el archivo DCVendorOutput.csv.  
  
```  
exec catalog.add_data_tap_by_guid   @execution_id,   
'{D978A2E4-E05D-4374-9B05-50178A8817E8}',   
'Paths[SRC DimDCVentor.OLE DB Source Output]',   
'D:\demos\datafiles\DCVendorOutput.csv'  
  
```  
  
## <a name="remarks"></a>Comentarios  
 Para agregar derivaciones de datos, la instancia de la ejecución debe estar en estado creado (un valor de 1 en el **estado** columna de la [catalog.operations &#40; Base de datos SSISDB &#41; ](../../integration-services/system-views/catalog-operations-ssisdb-database.md)vista). El valor de estado cambia cuando se ejecuta la ejecución. Puede crear una ejecución mediante una llamada a [catalog.create_execution &#40; Base de datos SSISDB &#41; ](../../integration-services/system-stored-procedures/catalog-create-execution-ssisdb-database.md).  
  
 A continuación se indican algunas consideraciones sobre el procedimiento almacenado add_data_tap_by_guid.  
  
-   Al agregar una derivación de datos, esta no se valida antes de que se ejecute el paquete.  
  
-   Se recomienda que limite el número de filas que se capturan durante la derivación de datos para evitar que se generen archivos de datos grandes. Si el equipo en el que se ejecuta el procedimiento almacenado se queda sin espacio para almacenar los archivos de datos, se detiene la ejecución del procedimiento almacenado.  
  
-   La ejecución del procedimiento almacenado add_data_tap_by_guid afecta al rendimiento del paquete. Se recomienda que ejecute el procedimiento almacenado solo para solucionar problemas de datos.  
  
-   Para tener acceso al archivo que almacena los datos derivados, debe tener permisos de administrador en el equipo en el que se ejecuta el procedimiento almacenado o debe ser el usuario que inició la ejecución que contiene el paquete con la derivación de datos.  
  
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
  
## <a name="see-also"></a>Vea también  
 [catalog.add_data_tap](../../integration-services/system-stored-procedures/catalog-add-data-tap.md)  
  
  
