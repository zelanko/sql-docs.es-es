---
title: "Descripción de los tipos de Cursor | Documentos de Microsoft"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: jdbc
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 4f4d3db7-4f76-450d-ab63-141237a4f034
caps.latest.revision: "51"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: dfd697881fbde24c797707990d53c2cc33576a24
ms.sourcegitcommit: 2713f8e7b504101f9298a0706bacd84bf2eaa174
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/18/2017
---
# <a name="understanding-cursor-types"></a>Descripción de los tipos de cursor
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  Las operaciones de una base de datos relacional actúan en un conjunto completo de filas. El conjunto de filas que devuelve una instrucción SELECT está compuesto por todas las filas que satisfacen las condiciones de la cláusula WHERE de la instrucción. Este conjunto completo de filas que devuelve la instrucción se conoce como conjunto de resultados. Las aplicaciones no siempre funcionan de forma eficaz con el conjunto de resultados completo si lo toman como una unidad. Estas aplicaciones necesitan un mecanismo que trabaje con una fila o un pequeño bloque de filas cada vez. Los cursores son una extensión de los conjuntos de resultados que proporcionan dicho mecanismo.  
  
 Para ampliar el procesamiento de los conjuntos de resultados, los cursores:  
  
-   Permiten situarse en filas específicas del conjunto de resultados.  
  
-   Recuperan una fila o un bloque de filas de la posición actual en el conjunto de resultados.  
  
-   Admiten modificaciones de los datos de las filas en la posición actual del conjunto de resultados.  
  
-   Aceptan diferentes grados de visibilidad para los cambios que realizan otros usuarios en la información de la base de datos que se presenta en el conjunto de resultados.  
  
> [!NOTE]  
>  Para obtener una descripción completa de la [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] tipos de cursor, vea el tema "Cursor Types (Database Engine)" en [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] libros en pantalla.  
  
 La especificación JDBC proporciona compatibilidad con los cursores de solo avance y los cursores desplazables que son sensibles o no a los cambios que realizan otros trabajos, y pueden ser de solo lectura o actualizables. Esta funcionalidad se proporciona mediante la [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] [SQLServerResultSet](../../connect/jdbc/reference/sqlserverresultset-class.md) clase.  
  
## <a name="remarks"></a>Comentarios  
 El controlador JDBC es compatible con los siguientes tipos de cursor:  
  
