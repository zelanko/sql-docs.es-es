---
title: "Catálogo de base de datos | Documentos de Microsoft"
ms.prod: sql-non-specified
ms.technology:
- samples
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: e47c0022-ce87-4ba5-a24b-df55efe66431
caps.latest.revision: 3
author: BarbKess
ms.author: barbkess
manager: jhubbard
robots: noindex,nofollow
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: f34a56282f5901fe13131cdd2e1c688054fca85f
ms.contentlocale: es-es
ms.lasthandoff: 08/02/2017

---
# <a name="database-catalog"></a>Catálogo de base de datos
La base de datos WideWorldImporters contiene todos los la información de las transacciones y datos diarios para ventas y compras, así como datos de detección de vehículos y salones inactivos.

## <a name="schemas"></a>Esquemas

WideWorldImporters utiliza esquemas para propósitos diferentes, como almacenamiento de datos, definir cómo los usuarios pueden tener acceso a los datos y proporcionar objetos para la integración y el desarrollo de almacenamiento de datos.

### <a name="data-schemas"></a>Esquemas de datos

Estos esquemas contienen los datos. Un número de tablas es necesarios para todos los otros esquemas y se encuentra en el esquema de la aplicación.

|Esquema|Description|
|-----------------------------|---------------------|
|Aplicación|Toda la aplicación a los usuarios, contactos y parámetros. Esto también contiene tablas de referencia con datos que se utilizan por varios esquemas|
|Purchasing|Elemento en existencias adquiere de proveedores y los detalles sobre los proveedores.|  
|Sales|Elemento ventas a clientes particulares y detalles acerca de las personas de los clientes y las ventas de existencias. |  
|Warehouse|Inventario de los artículos estándar y las transacciones.|  

### <a name="secure-access-schemas"></a>Esquemas de acceso seguro

Estos esquemas se utilizan para las aplicaciones externas que no pueden tener acceso directamente a las tablas de datos. Contienen vistas y procedimientos almacenados utilizados por las aplicaciones externas.

|Esquema|Description|
|-----------------------------|---------------------|
|Sitio web|Todo el acceso a la base de datos desde el sitio Web de la empresa es a través de este esquema.|
|Informes|Todo el acceso a la base de datos de informes de Reporting Services es a través de este esquema.|
|Power BI|Todo el acceso a la base de datos de los paneles de Power BI a través de la puerta de enlace empresarial es a través de este esquema.|

Tenga en cuenta que los informes y Power BI no se utilizan en la versión inicial de la base de datos de ejemplo. Sin embargo, los ejemplos de todos los servicios de informes y Power BI creados a partir de esta base de datos se les recomienda usar estos esquemas.

### <a name="development-schemas"></a>Esquemas de desarrollo

Esquemas de propósito especial

|Esquema|Description|
|-----------------------------|---------------------|
|Integración|Objetos y procedimientos necesarios para la integración de almacenamiento de datos (es decir, migrar los datos a la base de datos de WideWorldImportersDW).|
|Secuencias|Contiene secuencias que se utilizan por todas las tablas de la aplicación.|

## <a name="tables"></a>Tablas

Todas las tablas de la base de datos están en los esquemas de datos.

### <a name="application-schema"></a>Esquema de la aplicación

Detalles de los parámetros y usuarios (usuarios y contactos), junto con las tablas de referencia comunes (comunes a varios otros esquemas).

|Table|Description|
|-----------------------------|---------------------|
|SystemParameters|Contiene los parámetros configurables de todo el sistema.|
|personas|Contiene los nombres de usuario, información de contacto para todos los usuarios que usan la aplicación y para las personas con las que se encarga de Wide World Importers con en organizaciones de clientes. Esto incluye personal, los clientes, proveedores y los otros contactos. Para las personas que tienen permiso para usar el sistema o el sitio Web, la información incluye detalles de inicio de sesión.|
|Ciudades|Hay muchas direcciones almacenadas en el sistema, para las personas, direcciones de entrega de la organización de cliente, direcciones recogidas en proveedores, etcetera. Cada vez que se almacena una dirección, hay una referencia a una ciudad en esta tabla. También es una ubicación espacial para cada ciudad.|
|StateProvinces|Ciudades forman parte de los Estados o provincias. Esta tabla con información detallada sobre ellas, como los datos espaciales que describe los límites de cada estado o provincia.|
|Países|Los Estados o provincias forman parte de los países. Esta tabla con información detallada sobre ellas, como los datos espaciales que describe los límites de cada país.|
|DeliveryMethods|Opciones de entrega de elementos estándar (p. ej., camión/van, post, recogida, courier, etcetera.)|
|PaymentMethods|Opciones para hacer que los pagos (por ejemplo, efectivo, cheque, EFT, etcetera.)|
|TransactionTypes|Tipos de cliente, proveedor o las transacciones de existencias (p. ej., factura, nota de crédito, etcetera.)|

