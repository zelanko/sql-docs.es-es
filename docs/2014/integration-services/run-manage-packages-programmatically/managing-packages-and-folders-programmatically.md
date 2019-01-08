---
title: Administrar paquetes y carpetas mediante programación | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: reference
helpviewer_keywords:
- enumerators [Integration Services]
- packages [Integration Services], managing
- custom enumerators [Integration Services]
ms.assetid: ec59b75d-ba09-44ac-9039-9d593bb462d9
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: c41f5d59b440fe7b72153076fac5bf794ab6420e
ms.sourcegitcommit: 334cae1925fa5ac6c140e0b2c38c844c477e3ffb
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/13/2018
ms.locfileid: "53362138"
---
# <a name="managing-packages-and-folders-programmatically"></a>Administrar paquetes y carpetas mediante programación
  Cuando trabaja con paquetes [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] mediante programación, puede que desee determinar si existe un paquete o carpeta individual, o administrar las carpetas en las que se almacenan los paquetes. La clase <xref:Microsoft.SqlServer.Dts.Runtime.Application> del espacio de nombres <xref:Microsoft.SqlServer.Dts.Runtime> proporciona diferentes métodos para satisfacer estos requisitos.  
  
##  <a name="exists"></a> Determinar si existe un paquete o una carpeta  
 Para determinar mediante programación si existe un paquete guardado, llame a uno de los métodos siguientes antes de intentar cargar y ejecutar el paquete:  
  
|Ubicación de almacenamiento|Método que se llama|  
|----------------------|--------------------|  
|Almacén de paquetes SSIS|<xref:Microsoft.SqlServer.Dts.Runtime.Application.ExistsOnDtsServer%2A>|  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|<xref:Microsoft.SqlServer.Dts.Runtime.Application.ExistsOnSqlServer%2A>|  
  
 Para determinar mediante programación si existe una carpeta, llame a uno de los siguientes métodos antes de intentar enumerar los paquetes almacenados en la carpeta:  
  
|Ubicación de almacenamiento|Método que se llama|  
|----------------------|--------------------|  
|Almacén de paquetes SSIS|<xref:Microsoft.SqlServer.Dts.Runtime.Application.FolderExistsOnDtsServer%2A>|  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|<xref:Microsoft.SqlServer.Dts.Runtime.Application.FolderExistsOnSqlServer%2A>|  
  

  
##  <a name="managing"></a> Administrar paquetes y carpetas  
 La clase <xref:Microsoft.SqlServer.Dts.Runtime.Application> del espacio de nombres <xref:Microsoft.SqlServer.Dts.Runtime> proporciona métodos adicionales para administrar paquetes y las carpetas en las que están almacenados.  
  
###  <a name="managing_rempkg"></a> Quitar un paquete  
 Para quitar mediante programación un paquete guardado, llame a uno de los métodos siguientes:  
  
|Ubicación de almacenamiento|Método que se llama|  
|----------------------|--------------------|  
|Almacén de paquetes SSIS|<xref:Microsoft.SqlServer.Dts.Runtime.Application.RemoveFromDtsServer%2A>|  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|<xref:Microsoft.SqlServer.Dts.Runtime.Application.RemoveFromSqlServer%2A>|  
  

  
###  <a name="managing_create"></a> Crear una carpeta  
 Para crear mediante programación una carpeta de almacenamiento, llame a uno de los métodos siguientes:  
  
|Ubicación de almacenamiento|Método que se llama|  
|----------------------|--------------------|  
|Almacén de paquetes SSIS|<xref:Microsoft.SqlServer.Dts.Runtime.Application.CreateFolderOnDtsServer%2A>|  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|<xref:Microsoft.SqlServer.Dts.Runtime.Application.CreateFolderOnSqlServer%2A>|  
  

  
###  <a name="managing_remfldr"></a> Quitar una carpeta  
 Para quitar mediante programación una carpeta de almacenamiento, llame a uno de los métodos siguientes:  
  
|Ubicación de almacenamiento|Método que se llama|  
|----------------------|--------------------|  
|Almacén de paquetes SSIS|<xref:Microsoft.SqlServer.Dts.Runtime.Application.RemoveFolderFromDtsServer%2A>|  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|<xref:Microsoft.SqlServer.Dts.Runtime.Application.RemoveFolderFromSqlServer%2A>|  
  
  
  
###  <a name="managing_rename"></a> Cambiar el nombre de una carpeta  
 Para cambiar el nombre de una carpeta de almacenamiento mediante programación, llame a uno de los métodos siguientes:  
  
|Ubicación de almacenamiento|Método que se llama|  
|----------------------|--------------------|  
|Almacén de paquetes SSIS|<xref:Microsoft.SqlServer.Dts.Runtime.Application.RenameFolderOnDtsServer%2A>|  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|<xref:Microsoft.SqlServer.Dts.Runtime.Application.RenameFolderOnSqlServer%2A>|  
  

  
![Icono de Integration Services (pequeño)](../media/dts-16.gif "icono de Integration Services (pequeño)")**mantenerse actualizado con Integration Services**<br /> Para obtener las descargas, artículos, ejemplos y vídeos más recientes de Microsoft, así como soluciones seleccionadas de la comunidad, visite la página de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] en MSDN:<br /><br /> [Visite la página de Integration Services en MSDN](https://go.microsoft.com/fwlink/?LinkId=136655)<br /><br /> Para recibir notificaciones automáticas de estas actualizaciones, suscríbase a las fuentes RSS disponibles en la página.  
  
## <a name="see-also"></a>Vea también  
 [Administración de paquetes &#40;servicio SSIS&#41;](../service/package-management-ssis-service.md)   
 [Enumerar los paquetes disponibles mediante programación](../run-manage-packages-programmatically/enumerating-available-packages-programmatically.md)  
  
  
