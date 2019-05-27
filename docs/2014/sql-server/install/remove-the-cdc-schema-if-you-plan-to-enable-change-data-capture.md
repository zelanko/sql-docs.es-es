---
title: Quitar el esquema cdc si va a habilitar la captura de datos modificados | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- cdc schema
- change data capture
ms.assetid: 6a84aa25-0f31-4be3-b2dd-4f249b8254ae
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: cc580a6032a19eb8248759669278f8730fc617cb
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/23/2019
ms.locfileid: "66092947"
---
# <a name="remove-the-cdc-schema-if-you-plan-to-enable-change-data-capture"></a>Quitar el esquema cdc si se piensa habilitar la captura de datos modificados
  Una base de datos ya contiene un esquema cdc. Si piensa habilitar la captura de datos modificados después de la actualización, debe quitar primero este esquema cdc. Al habilitar una base de datos para la captura de datos modificados, [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] creará un nuevo esquema cdc.  
  
  
