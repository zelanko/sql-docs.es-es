---
description: dbo.sysnotifications (Transact-SQL)
title: Notificaciones de dbo.sys(Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- dbo.sysnotifications_TSQL
- sysnotifications
- sysnotifications_TSQL
- dbo.sysnotifications
dev_langs:
- TSQL
helpviewer_keywords:
- sysnotifications system table
ms.assetid: c5150d18-e8b7-48a7-ada7-77c583af6e41
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 8bcfd6b5b52a4f091337d55681be149ccd3f7900
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 09/08/2020
ms.locfileid: "89540373"
---
# <a name="dbosysnotifications-transact-sql"></a>dbo.sysnotifications (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  Contiene una fila por cada notificación.  
  
|Nombre de la columna|Tipo de datos|Descripción|  
|-----------------|---------------|-----------------|  
|**alert_id**|**int**|IDENTIFICADOR de la alerta.|  
|**operator_id**|**int**|Id. del operador al que se debe enviar la notificación.|  
|**notification_method**|**tinyint**|Método de notificación:<br /><br /> **1** = correo electrónico<br /><br /> **2** = buscapersonas<br /><br /> **4**  =  **NetSend**<br /><br /> **7** = todo|  
  
  
