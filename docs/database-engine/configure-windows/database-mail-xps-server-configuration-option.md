---
title: Database Mail XPs (opción de configuración del servidor) | Microsoft Docs
ms.custom: ''
ms.date: 11/27/2018
ms.prod: sql
ms.prod_service: high-availability
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
helpviewer_keywords:
- Database Mail XPs option
- Database Mail [SQL Server], enabling
ms.assetid: e22c4e63-1792-473b-af11-14a7931ca9ed
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: e16286e558d860a346ba8fff366009f064e65f91
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 02/01/2020
ms.locfileid: "68011957"
---
# <a name="database-mail-xps-server-configuration-option"></a>Database Mail XPs (opción de configuración del servidor)

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

Use la opción **DatabaseMail XPs** para habilitar Correo electrónico de base de datos en este servidor. Los valores posibles son:  
  
- `0`: Correo electrónico de base de datos no está disponible (el valor predeterminado).  
  
- `1`: Correo electrónico de base de datos está disponible.  
  
 La configuración surte efecto inmediatamente, sin necesidad de detener y reiniciar el servidor.  
  
 Tras habilitar Correo electrónico de base de datos, debe configurar una base de datos host de Correo electrónico de base de datos para usar Correo electrónico de base de datos.  
  
 Configurar la base de datos con el **Asistente para configuración del correo electrónico de base de datos** habilita los procedimientos almacenados extendidos de Correo electrónico de base de datos en la base de datos `msdb`. Si usa el **Asistente para configuración del correo electrónico de base de datos**, no tiene que usar el ejemplo `sp_configure` siguiente.  
  
 Si establece la opción **Mail XPs de base de datos** en `0`, impide que se inicie Correo electrónico de base de datos. Si está en ejecución cuando se establece la opción en `0`, continúa ejecutándose y enviando correo hasta que permanece inactivo durante el tiempo configurado en la opción `DatabaseMailExeMinimumLifeTime`.  
  
## <a name="examples"></a>Ejemplos
 En el ejemplo siguiente se habilitan los procedimientos almacenados extendidos de Correo electrónico de base de datos.  
  
```  
sp_configure 'show advanced options', 1;  
GO  
RECONFIGURE;  
GO  
sp_configure 'Database Mail XPs', 1;  
GO  
RECONFIGURE  
GO  
```  

En el ejemplo siguiente se habilitan los procedimientos almacenados extendidos de Correo electrónico de base de datos si todavía no está habilitado.

```sql
IF EXISTS (
    SELECT 1 FROM sys.configurations 
    WHERE NAME = 'Database Mail XPs' AND VALUE = 0)
BEGIN
  PRINT 'Enabling Database Mail XPs'
  EXEC sp_configure 'show advanced options', 1;  
  RECONFIGURE
  EXEC sp_configure 'Database Mail XPs', 1;  
  RECONFIGURE  
END
```

## <a name="see-also"></a>Consulte también
[Correo electrónico de base de datos](../../relational-databases/database-mail/database-mail.md)  
