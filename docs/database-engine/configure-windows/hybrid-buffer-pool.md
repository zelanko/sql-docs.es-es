---
title: Grupo de búferes híbrido | Microsoft Docs
ms.custom: ''
ms.date: 11/06/2018
ms.prod: sql
ms.prod_service: high-availability
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
ms.assetid: ''
author: DBArgenis
ms.author: argenisf
manager: craigg
ms.openlocfilehash: a8098c38b72ba44ab973fe5564b93740252bafc6
ms.sourcegitcommit: 1a5448747ccb2e13e8f3d9f04012ba5ae04bb0a3
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 11/12/2018
ms.locfileid: "51560312"
---
# <a name="hybrid-buffer-pool"></a>Grupo de búferes híbrido
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

Con SQL Server 2019 CTP 2.1 se ha introducido una característica nueva en el motor de base de datos de SQL Server que permite acceder directamente a las páginas de datos de los archivos de base de datos almacenados en dispositivos de memoria persistente (PMEM). 

En un sistema tradicional sin memoria persistente, SQL Server almacena en caché las páginas de datos en el grupo de búferes. Con Grupo de búferes híbrido, SQL Server omite la realización de una copia de la página en la parte basada en DRAM del grupo de búferes y, en su lugar, hace referencia a la página directamente en el archivo de base de datos que se encuentra en un dispositivo PMEM. El acceso a los archivos de datos en PMEM para el grupo de búferes híbrido se realiza mediante la E/S asignada a la memoria, también conocido como habilitación.

En un dispositivo PMEM solo se puede hacer referencia directamente a páginas limpias. Cuando una página está desfasada, se mantiene en DRAM y, después, se vuelve a escribir en el dispositivo PMEM.

Esta característica está disponible en Windows y Linux.

## <a name="enable-hybrid-buffer-pool"></a>Habilitación del grupo de búferes híbrido

En CTP 2.1, debe habilitar la marca de seguimiento de inicio 809 para poder usar el grupo de búferes híbrido.

## <a name="best-practices-for-hybrid-buffer-pool"></a>Procedimientos recomendados para el grupo de búferes híbrido

* Al dar formato al dispositivo PMEM en Windows, use el tamaño de unidad de asignación más grande disponible para NTFS (2 MB en Windows Server 2019) y asegúrese de que el dispositivo se ha habilitado para DAX (DirectAccess).
  