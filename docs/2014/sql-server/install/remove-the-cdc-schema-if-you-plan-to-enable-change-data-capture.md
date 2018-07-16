---
title: Quitar el esquema cdc si va a habilitar la captura de datos modificados | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- cdc schema
- change data capture
ms.assetid: 6a84aa25-0f31-4be3-b2dd-4f249b8254ae
caps.latest.revision: 8
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: f76517b1d97e9304569685ca4df4d3f5a5d57e7f
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/02/2018
ms.locfileid: "37222555"
---
# <a name="remove-the-cdc-schema-if-you-plan-to-enable-change-data-capture"></a>Quitar el esquema cdc si se piensa habilitar la captura de datos modificados
  Una base de datos ya contiene un esquema cdc. Si piensa habilitar la captura de datos modificados después de la actualización, debe quitar primero este esquema cdc. Al habilitar una base de datos para la captura de datos modificados, [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] creará un nuevo esquema cdc.  
  
  