|Conjunto de resultados<br /><br /> de conjunto de resultados|Tipo de cursor de SQL Server|Características|select<br /><br /> Método|response<br /><br /> de respuesta|Description|  
|------------------------------------|----------------------------|---------------------|-----------------------|----------------------------|-----------------|  
|TYPE_FORWARD_ONLY (CONCUR_READ_ONLY)|N/D|Solo avance y solo lectura|directo|completas|La aplicación tiene que hacer un único paso (hacia delante) a través del conjunto de resultados. Éste es el comportamiento predeterminado, que es el mismo que el de un cursor TYPE_SS_DIRECT_FORWARD_ONLY. El controlador lee todo el conjunto de resultados del servidor en una memoria durante la ejecución de la instrucción.|  
|TYPE_FORWARD_ONLY (CONCUR_READ_ONLY)|N/D|Solo avance y solo lectura|directo|adaptive|La aplicación tiene que hacer un único paso (hacia delante) a través del conjunto de resultados. Se comporta igual que un cursor TYPE_SS_DIRECT_FORWARD_ONLY. El controlador lee las filas del servidor a medida que la aplicación las solicita y, por tanto, reduce el uso de la memoria del lado cliente.|  
|TYPE_FORWARD_ONLY (CONCUR_READ_ONLY)|Avance rápido|Solo avance y solo lectura|cursor|N/D|La aplicación tiene que hacer un único paso (hacia delante) a través del conjunto de resultados mediante un cursor de servidor. Se comporta igual que un cursor TYPE_SS_SERVER_CURSOR_FORWARD_ONLY.<br /><br /> Las filas son recuperadas del servidor en bloques que son especificados por el tamaño de captura.|  
|TYPE_FORWARD_ONLY (CONCUR_UPDATABLE)|Dinámico (de solo avance)|Solo avance, actualizable|N/D|N/D|La aplicación tiene que hacer un único paso (hacia delante) a través del conjunto de resultados para actualizar una o varias filas.<br /><br /> Las filas son recuperadas del servidor en bloques que son especificados por el tamaño de captura.<br /><br /> De forma predeterminada, el tamaño de captura se fija cuando la aplicación llama a la [setFetchSize](../../connect/jdbc/reference/setfetchsize-method-sqlserverresultset.md) método de la [SQLServerResultSet](../../connect/jdbc/reference/sqlserverresultset-class.md) objeto.<br /><br /> **Nota:** el controlador JDBC proporciona una característica de almacenamiento en búfer adaptable que le permite recuperar los resultados de la ejecución de instrucción de la [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] como la aplicación los necesita, en lugar de todos a la vez. Por ejemplo, si la aplicación tuviera que recuperar una cantidad de datos demasiado grande para la memoria de la aplicación, el almacenamiento en búfer adaptable permite a la aplicación cliente recuperar ese valor como un flujo. El comportamiento predeterminado del controlador es "**adaptable**". Sin embargo, para obtener el almacenamiento en búfer adaptable para los conjuntos de resultados adaptables de solo avance, la aplicación tiene que llamar explícitamente a la [setResponseBuffering](../../connect/jdbc/reference/setresponsebuffering-method-sqlserverstatement.md) método de la [SQLServerStatement](../../connect/jdbc/reference/sqlserverstatement-class.md) objeto proporcionando un **cadena** valor "**adaptable"**. Para un código de ejemplo, vea [muestra de datos grandes actualización](../../connect/jdbc/updating-large-data-sample.md).|  
|TYPE_SCROLL_INSENSITIVE|Estático|Desplazable y no actualizable<br /><br /> Las actualizaciones, inserciones y eliminaciones en filas externas no son visibles.|N/D|N/D|La aplicación requiere una instantánea de base de datos. El conjunto de resultados no es adaptable. Solo es compatible CONCUR_READ_ONLY.  Todos los demás tipos de simultaneidad producirán una excepción cuando se usen con este tipo de cursor.<br /><br /> Las filas son recuperadas del servidor en bloques que son especificados por el tamaño de captura.|  
|TYPE_SCROLL_SENSITIVE<br /><br /> (CONCUR_READ_ONLY)|Keyset|Desplazable, de solo lectura. Las actualizaciones de filas externas son visibles y las eliminaciones aparecen como datos que faltan.<br /><br /> Las inserciones en filas externas no son visibles.|N/D|N/D|La aplicación tiene que ver datos cambiados solo para las filas existentes.<br /><br /> Las filas son recuperadas del servidor en bloques que son especificados por el tamaño de captura.|  
|TYPE_SCROLL_SENSITIVE<br /><br /> (CONCUR_UPDATABLE, CONCUR_SS_SCROLL_LOCKS, CONCUR_SS_OPTIMISTIC_CC, CONCUR_SS_OPTIMISTIC_CCVAL)|Keyset|Desplazable, actualizable.<br /><br /> Las actualizaciones de filas externas e internas son visibles y las eliminaciones aparecen como datos que faltan; las inserciones no son visibles.|N/D|N/D|La aplicación puede cambiar datos en las filas existentes mediante el objeto de conjunto de resultados. La aplicación también debe ser capaz de ver los cambios en filas hechos por otros desde fuera del objeto de conjunto de resultados.<br /><br /> Las filas son recuperadas del servidor en bloques que son especificados por el tamaño de captura.|  
|TYPE_SS_DIRECT_FORWARD_ONLY|N/D|Solo avance y solo lectura|N/D|completo o adaptable|Valor entero = 2003. Proporciona un cursor de solo lectura del lado cliente que está completamente almacenado en búfer. No se crea ningún cursor de servidor.<br /><br /> Solo es compatible el tipo de simultaneidad CONCUR_READ_ONLY. Todos los demás tipos de simultaneidad producen una excepción cuando se usan con este tipo de cursor.|  
|TYPE_SS_SERVER_CURSOR_FORWARD_ONLY|Avance rápido|Solo avance|N/D|N/D|Valor entero = 2004. Rápido, con acceso a todos los datos mediante un cursor de servidor. Es actualizable cuando se usa con un tipo de simultaneidad CONCUR_UPDATABLE.<br /><br /> Las filas son recuperadas del servidor en bloques que son especificados por el tamaño de captura.<br /><br /> Para obtener el almacenamiento en búfer adaptable para este caso, la aplicación tiene que llamar explícitamente a la [setResponseBuffering](../../connect/jdbc/reference/setresponsebuffering-method-sqlserverstatement.md) método de la [SQLServerStatement](../../connect/jdbc/reference/sqlserverstatement-class.md) objeto proporcionando un **cadena**  valor "**adaptable"**. Para un código de ejemplo, vea [muestra de datos grandes actualización](../../connect/jdbc/updating-large-data-sample.md).|  
|TYPE_SS_SCROLL_STATIC|Estático|No se reflejan las actualizaciones de los demás usuarios.|N/D|N/D|Valor entero = 1004. La aplicación requiere una instantánea de base de datos. Se trata de la [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]-sinónimo específico de para JDBC TYPE_SCROLL_INSENSITIVE y tiene el mismo comportamiento de configuración de simultaneidad.<br /><br /> Las filas son recuperadas del servidor en bloques que son especificados por el tamaño de captura.|  
|TYPE_SS_SCROLL_KEYSET<br /><br /> (CONCUR_READ_ONLY)|Keyset|Desplazable, de solo lectura. Las actualizaciones de filas externas son visibles y las eliminaciones aparecen como datos que faltan.<br /><br /> Las inserciones en filas externas no son visibles.|N/D|N/D|Valor entero = 1005. La aplicación solo tiene que ver los datos cambiados para las filas existentes. Se trata de la [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]-sinónimo específico de para JDBC TYPE_SCROLL_SENSITIVE y tiene el mismo comportamiento de configuración de simultaneidad.<br /><br /> Las filas son recuperadas del servidor en bloques que son especificados por el tamaño de captura.|  
|TYPE_SS_SCROLL_KEYSET<br /><br /> (CONCUR_UPDATABLE, CONCUR_SS_SCROLL_LOCKS, CONCUR_SS_OPTIMISTIC_CC, CONCUR_SS_OPTIMISTIC_CCVAL)|Keyset|Desplazable, actualizable.<br /><br /> Las actualizaciones de filas externas e internas son visibles y las eliminaciones aparecen como datos que faltan; las inserciones no son visibles.|N/D|N/D|Valor entero = 1005. Aplicación tiene que cambiar los datos o ver los datos cambiados para las filas existentes. Se trata de la [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]-sinónimo específico de para JDBC TYPE_SCROLL_SENSITIVE y tiene el mismo comportamiento de configuración de simultaneidad.<br /><br /> Las filas son recuperadas del servidor en bloques que son especificados por el tamaño de captura.|  
|TYPE_SS_SCROLL_DYNAMIC<br /><br /> (CONCUR_READ_ONLY)|Dinámica|Desplazable, de solo lectura.<br /><br /> Las actualizaciones e inserciones de las filas externas son visibles, y las eliminaciones aparecen como datos que faltan de forma transitoria en el búfer de captura actual.|N/D|N/D|Valor entero = 1006. La aplicación debe ver los datos cambiados para las filas existentes, así como las filas insertadas y eliminadas durante la duración del cursor.<br /><br /> Las filas son recuperadas del servidor en bloques que son especificados por el tamaño de captura.|  
|TYPE_SS_SCROLL_DYNAMIC<br /><br /> (CONCUR_UPDATABLE, CONCUR_SS_SCROLL_LOCKS, CONCUR_SS_OPTIMISTIC_CC, CONCUR_SS_OPTIMISTIC_CCVAL)|Dinámica|Desplazable, actualizable.<br /><br /> Las actualizaciones e inserciones de las filas externas e internas son visibles, y las eliminaciones aparecen como datos que faltan de forma transitoria en el búfer de captura actual.|N/D|N/D|Valor entero = 1006. La aplicación puede cambiar los datos de las filas existentes, o insertar o eliminar filas mediante el objeto de conjunto de resultados. La aplicación también debe ser capaz de ver los cambios, inserciones y eliminaciones en filas hechos por otros desde fuera del objeto de conjunto de resultados.<br /><br /> Las filas son recuperadas del servidor en bloques que son especificados por el tamaño de captura.|  
  