### <a name="purchasing-schema"></a>Compra de esquema

Detalles de proveedores y de las compras de artículos estándar.

|Table|Description|
|-----------------------------|---------------------|
|Suppliers|Tabla de la entidad principal para proveedores (entidades)|
|SupplierCategories|Categorías de proveedores (p. ej., sorpresa, juguetes, ropa, empaquetado, etcetera.)|
|SupplierTransactions|Todas las transacciones financieras que están relacionados con el proveedor (facturas, pagos)|
|PurchaseOrders|Detalles de pedidos de compra de proveedor|
|PurchaseOrderLines|Pedidos de compra de las líneas de detalle de proveedor|

 
### <a name="sales-schema"></a>Esquema de ventas

Detalles de clientes, vendedores y de ventas de artículos estándar.

|Table|Description|
|-----------------------------|---------------------|
|Clientes|Tablas de la entidad principal para los clientes (organizaciones o individuos)|
|CustomerCategories|Categorías de los clientes (es decir novedad tiendas, supermercados, etcetera.)|
|BuyingGroups|Organizaciones de clientes pueden formar parte de grupos que ejercen mayor potencia de compra|
|CustomerTransactions|Todas las transacciones financieras que están relacionados con el cliente (facturas, pagos)|
|SpecialDeals|Un precio especial. Esto puede incluir precios fijos, el descuento en dólares o como porcentaje de descuento.|
|Orders|Detalles de pedidos de cliente|
|OrderLines|Líneas de detalle de pedidos de cliente|
|Facturas|Detalles de facturas de cliente|
|InvoiceLines|Líneas de detalle de facturas de cliente|

### <a name="warehouse-schema"></a>Esquema de almacenamiento

Detalles de elementos de cotizaciones, sus explotaciones y transacciones.

