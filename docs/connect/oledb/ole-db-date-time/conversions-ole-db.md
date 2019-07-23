---
title: Enlaces y conversiones (OLE DB) | Microsoft Docs
description: Enlaces y conversiones (OLE DB)
ms.custom: ''
ms.date: 06/14/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
helpviewer_keywords:
- conversions [OLE DB]
- bindings [OLE DB]
- OLE DB, bindings and conversions
author: pmasl
ms.author: pelopes
ms.openlocfilehash: dc86193f40474fc373c1b0e7dd48e579e8548821
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "68015838"
---
# <a name="conversions-ole-db"></a>Conversiones (OLE DB)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  En esta sección se describe cómo convertir entre valores **DateTime** y **DateTimeOffset** . OLE DB ya proporciona las conversiones descritas en esta sección o son una extensión coherente de OLE DB.  
  
 El formato de literales y cadenas para las fechas y horas en OLE DB generalmente sigue la ISO y no depende de la configuración regional del cliente. Una excepción es DBTYPE_DATE, donde la norma es OLE Automation. Sin embargo, como OLE DB controlador para SQL Server solo convierte entre tipos cuando los datos se transmiten a o desde el cliente, no hay ninguna manera de que una aplicación fuerce OLE DB controlador de SQL Server para la conversión entre DBTYPE_DATE y formatos de cadena. De lo contrario, las cadenas usan los formatos siguientes (el texto entre corchetes indica un elemento opcional):  
  
-   El formato de las cadenas **DateTime** y **DateTimeOffset** es el siguiente:  
  
     *aaaa*-*mm*-*dd*[ *hh*:*mm*:*ss*[.*9999999*][ ± *hh*:*mm*]]  
  
-   El formato de las cadenas **time** es:  
  
     *hh*:*mm*:*ss*[.*9999999*]  
  
-   El formato de las cadenas de **fecha** es:  
  
     *aaaa*-*mm*-*dd*  
  
> [!NOTE]  
>  Las versiones anteriores de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client y de las conversiones OLE implementadas SQLOLEDB, en caso de un error en las conversiones estándar. El controlador de OLE DB para SQL Server sigue el mismo comportamiento [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] que Native Client. Como resultado, algunas conversiones realizadas por OLE DB controlador para SQL Server difieren de la especificación de OLE DB.  
  
 Las conversiones de las cadenas permiten flexibilidad en los espacios en blanco y el ancho de campo. Para obtener más información, vea la sección "formatos de datos: cadenas y literales" en [compatibilidad con tipos de datos para obtener OLE DB mejoras de fecha y hora](../../oledb/ole-db-date-time/data-type-support-for-ole-db-date-and-time-improvements.md).  
  
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
 [Conversiones realizadas de cliente a servidor](../../oledb/ole-db-date-time/conversions-performed-from-client-to-server.md)  
 Describe las conversiones de fecha y hora realizadas entre una aplicación cliente escrita con el controlador OLE DB para SQL Server y [!INCLUDE[ssKatmai](../../../includes/sskatmai-md.md)] (o posterior).  
  
 [Conversiones realizadas de servidor a cliente](../../oledb/ole-db-date-time/conversions-performed-from-server-to-client.md)  
 Describe las conversiones de fecha y hora realizadas entre [!INCLUDE[ssKatmai](../../../includes/sskatmai-md.md)] (o posterior) y una aplicación cliente escrita con el controlador OLE DB para SQL Server.  
  
## <a name="see-also"></a>Consulte también  
 [Mejoras de fecha y hora &#40;OLE DB&#41;](../../oledb/ole-db-date-time/date-and-time-improvements-ole-db.md)  
  
  