## <a name="cursor-positioning"></a>Colocación de los cursores  
 Los cursores TYPE_FORWARD_ONLY, TYPE_SS_DIRECT_FORWARD_ONLY y TYPE_SS_SERVER_CURSOR_FORWARD_ONLY solo admiten la [siguiente](../../connect/jdbc/reference/next-method-sqlserverresultset.md) método de colocación.  
  
 El cursor TYPE_SS_SCROLL_DYNAMIC no admite el [absoluta](../../connect/jdbc/reference/absolute-method-sqlserverresultset.md) y [getRow](../../connect/jdbc/reference/getrow-method-sqlserverresultset.md) métodos. El método absoluto puede conseguirse aproximadamente mediante una combinación de las llamadas a la [primer](../../connect/jdbc/reference/first-method-sqlserverresultset.md) y [relativa](../../connect/jdbc/reference/relative-method-sqlserverresultset.md) métodos para los cursores dinámicos.  
  
 El método getRow se admite solo los cursores TYPE_FORWARD_ONLY, TYPE_SS_DIRECT_FORWARD_ONLY, TYPE_SS_SERVER_CURSOR_FORWARD_ONLY, TYPE_SS_SCROLL_KEYSET y TYPE_SS_SCROLL_STATIC. GetRow (método) con todos los tipos de cursor de solo avance devuelve el número de filas leídas hasta el cursor.  
  
