---
title: Catálogo de base de datos WideWorldImporters OLTP - SQL | Microsoft Docs
ms.prod: sql
ms.prod_service: sql
ms.technology: samples
ms.custom: ''
ms.date: 04/04/2018
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 35228d6773e576b2d8b062c94aa8797d07f00809
ms.sourcegitcommit: e77197ec6935e15e2260a7a44587e8054745d5c2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2018
ms.locfileid: "38000667"
---
# <a name="wideworldimporters-database-catalog"></a>Catálogo de base de datos de WideWorldImporters
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
La base de datos WideWorldImporters contiene todos los la información de transacciones y datos diaria para ventas y compras, así como datos de detección de los vehículos y salas en frío.

## <a name="schemas"></a>Esquemas

WideWorldImporters utiliza esquemas para fines diferentes, como almacenamiento de datos, definir cómo los usuarios pueden acceder a los datos y proporcionar objetos de integración y desarrollo de almacén de datos.

### <a name="data-schemas"></a>Esquemas de datos

Estos esquemas contienen los datos. Un número de tablas es necesarios para todos los demás esquemas y se encuentra en el esquema de la aplicación.

|esquema|Descripción|
|-----------------------------|---------------------|
|Aplicación|Toda la aplicación a los usuarios, contactos y parámetros. Esta vista también contiene tablas de referencia con datos que se utilizan varios esquemas|
|Purchasing|Artículo comercial se adquiere de proveedores y los detalles sobre los proveedores.|  
|Sales|Elemento ventas a clientes particulares y detalles acerca de las personas de ventas y clientes de existencias. |  
|Warehouse|Elemento existencias de inventario y las transacciones.|  

### <a name="secure-access-schemas"></a>Acceso seguro a los esquemas

Estos esquemas se utilizan para las aplicaciones externas que no se permiten tener acceso directamente a las tablas de datos. Que contienen las vistas y procedimientos almacenados utilizados por las aplicaciones externas.

|esquema|Descripción|
|-----------------------------|---------------------|
|Sitio web|Todo el acceso a la base de datos desde el sitio Web de la empresa es a través de este esquema.|
|Informes|Todo el acceso a la base de datos de informes de Reporting Services es a través de este esquema.|
|Power BI|Todo el acceso a la base de datos de los paneles de Power BI a través de la puerta de enlace empresarial es a través de este esquema.|

Tenga en cuenta que los informes y Power BI no se utilizan en la versión inicial de la base de datos de ejemplo. Sin embargo, los ejemplos de todos los servicios de informes y Power BI creados a partir de esta base de datos se recomienda usar estos esquemas.

### <a name="development-schemas"></a>Esquemas de desarrollo

Esquemas de propósito especial

|esquema|Descripción|
|-----------------------------|---------------------|
|Integración|Objetos y procedimientos necesarios para la integración de almacén de datos (es decir, migrar los datos a la base de datos WideWorldImportersDW).|
|Secuencias|Contiene secuencias utilizadas por todas las tablas de la aplicación.|

## <a name="tables"></a>Tablas

Todas las tablas de la base de datos están en los esquemas de datos.

### <a name="application-schema"></a>Esquema de la aplicación

Detalles de los parámetros y las personas (usuarios y contactos), junto con las tablas de referencia comunes (comunes a varios otros esquemas).

|Table|Descripción|
|-----------------------------|---------------------|
|SystemParameters|Contiene los parámetros configurables de todo el sistema.|
|Personas|Contiene los nombres de usuario, información de contacto para todos los que usan la aplicación y para las personas que se ocupa de Wide World Importers en organizaciones de clientes. Esto incluye personal, los clientes, proveedores y otros contactos. Para las personas que tienen permiso para usar el sistema o el sitio Web, la información incluye detalles de inicio de sesión.|
|Ciudades|Hay muchas direcciones almacenadas en el sistema, para las personas, direcciones de entrega de la organización de cliente, las direcciones de recogida en proveedores, etcetera. Cada vez que se almacena una dirección, hay una referencia a una ciudad en esta tabla. También es una ubicación espacial para cada ciudad.|
|StateProvinces|Ciudades forman parte de los Estados o provincias. Esta tabla tiene detalles de ellas, como los datos espaciales que describe los límites de cada estado o provincia.|
|Países|Los Estados o provincias forman parte de los países. Esta tabla tiene información sobre ellas, como los datos espaciales que describe los límites de cada país.|
|DeliveryMethods|Alternativas para entregar los elementos estándar (por ejemplo, camión/van, post, pickup, courier, etcetera.)|
|PaymentMethods|Opciones de pago (por ejemplo, efectivo, cheque, EFT, etcetera.)|
|TransactionTypes|Tipos de cliente, proveedor o las transacciones de existencias (p. ej., factura, nota de crédito, etcetera.)|

