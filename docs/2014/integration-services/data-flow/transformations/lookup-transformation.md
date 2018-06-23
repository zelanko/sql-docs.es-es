---
title: Transformación Búsqueda | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- sql12.dts.designer.lookuptrans.f1
helpviewer_keywords:
- Lookup transformation
- joining columns [Integration Services]
- cache [Integration Services]
- match exactly [Integration Services]
- lookups [Integration Services]
- exact matches [Integration Services]
ms.assetid: de1cc8de-e7af-4727-b5a5-a1f0a739aa09
caps.latest.revision: 104
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.openlocfilehash: f7a4d4a05d738ee844b6eb63ab5c762fb84f6194
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36111201"
---
# <a name="lookup-transformation"></a>Transformación de búsqueda
  La transformación Búsqueda realiza búsquedas mediante la combinación de datos de columnas de entrada con columnas de un conjunto de datos de referencia. La búsqueda se utiliza para tener acceso a información adicional en una tabla relacionada que está basada en valores de columnas comunes.  
  
 El conjunto de datos de referencia puede ser un archivo caché, una tabla o una vista existente, una tabla nueva o el resultado de una consulta SQL. La transformación Búsqueda utiliza un administrador de conexiones OLE DB o un administrador de conexiones de caché para conectar con el conjunto de datos de referencia. Para obtener más información, vea [OLE DB Connection Manager](../../connection-manager/ole-db-connection-manager.md) y [Cache Connection Manager](../../connection-manager/cache-connection-manager.md).  
  
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
  