> [!NOTE]  
>  Cuando una aplicación realiza un llamada o una llamada no compatible al método getRow para colocar un cursor no compatible, se produce una excepción con el mensaje, "la operación solicitada no es compatible con este tipo de cursor."  
  
 Solo los cursores TYPE_SS_SCROLL_KEYSET y los cursores TYPE_SCROLL_SENSITIVE equivalentes exponen las filas eliminadas. Si el cursor está situado en una fila eliminada, valores de columna no están disponibles y el [rowDeleted](../../connect/jdbc/reference/rowdeleted-method-sqlserverresultset.md) método devuelve "true". Llamadas para obtener\<tipo > métodos inician una excepción con el mensaje, "No se puede obtener el valor de una fila eliminada". Las filas eliminadas no se pueden actualizar. Si intenta llamar a una actualización\<tipo > método en una fila eliminada, se produce una excepción con el mensaje, "no se puede actualizar una fila eliminada". El cursor TYPE_SS_SCROLL_DYNAMIC tiene el mismo comportamiento hasta que el cursor se mueve fuera del búfer de captura actual.  
  
 Los cursores dinámicos y hacia delante exponen las filas eliminadas de un modo similar, pero solo mientras siguen estando accesibles en el búfer de captura. Con los cursores hacia delante, esto es bastante sencillo. Con los cursores dinámicos resulta más complejo si el tamaño de la lectura es mayor que 1. Una aplicación puede mover el cursor hacia delante y hacia atrás dentro de la ventana que se define en el búfer de captura, pero la fila eliminada desaparecerá cuando el búfer de captura original en el que se actualizó permanezca.  Si una aplicación no desea ver las filas eliminadas de forma transitoria mediante cursores dinámicos, se debería usar una lectura relativa (0).  
  
 Si los valores de la clave de una fila de cursores TYPE_SS_SCROLL_KEYSET o TYPE_SCROLL_SENSITIVE se actualizan con el cursor, la fila conserva su posición original en el conjunto de resultados, independientemente de si la fila actualizada cumple los criterios de selección del cursor. Si la fila se actualizó fuera del cursor, una fila eliminada aparecerá en la posición original de la fila, pero solamente aparecerá en el cursor si otra fila con los valores de la nueva clave estaba presente en el cursor y se ha eliminado desde entonces.  
  
 Con los cursores dinámicos, las filas actualizadas conservarán su posición dentro del búfer de captura hasta que el búfer de captura que permanece defina la ventana.  Las filas actualizadas podrían reaparecer después en posiciones diferentes dentro del conjunto de resultados, o podrían desaparecer por completo. Las aplicaciones que tienen que evitar incoherencias transitorias en el conjunto de resultados deberían usar un tamaño de lectura de 1 (de forma predeterminada es de 8 filas con simultaneidad de CONCUR_SS_SCROLL_LOCKS y de 128 filas con otras).  
  
