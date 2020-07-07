---
title: Enlaces y conversiones (OLE DB)
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: ''
ms.topic: reference
helpviewer_keywords:
- conversions [OLE DB]
- bindings [OLE DB]
- OLE DB, bindings and conversions
ms.assetid: c187df58-a8c8-4c74-a76f-663abbc5f0c1
author: markingmyname
ms.author: maghan
ms.custom: seo-dt-2019
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 82c2e5f35d7418f9c1c44a9a7711b7ef546eb3ac
ms.sourcegitcommit: f3321ed29d6d8725ba6378d207277a57cb5fe8c2
ms.contentlocale: es-ES
ms.lasthandoff: 07/06/2020
ms.locfileid: "85998180"
---
# <a name="conversions-ole-db"></a>Conversiones (OLE DB)
[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

  En esta sección se describe cómo convertir entre valores **datetime** y **datetimeoffset**. OLE DB ya proporciona las conversiones descritas en esta sección o son una extensión coherente de OLE DB.  
  
 El formato de literales y cadenas para las fechas y horas en OLE DB generalmente sigue la ISO y no depende de la configuración regional del cliente. Una excepción es DBTYPE_DATE, donde la norma es OLE Automation. Sin embargo, debido a que [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client solamente convierte entre tipos cuando se transmiten datos a o desde el cliente, no hay ninguna manera de que una aplicación fuerce a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client a convertir entre DBTYPE_DATE y los formatos de cadena. De lo contrario, las cadenas usan los formatos siguientes (el texto entre corchetes indica un elemento opcional):  
  
-   El formato de las cadenas **datetime** y **datetimeoffset** es:  
  
     *AAAA* - *mm* - *DD*[ *HH*:*mm*:*SS*[.* 9999999*] [± *HH*:*mm*]]  
  
-   El formato de las cadenas **time** es:  
  
     *hh*:*mm*:*ss*[.*9999999*]  
  
-   El formato de las cadenas **date** es:  
  
     *AAAA* - *mm* - *DD*  
  
> [!NOTE]  
>  Las versiones anteriores de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client y de las conversiones OLE implementadas SQLOLEDB, en caso de un error en las conversiones estándar. Como resultado, algunas conversiones realizadas por [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client 10.0 y posteriores difieren de la especificación OLE DB.  
  
 Las conversiones de las cadenas permiten flexibilidad en los espacios en blanco y el ancho de campo. Para obtener más información, vea la sección "formatos de datos: cadenas y literales" en [compatibilidad con tipos de datos para obtener OLE DB mejoras de fecha y hora](../../relational-databases/native-client-ole-db-date-time/data-type-support-for-ole-db-date-and-time-improvements.md).  
  
 A continuación figuran las reglas de conversión generales:  
  
-   Cuando una cadena se convierte en un tipo de fecha y hora, la cadena se analiza primero como literal ISO. Si no ocurre así, la cadena se analiza como literal de fecha OLE, que tiene componentes de hora.  
  
-   Si no está presente la hora pero el receptor puede almacenar la hora, esta última se establece en cero. Si no hay ninguna fecha presente pero el receptor puede almacenar una, la fecha se establece en la fecha actual cuando se usan conversiones ISO y en 1899-12-30, cuando se usan conversiones OLE.  
  
-   Si no hay ninguna zona horaria en el tipo de datos que el cliente usa pero el servidor puede almacenar la zona horaria, se supone que los datos del cliente se encuentran en la zona horaria del cliente.  
  
-   Si no hay ninguna zona horaria en el servidor pero el cliente tiene información de la zona horaria, se presupone la zona horaria UTC. Este comportamiento es diferente al del servidor.  
  
-   Si está presente la hora pero el receptor no puede almacenarla, se omite el componente de hora.  
  
-   Si está presente la fecha pero el receptor no puede almacenarla, se omite el componente de fecha.  
  
-   Si se produce el truncamiento de segundos o fracciones de segundo al convertir de cliente a servidor, se devuelve DB_E_ERRORSOCCURRED y se establece el estado DBSTATUS_E_DATAOVERFLOW.  
  
-   Si el truncamiento de segundos o fracciones de segundo se produce al convertir del servidor al cliente, se establece DBSTATUS_S_TRUNCATED.  
  
## <a name="in-this-section"></a>En esta sección  
 [Conversiones realizadas de cliente a servidor](../../relational-databases/native-client-ole-db-date-time/conversions-performed-from-client-to-server.md)  
 Describe las conversiones de fecha y hora realizadas entre una aplicación cliente escrita con OLE DB de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client y [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] (o posterior).  
  
 [Conversiones realizadas de servidor a cliente](../../relational-databases/native-client-ole-db-date-time/conversions-performed-from-server-to-client.md)  
 Describe las conversiones de fecha y hora realizadas entre [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] (o posterior) y una aplicación cliente escrita con OLE DB de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client.  
  
## <a name="see-also"></a>Consulte también  
 [Mejoras de fecha y hora &#40;OLE DB&#41;](../../relational-databases/native-client-ole-db-date-time/date-and-time-improvements-ole-db.md)  
  
  
