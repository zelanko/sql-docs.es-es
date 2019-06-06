---
title: 'Error del servidor de Internet: Acceso denegado | Microsoft Docs'
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 11/09/2018
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- access denied error in RDS [ADO]
ms.assetid: e5b43cfa-da8d-430d-a2ab-5443dda47a16
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 1a7dbb125c3a320ac380d91b71aff7826c17e15d
ms.sourcegitcommit: 074d44994b6e84fe4552ad4843d2ce0882b92871
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/05/2019
ms.locfileid: "66718315"
---
# <a name="internet-server-error-access-denied"></a>Error del servidor de Internet: Acceso denegado
Si recibe este error, normalmente significa que Microsoft Internet Information Services (IIS) devolvió el estado siguiente:  
  
 HTTP_STATUS_DENIED 401  
  
 Asegúrese de que los directorios que se tiene acceso a IIS tienen los permisos adecuados. RDS se puede comunicar con un servidor Web de IIS que se ejecuta en uno de los tres modos de autenticación de contraseña: Anonymous, Basic o NT desafío/respuesta (llamada autenticación de Windows integrada en Windows 2000). Además, el servidor Web debe tener permisos en el equipo de origen de datos si es un equipo con Windows NT o Windows 2000.  
  
> [!IMPORTANT]
>  A partir de Windows 8 y Windows Server 2012, componentes de servidor RDS ya no están incluidos en el sistema operativo de Windows (consulte Windows 8 y [Windows Server 2012 Compatibility Cookbook](https://www.microsoft.com/download/details.aspx?id=27416) para obtener más detalles). Componentes de cliente RDS se quitará en una versión futura de Windows. Evite utilizar esta característica en nuevos trabajos de desarrollo y tenga previsto modificar las aplicaciones que actualmente la utilizan. Deben migrar las aplicaciones que usan RDS a [WCF Data Service](https://go.microsoft.com/fwlink/?LinkId=199565).  
  
## <a name="see-also"></a>Vea también  
 [Aspectos básicos de RDS](../../../ado/guide/remote-data-service/rds-fundamentals.md)




