---
description: Reservas de direcciones URL para implementaciones del servidor de informes de varias instancias
title: Reservas de direcciones URL para implementaciones del servidor de informes de varias instancias | Microsoft Docs
ms.date: 05/18/2016
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- URL reservations
ms.assetid: f67c83c0-1f74-42bb-bfc1-e50c38152d3d
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 53d12c7441b796bf4564bbaf05a84ecfd7aae86a
ms.sourcegitcommit: fe59f8dc27fd633f5dfce54519d6f5dcea577f56
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 10/09/2020
ms.locfileid: "91934569"
---
# <a name="url-reservations-for-multi-instance-report-server-deployments"></a>Reservas de direcciones URL para implementaciones del servidor de informes de varias instancias
  Si instala varias instancias de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] en el mismo equipo, debe tener en cuenta cómo va a definir las reservas de direcciones URL para cada instancia. En cada instancia, el servicio web del servidor de informes y el [!INCLUDE[ssRSWebPortal](../../includes/ssrswebportal.md)] deben tener al menos una reserva de direcciones URL cada uno. El conjunto completo de reservas debe ser único en HTTP.SYS.  
  
 Las direcciones URL duplicadas se detectan durante el registro de direcciones URL, que tiene lugar cuando se inicia el servicio. Si crea reservas de direcciones URL que no son únicas, el conflicto entre nombres no se puede detectar hasta que inicie el servicio. Por esta razón, debe seguir las reglas o convenciones de nomenclatura para garantizar que todos los valores son únicos.  
  
## <a name="default-naming-conventions"></a>Convenciones de nomenclatura predeterminadas  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] se puede instalar en una instancia con nombre de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Al instalar o configurar un servidor de informes en una instancia con nombre, el nombre de la instancia se incluye automáticamente en el directorio virtual en la reserva de direcciones URL predeterminada proporcionada por [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] . La tabla siguiente muestra las reservas de direcciones URL para una instancia predeterminada y una instancia con nombre.  
  
|Instancia de SQL Server|Reserva de direcciones URL predeterminada|  
|-------------------------|-----------------------------|  
|Predeterminada (MSSQLServer)|`https://+:80/reportserver`|  
|Con nombre (MynamedInstance)|`https://+:80/reportserver_MyNamedInstance`|  
  
 Para la instancia con nombre, el directorio virtual incluye el nombre de la instancia. Tanto la instancia predeterminada como la instancia con nombre escuchan en el mismo puerto, pero los nombres de directorios virtuales únicos determinan qué servidor de informes obtiene la solicitud.  
  
 Los procedimientos recomendados consisten en utilizar el nombre de directorio virtual para distinguir entre la instancia del servidor de informes. Proporciona una correspondencia clara entre una dirección URL y la instancia de destino, y garantiza que los nombres de aplicación son únicos en todo el sistema.  
  
## <a name="custom-naming-conventions"></a>Convenciones de nomenclatura personalizadas  
 Aunque se recomienda utilizar el nombre de la instancia, se pueden usar la sintaxis de la dirección URL y las convenciones de nomenclatura propias para cumplir las restricciones de nombre único para reservas de direcciones URL. Los ejemplos siguientes muestran los distintos enfoques para crear direcciones URL únicas para cada instancia.  
  
|Instancia predeterminada del servidor de informes (MSSQLSERVER)|ReportServer_MyNamedInstance|Unicidad|  
|----------------------------------------------------|-----------------------------------|----------------|  
|`https://+:80/reportserver`|`https://+:8888/reportserver`|Cada instancia escucha en un puerto diferente.|  
|`https://www.contoso.com/reportserver`|`https://SRVR-46/reportserver`|Cada instancia responde a nombres de servidor diferentes (nombre de dominio completo y nombre de equipo).|  
  
## <a name="uniqueness-requirements"></a>Requisitos de unicidad  
 Las tecnologías subyacentes utilizadas por [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] imponen los requisitos relativos a nombres únicos. HTTP.SYS requiere que todas las direcciones URL de su repositorio sean únicas. Puede cambiar el puerto, el nombre de host o el nombre de directorio virtual para crear una dirección URL única. [!INCLUDE[vstecasp](../../includes/vstecasp-md.md)] requiere que las identidades de aplicaciones sean únicas en el mismo proceso. Este requisito afecta a los nombres de directorio virtuales. Especifica que no se puede duplicar un nombre de directorio virtual en la misma instancia del servidor de informes.  
  
## <a name="see-also"></a>Consulte también  
 [Configurar las direcciones URL del servidor de informes &#40;Administrador de configuración del servidor de informes&#41;](../../reporting-services/install-windows/configure-report-server-urls-ssrs-configuration-manager.md)   
 [Configuración de una URL &#40;Administrador de configuración del servidor de informes&#41;](../../reporting-services/install-windows/configure-a-url-ssrs-configuration-manager.md)  
  
  
