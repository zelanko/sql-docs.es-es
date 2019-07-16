---
title: Mejoras de fecha y hora | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.reviewer: ''
ms.prod: sql
ms.technology: native-client
ms.topic: reference
ms.assetid: 9b1d0d9d-1f6e-4399-8f61-e23f9a486a7a
author: MightyPen
ms.author: genemi
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: fdb0f3382824f11e3058a23555ba0c60e24ef256
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "67987567"
---
# <a name="date-and-time-improvements"></a>Mejoras en la fecha y la hora
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../../includes/snac-deprecated.md)]

  En este tema se describe la compatibilidad de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client con los nuevos tipos de datos de fecha y hora que se introdujeron en [!INCLUDE[ssKatmai](../../../includes/sskatmai-md.md)].  
  
 Para obtener más información acerca de las mejoras de fecha y hora, vea [mejoras de fecha y hora &#40;OLE DB&#41; ](../../../relational-databases/native-client-ole-db-date-time/date-and-time-improvements-ole-db.md) y [mejoras de fecha y hora &#40;ODBC&#41;](../../../relational-databases/native-client-odbc-date-time/date-and-time-improvements-odbc.md).  
  
 Para obtener información sobre las aplicaciones de ejemplo que muestran esta característica, vea [Ejemplos de programación de datos de SQL Server](https://msftdpprodsamples.codeplex.com/).  
  
## <a name="usage"></a>Uso  
 En las secciones siguientes se describen varios modos de usar los nuevos tipos de fecha y hora.  
  
### <a name="use-date-as-a-distinct-data-type"></a>Usar date como un tipo de datos distinto  
 A partir de [!INCLUDE[ssKatmai](../../../includes/sskatmai-md.md)], la compatibilidad mejorada con los tipos de fecha y hora hace que el uso del tipo SQL_TYPE_DATE de ODBC (SQL_DATE en aplicaciones ODBC 2.0) y el tipo DBTYPE_DBDATE de OLE DB resulte más eficaz.  
  
### <a name="use-time-as-a-distinct-data-type"></a>Usar time como un tipo de datos distinto  
 OLE DB ya tiene un tipo de datos que solamente contiene la hora, DBTYPE_DBTIME, que ofrece una precisión de 1 segundo. En ODBC, el tipo equivalente es SQL_TYPE_TIME (SQL_TIME para aplicaciones ODBC 2.0).  
  
 El nuevo tipo de datos de hora de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] tiene una precisión de 100 nanosegundos para las fracciones de segundo. Esto requiere nuevos tipos en [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client: DBTYPE_DBTIME2 (OLE DB) y SQL_SS_TIME2 (ODBC). Las aplicaciones existentes escritas para utilizar horas sin fracciones de segundo pueden utilizar columnas time(0). Los tipos existentes DBTYPE_TIME de OLE DB y SQL_TYPE_TIME de ODBC y sus estructuras correspondientes deben funcionar correctamente, a menos que las aplicaciones se basen en el tipo devuelto en los metadatos.  
  
### <a name="use-time-as-a-distinct-data-type-with-extended-fractional-seconds-precision"></a>Usar time como un tipo de datos distinto con una precisión ampliada para las fracciones de segundo  
 Algunas aplicaciones, como las aplicaciones de fabricación y control de procesos, exigen la capacidad de controlar los datos de hora con una precisión de hasta 100 nanosegundos. Para este propósito, se han introducido los nuevos tipos DBTYPE_DBTIME2 (OLE DB) y SQL_SS_TIME2 (ODBC).  
  
### <a name="use-datetime-with-extended-fractional-seconds-precision"></a>Usar el tipo datetime con una precisión ampliada para las fracciones de segundo  
 OLE DB ya define un tipo con una precisión de hasta 1 nanosegundo. Sin embargo, este tipo ya se utiliza en aplicaciones [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] existentes y estas aplicaciones tienen una expectativa de tan solo 1/300 de precisión en segundos. El nuevo tipo **datetime2(3)** no es directamente compatible con el tipo datetime existente. Si existe el riesgo de que esto afecte al comportamiento de la aplicación, las aplicaciones deben utilizar una nueva marca DBCOLUMN para determinar el tipo de servidor real.  
  
 ODBC también define un tipo con una precisión de hasta 1 nanosegundo. Sin embargo, este tipo ya se utiliza en aplicaciones [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] existentes y tales aplicaciones solo esperan una precisión de 3 milisegundos. El nuevo **datetime2(3)** tipo no es directamente compatible con las existentes **datetime** tipo. **datetime2(3)** tiene una precisión de un milisegundo y **datetime** tiene una precisión de 1/300 de segundo. En ODBC, las aplicaciones pueden determinar qué tipo de servidor se está usando con el campo descriptor SQL_DESC_TYPE_NAME. Por lo tanto, el tipo SQL_TYPE_TIMESTAMP existente (SQL_TIMESTAMP para aplicaciones ODBC 2.0) puede utilizarse con ambos tipos.  
  
### <a name="use-datetime-with-extended-fractional-seconds-precision-and-timezone"></a>Usar el tipo datetime con una precisión ampliada para las fracciones de segundo y la zona horaria  
 Algunas aplicaciones requieren valores de fecha y hora con información de zona horaria. Los nuevos tipos DBTYPE_DBTIMESTAMPOFFSET (OLE DB) y SQL_SS_TIMESTAMPOFFSET (ODBC) admiten este uso.  
  
### <a name="use-datetimedatetimedatetimeoffset-data-with-client-side-conversions-consistent-with-existing-conversions"></a>Usar datos de tipo date/time/datetime/datetimeoffset con conversiones de cliente coherentes con las conversiones existentes  
 El estándar ODBC describe cómo funcionan las conversiones entre los tipos date, time y timestamp existentes. Estos tipos se han ampliada de modo coherente para incluir conversiones entre todos los tipos de fecha y hora introducidos en [!INCLUDE[ssKatmai](../../../includes/sskatmai-md.md)].  
  
## <a name="see-also"></a>Vea también  
 [Características de SQL Server Native Client](../../../relational-databases/native-client/features/sql-server-native-client-features.md)  
  
  
