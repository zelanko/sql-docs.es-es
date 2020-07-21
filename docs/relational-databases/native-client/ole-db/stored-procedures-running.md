---
title: Ejecución de procedimientos almacenados (OLE DB) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- stored procedures [OLE DB], executing
- OLE DB, stored procedures
- SQL Server Native Client OLE DB provider, stored procedures
ms.assetid: c77d9be9-2176-4438-8c7a-04b63ebece08
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 2c86490f0a33ba1582ebebb3a9c1da78553098ff
ms.sourcegitcommit: f3321ed29d6d8725ba6378d207277a57cb5fe8c2
ms.contentlocale: es-ES
ms.lasthandoff: 07/06/2020
ms.locfileid: "86012017"
---
# <a name="stored-procedures---running"></a>Procedimientos almacenados: ejecución
[!INCLUDE [SQL Server](../../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

  Cuando se ejecutan instrucciones, llamar a un procedimiento almacenado en el origen de datos (en lugar de ejecutar o preparar directamente una instrucción en la aplicación cliente) puede proporcionar lo siguiente:  
  
-   Mayor rendimiento.  
  
-   Sobrecarga de red reducida.  
  
-   Mejor coherencia  
  
-   Mayor exactitud  
  
-   Función agregada.  
  
 El [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] proveedor de OLE DB de Native Client admite tres de los mecanismos que [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] los procedimientos almacenados usan para devolver datos:  
  
-   Cada instrucción SELECT del procedimiento genera un conjunto de resultados.  
  
-   El procedimiento puede devolver datos mediante parámetros de salida.  
  
-   El procedimiento puede tener un código de retorno de tipo entero.  
  
 La aplicación debe ser capaz de manejar todos estos resultados de los procedimientos almacenados.  
  
 Diferentes proveedores OLE DB devuelven parámetros de salida y valores devueltos en diferentes momentos durante el procesamiento de los resultados. En el caso del [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] proveedor de OLE DB de Native Client, los parámetros de salida y los códigos de retorno no se suministran hasta que el consumidor haya recuperado o cancelado los conjuntos de resultados devueltos por el procedimiento almacenado. Los códigos de retorno y los parámetros de salida se devuelven en el último paquete TDS del servidor.  
  
 Los proveedores usan la propiedad DBPROP_OUTPUTPARAMETERAVAILABILITY para notificar cuando devuelve parámetros de salida y valores de retorno. Esta propiedad se encuentra en el conjunto de propiedades DBPROPSET_DATASOURCEINFO.  
  
 El [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] proveedor de OLE DB de Native Client establece la propiedad DBPROP_OUTPUTPARAMETERAVAILABILITY en DBPROPVAL_OA_ATROWRELEASE para indicar que no se devuelven los códigos de retorno y los parámetros de salida hasta que se procesa o libera el conjunto de resultados.  
  
## <a name="see-also"></a>Consulte también  
 [Procedimientos almacenados](../../../relational-databases/native-client/ole-db/stored-procedures.md)  
  
  
