---
title: Guardar un paquete mediante programación | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
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
ms.openlocfilehash: 07c926a292c657eecceb13ca1cdc1d3f8dcc5a71
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "65729260"
---
# <a name="saving-a-package-programmatically"></a>Guardar un paquete mediante programación

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  Después de generar un nuevo paquete o modificar uno existente mediante programación, por lo general desea guardar los cambios.  
  
 Todos los métodos utilizados en este tema para guardar paquetes requieren una referencia al ensamblado **Microsoft.SqlServer.ManagedDTS** . Después de agregar la referencia en un proyecto nuevo, importe el espacio de nombres <xref:Microsoft.SqlServer.Dts.Runtime> mediante una instrucción **using** o **Imports**.  
  
## <a name="saving-a-package-programmatically"></a>Guardar un paquete mediante programación  
 Para guardar un paquete mediante programación, llame a uno de los métodos siguientes de la clase de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] <xref:Microsoft.SqlServer.Dts.Runtime.Application>:  
  
|Ubicación de almacenamiento|Método que se llama|  
|----------------------|--------------------|  
|Archivo|<xref:Microsoft.SqlServer.Dts.Runtime.Application.SaveToXml%2A>|  
|Almacén de paquetes SSIS|<xref:Microsoft.SqlServer.Dts.Runtime.Application.SaveToDtsServer%2A>|  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|<xref:Microsoft.SqlServer.Dts.Runtime.Application.SaveToSqlServer%2A><br /><br /> o Administrador de configuración de<br /><br /> <xref:Microsoft.SqlServer.Dts.Runtime.Application.SaveToSqlServerAs%2A>|  
  
> [!IMPORTANT]  
>  Los métodos de la clase <xref:Microsoft.SqlServer.Dts.Runtime.Application> para trabajar con el almacén de paquetes SSIS solo admiten "." o el nombre del servidor local. No puede utilizar" "(local)" ni "localhost".  
  
## <a name="see-also"></a>Consulte también  
 [Guardar paquetes](../../integration-services/save-packages.md)  
  
  
