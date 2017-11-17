---
title: CREAR remoto tabla como SELECT (almacenamiento de datos en paralelo) | Documentos de Microsoft
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
caps.latest.revision: 9
author: barbkess
ms.author: barbkess
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: a0318d108d6dfaaa374af9a1ab8a148ff960dfcd
ms.contentlocale: es-es
ms.lasthandoff: 09/01/2017

---
# <a name="create-remote-table-as-select-parallel-data-warehouse"></a>CREAR remoto tabla como SELECT (almacenamiento de datos en paralelo)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-xxxx-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-xxxx-pdw-md.md)]

  Selecciona los datos de un [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] la base de datos y copia los datos en una nueva tabla en un SMP [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] base de datos en un servidor remoto. [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]usa el dispositivo, con todas las ventajas del procesamiento, para seleccionar los datos para la copia remota de las consultas MPP. Utilice esto para escenarios que requieren [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] funcionalidad.  
  
 Para configurar el servidor remoto, consulte "Copia de la tabla remota" en el [!INCLUDE[pdw-product-documentation](../../includes/pdw-product-documentation-md.md)].  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "icono de vínculo de tema") [convenciones de sintaxis de Transact-SQL &#40; Transact-SQL &#41;](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
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
 La base de datos para crear la tabla remota en. *database_name* es un [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] base de datos. Valor predeterminado es la base de datos predeterminada para el inicio de sesión de usuario en el destino [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] instancia.  
  
 *schema_name*  
 El esquema para la nueva tabla. Valor predeterminado es el esquema predeterminado para el inicio de sesión de usuario en el destino [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] instancia.  
  
 *table_name*  
 El nombre de la nueva tabla. Para obtener más información sobre permiten nombres de tabla, vea "Reglas de nomenclatura de objetos" en el [!INCLUDE[pdw-product-documentation](../../includes/pdw-product-documentation-md.md)].  
  
 La tabla remota se crea como un montón. No tiene desencadenadores o restricciones check. La intercalación de las columnas de la tabla remota es la misma que la intercalación de las columnas de tabla de origen. Esto se aplica a las columnas de tipo **char**, **nchar**, **varchar**, y **nvarchar**.  
  
 *conexión*  
 Una cadena de caracteres que especifica la `Data Source`, `User ID`, y `Password` parámetros para conectar con el servidor remoto y la base de datos.  
  
 La cadena de conexión es una lista delimitada por punto y coma de pares clave / valor. Palabras clave no distinguen entre mayúsculas y minúsculas. Se omiten los espacios entre los pares de clave y valor. Sin embargo, los valores pueden ser entre mayúsculas y minúsculas, según el origen de datos.  
  
 *Origen de datos*  
 Número de puerto del parámetro que especifica el nombre o dirección IP y TCP para SMP remoto [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 *nombre de host* o *dirección_IP*  
 Nombre del equipo servidor remoto o la dirección IPv4 del servidor remoto. No se admiten direcciones IPv6. Puede especificar un [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] con el nombre de instancia en el formato **nombreEquipo\nombreInstancia** o **IP_address\Instance_Name**. El servidor debe ser remoto y, por tanto, no se puede especificar como (local).  
  
 TCP *puerto* número  
 El número de puerto TCP para la conexión. Puede especificar un número de puerto TCP entre 0 y 65535 para una instancia de SQL Server que no está escuchando en el puerto 1433 predeterminado. Por ejemplo: **servidora, 1450** o **10.192.14.27,1435**  
  
> [!NOTE]  
>  Se recomienda conectarse a un servidor remoto mediante la dirección IP. Según la configuración de red, la conexión mediante el nombre del equipo puede requerir pasos adicionales para usar el servidor DNS no sea de dispositivo para resolver el nombre en el servidor correcto. Este paso no es necesario cuando se conecta con una dirección IP. Para obtener más información, vea "Usar un reenviador DNS para nombres DNS de resolución no dispositivo (Analytics Platform System)" en la [!INCLUDE[pdw-product-documentation](../../includes/pdw-product-documentation-md.md)].  
  
 *user_name*  
 Válido [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] nombre de inicio de sesión de autenticación. Número máximo de caracteres es 128.  
  
 *contraseña*  
 La contraseña de inicio de sesión. Número máximo de caracteres es 128.  
  
 *batch_size*  
 El número máximo de filas por lote. [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]envía las filas en lotes al servidor de destino. *Batch_size* es un entero positivo > = 0. Valor predeterminado es 0.  
  
 CON *common_table_expression*  
 Especifica un conjunto de resultados temporal con nombre, conocido como expresión de tabla común (CTE). Para obtener más información, consulte [con common_table_expression &#40; Transact-SQL &#41; ](../../t-sql/queries/with-common-table-expression-transact-sql.md).  
  
 Seleccione \<select_criteria > el predicado de consulta que especifica qué datos llenará la nueva tabla remota. Para obtener información sobre la instrucción SELECT, vea [SELECT &#40; Transact-SQL &#41; ](../../t-sql/queries/select-transact-sql.md).  
  
## <a name="permissions"></a>Permissions  
 Se necesita:  
  
-   Permiso SELECT en todos los objetos en la cláusula SELECT.  
  
-   Requiere el permiso CREATE TABLE en la base de datos SMP de destino.  
  
-   Requiere permisos SELECT en el esquema de destino SMP, INSERT y ALTER.  
  
## <a name="error-handling"></a>Tratamiento de errores  
 Si se produce un error en la copia de datos en la base de datos remota, [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] se anular la operación, registrará un error e intente eliminar la tabla remota. [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]no garantiza una limpieza correcta de la nueva tabla.  
  
## <a name="limitations-and-restrictions"></a>Limitaciones y restricciones  
 **Servidor de destino remoto**:  
  
-   TCP es el valor predeterminado y solo admite el protocolo para conectarse a un servidor remoto.  
  
-   El servidor de destino debe ser un servidor no sea de dispositivo. CREAR una tabla remota no puede utilizarse para copiar datos desde un dispositivo a otro.  
  
-   La instrucción CREATE TABLE remoto sólo crea tablas nuevas. Por lo tanto, no puede existir la nueva tabla. Ya deben existir la base de datos remota y el esquema.  
  
-   El servidor remoto debe disponer de espacio almacenar los datos que se transfieren desde el dispositivo a la [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] base de datos remota.  
  
 **Instrucción SELECT**:  
  
-   No se admiten las cláusulas ORDER BY y TOP en los criterios de selección.  
  
-   CREAR una tabla remota no se puede ejecutar dentro de una transacción activa o cuando está activa la configuración de confirmación automática desactivado para la sesión.  
  
 [SET ROWCOUNT &#40; Transact-SQL &#41; ](../../t-sql/statements/set-rowcount-transact-sql.md) no tiene ningún efecto en esta instrucción. Para lograr un comportamiento similar, utilice [TOP &#40; Transact-SQL &#41; ](../../t-sql/queries/top-transact-sql.md).  
  
## <a name="locking-behavior"></a>Comportamiento del bloqueo  
 Después de crear la tabla remota, la tabla de destino no está bloqueada hasta que se comienza a copiar. Por lo tanto, es posible que otro proceso Eliminar la tabla remota después de crearla y antes de que se comienza a copiar. Cuando esto ocurre, [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] generará un error y se producirá un error en la copia.  
  
## <a name="metadata"></a>Metadatos  
 Use [sys.dm_pdw_dms_workers &#40; Transact-SQL &#41; ](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-dms-workers-transact-sql.md) para ver el progreso de la copia de los datos seleccionados en el servidor remoto de SMP. Filas con el tipo PARALLEL_COPY_READER contienen esta información.  
  
## <a name="security"></a>Seguridad  
 CREAR una tabla remota utiliza [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] autenticación para conectarse a la instancia remota [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] instancia; no utiliza la autenticación de Windows.  
  
 El [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] red con orientación externa debe ser pasa, con excepción de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] puertos, puertos administrativos y los puertos de administración.  
  
 Para ayudar a evitar la pérdida accidental de datos o daños, la cuenta de usuario que se usa para copiar desde el dispositivo a la base de datos de destino debe tener los mínimos permisos necesarios en la base de datos de destino.  
  
 Configuración de conexión le permite conectarse a SMP [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] instancia con SSL protege los datos de nombre y la contraseña de usuario, pero con datos reales que se envían sin cifrados en texto no cifrado. Cuando esto ocurre, un usuario malintencionado podría interceptar el texto de la instrucción CREATE TABLE remoto, que contiene el [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] nombre de usuario y contraseña para iniciar sesión en SMP [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] instancia. Para evitar este riesgo, utilice el cifrado de datos en la conexión a SMP [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] instancia.  
  
##  <a name="Examples"></a> Ejemplos  
  
### <a name="a-creating-a-remote-table"></a>A. Crear una tabla remota  
 Este ejemplo se crea un [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tabla remota SMP denominada `MyOrdersTable` en la base de datos `OrderReporting` y el esquema `Orders`. El `OrderReporting` base de datos está en un servidor denominado `SQLA` que escucha en el puerto 1433 predeterminado. La conexión con el servidor utiliza las credenciales del usuario `David`, cuya contraseña es `e4n8@3`.  
  
```  
CREATE REMOTE TABLE OrderReporting.Orders.MyOrdersTable  
AT ( 'Data Source = SQLA, 1433; User ID = David; Password = e4n8@3;' )  
AS SELECT <select_criteria>;  
```  
  
### <a name="b-querying-the-sysdmpdwdmsworkers-dmv-for-remote-table-copy-status"></a>B. Consultar la DMV sys.dm_pdw_dms_workers para el estado de la copia de tabla remota  
 Esta consulta muestra cómo ver el estado de copia de una copia de la tabla remota.  
  
```  
SELECT * FROM sys.dm_pdw_dms_workers   
WHERE type = 'PARALLEL_COPY_READER';  
```  
  
### <a name="c-using-a-query-join-hint-with-create-remote-table"></a>C. Utilizar una sugerencia de combinación de la consulta con CREATE TABLE remoto  
 Esta consulta muestra la sintaxis básica para utilizar una sugerencia de combinación de la consulta con CREATE TABLE remoto. Después de la consulta se envía al nodo de Control, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], ejecute en los nodos de proceso, se aplicará la estrategia de combinación hash al generar el [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] plan de consulta. Para obtener más información sobre las sugerencias de combinación y cómo usar la cláusula OPTION, consulte [cláusula OPTION &#40; Transact-SQL &#41; ](../../t-sql/queries/option-clause-transact-sql.md).  
  
```  
USE ssawPDW;  
CREATE REMOTE TABLE OrderReporting.Orders.MyOrdersTable  
AT ( 'Data Source = SQLA, 1433; User ID = David; Password = e4n8@3;' )  
    AS SELECT T1.* FROM OrderReporting.Orders.MyOrdersTable T1   
    JOIN OrderReporting.Order.Customer T2  
    ON T1.CustomerID=T2.CustomerID OPTION (HASH JOIN);  
```  
  
  