-   Si no hay ninguna entrada correspondiente en el conjunto de datos de referencia, no se produce ninguna combinación. De forma predeterminada, la transformación Búsqueda trata como errores las filas sin entradas coincidentes. Sin embargo, la transformación Búsqueda se puede configurar para redirigir dichas filas a un resultado no coincidente. Para más información, vea [Editor de transformación Búsqueda &#40;página General&#41;](../../lookup-transformation-editor-general-page.md) y [Editor de transformación Búsqueda &#40;página Salida de error&#41;](../../lookup-transformation-editor-error-output-page.md).  
  
-   Si hay varias coincidencias en la tabla de referencia, la transformación Búsqueda devuelve solo la primera coincidencia devuelta por la consulta de búsqueda. Si se encuentran varias coincidencias, la transformación Búsqueda genera un error o advertencia solo cuando la transformación se ha configurado para cargar todo el conjunto de datos de referencia en la memoria caché. En este caso, la transformación Búsqueda genera una advertencia cuando detecta varias coincidencias mientras la transformación llena la memoria caché.  
  
 La combinación puede ser compuesta, lo que indica que pueden combinarse varias columnas de la entrada de transformación con columnas del conjunto de datos de referencia. La transformación admite la combinación de columnas con cualquier tipo de datos, a excepción de DT_R4, DT_R8, DT_TEXT, DT_NTEXT o DT_IMAGE. Para más información, consulte [Integration Services Data Types](../integration-services-data-types.md).  
  
 Normalmente, los valores del conjunto de datos de referencia se agregan a la salida de transformación. Por ejemplo, la transformación Búsqueda puede extraer un nombre de producto de una tabla mediante un valor de una columna de entrada y, después, agregar el nombre del producto a la salida de transformación. Los valores de la tabla de referencia pueden reemplazar valores de columnas o agregarse a nuevas columnas.  
  
 Las búsquedas realizadas por la transformación Búsqueda distinguen mayúsculas de minúsculas. Para evitar errores de búsqueda producidos por diferencias entre mayúsculas y minúsculas en los datos, utilice primero la transformación Mapa de caracteres para convertir los datos en mayúsculas o minúsculas. A continuación, incluya las funciones UPPER o LOWER en la instrucción SQL que genera la tabla de referencia. Para más información, vea [Transformación Mapa de caracteres](character-map-transformation.md), [UPPER &#40;Transact-SQL&#41;](/sql/t-sql/functions/upper-transact-sql) y [LOWER &#40;Transact-SQL&#41;](/sql/t-sql/functions/lower-transact-sql).  
  
 La transformación Búsqueda tiene las entradas y resultados siguientes:  
  
-   Entrada.  
  
-   Resultado coincidente. El resultado coincidente administra las filas de la entrada de transformación que coinciden como mínimo con una entrada del conjunto de datos de referencia.  
  
-   Resultado no coincidente. El resultado no coincidente administra las filas de la entrada que no coinciden como mínimo con una entrada del conjunto de datos de referencia. Si configura la transformación Búsqueda para que trate como errores las filas sin entradas coincidentes, las filas se redirigirán a la salida de errores. En los demás casos, la transformación redirigiría dichas filas al resultado no coincidente.  
  
    > [!NOTE]  
    >  En [!INCLUDE[ssISversion2005](../../../includes/ssisversion2005-md.md)], la transformación Búsqueda solo tenía un resultado. Para obtener más información sobre cómo ejecutar una transformación de búsqueda que se creó en [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)], consulte [actualizar transformaciones de búsqueda](../../../sql-server/install/upgrade-lookup-transformations.md).  
  
-   Resultado de errores  
  
## <a name="caching-the-reference-dataset"></a>Almacenar en caché el conjunto de datos de referencia  
 Una caché en memoria almacena el conjunto de datos de referencia y una tabla hash que indiza los datos. La memoria caché permanece en la memoria hasta que se completa la ejecución del paquete. Puede guardar la memoria caché en un archivo caché (.caw).  
  
 Al conservar la memoria caché en un archivo, el sistema la carga con más rapidez. De esta forma, se mejora el rendimiento de la transformación Búsqueda y del paquete. Recuerde que cuando utiliza un archivo caché, está trabajando con datos que no están tan actualizados como los de la base de datos.  
  
 A continuación se describen otras ventajas relacionadas con guardar la memoria caché en un archivo:  
  
-   ***El archivo caché se puede compartir entre varios paquetes. Para más información, vea***   [Implementar una transformación de búsqueda en el modo de caché completa mediante el Administrador de conexiones de caché](../../connection-manager/lookup-transformation-full-cache-mode-cache-connection-manager.md)  ***.***  
  
-   El archivo caché se puede implementar con un paquete. ***De esta forma, podrá utilizar los datos en varios equipos.*** Para obtener información, vea [Cómo crear e implementar una memoria caché para la transformación Búsqueda](create-and-deploy-a-cache-for-the-lookup-transformation.md).  
  
-   Usar el origen de archivo sin formato para leer datos del archivo caché. A continuación, puede utilizar otros componentes de flujo de datos para transformar o mover los datos. Para más información, consulte [Raw File Source](../raw-file-source.md).  
  
    > [!NOTE]  
    >  El administrador de conexiones de caché no admite archivos caché creados o modificados mediante el destino de archivo sin formato.  
  
-   Puede llevar a cabo operaciones y atributos de conjunto en el archivo caché utilizando la tarea Sistema de archivos. Para obtener más información, vea [File System Task](../../control-flow/file-system-task.md).  
  
 A continuación se enumeran las opciones de almacenamiento en caché:  
  
-   El conjunto de datos de referencia se genera mediante una tabla, vista o consulta SQL y se carga en la memoria caché antes de que se ejecute la transformación Búsqueda. Puede usar el administrador de conexiones OLE DB para tener acceso al conjunto de datos.  
  
     Esta opción de almacenamiento en caché es compatible con la opción de almacenamiento en caché completa disponible para la transformación Búsqueda en [!INCLUDE[ssISversion2005](../../../includes/ssisversion2005-md.md)].  
  
-   El conjunto de datos de referencia se genera a partir de un origen de datos conectado al flujo de datos o de un archivo caché, y se carga en la memoria caché antes de que se ejecute la transformación Búsqueda. Para tener acceso al conjunto de datos puede usar el administrador de conexiones de caché o la transformación Caché. Para obtener más información, consulte [Cache Connection Manager](../../connection-manager/cache-connection-manager.md) y [Cache Transform](cache-transform.md).  
  
-   El conjunto de datos de referencia se genera mediante una tabla, vista o consulta SQL durante la ejecución de la transformación Búsqueda. Las filas con entradas coincidentes en el conjunto de datos de referencia y las que no tienen entradas coincidentes se cargan en la memoria caché.  
  
     Cuando se supera el tamaño de la memoria caché, la transformación Búsqueda quita automáticamente de la memoria caché las filas utilizadas con menor frecuencia.  
  
     Esta opción de almacenamiento en caché es compatible con la opción de almacenamiento en caché parcial disponible para la transformación Búsqueda en [!INCLUDE[ssISversion2005](../../../includes/ssisversion2005-md.md)].  
  
-   El conjunto de datos de referencia se genera mediante una tabla, vista o consulta SQL durante la ejecución de la transformación Búsqueda. No se almacenan datos en la memoria caché.  
  
     Esta opción de almacenamiento en caché es compatible con la opción sin almacenamiento en caché disponible para la transformación Búsqueda en [!INCLUDE[ssISversion2005](../../../includes/ssisversion2005-md.md)].  
  
 [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] y [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] difieren en el modo en que comparan cadenas. Si la transformación Búsqueda se configura para cargar el conjunto de datos de referencia en la memoria caché antes de que se ejecute la transformación Búsqueda, [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] lleva a cabo la comparación de búsqueda en la memoria caché. En caso contrario, la operación de búsqueda utiliza una instrucción SQL con parámetros y [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] realiza la comparación de búsqueda. Por lo tanto, es posible que la transformación Búsqueda devuelva un número de coincidencias diferentes a partir de la misma tabla de búsqueda, en función del tipo de caché.  
  
## <a name="related-tasks"></a>Related Tasks  
 Puede establecer propiedades a través del Diseñador de [!INCLUDE[ssIS](../../../includes/ssis-md.md)] o mediante programación. Para obtener información detallada, vea los siguientes temas.  
  
-   [Implementación de una búsqueda en los modos No hay caché o Caché parcial](implement-a-lookup-in-no-cache-or-partial-cache-mode.md)  
  
-   [Implementación de una transformación Búsqueda en el modo Caché completa con el Administrador de conexiones de caché](../../connection-manager/lookup-transformation-full-cache-mode-cache-connection-manager.md)  
  
-   [Implementación de una transformación Búsqueda en el modo Caché completa con el Administrador de conexiones OLE DB](../../connection-manager/lookup-transformation-full-cache-mode-ole-db-connection-manager.md)  
  
-   [Establecer las propiedades de un componente de flujo de datos](../set-the-properties-of-a-data-flow-component.md)  
  
## <a name="related-content"></a>Contenido relacionado  
  
-   Vídeo, [Cómo implementar una transformación Búsqueda en modo de memoria caché completa (vídeo de SQL Server)](http://go.microsoft.com/fwlink/?LinkId=131031), en msdn.microsoft.com  
  
-   Entrada de blog, [Prácticas recomendadas para utilizar los modos de caché de la transformación Búsqueda](http://go.microsoft.com/fwlink/?LinkId=146623)(en inglés), en blogs.msdn.com  
  
-   Entrada de blog, [Patrón de búsqueda: sin distinción de mayúsculas y minúsculas](http://go.microsoft.com/fwlink/?LinkId=157782), en blogs.msdn.com  
  
-   Ejemplo, [Transformación de búsqueda](http://go.microsoft.com/fwlink/?LinkId=267528), en msftisprodsamples.codeplex.com.  
  
     Para obtener información acerca de cómo instalar muestras de producto y bases de datos de ejemplo de [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] , vea [Ejemplos del producto SQL Server Integration Services](http://go.microsoft.com/fwlink/?LinkId=267527).  
  
## <a name="see-also"></a>Vea también  
 [Transformación Búsqueda aproximada](fuzzy-lookup-transformation.md)   
 [Transformación Búsqueda de términos](term-lookup-transformation.md)   
 [Flujo de datos](../data-flow.md)   
 [Transformaciones de Integration Services](integration-services-transformations.md)  
  
  
