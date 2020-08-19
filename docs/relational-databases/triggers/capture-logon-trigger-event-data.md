---
description: Capturar datos de eventos de desencadenador logon
title: Capturar datos de eventos de desencadenador logon | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
ms.assetid: e05b1ab4-c10b-402a-9591-f6ec1e3db8c0
author: rothja
ms.author: jroth
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 8511e1021383921d52a190cb9df80b3d5939060a
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/17/2020
ms.locfileid: "88418909"
---
# <a name="capture-logon-trigger-event-data"></a>Capturar datos de eventos de desencadenador logon
[!INCLUDE[tsql-appliesto-ss2008-appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdbmi-xxxx-xxx-md.md)]
   Para capturar datos XML acerca de los eventos LOGON para utilizarlos dentro de los desencadenadores logon, utilice la función [EVENTDATA](../../t-sql/functions/eventdata-transact-sql.md). El evento LOGON devuelve el siguiente esquema de datos de eventos:  
  
 `<EVENT_INSTANCE>`  
  
 `<EventType>event_type</EventType>`  
  
 `<PostTime>post_time</PostTime>`  
  
 `<SPID>spid</SPID>`  
  
 `<ServerName>server_name</ServerName>`  
  
 `<LoginName>login_name</LoginName>`  
  
 `<LoginType>login_type</LoginType>`  
  
 `<SID>sid</SID>`  
  
 `<ClientHost>client_host</ClientHost>`  
  
 `<IsPooled>is_pooled</IsPooled>`  
  
 `</EVENT_INSTANCE>`  
  
 `<EventType>`  
 Contiene `LOGON`.  
  
 `<PostTime>`  
 Contiene la hora en la que se solicita que se establezca una sesión.  
  
 `<SID>`  
 Contiene el flujo binario codificado de base 64 del número de identificación de seguridad (SID) para el nombre de inicio de sesión especificado.  
  
 `<ClientHost>`  
 Contiene el nombre de host del cliente desde el que se realiza la conexión. El valor es '`<local_machine>`' si el nombre del cliente y del servidor son iguales. De lo contrario, el valor es la dirección IP del cliente.  
  
 `<IsPooled>`  
 Es `1` si la conexión se vuelve a utilizar empleando la agrupación de conexiones. De lo contrario, el valor es `0`.  
  
  