## <a name="cursor-conversion"></a>Conversión de cursores  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]en ocasiones, puede elegir implementar un tipo de cursor que no sea el solicitado, lo que se conoce como conversión implícita del cursor (o degradación del cursor). Para obtener más información acerca de la conversión implícita del cursor, vea el tema "Using Implicit Cursor Conversions" en [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] libros en pantalla.  
  
 Con [!INCLUDE[ssVersion2000](../../includes/ssversion2000_md.md)], al actualizar los datos a través de ResultSet.TYPE_SCROLL_SENSITIVE y ResultSet.CONCUR_UPDATABLE lo establece, se produce una excepción con un mensaje "el cursor es READ ONLY". Esta excepción se produce porque el [!INCLUDE[ssVersion2000](../../includes/ssversion2000_md.md)] ha realizado una conversión implícita del cursor para ese resultado establecido y no ha devuelto el cursor actualizado que se ha solicitado.  
  
 Como solución alternativa para este problema, puede elegir una de las siguientes dos soluciones:  
  
-   Asegurarse de que la tabla subyacente tiene una clave principal  
  
-   Use [SQLServerResultSet.TYPE_SS_SCROLL_DYNAMIC](../../connect/jdbc/reference/type-ss-scroll-dynamic-field-sqlserverresultset.md) en lugar de ResultSet.TYPE_SCROLL_SENSITIVE durante la creación de una instrucción.  
  
## <a name="cursor-updating"></a>Actualización de cursores  
 Las actualizaciones en contexto se admiten para los cursores cuyo tipo y simultaneidad lo permiten. Si el cursor no está situado en una fila actualizable en el conjunto de resultados (ninguna get\<tipo > llamada de método se realizó correctamente), una llamada a una actualización\<tipo > método producirá una excepción con el mensaje, "el conjunto de resultados no tiene ninguna fila actual". La especificación de JDBC indica que se inicia una excepción cuando se llama a un método de actualización con una columna de un cursor que sea CONCUR_READ_ONLY. En situaciones donde la fila no es actualizable, por ejemplo debido a un conflicto de simultaneidad optimista como una competencia de actualización o eliminación, la excepción podría no iniciarse hasta que [insertRow](../../connect/jdbc/reference/insertrow-method-sqlserverresultset.md), [updateRow](../../connect/jdbc/reference/updaterow-method-sqlserverresultset.md), o [deleteRow](../../connect/jdbc/reference/deleterow-method-sqlserverresultset.md) se llama.  
  
 Después de llamar a actualizar\<tipo >, no se puede tener acceso a la columna afectada por get\<tipo > hasta updateRow o [cancelRowUpdates](../../connect/jdbc/reference/cancelrowupdates-method-sqlserverresultset.md) se ha llamado. Esto evita los problemas que se producen porque una columna se actualiza con un tipo diferente del que devuelve el servidor, y las siguientes llamadas podrían invocar conversiones de tipos del lado cliente que dan resultados imprecisos. Llamadas para obtener\<tipo > se iniciará una excepción con el mensaje, "no se pueden tener acceso a las columnas actualizadas hasta a updateRow() o se ha llamado a cancelRowUpdates()".  
  
