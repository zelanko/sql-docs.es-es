---
title: Wide World Importers - base de datos de ejemplo para SQL | Documentos de Microsoft
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
robots: noindex,nofollow
ms.openlocfilehash: be5ed96b049d5fb7b4ecf5e6966b11390a08b04d
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="wide-world-importers-sample-databases-for-microsoft-sql"></a>Las bases de datos de ejemplo de Wide World Importers para Microsoft SQL
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
Se trata de una visión general de la empresa ficticia Wide World Importers y los flujos de trabajo que se mencionan en las bases de datos de ejemplo de WideWorldImporters para SQL Server y base de datos de SQL Azure.  

Wide World Importers (WWI) es un importador de mercancías novedad por mayor y un distribuidor que opere desde el área de la bahía de San Francisco.

Como un mayorista, los clientes del WWI son principalmente las empresas revenden a individuos. WWI vende a clientes particulares en los Estados Unidos incluidos los almacenes especializados, supermercados, informática almacenes y tiendas de atracción turísticos, algunos usuarios. WWI también vende a otros mayoristas a través de una red de agentes que promover los productos en nombre del WWI. Mientras que todos los clientes del WWI actualmente se basan en los Estados Unidos, la empresa va a insertar para la expansión en otros países.

WWI compra bienes de proveedores como novedad y fabricantes de juguete y otros mayoristas novedad. Los productos en su almacén de WWI y volver a ordenar de proveedores estándar según sea necesario para el cumplimiento de pedidos de clientes. También grandes volúmenes de materiales de embalaje de compra y vender en cantidades más pequeñas, como una comodidad para los clientes.

WWI inició recientemente para venderla a una variedad de comestible sorpresa como Chile bombones.  La empresa anteriormente no tenía que controlar elementos frío. Ahora, para satisfacer los requisitos de tratamiento de comida, debe supervisar la temperatura en su habitación refrigerador y cualquiera de los camiones que tienen secciones refrigerador.

## <a name="workflow-for-warehouse-stock-items"></a>Flujo de trabajo para los elementos estándar de almacenamiento

El flujo típico de cómo se almacena y se distribuyen elementos es como sigue:
- WWI crea pedidos de compra y envía los pedidos a los proveedores.
- Los elementos de envío de proveedores, WWI reciben y tiene en stock en su almacén.
- Elementos de orden de los clientes de WWI
- WWI rellena el pedido del cliente con elementos estándar en el almacén, y cuando no tiene suficientes existencias, solicitan las acciones adicionales de los proveedores.
- Algunos clientes no desean esperar para elementos que no están en el almacén. Si digamos pedido cinco diferentes elementos estándar y cuatro están disponibles, desean recibir los cuatro elementos y el resto de producto de pedido pendiente. El elemento se les enviará más adelante en un envío independiente.
- WWI facturas a los clientes para los artículos en existencias, por lo general convirtiendo el pedido a una factura.
- Los clientes pueden realizar pedidos de elementos que no están en el almacén. Estos elementos están pendientes.
- WWI ofrece artículos agotados a los clientes a través de sus propios van de entrega, o mediante otros métodos de transporte o correos.
- Los clientes pagar facturas para WWI.
- Periódicamente, WWI paga proveedores para los elementos creados en los pedidos de compra. Esto es a menudo en algún momento después de que han recibido los productos.

## <a name="data-warehouse-and-analysis-workflow"></a>Flujo de trabajo de análisis y almacenamiento de datos

Mientras el equipo en WWI utilizar SQL Server Reporting Services para generar informes operativos a partir de la base de datos WideWorldImporters, también necesita realizar análisis en sus datos y necesita para generar informes estratégicos. El equipo ha creado un modelo de datos de dimensión en una base de datos WideWorldImportersDW. Esta base de datos se rellena con un paquete de Integration Services.

SQL Server Analysis Services se utiliza para crear modelos de datos analíticos de los datos en el modelo de datos dimensionales. SQL Server Reporting Services se usa para generar informes estratégicos directamente desde el modelo de datos multidimensionales y también del modelo analítico. Power BI se usa para crear paneles desde los mismos datos. Los paneles se usan en los sitios Web y en los teléfonos y tabletas. *Nota: estos informes y modelos de datos no están disponibles*

## <a name="additional-workflows"></a>Flujos de trabajo adicionales

Se trata de flujos de trabajo adicionales.
- Notas de crédito de WWI problemas cuando un cliente no recibe la buena por algún motivo, o cuando los productos estén defectuosos. Estos se tratan como facturas negativo.
- WWI cuenta periódicamente las cantidades del inventario de artículos agotados para asegurarse de que las cantidades de stock que se muestran como disponibles en su sistema son correctos. (El proceso de hacer esto se denomina un stocktake).
- Temperaturas inactivas. Perecederos se almacenan en salas refrigerados. Datos del sensor de dichos locales se ingestión en la base de datos con fines de supervisión y análisis.
- Seguimiento de la ubicación vehículo. Los vehículos que transportan mercancías para WWI incluyen sensores que realizan el seguimiento de la ubicación. Esta ubicación es ingestión nuevo en la base de datos para la supervisión y más análisis.

## <a name="fiscal-year"></a>Año fiscal

La empresa funciona con un ejercicio que comienza el 1 de noviembre.

## <a name="terms-of-use"></a>Términos de uso

La licencia para la base de datos de ejemplo y el código de ejemplo se describe aquí: [license.txt](https://github.com/Microsoft/sql-server-samples/blob/master/license.txt)

La base de datos de ejemplo incluye datos públicos que se ha cargado desde data.gov y EarthData Natural. Los términos de uso se encuentran aquí: [http://www.naturalearthdata.com/about/terms-of-use/](http://www.naturalearthdata.com/about/terms-of-use/)
