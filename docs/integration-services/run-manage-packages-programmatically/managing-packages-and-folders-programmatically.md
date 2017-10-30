---
title: "Administrar paquetes y carpetas mediante programación | Documentos de Microsoft"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
helpviewer_keywords:
- enumerators [Integration Services]
- packages [Integration Services], managing
- custom enumerators [Integration Services]
ms.assetid: ec59b75d-ba09-44ac-9039-9d593bb462d9
caps.latest.revision: 33
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: a40acf3a586c74119d948291fd179f78833cb37a
ms.contentlocale: es-es
ms.lasthandoff: 09/26/2017

---
# <a name="managing-packages-and-folders-programmatically"></a>Administrar paquetes y carpetas mediante programación
<a name="top"></a>Cuando se trabaja mediante programación con [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] paquetes, puede que desee para determinar si existe un paquete individual o una carpeta, o para administrar las carpetas en el que se almacenan los paquetes. La clase <xref:Microsoft.SqlServer.Dts.Runtime.Application> del espacio de nombres <xref:Microsoft.SqlServer.Dts.Runtime> proporciona diferentes métodos para satisfacer estos requisitos.    
    
##  <a name="exists"></a>Determinar si existe un paquete o una carpeta    
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
    
 [Volver al principio](#top)    
    
##  <a name="managing"></a>Administrar paquetes y carpetas    
 La clase <xref:Microsoft.SqlServer.Dts.Runtime.Application> del espacio de nombres <xref:Microsoft.SqlServer.Dts.Runtime> proporciona métodos adicionales para administrar paquetes y las carpetas en las que están almacenados.    
    
###  <a name="managing_rempkg"></a>Al quitar un paquete    
 Para quitar mediante programación un paquete guardado, llame a uno de los métodos siguientes:    
    
|Ubicación de almacenamiento|Método que se llama|    
|----------------------|--------------------|    
|Almacén de paquetes SSIS|<xref:Microsoft.SqlServer.Dts.Runtime.Application.RemoveFromDtsServer%2A>|    
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|<xref:Microsoft.SqlServer.Dts.Runtime.Application.RemoveFromSqlServer%2A>|    
    
 [Volver al principio](#top)    
    
###  <a name="managing_create"></a>Crear una carpeta    
 Para crear mediante programación una carpeta de almacenamiento, llame a uno de los métodos siguientes:    
    
|Ubicación de almacenamiento|Método que se llama|    
|----------------------|--------------------|    
|Almacén de paquetes SSIS|<xref:Microsoft.SqlServer.Dts.Runtime.Application.CreateFolderOnDtsServer%2A>|    
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|<xref:Microsoft.SqlServer.Dts.Runtime.Application.CreateFolderOnSqlServer%2A>|    
    
 [Volver al principio](#top)    
    
###  <a name="managing_remfldr"></a>Quitar una carpeta    
 Para quitar mediante programación una carpeta de almacenamiento, llame a uno de los métodos siguientes:    
    
|Ubicación de almacenamiento|Método que se llama|    
|----------------------|--------------------|    
|Almacén de paquetes SSIS|<xref:Microsoft.SqlServer.Dts.Runtime.Application.RemoveFolderFromDtsServer%2A>|    
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|<xref:Microsoft.SqlServer.Dts.Runtime.Application.RemoveFolderFromSqlServer%2A>|    
    
 [Volver al principio](#top)    
    
###  <a name="managing_rename"></a>Cambiar el nombre de una carpeta    
 Para cambiar el nombre de una carpeta de almacenamiento mediante programación, llame a uno de los métodos siguientes:    
    
|Ubicación de almacenamiento|Método que se llama|    
|----------------------|--------------------|    
|Almacén de paquetes SSIS|<xref:Microsoft.SqlServer.Dts.Runtime.Application.RenameFolderOnDtsServer%2A>|    
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|<xref:Microsoft.SqlServer.Dts.Runtime.Application.RenameFolderOnSqlServer%2A>|    
    
 [Volver al principio](#top)    
    
## <a name="see-also"></a>Vea también    
 [Administración de paquetes &#40; Servicio SSIS &#41;](../../integration-services/service/package-management-ssis-service.md)     
 [Enumerar los paquetes disponibles mediante programación](../../integration-services/run-manage-packages-programmatically/enumerating-available-packages-programmatically.md)    
    
  

