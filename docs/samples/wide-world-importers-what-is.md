---
title: 'Wide World Importers: base de datos de ejemplo para SQL | Microsoft Docs'
ms.prod: sql
ms.prod_service: sql
ms.technology: samples
ms.custom: ''
ms.date: 04/04/2018
ms.reviewer: ''
ms.topic: conceptual
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 017f301d9888ddd4f90d70e7d993faf840640a66
ms.sourcegitcommit: 9c6a37175296144464ffea815f371c024fce7032
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/15/2018
ms.locfileid: "51670694"
---
# <a name="wide-world-importers-sample-databases-for-microsoft-sql"></a>Las bases de datos de ejemplo de Wide World Importers para SQL de Microsoft
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
Se trata de una visión general de la compañía ficticia Wide World Importers y los flujos de trabajo que se tratan en las bases de datos de ejemplo de WideWorldImporters para SQL Server y Azure SQL Database.  

Wide World Importers (WWI) es un importador de mercancías novedad por mayor y un distribuidor que opera desde el área de la bahía de San Francisco.

Como un mayorista, los clientes de WWI son principalmente las empresas revenden a individuos. WWI vende a clientes particulares de Estados Unidos como almacenes de especialidad, supermercados, informática almacenes, departamentos de atracción de turismo y algunas personas. WWI también vende a otros mayoristas a través de una red de los agentes que promueven los productos en nombre de WWI. Mientras que todos los clientes de WWI actualmente se basan en los Estados Unidos, la empresa va a insertar expansión en otros países.

WWI compra productos de proveedores como novedad y fabricantes de juguete y otros mayoristas novedad. Los productos en su almacén de WWI y reordenación de proveedores cotización según sea necesario para cumplir los pedidos del cliente. También grandes volúmenes de materiales de empaquetado de compra y venderlos en cantidades menores como una comodidad para los clientes.

Recientemente WWI comenzado a vender una variedad de comestible sorpresa, como el chile bombones.  La compañía anteriormente no tenía que controlar elementos refrigerados. Ahora, para satisfacer los requisitos de control de alimentos, deben supervisar la temperatura en su sala de refrigerador y cualquiera de sus camionetas que tienen secciones del refrigerador.

## <a name="workflow-for-warehouse-stock-items"></a>Flujo de trabajo para los elementos de stock de almacén

El flujo típico para el modo en que se almacenó y distribuidas es como sigue:
- WWI crea pedidos de compra y envía los pedidos a los proveedores.
- Los elementos de envío de proveedores, WWI los recibe y tiene en stock en su almacén.
- Elementos de pedidos de clientes de WWI
- WWI rellena el pedido del cliente con elementos estándar en el almacén, y cuando no tienen suficientes existencias, ordenan el material adicional a los proveedores.
- Algunos clientes no desean esperar para los elementos que no están disponibles. Si por ejemplo pedido cinco diferentes artículos agotados y cuatro están disponibles, desean recibir los cuatro elementos y el resto de producto de pedido pendiente. El elemento se les enviará más adelante en un envío independiente.
- WWI facturas normalmente a los clientes para los elementos de cotizaciones, convirtiendo el pedido a una factura.
- Los clientes pueden solicitar elementos que no están disponibles. Estos elementos están pendientes.
- WWI entrega stock elementos a los clientes a través de sus propios camionetas de entrega, o mediante otros métodos de transporte o correos.
- Los clientes pagan las facturas a WWI.
- Periódicamente, WWI paga proveedores para los elementos que estaban en pedidos de compra. Esto es a menudo en algún momento después de que han recibido los productos.

## <a name="data-warehouse-and-analysis-workflow"></a>Flujo de trabajo de análisis y almacenamiento de datos

Aunque el equipo de WWI usa SQL Server Reporting Services para generar informes operativos desde la base de datos WideWorldImporters, también que necesitan para realizar análisis en sus datos y necesita generar informes estratégicos. El equipo ha creado un modelo de datos de dimensión en una base de datos WideWorldImportersDW. Esta base de datos se rellena con un paquete de Integration Services.

SQL Server Analysis Services se usa para crear modelos de datos de análisis de los datos en el modelo de datos dimensional. SQL Server Reporting Services se usa para generar informes estratégicos directamente desde el modelo de datos dimensional y también desde el modelo de análisis. Se usa Power BI para crear paneles de los mismos datos. Los paneles se usan en los sitios Web y en teléfonos y tabletas. *Nota: estos informes y modelos de datos todavía no están disponibles*

## <a name="additional-workflows"></a>Flujos de trabajo adicionales

Estos son los flujos de trabajo adicionales.
- Notas de crédito de WWI problemas cuando un cliente no recibe lo bueno por algún motivo, o cuando los productos son defectuosos. Estos se tratan como facturas negativo.
- WWI cuenta periódicamente las cantidades disponibles de stock elementos para asegurarse de que las cantidades de stock que se muestran como disponibles en su sistema sean precisas. (El proceso de hacer esto se denomina un stocktake).
- Temperaturas en frío. Mercancías perecederas se almacenan en las salas refrigeradas. Datos del sensor desde dichos locales se ingieren en la base de datos para fines de supervisión y análisis.
- Ubicación del vehículo de seguimiento. Vehículos que transportan mercancías para WWI incluyen sensores que realizan el seguimiento de la ubicación. Esta ubicación se ingiere nuevo en la base de datos para análisis y supervisión adicional.

## <a name="fiscal-year"></a>Año fiscal

La empresa opera con un ejercicio que comienza el 1 de noviembre.

## <a name="terms-of-use"></a>Términos de uso

La licencia para la base de datos de ejemplo y el código de ejemplo se describe aquí: [license.txt](https://github.com/Microsoft/sql-server-samples/blob/master/license.txt)

La base de datos de ejemplo incluye los datos públicos que se ha cargado desde data.gov y EarthData Natural. Los términos de uso están aquí: [https://www.naturalearthdata.com/about/terms-of-use/](https://www.naturalearthdata.com/about/terms-of-use/)
