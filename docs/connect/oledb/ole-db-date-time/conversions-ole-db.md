---
title: Enlaces y conversiones (OLE DB) | Documentos de Microsoft
description: Enlaces y conversiones (OLE DB)
ms.custom: ''
ms.date: 03/26/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: ''
ms.component: ole-db-date-time
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- conversions [OLE DB]
- bindings [OLE DB]
- OLE DB, bindings and conversions
author: pmasl
ms.author: Pedro.Lopes
manager: craigg
ms.openlocfilehash: 88160d0c1e8e2b8b891920a37f7596a57b5efb36
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="conversions-ole-db"></a>Conversiones (OLE DB)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  En esta sección se describe cómo convertir entre **datetime** y **datetimeoffset** valores. OLE DB ya proporciona las conversiones descritas en esta sección o son una extensión coherente de OLE DB.  
  
 El formato de literales y cadenas para las fechas y horas en OLE DB generalmente sigue la ISO y no depende de la configuración regional del cliente. Una excepción es DBTYPE_DATE, donde la norma es OLE Automation. Sin embargo, porque el controlador OLE DB para SQL Server sólo realiza conversiones entre tipos cuando se transmiten datos a o desde el cliente, no hay ninguna manera de una aplicación forzar el controlador OLE DB para SQL Server realizar conversiones entre los formatos de cadena y DBTYPE_DATE. De lo contrario, las cadenas usan los formatos siguientes (el texto entre corchetes indica un elemento opcional):  
  
-   El formato de **datetime** y **datetimeoffset** cadenas es:  
  
     *aaaa*-*mm*-*dd*[ *hh*:*mm*:*ss*[. *9999999*] [± *hh*:*mm*]]  
  
-   El formato de **tiempo** cadenas es:  
  
     *hh*:*mm*:*ss*[. *9999999*]  
  
-   El formato de **fecha** cadenas es:  
  
     *aaaa*-*mm*-*dd*  
  
> [!NOTE]  
>  Las versiones anteriores de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client y de las conversiones OLE implementadas SQLOLEDB, en caso de un error en las conversiones estándar. El controlador OLE DB para SQL Server sigue el mismo comportamiento que [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client. Como resultado, algunas conversiones realizadas por el controlador OLE DB para SQL Server son distintas de la especificación de OLE DB.  
  
 Las conversiones de las cadenas permiten flexibilidad en los espacios en blanco y el ancho de campo. Para obtener más información, vea la sección "Formatos de datos: cadenas y literales" de [compatibilidad de tipos de datos para mejoras de hora y fecha de OLE DB](../../oledb/ole-db-date-time/data-type-support-for-ole-db-date-and-time-improvements.md).  
  
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
  
## <a name="see-also"></a>Vea también  
 [Fecha y hora mejoras & #40; OLE DB & #41;](../../oledb/ole-db-date-time/date-and-time-improvements-ole-db.md)  
  
  
