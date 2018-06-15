---
title: Ejecutar procedimientos almacenados (OLE DB) | Documentos de Microsoft
description: Ejecutar procedimientos almacenados (OLE DB)
ms.custom: ''
ms.date: 06/12/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.component: oledb|ole-db
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- stored procedures [OLE DB], executing
- OLE DB, stored procedures
- OLE DB Driver for SQL Server, stored procedures
author: pmasl
ms.author: Pedro.Lopes
manager: craigg
ms.openlocfilehash: 9919fedbb999600e17c767a3206a587b99aec4da
ms.sourcegitcommit: 354ed9c8fac7014adb0d752518a91d8c86cdce81
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/14/2018
ms.locfileid: "35611890"
---
# <a name="stored-procedures---running"></a>Procedimientos almacenados: ejecución
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-asdbmi-md](../../../includes/appliesto-ss-asdb-asdw-pdw-asdbmi-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  Al ejecutar las instrucciones, puede proporcionar una llamada a un procedimiento almacenado en el origen de datos (en lugar de ejecutar o preparar directamente una instrucción en la aplicación cliente):  
  
-   Mayor rendimiento.  
  
-   Sobrecarga de red reducida.  
  
-   Mejor coherencia  
  
-   Mayor exactitud  
  
-   Funcionalidad agregada.  
  
 El controlador OLE DB para SQL Server admite tres de los mecanismos que [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] utilizan procedimientos almacenados para devolver datos:  
  
-   Cada instrucción SELECT del procedimiento genera un conjunto de resultados.  
  
-   El procedimiento puede devolver datos mediante parámetros de salida.  
  
-   El procedimiento puede tener un código de retorno de tipo entero.  
  
 La aplicación debe ser capaz de manejar todos estos resultados de los procedimientos almacenados.  
  
 Diferentes proveedores OLE DB devuelven parámetros de salida y valores devueltos en diferentes momentos durante el procesamiento de los resultados. El controlador OLE DB para SQL Server, en el caso de los parámetros de salida y códigos de retorno no se proporcionan hasta después de que el consumidor haya recuperado o cancelado los conjuntos de resultados devueltos por el procedimiento almacenado. Los códigos de retorno y los parámetros de salida se devuelven en el último paquete TDS del servidor.  
  
 Los proveedores usan la propiedad DBPROP_OUTPUTPARAMETERAVAILABILITY para notificar cuando devuelve parámetros de salida y valores de retorno. Esta propiedad se encuentra en el conjunto de propiedades DBPROPSET_DATASOURCEINFO.  
  
 El controlador OLE DB para SQL Server se establece la propiedad DBPROP_OUTPUTPARAMETERAVAILABILITY en DBPROPVAL_OA_ATROWRELEASE para indicar que los códigos de retorno y parámetros de salida no se devuelven hasta que se procese o lance el conjunto de resultados.  
  
## <a name="see-also"></a>Vea también  
 [Procedimientos almacenados](../../oledb/ole-db/stored-procedures.md)  
  
  
