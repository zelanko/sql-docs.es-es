---
title: Cursores | Microsoft Docs
ms.custom: ''
ms.date: 03/11/2020
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- results [SQL Server], cursors
- Transact-SQL cursors, about cursors
- cursors [SQL Server]
- data access [SQL Server], cursors
- result sets [SQL Server], cursors
- requesting cursors
- cursors [SQL Server], about cursors
ms.assetid: e668b40c-bd4d-4415-850d-20fc4872ee72
author: rothja
ms.author: jroth
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: a053f49a6ab3b42e31c5b71c2d2d558ea3170440
ms.sourcegitcommit: 59c09dbe29882cbed539229a9bc1de381a5a4471
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 03/11/2020
ms.locfileid: "79112337"
---
# <a name="cursors"></a>Cursores
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  Las operaciones de una base de datos relacional actúan en un conjunto completo de filas. Por ejemplo, el conjunto de filas que devuelve una instrucción `SELECT` está compuesto por todas las filas que satisfacen las condiciones de la cláusula `WHERE` de la instrucción. Este conjunto completo de filas que devuelve la instrucción se conoce como conjunto de resultados. Las aplicaciones, especialmente las aplicaciones interactivas en línea, no siempre trabajan de forma eficaz con el conjunto de resultados completo si lo toman como una unidad. Estas aplicaciones necesitan un mecanismo que trabaje con una fila o un pequeño bloque de filas cada vez. Los cursores son una extensión de los conjuntos de resultados que proporcionan dicho mecanismo.  
  
 Los cursores amplían el procesamiento de los resultados porque:  
  
-   Permiten situarse en filas específicas del conjunto de resultados.  
  
-   Recuperan una fila o un bloque de filas de la posición actual en el conjunto de resultados.  
  
-   Aceptan modificaciones de los datos de las filas en la posición actual del conjunto de resultados.  
  
-   Aceptan diferentes grados de visibilidad para los cambios que realizan otros usuarios en la información de la base de datos que se presenta en el conjunto de resultados.  
  
-   Proporcionan instrucciones [!INCLUDE[tsql](../includes/tsql-md.md)] en scripts, procedimientos almacenados y acceso de desencadenadores a los datos de un conjunto de resultados.  
  
