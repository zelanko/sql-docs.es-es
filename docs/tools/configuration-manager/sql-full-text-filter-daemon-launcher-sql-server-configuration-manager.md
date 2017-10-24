---
title: "Selector de demonio de filtro de texto completo SQL (Administrador de configuración de SQL Server) | Documentos de Microsoft"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: d0dc03db-5f76-4558-b041-1ac7b9b5bb16
caps.latest.revision: 8
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 3b4768f274310400e99a355676b2c0cd7a27666e
ms.contentlocale: es-es
ms.lasthandoff: 08/02/2017

---
# <a name="sql-full-text-filter-daemon-launcher-sql-server-configuration-manager"></a>Selector de demonio de filtro de texto completo de SQL (Administrador de configuración de SQL Server)
  A partir de [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)], [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] utiliza el servicio del iniciador del demonio de filtro de la búsqueda de texto completo (iniciador de FDHOST) para iniciar el proceso de host de demonio de filtro, que administra las operaciones de filtrado y separación de palabras de la búsqueda de texto completo. Este servicio debe estar ejecutándose para poder utilizar la búsqueda de texto completo. El servicio del iniciador de FDHOST reconoce las instancias y está asociado a una instancia concreta de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. El servicio del iniciador de FDHOST propaga la información de la cuenta de servicio a cada proceso de host de demonio de filtro iniciado. Para obtener información sobre los procesos de host de demonio de filtro, vea "Arquitectura de la búsqueda de texto completo" en los Libros en pantalla de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
  

