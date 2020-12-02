---
description: Guardar un paquete mediante programación
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
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 4ce0606f8d63015be37b5230a47cb66c82cf1a20
ms.sourcegitcommit: c5078791a07330a87a92abb19b791e950672e198
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 11/26/2020
ms.locfileid: "88352111"
---
# <a name="saving-a-package-programmatically"></a>Guardar un paquete mediante programación

[!INCLUDE[sqlserver-ssis](../../includes/applies-to-version/sqlserver-ssis.md)]


  Después de generar un nuevo paquete o modificar uno existente mediante programación, por lo general desea guardar los cambios.  
  
 Todos los métodos utilizados en este tema para guardar paquetes requieren una referencia al ensamblado **Microsoft.SqlServer.ManagedDTS** . Después de agregar la referencia en un proyecto nuevo, importe el espacio de nombres <xref:Microsoft.SqlServer.Dts.Runtime> mediante una instrucción **using** o **Imports**.  
  
## <a name="saving-a-package-programmatically"></a>Guardar un paquete mediante programación  
 Para guardar un paquete mediante programación, llame a uno de los métodos siguientes de la clase de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] <xref:Microsoft.SqlServer.Dts.Runtime.Application>:  
  
|Ubicación de almacenamiento|Método que se llama|  
|----------------------|--------------------|  
|Archivo|<xref:Microsoft.SqlServer.Dts.Runtime.Application.SaveToXml%2A>|  
|Almacén de paquetes SSIS|<xref:Microsoft.SqlServer.Dts.Runtime.Application.SaveToDtsServer%2A>|  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|<xref:Microsoft.SqlServer.Dts.Runtime.Application.SaveToSqlServer%2A><br /><br /> o bien<br /><br /> <xref:Microsoft.SqlServer.Dts.Runtime.Application.SaveToSqlServerAs%2A>|  
  
> [!IMPORTANT]  
>  Los métodos de la clase <xref:Microsoft.SqlServer.Dts.Runtime.Application> para trabajar con el almacén de paquetes SSIS solo admiten "." o el nombre del servidor local. No puede utilizar" "(local)" ni "localhost".  
  
## <a name="see-also"></a>Vea también  
 [Guardar paquetes](../../integration-services/save-packages.md)  
  
  