> [!TIP]
> En algunos escenarios, si hay una clave principal en una tabla, se puede usar un bucle `WHILE` en lugar de un cursor, sin incurrir en la sobrecarga de un cursor.
> Pero hay escenarios donde los cursores no solo son inevitables, sino que realmente se necesitan. Cuando ese es el caso, si no hay ningún requisito para actualizar las tablas en función del cursor, se usan cursores *firehose*, lo que significa cursores [de avance rápido y de solo lectura](#forward-only).
  
## <a name="cursor-implementations"></a>Implementaciones de cursores  
[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] admite tres implementaciones de cursores.  
  
### <a name="transact-sql-cursors"></a>cursores de Transact-SQL  
Los cursores [!INCLUDE[tsql](../includes/tsql-md.md)] se basan en la sintaxis de `DECLARE CURSOR` y se usan principalmente en scripts de [!INCLUDE[tsql](../includes/tsql-md.md)], procedimientos almacenados y desencadenadores. [!INCLUDE[tsql](../includes/tsql-md.md)] se implementan en el servidor y se administran mediante instrucciones [!INCLUDE[tsql](../includes/tsql-md.md)] enviadas del cliente al servidor. También se pueden encontrar en lotes, procedimientos almacenados o desencadenadores.  
  
### <a name="application-programming-interface-api-server-cursors"></a>Cursores de servidor de la API (Interfaz de programación de aplicaciones)  
Los cursores de API admiten las funciones de cursor de API con OLE DB y ODBC. Los cursores de servidor de la API están implementados en el servidor. Cada vez que una aplicación cliente llama a una función de cursor de la API, el proveedor OLE DB de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Native Client o el controlador de ODBC transmite la solicitud al servidor para que realice una acción con el cursor de servidor de la API.  
  
### <a name="client-cursors"></a>Cursores del cliente  
Los cursores del cliente los implementan de forma interna el controlador ODBC de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Native Client y la DLL que implementa la API ADO. Los cursores del cliente se implementan almacenando en caché todas las filas de conjuntos de resultados del cliente. Cada vez que una aplicación cliente llama a una función de cursor de la API, el controlador ODBC de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Native Client o la DLL de ADO realizan la operación de cursor en las filas del conjunto de resultados almacenadas en la memoria caché del cliente.  
  
## <a name="type-of-cursors"></a>Tipo de cursores  
[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] admite cuatro tipos de cursor. 

> [!NOTE]
> Los cursores pueden aprovechar las tablas de trabajo de tempdb. Como sucede con las operaciones de agregación o de ordenación que se desbordan, estas incurren en E/S y son un cuello de botella de rendimiento potencial. Los cursores `STATIC` usan tablas de trabajo desde su inicio. Para obtener más información, vea las [tablas de trabajo en la Guía de arquitectura de procesamiento de consultas](../relational-databases/query-processing-architecture-guide.md#worktables).

### <a name="forward-only"></a>Solo avance  
Un cursor de solo avance se especifica como `FORWARD_ONLY` y `READ_ONLY`, y no admite el desplazamiento. También se denominan cursores *firehose* y solo admiten la captura de las filas en serie desde el principio hasta el final del cursor. Las filas no se obtienen de la base de datos hasta que se han capturado. Los efectos de las instrucciones `INSERT`, `UPDATE` y `DELETE` que ejecuta el usuario actual o que confirman otros usuarios y que afectan a las filas del conjunto de resultados se hacen visibles a medida que se capturan las filas del cursor.  
  
 Como el cursor no se puede desplazar hacia atrás, la mayoría de los cambios realizados en las filas de la base de datos tras capturar la fila no se pueden ver a través del cursor. En los casos en los que se modifica un valor utilizado para determinar la ubicación de la fila en el conjunto de resultados, por ejemplo, si se actualiza una columna abarcada por un índice clúster, el valor modificado se puede ver a través del cursor.  
  
 Aunque los modelos de cursor de la API de base de datos consideran el cursor de solo avance como un tipo más, [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] no establece esta distinción. [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] considera que las opciones de desplazamiento de solo avance y de desplazamiento son las que se pueden aplicar a los cursores estáticos, a los controlados por conjunto de claves y a los dinámicos. [!INCLUDE[tsql](../includes/tsql-md.md)] cursores admiten cursores estáticos controlados por conjunto de claves y dinámicos que sean de solo avance. Los modelos de cursor de la API de bases de datos dan por sentado que los cursores estáticos, los controlados por conjunto de claves y los dinámicos siempre se pueden desplazar. Cuando se establece el atributo o propiedad de un cursor de la API de bases de datos como de solo avance, [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] lo implementa como cursor dinámico de solo avance.  
  
### <a name="static"></a>estática  
 El conjunto de resultados completo de un cursor estático se genera en **tempdb** cuando se abre el cursor. Un cursor estático siempre muestra el conjunto de resultados tal como estaba al abrir el cursor. Los cursores estáticos detectan pocos cambios o ningún cambio, pero consumen relativamente pocos recursos al desplazarse.  
  
El cursor no refleja las modificaciones realizadas en la base de datos que afectan a la pertenencia al conjunto de resultados o a los valores modificados en las columnas de las filas que forman el conjunto de resultados. Un cursor estático no muestra las nuevas filas insertadas en la base de datos después de abrir el cursor, aunque coincidan con las condiciones de búsqueda de la instrucción `SELECT` del cursor. Si otros usuarios actualizan las filas que conforman el conjunto de resultados, los nuevos valores de datos no se muestran en el cursor estático. El cursor estático muestra las filas eliminadas de la base de datos una vez que se ha abierto el cursor. Las operaciones `UPDATE`, `INSERT` o `DELETE` no se reflejan en un cursor estático (a menos que se cierre y se vuelva a abrir), ni tampoco las modificaciones realizadas con la misma conexión que abrió el cursor.  
  
> [!NOTE]
> [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] cursores estáticos son siempre de solo lectura.  
  
> [!NOTE]
> Como el conjunto de resultados de un cursor estático se almacena en una tabla de trabajo de **tempdb**, el tamaño de las filas del conjunto de resultados no puede exceder el tamaño máximo de fila en una tabla de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)].  
> Para obtener más información, vea las [tablas de trabajo en la Guía de arquitectura de procesamiento de consultas](../relational-databases/query-processing-architecture-guide.md#worktables). Para obtener más información sobre el tamaño máximo de fila, vea [Especificaciones de capacidad máxima para SQL Server](../sql-server/maximum-capacity-specifications-for-sql-server.md).  
  
[!INCLUDE[tsql](../includes/tsql-md.md)] utiliza el término INSENSITIVE para los cursores estáticos. Algunas API de base de datos los identifican como cursores de instantánea.  
  
### <a name="keyset"></a>Keyset  
La pertenencia y el orden de las filas en un cursor dinámico se fijan al abrir el cursor. Los cursores dinámicos se supervisan mediante un conjunto de identificadores únicos (claves) denominado conjunto de claves. Las claves se generan a partir de un conjunto de columnas que identifican las filas del conjunto de resultados de forma unívoca. El conjunto de claves es el conjunto de valores de clave de todas las filas que han sido calificadas para la instrucción `SELECT` en el momento de abrirse el cursor. El conjunto de claves de un cursor dinámico se genera en **tempdb** al abrir el cursor.  
  
### <a name="dynamic"></a>Dinámica  
Los cursores dinámicos son los opuestos a los cursores estáticos. Reflejan todas las modificaciones realizadas en las filas de su conjunto de resultados al desplazarse por el cursor. Los valores de datos, el orden y la pertenencia de las filas del conjunto de resultados pueden cambiar con cada captura. Todas las instrucciones `UPDATE`, `INSERT` y `DELETE` que realizan todos los usuarios son visibles a través del cursor. Las actualizaciones se muestran inmediatamente si se realizan a través del cursor mediante una función de API, como **SQLSetPos**, o la cláusula `WHERE CURRENT OF` de [!INCLUDE[tsql](../includes/tsql-md.md)]. Las actualizaciones realizadas fuera del cursor no son visibles hasta que se confirman, a menos que el nivel de aislamiento de transacción del cursor sea de lectura no confirmada. Para obtener más información sobre los niveles de aislamiento, vea [SET TRANSACTION ISOLATION LEVEL &#40;Transact-SQL&#41;](../t-sql/statements/set-transaction-isolation-level-transact-sql.md). 
 
> [!NOTE]
> Los planes de cursor dinámico no utilizan nunca índices espaciales.  
  
## <a name="requesting-a-cursor"></a>Solicitar un cursor  
 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] admite dos métodos para solicitar un cursor:  
  
-   [!INCLUDE[tsql](../includes/tsql-md.md)]  
  
     El lenguaje [!INCLUDE[tsql](../includes/tsql-md.md)] admite una sintaxis para utilizar cursores modelada a partir de la sintaxis de cursores ISO.  
  
-   Funciones de cursor para interfaces de programación de aplicaciones (API) de bases de datos  
  
     [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] admite la funcionalidad de cursores de las siguientes API de bases de datos:  
  
    -   ADO ([!INCLUDE[msCoName](../includes/msconame-md.md)] ActiveX Data Object)  
  
    -   OLE DB  
  
    -   ODBC (Conectividad abierta de bases de datos)  
  
Una aplicación nunca debe mezclar estos dos métodos de solicitud de cursores. Una aplicación que ya ha utilizado la API para determinar el comportamiento de cursores no debe ejecutar una instrucción DECLARE CURSOR de [!INCLUDE[tsql](../includes/tsql-md.md)] para solicitar también un cursor [!INCLUDE[tsql](../includes/tsql-md.md)] . Una aplicación solo debe ejecutar DECLARE CURSOR si antes ha vuelto a establecer todos los atributos de cursores de la API a sus valores predeterminados.  
  
Si no se ha solicitado un cursor [!INCLUDE[tsql](../includes/tsql-md.md)] ni un cursor de la API, [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] devuelve de forma predeterminada un conjunto de resultados completo, conocido como conjunto de resultados predeterminado, a la aplicación.  
  
## <a name="cursor-process"></a>Proceso de cursores  
 [!INCLUDE[tsql](../includes/tsql-md.md)] y los cursores de la API poseen una sintaxis diferente, se utiliza el siguiente proceso general con todos los cursores de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] :  
  
