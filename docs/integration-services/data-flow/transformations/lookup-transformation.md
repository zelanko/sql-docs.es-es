---
title: "Transformación búsqueda | Documentos de Microsoft"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: data-flow
ms.reviewer: 
ms.suite: sql
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.dts.designer.lookuptrans.f1
- sql13.dts.designer.lookuptransformation.general.f1
- sql13.dts.designer.lookuptransformation.referencetable.f1
- sql13.dts.designer.lookuptransformation.columns.f1
- sql13.dts.designer.lookuptransformation.advanced.f1
helpviewer_keywords:
- Lookup transformation
- joining columns [Integration Services]
- cache [Integration Services]
- match exactly [Integration Services]
- lookups [Integration Services]
- exact matches [Integration Services]
ms.assetid: de1cc8de-e7af-4727-b5a5-a1f0a739aa09
caps.latest.revision: 106
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 4b557efa62075f7b88e6b70cf5950546444b95d8
ms.openlocfilehash: ee0c7e667e933c98bdbc228244a9dea1cf2c9bdd
ms.contentlocale: es-es
ms.lasthandoff: 08/19/2017

---
# <a name="lookup-transformation"></a>Transformación Búsqueda
  La transformación Búsqueda realiza búsquedas mediante la combinación de datos de columnas de entrada con columnas de un conjunto de datos de referencia. La búsqueda se utiliza para tener acceso a información adicional en una tabla relacionada que está basada en valores de columnas comunes.  
  
 El conjunto de datos de referencia puede ser un archivo caché, una tabla o una vista existente, una tabla nueva o el resultado de una consulta SQL. La transformación Búsqueda utiliza un administrador de conexiones OLE DB o un administrador de conexiones de caché para conectar con el conjunto de datos de referencia. Para obtener más información, vea [OLE DB Connection Manager](../../../integration-services/connection-manager/ole-db-connection-manager.md) y [Cache Connection Manager](../../../integration-services/data-flow/transformations/cache-connection-manager.md).  
  
 Puede configurar la transformación Búsqueda de las siguientes maneras:  
  
-   Seleccionar el administrador de conexiones que desea utilizar. Si desea conectarse a una base de datos, seleccione un administrador de conexiones OLE DB. Si desea conectarse a un archivo caché, seleccione un administrador de conexiones de caché.  
  
-   Especificar la tabla o vista que contiene el conjunto de datos de referencia.  
  
-   Generar una base de datos de referencia al especificar una instrucción SQL.  
  
-   Especificar las combinaciones entre los datos de entrada y el conjunto de datos de referencia.  
  
-   Agregar columnas del conjunto de datos de referencia a la salida de transformación Búsqueda.  
  
-   Configurar las opciones de almacenamiento en caché.  
  
 La transformación Búsqueda admite los siguientes proveedores de bases de datos para el administrador de conexiones OLE DB:  
  
-   [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]  
  
-   Oracle  
  
-   DB2  
  
 La transformación Búsqueda intenta realizar una combinación de igualdad entre valores de la entrada de la transformación y valores del conjunto de datos de referencia. Una combinación de igualdad quiere decir que cada fila de la entrada de transformación debe coincidir con, al menos, una fila del conjunto de datos de referencia. Si una combinación de no es posible, la transformación Búsqueda realiza una de las siguientes acciones:  
  
-   Si no hay ninguna entrada correspondiente en el conjunto de datos de referencia, no se produce ninguna combinación. De forma predeterminada, la transformación Búsqueda trata como errores las filas sin entradas coincidentes. Sin embargo, la transformación Búsqueda se puede configurar para redirigir dichas filas a un resultado no coincidente.  
  