### <a name="purchasing-schema"></a>Esquema de la compra

Detalles de proveedores y de las compras de artículo comercial.

|Table|Descripción|
|-----------------------------|---------------------|
|Suppliers|Tabla de la entidad principal para proveedores (organizaciones)|
|SupplierCategories|Categorías de proveedores (p. ej., sorpresa, juguetes, ropa, empaquetado, etcetera.)|
|SupplierTransactions|Todas las transacciones financieras que están relacionados con el proveedor (facturas, pagos)|
|PurchaseOrders|Detalles de pedidos de compra del proveedor|
|PurchaseOrderLines|Líneas de detalles del proveedor de pedidos de compra|

 
### <a name="sales-schema"></a>Esquema de ventas

Detalles de los clientes, vendedores y de ventas de artículos estándar.

|Table|Descripción|
|-----------------------------|---------------------|
|Clientes|Tablas de la entidad principal para los clientes (organizaciones o individuos)|
|CustomerCategories|Categorías para los clientes (es decir novedad almacenes, supermercados, etcetera.)|
|BuyingGroups|Organizaciones de clientes pueden formar parte de grupos que ejercer mayor poder de compra|
|CustomerTransactions|Todas las transacciones financieras que están relacionados con clientes (facturas, pagos)|
|SpecialDeals|Precio especial. Esto puede incluir precios fijos, de descuento en dólares o el porcentaje de descuento.|
|Orders|Detalle de pedidos de cliente|
|OrderLines|Líneas de detalles de pedidos de cliente|
|Facturas|Detalles de facturas de cliente|
|InvoiceLines|Líneas de detalles de facturas de cliente|

### <a name="warehouse-schema"></a>Esquema de almacenamiento

Detalles de artículos de stock holdings y sus transacciones.