> [!NOTE]  
>  Si se llama al método updateRow cuando no hay columnas que se hayan actualizado, el controlador JDBC iniciará una excepción con el mensaje, "llamó a updateRow() cuando no hay columnas se han actualizado."  
  
 Después de [moveToInsertRow](../../connect/jdbc/reference/movetoinsertrow-method-sqlserverresultset.md) ha sido llama, una excepción se producirá si cualquier otro método que obtener\<tipo >, actualizar\<tipo >, insertRow y otros métodos de colocación del cursor (incluidos [ moveToCurrentRow](../../connect/jdbc/reference/movetocurrentrow-method-sqlserverresultset.md)) se llaman en el conjunto de resultados. El método moveToInsertRow coloca de hecho el conjunto de resultados en modo de inserción y métodos de colocación de cursores terminan dicho modo. Llamadas para colocar cursores relativos mueven el cursor en relación con la posición en que estaba antes de llama a moveToInsertRow. Después de las llamadas para colocar cursores, la posición final del cursor de destino se convierte en la nueva posición del cursor.  
  
 Si la llamada realizada mientras en insert modo no se realiza correctamente para colocar un cursor, se llamó a la posición del cursor después de la llamada errónea es la posición del cursor original antes de moveToInsetRow. Si se produce un error de insertRow, el cursor permanece en la fila de inserción y el cursor permanece en modo de inserción.  
  
 Las columnas de la fila de inserción están inicialmente en un estado sin inicializar. Llamadas a la actualización\<tipo > método establece el estado de las columnas en inicializado. Una llamada a get\<tipo > método para una columna sin inicializar inicia una excepción. Una llamada al método insertRow devuelve todas las columnas en la fila de inserción a un estado sin inicializar.  
  
 Si alguna columna está sin inicializar cuando se llama al método insertRow, se inserta el valor predeterminado de la columna. Si no hay ningún valor predeterminado pero la columna admite valores NULL, se inserta el valor NULL. Si no hay ningún valor predeterminado y la columna no admite valores NULL, el servidor devolverá un error y se iniciará una excepción.  
  
> [!NOTE]  
>  Las llamadas al método getRow devuelve 0 cuando se encuentra en modo de inserción.  
>   
>  El controlador JDBC no es compatible con las eliminaciones o actualizaciones por posición. Según la especificación de JDBC, el [setCursorName](../../connect/jdbc/reference/setcursorname-method-sqlserverstatement.md) método no tiene ningún efecto y el [getCursorName](../../connect/jdbc/reference/getcursorname-method-sqlserverresultset.md) método producirá una excepción si se llama.  
>   
>  Los cursores estáticos y de solo lectura nunca son actualizables.  
>   
>  SQL Server restringe los cursores de servidor a un solo conjunto de resultados. Si un lote o procedimiento almacenado contiene varias instrucciones, se debe usar un cursor de cliente de solo lectura y de solo avance.  
  
## <a name="see-also"></a>Vea también  
 [Administrar conjuntos de resultados con el controlador JDBC](../../connect/jdbc/managing-result-sets-with-the-jdbc-driver.md)  
  
  
