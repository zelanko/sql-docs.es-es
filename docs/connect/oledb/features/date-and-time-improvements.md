---
title: Fecha y hora mejoras | Documentos de Microsoft
description: Mejoras de fecha y hora en el controlador OLE DB para SQL Server
ms.custom: ''
ms.date: 03/26/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: ''
ms.component: oledb|features
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: reference
author: pmasl
ms.author: Pedro.Lopes
manager: craigg
ms.openlocfilehash: ff0d3b561725cef71928728c291ad89acbfca52d
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="date-and-time-improvements"></a>Fecha y hora mejoras
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  Este tema describe el controlador OLE DB para SQL Server admiten para los tipos de datos de fecha y hora en que se agregaron en [!INCLUDE[ssKatmai](../../../includes/sskatmai-md.md)].  
  
 Para obtener más información acerca de las mejoras de fecha y hora, vea [fecha y hora mejoras &#40;OLE DB&#41;](../../oledb/ole-db-date-time/date-and-time-improvements-ole-db.md).  
  
 Para obtener información acerca de las aplicaciones de ejemplo que muestran esta característica, consulte [ejemplos de programación de datos de SQL Server](http://msftdpprodsamples.codeplex.com/).  
  
## <a name="usage"></a>Uso  
 En las secciones siguientes se describen varios modos de usar los nuevos tipos de fecha y hora.  
  
### <a name="use-date-as-a-distinct-data-type"></a>Usar date como un tipo de datos distinto  
 A partir de [!INCLUDE[ssKatmai](../../../includes/sskatmai-md.md)], compatibilidad mejorada para los tipos de fecha y hora resulta más eficaz utilizar el tipo DBTYPE_DBDATE de OLE DB.  
  
### <a name="use-time-as-a-distinct-data-type"></a>Usar time como un tipo de datos distinto  
 OLE DB ya tiene un tipo de datos que solamente contiene la hora, DBTYPE_DBTIME, que ofrece una precisión de 1 segundo.
  
 El nuevo [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] tiempo en el tipo de datos tiene fracciones de segundos con precisión de 100 nanosegundos. Esto requiere un nuevo tipo de controlador de OLE DB para SQL Server: DBTYPE_DBTIME2. Las aplicaciones existentes escritas para utilizar horas sin fracciones de segundo pueden utilizar columnas time(0). El tipo de DBTYPE_TIME de OLE DB existente y sus estructuras correspondientes deben funcionar correctamente, a menos que las aplicaciones que se basan en el tipo devuelto en metadatos.  
  
### <a name="use-time-as-a-distinct-data-type-with-extended-fractional-seconds-precision"></a>Usar time como un tipo de datos distinto con una precisión ampliada para las fracciones de segundo  
 Algunas aplicaciones, como las aplicaciones de fabricación y control de procesos, exigen la capacidad de controlar los datos de hora con una precisión de hasta 100 nanosegundos. Nuevo tipo para este fin en OLE DB es DBTYPE_DBTIME2.  
  
### <a name="use-datetime-with-extended-fractional-seconds-precision"></a>Usar el tipo datetime con una precisión ampliada para las fracciones de segundo  
 OLE DB ya define un tipo con una precisión de hasta 1 nanosegundo. Sin embargo, este tipo ya se utiliza en aplicaciones [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] existentes y estas aplicaciones tienen una expectativa de tan solo 1/300 de precisión en segundos. El nuevo **datetime2(3)** tipo no es directamente compatible con el tipo de fecha y hora existente. Si existe el riesgo de que esto afecte al comportamiento de la aplicación, las aplicaciones deben utilizar una nueva marca DBCOLUMN para determinar el tipo de servidor real.    
  
### <a name="use-datetime-with-extended-fractional-seconds-precision-and-timezone"></a>Usar el tipo datetime con una precisión ampliada para las fracciones de segundo y la zona horaria  
 Algunas aplicaciones requieren valores de fecha y hora con información de zona horaria. Esto es compatible con el nuevo tipo DBTYPE_DBTIMESTAMPOFFSET.
  
### <a name="use-datetimedatetimedatetimeoffset-data-with-client-side-conversions-consistent-with-existing-conversions"></a>Usar datos de tipo date/time/datetime/datetimeoffset con conversiones de cliente coherentes con las conversiones existentes  
 Se han ampliado las conversiones de una manera coherente para incluir conversiones entre todos los tipos de fecha y hora introducidos en [!INCLUDE[ssKatmai](../../../includes/sskatmai-md.md)].  
  
## <a name="see-also"></a>Vea también  
 [Controlador OLE DB para las características de SQL Server](../../oledb/features/oledb-driver-for-sql-server-features.md)  
  
  
