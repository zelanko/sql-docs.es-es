---
title: "server trigger recursion (opci&#243;n de configuraci&#243;n del servidor) | Microsoft Docs"
ms.custom: ""
ms.date: "03/02/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "database-engine"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "desencadenadores recursivos [SQL Server]"
  - "desencadenadores [SQL Server], recursivos"
  - "server trigger recursion, opción"
ms.assetid: da4c25f5-d04c-4951-a3db-409e71a1b468
caps.latest.revision: 24
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 24
---
# server trigger recursion (opci&#243;n de configuraci&#243;n del servidor)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Use la opción **server trigger recursion** para especificar si se permite la activación repetida de los desencadenadores del servidor. Cuando esta opción se establece en 1 (activada), se permite esta activación repetida. Cuando el valor es 0 (desactivada), los desencadenadores del servidor no pueden activarse repetidamente. Cuando la opción server trigger recursion se establece en 0 (desactivada), solo se impide la recursividad directa. (Para deshabilitar la recursividad indirecta, establezca la opción **nested triggers** en 0). El valor predeterminado para esta opción es 1 (activada). El valor surte efecto inmediatamente (sin necesidad de reiniciar el servidor).  
  
 Para obtener más información, vea [Crear desencadenadores anidado](../../relational-databases/triggers/create-nested-triggers.md).  
  
## Vea también  
 [RECONFIGURE &#40;Transact-SQL&#41;](../../t-sql/language-elements/reconfigure-transact-sql.md)   
 [Opciones de configuración de servidor &#40;SQL Server&#41;](../../database-engine/configure-windows/server-configuration-options-sql-server.md)   
 [sp_configure &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md)  
  
  