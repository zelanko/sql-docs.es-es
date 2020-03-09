---
title: Conexión de contexto
description: Describe la conexión de contexto.
ms.date: 08/15/2019
ms.assetid: e443ca86-9243-4234-a822-ed10a53a9de0
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
author: rothja
ms.author: jroth
ms.reviewer: v-kaywon
ms.openlocfilehash: 6dd4260fa15b737ce6b1411056b82bac93f33fa6
ms.sourcegitcommit: 610e49c3e1fa97056611a85e31e06ab30fd866b1
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 03/07/2020
ms.locfileid: "78897009"
---
# <a name="the-context-connection"></a>Conexión de contexto

[!INCLUDE[Driver_ADONET_Download](../../../includes/driver_adonet_download.md)]

El problema de acceso interno a los datos es un escenario bastante común. Es decir, desea tener acceso al mismo servidor en que se ejecuta el procedimiento almacenado o función de Common Language Runtime (CLR). Una opción es crear una conexión mediante <xref:Microsoft.Data.SqlClient.SqlConnection>, especificar una cadena de conexión que señale al servidor local y abrir la conexión. Esto requiere especificar las credenciales para iniciar sesión. La conexión está en una sesión de base de datos distinta que el procedimiento almacenado o función, puede tener opciones `SET` distintas, está en una transacción aparte, no ve las tablas temporales, etc. Si el código del procedimiento almacenado administrado o de la función está en ejecución en el proceso de SQL Server, es porque alguien se ha conectado a ese servidor y ha ejecutado una instrucción SQL para invocarlo. Probablemente desea que el procedimiento almacenado o función se ejecute en el contexto de esa conexión, junto con la transacción, las opciones `SET`, etc. Esto se denomina la conexión de contexto.  
  
La conexión de contexto le permite ejecutar las instrucciones Transact-SQL en el mismo contexto que se invocó el código en primer lugar. Para obtener más información, vea el tema [La conexión de contexto](https://go.microsoft.com/fwlink/?LinkId=115395) en los Libros en pantalla de SQL Server.