|Table|Descripción|
|-----------------------------|---------------------|
|StockItems|Tabla de la entidad principal para los elementos estándar|
|StockItemHoldings|Columnas no temporal para los elementos estándar. Estas son las columnas actualizadas con frecuencia.|
|StockGroups|Grupos para clasificar los elementos de cotizaciones (p. ej., sorpresa, juguetes, comestible sorpresa, etcetera.)|
|StockItemStockGroups|Los elementos que cotizaciones están en el que agrupa stock (varios a varios)|
|Colores|Elementos de cotizaciones (opcionalmente) pueden tener los colores|
|PackageTypes|Se pueden empaquetar maneras en que los elementos de cotizaciones (p. ej., cuadro, sobre el embalaje, paleta, kg, etcetera.|
|StockItemTransactions|Transacciones que abarcan todos los movimientos de todos los elementos de cotizaciones (recepción, la venta, cancelación)|
|VehicleTemperatures|Grabado con regularidad las temperaturas de los refrigeradores de vehículo|
|ColdRoomTemperatures|Periódicamente se registran las temperaturas de los refrigeradores salón en frío|


## <a name="design-considerations"></a>Consideraciones de diseño

Diseño de base de datos es subjetivo y no hay ninguna manera correcta o errónea de diseñar una base de datos. Los esquemas y tablas en esta base de datos muestran ideas sobre cómo puede diseñar su propia base de datos.

### <a name="schema-design"></a>Diseño de esquema

WideWorldImporters usa un pequeño número de esquemas para que resulte fácil de entender el sistema de base de datos y muestran principios de la base de datos.  

Siempre que sea posible, la base de datos coloca las tablas que suelen consultarse juntas en el mismo esquema para minimizar la complejidad de la combinación.

El esquema de base de datos ha sido generadas por el código según una serie de tablas de metadatos en otra base de datos WWI_Preparation. Esto proporciona WideWorldImporters un grado muy alto de la coherencia del diseño, nomenclatura coherencia e integridad. Para obtener más información sobre cómo se ha generado el esquema, vea el código fuente: [todo el mundo-importadores/wwi-base de datos-secuencias de comandos](https://github.com/Microsoft/sql-server-samples/tree/master/samples/databases/wide-world-importers/sample-scripts)

### <a name="table-design"></a>Diseño de tabla

- Todas las tablas tienen claves principales de columna única por motivos de simplicidad de combinación.
- Todos los esquemas, tablas, columnas, índices y restricciones check tienen una descripción de propiedad que se puede usar para identificar el propósito del objeto o columna extendida. Las tablas optimizadas para memoria son una excepción a esto ya que actualmente no admiten las propiedades extendidas.
- Todas las claves externas se indizan automáticamente a menos que haya otro índice no agrupado que tiene el mismo componente de la izquierda.
- Numeración automática en las tablas se basa en secuencias. Estas secuencias están más fáciles trabajar con entre servidores vinculados y los entornos similares a las columnas de identidad. Las tablas optimizadas para memoria usan columnas de identidad ya que no se admiten en SQL Server 2016.
- Se utiliza una única secuencia (TransactionID) para estas tablas: CustomerTransactions, SupplierTransactions y StockItemTransactions. Este ejemplo muestra cómo un conjunto de tablas puede tener una única secuencia.
- Algunas columnas tienen valores predeterminados adecuados.

### <a name="security-schemas"></a>Esquemas de seguridad

Para la seguridad, WideWorldImporters no permite que aplicaciones externas para tener acceso directamente a los esquemas de datos. Para aislar el acceso, WideWorldImporters utiliza los esquemas de acceso de seguridad que no contienen datos, pero contiene vistas y procedimientos almacenados. Las aplicaciones externas utilizan los esquemas de seguridad para recuperar los datos que se pueden ver.  De este modo, los usuarios pueden sólo ejecutar las vistas y procedimientos almacenados en los esquemas de acceso seguro

Por ejemplo, este ejemplo incluye los paneles de Power BI. Una aplicación externa obtiene acceso a estos paneles de Power BI desde la puerta de enlace de Power BI como un usuario que tenga permiso de solo lectura en el esquema de Power BI.  Para obtener permiso de solo lectura, el usuario solo necesita permiso SELECT y EXECUTE en el esquema de Power BI. Un administrador de base de datos de WWI asigna estos permisos según sea necesario.

## <a name="stored-procedures"></a>Procedimientos almacenados

Los procedimientos almacenados se organizan en esquemas. La mayoría de los esquemas se utiliza para la configuración o con fines de ejemplo.

El `Website` esquema contiene los procedimientos almacenados que pueden utilizarse por un front-end Web.

El `Reports` y `PowerBI` esquemas están diseñados para reporting services y con fines de Power BI. Las extensiones de la muestra se recomienda usar estos esquemas con fines informativos.

### <a name="website-schema"></a>Esquema del sitio Web

Estos son los procedimientos utilizados por una aplicación cliente, como un front-end Web.

|Procedimiento|Finalidad|
|-----------------------------|---------------------|
|ActivateWebsiteLogon|Permite a una persona (desde `Application.People`) para tener acceso al sitio Web.|
|ChangePassword|Cambia una contraseña de usuario (para usuarios que no usan mecanismos de autenticación externos).|
|InsertCustomerOrders|Permite insertar uno o varios de los pedidos de cliente (incluidas las líneas de pedido).|
|InvoiceCustomerOrders|Toma una lista de pedidos que se va a facturar y procesa las facturas.|
|RecordColdRoomTemperatures|Toma una lista de datos del sensor, como un parámetro con valores de tabla (TVP) y se aplica a los datos a la `Warehouse.ColdRoomTemperatures` tabla temporal.|
|RecordVehicleTemperature|Toma una matriz JSON y lo usa para actualizar `Warehouse.VehicleTemperatures`.|
|SearchForCustomers|Busca los clientes por nombre o parte del nombre (el nombre de la empresa o el nombre de persona).|
|SearchForPeople|Busca personas por nombre o parte del nombre.|
|SearchForStockItems|Busca elementos cotizaciones por nombre o parte del nombre o los comentarios de marketing.|
|SearchForStockItemsByTags|Busca elementos cotizaciones por etiquetas.|
|SearchForSuppliers|Busca proveedores por nombre o parte del nombre (el nombre de la empresa o el nombre de persona).|

### <a name="integration-schema"></a>Esquema de la integración

Los procedimientos almacenados en este esquema se utilizan el proceso ETL. Obtienen los datos necesarios de varias tablas para el período de tiempo requerido por la [paquete ETL](wide-world-importers-perform-etl.md).

### <a name="dataloadsimulation-schema"></a>Esquema DataLoadSimulation

Simula una carga de trabajo que inserta las compras y ventas. El procedimiento almacenado principal es `PopulateDataToCurrentDate`, que se usa para insertar datos de ejemplo hasta la fecha actual.

|Procedimiento|Finalidad|
|-----------------------------|---------------------|
|Configuration_ApplyDataLoadSimulationProcedures|Vuelve a crear los procedimientos necesarios para datos de simulación de carga. Esto es necesario para llevar los datos a la fecha actual.|
|Configuration_RemoveDataLoadSimulationProcedures|Esto quita los procedimientos de nuevo una vez completada la simulación de datos.|
|DeactiveTemporalTablesBeforeDataLoad|Quita la naturaleza temporal de todas las tablas temporales y si procede, se aplica un desencadenador para que se pueden realizar cambios como si se han aplicado en una fecha antes de permitir que las tablas temporales y sys.|
|PopulateDataToCurrentDate|Se usa para incorporar los datos hasta la fecha actual. Se debe ejecutar antes de otras opciones de configuración después de restaurar la base de datos desde una copia de seguridad inicial.|
|ReactivateTemporalTablesAfterDataLoad|Restablece las tablas temporales, como la comprobación de coherencia de los datos. (Quita los desencadenadores asociados).|


### <a name="application-schema"></a>Esquema de la aplicación

Estos procedimientos se usan para configurar el ejemplo. Se utilizan para aplicar las características de enterprise edition a la versión de standard edition de la muestra y también para agregar la auditoría y la indización de texto completo.

|Procedimiento|Finalidad|
|-----------------------------|---------------------|
|AddRoleMemberIfNonexistant|Agrega a un miembro a una función de si el miembro no está en el rol|
|Configuration_ApplyAuditing|Agrega la auditoría. Auditoría de servidor se aplica a bases de datos de la edición standard; auditoría de base de datos adicional se agrega para enterprise edition.|
|Configuration_ApplyColumnstoreIndexing|Se aplica la indización para el almacén de columnas `Sales.OrderLines` y `Sales.InvoiceLines` y vuelve a indizar apropiadamente.|
|Configuration_ApplyFullTextIndexing|Se aplica a los índices de texto completo para `Application.People`, `Sales.Customers`, `Purchasing.Suppliers`, y `Warehouse.StockItems`. Reemplaza `Website.SearchForPeople`, `Website.SearchForSuppliers`, `Website.SearchForCustomers`, `Website.SearchForStockItems`, `Website.SearchForStockItemsByTags` con los procedimientos de reemplazo que usar indización de texto completo.|
|Configuration_ApplyPartitioning|Se aplica a las particiones de tablas `Sales.CustomerTransactions and `'Purchasing.SupplierTransactions y reorganiza los índices para satisfacer.|
|Configuration_ApplyRowLevelSecurity|Se aplica la seguridad de nivel de fila para filtrar los clientes por ventas funciones relacionadas de territorio.|
|Configuration_ConfigureForEnterpriseEdition|Se aplica la indexación de almacén de columnas, texto completo, en memoria, polybase y creación de particiones.|
|Configuration_EnableInMemory|Agrega un grupo de archivos optimizados para memoria (cuando no trabaja en Azure), reemplaza `Warehouse.ColdRoomTemperatures`, `Warehouse.VehicleTemperatures` por sus equivalentes en memoria y migra los datos, se vuelve a crear la `Website.OrderIDList`, `Website.OrderList`, `Website.OrderLineList`, `Website.SensorDataList` con los tipos de tabla optimizado para memoria equivalentes, quita y vuelve a crear los procedimientos `Website.InvoiceCustomerOrders`, `Website.InsertCustomerOrders`, y `Website.RecordColdRoomTemperatures` que usa estos tipos de tabla.|
|Configuration_RemoveAuditing|Quita la configuración de auditoría.|
|Configuration_RemoveRowLevelSecurity|Quita la configuración de seguridad de nivel de fila (Esto es necesario para los cambios realizados en las tablas asociadas).|
|CreateRoleIfNonExistant|Crea un rol de base de datos si aún no existe.|


### <a name="sequences-schema"></a>Esquema de secuencias

Procedimientos para configurar las secuencias en la base de datos.

|Procedimiento|Finalidad|
|-----------------------------|---------------------|
|ReseedAllSequences|Llama al procedimiento ReseedSequenceBeyondTableValue para todas las secuencias.|
|ReseedSequenceBeyondTableValue|Se utiliza para volver a colocar el siguiente valor de secuencia por encima del valor en cualquier tabla que usa la misma secuencia. (Por ejemplo, un DBCC CHECKIDENT para equivalente de columnas de identidad para las secuencias, pero en potencialmente varias tablas).|
