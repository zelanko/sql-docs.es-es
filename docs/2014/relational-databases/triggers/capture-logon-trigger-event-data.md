---
title: Capturar datos de eventos de desencadenador logon | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
ms.assetid: e05b1ab4-c10b-402a-9591-f6ec1e3db8c0
author: rothja
ms.author: jroth
ms.openlocfilehash: b11323702d7468d07783b4d1c763dba691479d9c
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/18/2020
ms.locfileid: "85043063"
---
# <a name="capture-logon-trigger-event-data"></a>Capturar datos de eventos de desencadenador logon
  Para capturar datos XML acerca de los eventos LOGON para utilizarlos dentro de los desencadenadores logon, utilice la función [EVENTDATA](/sql/t-sql/functions/eventdata-transact-sql) . El evento LOGON devuelve el siguiente esquema de datos de eventos:  
  
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
  
  
