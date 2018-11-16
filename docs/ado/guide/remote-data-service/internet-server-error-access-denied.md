---
title: 'Error en servidor Internet: Acceso denegado | Microsoft Docs'
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
manager: craigg
ms.openlocfilehash: 2b7c562e57341dd027a4cd9bdc3a0fa4bbe51ae5
ms.sourcegitcommit: 1a5448747ccb2e13e8f3d9f04012ba5ae04bb0a3
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/12/2018
ms.locfileid: "51558402"
---
# <a name="internet-server-error-access-denied"></a>Error en servidor Internet: acceso denegado
Si recibe este error, normalmente significa que Microsoft Internet Information Services (IIS) devolvió el estado siguiente:  
  
 HTTP_STATUS_DENIED 401  
  
 Asegúrese de que los directorios que se tiene acceso a IIS tienen los permisos adecuados. RDS se puede comunicar con un servidor Web de IIS que se ejecuta en uno de los tres modos de autenticación de contraseña: anónimo, básico o desafío/respuesta de NT (denominada autenticación de Windows integrada en Windows 2000). Además, el servidor Web debe tener permisos en el equipo de origen de datos si es un equipo con Windows NT o Windows 2000.  
  
> [!IMPORTANT]
>  A partir de Windows 8 y Windows Server 2012, componentes de servidor RDS ya no están incluidos en el sistema operativo de Windows (consulte Windows 8 y [Windows Server 2012 Compatibility Cookbook](https://www.microsoft.com/download/details.aspx?id=27416) para obtener más detalles). Componentes de cliente RDS se quitará en una versión futura de Windows. Evite utilizar esta característica en nuevos trabajos de desarrollo y tenga previsto modificar las aplicaciones que actualmente la utilizan. Deben migrar las aplicaciones que usan RDS a [WCF Data Service](https://go.microsoft.com/fwlink/?LinkId=199565).  
  
## <a name="see-also"></a>Vea también  
 [Aspectos básicos de RDS](../../../ado/guide/remote-data-service/rds-fundamentals.md)




