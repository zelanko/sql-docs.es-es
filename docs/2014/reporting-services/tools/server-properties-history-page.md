---
title: Propiedades del servidor (página Historial) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
f1_keywords:
- sql12.swb.reportserver.serverproperties.history.f1
ms.assetid: be9d8018-a46f-4625-9ae1-138ebe6b38ba
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: c10649c3dbe873464bcc52ca5bc54e5b948d547a
ms.sourcegitcommit: 8d6fb6bbe3491925909b83103c409effa006df88
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/22/2019
ms.locfileid: "59951281"
---
# <a name="server-properties-history-page"></a>Propiedades del servidor (página Historial)
  Utilice esta página para establecer un valor predeterminado para el número de copias del historial del informe que deben guardarse. El valor predeterminado proporciona un valor inicial que establece los límites del historial de informes para todos los informes. Existe la posibilidad de modificar esta configuración para informes individuales.  
  
 El historial de informes es una colección de instantáneas de informe que incluye datos de informe y diseño actual para el informe en el momento en que se crea la instantánea. Puede usar el historial de informes para mantener una copia de un informe como se encontraba en una fecha u hora específicas. Puede crear y administrar el historial de informes para informes individuales que se ejecutan en un servidor de informes en modo nativo o un servidor de informes que se configura para modo integrado con SharePoint.  
  
 Las instantáneas del historial de informes están almacenadas en la base de datos del servidor de informes. Si mantiene un número ilimitado de instantáneas, asegúrese de comprobar periódicamente el tamaño de la base de datos para asegurarse de que no crece demasiado rápido ni consume demasiado espacio en disco.  
  
 Para abrir esta página, inicie [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], conéctese a una instancia del servidor de informes, haga clic con el botón secundario en el nombre del servidor de informes y seleccione **Propiedades**. Haga clic en **Historial** para abrir esta página.  
  
## <a name="options"></a>Opciones  
 **Conservar un número ilimitado de instantáneas en el historial de informe**  
 Conserve todas las instantáneas del historial de informes. Para reducir el tamaño del historial de informe, debe eliminar las instantáneas manualmente.  
  
 **Limitar las copias del historial de informe**  
 Conserve un número fijo de instantáneas del historial de informes. Cuando se alcanza el límite, las copias más antiguas se eliminan del historial de informe para dejar sitio para las nuevas.  
  
 Si posteriormente limita el historial del informe, cuando el historial del informe existente exceda el límite especificado, el servidor de informes lo reducirá según el nuevo límite. Las instantáneas de informe más antiguas son las que se eliminan primero. Si el historial del informe está vacío o por debajo del límite, se agregan nuevas instantáneas de informe. Cuando se alcanza el límite, se elimina la instantánea del informe más antigua cuando se agrega una nueva.  
  
## <a name="see-also"></a>Vea también  
 [Establecer las propiedades del servidor de informes &#40;Management Studio&#41;](set-report-server-properties-management-studio.md)   
 [Conectar con un servidor de informes en Management Studio](connect-to-a-report-server-in-management-studio.md)   
 [Servidor de informes en Management Studio (Ayuda F1)](report-server-in-management-studio-f1-help.md)  
  
  