|Table|Description|
|-----------------------------|---------------------|
|StockItems|Tabla de la entidad principal para los elementos estándar|
|StockItemHoldings|Columnas no temporales para los elementos estándar. Estas columnas arefrequently actualizado.|
|StockGroups|Grupos para clasificar los elementos estándar (p. ej., sorpresa, juguetes, sorpresa comestible, etcetera)|
|StockItemStockGroups|Qué elementos estándar se encuentran en el que agrupa existencias (varios a varios)|
|Colores|Elementos de cotizaciones (opcionalmente) pueden tener colores|
|PackageTypes|Se pueden empaquetar maneras que almacenar artículos (p. ej., cuadro, caja, palet, kg, etcetera.|
|StockItemTransactions|Transacciones que abarcan todos los movimientos de todos los elementos de cotizaciones (recepción, la venta, cancelación)|
|VehicleTemperatures|Temperaturas con regularidad grabadas de enfriadores de vehículo|
|ColdRoomTemperatures|Con regularidad registran temperaturas de enfriadores sala inactivos|


## <a name="design-considerations"></a>Consideraciones de diseño

Diseño de base de datos es subjetivo y no hay ninguna manera correcta o incorrecta para diseñar una base de datos. Las tablas de esta base de datos y esquemas mostrar ideas sobre cómo puede diseñar su propia base de datos.

### <a name="schema-design"></a>Diseño de esquema

WideWorldImporters utiliza un número pequeño de esquemas para que resulte fácil de entender el sistema de base de datos y muestran los principios de la base de datos.  

Siempre que sea posible, la base de datos coloca las tablas que habitualmente se consultan juntos en el mismo esquema para minimizar la complejidad de la combinación.

El esquema de base de datos ha sido generado por el código en función de una serie de tablas de metadatos en otra base de datos WWI_Preparation. Esto proporciona WideWorldImporters un elevado grado de coherencia de diseño, nomenclatura coherencia e integridad. Para obtener más información sobre cómo se ha generado el esquema, vea el código fuente: [todo el mundo-importadores/wwi-base de datos-secuencias de comandos](https://github.com/Microsoft/sql-server-samples/tree/master/samples/databases/wide-world-importers/wwi-database-scripts)

### <a name="table-design"></a>Diseño de tabla

- Todas las tablas con claves principales de columna única por motivos de simplicidad de combinación.
- Todos los esquemas, tablas, columnas, índices y restricciones check tienen una descripción de la propiedad que puede usarse para identificar el propósito del objeto o columna extendida. Tablas optimizadas en memoria son una excepción a esto ya que no admitan actualmente las propiedades extendidas.
- Todas las claves externas se indizan automáticamente a menos que haya otro índice no clúster que tenga el mismo componente izquierdo.
- Numeración automática en las tablas se basa en secuencias. Estas secuencias son más fáciles de trabajar con entre los servidores vinculados y entornos similares a las columnas de identidad. Tablas optimizadas en memoria utilizan las columnas de identidad ya que no admiten en SQL Server 2016.
- Una única secuencia (TransactionID) se usa para estas tablas: CustomerTransactions, SupplierTransactions y StockItemTransactions. Esto demuestra cómo un conjunto de tablas puede tener una única secuencia.
- Algunas columnas tienen valores predeterminados adecuados.

### <a name="security-schemas"></a>Esquemas de seguridad

Para la seguridad, WideWorldImporters no permite acceso directo a los esquemas de los datos de las aplicaciones externas. Para aislar el acceso, WideWorldImporters utiliza los esquemas de acceso de seguridad que no contienen datos, pero contienen vistas y procedimientos almacenados. Las aplicaciones externas utilizan los esquemas de seguridad para recuperar los datos que se pueden ver.  De esta manera, los usuarios solo pueden ejecutar las vistas y procedimientos almacenados en los esquemas de acceso seguro

Por ejemplo, este ejemplo incluye los paneles de Power BI. Una aplicación externa obtiene acceso a estos paneles de Power BI de la puerta de enlace de Power BI como un usuario que tenga permiso de solo lectura en el esquema de Power BI.  Para obtener permiso de solo lectura, el usuario solo necesita el permiso SELECT y EXECUTE en el esquema de Power BI. Un administrador de base de datos en WWI asigna estos permisos según sea necesario.

## <a name="stored-procedures"></a>Procedimientos almacenados

Los procedimientos almacenados se organizan en esquemas. La mayoría de los esquemas se utiliza para la configuración o con fines de ejemplo.

El `Website` esquema contiene los procedimientos almacenados que pueden usarse en un front-end Web.

El `Reports` y `PowerBI` esquemas están diseñados para reporting services y con fines de Power BI. Las extensiones de la muestra se les recomienda usar estos esquemas con fines informativos.

### <a name="website-schema"></a>Esquema de sitio Web

Se trata de los procedimientos empleados en una aplicación de cliente, como un front-end Web.

|Procedimiento|Finalidad|
|-----------------------------|---------------------|
|ActivateWebsiteLogon|Permite que una persona (desde `Application.People`) para tener acceso al sitio Web.|
|ChangePassword|Cambia una contraseña de usuario (para los usuarios que no usan mecanismos de autenticación externo).|
|InsertCustomerOrders|Permite insertar uno o varios de los pedidos de cliente (incluidas las líneas de pedido).|
|InvoiceCustomerOrders|Toma una lista de pedidos que se va a facturar y procesa las facturas.|
|RecordColdRoomTemperatures|Toma una lista de datos de sensor, como un parámetro con valores de tabla (TVP) y se aplica a los datos a la `Warehouse.ColdRoomTemperatures` tabla temporal.|
|RecordVehicleTemperature|Toma una matriz JSON y lo utiliza para actualizar `Warehouse.VehicleTemperatures`.|
|SearchForCustomers|Busca los clientes por nombre o parte del nombre (el nombre de la empresa o el nombre de persona).|
|SearchForPeople|Busca personas por nombre o parte del nombre.|
|SearchForStockItems|Busca artículos agotados por nombre o parte del nombre o los comentarios de marketing.|
|SearchForStockItemsByTags|Busca artículos agotados por etiquetas.|
|SearchForSuppliers|Busca proveedores por nombre o parte del nombre (el nombre de la empresa o el nombre de persona).|

### <a name="integration-schema"></a>Esquema de integración

Los procedimientos almacenados en este esquema se utilizan el proceso ETL. Obtienen los datos necesarios de varias tablas para el período de tiempo necesario para la [paquete ETL](https://msdn.microsoft.com/library/mt734218.aspx).

### <a name="dataloadsimulation-schema"></a>Esquema de DataLoadSimulation

Simula una carga de trabajo que inserta las compras y ventas. El procedimiento almacenado principal es `PopulateDataToCurrentDate`, que se utiliza para insertar datos de ejemplo hasta la fecha actual.

|Procedimiento|Finalidad|
|-----------------------------|---------------------|
|Configuration_ApplyDataLoadSimulationProcedures|Vuelve a crear los procedimientos necesarios para datos de simulación de carga. Esto es necesario para poner los datos hasta la fecha actual.|
|Configuration_RemoveDataLoadSimulationProcedures|Esto quita los procedimientos de nuevo una vez completada la simulación de datos.|
|DeactiveTemporalTablesBeforeDataLoad|Quita la naturaleza temporal de todas las tablas temporales y si procede, se aplica un desencadenador para que se pueden realizar cambios como si se han aplicado a una fecha anterior de permitir que las tablas temporales y sys.|
|PopulateDataToCurrentDate|Se usa para incorporar los datos hasta la fecha actual. Debe ejecutarse antes de otras opciones de configuración después de restaurar la base de datos desde una copia de seguridad inicial.|
|ReactivateTemporalTablesAfterDataLoad|Restablece las tablas temporales, incluida la comprobación de coherencia de los datos. (Quita los desencadenadores asociados).|


### <a name="application-schema"></a>Esquema de la aplicación

Estos procedimientos se utilizan para configurar el ejemplo. Se utilizan para aplicar características de la edición enterprise a la versión de edición estándar de la muestra así como agregar auditoría y la indización de texto completo.

|Procedimiento|Finalidad|
|-----------------------------|---------------------|
|AddRoleMemberIfNonexistant|Agrega a un miembro a un rol si el miembro no se encuentra en la función|
|Configuration_ApplyAuditing|Agrega la auditoría. Auditoría de servidor se aplica a las bases de datos de edición standard; auditoría de base de datos adicional se agrega para enterprise edition.|
|Configuration_ApplyColumnstoreIndexing|Se aplica la indización para el almacén de columnas `Sales.OrderLines` y `Sales.InvoiceLines` e indexar adecuadamente.|
|Configuration_ApplyFullTextIndexing|Se aplica a los índices de texto completo a `Application.People`, `Sales.Customers`, `Purchasing.Suppliers`, y `Warehouse.StockItems`. Reemplaza `Website.SearchForPeople`, `Website.SearchForSuppliers`, `Website.SearchForCustomers`, `Website.SearchForStockItems`, `Website.SearchForStockItemsByTags` con los procedimientos de reemplazo que utilizan la indización de texto completo.|
|Configuration_ApplyPartitioning|Se aplica a la partición de tablas `Sales.CustomerTransactions and `'Purchasing.SupplierTransactions y reorganiza los índices para satisfacer.|
|Configuration_ApplyRowLevelSecurity|Se aplica la seguridad de nivel de fila para filtrar los clientes por ventas territorio funciones relacionadas.|
|Configuration_ConfigureForEnterpriseEdition|Se aplica la indización de almacén de columnas, texto completo, en memoria, polybase y particiones.|
|Configuration_EnableInMemory|Agrega un grupo de archivos con optimización para memoria (cuando no trabaje en Azure), reemplaza `Warehouse.ColdRoomTemperatures`, `Warehouse.VehicleTemperatures` con equivalentes en memoria y migra los datos, vuelve a crear la `Website.OrderIDList`, `Website.OrderList`, `Website.OrderLineList`, `Website.SensorDataList` tipos de tabla con optimización para memoria equivalentes, quita y vuelve a crear los procedimientos `Website.InvoiceCustomerOrders`, `Website.InsertCustomerOrders`, y `Website.RecordColdRoomTemperatures` que usa estos tipos de tabla.|
|Configuration_RemoveAuditing|Quita la configuración de auditoría.|
|Configuration_RemoveRowLevelSecurity|Quita la configuración de seguridad de nivel de fila (Esto es necesario para los cambios en las tablas asociadas).|
|CreateRoleIfNonExistant|Crea un rol de base de datos si aún no existe.|


### <a name="sequences-schema"></a>Esquema de secuencias

Procedimientos para configurar las secuencias en la base de datos.

|Procedimiento|Finalidad|
|-----------------------------|---------------------|
|ReseedAllSequences|Llama al procedimiento ReseedSequenceBeyondTableValue para todas las secuencias.|
|ReseedSequenceBeyondTableValue|Se utiliza para volver a colocar el siguiente valor de secuencia por encima del valor de cualquier tabla que usa la misma secuencia. (Por ejemplo, una DBCC CHECKIDENT para equivalente de columnas de identidad para las secuencias pero entre varias tablas potencialmente).|

