---
description: MSSQLSERVER_15599
title: MSSQLSERVER_15599 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: language-reference
helpviewer_keywords:
- 15599 (Database Engine error)
ms.assetid: 97e427a9-8587-46ea-954b-974b5df9c223
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: eca555fb3ced04a0258db78c89c53e8cef9d9c20
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/17/2020
ms.locfileid: "88333821"
---
# <a name="mssqlserver_15599"></a>MSSQLSERVER_15599
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  
## <a name="details"></a>Detalles  
  
| Atributo | Value |  
| :-------- | :---- |  
|Nombre de producto|SQL Server|  
|Id. de evento|15599|  
|Origen de eventos|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nombre simbólico|SEC_LOCAL_TEMP_AUDIT_PERMISSIONS|  
|Texto del mensaje|No se pueden establecer permisos ni auditoría y en objetos temporales locales.|  
  
## <a name="explanation"></a>Explicación  
La auditoría y los permisos no tienen ningún efecto cuando se establecen en objetos locales o globales temporales. Las instrucciones no producen un error (las operaciones vuelven correctamente), pero no tienen ningún efecto.  
  
Este comportamiento no ha cambiado, pero a partir de [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)], este mensaje informativo alerta al usuario.  
  
## <a name="user-action"></a>Acción del usuario  
No es necesaria ninguna acción, pero considere la posibilidad de quitar las instrucciones que intentan establecer la auditoría o los permisos en objetos locales o globales temporales.  
  
