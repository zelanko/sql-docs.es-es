---
title: Quitar el esquema CDC si tiene previsto habilitar la captura de datos modificados | Microsoft Docs
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
ms.openlocfilehash: abdb33fa3d1ff022a65ed569f19d48bcf4468501
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/18/2020
ms.locfileid: "85059150"
---
# <a name="remove-the-cdc-schema-if-you-plan-to-enable-change-data-capture"></a>Quitar el esquema cdc si se piensa habilitar la captura de datos modificados
  Una base de datos ya contiene un esquema cdc. Si piensa habilitar la captura de datos modificados después de la actualización, debe quitar primero este esquema cdc. Al habilitar una base de datos para la captura de datos modificados, [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] creará un nuevo esquema cdc.  
  
  
