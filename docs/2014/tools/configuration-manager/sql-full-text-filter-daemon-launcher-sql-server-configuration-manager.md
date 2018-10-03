---
title: Selector de demonio de filtro de texto completo de SQL (Administrador de configuración de SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- configmgr-client
ms.topic: conceptual
ms.assetid: d0dc03db-5f76-4558-b041-1ac7b9b5bb16
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: ca40d5db19ef4f24e93af444a0ef8c2e7179b159
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/02/2018
ms.locfileid: "48169935"
---
# <a name="sql-full-text-filter-daemon-launcher-sql-server-configuration-manager"></a>Selector de demonio de filtro de texto completo de SQL (Administrador de configuración de SQL Server)
  A partir de [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)], [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] utiliza el servicio del iniciador del demonio de filtro de la búsqueda de texto completo (iniciador de FDHOST) para iniciar el proceso de host de demonio de filtro, que administra las operaciones de filtrado y separación de palabras de la búsqueda de texto completo. Este servicio debe estar ejecutándose para poder utilizar la búsqueda de texto completo. El servicio del iniciador de FDHOST reconoce las instancias y está asociado a una instancia concreta de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. El servicio del iniciador de FDHOST propaga la información de la cuenta de servicio a cada proceso de host de demonio de filtro iniciado. Para obtener información sobre los procesos de host de demonio de filtro, vea "Arquitectura de la búsqueda de texto completo" en los Libros en pantalla de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
  
