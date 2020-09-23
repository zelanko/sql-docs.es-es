---
title: Ejecución de procedimientos almacenados (OLE DB) | Microsoft Docs
description: Obtenga información sobre las ventajas de llamar a un procedimiento almacenado en el origen de datos y los mecanismos que OLE DB Driver for SQL Server ofrece para devolver datos.
ms.custom: ''
ms.date: 06/12/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
helpviewer_keywords:
- stored procedures [OLE DB], executing
- OLE DB, stored procedures
- OLE DB Driver for SQL Server, stored procedures
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 244a5719285589b182b14e5214fd0b27050db2a0
ms.sourcegitcommit: c95f3ef5734dec753de09e07752a5d15884125e2
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/25/2020
ms.locfileid: "88858833"
---
# <a name="stored-procedures---running"></a>Procedimientos almacenados: ejecución
[!INCLUDE [SQL Server](../../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  Cuando se ejecutan instrucciones, llamar a un procedimiento almacenado en el origen de datos (en lugar de ejecutar o preparar directamente una instrucción en la aplicación cliente) puede proporcionar lo siguiente:  
  
-   Mayor rendimiento.  
  
-   Sobrecarga de red reducida.  
  
-   Mejor coherencia  
  
-   Mayor exactitud  
  
-   Función agregada.  
  
 OLE DB Driver for SQL Server admite tres de los mecanismos que los procedimientos almacenados de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] usan para devolver datos:  
  
-   Cada instrucción SELECT del procedimiento genera un conjunto de resultados.  
  
-   El procedimiento puede devolver datos mediante parámetros de salida.  
  
-   El procedimiento puede tener un código de retorno de tipo entero.  
  
 La aplicación debe ser capaz de manejar todos estos resultados de los procedimientos almacenados.  
  
 Diferentes proveedores OLE DB devuelven parámetros de salida y valores devueltos en diferentes momentos durante el procesamiento de los resultados. En el caso del controlador OLE DB para SQL Server, los parámetros de salida y los códigos de retorno no se proporcionan hasta después de que el consumidor haya recuperado o cancelado los conjuntos de resultados devueltos por el procedimiento almacenado. Los códigos de retorno y los parámetros de salida se devuelven en el último paquete TDS del servidor.  
  
 Los proveedores usan la propiedad DBPROP_OUTPUTPARAMETERAVAILABILITY para notificar cuando devuelve parámetros de salida y valores de retorno. Esta propiedad se encuentra en el conjunto de propiedades DBPROPSET_DATASOURCEINFO.  
  
 El controlador OLE DB para SQL Server establece la propiedad DBPROP_OUTPUTPARAMETERAVAILABILITY en DBPROPVAL_OA_ATROWRELEASE para indicar que no se devuelven los códigos de retorno y los parámetros de salida hasta que no se procese o publique el conjunto de resultados.  
  
## <a name="see-also"></a>Consulte también  
 [Procedimientos almacenados](../../oledb/ole-db/stored-procedures.md)  
  
  