1.  Asigne un cursor al conjunto de resultados de una instrucción [!INCLUDE[tsql](../includes/tsql-md.md)] y defina características del cursor como, por ejemplo, si sus filas se pueden actualizar.  
  
2.  Ejecute la instrucción [!INCLUDE[tsql](../includes/tsql-md.md)] para llenar el cursor.  
  
3.  Recupere las filas del cursor que desea ver. La operación de recuperación de una fila o un bloque de filas de un cursor recibe el nombre de captura. La realización de una serie de capturas para obtener filas, ya sea hacia adelante o hacia atrás, recibe el nombre de desplazamiento.  
  
4.  Existe la opción de realizar operaciones de modificación (actualización o eliminación) en la fila de la posición actual del cursor.  
  
5.  Cierre el cursor.  
  
## <a name="related-content"></a>Contenido relacionado  
[Comportamientos de los cursores](../relational-databases/native-client-odbc-cursors/cursor-behaviors.md)    
[Cómo se implementan los cursores](../relational-databases/native-client-odbc-cursors/implementation/how-cursors-are-implemented.md)  
  
## <a name="see-also"></a>Consulte también  
[DECLARE CURSOR &#40;Transact-SQL&#41;](../t-sql/language-elements/declare-cursor-transact-sql.md)   
[Cursores &#40;Transact-SQL&#41;](../t-sql/language-elements/cursors-transact-sql.md)   
[Funciones del cursor &#40;Transact-SQL&#41;](../t-sql/functions/cursor-functions-transact-sql.md)   
[Procedimientos almacenados de cursor &#40;Transact-SQL&#41;](../relational-databases/system-stored-procedures/cursor-stored-procedures-transact-sql.md)   
[SET TRANSACTION ISOLATION LEVEL &#40;Transact-SQL&#41;](../t-sql/statements/set-transaction-isolation-level-transact-sql.md)    

  
