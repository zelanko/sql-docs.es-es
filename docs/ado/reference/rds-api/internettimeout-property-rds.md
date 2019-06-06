---
title: La propiedad InternetTimeout (RDS) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
helpviewer_keywords:
- InternetTimeout property [ADO]
ms.assetid: 4d1c8892-4bbc-4e71-bf4b-ba52c0ea9549
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 6a5886ae206f3b16f30da406a8ccc42cc8cba7a0
ms.sourcegitcommit: 074d44994b6e84fe4552ad4843d2ce0882b92871
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/05/2019
ms.locfileid: "66712456"
---
# <a name="internettimeout-property-rds"></a>Propiedad InternetTimeout (RDS)
Indica el número de milisegundos que transcurrirán antes de que una solicitud agota el tiempo.  
  
> [!IMPORTANT]
>  A partir de Windows 8 y Windows Server 2012, componentes de servidor RDS ya no están incluidos en el sistema operativo de Windows (consulte Windows 8 y [Windows Server 2012 Compatibility Cookbook](https://www.microsoft.com/download/details.aspx?id=27416) para obtener más detalles). Componentes de cliente RDS se quitará en una versión futura de Windows. Evite utilizar esta característica en nuevos trabajos de desarrollo y tenga previsto modificar las aplicaciones que actualmente la utilizan. Deben migrar las aplicaciones que usan RDS a [WCF Data Service](https://go.microsoft.com/fwlink/?LinkId=199565).  
  
## <a name="settings-and-return-values"></a>Configuración y valores devueltos  
 Establece o devuelve un **largo** valor que representa el número de milisegundos antes de la solicitud agota el tiempo.  
  
## <a name="remarks"></a>Comentarios  
 Esta propiedad solo se aplica a las solicitudes enviadas con los protocolos HTTP o HTTPS.  
  
 Las solicitudes en un entorno de tres niveles pueden tardar varios minutos en ejecutarse. Use esta propiedad para especificar un tiempo adicional para solicitudes de ejecución prolongada.  
  
## <a name="applies-to"></a>Se aplica a  
  
|||  
|-|-|  
|[Objeto DataControl (RDS)](../../../ado/reference/rds-api/datacontrol-object-rds.md)|[Objeto DataSpace (RDS)](../../../ado/reference/rds-api/dataspace-object-rds.md)|  
  
## <a name="see-also"></a>Vea también  
 [Ejemplo de la propiedad InternetTimeout (VB)](../../../ado/reference/rds-api/internettimeout-property-example-vb.md)   
 [Ejemplo de la propiedad InternetTimeout (VC ++)](../../../ado/reference/rds-api/internettimeout-property-example-vc.md)   
 