-   Si hay varias coincidencias en la tabla de referencia, la transformación Búsqueda devuelve solo la primera coincidencia devuelta por la consulta de búsqueda. Si se encuentran varias coincidencias, la transformación Búsqueda genera un error o advertencia solo cuando la transformación se ha configurado para cargar todo el conjunto de datos de referencia en la memoria caché. En este caso, la transformación Búsqueda genera una advertencia cuando detecta varias coincidencias mientras la transformación llena la memoria caché.  
  
 La combinación puede ser compuesta, lo que indica que pueden combinarse varias columnas de la entrada de transformación con columnas del conjunto de datos de referencia. La transformación admite la combinación de columnas con cualquier tipo de datos, a excepción de DT_R4, DT_R8, DT_TEXT, DT_NTEXT o DT_IMAGE. Para más información, consulte [Integration Services Data Types](../../../integration-services/data-flow/integration-services-data-types.md).  
  
 Normalmente, los valores del conjunto de datos de referencia se agregan a la salida de transformación. Por ejemplo, la transformación Búsqueda puede extraer un nombre de producto de una tabla mediante un valor de una columna de entrada y, después, agregar el nombre del producto a la salida de transformación. Los valores de la tabla de referencia pueden reemplazar valores de columnas o agregarse a nuevas columnas.  
  
 Las búsquedas realizadas por la transformación Búsqueda distinguen mayúsculas de minúsculas. Para evitar errores de búsqueda producidos por diferencias entre mayúsculas y minúsculas en los datos, utilice primero la transformación Mapa de caracteres para convertir los datos en mayúsculas o minúsculas. A continuación, incluya las funciones UPPER o LOWER en la instrucción SQL que genera la tabla de referencia. Para más información, vea [Transformación Mapa de caracteres](../../../integration-services/data-flow/transformations/character-map-transformation.md), [UPPER &#40;Transact-SQL&#41;](../../../t-sql/functions/upper-transact-sql.md) y [LOWER &#40;Transact-SQL&#41;](../../../t-sql/functions/lower-transact-sql.md).  
  
 La transformación Búsqueda tiene las entradas y resultados siguientes:  
  
-   Entrada.  
  
-   Resultado coincidente. El resultado coincidente administra las filas de la entrada de transformación que coinciden como mínimo con una entrada del conjunto de datos de referencia.  
  
-   Resultado no coincidente. El resultado no coincidente administra las filas de la entrada que no coinciden como mínimo con una entrada del conjunto de datos de referencia. Si configura la transformación Búsqueda para que trate como errores las filas sin entradas coincidentes, las filas se redirigirán a la salida de errores. En los demás casos, la transformación redirigiría dichas filas al resultado no coincidente.  
  
-   Resultado de errores  
  
## <a name="caching-the-reference-dataset"></a>Almacenar en caché el conjunto de datos de referencia  
 Una caché en memoria almacena el conjunto de datos de referencia y una tabla hash que indiza los datos. La memoria caché permanece en la memoria hasta que se completa la ejecución del paquete. Puede guardar la memoria caché en un archivo caché (.caw).  
  
 Al conservar la memoria caché en un archivo, el sistema la carga con más rapidez. De esta forma, se mejora el rendimiento de la transformación Búsqueda y del paquete. Recuerde que cuando utiliza un archivo caché, está trabajando con datos que no están tan actualizados como los de la base de datos.  
  
 A continuación se describen otras ventajas relacionadas con guardar la memoria caché en un archivo:  
  
-   ***El archivo caché se puede compartir entre varios paquetes. Para más información, vea***   [Implementar una transformación de búsqueda en el modo de caché completa mediante el Administrador de conexiones de caché](../../../integration-services/data-flow/transformations/lookup-transformation-full-cache-mode-cache-connection-manager.md)  ***.***  
  
-   El archivo caché se puede implementar con un paquete. ***De esta forma, podrá utilizar los datos en varios equipos.*** Para obtener información, vea [Cómo crear e implementar una memoria caché para la transformación Búsqueda](../../../integration-services/data-flow/transformations/create-and-deploy-a-cache-for-the-lookup-transformation.md).  
  
-   Usar el origen de archivo sin formato para leer datos del archivo caché. A continuación, puede utilizar otros componentes de flujo de datos para transformar o mover los datos. Para más información, consulte [Raw File Source](../../../integration-services/data-flow/raw-file-source.md).  
  
    > [!NOTE]  
    >  El administrador de conexiones de caché no admite archivos caché creados o modificados mediante el destino de archivo sin formato.  
  
-   Puede llevar a cabo operaciones y atributos de conjunto en el archivo caché utilizando la tarea Sistema de archivos. Para obtener más información, vea [File System Task](../../../integration-services/control-flow/file-system-task.md).  
  
 A continuación se enumeran las opciones de almacenamiento en caché:  
  
-   El conjunto de datos de referencia se genera mediante una tabla, vista o consulta SQL y se carga en la memoria caché antes de que se ejecute la transformación Búsqueda. Puede usar el administrador de conexiones OLE DB para tener acceso al conjunto de datos.  
  
     Esta opción de almacenamiento en caché es compatible con la opción de almacenamiento en caché completa disponible para la transformación Búsqueda en [!INCLUDE[ssISversion2005](../../../includes/ssisversion2005-md.md)].  
  
-   El conjunto de datos de referencia se genera a partir de un origen de datos conectado al flujo de datos o de un archivo caché, y se carga en la memoria caché antes de que se ejecute la transformación Búsqueda. Para tener acceso al conjunto de datos puede usar el administrador de conexiones de caché o la transformación Caché. Para obtener más información, consulte [Cache Connection Manager](../../../integration-services/data-flow/transformations/cache-connection-manager.md) y [Cache Transform](../../../integration-services/data-flow/transformations/cache-transform.md).  
  
-   El conjunto de datos de referencia se genera mediante una tabla, vista o consulta SQL durante la ejecución de la transformación Búsqueda. Las filas con entradas coincidentes en el conjunto de datos de referencia y las que no tienen entradas coincidentes se cargan en la memoria caché.  
  
     Cuando se supera el tamaño de la memoria caché, la transformación Búsqueda quita automáticamente de la memoria caché las filas utilizadas con menor frecuencia.  
  
     Esta opción de almacenamiento en caché es compatible con la opción de almacenamiento en caché parcial disponible para la transformación Búsqueda en [!INCLUDE[ssISversion2005](../../../includes/ssisversion2005-md.md)].  
  
-   El conjunto de datos de referencia se genera mediante una tabla, vista o consulta SQL durante la ejecución de la transformación Búsqueda. No se almacenan datos en la memoria caché.  
  
     Esta opción de almacenamiento en caché es compatible con la opción sin almacenamiento en caché disponible para la transformación Búsqueda en [!INCLUDE[ssISversion2005](../../../includes/ssisversion2005-md.md)].  
  
 [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] y [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] difieren en el modo en que comparan cadenas. Si la transformación Búsqueda se configura para cargar el conjunto de datos de referencia en la memoria caché antes de que se ejecute la transformación Búsqueda, [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] lleva a cabo la comparación de búsqueda en la memoria caché. En caso contrario, la operación de búsqueda utiliza una instrucción SQL con parámetros y [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] realiza la comparación de búsqueda. Por lo tanto, es posible que la transformación Búsqueda devuelva un número de coincidencias diferentes a partir de la misma tabla de búsqueda, en función del tipo de caché.  
  
## <a name="related-tasks"></a>Tareas relacionadas  
 Puede establecer propiedades a través del Diseñador de [!INCLUDE[ssIS](../../../includes/ssis-md.md)] o mediante programación. Para obtener información detallada, vea los siguientes temas.  
  
-   [Implementar una búsqueda en modo No hay caché o Caché parcial](../../../integration-services/data-flow/transformations/implement-a-lookup-in-no-cache-or-partial-cache-mode.md)  
  
-   [Implementación de una transformación Búsqueda en el modo Caché completa con el Administrador de conexiones de caché](../../../integration-services/data-flow/transformations/lookup-transformation-full-cache-mode-cache-connection-manager.md)  
  
-   [Implementar una transformación Búsqueda en el modo de caché completa mediante el Administrador de conexiones OLE DB](../../../integration-services/data-flow/transformations/lookup-transformation-full-cache-mode-ole-db-connection-manager.md)  
  
-   [Establecer las propiedades de un componente de flujo de datos](../../../integration-services/data-flow/set-the-properties-of-a-data-flow-component.md)  
  
## <a name="related-content"></a>Contenido relacionado  
  
-   Vídeo, [Cómo implementar una transformación Búsqueda en modo de memoria caché completa (vídeo de SQL Server)](http://go.microsoft.com/fwlink/?LinkId=131031), en msdn.microsoft.com  
  
-   Entrada de blog, [Prácticas recomendadas para utilizar los modos de caché de la transformación Búsqueda](http://go.microsoft.com/fwlink/?LinkId=146623)(en inglés), en blogs.msdn.com  
  
-   Entrada de blog, [Patrón de búsqueda: sin distinción de mayúsculas y minúsculas](http://go.microsoft.com/fwlink/?LinkId=157782), en blogs.msdn.com  
  
-   Ejemplo, [Transformación de búsqueda](http://go.microsoft.com/fwlink/?LinkId=267528), en msftisprodsamples.codeplex.com.  
  
     Para obtener información acerca de cómo instalar muestras de producto y bases de datos de ejemplo de [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] , vea [Ejemplos del producto SQL Server Integration Services](http://go.microsoft.com/fwlink/?LinkId=267527).  
  
## <a name="lookup-transformation-editor-general-page"></a>Editor de transformación Búsqueda (página General)
  Utilice la página **General** del cuadro de diálogo Editor de transformación Búsqueda para seleccionar el modo de caché y el tipo de conexión, y especificar cómo administrar las filas sin entradas coincidentes.  
  
### <a name="options"></a>Opciones  
 **Caché completa**  
 Generey cargue el conjunto de datos de referencia en la caché antes de que se ejecute la transformación Búsqueda.  
  
 **Caché parcial**  
 Genere el conjunto de datos de referencia durante la ejecución de la transformación Búsqueda. Cargue en la caché las filas con entradas coincidentes del conjunto de datos de referencia y las que no tienen entradas coincidentes.  
  
 **Sin caché**  
 Genere el conjunto de datos de referencia durante la ejecución de la transformación Búsqueda. No se carga ningún dato en la caché.  
  
 **Administrador de conexiones de caché**  
 Configure la transformación Búsqueda para utilizar un administrador de conexiones de caché. Esta opción solo está disponible si también está seleccionada la opción Caché completa.  
  
 **OLE DB, administrador de conexiones**  
 Configure la transformación Búsqueda para utilizar un administrador de conexiones OLE DB.  
  
 **Especificar cómo administrar las filas sin entradas coincidentes**  
 Seleccione una opción para administrar las filas que no coincidan por lo menos con una entrada del conjunto de datos de referencia.  
  
 Al seleccionar **Redirigir filas a resultados no coincidentes**, las filas se redirigen a un resultado sin coincidencia y no se tratan como errores. La opción **Error** de la página **Salida de error** del cuadro de diálogo **Editor de transformación Búsqueda** no está disponible.  
  
 Al seleccionar cualquier otra opción del cuadro de lista **Especifique cómo administrar las filas sin entradas coincidentes** , las filas se tratan como errores. La opción **Error** de la página **Salida de error** está disponible.  
  
### <a name="external-resources"></a>Recursos externos  
 Entrada del blog, [Lookup cache modes](http://go.microsoft.com/fwlink/?LinkId=219518) en blogs.msdn.com  
  
## <a name="lookup-transformation-editor-connection-page"></a>Editor de transformación Búsqueda (página Conexión)
  Utilice la página **Conexión** del cuadro de diálogo **Editor de transformación Búsqueda** para seleccionar un administrador de conexiones. Si selecciona un administrador de conexiones OLE DB, también selecciona una consulta, tabla o vista para generar el conjunto de datos de referencia.  
  
### <a name="options"></a>Opciones  
 Las opciones siguientes están disponibles al seleccionar **Caché completa** y **Administrador de conexiones de caché** en la página General del cuadro de diálogo **Editor de transformación Búsqueda** .  
  
 **Administrador de conexiones de caché**  
 Seleccione un administrador de conexiones de caché de la lista o cree una conexión haciendo clic en **Nueva**.  
  
 **Nueva**  
 Cree una conexión mediante el cuadro de diálogo **Editor del administrador de conexiones de caché** .  
  
 Las opciones siguientes están disponibles al seleccionar **Caché completa**, **Caché parcial**o **Sin caché**, y **Administrador de conexiones OLE DB**en la página General del cuadro de diálogo **Editor de transformación Búsqueda** .  
  
 **Administrador de conexiones OLE DB**  
 Seleccione un administrador de conexiones OLE DB de la lista o cree una conexión haciendo clic en **Nueva**.  
  
 **Nueva**  
 Cree una conexión mediante el cuadro de diálogo **Configurar el administrador de conexiones OLE DB** .  
  
 **Usar una tabla o una vista**  
 Seleccione una tabla o vista de la lista o cree una tabla haciendo clic en **Nueva**.  
  
> [!NOTE]  
>  Si especifica una instrucción SQL en la página **Avanzadas** del **Editor de transformación Búsqueda**, esa instrucción SQL invalida y reemplaza el nombre de tabla seleccionado aquí. Para obtener más información, vea [Editor de transformación Búsqueda &#40;página Avanzadas&#41;](../../../integration-services/data-flow/transformations/lookup-transformation-editor-advanced-page.md).  
  
 **Nueva**  
 Cree una tabla mediante el cuadro de diálogo **Crear tabla** .  
  
 **Usar los resultados de una consulta SQL**  
 Elija esta opción para buscar una consulta preexistente, generar una consulta nueva, comprobar la sintaxis de consulta y obtener una vista previa de los resultados de la consulta.  
  
 **Generar consulta**  
 Cree la instrucción Transact-SQL para ejecutarla mediante el **Generador de consultas**, herramienta gráfica que se usa para crear consultas examinando datos.  
  
 **Examinar**  
 Utilice esta opción para examinar una consulta preexistente guardada como un archivo.  
  
 **Analizar consulta**  
 Compruebe la sintaxis de la consulta.  
  
 **Vista previa**  
 Obtenga una vista previa de los resultados mediante el cuadro de diálogo **Vista previa de los resultados de la consulta** . Esta opción muestra hasta 200 filas.  
  
### <a name="external-resources"></a>Recursos externos  
 Entrada del blog, [Lookup cache modes](http://go.microsoft.com/fwlink/?LinkId=219518) en blogs.msdn.com  
  
## <a name="lookup-transformation-editor-columns-page"></a>Editor de transformación Búsqueda (página Columnas)
  Use la página **Columnas** del cuadro de diálogo **Editor de transformación Búsqueda** para especificar la combinación entre la tabla de origen y la tabla de referencia, y para seleccionar columnas de búsqueda de la tabla de referencia.  
  
### <a name="options"></a>Opciones  
 **Columnas de entrada disponibles**  
 Muestra la lista de columnas de entrada disponibles. Las columnas de entrada son las columnas del flujo de datos de un origen conectado. Las columnas de entrada y la columna de búsqueda deben tener tipos de datos coincidentes.  
  
 Utilice una operación de arrastrar y colocar para asignar columnas de entrada disponibles a columnas de búsqueda.  
  
 También puede asignar columnas de entrada a columnas de búsqueda utilizando el teclado, resaltando una columna en la tabla **Columnas de entrada disponibles** , presionando la tecla de aplicación y haciendo clic en **Editar asignaciones**a continuación.  
  
 **Columnas de búsqueda disponibles**  
 Muestra la lista de columnas de búsqueda. Las columnas de búsqueda son columnas de la tabla de referencia en las que desea buscar valores que coinciden con las columnas de entrada.  
  
 Utilice una operación de arrastrar y colocar para asignar columnas de búsqueda disponibles a columnas de entrada.  
  
 Use las casillas para seleccionar las columnas de búsqueda de la tabla de referencia en las que se realizarán operaciones de búsqueda.  
  
 También puede asignar columnas de búsqueda a columnas de entrada utilizando el teclado, resaltando una columna en la tabla **Columnas de búsqueda disponibles** , presionando la tecla de aplicación y haciendo clic en **Editar asignaciones**a continuación.  
  
 **columna de búsqueda**  
 Muestra las columnas de búsqueda seleccionadas. Las selecciones se reflejan en las casillas activadas en la tabla **Columnas de búsqueda disponibles** .  
  
 **Operación de búsqueda**  
 Seleccione una operación de búsqueda de la lista para llevar a cabo en la columna de búsqueda.  
  
 **Alias de salida**  
 Escriba un alias para la salida de cada columna de búsqueda. El valor predeterminado es el nombre de la columna de búsqueda; no obstante, puede elegir un nombre descriptivo exclusivo.  
  
## <a name="lookup-transformation-editor-advanced-page"></a>Editor de transformación Búsqueda (página Avanzadas)
  Utilice la página **Avanzadas** del cuadro de diálogo **Editor de transformación Búsqueda** para configurar el almacenamiento parcial en caché y modificar la instrucción SQL para la transformación Búsqueda.  
  
### <a name="options"></a>Opciones  
 **Tamaño de caché (32 bits)**  
 Ajuste el tamaño de caché (en megabytes) para los equipos de 32 bits. El valor predeterminado es 5 megabytes.  
  
 **Tamaño de caché (64 bits)**  
 Ajuste el tamaño de caché (en megabytes) para los equipos de 64 bits. El valor predeterminado es 5 megabytes.  
  
 **Habilitar caché para filas sin entradas coincidentes**  
 Almacene en caché filas sin entradas coincidentes en el conjunto de datos de referencia.  
  
 **Asignación de caché**  
 Especifique el porcentaje de caché que se debe asignar a las filas sin entradas coincidentes en el conjunto de datos de referencia.  
  
 **Modificar la instrucción SQL**  
 Modifique la instrucción SQL que se utiliza para generar el conjunto de datos de referencia.  
  
> [!NOTE]  
>  La instrucción SQL opcional que se especifica en esta página invalida y reemplaza el nombre de tabla que se especificó en la página **Conexión** del **Editor de transformación Búsqueda**. Para más información, vea [Editor de transformación Búsqueda &#40;página Conexión&#41;](../../../integration-services/data-flow/transformations/lookup-transformation-editor-connection-page.md).  
  
 **Establecer parámetros**  
 Asigne columnas de entrada a parámetros mediante el cuadro de diálogo **Establecer parámetros de consulta** .  
  
### <a name="external-resources"></a>Recursos externos  
 Entrada del blog, [Lookup cache modes](http://go.microsoft.com/fwlink/?LinkId=219518) en blogs.msdn.com  
  
## <a name="see-also"></a>Vea también  
 [Transformación Búsqueda aproximada](../../../integration-services/data-flow/transformations/fuzzy-lookup-transformation.md)   
 [Transformación Búsqueda de términos](../../../integration-services/data-flow/transformations/term-lookup-transformation.md)   
 [Flujo de datos](../../../integration-services/data-flow/data-flow.md)   
 [Transformaciones de Integration Services](../../../integration-services/data-flow/transformations/integration-services-transformations.md)  
  
  

