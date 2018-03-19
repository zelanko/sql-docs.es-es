---
title: CREATE REMOTE TABLE AS SELECT (Parallel Data Warehouse) | Microsoft Docs
ms.custom: 
ms.date: 08/10/2017
ms.prod: 
ms.prod_service: pdw
ms.reviewer: 
ms.service: sql-data-warehouse
ms.component: t-sql|statements
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 16ef8191-7587-45a3-9ee9-7d99b7088de3
caps.latest.revision: 
author: barbkess
ms.author: barbkess
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 1a44f5f46a60959b38b3e8121847e0c80c1ba82b
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 01/25/2018
---
# <a name="create-remote-table-as-select-parallel-data-warehouse"></a>CREATE REMOTE TABLE AS SELECT (Parallel Data Warehouse)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-xxxx-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-xxxx-pdw-md.md)]

  Selecciona los datos de una base de datos [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] y copia esos datos en una nueva tabla en una base de datos [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] SMP en un servidor remoto. [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] usa el dispositivo, con todas las ventajas del procesamiento de consultas MPP, para seleccionar los datos de la copia remota. Úselo para escenarios que necesiten la funcionalidad de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 Para configurar el servidor remoto, vea "Copia de la tabla remota" en la [!INCLUDE[pdw-product-documentation](../../includes/pdw-product-documentation-md.md)].  
  
 ![Icono de vínculo a temas](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo a temas") [Convenciones de sintaxis de Transact-SQL &#40;Transact-SQL&#41;](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
CREATE REMOTE TABLE [ database_name . [ schema_name ] . | schema_name. ] table_name     AT ('<connection_string>')  
    [ WITH ( BATCH_SIZE = batch_size ) ]  
    AS <select_statement>  
[;]  
  
<connection_string> ::=   
    Data Source = { IP_address | hostname } [, port ]; User ID = user_name ;Password = password;  
  
<select_statement> ::=  
    [ WITH <common_table_expression> [ ,...n ] ]  
    SELECT <select_criteria>  
```  
  
## <a name="arguments"></a>Argumentos  
 *database_name*  
 Base de datos en la que se va a crear la tabla remota. *database_name* es un nombre de base de datos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. El valor predeterminado es la base de datos predeterminada para el inicio de sesión del usuario en la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] de destino.  
  
 *schema_name*  
 Esquema de la nueva tabla. El valor predeterminado es el esquema predeterminado para el inicio de sesión del usuario en la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] de destino.  
  
 *table_name*  
 Nombre de la nueva tabla. Para obtener detalles sobre los nombres de tabla permitidos, vea "Normas de nomenclatura de objetos" en la [!INCLUDE[pdw-product-documentation](../../includes/pdw-product-documentation-md.md)].  
  
 La tabla remota se crea como un montón. No tiene desencadenadores ni restricciones Check. La intercalación de las columnas de la tabla remota es la misma que la de las columnas de la tabla de origen. Esto se aplica a las columnas de tipo **char**, **nchar**, **varchar** y **nvarchar**.  
  
 *connection_string*  
 Cadena de caracteres que especifica los parámetros `Data Source`, `User ID` y `Password` para conectar con el servidor remoto y la base de datos.  
  
 La cadena de conexión es una lista delimitada por puntos y coma de pares de clave y valor. En las palabras clave no se distingue entre mayúsculas y minúsculas. Se omiten los espacios entre los pares de clave y valor. Pero los valores pueden distinguir entre mayúsculas y minúsculas según el origen de datos.  
  
 *Origen de datos*  
 Parámetro que especifica el nombre o la dirección IP, y el número de puerto TCP, del servidor [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] SMP remoto.  
  
 *hostname* o *IP_address*  
 Nombre del equipo de servidor remoto o la dirección IPv4 del servidor remoto. No se admiten direcciones IPv6. Puede especificar una instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] con nombre en el formato **Computer_Name\Instance_Name** o **IP_address\Instance_Name**. El servidor debe ser remoto y, por tanto, no se puede especificar como (local).  
  
 TCP *port* number  
 Número de puerto TCP para la conexión. Puede especificar un número de puerto TCP entre 0 y 65535 para una instancia de SQL Server que no esté escuchando en el puerto predeterminado 1433. Por ejemplo: **ServerA,1450** o **10.192.14.27,1435**  
  
> [!NOTE]  
>  Se recomienda conectar a un servidor remoto mediante la dirección IP. Según la configuración de red, la conexión mediante el nombre del equipo podría requerir pasos adicionales para usar el servidor DNS que no es de dispositivo para resolver el nombre en el servidor correcto. Este paso no es necesario al conectar con una dirección IP. Para obtener más información, vea "Uso de un reenviador DNS para resolver los nombres DNS que no sean de dispositivos (Analytics Platform System)" en la [!INCLUDE[pdw-product-documentation](../../includes/pdw-product-documentation-md.md)].  
  
 *user_name*  
 Nombre de inicio de sesión de autenticación de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] válido. El número máximo de caracteres es 128.  
  
 *password*  
 La contraseña de inicio de sesión. El número máximo de caracteres es 128.  
  
 *batch_size*  
 Número máximo de filas por lote. [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] envía las filas en lotes al servidor de destino. *Batch_size* es un entero positivo >= 0. El valor predeterminado es 0.  
  
 WITH *common_table_expression*  
 Especifica un conjunto de resultados temporal con nombre, conocido como expresión de tabla común (CTE). Para obtener más información, vea [WITH common_table_expression &#40;Transact-SQL&#41;](../../t-sql/queries/with-common-table-expression-transact-sql.md).  
  
 SELECT \<select_criteria> Predicado de consulta que especifica qué datos van a llenar la nueva tabla remota. Para obtener más información sobre la instrucción SELECT, vea [SELECT &#40;Transact-SQL&#41;](../../t-sql/queries/select-transact-sql.md).  
  
## <a name="permissions"></a>Permisos  
 Requiere:  
  
-   Permiso SELECT en todos los objetos de la cláusula SELECT.  
  
-   Permiso CREATE TABLE en la base de datos SMP de destino.  
  
-   Permisos ALTER, INSERT y SELECT en el esquema SMP de destino.  
  
## <a name="error-handling"></a>Tratamiento de errores  
 Si se produce un error al copiar datos en la base de datos remota, [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] anula la operación, registra un error e intenta eliminar la tabla remota. [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] no garantiza una limpieza correcta de la nueva tabla.  
  
## <a name="limitations-and-restrictions"></a>Limitaciones y restricciones  
 **Servidor de destino remoto**:  
  
-   TCP es el valor predeterminado y el único protocolo admitido para conectarse a un servidor remoto.  
  
-   El servidor de destino debe ser un servidor que no sea de dispositivo. CREATE REMOTE TABLE no puede usarse para copiar datos de un dispositivo en otro.  
  
-   La instrucción CREATE REMOTE TABLE solo crea tablas nuevas. Por lo tanto, la nueva tabla no puede existir previamente. La base de datos remota y el esquema ya deben existir.  
  
-   El servidor remoto debe disponer de espacio para almacenar los datos que se transfieren desde el dispositivo a la base de datos remota de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 **Instrucción SELECT**:  
  
-   No se admiten las cláusulas ORDER BY y TOP en los criterios de selección.  
  
-   CREATE REMOTE TABLE no se puede ejecutar dentro de una transacción activa ni cuando está activo el valor AUTOCOMMIT OFF de la sesión.  
  
 [SET ROWCOUNT &#40;Transact-SQL&#41;](../../t-sql/statements/set-rowcount-transact-sql.md) no tiene ningún efecto en esta instrucción. Para lograr un comportamiento similar, use [TOP &#40;Transact-SQL&#41;](../../t-sql/queries/top-transact-sql.md).  
  
## <a name="locking-behavior"></a>Comportamiento del bloqueo  
 Después de crear la tabla remota, la tabla de destino no se bloquea hasta que se inicia la copia. Por lo tanto, es posible que otro proceso elimine la tabla remota después de su creación y antes del inicio de la copia. Cuando ocurre esto, [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] genera un error y se produce un error en la copia.  
  
## <a name="metadata"></a>Metadatos  
 Use [sys.dm_pdw_dms_workers &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-dms-workers-transact-sql.md) para ver el progreso de la copia de los datos seleccionados en el servidor SMP remoto. Las filas con el tipo PARALLEL_COPY_READER contienen esta información.  
  
## <a name="security"></a>Seguridad  
 CREATE REMOTE TABLE usa Autenticación de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para conectarse a la instancia remota de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]; no usa Autenticación de Windows.  
  
 La red externa de [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] debe tener un firewall, a excepción de los puertos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], los puertos administrativos y los puertos de administración.  
  
 Para evitar pérdidas o daños accidentales en los datos, la cuenta de usuario usada para copiar desde el dispositivo a la base de datos de destino debe tener solo los permisos mínimos necesarios en la base de datos de destino.  
  
 La configuración de conexión permite conectarse a la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] SMP; SSL protege los datos de nombre de usuario y contraseña, pero los datos reales se envían sin cifrar en texto no cifrado. Cuando ocurre esto, un usuario malintencionado puede interceptar el texto de la instrucción CREATE REMOTE TABLE, que contiene el nombre de usuario y la contraseña de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para iniciar sesión en la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] SMP. Para evitar este riesgo, use cifrado de datos en la conexión a la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] SMP.  
  
##  <a name="Examples"></a> Ejemplos  
  
### <a name="a-creating-a-remote-table"></a>A. Crear una tabla remota  
 En este ejemplo se crea una tabla remota SMP de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] denominada `MyOrdersTable` en la base de datos `OrderReporting` y el esquema `Orders`. La base de datos `OrderReporting` está en un servidor denominado `SQLA` que escucha en el puerto predeterminado 1433. La conexión con el servidor usa las credenciales del usuario `David`, cuya contraseña es `e4n8@3`.  
  
```  
CREATE REMOTE TABLE OrderReporting.Orders.MyOrdersTable  
AT ( 'Data Source = SQLA, 1433; User ID = David; Password = e4n8@3;' )  
AS SELECT <select_criteria>;  
```  
  
### <a name="b-querying-the-sysdmpdwdmsworkers-dmv-for-remote-table-copy-status"></a>B. Consultar la DMV sys.dm_pdw_dms_workers para obtener el estado de copia de tabla remota  
 Esta consulta muestra cómo ver el estado de copia de una copia de tabla remota.  
  
```  
SELECT * FROM sys.dm_pdw_dms_workers   
WHERE type = 'PARALLEL_COPY_READER';  
```  
  
### <a name="c-using-a-query-join-hint-with-create-remote-table"></a>C. Usar una sugerencia de combinación de consulta con CREATE REMOTE TABLE  
 Esta consulta muestra la sintaxis básica para usar una sugerencia de combinación de consulta con CREATE REMOTE TABLE. Una vez enviada la consulta al nodo de control, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], que se ejecuta en los nodos de proceso, se aplica la estrategia de combinación hash al generar el plan de consulta de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Para obtener más información sobre las sugerencias de combinación y cómo usar la cláusula OPTION, vea [OPTION &#40;cláusula de Transact-SQL&#41;](../../t-sql/queries/option-clause-transact-sql.md).  
  
```  
USE ssawPDW;  
CREATE REMOTE TABLE OrderReporting.Orders.MyOrdersTable  
AT ( 'Data Source = SQLA, 1433; User ID = David; Password = e4n8@3;' )  
    AS SELECT T1.* FROM OrderReporting.Orders.MyOrdersTable T1   
    JOIN OrderReporting.Order.Customer T2  
    ON T1.CustomerID=T2.CustomerID OPTION (HASH JOIN);  
```  
  
  

