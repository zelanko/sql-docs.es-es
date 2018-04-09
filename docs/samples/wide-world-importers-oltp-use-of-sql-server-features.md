---
title: Uso de características de SQL Server y capacidades | Documentos de Microsoft
ms.prod: sql-non-specified
ms.prod_service: sql-non-specified
ms.service: ''
ms.component: samples
ms.technology:
- samples
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 06f89721-8478-4abc-8ada-e9c73b08bf51
caps.latest.revision: 2
author: BarbKess
ms.author: barbkess
manager: craigg
robots: noindex,nofollow
ms.workload: Inactive
ms.openlocfilehash: d7d50fda2571b90205fbb18aadfb858615ad4f0b
ms.sourcegitcommit: d6b1695c8cbc70279b7d85ec4dfb66a4271cdb10
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/08/2018
---
# <a name="use-of-sql-server-features-and-capabilities"></a>Uso de las capacidades y características de SQL Server
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
WideWorldImporters el uso de características de SQL Server y capacidades de la base de datos OLTP.

WideWorldImporters está diseñado para mostrar muchas de las características claves de SQL Server, incluidas las características más recientes que se introdujo en SQL Server 2016. La siguiente es una lista de características de SQL Server y las capacidades y una descripción de cómo se utilizan en WideWorldImporters.

