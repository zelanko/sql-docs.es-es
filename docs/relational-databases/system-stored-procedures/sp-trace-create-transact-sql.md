---
title: sp_trace_create (Transact-SQL) | Documentos de Microsoft
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sp_trace_create_TSQL
- sp_trace_create
dev_langs:
- TSQL
helpviewer_keywords:
- sp_trace_create
ms.assetid: f3a43597-4c5a-4520-bcab-becdbbf81d2e
caps.latest.revision: 38
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 06588729794b9a5b62b82e0576f955536687f57e
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/04/2018
---
# <a name="sptracecreate-transact-sql"></a>sp_trace_create (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Crea una definición de seguimiento. El nuevo seguimiento estará en estado de detención.  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)] Use eventos extendidos en su lugar.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
sp_trace_create [ @traceid = ] trace_id OUTPUT   
          , [ @options = ] option_value   
          , [ @tracefile = ] 'trace_file'   
     [ , [ @maxfilesize = ] max_file_size ]  
     [ , [ @stoptime = ] 'stop_time' ]  
     [ , [ @filecount = ] 'max_rollover_files' ]  
```  
  
## <a name="arguments"></a>Argumentos  
 [  **@traceid=** ] *trace_id*  
 Es el número asignado por [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para el nuevo objeto trace. Se pasará por alto cualquier entrada proporcionada por el usuario. *trace_id* es **int**, su valor predeterminado es null. El usuario emplea el *trace_id* valor para identificar, modificar y controlar el seguimiento definido por este procedimiento almacenado.  
  
 [  **@options=** ] *option_value*  
 Especifica las opciones establecidas para el seguimiento. *option_value* es **int**, no tiene ningún valor predeterminado. Los usuarios pueden elegir una combinación de estas opciones especificando el valor de la suma de las opciones seleccionadas. Por ejemplo, para activar ambas opciones, TRACE_FILE_ROLLOVER y SHUTDOWN_ON_ERROR, especifique **6** para *option_value*.  
  
 En la tabla siguiente se muestran las opciones, las descripciones y sus valores.  
  
|Nombre de la opción|Valor de la opción|Description|  
|-----------------|------------------|-----------------|  
|TRACE_FILE_ROLLOVER|**2**|Especifica que, cuando la *max_file_size* se alcanza, actual se cierra el archivo de seguimiento y se crea un nuevo archivo. Todos los nuevos registros se escribirán en el archivo nuevo. El archivo nuevo tendrá el mismo nombre que el archivo anterior, pero se agregará un entero para indicar su secuencia. Por ejemplo, si el archivo de seguimiento original se llama FILENAME.TRC, siguiente archivo de seguimiento se llamará FILENAME_1.TRC, el siguiente archivo de seguimiento se llamará FILENAME_2.TRC, y así sucesivamente.<br /><br /> A medida que se creen más archivos de seguimiento de sustitución incremental, el valor entero agregado al nombre del archivo aumentará secuencialmente.<br /><br /> SQL Server utiliza el valor predeterminado de *max_file_size* (5 MB) si se especifica esta opción sin especificar un valor para *max_file_size*.|  
|SHUTDOWN_ON_ERROR|**4**|Especifica que, si por cualquier razón, no se puede escribir el seguimiento en el archivo, SQL Server se cerrará. Esta opción es muy útil cuando se realizan seguimientos de auditoría de seguridad.|  
|TRACE_PRODUCE_BLACKBOX|**8**|Especifica que el servidor guardará un registro de los últimos 5 MB de información de seguimiento producidos por el servidor. TRACE_PRODUCE_BLACKBOX es incompatible con las demás opciones.|  
  
 [  **@tracefile=** ] *'**trace_file**'*  
 Especifica la ubicación y el nombre de archivo en que se escribirá el seguimiento. *trace_file* es **nvarchar(245)** no tiene ningún valor predeterminado. *trace_file* puede ser un directorio local (como N 'C:\MSSQL\Trace\trace.trc') o una ruta UNC a un recurso compartido o una ruta de acceso (N'\\\\*Servername*\\*Sharename* \\ *Directorio*\trace.trc').  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] se anexará un **.trc** extensión a todos los nombres de archivo de seguimiento. Si la opción TRACE_FILE_ROLLOVER y *max_file_size* se especifican, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] crea un nuevo archivo de seguimiento cuando el archivo de seguimiento original alcanza su tamaño máximo. El nuevo archivo tiene el mismo nombre que el archivo original, pero _*n* se anexa para indicar su secuencia, a partir de **1**. Por ejemplo, si el primer archivo de seguimiento se denomina **nombreDeArchivo.trc**, el segundo archivo de seguimiento se denomina **filename_1.trc**.  
  
 Si usa la opción TRACE_FILE_ROLLOVER, no es recomendable que emplee caracteres de subrayado en el nombre de archivo de seguimiento original. Si usa caracteres de subrayado, puede producirse el siguiente comportamiento:  
  
-   [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] no carga automáticamente o le solicita que cargue los archivos de sustitución incremental (si alguna de estas opciones de sustitución incremental de archivos están configurado).  
  
-   La función fn_trace_gettable no carga archivos de sustitución incremental (cuando se especifica mediante el uso de la *number_files* argumento) donde el nombre de archivo original termina con un carácter de subrayado y un valor numérico. (Esto no se aplica al carácter de subrayado y al número que se anexan automáticamente cuando un archivo realiza la sustitución incremental).  
  
> [!NOTE]  
>  Para solucionar estos comportamientos, puede cambiar el nombre de los archivos de seguimiento y quitar los caracteres de subrayado del nombre de archivo original. Por ejemplo, si el archivo original se denomina **my_trace.trc**, y el archivo de sustitución incremental se denomina **my_trace_1.trc**, puede cambiar el nombre de los archivos a **mytrace.trc** y **mytrace_1.trc** antes de abrir los archivos en [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)].  
  
 *trace_file* no se puede especificar cuando se utiliza la opción TRACE_PRODUCE_BLACKBOX.  
  
 [  **@maxfilesize=** ] *max_file_size*  
 Especifica el tamaño máximo en megabytes (MB) que puede alcanzar un archivo de seguimiento. *max_file_size* es **bigint**, con un valor predeterminado de **5**.  
  
 Si se especifica este parámetro sin la opción TRACE_FILE_ROLLOVER, la traza detiene el registro en el archivo cuando el espacio en disco utilizado excede la cantidad especificada por *max_file_size*.  
  
 [  **@stoptime=** ] **'***stop_time***'**  
 Especifica la fecha y la hora de la detención del seguimiento. *stop_time* es **datetime**, su valor predeterminado es null. Si es NULL, el seguimiento se ejecuta hasta que se detiene de forma manual o bien hasta que se cierra el servidor.  
  
 Si ambos *stop_time* y *max_file_size* se especifican, y TRACE_FILE_ROLLOVER, no se especifica, el seguimiento se detiene cuando se alcanza la hora de detención especificada o el tamaño máximo de archivo. Si *stop_time*, *max_file_size*y se especifica TRACE_FILE_ROLLOVER, el seguimiento se detiene en la hora de detención especificada, suponiendo que el seguimiento no se llene la unidad.  
  
 [  **@filecount=** ] **'***max_rollover_files***'**  
 Especifica el número máximo de archivos de seguimiento que se pueden mantener con el mismo nombre de archivo base. *MAX_ROLLOVER_FILES* es **int**, mayor que uno. Este parámetro solo es válido si se especifica la opción TRACE_FILE_ROLLOVER. Cuando *max_rollover_files* se especifica, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] intenta mantener más de *max_rollover_files* archivos de seguimiento eliminando el archivo de seguimiento más antiguo antes de abrir un archivo de seguimiento. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] hace un seguimiento de la edad de los archivos de seguimiento agregando un número al nombre del archivo base.  
  
 Por ejemplo, cuando la *trace_file* parámetro se especifica como "c:\mytrace", un archivo con el nombre "c:\mytrace_123.trc" es anterior a un archivo con el nombre "c:\mytrace_124.trc". Si *max_rollover_files* está establecido en 2, SQL Server eliminará el archivo "c:\mytrace_123.trc" antes de crear el archivo de seguimiento "c:\mytrace_125.trc".  
  
 Observe que [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] solo intenta eliminar cada archivo una vez, y no puede eliminar un archivo que esté siendo utilizado en otro proceso. Por lo tanto, si otra aplicación está utilizando archivos de seguimiento mientras se ejecuta el seguimiento, puede que [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] deje estos archivos de seguimiento en el sistema de archivos.  
  
## <a name="return-code-values"></a>Valores de código de retorno  
 En la tabla siguiente se describen los valores del código que los usuarios pueden obtener después de completar el procedimiento almacenado.  
  
|Código de retorno|Description|  
|-----------------|-----------------|  
|0|Ningún error.|  
|1|Error desconocido.|  
|10|Opciones no válidas. Se devuelve cuando las opciones especificadas no son compatibles.|  
|12|Archivo no creado.|  
|13|Memoria insuficiente. Se devuelve cuando no hay memoria suficiente para realizar la acción especificada.|  
|14|Hora de detención no válida. Se devuelve cuando ya se ha alcanzado la hora de detención especificada.|  
|15|Parámetros no válidos. Se devuelve cuando el usuario ha proporcionado parámetros no compatibles.|  
  
## <a name="remarks"></a>Comentarios  
 **sp_trace_create** es un [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] procedimiento almacenado que realiza muchas de las acciones ejecutadas previamente por **xp_trace_\***  disponibles en versiones anteriores de SQL Server de procedimientos almacenados extendidos. Use **sp_trace_create** en lugar de:  
  
-   **xp_trace_addnewqueue**  
  
-   **xp_trace_setqueuecreateinfo**  
  
-   **xp_trace_setqueuedestination**  
  
 **sp_trace_create** solo crea una definición de seguimiento. Este procedimiento almacenado no se puede utilizar para iniciar o cambiar un seguimiento.  
  
 Parámetros de seguimiento de SQL todos los procedimientos almacenados (**sp_trace_xx**) deben escribirse. Si no se llama a estos parámetros con los tipos de datos de parámetros de entrada correctos, según se especifica en la descripción del argumento, el procedimiento almacenado devolverá un error.  
  
 Para **sp_trace_create**, la [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] cuenta de servicio debe tener permiso de escritura en la carpeta de archivos de seguimiento. Si la cuenta del servicio [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] no es administrador en el equipo donde se encuentra el archivo de seguimiento, debe conceder explícitamente permiso de escritura a la cuenta del servicio [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
> [!NOTE]  
>  Puede cargar automáticamente el archivo de seguimiento creado con **sp_trace_create** en una tabla utilizando la **fn_trace_gettable** función del sistema. Para obtener información sobre cómo usar esta función del sistema, consulte [sys.fn_trace_gettable &#40;Transact-SQL&#41;](../../relational-databases/system-functions/sys-fn-trace-gettable-transact-sql.md).  
  
 Para obtener un ejemplo de cómo usar los procedimientos almacenados de seguimiento, vea [Crear un seguimiento &#40;Transact-SQL&#41;](../../relational-databases/sql-trace/create-a-trace-transact-sql.md).  
  
 **TRACE_PRODUCE_BLACKBOX** tiene las siguientes características:  
  
-   Es un seguimiento de sustitución incremental. El valor predeterminado *file_count* es 2 pero puede reemplazarse por el usuario mediante *filecount* opción.  
  
-   El valor predeterminado *file_size* tal y como en otros seguimientos es 5 MB y se puede cambiar.  
  
-   No se puede especificar ningún nombre de archivo. El archivo se guardará como: **N'%SQLDIR%\MSSQL\DATA\blackbox.trc'**  
  
-   Solo los eventos siguientes y sus columnas están contenidos en el seguimiento:  
  
    -   **A partir de RPC**  
  
    -   **A partir de lote**  
  
    -   **(Excepción)**  
  
    -   **Atención**  
  
-   Los eventos o columnas no se pueden agregar o quitar de este seguimiento.  
  
-   No se pueden especificar filtros para este seguimiento.  
  
## <a name="permissions"></a>Permissions  
 El usuario debe tener permiso ALTER TRACE.  
  
## <a name="see-also"></a>Vea también  
 [sp_trace_generateevent &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-trace-generateevent-transact-sql.md)   
 [sp_trace_setevent &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-trace-setevent-transact-sql.md)   
 [sp_trace_setfilter &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-trace-setfilter-transact-sql.md)   
 [sp_trace_setstatus &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-trace-setstatus-transact-sql.md)   
 [Seguimiento de SQL](../../relational-databases/sql-trace/sql-trace.md)  
  
  
