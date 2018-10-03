---
title: Mejoras de fecha y hora | Microsoft Docs
description: Mejoras de fecha y hora en el controlador de OLE DB para SQL Server
ms.custom: ''
ms.date: 06/12/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
author: pmasl
ms.author: pelopes
manager: craigg
ms.openlocfilehash: 7f41b727fe84ab0454a85466cfa74c376788b9e7
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MTE75
ms.contentlocale: es-ES
ms.lasthandoff: 10/01/2018
ms.locfileid: "47730583"
---
# <a name="date-and-time-improvements"></a>Mejoras en la fecha y la hora
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  Este tema describe el controlador OLE DB para SQL Server admiten para los tipos de datos de fecha y hora en que se agregaron en [!INCLUDE[ssKatmai](../../../includes/sskatmai-md.md)].  
  
 Para obtener más información acerca de las mejoras de fecha y hora, vea [mejoras de fecha y hora &#40;OLE DB&#41;](../../oledb/ole-db-date-time/date-and-time-improvements-ole-db.md).  
  
 Para obtener información sobre las aplicaciones de ejemplo que muestran esta característica, vea [Ejemplos de programación de datos de SQL Server](http://msftdpprodsamples.codeplex.com/).  
  
## <a name="usage"></a>Uso  
 En las secciones siguientes se describen varios modos de usar los nuevos tipos de fecha y hora.  
  
### <a name="use-date-as-a-distinct-data-type"></a>Usar date como un tipo de datos distinto  
 Empezando por [!INCLUDE[ssKatmai](../../../includes/sskatmai-md.md)], compatibilidad mejorada para los tipos de fecha y hora resulta más eficaz utilizar el tipo DBTYPE_DBDATE de OLE DB.  
  
### <a name="use-time-as-a-distinct-data-type"></a>Usar time como un tipo de datos distinto  
 OLE DB ya tiene un tipo de datos que solamente contiene la hora, DBTYPE_DBTIME, que ofrece una precisión de 1 segundo.
  
 El nuevo tipo de datos de hora de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] tiene una precisión de 100 nanosegundos para las fracciones de segundo. Esto requiere un nuevo tipo de controlador de OLE DB para SQL Server: DBTYPE_DBTIME2. Las aplicaciones existentes escritas para utilizar horas sin fracciones de segundo pueden utilizar columnas time(0). El tipo existente DBTYPE_TIME de OLE DB y sus estructuras correspondientes deberían funcionar correctamente, a menos que las aplicaciones se basen en el tipo devuelto en los metadatos.  
  
### <a name="use-time-as-a-distinct-data-type-with-extended-fractional-seconds-precision"></a>Usar time como un tipo de datos distinto con una precisión ampliada para las fracciones de segundo  
 Algunas aplicaciones, como las aplicaciones de fabricación y control de procesos, exigen la capacidad de controlar los datos de hora con una precisión de hasta 100 nanosegundos. Nuevo tipo para este propósito en OLE DB es DBTYPE_DBTIME2.  
  
### <a name="use-datetime-with-extended-fractional-seconds-precision"></a>Usar el tipo datetime con una precisión ampliada para las fracciones de segundo  
 OLE DB ya define un tipo con una precisión de hasta 1 nanosegundo. Sin embargo, este tipo ya se utiliza en aplicaciones [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] existentes y estas aplicaciones tienen una expectativa de tan solo 1/300 de precisión en segundos. El nuevo tipo **datetime2(3)** no es directamente compatible con el tipo datetime existente. Si existe el riesgo de que esto afecte al comportamiento de la aplicación, las aplicaciones deben utilizar una nueva marca DBCOLUMN para determinar el tipo de servidor real.    
  
### <a name="use-datetime-with-extended-fractional-seconds-precision-and-timezone"></a>Usar el tipo datetime con una precisión ampliada para las fracciones de segundo y la zona horaria  
 Algunas aplicaciones requieren valores de fecha y hora con información de zona horaria. Esto es compatible con el nuevo tipo DBTYPE_DBTIMESTAMPOFFSET.
  
### <a name="use-datetimedatetimedatetimeoffset-data-with-client-side-conversions-consistent-with-existing-conversions"></a>Usar datos de tipo date/time/datetime/datetimeoffset con conversiones de cliente coherentes con las conversiones existentes  
 Estas conversiones se han ampliado de modo coherente para incluir conversiones entre todos los tipos de fecha y hora introducidos en [!INCLUDE[ssKatmai](../../../includes/sskatmai-md.md)].  
  
## <a name="see-also"></a>Ver también  
 [Controlador OLE DB para las características de SQL Server](../../oledb/features/oledb-driver-for-sql-server-features.md)  
  
  
