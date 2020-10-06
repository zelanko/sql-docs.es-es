---
description: Configuración de servidores virtuales en IIS
title: Configuración de servidores virtuales en IIS | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 11/09/2018
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- virtual servers in RDS [ADO]
ms.assetid: 2b4786c6-40c4-4ce1-9ad4-03df436e0aff
author: rothja
ms.author: jroth
ms.openlocfilehash: b8e1899e6393f1dc7ae4d9b2080d349bbedf1d41
ms.sourcegitcommit: c7f40918dc3ecdb0ed2ef5c237a3996cb4cd268d
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/05/2020
ms.locfileid: "91724796"
---
# <a name="configuring-virtual-servers-on-iis"></a>Configuración de servidores virtuales en IIS
Al crear servidores virtuales en Internet Information Services 4,0, se necesitan los dos pasos adicionales siguientes para configurar el servidor virtual para que funcione con RDS:  
  
1.  Al configurar el servidor, Active "permitir acceso de ejecución".  
  
2.  Mueva msadcs.dll a *vroot*\msadc, donde *vroot* es el directorio principal del servidor virtual.  
  
> [!IMPORTANT]
>  A partir de Windows 8 y Windows Server 2012, los componentes de servidor RDS ya no se incluyen en el sistema operativo Windows (consulte la guía de compatibilidad de Windows 8 y [Windows server 2012](https://www.microsoft.com/download/details.aspx?id=27416) para obtener más detalles). Los componentes de cliente RDS se quitarán en una versión futura de Windows. Evite utilizar esta característica en nuevos trabajos de desarrollo y tenga previsto modificar las aplicaciones que actualmente la utilizan. Las aplicaciones que utilizan RDS deben migrar al [servicio de datos de WCF](/dotnet/framework/wcf/).  
  
## <a name="see-also"></a>Consulte también  
 [Aspectos básicos de RDS](./rds-fundamentals.md)