|Característica de SQL Server o la funcionalidad de|Uso de WideWorldImporters|
|-----------------------------|---------------------|
|Tablas temporales|Hay muchas tablas temporales, incluidas todas las tablas de referencia de estilo de búsqueda y entidades principales como StockItems, los clientes y proveedores. Uso de tablas temporales permite cómodamente realizar un seguimiento de la historia de estas entidades.|
|Llamadas AJAX para JSON|La aplicación usa con frecuencia llamadas AJAX para consultar estas tablas: personas, los clientes, proveedores y StockItems. Las llamadas devuelven cargas JSON (es decir, se distribuirán los datos que se devuelven como datos JSON). Ver, por ejemplo, el procedimiento almacenado `Website.SearchForCustomers`.|
|Bolsas de propiedad y valor JSON|Un número de tablas tiene columnas que contienen datos JSON para ampliar los datos relacionales en la tabla. Por ejemplo, `Application.SystemParameters` tiene una columna para la configuración de la aplicación y `Application.People` tiene una columna a las preferencias de usuario del registro. Estas tablas utilizan un `nvarchar(max)` columna para registrar los datos JSON, junto con una restricción CHECK mediante la función integrada `ISJSON` para asegurarse de la columna de valores son un valor JSON válido.|
|Seguridad de nivel de fila (RLS)|Seguridad de nivel de fila (RLS) se utiliza para limitar el acceso a la tabla Customers, en función de la pertenencia al rol. Cada territorio de ventas tiene un rol y un usuario. Para ver esto en acción, use el script correspondiente en el ejemplo script.zip, que forma parte de la [versión del ejemplo](http://go.microsoft.com/fwlink/?LinkID=800630).|
|análisis operativo en tiempo real|(Versión completa de la base de datos) Las tablas transaccional core `Sales.InvoiceLines` y `Sales.OrderLines` tienen un índice de almacén de columnas no clúster para admitir la ejecución eficaz de las consultas analíticas en la base de datos transaccional con un impacto mínimo en la carga de trabajo operativa. Ejecuta las transacciones y análisis de la misma base de datos también se conoce como [híbrida transaccional/analítico de procesamiento (HTAP)](https://wikipedia.org/wiki/Hybrid_Transactional/Analytical_Processing_(HTAP)). Para ver esto en acción, use el script correspondiente en el ejemplo script.zip, que forma parte de la [versión del ejemplo](http://go.microsoft.com/fwlink/?LinkID=800630).|
|PolyBase|Para ver esta PolyBase en acción, utilizando una tabla externa con un conjunto de datos público hospedado en el almacenamiento de blobs de Azure, use la secuencia de comandos correspondiente en el ejemplo script.zip, que forma parte de la [versión del ejemplo](http://go.microsoft.com/fwlink/?LinkID=800630).|
|OLTP en memoria|(Versión completa de la base de datos) Los tipos de tabla están todos los optimizadas en memoria, de modo que con valores de tabla de parámetros (Tvp todos los) que se benefician de la optimización de memoria.<br/><br/>Las dos tablas de supervisión, `Warehouse.VehicleTemperatures` y `Warehouse.ColdRoomTemperatures`, están optimizadas en memoria. Esto permite que la tabla ColdRoomTemperatures rellenarse a mayor velocidad que una tabla tradicional basada en disco. La tabla VehicleTemperatures contiene la carga de JSON y se presta a extensión hacia escenarios de IoT. La tabla VehicleTemperatures aún más se presta a los escenarios que implican EventHubs y análisis de transmisiones, Power BI.<br/><br/>El procedimiento almacenado `Website.RecordColdRoomTemperatures` se compila de forma nativa para mejorar aún más el rendimiento de la grabación de temperaturas inactivas.<br/><br/>Para ver un ejemplo de OLTP en memoria en acción, vea el controlador de carga de trabajo de vehículo ubicaciones en drivers.zip de la carga de trabajo, que forma parte de la [versión del ejemplo](http://go.microsoft.com/fwlink/?LinkID=800630).|
|Índice de almacén de columnas agrupado|(Versión completa de la base de datos) La tabla `Warehouse.StockItemTransactions` utiliza un índice de almacén de columnas agrupado. El número de filas en esta tabla se espera que aumentan de tamaño y el índice de almacén de columnas agrupado significativamente reduce el tamaño en disco de la tabla y mejora el rendimiento de las consultas. La modificación en esta tabla son solo realiza inserciones: no hay ninguna actualización o eliminación en esta tabla en la carga de trabajo en línea - e índice columnstore agrupado se realiza correctamente para las cargas de trabajo de inserción.|
|Enmascaramiento de datos dinámicos|En el esquema de base de datos, el enmascaramiento de datos se ha aplicado a los detalles de bank mantenidos para proveedores, en la tabla `Purchasing.Suppliers`. Personal sin privilegios de administrador no tendrá acceso a esta información.|
|Always Encrypted|Se incluye una demostración para Always Encrypted en el samples.zip descargable, que forma parte de la [versión del ejemplo](http://go.microsoft.com/fwlink/?LinkID=800630)... La demostración, crea una clave de cifrado de una tabla mediante el cifrado de datos confidenciales o una aplicación de ejemplo pequeña que inserta datos en la tabla.|
|Ajustar la base de datos|El `Warehouse.ColdRoomTemperatures` tabla se ha implementado como una tabla temporal y está optimizada en memoria en la versión completa de la base de datos de ejemplo. La tabla de almacenamiento está basada en disco y puede ajustarse en Azure.|
|Índices de texto completo|Índices de texto completo mejoran las búsquedas para las personas, los clientes y StockItems. Los índices se aplican a las consultas solo si tiene instalados en su instancia de SQL Server de indización de texto completo. Una columna calculada no persistente se utiliza para crear los datos que es el texto completo indiza en la tabla StockItems.<br/><br/>`CONCAT` se utiliza para concatenar los campos para crear SearchData que tiene índices de texto completo.<br/>Para habilitar el uso de índices de texto completo en el ejemplo de ejecutar la siguiente instrucción en la base de datos:<br/><br/>    `EXECUTE [Application].[Configuration_ConfigureFullTextIndexing]`<br/><br/>El procedimiento crea un catálogo de texto completo predeterminado si uno no existe, reemplaza las vistas de búsqueda con versiones de texto completo de esas vistas).<br/><br/>Tenga en cuenta que utiliza índices de texto completo en SQL Server, es necesario seleccionar la opción de texto completo durante la instalación. No requiere la base de datos de SQL Azure y una configuración concreta para habilitar los índices de texto completo.|
|Indizar las columnas calculadas persistentes|Indizar columnas calculadas persistentes que se usan en SupplierTransactions y CustomerTransactions.|
|Restricciones CHECK|Es una restricción check relativamente complejo en `Sales.SpecialDeals`. Esto garantiza que uno y solo uno de DiscountAmount, DiscountPercentage, y se configura UnitPrice.|
|Restricciones UNIQUE|Muchos a muchos construcción (y las restricciones únicas) se configuran para 'Warehouse.StockItemStockGroups.|
|Particiones de tabla|(Versión completa de la base de datos) Las tablas `Sales.CustomerTransactions` y `Purchasing.SupplierTransactions` se dividen por año con la función de partición `PF_TransactionDate` y el esquema de partición `PS_TransactionDate`. Creación de particiones se utiliza para mejorar la facilidad de uso de tablas de gran tamaño.|
|Procesamiento de la lista|Un tipo de tabla de ejemplo `Website.OrderIDList` se proporciona. Se utiliza un procedimiento de ejemplo `Website.InvoiceCustomerOrders`. El procedimiento utiliza expresiones de tabla común (CTE), TRY/CATCH, JSON_MODIFY, XACT_ABORT, NOCOUNT, THROW y XACT_STATE para muestra la capacidad para procesar una lista de pedidos, en lugar de simplemente un único pedido, para minimizar los viajes de ida y de la aplicación para el motor de base de datos.|
|Compresión GZip|El `Warehouse.VehicleTemperature`s tabla contiene los datos de sensor completa, pero cuando estos datos tiene más de unos meses, se comprimen para conservar espacio mediante la función COMPRESS, que usa la compresión GZip.<br/><br/>La vista `Website.VehicleTemperatures` al recuperar los datos que se comprimieron anteriormente, se utiliza la función de DESCOMPRESIÓN.|
|Almacén de consultas|Almacén de consultas está habilitado en la base de datos. Después de ejecutar algunas consultas, abra la base de datos en Management Studio, abra el nodo de almacén de consultas, que se encuentra en la base de datos, y abrir el informe principales consultas que consumen recursos para ver las ejecuciones de consulta y los planes para las consultas que se ha ejecutado.|
|STRING_SPLIT|La columna `DeliveryInstructions` en la tabla `Sales.Invoices`tiene un valor delimitado por comas que puede usarse para mostrar STRING_SPLIT.|
|Auditar|SQL Server Audit pueden habilitarse para esta base de datos de ejemplo mediante la ejecución de la siguiente instrucción en la base de datos:<br/><br/>    `EXECUTE [Application].[Configuration_ApplyAuditing]`<br/><br/>En la base de datos de SQL Azure, se habilita la auditoría a través de la [portal de Azure](https://portal.azure.com/).<br/><br/>Operaciones de seguridad que implican los inicios de sesión, roles y permisos se registran en todos los sistemas donde está habilitada la auditoría (incluidos los sistemas de edición estándar). Auditoría se dirige al registro de aplicación ya está disponible en todos los sistemas y no requiere permisos adicionales. Una advertencia es dado que para una mayor seguridad, se deben redirigir al registro de seguridad o a un archivo en una carpeta segura. Se proporciona un vínculo para describir la configuración adicional necesaria.<br/><br/>Para los sistemas de evaluación/developer o enterprise edition, se audita el acceso a todos los datos transaccionales financieros.|
