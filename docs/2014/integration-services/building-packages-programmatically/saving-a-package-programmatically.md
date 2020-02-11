---
title: Guardar un paquete mediante programación | Microsoft Docs
ms.custom: ''
ms.date: 04/27/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: reference
helpviewer_keywords:
- programmatically saving a package
- saving a package programmatically
ms.assetid: 4204f817-d5df-475a-9338-d7f01305d566
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 0304d4ba3388874fbd2c19001b12094f1df4d351
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "62836714"
---
# <a name="saving-a-package-programmatically"></a>Guardar un paquete mediante programación
  Después de generar un nuevo paquete o modificar uno existente mediante programación, por lo general desea guardar los cambios.  
  
 Todos los métodos utilizados en este tema para guardar paquetes requieren una referencia al ensamblado `Microsoft.SqlServer.ManagedDTS`. Después de agregar la referencia en un proyecto nuevo, importe el <xref:Microsoft.SqlServer.Dts.Runtime> espacio de nombres `using` con `Imports` una instrucción o.  
  
## <a name="saving-a-package-programmatically"></a>Guardar un paquete mediante programación  
 Para guardar un paquete mediante programación, llame a uno de los métodos siguientes de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] <xref:Microsoft.SqlServer.Dts.Runtime.Application> la clase:  
  
|Ubicación de almacenamiento|Método que se llama|  
|----------------------|--------------------|  
|Archivo|<xref:Microsoft.SqlServer.Dts.Runtime.Application.SaveToXml%2A>|  
|Almacén de paquetes SSIS|<xref:Microsoft.SqlServer.Dts.Runtime.Application.SaveToDtsServer%2A>|  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|<xref:Microsoft.SqlServer.Dts.Runtime.Application.SaveToSqlServer%2A><br /><br /> or<br /><br /> <xref:Microsoft.SqlServer.Dts.Runtime.Application.SaveToSqlServerAs%2A>|  
  
> [!IMPORTANT]  
>  Los métodos de la clase <xref:Microsoft.SqlServer.Dts.Runtime.Application> para trabajar con el almacén de paquetes SSIS solo admiten "." o el nombre del servidor local. No puede utilizar" "(local)" ni "localhost".  
  
![Integration Services icono (pequeño)](../media/dts-16.gif "Icono de Integration Services (pequeño)")  **Manténgase al día con Integration Services**<br /> Para obtener las descargas, artículos, ejemplos y vídeos más recientes de Microsoft, así como soluciones seleccionadas de la comunidad, visite la página de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] en MSDN:<br /><br /> [Visite la página de Integration Services en MSDN](https://go.microsoft.com/fwlink/?LinkId=136655)<br /><br /> Para recibir notificaciones automáticas de estas actualizaciones, suscríbase a las fuentes RSS disponibles en la página.  
  
## <a name="see-also"></a>Consulte también  
 [Guardar paquetes](../save-packages.md)  
  
  
